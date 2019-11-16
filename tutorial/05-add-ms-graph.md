<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ba109-101">在本练习中，将把 Microsoft Graph 合并到应用程序中。</span><span class="sxs-lookup"><span data-stu-id="ba109-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="ba109-102">对于此应用程序，您将使用[适用于 Java 的 Microsoft GRAPH SDK](https://github.com/microsoftgraph/msgraph-sdk-java)调用 microsoft graph。</span><span class="sxs-lookup"><span data-stu-id="ba109-102">For this application, you will use the [Microsoft Graph SDK for Java](https://github.com/microsoftgraph/msgraph-sdk-java) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="ba109-103">从 Outlook 获取日历事件</span><span class="sxs-lookup"><span data-stu-id="ba109-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="ba109-104">在本节中，您将扩展`GraphHelper`类以添加一个函数，以获取用户的事件并更新`CalendarFragment`以使用这些新函数。</span><span class="sxs-lookup"><span data-stu-id="ba109-104">In this section you will extend the `GraphHelper` class to add a function to get the user's events and update `CalendarFragment` to use these new functions.</span></span>

1. <span data-ttu-id="ba109-105">打开**microsoft.windowsazure.activedirectory.graphhelper**文件，并将以下`import`语句添加到文件顶部。</span><span class="sxs-lookup"><span data-stu-id="ba109-105">Open the **GraphHelper** file and add the following `import` statements to the top of the file.</span></span>

    ```java
    import com.microsoft.graph.options.Option;
    import com.microsoft.graph.options.QueryOption;
    import com.microsoft.graph.requests.extensions.IEventCollectionPage;
    import java.util.LinkedList;
    import java.util.List;
    ```

1. <span data-ttu-id="ba109-106">将以下函数添加到`GraphHelper`类中。</span><span class="sxs-lookup"><span data-stu-id="ba109-106">Add the following functions to the `GraphHelper` class.</span></span>

    ```java
    public void getEvents(String accessToken, ICallback<IEventCollectionPage> callback) {
        mAccessToken = accessToken;

        // Use query options to sort by created time
        final List<Option> options = new LinkedList<Option>();
        options.add(new QueryOption("orderby", "createdDateTime DESC"));


        // GET /me/events
        mClient.me().events().buildRequest(options)
                .select("subject,organizer,start,end")
                .get(callback);

    }

    // Debug function to get the JSON representation of a Graph
    // object
    public String serializeObject(Object object) {
        return mClient.getSerializer().serializeObject(object);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="ba109-107">考虑中`getEvents`的代码执行的操作。</span><span class="sxs-lookup"><span data-stu-id="ba109-107">Consider what the code in `getEvents` is doing.</span></span>
    >
    > - <span data-ttu-id="ba109-108">将调用的 URL 为`/v1.0/me/events`。</span><span class="sxs-lookup"><span data-stu-id="ba109-108">The URL that will be called is `/v1.0/me/events`.</span></span>
    > - <span data-ttu-id="ba109-109">`select`函数将为每个事件返回的字段限制为只 > 视图实际使用的字段。</span><span class="sxs-lookup"><span data-stu-id="ba109-109">The `select` function limits the fields returned for each events to just > those the view will actually use.</span></span>
    > - <span data-ttu-id="ba109-110">`QueryOption`指定的`orderby`名称用于按创建日期和时间对结果进行排序，最新项目最先开始。</span><span class="sxs-lookup"><span data-stu-id="ba109-110">The `QueryOption` named `orderby` is used to sort the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="ba109-111">将以下`import`语句添加到**CalendarFragment**文件的顶部。</span><span class="sxs-lookup"><span data-stu-id="ba109-111">Add the following `import` statements to the top of the **CalendarFragment** file.</span></span>

    ```java
    import android.util.Log;
    import android.widget.ListView;
    import android.widget.ProgressBar;
    import com.microsoft.graph.concurrency.ICallback;
    import com.microsoft.graph.core.ClientException;
    import com.microsoft.graph.models.extensions.Event;
    import com.microsoft.graph.requests.extensions.IEventCollectionPage;
    import com.microsoft.identity.client.AuthenticationCallback;
    import com.microsoft.identity.client.IAuthenticationResult;
    import com.microsoft.identity.client.exception.MsalException;
    import java.util.List;
    ```

1. <span data-ttu-id="ba109-112">将以下成员添加到`CalendarFragment`类中。</span><span class="sxs-lookup"><span data-stu-id="ba109-112">Add the following members to the `CalendarFragment` class.</span></span>

    ```java
    private List<Event> mEventList = null;
    private ProgressBar mProgress = null;
    ```

1. <span data-ttu-id="ba109-113">将以下函数添加到`CalendarFragment`类中，以隐藏和显示进度栏，以及在中`getEvents` `GraphHelper`为函数提供回调。</span><span class="sxs-lookup"><span data-stu-id="ba109-113">Add the following functions to the `CalendarFragment` class to hide and show the progress bar, and to provide a callback for the `getEvents` function in `GraphHelper`.</span></span>

    ```java
    private void showProgressBar() {
        getActivity().runOnUiThread(new Runnable() {
            @Override
            public void run() {
                mProgress.setVisibility(View.VISIBLE);
            }
        });
    }

    private void hideProgressBar() {
        getActivity().runOnUiThread(new Runnable() {
            @Override
            public void run() {
                mProgress.setVisibility(View.GONE);
            }
        });
    }

    private ICallback<IEventCollectionPage> getEventsCallback() {
        return new ICallback<IEventCollectionPage>() {
            @Override
            public void success(IEventCollectionPage iEventCollectionPage) {
                mEventList = iEventCollectionPage.getCurrentPage();

                // Temporary for debugging
                String jsonEvents = GraphHelper.getInstance().serializeObject(mEventList);
                Log.d("GRAPH", jsonEvents);

                hideProgressBar();
            }

            @Override
            public void failure(ClientException ex) {
                Log.e("GRAPH", "Error getting events", ex);
                hideProgressBar();
            }
        };
    }
    ```

1. <span data-ttu-id="ba109-114">重写`onCreate` `CalendarFragment`类中的函数，以从 Microsoft Graph 中获取用户的事件。</span><span class="sxs-lookup"><span data-stu-id="ba109-114">Override the `onCreate` function in the `CalendarFragment` class to get the user's events from Microsoft Graph.</span></span>

    ```java
    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        mProgress = getActivity().findViewById(R.id.progressbar);
        showProgressBar();

        // Get a current access token
        AuthenticationHelper.getInstance()
                .acquireTokenSilently(new AuthenticationCallback() {
                    @Override
                    public void onSuccess(IAuthenticationResult authenticationResult) {
                        final GraphHelper graphHelper = GraphHelper.getInstance();

                        // Get the user's events
                        graphHelper.getEvents(authenticationResult.getAccessToken(),
                                getEventsCallback());
                    }

                    @Override
                    public void onError(MsalException exception) {
                        Log.e("AUTH", "Could not get token silently", exception);
                        hideProgressBar();
                    }

                    @Override
                    public void onCancel() {
                        hideProgressBar();
                    }
                });
    }
    ```

<span data-ttu-id="ba109-115">请注意此代码执行的操作。</span><span class="sxs-lookup"><span data-stu-id="ba109-115">Notice what this code does.</span></span> <span data-ttu-id="ba109-116">首先，它调用`acquireTokenSilently`以获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="ba109-116">First, it calls `acquireTokenSilently` to get the access token.</span></span> <span data-ttu-id="ba109-117">每次需要访问令牌时调用此方法是一种最佳做法，因为它充分利用 MSAL 的缓存和令牌刷新能力。</span><span class="sxs-lookup"><span data-stu-id="ba109-117">Calling this method every time an access token is needed is a best practice because it takes advantage of MSAL's caching and token refresh abilities.</span></span> <span data-ttu-id="ba109-118">在内部，MSAL 检查缓存的令牌，然后检查它是否已过期。</span><span class="sxs-lookup"><span data-stu-id="ba109-118">Internally, MSAL checks for a cached token, then checks if it is expired.</span></span> <span data-ttu-id="ba109-119">如果令牌存在且未过期，它只返回缓存的令牌。</span><span class="sxs-lookup"><span data-stu-id="ba109-119">If the token is present and not expired, it just returns the cached token.</span></span> <span data-ttu-id="ba109-120">如果已过期，则它会在返回之前尝试刷新令牌。</span><span class="sxs-lookup"><span data-stu-id="ba109-120">If it is expired, it attempts to refresh the token before returning it.</span></span>

<span data-ttu-id="ba109-121">检索到令牌后，代码将调用`getEvents`方法以获取用户的事件。</span><span class="sxs-lookup"><span data-stu-id="ba109-121">Once the token is retrieved, the code then calls the `getEvents` method to get the user's events.</span></span>

<span data-ttu-id="ba109-122">您现在可以运行应用程序，登录，然后点击菜单中的 "**日历**" 导航项。</span><span class="sxs-lookup"><span data-stu-id="ba109-122">You can now run the app, sign in, and tap the **Calendar** navigation item in the menu.</span></span> <span data-ttu-id="ba109-123">您应该会在 Android Studio 的调试日志中看到事件的 JSON 转储。</span><span class="sxs-lookup"><span data-stu-id="ba109-123">You should see a JSON dump of the events in the debug log in Android Studio.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="ba109-124">显示结果</span><span class="sxs-lookup"><span data-stu-id="ba109-124">Display the results</span></span>

<span data-ttu-id="ba109-125">现在，您可以将 JSON 转储替换为以用户友好的方式显示结果的内容。</span><span class="sxs-lookup"><span data-stu-id="ba109-125">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="ba109-126">在本节中，您将向日历`ListView`片段中添加一个，为`ListView`中的每个项目创建一个布局，并为其创建自定义列表`ListView`适配器，以便将每个`Event`字段的字段`TextView`映射到视图中的相应字段。</span><span class="sxs-lookup"><span data-stu-id="ba109-126">In this section, you will add a `ListView` to the calendar fragment, create a layout for each item in the `ListView`, and create a custom list adapter for the `ListView` that maps the fields of each `Event` to the appropriate `TextView` in the view.</span></span>

1. <span data-ttu-id="ba109-127">将`TextView` in **app/res/layout/fragment_calendar .xml**替换为`ListView`。</span><span class="sxs-lookup"><span data-stu-id="ba109-127">Replace the `TextView` in **app/res/layout/fragment_calendar.xml** with a `ListView`.</span></span>

    ```xml
    <ListView
        android:id="@+id/eventlist"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:divider="@color/colorPrimary"
        android:dividerHeight="1dp" />
    ```

1. <span data-ttu-id="ba109-128">右键单击 "**应用/分辨率/布局**" 文件夹，然后选择 "**新建**"，然后选择 "**布局资源文件**"。</span><span class="sxs-lookup"><span data-stu-id="ba109-128">Right-click the **app/res/layout** folder and select **New**, then **Layout resource file**.</span></span>

1. <span data-ttu-id="ba109-129">将文件`event_list_item`命名，将**根元素**更改为`RelativeLayout`，然后选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="ba109-129">Name the file `event_list_item`, change the **Root element** to `RelativeLayout`, and select **OK**.</span></span>

1. <span data-ttu-id="ba109-130">打开**event_list_item .xml**文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ba109-130">Open the **event_list_item.xml** file and replace its contents with the following.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:padding="10dp">

        <TextView
            android:id="@+id/eventsubject"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Subject"
            android:textSize="20sp" />

        <TextView
            android:id="@+id/eventorganizer"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@id/eventsubject"
            android:text="Adele Vance"
            android:textSize="15sp" />

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@id/eventorganizer"
            android:orientation="horizontal">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:paddingEnd="2sp"
                android:text="Start:"
                android:textSize="15sp"
                android:textStyle="bold" />

            <TextView
                android:id="@+id/eventstart"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="1:30 PM 2/19/2019"
                android:textSize="15sp" />

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:paddingStart="5sp"
                android:paddingEnd="2sp"
                android:text="End:"
                android:textSize="15sp"
                android:textStyle="bold" />

            <TextView
                android:id="@+id/eventend"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="1:30 PM 2/19/2019"
                android:textSize="15sp" />
        </LinearLayout>
    </RelativeLayout>
    ```

