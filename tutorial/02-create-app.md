<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="d46e8-101">首先创建新的 Android Studio 项目。</span><span class="sxs-lookup"><span data-stu-id="d46e8-101">Begin by creating a new Android Studio project.</span></span>

1. <span data-ttu-id="d46e8-102">打开 Android Studio，然后选择 **在欢迎** 屏幕上启动新的 Android Studio 项目。</span><span class="sxs-lookup"><span data-stu-id="d46e8-102">Open Android Studio, and select **Start a new Android Studio project** on the welcome screen.</span></span>

1. <span data-ttu-id="d46e8-103">在"**新建项目"对话框中**，选择 **"空活动"，** 然后选择"下 **一步"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-103">In the **Create New Project** dialog, select **Empty Activity**, then select **Next**.</span></span>

    ![Android Studio 中"新建项目"对话框的屏幕截图](./images/choose-project.png)

1. <span data-ttu-id="d46e8-105">在 **"配置项目"对话框中**，将"名称"设置为，确保"语言"字段设置为，并确保 `Graph Tutorial`  `Java` **将"最低 API"** 级别设置为 `API 29: Android 10.0 (Q)` 。</span><span class="sxs-lookup"><span data-stu-id="d46e8-105">In the **Configure your project** dialog, set the **Name** to `Graph Tutorial`, ensure the **Language** field is set to `Java`, and ensure the **Minimum API level** is set to `API 29: Android 10.0 (Q)`.</span></span> <span data-ttu-id="d46e8-106">根据需要 **修改程序包名称和\*\*\*\*保存** 位置。</span><span class="sxs-lookup"><span data-stu-id="d46e8-106">Modify the **Package name** and **Save location** as needed.</span></span> <span data-ttu-id="d46e8-107">选择“完成”。</span><span class="sxs-lookup"><span data-stu-id="d46e8-107">Select **Finish**.</span></span>

    !["配置项目"对话框的屏幕截图](./images/configure-project.png)

> [!IMPORTANT]
> <span data-ttu-id="d46e8-109">本教程中的代码和说明使用程序包名称 **com.example.graphtu一l。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-109">The code and instructions in this tutorial use the package name **com.example.graphtutorial**.</span></span> <span data-ttu-id="d46e8-110">如果在创建项目时使用不同的程序包名称，请务必在看到此值时使用程序包名称。</span><span class="sxs-lookup"><span data-stu-id="d46e8-110">If you use a different package name when creating the project, be sure to use your package name wherever you see this value.</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="d46e8-111">安装依赖项</span><span class="sxs-lookup"><span data-stu-id="d46e8-111">Install dependencies</span></span>

