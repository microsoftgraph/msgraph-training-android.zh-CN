<!-- markdownlint-disable MD002 MD041 -->

首先创建一个新的 Android Studio 项目。

1. 打开 Android Studio，并在欢迎屏幕上选择 "**启动新的 Android studio 项目**"。

1. 在 "**新建项目**" 对话框中，选择 "**空活动**"，然后选择 "**下一步**"。

    ![Android Studio 中的 "新建项目" 对话框的屏幕截图](./images/choose-project.png)

1. 在 "**配置项目**" 对话框中，将**** "名称`Graph Tutorial`" 设置为，确保 "**语言**" `Java`字段设置为，并确保将 "**最小 API" 级别**设置为`API 29: Android 10.0 (Q)`。 根据需要修改**包名称**和**保存位置**。 选择“完成”****。

    !["配置项目" 对话框的屏幕截图](./images/configure-project.png)

> [!IMPORTANT]
> 本教程中的代码和说明使用程序包名称**graphtutorial**。 如果您在创建项目时使用不同的包名称，请务必使用您的程序包名称，无论您何时看到此值。

## <a name="install-dependencies"></a>安装依赖项

在继续之前，请安装稍后将使用的一些其他依赖项。

- `com.google.android.material:material`使[导航视图](https://material.io/develop/android/components/navigation-view/)对应用程序可用。
- [适用于 Android 的 Microsoft 身份验证库（MSAL）](https://github.com/AzureAD/microsoft-authentication-library-for-android)来处理 Azure AD 身份验证和令牌管理。
- [Microsoft GRAPH SDK For Java](https://github.com/microsoftgraph/msgraph-sdk-java) ，用于调用 microsoft graph。

1. 展开 " **Gradle 脚本**"，然后打开 " **Gradle" （Module： app）** 文件。

1. 在`dependencies`值中添加以下行。

    ```Gradle
    implementation 'com.google.android.material:material:1.0.0'
    implementation 'com.microsoft.identity.client:msal:1.0.0'
    implementation 'com.microsoft.graph:microsoft-graph:1.6.0'
    ```

1. 在`packagingOptions` **gradle （Module： app）** 文件中的`android`值内添加值。

    ```Gradle
    packagingOptions {
        pickFirst 'META-INF/jersey-module-version'
    }
    ```

1. 保存所做的更改。 在 "**文件**" 菜单上，选择 "**使用 Gradle 文件同步项目**"。

## <a name="design-the-app"></a>设计应用程序

应用程序将使用导航抽屉在不同视图之间导航。 在此步骤中，将更新活动以使用导航抽屉版式，并为视图添加片段。

### <a name="create-a-navigation-drawer"></a>创建导航抽屉

在本节中，您将为应用的导航菜单创建图标，为应用程序创建菜单，并更新应用程序的主题和布局以与导航抽屉兼容。

#### <a name="create-icons"></a>创建图标

1. 右键单击 " **app/res/可以绘制**" 文件夹，然后选择 "**新建**"，然后选择 "**矢量资产**"。

1. 单击 "**剪贴画**" 旁边的 "图标" 按钮。

1. 在 "**选择图标**" 窗口中`home` ，键入搜索栏，然后选择 "**主页**" 图标，然后选择 **"确定"**。

1. 将**名称**更改为`ic_menu_home`。

    !["配置矢量资产" 窗口的屏幕截图](./images/create-icon.png)

1. 依次选择 "**下一步**" 和 "**完成**"。

1. 重复上一步以创建其他三个图标。

    - 名称： `ic_menu_calendar`，图标：`event`
    - 名称： `ic_menu_signout`，图标：`exit to app`
    - 名称： `ic_menu_signin`，图标：`person add`

#### <a name="create-the-menu"></a>创建菜单

1. 右键单击 " **res** " 文件夹，然后选择 "**新建**"，然后选择 " **Android 资源目录**"。

1. 将**资源类型**更改为`menu` ，然后选择 **"确定"**。

1. 右键单击新的**菜单**文件夹，然后选择 "**新建**"，然后选择 "**菜单资源文件**"。

1. 命名该文件`drawer_menu` ，然后选择 **"确定"**。

1. 打开文件时，选择 "**文本**" 选项卡以查看 XML，然后将整个内容替换为以下内容。

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

#### <a name="update-application-theme-and-layout"></a>更新应用程序主题和布局

1. 打开 "**应用程序/res/values/styles** " 文件，并`Theme.AppCompat.Light.DarkActionBar`将`Theme.AppCompat.Light.NoActionBar`替换为。

1. 在`style`元素内添加以下行。

    ```xml
    <item name="windowActionBar">false</item>
    <item name="windowNoTitle">true</item>
    <item name="android:statusBarColor">@android:color/transparent</item>
    ```

1. 右键单击 "**应用程序/分辨率/布局**" 文件夹。

1. 选择 "**新建**"，然后选择 "**布局资源文件**"。

1. 将文件`nav_header`命名并将**根元素**更改为`LinearLayout`，然后选择 **"确定"**。

1. 打开**nav_header .xml**文件，然后选择 "**文本**" 选项卡。将整个内容替换为以下内容。

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

1. 通过将现有的 XML 替换为以下项，打开**应用程序/res/layout/activity_main .xml**文件并将布局更新为 a `DrawerLayout` 。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
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

            <androidx.appcompat.widget.Toolbar
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

        <com.google.android.material.navigation.NavigationView
            android:id="@+id/nav_view"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:layout_gravity="start"
            app:headerLayout="@layout/nav_header"
            app:menu="@menu/drawer_menu" />

    </androidx.drawerlayout.widget.DrawerLayout>
    ```

1. 打开**应用程序/res/values/strings**并在`resources`元素中添加以下元素。

    ```xml
    <string name="navigation_drawer_open">Open navigation drawer</string>
    <string name="navigation_drawer_close">Close navigation drawer</string>
    ```

1. 打开**app/java/com 示例/graphtutorial/MainActivity**文件，并将整个内容替换为以下内容。

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

### <a name="add-fragments"></a>添加片段

在本节中，您将为 "主页" 和 "日历" 视图创建片段。

1. 右键单击 "**应用/分辨率/布局**" 文件夹，然后选择 "**新建**"，然后选择 "**布局资源文件**"。

1. 将文件`fragment_home`命名并将**根元素**更改为`RelativeLayout`，然后选择 **"确定"**。

1. 打开**fragment_home .xml**文件，并将其内容替换为以下内容。

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

1. 右键单击 "**应用/分辨率/布局**" 文件夹，然后选择 "**新建**"，然后选择 "**布局资源文件**"。

1. 将文件`fragment_calendar`命名并将**根元素**更改为`RelativeLayout`，然后选择 **"确定"**。

1. 打开**fragment_calendar .xml**文件，并将其内容替换为以下内容。

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

1. 右键单击 " **app/java/graphtutorial** " 文件夹，然后选择 "**新建**"，然后依次选择 " **java 类**"。

1. 命名该类`HomeFragment`并将**超类**设置为`androidx.fragment.app.Fragment`，然后选择 **"确定"**。

1. 打开 " **HomeFragment** " 文件，并将其内容替换为以下内容。

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

1. 右键单击 " **app/java/graphtutorial** " 文件夹，然后选择 "**新建**"，然后依次选择 " **java 类**"。

1. 命名该类`CalendarFragment`并将**超类**设置为`androidx.fragment.app.Fragment`，然后选择 **"确定"**。

1. 打开 " **CalendarFragment** " 文件，并将其内容替换为以下内容。

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

        @Nullable
        @Override
        public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
            return inflater.inflate(R.layout.fragment_calendar, container, false);
        }
    }
    ```

1. 打开**MainActivity**文件，并将以下函数添加到类中。

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

1. 将现有的 `onNavigationItemSelected` 函数替换为以下内容。

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

1. 在该`onCreate`函数的末尾添加以下内容，以在应用程序启动时加载主片段。

    ```java
    // Load the home fragment by default on startup
    if (savedInstanceState == null) {
        openHomeFragment(mUserName);
    }
    ```

1. 保存所有更改。

1. 在 "**运行**" 菜单上，选择 **"运行 ' 应用 '"**。

在点击 "登录 **" 或 "注销** **"** 按钮时，应用的菜单应工作在两个片段之间导航并发生变化。

![应用程序的屏幕截图](./images/app-screens.png)