1. <span data-ttu-id="ba109-131">右键单击 " **app/java/graphtutorial** " 文件夹，然后选择 "**新建**"，然后依次选择 " **java 类**"。</span><span class="sxs-lookup"><span data-stu-id="ba109-131">Right-click the **app/java/com.example.graphtutorial** folder and select **New**, then **Java Class**.</span></span>

1. <span data-ttu-id="ba109-132">命名该类`EventListAdapter`并选择 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="ba109-132">Name the class `EventListAdapter` and select **OK**.</span></span>

1. <span data-ttu-id="ba109-133">打开 " **EventListAdapter** " 文件，并将其内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="ba109-133">Open the **EventListAdapter** file and replace its contents with the following.</span></span>

    ```java
    package com.example.graphtutorial;

    import android.content.Context;
    import android.view.LayoutInflater;
    import android.view.View;
    import android.view.ViewGroup;
    import android.widget.ArrayAdapter;
    import android.widget.TextView;
    import androidx.annotation.NonNull;
    import com.microsoft.graph.models.extensions.DateTimeTimeZone;
    import com.microsoft.graph.models.extensions.Event;
    import java.time.LocalDateTime;
    import java.time.ZoneId;
    import java.time.ZonedDateTime;
    import java.time.format.DateTimeFormatter;
    import java.time.format.FormatStyle;
    import java.util.List;
    import java.util.TimeZone;

    public class EventListAdapter extends ArrayAdapter<Event> {
        private Context mContext;
        private int mResource;
        private ZoneId mLocalTimeZoneId;

        // Used for the ViewHolder pattern
        // https://developer.android.com/training/improving-layouts/smooth-scrolling
        static class ViewHolder {
            TextView subject;
            TextView organizer;
            TextView start;
            TextView end;
        }

        public EventListAdapter(Context context, int resource, List<Event> events) {
            super(context, resource, events);
            mContext = context;
            mResource = resource;
            mLocalTimeZoneId = TimeZone.getDefault().toZoneId();
        }

        @NonNull
        @Override
        public View getView(int position, View convertView, ViewGroup parent) {
            Event event = getItem(position);

            ViewHolder holder;

            if (convertView == null) {
                LayoutInflater inflater = LayoutInflater.from(mContext);
                convertView = inflater.inflate(mResource, parent, false);

                holder = new ViewHolder();
                holder.subject = convertView.findViewById(R.id.eventsubject);
                holder.organizer = convertView.findViewById(R.id.eventorganizer);
                holder.start = convertView.findViewById(R.id.eventstart);
                holder.end = convertView.findViewById(R.id.eventend);

                convertView.setTag(holder);
            } else {
                holder = (ViewHolder) convertView.getTag();
            }

            holder.subject.setText(event.subject);
            holder.organizer.setText(event.organizer.emailAddress.name);
            holder.start.setText(getLocalDateTimeString(event.start));
            holder.end.setText(getLocalDateTimeString(event.end));

            return convertView;
        }

        // Convert Graph's DateTimeTimeZone format to
        // a LocalDateTime, then return a formatted string
        private String getLocalDateTimeString(DateTimeTimeZone dateTime) {
            ZonedDateTime localDateTime = LocalDateTime.parse(dateTime.dateTime)
                    .atZone(ZoneId.of(dateTime.timeZone))
                    .withZoneSameInstant(mLocalTimeZoneId);

            return String.format("%s %s",
                    localDateTime.format(DateTimeFormatter.ofLocalizedDate(FormatStyle.MEDIUM)),
                    localDateTime.format(DateTimeFormatter.ofLocalizedTime(FormatStyle.SHORT)));
        }
    }
    ```

