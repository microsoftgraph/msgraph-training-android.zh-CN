<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ed298-101">在本练习中, 你将扩展上一练习中的应用程序, 以支持 Azure AD 的身份验证。</span><span class="sxs-lookup"><span data-stu-id="ed298-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="ed298-102">若要获取所需的 OAuth 访问令牌以调用 Microsoft Graph, 这是必需的。</span><span class="sxs-lookup"><span data-stu-id="ed298-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="ed298-103">在此步骤中, 您会将[适用于 Android 的 Microsoft 身份验证库 (MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-android)集成到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="ed298-103">In this step you will integrate the [Microsoft Authentication Library (MSAL) for Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) into the application.</span></span>

<span data-ttu-id="ed298-104">右键单击 " **app/res/values** " 文件夹, 然后选择 "**新建**", 然后选择 "**值资源文件**"。</span><span class="sxs-lookup"><span data-stu-id="ed298-104">Right-click the **app/res/values** folder and choose **New**, then **Values resource file**.</span></span> <span data-ttu-id="ed298-105">命名该文件`oauth_strings` , 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="ed298-105">Name the file `oauth_strings` and choose **OK**.</span></span> <span data-ttu-id="ed298-106">将以下值添加到`resources`元素中。</span><span class="sxs-lookup"><span data-stu-id="ed298-106">Add the following values to the `resources` element.</span></span>

```xml
<string name="oauth_app_id">YOUR_APP_ID_HERE</string>
<string name="oauth_redirect_uri">msalYOUR_APP_ID_HERE</string>
<string-array name="oauth_scopes">
    <item>User.Read</item>
    <item>Calendars.Read</item>
</string-array>
```

> [!IMPORTANT]
> <span data-ttu-id="ed298-107">如果您使用的是源代码管理 (如 git), 现在可以从源代码管理中排除`oauth_strings.xml`该文件, 以避免无意中泄漏您的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="ed298-107">If you're using source control such as git, now would be a good time to exclude the `oauth_strings.xml` file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="ed298-108">实施登录</span><span class="sxs-lookup"><span data-stu-id="ed298-108">Implement sign-in</span></span>

<span data-ttu-id="ed298-109">展开 "**应用/清单**" 文件夹, 然后打开 " **androidmanifest.xml**"。</span><span class="sxs-lookup"><span data-stu-id="ed298-109">Expand the **app/manifests** folder and open **AndroidManifest.xml**.</span></span> <span data-ttu-id="ed298-110">将以下元素添加到`application`元素上方。</span><span class="sxs-lookup"><span data-stu-id="ed298-110">Add the following elements above the `application` element.</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

<span data-ttu-id="ed298-111">为了使 MSAL 库对用户进行身份验证, 需要这些权限。</span><span class="sxs-lookup"><span data-stu-id="ed298-111">These permissions are required in order for the MSAL library to authenticate the user.</span></span>

<span data-ttu-id="ed298-112">现在, 在`application`元素中添加以下元素。</span><span class="sxs-lookup"><span data-stu-id="ed298-112">Now add the following element inside the `application` element.</span></span>

```xml
<activity android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />

        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <data
            android:host="auth"
            android:scheme="@string/oauth_redirect_uri" />
    </intent-filter>
</activity>
```

<span data-ttu-id="ed298-113">这样, MSAL 可以使用浏览器对用户进行身份验证, 并将重定向 URI 注册为应用程序处理的。</span><span class="sxs-lookup"><span data-stu-id="ed298-113">This allows MSAL to use a browser to authenticate the user, and registers your redirect URI as being handled by the app.</span></span>

### <a name="implement-an-authentication-helper"></a><span data-ttu-id="ed298-114">实现身份验证帮助程序</span><span class="sxs-lookup"><span data-stu-id="ed298-114">Implement an authentication helper</span></span>

<span data-ttu-id="ed298-115">右键单击**app/java/.com graphtutorial**文件夹, 然后依次选择 "**新建**"、" **java 类**"。</span><span class="sxs-lookup"><span data-stu-id="ed298-115">Right-click the **app/java/com.example.graphtutorial** folder and choose **New**, then **Java Class**.</span></span> <span data-ttu-id="ed298-116">命名该类`AuthenticationHelper`并选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="ed298-116">Name the class `AuthenticationHelper` and choose **OK**.</span></span> <span data-ttu-id="ed298-117">打开新文件, 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ed298-117">Open the new file and replace its contents with the following.</span></span>

