# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="62eeb-101">如何运行已完成的项目</span><span class="sxs-lookup"><span data-stu-id="62eeb-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62eeb-102">先决条件</span><span class="sxs-lookup"><span data-stu-id="62eeb-102">Prerequisites</span></span>

<span data-ttu-id="62eeb-103">若要在此文件夹中运行已完成的项目，您需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="62eeb-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="62eeb-104">安装在开发计算机上的[Android Studio](https://developer.android.com/studio/) 。</span><span class="sxs-lookup"><span data-stu-id="62eeb-104">[Android Studio](https://developer.android.com/studio/) installed on your development machine.</span></span> <span data-ttu-id="62eeb-105">（**注意：** 本教程是使用 android Studio 版本3.5.1 和 ANDROID 10.0 SDK 编写的。</span><span class="sxs-lookup"><span data-stu-id="62eeb-105">(**Note:** This tutorial was written with Android Studio version 3.5.1 and the Android 10.0 SDK.</span></span> <span data-ttu-id="62eeb-106">本指南中的步骤可能适用于其他版本，但尚未经过测试。</span><span class="sxs-lookup"><span data-stu-id="62eeb-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="62eeb-107">使用 Outlook.com 上的邮箱的个人 Microsoft 帐户，或者是 Microsoft 工作或学校帐户。</span><span class="sxs-lookup"><span data-stu-id="62eeb-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="62eeb-108">如果你没有 Microsoft 帐户，可以使用以下几种方法获取免费帐户：</span><span class="sxs-lookup"><span data-stu-id="62eeb-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="62eeb-109">你可以[注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。</span><span class="sxs-lookup"><span data-stu-id="62eeb-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="62eeb-110">你可以[注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program)以获取免费的 office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="62eeb-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-an-application-with-the-azure-portal"></a><span data-ttu-id="62eeb-111">在 Azure 门户中注册应用程序</span><span class="sxs-lookup"><span data-stu-id="62eeb-111">Register an application with the Azure Portal</span></span>

1. <span data-ttu-id="62eeb-112">打开浏览器，并转到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。然后，使用**个人帐户**（亦称为“Microsoft 帐户”）或**工作或学校帐户**登录。</span><span class="sxs-lookup"><span data-stu-id="62eeb-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="62eeb-113">选择左侧导航栏中的“**Azure Active Directory**”，再选择“**管理**”下的“**应用注册**”。</span><span class="sxs-lookup"><span data-stu-id="62eeb-113">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="62eeb-114">应用注册的屏幕截图</span><span class="sxs-lookup"><span data-stu-id="62eeb-114">A screenshot of the App registrations</span></span> ](../../tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="62eeb-115">选择“新注册”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="62eeb-115">Select **New registration**.</span></span> <span data-ttu-id="62eeb-116">在“注册应用”\*\*\*\* 页上，按如下方式设置值。</span><span class="sxs-lookup"><span data-stu-id="62eeb-116">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="62eeb-117">将“名称”\*\*\*\* 设置为“`Android Graph Tutorial`”。</span><span class="sxs-lookup"><span data-stu-id="62eeb-117">Set **Name** to `Android Graph Tutorial`.</span></span>
    - <span data-ttu-id="62eeb-118">将“受支持的帐户类型”\*\*\*\* 设置为“任何组织目录中的帐户和个人 Microsoft 帐户”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="62eeb-118">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="62eeb-119">在 "**重定向 URI**" 下，将 dropdown 设置为 "**公用客户端/本机（移动 & 桌面）** "，并将值设置为`msauth://YOUR_PACKAGE_NAME/callback`，替换`YOUR_PACKAGE_NAME`为项目的包名称。</span><span class="sxs-lookup"><span data-stu-id="62eeb-119">Under **Redirect URI**, set the dropdown to **Public client/native (mobile & desktop)** and set the value to `msauth://YOUR_PACKAGE_NAME/callback`, replacing `YOUR_PACKAGE_NAME` with your project's package name.</span></span>

    !["注册应用程序" 页的屏幕截图](../../tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="62eeb-121">选择 "**注册**"。</span><span class="sxs-lookup"><span data-stu-id="62eeb-121">Select **Register**.</span></span> <span data-ttu-id="62eeb-122">在 " **Android Graph 教程**" 页上，复制**应用程序（客户端） ID**的值并保存它，下一步将需要它。</span><span class="sxs-lookup"><span data-stu-id="62eeb-122">On the **Android Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新应用注册的应用程序 ID 的屏幕截图](../../tutorial/images/aad-application-id.png)

## <a name="configure-the-sample"></a><span data-ttu-id="62eeb-124">配置示例</span><span class="sxs-lookup"><span data-stu-id="62eeb-124">Configure the sample</span></span>

1. <span data-ttu-id="62eeb-125">将`msal_config.json.example`文件重命名`msal_config.json`为，并将文件移动`GraphTutorial/app/src/main/res/raw`到目录中。</span><span class="sxs-lookup"><span data-stu-id="62eeb-125">Rename the `msal_config.json.example` file to `msal_config.json` and move the file into the `GraphTutorial/app/src/main/res/raw` directory.</span></span>
1. <span data-ttu-id="62eeb-126">编辑`msal_config.json`文件并进行以下更改。</span><span class="sxs-lookup"><span data-stu-id="62eeb-126">Edit the `msal_config.json` file and make the following changes.</span></span>
    1. <span data-ttu-id="62eeb-127">将`YOUR_APP_ID_HERE`替换为你从 Azure 门户获取的**应用程序 Id** 。</span><span class="sxs-lookup"><span data-stu-id="62eeb-127">Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the Azure portal.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="62eeb-128">运行示例</span><span class="sxs-lookup"><span data-stu-id="62eeb-128">Run the sample</span></span>

<span data-ttu-id="62eeb-129">在 Android Studio 中，选择 "**运行**" 菜单上的 **"运行 ' 应用程序 '"** 。</span><span class="sxs-lookup"><span data-stu-id="62eeb-129">In Android Studio, select **Run 'app'** on the **Run** menu.</span></span>
