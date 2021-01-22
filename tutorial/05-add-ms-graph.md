<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="4a8b7-101">在此练习中，你将 Microsoft Graph 合并到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="4a8b7-102">对于此应用程序，你将使用 Microsoft [Graph SDK for Java](https://github.com/microsoftgraph/msgraph-sdk-java) 调用 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-102">For this application, you will use the [Microsoft Graph SDK for Java](https://github.com/microsoftgraph/msgraph-sdk-java) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="4a8b7-103">从 Outlook 获取日历事件</span><span class="sxs-lookup"><span data-stu-id="4a8b7-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="4a8b7-104">在此部分中，您将扩展类以添加一个函数，获取当前一周的用户事件，并 `GraphHelper` 更新为 `CalendarFragment` 使用这些新函数。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-104">In this section you will extend the `GraphHelper` class to add a function to get the user's events for the current week and update `CalendarFragment` to use these new functions.</span></span>

1. <span data-ttu-id="4a8b7-105">打开 **GraphHelper，** 将以下 `import` 语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-105">Open **GraphHelper** and add the following `import` statements to the top of the file.</span></span>

    ```java
    import com.microsoft.graph.options.Option;
    import com.microsoft.graph.options.HeaderOption;
    import com.microsoft.graph.options.QueryOption;
    import com.microsoft.graph.requests.extensions.IEventCollectionPage;
    import com.microsoft.graph.requests.extensions.IEventCollectionRequestBuilder;
    import java.time.ZonedDateTime;
    import java.time.format.DateTimeFormatter;
    import java.util.LinkedList;
    import java.util.List;
    ```

1. <span data-ttu-id="4a8b7-106">将以下函数添加到 `GraphHelper` 类。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-106">Add the following functions to the `GraphHelper` class.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/GraphHelper.java" id="GetEventsSnippet":::

    > [!NOTE]
    > <span data-ttu-id="4a8b7-107">考虑代码正在 `getCalendarView` 执行哪些工作。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-107">Consider what the code in `getCalendarView` is doing.</span></span>
    >
    > - <span data-ttu-id="4a8b7-108">将调用的 URL 为 `/v1.0/me/calendarview` 。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-108">The URL that will be called is `/v1.0/me/calendarview`.</span></span>
    >   - <span data-ttu-id="4a8b7-109">和 `startDateTime` `endDateTime` 查询参数定义日历视图的开始和结束。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-109">The `startDateTime` and `endDateTime` query parameters define the start and end of the calendar view.</span></span>
    >   - <span data-ttu-id="4a8b7-110">标头使 Microsoft Graph 返回用户时区中每个事件的开始时间 `Prefer: outlook.timezone` 和结束时间。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-110">the `Prefer: outlook.timezone` header causes the Microsoft Graph to return the start and end times of each event in the user's time zone.</span></span>
    >   - <span data-ttu-id="4a8b7-111">`select`该函数将每个事件返回的字段限制为仅视图将实际使用的字段。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-111">The `select` function limits the fields returned for each events to just those the view will actually use.</span></span>
    >   - <span data-ttu-id="4a8b7-112">该 `orderby` 函数按开始时间对结果进行排序。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-112">The `orderby` function sorts the results by start time.</span></span>
    >   - <span data-ttu-id="4a8b7-113">该 `top` 函数每页请求 25 个结果。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-113">The `top` function requests 25 results per page.</span></span>
    > - <span data-ttu-id="4a8b7-114">定义回调 () 检查是否有更多结果 `pagingCallback` 可用，并根据需要请求其他页面。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-114">A callback is defined (`pagingCallback`) to check if there are more results available and to request additional pages if needed.</span></span>

1. <span data-ttu-id="4a8b7-115">右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-115">Right-click the **app/java/com.example.graphtutorial** folder and select **New**, then **Java Class**.</span></span> <span data-ttu-id="4a8b7-116">命名类 `GraphToIana` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="4a8b7-116">Name the class `GraphToIana` and select **OK**.</span></span>

1. <span data-ttu-id="4a8b7-117">打开新文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-117">Open the new file and replace its contents with the following.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/GraphToIana.java" id="GraphToIanaSnippet":::

1. <span data-ttu-id="4a8b7-118">将以下 `import` 语句添加到 **CalendarFragment** 文件的顶部。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-118">Add the following `import` statements to the top of the **CalendarFragment** file.</span></span>

    ```java
    import android.util.Log;
    import android.widget.ListView;
    import com.google.android.material.snackbar.BaseTransientBottomBar;
    import com.google.android.material.snackbar.Snackbar;
    import com.microsoft.graph.concurrency.ICallback;
    import com.microsoft.graph.core.ClientException;
    import com.microsoft.graph.models.extensions.Event;
    import com.microsoft.identity.client.AuthenticationCallback;
    import com.microsoft.identity.client.IAuthenticationResult;
    import com.microsoft.identity.client.exception.MsalException;
    import java.time.DayOfWeek;
    import java.time.ZoneId;
    import java.time.ZonedDateTime;
    import java.time.temporal.ChronoUnit;
    import java.time.temporal.TemporalAdjusters;
    import java.util.List;
    ```

1. <span data-ttu-id="4a8b7-119">将以下成员添加到 `CalendarFragment` 类。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-119">Add the following member to the `CalendarFragment` class.</span></span>

    ```java
    private List<Event> mEventList = null;
    ```

1. <span data-ttu-id="4a8b7-120">将以下函数添加到 `CalendarFragment` 类中以隐藏和显示进度栏。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-120">Add the following functions to the `CalendarFragment` class to hide and show the progress bar.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/CalendarFragment.java" id="ProgressBarSnippet":::

1. <span data-ttu-id="4a8b7-121">添加以下函数，为中的 `getCalendarView` 函数提供回调 `GraphHelper` 。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-121">Add the following function to provide a callback for the `getCalendarView` function in `GraphHelper`.</span></span>

    ```java
    private ICallback<List<Event>> getCalendarViewCallback() {
        return new ICallback<List<Event>>() {
            @Override
            public void success(List<Event> eventList) {
                mEventList = eventList;

                // Temporary for debugging
                String jsonEvents = GraphHelper.getInstance().serializeObject(mEventList);
                Log.d("GRAPH", jsonEvents);

                hideProgressBar();
            }

            @Override
            public void failure(ClientException ex) {
                hideProgressBar();
                Log.e("GRAPH", "Error getting events", ex);
                Snackbar.make(getView(),
                    ex.getMessage(),
                    BaseTransientBottomBar.LENGTH_LONG).show();
            }
        };
    }
    ```

1. <span data-ttu-id="4a8b7-122">将类 `onCreateView` 中的现有 `CalendarFragment` 函数替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-122">Replace the existing `onCreateView` function in the `CalendarFragment` class with the following.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/CalendarFragment.java" id="OnCreateViewSnippet":::

    <span data-ttu-id="4a8b7-123">请注意此代码执行什么功能。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-123">Notice what this code does.</span></span> <span data-ttu-id="4a8b7-124">首先，它调用 `acquireTokenSilently` 获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-124">First, it calls `acquireTokenSilently` to get the access token.</span></span> <span data-ttu-id="4a8b7-125">每次需要访问令牌时调用此方法是一种最佳实践，因为它利用 MSAL 的缓存和令牌刷新功能。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-125">Calling this method every time an access token is needed is a best practice because it takes advantage of MSAL's caching and token refresh abilities.</span></span> <span data-ttu-id="4a8b7-126">在内部，MSAL 检查缓存令牌，然后检查其是否已过期。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-126">Internally, MSAL checks for a cached token, then checks if it is expired.</span></span> <span data-ttu-id="4a8b7-127">如果令牌存在且未过期，它将仅返回缓存的令牌。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-127">If the token is present and not expired, it just returns the cached token.</span></span> <span data-ttu-id="4a8b7-128">如果令牌已过期，它将尝试在返回令牌之前刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-128">If it is expired, it attempts to refresh the token before returning it.</span></span>

    <span data-ttu-id="4a8b7-129">检索令牌后，代码将调用该方法 `getCalendarView` ，获取用户的事件。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-129">Once the token is retrieved, the code then calls the `getCalendarView` method to get the user's events.</span></span>

1. <span data-ttu-id="4a8b7-130">运行应用、登录，然后点击菜单中的 **"** 日历"导航项。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-130">Run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="4a8b7-131">你应该在 Android Studio 的调试日志中看到事件的 JSON 转储。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-131">You should see a JSON dump of the events in the debug log in Android Studio.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="4a8b7-132">显示结果</span><span class="sxs-lookup"><span data-stu-id="4a8b7-132">Display the results</span></span>

<span data-ttu-id="4a8b7-133">现在，可以将 JSON 转储替换为某些内容，以用户友好的方式显示结果。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-133">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="4a8b7-134">在此部分中，您将向日历片段添加一个，为每个项目创建一个布局，然后为将每个字段映射到视图中相应的字段的自定义列表 `ListView` `ListView` `ListView` `Event` `TextView` 适配器。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-134">In this section, you will add a `ListView` to the calendar fragment, create a layout for each item in the `ListView`, and create a custom list adapter for the `ListView` that maps the fields of each `Event` to the appropriate `TextView` in the view.</span></span>

1. <span data-ttu-id="4a8b7-135">将 `TextView` 应用 **/res/layout/fragment_calendar.xml** 替换为 `ListView` 。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-135">Replace the `TextView` in **app/res/layout/fragment_calendar.xml** with a `ListView`.</span></span>

    :::code language="xml" source="../demo/GraphTutorial/app/src/main/res/layout/fragment_calendar.xml" highlight="6-11":::

1. <span data-ttu-id="4a8b7-136">右键单击 **应用/res/layout** 文件夹，然后选择 **"新建**"，然后选择 **"布局"资源文件**。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-136">Right-click the **app/res/layout** folder and select **New**, then **Layout resource file**.</span></span>

1. <span data-ttu-id="4a8b7-137">命名文件 `event_list_item` ，将 **根元素更改为** `RelativeLayout` ，然后选择 **"确定"。**</span><span class="sxs-lookup"><span data-stu-id="4a8b7-137">Name the file `event_list_item`, change the **Root element** to `RelativeLayout`, and select **OK**.</span></span>

1. <span data-ttu-id="4a8b7-138">打开 **event_list_item.xml** 文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-138">Open the **event_list_item.xml** file and replace its contents with the following.</span></span>

    :::code language="xml" source="../demo/GraphTutorial/app/src/main/res/layout/event_list_item.xml":::

1. <span data-ttu-id="4a8b7-139">右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-139">Right-click the **app/java/com.example.graphtutorial** folder and select **New**, then **Java Class**.</span></span>

1. <span data-ttu-id="4a8b7-140">命名类 `EventListAdapter` ，然后选择"**确定"。**</span><span class="sxs-lookup"><span data-stu-id="4a8b7-140">Name the class `EventListAdapter` and select **OK**.</span></span>

1. <span data-ttu-id="4a8b7-141">打开 **EventListAdapter** 文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-141">Open the **EventListAdapter** file and replace its contents with the following.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/EventListAdapter.java" id="EventListAdapterSnippet":::

1. <span data-ttu-id="4a8b7-142">打开 **CalendarFragment** 类，将以下函数添加到该类。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-142">Open the **CalendarFragment** class and add the following function to the class.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/CalendarFragment.java" id="AddEventsToListSnippet":::

1. <span data-ttu-id="4a8b7-143">将替代中的临时调试 `success` 代码替换为 `addEventsToList();` 。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-143">Replace the temporary debugging code from the `success` override with `addEventsToList();`.</span></span>

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/CalendarFragment.java" id="SuccessSnippet" highlight="5":::

1. <span data-ttu-id="4a8b7-144">运行应用、登录并点击 **日历导航** 项。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-144">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="4a8b7-145">应看到事件列表。</span><span class="sxs-lookup"><span data-stu-id="4a8b7-145">You should see the list of events.</span></span>

    ![事件表的屏幕截图](./images/calendar-list.png)