<span data-ttu-id="d46e8-112">在继续之前，请安装一些稍后将使用的其他依赖项。</span><span class="sxs-lookup"><span data-stu-id="d46e8-112">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="d46e8-113">`com.google.android.material:material` 使 [导航视图](https://material.io/develop/android/components/navigation-view/) 对应用可用。</span><span class="sxs-lookup"><span data-stu-id="d46e8-113">`com.google.android.material:material` to make the [navigation view](https://material.io/develop/android/components/navigation-view/) available to the app.</span></span>
- <span data-ttu-id="d46e8-114">[Microsoft 身份验证库 (MSAL) For Android，](https://github.com/AzureAD/microsoft-authentication-library-for-android) 用于处理 Azure AD 身份验证和令牌管理。</span><span class="sxs-lookup"><span data-stu-id="d46e8-114">[Microsoft Authentication Library (MSAL) for Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) to handle Azure AD authentication and token management.</span></span>
- <span data-ttu-id="d46e8-115">[用于调用Java](https://github.com/microsoftgraph/msgraph-sdk-java) Microsoft Graph 的 Microsoft Graph SDK。</span><span class="sxs-lookup"><span data-stu-id="d46e8-115">[Microsoft Graph SDK for Java](https://github.com/microsoftgraph/msgraph-sdk-java) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="d46e8-116">展开 **Gradle 脚本**，然后打开 **build.gradle (模块：Graph_Tutorial.app) 。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-116">Expand **Gradle Scripts**, then open **build.gradle (Module: Graph_Tutorial.app)**.</span></span>

1. <span data-ttu-id="d46e8-117">在值中添加以下 `dependencies` 行。</span><span class="sxs-lookup"><span data-stu-id="d46e8-117">Add the following lines inside the `dependencies` value.</span></span>

    :::code language="gradle" source="../demo/GraphTutorial/app/build.gradle" id="DependenciesSnippet":::

1. <span data-ttu-id="d46e8-118">在 `packagingOptions` build.gradle (模块中的值内添加一 `android` **个值：Graph_Tutorial.app) 。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-118">Add a `packagingOptions` value inside the `android` value in **build.gradle (Module: Graph_Tutorial.app)**.</span></span>

    ```Gradle
    packagingOptions {
        pickFirst 'META-INF/jersey-module-version'
    }
    ```

1. <span data-ttu-id="d46e8-119">为 MicrosoftDeviceSDK 库添加 Azure Maven 存储库，这是 MSAL 的依赖项。</span><span class="sxs-lookup"><span data-stu-id="d46e8-119">Add the Azure Maven repository for the MicrosoftDeviceSDK library, a dependency of MSAL.</span></span> <span data-ttu-id="d46e8-120">打开 **build.gradle (项目：Graph_Tutorial)**。</span><span class="sxs-lookup"><span data-stu-id="d46e8-120">Open **build.gradle (Project: Graph_Tutorial)**.</span></span> <span data-ttu-id="d46e8-121">将以下内容添加到 `repositories` 值中的 `allprojects` 值中。</span><span class="sxs-lookup"><span data-stu-id="d46e8-121">Add the following to the `repositories` value inside the `allprojects` value.</span></span>

    ```Gradle
    maven {
        url 'https://pkgs.dev.azure.com/MicrosoftDeviceSDK/DuoSDK-Public/_packaging/Duo-SDK-Feed/maven/v1'
    }
    ```

1. <span data-ttu-id="d46e8-122">保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="d46e8-122">Save your changes.</span></span> <span data-ttu-id="d46e8-123">在"**文件"** 菜单上，选择 **"使用 Gradle 文件同步项目"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-123">On the **File** menu, select **Sync Project with Gradle Files**.</span></span>

## <a name="design-the-app"></a><span data-ttu-id="d46e8-124">设计应用</span><span class="sxs-lookup"><span data-stu-id="d46e8-124">Design the app</span></span>

<span data-ttu-id="d46e8-125">应用程序将使用导航箱在不同视图之间导航。</span><span class="sxs-lookup"><span data-stu-id="d46e8-125">The application will use a navigation drawer to navigate between different views.</span></span> <span data-ttu-id="d46e8-126">在此步骤中，您将更新活动以使用导航箱布局，并添加视图的片段。</span><span class="sxs-lookup"><span data-stu-id="d46e8-126">In this step you will update the activity to use a navigation drawer layout, and add fragments for the views.</span></span>

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="d46e8-127">创建导航箱</span><span class="sxs-lookup"><span data-stu-id="d46e8-127">Create a navigation drawer</span></span>

<span data-ttu-id="d46e8-128">在此部分中，你将为应用的导航菜单创建图标，为应用程序创建菜单，并更新应用程序的主题和布局，以与导航箱兼容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-128">In this section you will create icons for the app's navigation menu, create a menu for the application, and update the application's theme and layout to be compatible with a navigation drawer.</span></span>

#### <a name="create-icons"></a><span data-ttu-id="d46e8-129">创建图标</span><span class="sxs-lookup"><span data-stu-id="d46e8-129">Create icons</span></span>

1. <span data-ttu-id="d46e8-130">右键单击 **应用/res/drawable** 文件夹，然后选择 **"新建**"，然后选择 **"矢量资源"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-130">Right-click the **app/res/drawable** folder and select **New**, then **Vector Asset**.</span></span>

1. <span data-ttu-id="d46e8-131">单击剪贴画旁边的 **图标按钮**。</span><span class="sxs-lookup"><span data-stu-id="d46e8-131">Click the icon button next to **Clip Art**.</span></span>

1. <span data-ttu-id="d46e8-132">在 **"选择图标**"窗口中，在搜索栏中键入，然后选择"主页 `home` "图标并选择 **"确定"。** </span><span class="sxs-lookup"><span data-stu-id="d46e8-132">In the **Select Icon** window, type `home` in the search bar, then select the **Home** icon and select **OK**.</span></span>

1. <span data-ttu-id="d46e8-133">将 **名称更改为** `ic_menu_home` 。</span><span class="sxs-lookup"><span data-stu-id="d46e8-133">Change the **Name** to `ic_menu_home`.</span></span>

    !["配置矢量资源"窗口的屏幕截图](./images/create-icon.png)

1. <span data-ttu-id="d46e8-135">选择 **"下一** 步"，然后选择"**完成"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-135">Select **Next**, then **Finish**.</span></span>

1. <span data-ttu-id="d46e8-136">重复上一步，再创建四个图标。</span><span class="sxs-lookup"><span data-stu-id="d46e8-136">Repeat the previous step to create four more icons.</span></span>

    - <span data-ttu-id="d46e8-137">名称 `ic_menu_calendar` ：，图标： `event`</span><span class="sxs-lookup"><span data-stu-id="d46e8-137">Name: `ic_menu_calendar`, Icon: `event`</span></span>
    - <span data-ttu-id="d46e8-138">名称 `ic_menu_add_event` ：，图标： `add box`</span><span class="sxs-lookup"><span data-stu-id="d46e8-138">Name: `ic_menu_add_event`, Icon: `add box`</span></span>
    - <span data-ttu-id="d46e8-139">名称 `ic_menu_signout` ：，图标： `exit to app`</span><span class="sxs-lookup"><span data-stu-id="d46e8-139">Name: `ic_menu_signout`, Icon: `exit to app`</span></span>
    - <span data-ttu-id="d46e8-140">名称 `ic_menu_signin` ：，图标： `person add`</span><span class="sxs-lookup"><span data-stu-id="d46e8-140">Name: `ic_menu_signin`, Icon: `person add`</span></span>

#### <a name="create-the-menu"></a><span data-ttu-id="d46e8-141">创建菜单</span><span class="sxs-lookup"><span data-stu-id="d46e8-141">Create the menu</span></span>

1. <span data-ttu-id="d46e8-142">右键单击 **res** 文件夹，然后选择 **"新建**"，然后选择 **"Android 资源目录"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-142">Right-click the **res** folder and select **New**, then **Android Resource Directory**.</span></span>

1. <span data-ttu-id="d46e8-143">将资源 **类型更改为并选择** `menu` "**确定"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-143">Change the **Resource type** to `menu` and select **OK**.</span></span>

1. <span data-ttu-id="d46e8-144">右键单击新 **菜单** 文件夹，然后选择 **"新建**"，然后选择 **"菜单资源文件"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-144">Right-click the new **menu** folder and select **New**, then **Menu resource file**.</span></span>

1. <span data-ttu-id="d46e8-145">命名文件 `drawer_menu` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-145">Name the file `drawer_menu` and select **OK**.</span></span>

1. <span data-ttu-id="d46e8-146">文件打开后，选择"代码 **"选项卡以查看** XML，然后将整个内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-146">When the file opens, select the **Code** tab to view the XML, then replace the entire contents with the following.</span></span>

    :::code language="xml" source="../demo/GraphTutorial/app/src/main/res/menu/drawer_menu.xml":::

#### <a name="update-application-theme-and-layout"></a><span data-ttu-id="d46e8-147">更新应用程序主题和布局</span><span class="sxs-lookup"><span data-stu-id="d46e8-147">Update application theme and layout</span></span>

1. <span data-ttu-id="d46e8-148">打开 **应用/res/values/styles.xml** 并替换为 `Theme.AppCompat.Light.DarkActionBar` `Theme.AppCompat.Light.NoActionBar` 。</span><span class="sxs-lookup"><span data-stu-id="d46e8-148">Open the **app/res/values/styles.xml** file and replace `Theme.AppCompat.Light.DarkActionBar` with `Theme.AppCompat.Light.NoActionBar`.</span></span>

1. <span data-ttu-id="d46e8-149">在元素中添加以下 `style` 行。</span><span class="sxs-lookup"><span data-stu-id="d46e8-149">Add the following lines inside the `style` element.</span></span>

    ```xml
    <item name="windowActionBar">false</item>
    <item name="windowNoTitle">true</item>
    <item name="android:statusBarColor">@android:color/transparent</item>
    ```

1. <span data-ttu-id="d46e8-150">右键单击 **应用/res/layout** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="d46e8-150">Right-click the **app/res/layout** folder.</span></span>

1. <span data-ttu-id="d46e8-151">选择 **"新建**"，然后选择 **"布局"资源文件**。</span><span class="sxs-lookup"><span data-stu-id="d46e8-151">Select **New**, then **Layout resource file**.</span></span>

1. <span data-ttu-id="d46e8-152">命名文件 `nav_header` ，然后将 **根元素更改为** `LinearLayout` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-152">Name the file `nav_header` and change the **Root element** to `LinearLayout`, then select **OK**.</span></span>

1. <span data-ttu-id="d46e8-153">打开nav_header.xml **并选择** "文本 **"** 选项卡。将整个内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-153">Open the **nav_header.xml** file and select the **Text** tab. Replace the entire contents with the following.</span></span>

    :::code language="xml" source="../demo/GraphTutorial/app/src/main/res/layout/nav_header.xml":::

1. <span data-ttu-id="d46e8-154">打开 **应用/res/layout/activity_main.xml** 文件，将现有 XML 替换为以下内容，将布局更新为 `DrawerLayout` a。</span><span class="sxs-lookup"><span data-stu-id="d46e8-154">Open the **app/res/layout/activity_main.xml** file and update the layout to a `DrawerLayout` by replacing the existing XML with the following.</span></span>

    :::code language="xml" source="../demo/GraphTutorial/app/src/main/res/layout/activity_main.xml":::

1. <span data-ttu-id="d46e8-155">打开 **应用/res/values/strings.xml，** 并添加元素中的以下 `resources` 元素。</span><span class="sxs-lookup"><span data-stu-id="d46e8-155">Open **app/res/values/strings.xml** and add the following elements inside the `resources` element.</span></span>

    ```xml
    <string name="navigation_drawer_open">Open navigation drawer</string>
    <string name="navigation_drawer_close">Close navigation drawer</string>
    ```

1. <span data-ttu-id="d46e8-156">打开 **app/java/com.example/graphtu一l/MainActivity** 文件，将全部内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-156">Open the **app/java/com.example/graphtutorial/MainActivity** file and replace the entire contents with the following.</span></span>

    ```java
    package com.example.graphtutorial;

    import android.os.Bundle;
    import android.view.Menu;
    import android.view.MenuItem;
    import android.view.View;
    import android.widget.FrameLayout;
    import android.widget.ProgressBar;
    import android.widget.TextView;
    import androidx.annotation.NonNull;
    import androidx.appcompat.app.ActionBarDrawerToggle;
    import androidx.appcompat.app.AppCompatActivity;
    import androidx.appcompat.widget.Toolbar;
    import androidx.core.view.GravityCompat;
    import androidx.drawerlayout.widget.DrawerLayout;
    import com.google.android.material.navigation.NavigationView;

    public class MainActivity extends AppCompatActivity implements NavigationView.OnNavigationItemSelectedListener {
        private static final String SAVED_IS_SIGNED_IN = "isSignedIn";
        private static final String SAVED_USER_NAME = "userName";
        private static final String SAVED_USER_EMAIL = "userEmail";
        private static final String SAVED_USER_TIMEZONE = "userTimeZone";

        private DrawerLayout mDrawer;
        private NavigationView mNavigationView;
        private View mHeaderView;
        private boolean mIsSignedIn = false;
        private String mUserName = null;
        private String mUserEmail = null;
        private String mUserTimeZone = null;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            // Set the toolbar
            Toolbar toolbar = findViewById(R.id.toolbar);
            setSupportActionBar(toolbar);

            mDrawer = findViewById(R.id.drawer_layout);

            // Add the hamburger menu icon
            ActionBarDrawerToggle toggle = new ActionBarDrawerToggle(this, mDrawer, toolbar,
                    R.string.navigation_drawer_open, R.string.navigation_drawer_close);
            mDrawer.addDrawerListener(toggle);
            toggle.syncState();

            mNavigationView = findViewById(R.id.nav_view);

            // Set user name and email
            mHeaderView = mNavigationView.getHeaderView(0);
            setSignedInState(mIsSignedIn);

            // Listen for item select events on menu
            mNavigationView.setNavigationItemSelectedListener(this);

            if (savedInstanceState == null) {
                // Load the home fragment by default on startup
                openHomeFragment(mUserName);
            } else {
                // Restore state
                mIsSignedIn = savedInstanceState.getBoolean(SAVED_IS_SIGNED_IN);
                mUserName = savedInstanceState.getString(SAVED_USER_NAME);
                mUserEmail = savedInstanceState.getString(SAVED_USER_EMAIL);
                mUserTimeZone = savedInstanceState.getString(SAVED_USER_TIMEZONE);
                setSignedInState(mIsSignedIn);
            }
        }

        @Override
        protected void onSaveInstanceState(@NonNull Bundle outState) {
            super.onSaveInstanceState(outState);
            outState.putBoolean(SAVED_IS_SIGNED_IN, mIsSignedIn);
            outState.putString(SAVED_USER_NAME, mUserName);
            outState.putString(SAVED_USER_EMAIL, mUserEmail);
            outState.putString(SAVED_USER_TIMEZONE, mUserTimeZone);
        }

        @Override
        public boolean onNavigationItemSelected(@NonNull MenuItem menuItem) {
            // TEMPORARY
            return false;
        }

        @Override
        public void onBackPressed() {
            if (mDrawer.isDrawerOpen(GravityCompat.START)) {
                mDrawer.closeDrawer(GravityCompat.START);
            } else {
                super.onBackPressed();
            }
        }

        public void showProgressBar()
        {
            FrameLayout container = findViewById(R.id.fragment_container);
            ProgressBar progressBar = findViewById(R.id.progressbar);
            container.setVisibility(View.GONE);
            progressBar.setVisibility(View.VISIBLE);
        }

        public void hideProgressBar()
        {
            FrameLayout container = findViewById(R.id.fragment_container);
            ProgressBar progressBar = findViewById(R.id.progressbar);
            progressBar.setVisibility(View.GONE);
            container.setVisibility(View.VISIBLE);
        }

        // Update the menu and get the user's name and email
        private void setSignedInState(boolean isSignedIn) {
            mIsSignedIn = isSignedIn;

            mNavigationView.getMenu().clear();
            mNavigationView.inflateMenu(R.menu.drawer_menu);

            Menu menu = mNavigationView.getMenu();

            // Hide/show the Sign in, Calendar, and Sign Out buttons
            if (isSignedIn) {
                menu.removeItem(R.id.nav_signin);
            } else {
                menu.removeItem(R.id.nav_home);
                menu.removeItem(R.id.nav_calendar);
                menu.removeItem(R.id.nav_create_event);
                menu.removeItem(R.id.nav_signout);
            }

            // Set the user name and email in the nav drawer
            TextView userName = mHeaderView.findViewById(R.id.user_name);
            TextView userEmail = mHeaderView.findViewById(R.id.user_email);

            if (isSignedIn) {
                // For testing
                mUserName = "Lynne Robbins";
                mUserEmail = "lynner@contoso.com";
                mUserTimeZone = "Pacific Standard Time";

                userName.setText(mUserName);
                userEmail.setText(mUserEmail);
            } else {
                mUserName = null;
                mUserEmail = null;
                mUserTimeZone = null;

                userName.setText("Please sign in");
                userEmail.setText("");
            }
        }
    }
    ```

### <a name="add-fragments"></a><span data-ttu-id="d46e8-157">添加片段</span><span class="sxs-lookup"><span data-stu-id="d46e8-157">Add fragments</span></span>

<span data-ttu-id="d46e8-158">在此部分中，你将为家庭视图和日历视图创建片段。</span><span class="sxs-lookup"><span data-stu-id="d46e8-158">In this section you will create fragments for the home and calendar views.</span></span>

1. <span data-ttu-id="d46e8-159">右键单击 **应用/res/layout** 文件夹，然后选择 **"新建**"，然后选择 **"布局"资源文件**。</span><span class="sxs-lookup"><span data-stu-id="d46e8-159">Right-click the **app/res/layout** folder and select **New**, then **Layout resource file**.</span></span>

1. <span data-ttu-id="d46e8-160">命名文件 `fragment_home` ，然后将 **根元素更改为** `RelativeLayout` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-160">Name the file `fragment_home` and change the **Root element** to `RelativeLayout`, then select **OK**.</span></span>

1. <span data-ttu-id="d46e8-161">打开 **fragment_home.xml** 文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-161">Open the **fragment_home.xml** file and replace its contents with the following.</span></span>

    :::code language="xml" source="../demo/GraphTutorial/app/src/main/res/layout/fragment_home.xml":::

1. <span data-ttu-id="d46e8-162">右键单击 **应用/res/layout** 文件夹，然后选择 **"新建**"，然后选择 **"布局"资源文件**。</span><span class="sxs-lookup"><span data-stu-id="d46e8-162">Right-click the **app/res/layout** folder and select **New**, then **Layout resource file**.</span></span>

1. <span data-ttu-id="d46e8-163">命名文件 `fragment_calendar` ，然后将 **根元素更改为** `RelativeLayout` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-163">Name the file `fragment_calendar` and change the **Root element** to `RelativeLayout`, then select **OK**.</span></span>

1. <span data-ttu-id="d46e8-164">打开 **fragment_calendar.xml** 文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-164">Open the **fragment_calendar.xml** file and replace its contents with the following.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:text="Calendar"
            android:textSize="30sp" />

    </RelativeLayout>
    ```

1. <span data-ttu-id="d46e8-165">右键单击 **应用/res/layout** 文件夹，然后选择 **"新建**"，然后选择 **"布局"资源文件**。</span><span class="sxs-lookup"><span data-stu-id="d46e8-165">Right-click the **app/res/layout** folder and select **New**, then **Layout resource file**.</span></span>

1. <span data-ttu-id="d46e8-166">命名文件 `fragment_new_event` ，然后将 **根元素更改为** `RelativeLayout` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-166">Name the file `fragment_new_event` and change the **Root element** to `RelativeLayout`, then select **OK**.</span></span>

1. <span data-ttu-id="d46e8-167">打开 **fragment_new_event.xml** 文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-167">Open the **fragment_new_event.xml** file and replace its contents with the following.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:text="New Event"
            android:textSize="30sp" />

    </RelativeLayout>
    ```

1. <span data-ttu-id="d46e8-168">右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。</span><span class="sxs-lookup"><span data-stu-id="d46e8-168">Right-click the **app/java/com.example.graphtutorial** folder and select **New**, then **Java Class**.</span></span>

1. <span data-ttu-id="d46e8-169">命名类 `HomeFragment` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-169">Name the class `HomeFragment`, then select **OK**.</span></span>

1. <span data-ttu-id="d46e8-170">打开 **HomeFragment** 文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-170">Open the **HomeFragment** file and replace its contents with the following.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/HomeFragment.java" id="HomeSnippet":::

1. <span data-ttu-id="d46e8-171">右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。</span><span class="sxs-lookup"><span data-stu-id="d46e8-171">Right-click the **app/java/com.example.graphtutorial** folder and select **New**, then **Java Class**.</span></span>

1. <span data-ttu-id="d46e8-172">命名类 `CalendarFragment` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-172">Name the class `CalendarFragment`, then select **OK**.</span></span>

1. <span data-ttu-id="d46e8-173">打开 **CalendarFragment** 文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-173">Open the **CalendarFragment** file and replace its contents with the following.</span></span>

    ```java
    package com.example.graphtutorial;

    import android.os.Bundle;
    import android.view.LayoutInflater;
    import android.view.View;
    import android.view.ViewGroup;
    import androidx.annotation.NonNull;
    import androidx.annotation.Nullable;
    import androidx.fragment.app.Fragment;

    public class CalendarFragment extends Fragment {
        private static final String TIME_ZONE = "timeZone";

        private String mTimeZone;

        public CalendarFragment() {}

        public static CalendarFragment createInstance(String timeZone) {
            CalendarFragment fragment = new CalendarFragment();

            // Add the provided time zone to the fragment's arguments
            Bundle args = new Bundle();
            args.putString(TIME_ZONE, timeZone);
            fragment.setArguments(args);
            return fragment;
        }

        @Override
        public void onCreate(@Nullable Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            if (getArguments() != null) {
                mTimeZone = getArguments().getString(TIME_ZONE);
            }
        }

        @Nullable
        @Override
        public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
            return inflater.inflate(R.layout.fragment_calendar, container, false);
        }
    }
    ```

1. <span data-ttu-id="d46e8-174">右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。</span><span class="sxs-lookup"><span data-stu-id="d46e8-174">Right-click the **app/java/com.example.graphtutorial** folder and select **New**, then **Java Class**.</span></span>

1. <span data-ttu-id="d46e8-175">命名类 `NewEventFragment` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-175">Name the class `NewEventFragment`, then select **OK**.</span></span>

1. <span data-ttu-id="d46e8-176">打开 **NewEventFragment** 文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-176">Open the **NewEventFragment** file and replace its contents with the following.</span></span>

    ```java
    package com.example.graphtutorial;

    import android.os.Bundle;
    import android.view.LayoutInflater;
    import android.view.View;
    import android.view.ViewGroup;
    import androidx.annotation.NonNull;
    import androidx.annotation.Nullable;
    import androidx.fragment.app.Fragment;

    public class NewEventFragment extends Fragment {
        private static final String TIME_ZONE = "timeZone";

        private String mTimeZone;

        public NewEventFragment() {}

        public static NewEventFragment createInstance(String timeZone) {
            NewEventFragment fragment = new NewEventFragment();

            // Add the provided time zone to the fragment's arguments
            Bundle args = new Bundle();
            args.putString(TIME_ZONE, timeZone);
            fragment.setArguments(args);
            return fragment;
        }

        @Override
        public void onCreate(@Nullable Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            if (getArguments() != null) {
                mTimeZone = getArguments().getString(TIME_ZONE);
            }
        }

        @Nullable
        @Override
        public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
            return inflater.inflate(R.layout.fragment_new_event, container, false);
        }
    }
    ```

1. <span data-ttu-id="d46e8-177">打开 **MainActivity.java** 文件，将以下函数添加到类中。</span><span class="sxs-lookup"><span data-stu-id="d46e8-177">Open the **MainActivity.java** file and add the the following functions to the class.</span></span>

    ```java
    // Load the "Home" fragment
    public void openHomeFragment(String userName) {
        HomeFragment fragment = HomeFragment.createInstance(userName);
        getSupportFragmentManager().beginTransaction()
                .replace(R.id.fragment_container, fragment)
                .commit();
        mNavigationView.setCheckedItem(R.id.nav_home);
    }

    // Load the "Calendar" fragment
    private void openCalendarFragment(String timeZone) {
        CalendarFragment fragment = CalendarFragment.createInstance(timeZone);
        getSupportFragmentManager().beginTransaction()
                .replace(R.id.fragment_container, fragment)
                .commit();
        mNavigationView.setCheckedItem(R.id.nav_calendar);
    }

    // Load the "New Event" fragment
    private void openNewEventFragment(String timeZone) {
        NewEventFragment fragment = NewEventFragment.createInstance(timeZone);
        getSupportFragmentManager().beginTransaction()
                .replace(R.id.fragment_container, fragment)
                .commit();
        mNavigationView.setCheckedItem(R.id.nav_create_event);
    }

    private void signIn() {
        setSignedInState(true);
        openHomeFragment(mUserName);
    }

    private void signOut() {
        setSignedInState(false);
        openHomeFragment(mUserName);
    }
    ```

1. <span data-ttu-id="d46e8-178">将现有的 `onNavigationItemSelected` 函数替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="d46e8-178">Replace the existing `onNavigationItemSelected` function with the following.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/MainActivity.java" id="OnNavItemSelectedSnippet":::

1. <span data-ttu-id="d46e8-179">保存所有更改。</span><span class="sxs-lookup"><span data-stu-id="d46e8-179">Save all of your changes.</span></span>

1. <span data-ttu-id="d46e8-180">在"**运行"** 菜单上，选择 **"运行应用"。**</span><span class="sxs-lookup"><span data-stu-id="d46e8-180">On the **Run** menu, select **Run 'app'**.</span></span>

<span data-ttu-id="d46e8-181">应用的菜单应该可以在两个片段之间导航，并在点击"登录"或"注销"按钮 **时** 更改。</span><span class="sxs-lookup"><span data-stu-id="d46e8-181">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![应用程序的屏幕截图](./images/app-screens.png)
