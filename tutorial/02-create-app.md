<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e8156-101">首先创建一个新的 Android Studio 项目。</span><span class="sxs-lookup"><span data-stu-id="e8156-101">Begin by creating a new Android Studio project.</span></span>

1. <span data-ttu-id="e8156-102">打开 Android Studio, 并在欢迎屏幕上选择 "**启动新的 Android studio 项目**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-102">Open Android Studio, and select **Start a new Android Studio project** on the welcome screen.</span></span>

1. <span data-ttu-id="e8156-103">在 "**新建项目**" 对话框中, 选择 "**空活动**", 然后选择 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-103">In the **Create New Project** dialog, select **Empty Activity**, then select **Next**.</span></span>

    ![Android Studio 中的 "新建项目" 对话框的屏幕截图](./images/choose-project.png)

1. <span data-ttu-id="e8156-105">在 "**配置项目**" 对话框中, 将\*\*\*\* "名称`Graph Tutorial`" 设置为, 确保 "**语言**" `Java`字段设置为, 并确保将 "**最小 API" 级别**设置为`API 27: Android 8.1 (Oreo)`。</span><span class="sxs-lookup"><span data-stu-id="e8156-105">In the **Configure your project** dialog, set the **Name** to `Graph Tutorial`, ensure the **Language** field is set to `Java`, and ensure the **Minimum API level** is set to `API 27: Android 8.1 (Oreo)`.</span></span> <span data-ttu-id="e8156-106">根据需要修改**包名称**和**保存位置**。</span><span class="sxs-lookup"><span data-stu-id="e8156-106">Modify the **Package name** and **Save location** as needed.</span></span> <span data-ttu-id="e8156-107">选择“完成”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="e8156-107">Select **Finish**.</span></span>

    !["配置项目" 对话框的屏幕截图](./images/configure-project.png)

> [!IMPORTANT]
> <span data-ttu-id="e8156-109">确保为在这些实验室说明中指定的项目输入完全相同的名称。</span><span class="sxs-lookup"><span data-stu-id="e8156-109">Ensure that you enter the exact same name for the project that is specified in these lab instructions.</span></span> <span data-ttu-id="e8156-110">项目名称将成为代码中的命名空间的一部分。</span><span class="sxs-lookup"><span data-stu-id="e8156-110">The project name becomes part of the namespace in the code.</span></span> <span data-ttu-id="e8156-111">这些指令中的代码取决于与这些说明中指定的项目名称匹配的命名空间。</span><span class="sxs-lookup"><span data-stu-id="e8156-111">The code inside these instructions depends on the namespace matching the project name specified in these instructions.</span></span> <span data-ttu-id="e8156-112">如果使用其他项目名称, 则代码将不会编译, 除非您调整所有命名空间以匹配您在创建项目时输入的项目名称。</span><span class="sxs-lookup"><span data-stu-id="e8156-112">If you use a different project name the code will not compile unless you adjust all the namespaces to match the project name you enter when you create the project.</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="e8156-113">安装依赖项</span><span class="sxs-lookup"><span data-stu-id="e8156-113">Install dependencies</span></span>

<span data-ttu-id="e8156-114">在继续之前, 请安装稍后将使用的一些其他依赖项。</span><span class="sxs-lookup"><span data-stu-id="e8156-114">Before moving on, install some additional dependencies that you will use later.</span></span>

