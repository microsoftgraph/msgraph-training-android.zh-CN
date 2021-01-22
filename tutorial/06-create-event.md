<!-- markdownlint-disable MD002 MD041 -->

在此部分中，您将添加在用户日历上创建事件的能力。

1. 打开 **GraphHelper，** 将以下 `import` 语句添加到文件顶部。

    ```java
    import com.microsoft.graph.models.extensions.Attendee;
    import com.microsoft.graph.models.extensions.DateTimeTimeZone;
    import com.microsoft.graph.models.extensions.EmailAddress;
    import com.microsoft.graph.models.extensions.ItemBody;
    import com.microsoft.graph.models.generated.AttendeeType;
    import com.microsoft.graph.models.generated.BodyType;
    ```

1. 将以下函数 `GraphHelper` 添加到类以创建新事件。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/GraphHelper.java" id="CreateEventSnippet":::

## <a name="update-new-event-fragment"></a>更新新事件片段

1. 右键单击 **app/java/com.example.graphtu一l** 文件夹，然后选择"新建 **"，Java类**。 命名类 `EditTextDateTimePicker` ，然后选择"**确定"。**

1. 打开新文件，并将其内容替换为以下内容。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/EditTextDateTimePicker.java" id="DateTimePickerSnippet":::

    此类包装控件，在用户点击控件时显示日期和时间选取器，然后使用选取的日期和时间 `EditText` 更新值。

1. 打开 **应用/res/layout/fragment_new_event.xml** 并将其内容替换为以下内容。

    :::code language="xml" source="../demo/GraphTutorial/app/src/main/res/layout/fragment_new_event.xml":::

1. 打开 **NewEventFragment，** 在文件顶部 `import` 添加以下语句。

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

1. 将以下成员添加到 `NewEventFragment` 类。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/NewEventFragment.java" id="InputsSnippet":::

1. 添加以下函数以显示和隐藏进度栏。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/NewEventFragment.java" id="ProgressBarSnippet":::

1. 添加以下函数以从输入控件获取值并调用 `GraphHelper.createEvent` 函数。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/NewEventFragment.java" id="CreateEventSnippet":::

1. 将现有的 `onCreateView` 替换为以下内容。

    :::code language="java" source="../demo/GraphTutorial/app/src/main/java/com/example/graphtutorial/NewEventFragment.java" id="OnCreateViewSnippet":::

1. 保存更改并重新启动该应用。 选择 **"新建事件**"菜单项，填写表单，然后选择"**创建"。**

    ![应用程序中创建事件表单的屏幕截图](images/create-event.png)
