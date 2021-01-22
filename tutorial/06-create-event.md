<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="41120-101">在此部分中，您将添加在用户日历上创建事件的能力。</span><span class="sxs-lookup"><span data-stu-id="41120-101">In this section you will add the ability to create events on the user's calendar.</span></span>

1. <span data-ttu-id="41120-102">打开 **GraphHelper，** 将以下 `import` 语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="41120-102">Open **GraphHelper** and add the following `import` statements to the top of the file.</span></span>

    ```java
    import com.microsoft.graph.models.extensions.Attendee;
    import com.microsoft.graph.models.extensions.DateTimeTimeZone;
    import com.microsoft.graph.models.extensions.EmailAddress;
    import com.microsoft.graph.models.extensions.ItemBody;
    import com.microsoft.graph.models.generated.AttendeeType;
    import com.microsoft.graph.models.generated.BodyType;
    ```

1. <span data-ttu-id="41120-103">将以下函数 `GraphHelper` 添加到类以创建新事件。</span><span class="sxs-lookup"><span data-stu-id="41120-103">Add the following function to the `GraphHelper` class to create a new event.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/GraphHelper.java" id="CreateEventSnippet":::

## <a name="update-new-event-fragment"></a><span data-ttu-id="41120-104">更新新事件片段</span><span class="sxs-lookup"><span data-stu-id="41120-104">Update new event fragment</span></span>

1. <span data-ttu-id="41120-105">右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。</span><span class="sxs-lookup"><span data-stu-id="41120-105">Right-click the **app/java/com.example.graphtutorial** folder and select **New**, then **Java Class**.</span></span> <span data-ttu-id="41120-106">命名类 `EditTextDateTimePicker` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="41120-106">Name the class `EditTextDateTimePicker` and select **OK**.</span></span>

1. <span data-ttu-id="41120-107">打开新文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="41120-107">Open the new file and replace its contents with the following.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/EditTextDateTimePicker.java" id="DateTimePickerSnippet":::

    <span data-ttu-id="41120-108">此类包装控件，在用户点击控件时显示日期和时间选取器，然后使用选取的日期和时间 `EditText` 更新值。</span><span class="sxs-lookup"><span data-stu-id="41120-108">This class wraps an `EditText` control, showing a date and time picker when the user taps it, and updating the value with the date and time picked.</span></span>

1. <span data-ttu-id="41120-109">打开 **应用/res/layout/fragment_new_event.xml** 并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="41120-109">Open **app/res/layout/fragment_new_event.xml** and replace its contents with the following.</span></span>

    :::code language="xml" source="../demo/GraphTutorial/app/src/main/res/layout/fragment_new_event.xml":::

1. <span data-ttu-id="41120-110">打开 **NewEventFragment，** 在文件顶部 `import` 添加以下语句。</span><span class="sxs-lookup"><span data-stu-id="41120-110">Open **NewEventFragment** and add the following `import` statements at the top of the file.</span></span>

    ```java
    import android.util.Log;
    import android.widget.Button;
    import com.google.android.material.snackbar.BaseTransientBottomBar;
    import com.google.android.material.snackbar.Snackbar;
    import com.google.android.material.textfield.TextInputLayout;
    import com.microsoft.graph.concurrency.ICallback;
    import com.microsoft.graph.core.ClientException;
    import com.microsoft.graph.models.extensions.Event;
    import com.microsoft.identity.client.AuthenticationCallback;
    import com.microsoft.identity.client.IAuthenticationResult;
    import com.microsoft.identity.client.exception.MsalException;
    import java.time.ZoneId;
    import java.time.ZonedDateTime;
    ```

1. <span data-ttu-id="41120-111">将以下成员添加到 `NewEventFragment` 类。</span><span class="sxs-lookup"><span data-stu-id="41120-111">Add the following members to the `NewEventFragment` class.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/NewEventFragment.java" id="InputsSnippet":::

1. <span data-ttu-id="41120-112">添加以下函数以显示和隐藏进度栏。</span><span class="sxs-lookup"><span data-stu-id="41120-112">Add the following functions to show and hide a progress bar.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/NewEventFragment.java" id="ProgressBarSnippet":::

1. <span data-ttu-id="41120-113">添加以下函数以从输入控件获取值并调用 `GraphHelper.createEvent` 函数。</span><span class="sxs-lookup"><span data-stu-id="41120-113">Add the following functions to get the values from the input controls and call the `GraphHelper.createEvent` function.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/NewEventFragment.java" id="CreateEventSnippet":::

1. <span data-ttu-id="41120-114">将现有的 `onCreateView` 替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="41120-114">Replace the existing `onCreateView` with the following.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/NewEventFragment.java" id="OnCreateViewSnippet":::

1. <span data-ttu-id="41120-115">保存更改并重新启动该应用。</span><span class="sxs-lookup"><span data-stu-id="41120-115">Save your changes and restart the app.</span></span> <span data-ttu-id="41120-116">选择 **"新建事件**"菜单项，填写表单，然后选择"**创建"。**</span><span class="sxs-lookup"><span data-stu-id="41120-116">Select the **New Event** menu item, fill in the form, and select **CREATE**.</span></span>

    ![应用程序中创建事件表单的屏幕截图](images/create-event.png)