```java
package com.example.graphtutorial;

import android.app.Activity;
import android.content.Context;
import android.content.Intent;

import com.microsoft.identity.client.AuthenticationCallback;
import com.microsoft.identity.client.IAccount;
import com.microsoft.identity.client.PublicClientApplication;

// Singleton class - the app only needs a single instance
// of PublicClientApplication
public class AuthenticationHelper {
    private static AuthenticationHelper INSTANCE = null;
    private PublicClientApplication mPCA = null;
    private String[] mScopes;

    private AuthenticationHelper(Context ctx) {
        String appId = ctx.getResources().getString(R.string.oauth_app_id);
        mScopes = ctx.getResources().getStringArray(R.array.oauth_scopes);
        mPCA = new PublicClientApplication(ctx, appId);
    }

    public static synchronized AuthenticationHelper getInstance(Context ctx) {
        if (INSTANCE == null) {
            INSTANCE = new AuthenticationHelper(ctx);
        }

        return INSTANCE;
    }

    // Version called from fragments. Does not create an
    // instance if one doesn't exist
    public static synchronized AuthenticationHelper getInstance() {
        if (INSTANCE == null) {
            throw new IllegalStateException(
                    "AuthenticationHelper has not been initialized from MainActivity");
        }

        return INSTANCE;
    }

    public boolean hasAccount() {
        return !mPCA.getAccounts().isEmpty();
    }

    public void handleRedirect(int requestCode, int resultCode, Intent data) {
        mPCA.handleInteractiveRequestRedirect(requestCode, resultCode, data);
    }

    public void acquireTokenInteractively(Activity activity, AuthenticationCallback callback) {
        mPCA.acquireToken(activity, mScopes, callback);
    }

    public void acquireTokenSilently(AuthenticationCallback callback) {
        mPCA.acquireTokenSilentAsync(mScopes, mPCA.getAccounts().get(0), callback);
    }

    public void signOut() {
        for (IAccount account : mPCA.getAccounts()) {
            mPCA.removeAccount(account);
        }
    }
}
```

<span data-ttu-id="ed298-118">现在, `MainActivity`更新以使用此新类。</span><span class="sxs-lookup"><span data-stu-id="ed298-118">Now update `MainActivity` to use this new class.</span></span> <span data-ttu-id="ed298-119">打开**MainActivity** , 并添加以下`import`语句。</span><span class="sxs-lookup"><span data-stu-id="ed298-119">Open **MainActivity** and add the following `import` statements.</span></span>

```java
import android.content.Intent;
import android.support.annotation.Nullable;
import android.util.Log;

import com.microsoft.identity.client.AuthenticationCallback;
import com.microsoft.identity.client.AuthenticationResult;
import com.microsoft.identity.client.exception.MsalClientException;
import com.microsoft.identity.client.exception.MsalException;
import com.microsoft.identity.client.exception.MsalServiceException;
import com.microsoft.identity.client.exception.MsalUiRequiredException;
```

<span data-ttu-id="ed298-120">接下来, 将以下成员属性添加到`MainActivity`类中。</span><span class="sxs-lookup"><span data-stu-id="ed298-120">Next, add the following member property to the `MainActivity` class.</span></span>

```java
private AuthenticationHelper mAuthHelper = null;
```

<span data-ttu-id="ed298-121">更新`onCreate`以进行`mAuthHelper`设置。</span><span class="sxs-lookup"><span data-stu-id="ed298-121">Update `onCreate` to set `mAuthHelper`.</span></span> <span data-ttu-id="ed298-122">将以下项添加到`onCreate`函数的末尾。</span><span class="sxs-lookup"><span data-stu-id="ed298-122">Add the following to the end of the `onCreate` function.</span></span>

```java
// Get the authentication helper
mAuthHelper = AuthenticationHelper.getInstance(getApplicationContext());
```

<span data-ttu-id="ed298-123">添加用于处理身份`onActivityResult`验证响应的替代。</span><span class="sxs-lookup"><span data-stu-id="ed298-123">Add an override for `onActivityResult` to handle authentication responses.</span></span>

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    mAuthHelper.handleRedirect(requestCode, resultCode, data);
}
```

<span data-ttu-id="ed298-124">现在, 将以下函数添加到`MainActivity`类中。</span><span class="sxs-lookup"><span data-stu-id="ed298-124">Now, add the following functions to the `MainActivity` class.</span></span>

```java
// Silently sign in - used if there is already a
// user account in the MSAL cache
private void doSilentSignIn() {
    mAuthHelper.acquireTokenSilently(getAuthCallback());
}

// Prompt the user to sign in
private void doInteractiveSignIn() {
    mAuthHelper.acquireTokenInteractively(this, getAuthCallback());
}

