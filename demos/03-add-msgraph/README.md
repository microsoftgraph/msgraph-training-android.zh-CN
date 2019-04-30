# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="b95b9-101">如何运行已完成的项目</span><span class="sxs-lookup"><span data-stu-id="b95b9-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b95b9-102">先决条件</span><span class="sxs-lookup"><span data-stu-id="b95b9-102">Prerequisites</span></span>

<span data-ttu-id="b95b9-103">若要在此文件夹中运行已完成的项目, 您需要以下各项:</span><span class="sxs-lookup"><span data-stu-id="b95b9-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="b95b9-104">安装在开发计算机上的[Android Studio](https://developer.android.com/studio/) 。</span><span class="sxs-lookup"><span data-stu-id="b95b9-104">[Android Studio](https://developer.android.com/studio/) installed on your development machine.</span></span> <span data-ttu-id="b95b9-105">(**注意:** 本教程是使用 android Studio 版本3.3.1 在 1.8.0 JRE 和 Android 9.0 SDK 中编写的。</span><span class="sxs-lookup"><span data-stu-id="b95b9-105">(**Note:** This tutorial was written with Android Studio version 3.3.1 with the 1.8.0 JRE and the Android 9.0 SDK.</span></span> <span data-ttu-id="b95b9-106">本指南中的步骤可能适用于其他版本, 但尚未经过测试。</span><span class="sxs-lookup"><span data-stu-id="b95b9-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="b95b9-107">使用 Outlook.com 上的邮箱的个人 Microsoft 帐户, 或者是 microsoft 工作或学校帐户。</span><span class="sxs-lookup"><span data-stu-id="b95b9-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="b95b9-108">如果你没有 Microsoft 帐户, 可以使用以下几种方法获取免费帐户:</span><span class="sxs-lookup"><span data-stu-id="b95b9-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="b95b9-109">你可以[注册新的个人 Microsoft 帐户](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1)。</span><span class="sxs-lookup"><span data-stu-id="b95b9-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="b95b9-110">你可以[注册 office 365 开发人员计划](https://developer.microsoft.com/office/dev-program)以获取免费的 office 365 订阅。</span><span class="sxs-lookup"><span data-stu-id="b95b9-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-an-application-with-the-azure-portal"></a><span data-ttu-id="b95b9-111">在 Azure 门户中注册应用程序</span><span class="sxs-lookup"><span data-stu-id="b95b9-111">Register an application with the Azure Portal</span></span>

1. <span data-ttu-id="b95b9-112">打开浏览器，并转到 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。然后，使用**个人帐户**（亦称为“Microsoft 帐户”）或**工作或学校帐户**登录。</span><span class="sxs-lookup"><span data-stu-id="b95b9-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="b95b9-113">选择左侧导航栏中的“Azure Active Directory”\*\*\*\*，再选择“管理”\*\*\*\* 下的“应用注册(预览版)”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b95b9-113">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations (Preview)** under **Manage**.</span></span>

    ![<span data-ttu-id="b95b9-114">应用注册的屏幕截图</span><span class="sxs-lookup"><span data-stu-id="b95b9-114">A screenshot of the App registrations</span></span> ](../../tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="b95b9-115">选择“新注册”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b95b9-115">Select **New registration**.</span></span> <span data-ttu-id="b95b9-116">在“注册应用”\*\*\*\* 页上，按如下方式设置值。</span><span class="sxs-lookup"><span data-stu-id="b95b9-116">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="b95b9-117">将“名称”\*\*\*\* 设置为“`Android Graph Tutorial`”。</span><span class="sxs-lookup"><span data-stu-id="b95b9-117">Set **Name** to `Android Graph Tutorial`.</span></span>
    - <span data-ttu-id="b95b9-118">将“受支持的帐户类型”\*\*\*\* 设置为“任何组织目录中的帐户和个人 Microsoft 帐户”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b95b9-118">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="b95b9-119">保留“重定向 URI”\*\*\*\* 为空。</span><span class="sxs-lookup"><span data-stu-id="b95b9-119">Leave **Redirect URI** empty.</span></span>

    !["注册应用程序" 页的屏幕截图](../../tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="b95b9-121">选择“注册”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="b95b9-121">Choose **Register**.</span></span> <span data-ttu-id="b95b9-122">在 " **Xamarin Graph 教程**" 页上, 复制**应用程序 (客户端) ID**的值并保存它, 下一步将需要它。</span><span class="sxs-lookup"><span data-stu-id="b95b9-122">On the **Xamarin Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![新应用注册的应用程序 ID 的屏幕截图](../../tutorial/images/aad-application-id.png)

1. <span data-ttu-id="b95b9-124">选择 "**添加重定向 URI** " 链接。</span><span class="sxs-lookup"><span data-stu-id="b95b9-124">Select the **Add a Redirect URI** link.</span></span> <span data-ttu-id="b95b9-125">在 "**重定向 uri** " 页上, 找到 "**公共客户端 (移动、桌面)** " 部分的 "建议的重定向 uri" 部分。</span><span class="sxs-lookup"><span data-stu-id="b95b9-125">On the **Redirect URIs** page, locate the **Suggested Redirect URIs for public clients (mobile, desktop)** section.</span></span> <span data-ttu-id="b95b9-126">选择以开头`msal`和复制的 URI, 然后选择 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="b95b9-126">Select the URI that begins with `msal` and copy it, then choose **Save**.</span></span> <span data-ttu-id="b95b9-127">保存复制的重定向 URI, 在下一步中将需要它。</span><span class="sxs-lookup"><span data-stu-id="b95b9-127">Save the copied redirect URI, you will need it in the next step.</span></span>

    !["重定向 uri" 页的屏幕截图](../../tutorial/images/aad-redirect-uris.png)

## <a name="run-the-sample"></a><span data-ttu-id="b95b9-129">运行示例</span><span class="sxs-lookup"><span data-stu-id="b95b9-129">Run the sample</span></span>

<span data-ttu-id="b95b9-130">在 Android Studio 中, 选择 "**运行**" 菜单上的 **"运行 ' 应用程序 '"** 。</span><span class="sxs-lookup"><span data-stu-id="b95b9-130">In Android Studio, choose **Run 'app'** on the **Run** menu.</span></span>