<!-- markdownlint-disable MD002 MD041 -->

在此练习中，你将扩展上一练习中的应用程序，以支持使用 Azure AD 进行身份验证。 这是获取调用 Microsoft Graph 所需的 OAuth 访问令牌所必需的。 为此，你将 Microsoft 身份验证库 [ (MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-android)) Android 集成到应用程序中。

1. 右键单击 **res** 文件夹，然后选择 **"新建**"，然后选择 **"Android 资源目录"。**

1. 将资源 **类型更改为并选择** `raw` "**确定"。**

1. 右键单击新的 **原始** 文件夹，然后选择 **"新建**"，然后选择"**文件"。**

1. 命名文件 `msal_config.json` ，然后选择"**确定"。**

1. 将以下内容添加到文件msal_config.js **文件** 。

    :::code language="json" source="../demo/GraphTutorial/msal_config.json.example":::

1. 替换为 `YOUR_APP_ID_HERE` 应用注册的应用 ID，并替换为 `com.example.graphtutorial` 项目的程序包名称。

    > [!IMPORTANT]
    > 如果你使用的是源代码管理（如 git），那么现在应该将文件从源代码管理中排除，以避免意外泄露 `msal_config.json` 应用 ID。

## <a name="implement-sign-in"></a>实现登录

在此部分中，你将更新清单以允许 MSAL 使用浏览器对用户进行身份验证、将重定向 URI 注册为由应用处理、创建身份验证帮助程序类，以及更新应用以登录和注销。

1. 展开 **应用/清单** 文件夹 **并打开** AndroidManifest.xml。 在元素上方添加以下 `application` 元素。

    ```xml
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    ```

    > [!NOTE]
    > MSAL 库需要这些权限才能对用户进行身份验证。

1. 在元素中添加以下元素， `application` 将 `YOUR_PACKAGE_NAME_HERE` 字符串替换为程序包名称。

    ```xml
    <!--Intent filter to capture authorization code response from the default browser on the
        device calling back to the app after interactive sign in -->
    <activity
        android:name="com.microsoft.identity.client.BrowserTabActivity">
        <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data
                android:scheme="msauth"
                android:host="YOUR_PACKAGE_NAME_HERE"
                android:path="/callback" />
        </intent-filter>
    </activity>
    ```

1. 右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。 将 **类型更改为****接口**。 命名接口 `IAuthenticationHelperCreatedListener` ，然后选择"**确定"。**

1. 打开新文件，并将其内容替换为以下内容。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/IAuthenticationHelperCreatedListener.java" id="ListenerSnippet":::

1. 右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。 命名类 `AuthenticationHelper` ，然后选择"**确定"。**

1. 打开新文件，并将其内容替换为以下内容。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/AuthenticationHelper.java" id="AuthHelperSnippet":::

1. 打开 **MainActivity** 并添加以下 `import` 语句。

    ```java
    import android.util.Log;

    import com.microsoft.identity.client.AuthenticationCallback;
    import com.microsoft.identity.client.IAuthenticationResult;
    import com.microsoft.identity.client.exception.MsalClientException;
    import com.microsoft.identity.client.exception.MsalException;
    import com.microsoft.identity.client.exception.MsalServiceException;
    import com.microsoft.identity.client.exception.MsalUiRequiredException;
    ```

1. 将以下成员属性添加到 `MainActivity` 类。

    ```java
    private AuthenticationHelper mAuthHelper = null;
    private boolean mAttemptInteractiveSignIn = false;
    ```

1. 将以下代码添加到`onCreate` 函数末尾。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/MainActivity.java" id="InitialLoginSnippet":::

1. 将以下函数添加到 `MainActivity` 类。

    ```java
    // Silently sign in - used if there is already a
    // user account in the MSAL cache
    private void doSilentSignIn(boolean shouldAttemptInteractive) {
        mAttemptInteractiveSignIn = shouldAttemptInteractive;
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
            public void onSuccess(IAuthenticationResult authenticationResult) {
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
                    if (mAttemptInteractiveSignIn) {
                        doInteractiveSignIn();
                    }
                } else if (exception instanceof MsalClientException) {
                    if (exception.getErrorCode() == "no_current_account" ||
                        exception.getErrorCode() == "no_account_found") {
                        Log.d("AUTH", "No current account, interactive login required");
                        if (mAttemptInteractiveSignIn) {
                            doInteractiveSignIn();
                        }
                    } else {
                        // Exception inside MSAL, more info inside MsalError.java
                        Log.e("AUTH", "Client error authenticating", exception);
                    }
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

1. 将现有 `signIn` 函数 `signOut` 和函数替换为以下内容。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/MainActivity.java" id="SignInAndOutSnippet":::

    > [!NOTE]
    > 请注意， `signIn` 此方法通过 (执行无提示 `doSilentSignIn`) 。 如果无提示登录失败，此方法的回调将执行交互式登录。 这样可以避免每次用户启动应用时提示用户。

1. 保存更改并运行该应用程序。

1. 点击"登录 **"** 菜单项时，浏览器将打开至 Azure AD 登录页。 使用你的帐户登录。

应用恢复后，你应该会看到访问令牌在 Android Studio 的调试日志中打印。

![Android Studio 中的 Logcat 窗口屏幕截图](./images/debugger-access-token.png)

## <a name="get-user-details"></a>获取用户详细信息

在此部分中，你将创建一个帮助程序类来保存对 Microsoft Graph 的所有调用，并更新该类以使用此新类获取 `MainActivity` 登录用户。

1. 右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。 命名类 `GraphHelper` ，然后选择"**确定"。**

1. 打开新文件，并将其内容替换为以下内容。

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
            mClient.me().buildRequest()
                    .select("displayName,mail,mailboxSettings,userPrincipalName")
                    .get(callback);
        }
    }
    ```

    > [!NOTE]
    > 考虑此代码执行哪些功能。
    >
    > - 它实现接口 `IAuthenticationProvider` 以在传出 HTTP 请求的 `Authorization` 标头中插入访问令牌。
    > - 它公开 `getUser` 了一个函数，用于从 Graph 终结点获取已登录 `/me` 用户的信息。

1. 将以下 `import` 语句添加到 **MainActivity** 文件的顶部。

    ```java
    import com.microsoft.graph.concurrency.ICallback;
    import com.microsoft.graph.core.ClientException;
    import com.microsoft.graph.models.extensions.User;
    ```

1. 将以下函数添加到 `MainActivity` 类以生成 Graph `ICallback` 调用。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/MainActivity.java" id="GetUserCallbackSnippet":::

1. 删除以下用于设置用户名和电子邮件的行：

    ```java
    // For testing
    mUserName = "Megan Bowen";
    mUserEmail = "meganb@contoso.com";
    ```

1. 将 `onSuccess` 以下替代 `AuthenticationCallback` 项替换为以下内容。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/MainActivity.java" id="OnSuccessSnippet":::

1. 保存更改并运行该应用程序。 登录 UI 后，会使用用户的 显示名称 和电子邮件地址进行更新。
