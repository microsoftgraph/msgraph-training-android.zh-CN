# <a name="how-to-run-the-completed-project"></a>如何运行已完成的项目

## <a name="prerequisites"></a>先决条件

若要在此文件夹中运行已完成的项目，您需要以下各项：

- [Android Studio](https://developer.android.com/studio/) 安装在开发计算机上。  (**注意：** 本教程是使用 Android Studio 3.6.2 版和 Android 10.0 SDK 编写的。 本指南中的步骤可能与其他版本一样，但尚未测试。) 
- 具有邮箱的个人 Microsoft 帐户Outlook.com Microsoft 工作或学校帐户。

如果你没有 Microsoft 帐户，则有几个选项可以获取免费帐户：

- 你可以 [注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。
- 你可以 [注册 Office 365 开发人员计划](https://developer.microsoft.com/office/dev-program) ，获取免费的 Office 365 订阅。

## <a name="register-an-application-with-the-azure-portal"></a>向 Azure 门户注册应用程序

1. 打开浏览器，并转到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。然后，使用 **个人帐户**（亦称为“Microsoft 帐户”）或 **工作或学校帐户** 登录。

1. 选择左侧导航栏中的“**Azure Active Directory**”，再选择“**管理**”下的“**应用注册**”。

    ![应用注册的屏幕截图 ](../../tutorial/images/aad-portal-app-registrations.png)

1. 选择“新注册”。 在“注册应用”页上，按如下方式设置值。

    - 将“名称”设置为“`Android Graph Tutorial`”。
    - 将“受支持的帐户类型”设置为“任何组织目录中的帐户和个人 Microsoft 帐户”。
    - 在 **"重定向 URI"** 下，将下拉列表设置为公共客户端/本机 **(移动&桌面)** 并设置值，以替换为项目的 `msauth://YOUR_PACKAGE_NAME/callback` `YOUR_PACKAGE_NAME` 程序包名称。

    !["注册应用程序"页的屏幕截图](../../tutorial/images/aad-register-an-app.png)

1. 选择“**注册**”。 在 **"Android Graph** 教程"页上，复制应用程序 (客户端) **ID** 并保存它，下一步中将需要该值。

    ![新应用注册的应用程序 ID 屏幕截图](../../tutorial/images/aad-application-id.png)

## <a name="configure-the-sample"></a>配置示例

1. 将 `msal_config.json.example` 文件重命名为 `msal_config.json` 并移动到 `GraphTutorial/app/src/main/res/raw` 目录中。
1. 编辑 `msal_config.json` 文件并做出以下更改。
    1. 替换为 `YOUR_APP_ID_HERE` 从Azure 门户获取的应用程序 ID。
    1. 替换为 `com.example.graphtutorial` 程序包名称。

## <a name="run-the-sample"></a>运行示例

在 Android Studio 中，**在"运行"菜单****上选择"** 运行应用"。