// Handles the authentication result
public AuthenticationCallback getAuthCallback() {
    return new AuthenticationCallback() {

        @Override
        public void onSuccess(AuthenticationResult authenticationResult) {
            // Log the token for debug purposes
            String accessToken = authenticationResult.getAccessToken();
            Log.d("AUTH", String.format("Access token: %s", accessToken));
            hideProgressBar();

            setSignedInState(true);
            openHomeFragment(mUserName);
        }

        @Override
        public void onError(MsalException exception) {
            // Check the type of exception and handle appropriately
            if (exception instanceof MsalUiRequiredException) {
                Log.d("AUTH", "Interactive login required");
                doInteractiveSignIn();

            } else if (exception instanceof MsalClientException) {
                // Exception inside MSAL, more info inside MsalError.java
                Log.e("AUTH", "Client error authenticating", exception);
            } else if (exception instanceof MsalServiceException) {
                // Exception when communicating with the auth server, likely config issue
                Log.e("AUTH", "Service error authenticating", exception);
            }
            hideProgressBar();
        }

        @Override
        public void onCancel() {
            // User canceled the authentication
            Log.d("AUTH", "Authentication canceled");
            hideProgressBar();
        }
    };
}
```

<span data-ttu-id="ed298-125">最后, 将现有`signIn`和`signOut`函数替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="ed298-125">Finally, replace the existing `signIn` and `signOut` functions with the following.</span></span>

```java
private void signIn() {
    showProgressBar();
    if (mAuthHelper.hasAccount()) {
        doSilentSignIn();
    } else {
        doInteractiveSignIn();
    }
}

private void signOut() {
    mAuthHelper.signOut();

    setSignedInState(false);
    openHomeFragment(mUserName);
}
```

<span data-ttu-id="ed298-126">请注意, `signIn`该方法首先检查 MSAL 缓存中是否已有用户帐户。</span><span class="sxs-lookup"><span data-stu-id="ed298-126">Notice that the `signIn` method first checks if there is a user account already in the MSAL cache.</span></span> <span data-ttu-id="ed298-127">如果有, 它会尝试以静默方式刷新其令牌, 从而避免在每次启动应用程序时提示用户。</span><span class="sxs-lookup"><span data-stu-id="ed298-127">If there is, it attempts to refresh its tokens silently, avoiding having to prompt the user every time they launch the app.</span></span>

<span data-ttu-id="ed298-128">保存更改并运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="ed298-128">Save your changes and run the app.</span></span> <span data-ttu-id="ed298-129">点击 "**登录**" 菜单项时, 会打开 "Azure AD 登录" 页的浏览器。</span><span class="sxs-lookup"><span data-stu-id="ed298-129">When you tap the **Sign in** menu item, a browser opens to the Azure AD login page.</span></span> <span data-ttu-id="ed298-130">使用你的帐户登录。</span><span class="sxs-lookup"><span data-stu-id="ed298-130">Sign in with your account.</span></span> <span data-ttu-id="ed298-131">在应用程序恢复后, 您应该会看到在 Android Studio 的调试日志中打印的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="ed298-131">Once the app resumes, you should see an access token printed in the debug log in Android Studio.</span></span>

![Android Studio 中的 Logcat 窗口的屏幕截图](./images/debugger-access-token.png)

## <a name="get-user-details"></a><span data-ttu-id="ed298-133">获取用户详细信息</span><span class="sxs-lookup"><span data-stu-id="ed298-133">Get user details</span></span>

<span data-ttu-id="ed298-134">首先, 创建帮助程序类以保存对 Microsoft Graph 的所有调用。</span><span class="sxs-lookup"><span data-stu-id="ed298-134">Start by creating a helper class to hold all of the calls to Microsoft Graph.</span></span> <span data-ttu-id="ed298-135">右键单击**app/java/.com graphtutorial**文件夹, 然后依次选择 "**新建**"、" **java 类**"。</span><span class="sxs-lookup"><span data-stu-id="ed298-135">Right-click the **app/java/com.example.graphtutorial** folder and choose **New**, then **Java Class**.</span></span> <span data-ttu-id="ed298-136">命名该类`GraphHelper`并选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="ed298-136">Name the class `GraphHelper` and choose **OK**.</span></span> <span data-ttu-id="ed298-137">打开新文件, 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ed298-137">Open the new file and replace its contents with the following.</span></span>

```java
package com.example.graphtutorial;

import com.microsoft.graph.authentication.IAuthenticationProvider;
import com.microsoft.graph.concurrency.ICallback;
import com.microsoft.graph.http.IHttpRequest;
import com.microsoft.graph.models.extensions.IGraphServiceClient;
import com.microsoft.graph.models.extensions.User;
import com.microsoft.graph.requests.extensions.GraphServiceClient;

// Singleton class - the app only needs a single instance
// of the Graph client
public class GraphHelper implements IAuthenticationProvider {
    private static GraphHelper INSTANCE = null;
    private IGraphServiceClient mClient = null;
    private String mAccessToken = null;