- <span data-ttu-id="e8156-115">`com.android.support:design`使导航抽屉布局对应用程序可用。</span><span class="sxs-lookup"><span data-stu-id="e8156-115">`com.android.support:design` to make the navigation drawer layouts available to the app.</span></span>
- <span data-ttu-id="e8156-116">[适用于 Android 的 Microsoft 身份验证库 (MSAL)](https://github.com/AzureAD/microsoft-authentication-library-for-android)来处理 Azure AD 身份验证和令牌管理。</span><span class="sxs-lookup"><span data-stu-id="e8156-116">[Microsoft Authentication Library (MSAL) for Android](https://github.com/AzureAD/microsoft-authentication-library-for-android) to handle Azure AD authentication and token management.</span></span>
- <span data-ttu-id="e8156-117">[Microsoft GRAPH SDK For Java](https://github.com/microsoftgraph/msgraph-sdk-java) , 用于调用 microsoft graph。</span><span class="sxs-lookup"><span data-stu-id="e8156-117">[Microsoft Graph SDK for Java](https://github.com/microsoftgraph/msgraph-sdk-java) for making calls to the Microsoft Graph.</span></span>

1. <span data-ttu-id="e8156-118">展开 " **Gradle 脚本**", 然后打开 " **Gradle" (Module: app)** 文件。</span><span class="sxs-lookup"><span data-stu-id="e8156-118">Expand **Gradle Scripts**, then open the **build.gradle (Module: app)** file.</span></span>

1. <span data-ttu-id="e8156-119">在`dependencies`值中添加以下行。</span><span class="sxs-lookup"><span data-stu-id="e8156-119">Add the following lines inside the `dependencies` value.</span></span>

    ```Gradle
    implementation 'com.android.support:design:28.0.0'
    implementation 'com.microsoft.graph:microsoft-graph:1.4.0'
    implementation 'com.microsoft.identity.client:msal:0.2.2'
    ```

    > [!NOTE]
    > <span data-ttu-id="e8156-120">如果使用的是不同的 SDK 版本, 请务必将更改`28.0.0`为与**gradle**中已存在的`com.android.support:appcompat-v7`依赖项版本相匹配。</span><span class="sxs-lookup"><span data-stu-id="e8156-120">If you are using a different SDK version, make sure to change the `28.0.0` to match the version of the `com.android.support:appcompat-v7` dependency already present in **build.gradle**.</span></span>

1. <span data-ttu-id="e8156-121">在`packagingOptions` **gradle (Module: app)** 文件中的值的`android`内部添加一个。</span><span class="sxs-lookup"><span data-stu-id="e8156-121">Add a `packagingOptions` inside the `android` value in the **build.gradle (Module: app)** file.</span></span>

    ```Gradle
    packagingOptions {
        pickFirst 'META-INF/jersey-module-version'
    }
    ```

1. <span data-ttu-id="e8156-122">保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="e8156-122">Save your changes.</span></span> <span data-ttu-id="e8156-123">在 "**文件**" 菜单上, 选择 "**使用 Gradle 文件同步项目**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-123">On the **File** menu, select **Sync Project with Gradle Files**.</span></span>

## <a name="design-the-app"></a><span data-ttu-id="e8156-124">设计应用程序</span><span class="sxs-lookup"><span data-stu-id="e8156-124">Design the app</span></span>

<span data-ttu-id="e8156-125">应用程序将使用[导航抽屉](https://developer.android.com/training/implementing-navigation/nav-drawer)在不同视图之间导航。</span><span class="sxs-lookup"><span data-stu-id="e8156-125">The application will use a [navigation drawer](https://developer.android.com/training/implementing-navigation/nav-drawer) to navigate between different views.</span></span> <span data-ttu-id="e8156-126">在此步骤中, 将更新活动以使用导航抽屉版式, 并为视图添加片段。</span><span class="sxs-lookup"><span data-stu-id="e8156-126">In this step you will update the activity to use a navigation drawer layout, and add fragments for the views.</span></span>

### <a name="create-a-navigation-drawer"></a><span data-ttu-id="e8156-127">创建导航抽屉</span><span class="sxs-lookup"><span data-stu-id="e8156-127">Create a navigation drawer</span></span>

<span data-ttu-id="e8156-128">在本节中, 您将为应用的导航菜单创建图标, 为应用程序创建菜单, 并更新应用程序的主题和布局以与导航抽屉兼容。</span><span class="sxs-lookup"><span data-stu-id="e8156-128">In this section you will create icons for the app's navigation menu, create a menu for the application, and update the application's theme and layout to be compatible with a navigation drawer.</span></span>

#### <a name="create-icons"></a><span data-ttu-id="e8156-129">创建图标</span><span class="sxs-lookup"><span data-stu-id="e8156-129">Create icons</span></span>

1. <span data-ttu-id="e8156-130">右键单击 " **app/res/可以绘制**" 文件夹, 然后选择 "**新建**", 然后选择 "**矢量资产**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-130">Right-click the **app/res/drawable** folder and select **New**, then **Vector Asset**.</span></span>

1. <span data-ttu-id="e8156-131">单击 "**剪贴画**" 旁边的 "图标" 按钮。</span><span class="sxs-lookup"><span data-stu-id="e8156-131">Click the icon button next to **Clip Art**.</span></span>

1. <span data-ttu-id="e8156-132">在 "**选择图标**" 窗口中`home` , 键入搜索栏, 然后选择 "**主页**" 图标, 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="e8156-132">In the **Select Icon** window, type `home` in the search bar, then select the **Home** icon and select **OK**.</span></span>

1. <span data-ttu-id="e8156-133">将**名称**更改为`ic_menu_home`。</span><span class="sxs-lookup"><span data-stu-id="e8156-133">Change the **Name** to `ic_menu_home`.</span></span>

    !["配置矢量资产" 窗口的屏幕截图](./images/create-icon.png)

1. <span data-ttu-id="e8156-135">依次选择 "**下一步**" 和 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-135">Select **Next**, then **Finish**.</span></span>

1. <span data-ttu-id="e8156-136">重复上一步以创建其他三个图标。</span><span class="sxs-lookup"><span data-stu-id="e8156-136">Repeat the previous step to create three more icons.</span></span>

    - <span data-ttu-id="e8156-137">名称: `ic_menu_calendar`, 图标:`event`</span><span class="sxs-lookup"><span data-stu-id="e8156-137">Name: `ic_menu_calendar`, Icon: `event`</span></span>
    - <span data-ttu-id="e8156-138">名称: `ic_menu_signout`, 图标:`exit to app`</span><span class="sxs-lookup"><span data-stu-id="e8156-138">Name: `ic_menu_signout`, Icon: `exit to app`</span></span>
    - <span data-ttu-id="e8156-139">名称: `ic_menu_signin`, 图标:`person add`</span><span class="sxs-lookup"><span data-stu-id="e8156-139">Name: `ic_menu_signin`, Icon: `person add`</span></span>

#### <a name="create-the-menu"></a><span data-ttu-id="e8156-140">创建菜单</span><span class="sxs-lookup"><span data-stu-id="e8156-140">Create the menu</span></span>

1. <span data-ttu-id="e8156-141">右键单击 " **res** " 文件夹, 然后选择 "**新建**", 然后选择 " **Android 资源目录**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-141">Right-click the **res** folder and select **New**, then **Android Resource Directory**.</span></span>

1. <span data-ttu-id="e8156-142">将**资源类型**更改为`menu` , 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="e8156-142">Change the **Resource type** to `menu` and select **OK**.</span></span>

1. <span data-ttu-id="e8156-143">右键单击新的**菜单**文件夹, 然后选择 "**新建**", 然后选择 "**菜单资源文件**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-143">Right-click the new **menu** folder and select **New**, then **Menu resource file**.</span></span>

1. <span data-ttu-id="e8156-144">命名该文件`drawer_menu` , 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="e8156-144">Name the file `drawer_menu` and select **OK**.</span></span>

1. <span data-ttu-id="e8156-145">打开文件时, 选择 "**文本**" 选项卡以查看 XML, 然后将整个内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="e8156-145">When the file opens, select the **Text** tab to view the XML, then replace the entire contents with the following.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <menu xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        tools:showIn="navigation_view">

        <group android:checkableBehavior="single">
            <item
                android:id="@+id/nav_home"
                android:icon="@drawable/ic_menu_home"
                android:title="Home" />

            <item
                android:id="@+id/nav_calendar"
                android:icon="@drawable/ic_menu_calendar"
                android:title="Calendar" />
        </group>

        <item android:title="Account">
            <menu>
                <item
                    android:id="@+id/nav_signin"
                    android:icon="@drawable/ic_menu_signin"
                    android:title="Sign In" />

                <item
                    android:id="@+id/nav_signout"
                    android:icon="@drawable/ic_menu_signout"
                    android:title="Sign Out" />
            </menu>
        </item>

    </menu>
    ```

#### <a name="update-application-theme-and-layout"></a><span data-ttu-id="e8156-146">更新应用程序主题和布局</span><span class="sxs-lookup"><span data-stu-id="e8156-146">Update application theme and layout</span></span>

1. <span data-ttu-id="e8156-147">打开 "**应用程序/res/values/styles** " 文件, 并`Theme.AppCompat.Light.DarkActionBar`将`Theme.AppCompat.Light.NoActionBar`替换为。</span><span class="sxs-lookup"><span data-stu-id="e8156-147">Open the **app/res/values/styles.xml** file and replace `Theme.AppCompat.Light.DarkActionBar` with `Theme.AppCompat.Light.NoActionBar`.</span></span>

1. <span data-ttu-id="e8156-148">在`style`元素内添加以下行。</span><span class="sxs-lookup"><span data-stu-id="e8156-148">Add the following lines inside the `style` element.</span></span>

    ```xml
    <item name="windowActionBar">false</item>
    <item name="windowNoTitle">true</item>
    <item name="android:statusBarColor">@android:color/transparent</item>
    ```

1. <span data-ttu-id="e8156-149">右键单击 "**应用程序/分辨率/布局**" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e8156-149">Right-click the **app/res/layout** folder.</span></span>

1. <span data-ttu-id="e8156-150">选择 "**新建**", 然后选择 "**布局资源文件**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-150">Select **New**, then **Layout resource file**.</span></span>

1. <span data-ttu-id="e8156-151">将文件`nav_header`命名并将**根元素**更改为`LinearLayout`, 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="e8156-151">Name the file `nav_header` and change the **Root element** to `LinearLayout`, then select **OK**.</span></span>

1. <span data-ttu-id="e8156-152">打开**nav_header**文件并选择 "**文本**" 选项卡。将整个内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="e8156-152">Open the **nav_header.xml** file and select the **Text** tab. Replace the entire contents with the following.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="176dp"
        android:background="@color/colorPrimary"
        android:gravity="bottom"
        android:orientation="vertical"
        android:padding="16dp"
        android:theme="@style/ThemeOverlay.AppCompat.Dark">

        <ImageView
            android:id="@+id/user_profile_pic"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@mipmap/ic_launcher" />

        <TextView
            android:id="@+id/user_name"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:paddingTop="8dp"
            android:text="Test User"
            android:textAppearance="@style/TextAppearance.AppCompat.Body1" />

        <TextView
            android:id="@+id/user_email"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="test@contoso.com" />

    </LinearLayout>
    ```

1. <span data-ttu-id="e8156-153">通过将现有 XML 替换为以下项, 打开**app/res/layout/activity_main**文件`DrawerLayout`并将布局更新为 a。</span><span class="sxs-lookup"><span data-stu-id="e8156-153">Open the **app/res/layout/activity_main.xml** file and update the layout to a `DrawerLayout` by replacing the existing XML with the following.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:id="@+id/drawer_layout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:fitsSystemWindows="true"
        tools:context=".MainActivity"
        tools:openDrawer="start">

        <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">

            <ProgressBar
                android:id="@+id/progressbar"
                android:layout_width="75dp"
                android:layout_height="75dp"
                android:layout_centerInParent="true"
                android:visibility="gone"/>

            <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                android:background="@color/colorPrimary"
                android:elevation="4dp"
                android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar" />

            <FrameLayout
                android:id="@+id/fragment_container"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:layout_below="@+id/toolbar" />
        </RelativeLayout>

        <android.support.design.widget.NavigationView
            android:id="@+id/nav_view"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:layout_gravity="start"
            app:headerLayout="@layout/nav_header"
            app:menu="@menu/drawer_menu" />

    </android.support.v4.widget.DrawerLayout>
    ```

1. <span data-ttu-id="e8156-154">打开**应用程序/res/values/strings**并在`resources`元素中添加以下元素。</span><span class="sxs-lookup"><span data-stu-id="e8156-154">Open **app/res/values/strings.xml** and add the following elements inside the `resources` element.</span></span>

    ```xml
    <string name="navigation_drawer_open">Open navigation drawer</string>
    <string name="navigation_drawer_close">Close navigation drawer</string>
    ```

1. <span data-ttu-id="e8156-155">打开**app/java/com 示例/graphtutorial/MainActivity**文件, 并将整个内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="e8156-155">Open the **app/java/com.example/graphtutorial/MainActivity** file and replace the entire contents with the following.</span></span>

    ```java
    package com.example.graphtutorial;

    import android.support.annotation.NonNull;
    import android.support.design.widget.NavigationView;
    import android.support.v4.view.GravityCompat;
    import android.support.v4.widget.DrawerLayout;
    import android.support.v7.app.ActionBarDrawerToggle;
    import android.support.v7.app.AppCompatActivity;
    import android.os.Bundle;
    import android.support.v7.widget.Toolbar;
    import android.view.Menu;
    import android.view.MenuItem;
    import android.view.View;
    import android.widget.FrameLayout;
    import android.widget.ProgressBar;
    import android.widget.TextView;

    public class MainActivity extends AppCompatActivity implements NavigationView.OnNavigationItemSelectedListener {
        private DrawerLayout mDrawer;
        private NavigationView mNavigationView;
        private View mHeaderView;
        private boolean mIsSignedIn = false;
        private String mUserName = null;
        private String mUserEmail = null;

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

            Menu menu = mNavigationView.getMenu();

            // Hide/show the Sign in, Calendar, and Sign Out buttons
            menu.findItem(R.id.nav_signin).setVisible(!isSignedIn);
            menu.findItem(R.id.nav_calendar).setVisible(isSignedIn);
            menu.findItem(R.id.nav_signout).setVisible(isSignedIn);

            // Set the user name and email in the nav drawer
            TextView userName = mHeaderView.findViewById(R.id.user_name);
            TextView userEmail = mHeaderView.findViewById(R.id.user_email);

            if (isSignedIn) {
                // For testing
                mUserName = "Megan Bowen";
                mUserEmail = "meganb@contoso.com";

                userName.setText(mUserName);
                userEmail.setText(mUserEmail);
            } else {
                mUserName = null;
                mUserEmail = null;

                userName.setText("Please sign in");
                userEmail.setText("");
            }
        }
    }
    ```

### <a name="add-fragments"></a><span data-ttu-id="e8156-156">添加片段</span><span class="sxs-lookup"><span data-stu-id="e8156-156">Add fragments</span></span>

<span data-ttu-id="e8156-157">在本节中, 您将为 "主页" 和 "日历" 视图创建片段。</span><span class="sxs-lookup"><span data-stu-id="e8156-157">In this section you will create fragments for the home and calendar views.</span></span>

1. <span data-ttu-id="e8156-158">右键单击 "**应用/分辨率/布局**" 文件夹, 然后选择 "**新建**", 然后选择 "**布局资源文件**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-158">Right-click the **app/res/layout** folder and select **New**, then **Layout resource file**.</span></span>

1. <span data-ttu-id="e8156-159">将文件`fragment_home`命名并将**根元素**更改为`RelativeLayout`, 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="e8156-159">Name the file `fragment_home` and change the **Root element** to `RelativeLayout`, then select **OK**.</span></span>

1. <span data-ttu-id="e8156-160">打开 " **fragment_home** " 文件, 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="e8156-160">Open the **fragment_home.xml** file and replace its contents with the following.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:orientation="vertical">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center_horizontal"
                android:text="Welcome!"
                android:textSize="30sp" />

            <TextView
                android:id="@+id/home_page_username"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center_horizontal"
                android:paddingTop="8dp"
                android:text="Please sign in"
                android:textSize="20sp" />
        </LinearLayout>

    </RelativeLayout>
    ```

1. <span data-ttu-id="e8156-161">右键单击 "**应用/分辨率/布局**" 文件夹, 然后选择 "**新建**", 然后选择 "**布局资源文件**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-161">Right-click the **app/res/layout** folder and select **New**, then **Layout resource file**.</span></span>

1. <span data-ttu-id="e8156-162">将文件`fragment_calendar`命名并将**根元素**更改为`RelativeLayout`, 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="e8156-162">Name the file `fragment_calendar` and change the **Root element** to `RelativeLayout`, then select **OK**.</span></span>

1. <span data-ttu-id="e8156-163">打开 " **fragment_calendar** " 文件, 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="e8156-163">Open the **fragment_calendar.xml** file and replace its contents with the following.</span></span>

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

1. <span data-ttu-id="e8156-164">右键单击 " **app/java/graphtutorial** " 文件夹, 然后选择 "**新建**", 然后依次选择 " **java 类**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-164">Right-click the **app/java/com.example.graphtutorial** folder and select **New**, then **Java Class**.</span></span>

1. <span data-ttu-id="e8156-165">命名该类`HomeFragment`并将**超类**设置为`android.support.v4.app.Fragment`, 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="e8156-165">Name the class `HomeFragment` and set the **Superclass** to `android.support.v4.app.Fragment`, then select **OK**.</span></span>

1. <span data-ttu-id="e8156-166">打开 " **HomeFragment** " 文件, 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="e8156-166">Open the **HomeFragment** file and replace its contents with the following.</span></span>

    ```java
    package com.example.graphtutorial;

    import android.os.Bundle;
    import android.support.annotation.NonNull;
    import android.support.annotation.Nullable;
    import android.support.v4.app.Fragment;
    import android.view.LayoutInflater;
    import android.view.View;
    import android.view.ViewGroup;
    import android.widget.TextView;

    public class HomeFragment extends Fragment {
        private static final String USER_NAME = "userName";

        private String mUserName;

        public HomeFragment() {

        }

        public static HomeFragment createInstance(String userName) {
            HomeFragment fragment = new HomeFragment();

            // Add the provided username to the fragment's arguments
            Bundle args = new Bundle();
            args.putString(USER_NAME, userName);
            fragment.setArguments(args);
            return fragment;
        }

        @Override
        public void onCreate(@Nullable Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            if (getArguments() != null) {
                mUserName = getArguments().getString(USER_NAME);
            }
        }

        @Nullable
        @Override
        public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
            View homeView = inflater.inflate(R.layout.fragment_home, container, false);

            // If there is a username, replace the "Please sign in" with the username
            if (mUserName != null) {
                TextView userName = homeView.findViewById(R.id.home_page_username);
                userName.setText(mUserName);
            }

            return homeView;
        }
    }
    ```

1. <span data-ttu-id="e8156-167">右键单击 " **app/java/graphtutorial** " 文件夹, 然后选择 "**新建**", 然后依次选择 " **java 类**"。</span><span class="sxs-lookup"><span data-stu-id="e8156-167">Right-click the **app/java/com.example.graphtutorial** folder and select **New**, then **Java Class**.</span></span>

1. <span data-ttu-id="e8156-168">命名该类`CalendarFragment`并将**超类**设置为`android.support.v4.app.Fragment`, 然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="e8156-168">Name the class `CalendarFragment` and set the **Superclass** to `android.support.v4.app.Fragment`, then select **OK**.</span></span>

1. <span data-ttu-id="e8156-169">打开 " **CalendarFragment** " 文件, 并将以下函数添加`CalendarFragment`到类中。</span><span class="sxs-lookup"><span data-stu-id="e8156-169">Open the **CalendarFragment** file and add the following function to the `CalendarFragment` class.</span></span>

    ```java
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_calendar, container, false);
    }
    ```

1. <span data-ttu-id="e8156-170">打开**MainActivity**文件, 并将以下函数添加到类中。</span><span class="sxs-lookup"><span data-stu-id="e8156-170">Open the **MainActivity.java** file and add the the following functions to the class.</span></span>

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
    private void openCalendarFragment() {
        getSupportFragmentManager().beginTransaction()
                .replace(R.id.fragment_container, new CalendarFragment())
                .commit();
        mNavigationView.setCheckedItem(R.id.nav_calendar);
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

1. <span data-ttu-id="e8156-171">将现有的 `onNavigationItemSelected` 函数替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="e8156-171">Replace the existing `onNavigationItemSelected` function with the following.</span></span>

    ```java
    @Override
    public boolean onNavigationItemSelected(@NonNull MenuItem menuItem) {
        // Load the fragment that corresponds to the selected item
        switch (menuItem.getItemId()) {
            case R.id.nav_home:
                openHomeFragment(mUserName);
                break;
            case R.id.nav_calendar:
                openCalendarFragment();
                break;
            case R.id.nav_signin:
                signIn();
                break;
            case R.id.nav_signout:
                signOut();
                break;
        }

        mDrawer.closeDrawer(GravityCompat.START);

        return true;
    }
    ```

1. <span data-ttu-id="e8156-172">在该`onCreate`函数的末尾添加以下内容, 以在应用程序启动时加载主片段。</span><span class="sxs-lookup"><span data-stu-id="e8156-172">Add the following at the end of the `onCreate` function to load the home fragment when the app starts.</span></span>

    ```java
    // Load the home fragment by default on startup
    if (savedInstanceState == null) {
        openHomeFragment(mUserName);
    }
    ```

1. <span data-ttu-id="e8156-173">保存所有更改。</span><span class="sxs-lookup"><span data-stu-id="e8156-173">Save all of your changes.</span></span>

1. <span data-ttu-id="e8156-174">在 "**运行**" 菜单上, 选择 **"运行 ' 应用 '"**。</span><span class="sxs-lookup"><span data-stu-id="e8156-174">On the **Run** menu, select **Run 'app'**.</span></span>

<span data-ttu-id="e8156-175">在点击 "登录" 或 "注销 **"** 按钮时, 应用的菜单应工作在两个片段\*\*\*\* 之间导航并发生变化。</span><span class="sxs-lookup"><span data-stu-id="e8156-175">The app's menu should work to navigate between the two fragments and change when you tap the **Sign in** or **Sign out** buttons.</span></span>

![应用程序的屏幕截图](./images/app-screens.png)