1. <span data-ttu-id="ba109-134">打开**CalendarFragment**类，并将以下函数添加到类中。</span><span class="sxs-lookup"><span data-stu-id="ba109-134">Open the **CalendarFragment** class and add the following function to the class.</span></span>

    ```java
    private void addEventsToList() {
        getActivity().runOnUiThread(new Runnable() {
            @Override
            public void run() {
                ListView eventListView = getView().findViewById(R.id.eventlist);

                EventListAdapter listAdapter = new EventListAdapter(getActivity(),
                        R.layout.event_list_item, mEventList);

                eventListView.setAdapter(listAdapter);
            }
        });
    }
    ```

1. <span data-ttu-id="ba109-135">在`success`重写中的`mEventList = iEventCollectionPage.getCurrentPage();`行后添加以下代码行。</span><span class="sxs-lookup"><span data-stu-id="ba109-135">Add the following line of code in the `success` override after the `mEventList = iEventCollectionPage.getCurrentPage();` line.</span></span>

    ```java
    addEventsToList();
    ```

1. <span data-ttu-id="ba109-136">运行应用程序，登录，然后点击 "**日历**" 导航项。</span><span class="sxs-lookup"><span data-stu-id="ba109-136">Run the app, sign in, and tap the **Calendar** navigation item.</span></span> <span data-ttu-id="ba109-137">您应该会看到事件列表。</span><span class="sxs-lookup"><span data-stu-id="ba109-137">You should see the list of events.</span></span>

    ![事件表的屏幕截图](./images/calendar-list.png)
