# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="9ddb3-101">如何运行已完成的项目</span><span class="sxs-lookup"><span data-stu-id="9ddb3-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ddb3-102">先决条件</span><span class="sxs-lookup"><span data-stu-id="9ddb3-102">Prerequisites</span></span>

<span data-ttu-id="9ddb3-103">若要在此文件夹中运行已完成的项目，您需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="9ddb3-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="9ddb3-104">[Android Studio](https://developer.android.com/studio/) 安装在开发计算机上。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-104">[Android Studio](https://developer.android.com/studio/) installed on your development machine.</span></span> <span data-ttu-id="9ddb3-105"> (**注意：** 本教程是使用 Android Studio 3.6.2 版和 Android 10.0 SDK 编写的。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-105">(**Note:** This tutorial was written with Android Studio version 3.6.2 and the Android 10.0 SDK.</span></span> <span data-ttu-id="9ddb3-106">本指南中的步骤可能与其他版本一样，但尚未测试。) </span><span class="sxs-lookup"><span data-stu-id="9ddb3-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="9ddb3-107">具有邮箱的个人 Microsoft 帐户Outlook.com Microsoft 工作或学校帐户。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="9ddb3-108">如果你没有 Microsoft 帐户，则有几个选项可以获取免费帐户：</span><span class="sxs-lookup"><span data-stu-id="9ddb3-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="9ddb3-109">你可以 [注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="9ddb3-110">你可以 [注册 Office 365 开发人员计划](https://developer.microsoft.com/office/dev-program) ，获取免费的 Office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-an-application-with-the-azure-portal"></a><span data-ttu-id="9ddb3-111">向 Azure 门户注册应用程序</span><span class="sxs-lookup"><span data-stu-id="9ddb3-111">Register an application with the Azure Portal</span></span>

1. <span data-ttu-id="9ddb3-112">打开浏览器，并转到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。然后，使用 **个人帐户**（亦称为“Microsoft 帐户”）或 **工作或学校帐户** 登录。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="9ddb3-113">选择左侧导航栏中的“**Azure Active Directory**”，再选择“**管理**”下的“**应用注册**”。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-113">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="9ddb3-114">应用注册的屏幕截图</span><span class="sxs-lookup"><span data-stu-id="9ddb3-114">A screenshot of the App registrations</span></span> ](../../tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="9ddb3-115">选择“新注册”。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-115">Select **New registration**.</span></span> <span data-ttu-id="9ddb3-116">在“注册应用”页上，按如下方式设置值。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-116">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="9ddb3-117">将“名称”设置为“`Android Graph Tutorial`”。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-117">Set **Name** to `Android Graph Tutorial`.</span></span>
    - <span data-ttu-id="9ddb3-118">将“受支持的帐户类型”设置为“任何组织目录中的帐户和个人 Microsoft 帐户”。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-118">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="9ddb3-119">在 **"重定向 URI"** 下，将下拉列表设置为公共客户端/本机 **(移动&桌面)** 并设置值，以替换为项目的 `msauth://YOUR_PACKAGE_NAME/callback` `YOUR_PACKAGE_NAME` 程序包名称。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-119">Under **Redirect URI**, set the dropdown to **Public client/native (mobile & desktop)** and set the value to `msauth://YOUR_PACKAGE_NAME/callback`, replacing `YOUR_PACKAGE_NAME` with your project's package name.</span></span>

    !["注册应用程序"页的屏幕截图](../../tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="9ddb3-121">选择“**注册**”。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-121">Select **Register**.</span></span> <span data-ttu-id="9ddb3-122">在 **"Android Graph** 教程"页上，复制应用程序 (客户端) **ID** 并保存它，下一步中将需要该值。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-122">On the **Android Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新应用注册的应用程序 ID 屏幕截图](../../tutorial/images/aad-application-id.png)

## <a name="configure-the-sample"></a><span data-ttu-id="9ddb3-124">配置示例</span><span class="sxs-lookup"><span data-stu-id="9ddb3-124">Configure the sample</span></span>

1. <span data-ttu-id="9ddb3-125">将 `msal_config.json.example` 文件重命名为 `msal_config.json` 并移动到 `GraphTutorial/app/src/main/res/raw` 目录中。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-125">Rename the `msal_config.json.example` file to `msal_config.json` and move the file into the `GraphTutorial/app/src/main/res/raw` directory.</span></span>
1. <span data-ttu-id="9ddb3-126">编辑 `msal_config.json` 文件并做出以下更改。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-126">Edit the `msal_config.json` file and make the following changes.</span></span>
    1. <span data-ttu-id="9ddb3-127">替换为 `YOUR_APP_ID_HERE` 从Azure 门户获取的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-127">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the Azure portal.</span></span>
    1. <span data-ttu-id="9ddb3-128">替换为 `com.example.graphtutorial` 程序包名称。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-128">Replace `com.example.graphtutorial` with your package name.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="9ddb3-129">运行示例</span><span class="sxs-lookup"><span data-stu-id="9ddb3-129">Run the sample</span></span>

<span data-ttu-id="9ddb3-130">在 Android Studio 中，**在"运行"菜单\*\*\*\*上选择"** 运行应用"。</span><span class="sxs-lookup"><span data-stu-id="9ddb3-130">In Android Studio, select **Run 'app'** on the **Run** menu.</span></span>