    private GraphHelper() {
        mClient = GraphServiceClient.builder()
                .authenticationProvider(this).buildClient();
    }

    public static synchronized GraphHelper getInstance() {
        if (INSTANCE == null) {
            INSTANCE = new GraphHelper();
        }

        return INSTANCE;
    }

    // Part of the Graph IAuthenticationProvider interface
    // This method is called before sending the HTTP request
    @Override
    public void authenticateRequest(IHttpRequest request) {
        // Add the access token in the Authorization header
        request.addHeader("Authorization", "Bearer " + mAccessToken);
    }

    public void getUser(String accessToken, ICallback<User> callback) {
        mAccessToken = accessToken;

        // GET /me (logged in user)
        mClient.me().buildRequest().get(callback);
    }
}
```

<span data-ttu-id="ed298-138">请注意此代码执行的操作。</span><span class="sxs-lookup"><span data-stu-id="ed298-138">Note what this code does.</span></span>

- <span data-ttu-id="ed298-139">它实现`IAuthenticationProvider`接口以在传出 HTTP 请求的`Authorization`标头中插入访问令牌。</span><span class="sxs-lookup"><span data-stu-id="ed298-139">It implements the `IAuthenticationProvider` interface to insert the access token in the `Authorization` header on outgoing HTTP requests.</span></span>
- <span data-ttu-id="ed298-140">它公开了`getUser`一个函数, 用于从`/me` Graph 终结点获取已登录用户的信息。</span><span class="sxs-lookup"><span data-stu-id="ed298-140">It exposes a `getUser` function to get the logged-in user's information from the `/me` Graph endpoint.</span></span>

<span data-ttu-id="ed298-141">现在, 将`MainActivity`类更新为使用此新类获取已登录用户。</span><span class="sxs-lookup"><span data-stu-id="ed298-141">Now update the `MainActivity` class to use this new class to get the logged-in user.</span></span> <span data-ttu-id="ed298-142">将以下`import`语句添加到**MainActivity**文件的顶部。</span><span class="sxs-lookup"><span data-stu-id="ed298-142">Add the following `import` statements to the top of the **MainActivity** file.</span></span>

```java
import com.microsoft.graph.concurrency.ICallback;
import com.microsoft.graph.core.ClientException;
import com.microsoft.graph.models.extensions.IGraphServiceClient;
import com.microsoft.graph.models.extensions.User;
```

<span data-ttu-id="ed298-143">接下来, 将以下函数添加到`MainActivity`类中, 以`ICallback`生成用于图形调用的。</span><span class="sxs-lookup"><span data-stu-id="ed298-143">Next, add the following function to the `MainActivity` class to generate an `ICallback` for the Graph call.</span></span>

```java
private ICallback<User> getUserCallback() {
    return new ICallback<User>() {
        @Override
        public void success(User user) {
            Log.d("AUTH", "User: " + user.displayName);

            mUserName = user.displayName;
            mUserEmail = user.mail == null ? user.userPrincipalName : user.mail;

            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    hideProgressBar();

                    setSignedInState(true);
                    openHomeFragment(mUserName);
                }
            });

        }

        @Override
        public void failure(ClientException ex) {
            Log.e("AUTH", "Error getting /me", ex);
            mUserName = "ERROR";
            mUserEmail = "ERROR";

            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    hideProgressBar();

                    setSignedInState(true);
                    openHomeFragment(mUserName);
                }
            });
        }
    };
}
```

<span data-ttu-id="ed298-144">删除设置用户名和电子邮件的以下行:</span><span class="sxs-lookup"><span data-stu-id="ed298-144">Remove the following lines that set the user name and email:</span></span>

```java
// For testing
mUserName = "Megan Bowen";
mUserEmail = "meganb@contoso.com";
```

<span data-ttu-id="ed298-145">最后, 将`AuthenticationCallback`中`onSuccess`的替代替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="ed298-145">Finally, replace the `onSuccess` override in the `AuthenticationCallback` with the following.</span></span>

```java
@Override
public void onSuccess(AuthenticationResult authenticationResult) {
    // Log the token for debug purposes
    String accessToken = authenticationResult.getAccessToken();
    Log.d("AUTH", String.format("Access token: %s", accessToken));

    // Get Graph client and get user
    GraphHelper graphHelper = GraphHelper.getInstance();
    graphHelper.getUser(accessToken, getUserCallback());
}
```

<span data-ttu-id="ed298-146">如果您现在保存更改并运行应用程序, 则在使用用户的显示名称和电子邮件地址更新 UI 后, 登录 UI。</span><span class="sxs-lookup"><span data-stu-id="ed298-146">If you save your changes and run the app now, after sign-in the UI is updated with the user's display name and email address.</span></span>
