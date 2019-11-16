# <a name="microsoft-graph-training-module---build-android-native-apps-with-the-microsoft-graph-java-sdk"></a>Microsoft Graph 培训模块-使用 Microsoft Graph Java SDK 构建 Android 本机应用

本模块将介绍如何通过构建本机移动 Android 应用程序，使用 Microsoft Graph SDK 来访问 Office 365 中的数据。

## <a name="lab---build-android-native-apps-with-the-microsoft-graph-java-sdk"></a>Lab-使用 Microsoft Graph Java SDK 生成 Android 本机应用

在此实验室中，将使用 Azure AD v2 身份验证终结点和 Microsoft 身份验证库（MSAL）创建 Android 应用程序，以使用 Microsoft Graph 访问 Office 365 中的数据。

- [Android Microsoft Graph 教程](https://docs.microsoft.com/graph/tutorials/android)

## <a name="demos"></a>演示

此存储库中的[演示](./demos)目录包含与完成教程的各个部分对应的项目的副本。 如果只想演示教程的某个特定部分，则可以从上一节中的版本开始。

- [01-创建-应用](demos/01-create-app)：已完成[创建 Android 应用](https://docs.microsoft.com/graph/tutorials/android?tutorial-step=1)
- [02-添加-aad-auth](demos/02-add-aad-auth)：已完成[添加 Azure AD 身份验证](https://docs.microsoft.com/graph/tutorials/android?tutorial-step=3)
- [03-外接 msgraph](demos/03-add-msgraph)：已完成[获取日历数据](https://docs.microsoft.com/graph/tutorials/android?tutorial-step=4)

## <a name="completed-sample"></a>已完成示例

如果只想使用此实验室生成已完成的示例，可以在此处找到它。

- [已完成项目](demos/03-add-msgraph)

## <a name="watch-the-module"></a>观看模块

此模块已记录并在 Office 开发 YouTube 频道中可用：[使用 Microsoft Graph JAVA SDK 生成 Android 本机应用](https://youtu.be/BLmOmv4FSsQ)

## <a name="contributors"></a>参与者

| 角色                | 作者（s）                                               |
| -------------------- | ------------------------------------------------------- |
| 实验室手册/幻灯片 | Andrew Connell （Microsoft MVP，Voitanos） @andrewconnell |
| 代码                 | Jason 约翰（Microsoft） @jasonjohmsft                |
| 承办人/支持    | Yina Arenas （Microsoft） @yinaa                          |

## <a name="version-history"></a>版本历史记录

| 版本 | 日期               | 注释                                                                   |
| ------- | ------------------ | -------------------------------------------------------------------------- |
| 1.9     | 2019年11月13日  | 使用 androidx 项目和最新的 Android SDK MSAL、Graph SDK 重新创建的项目 |
| 1.8     | 2019年6月18日      | 更新了用于刷新截屏视频录制的自述文件                           |
| 1.7     | 2019年3月30日     | FY2019Q4 内容刷新                                                   |
| 1.6     | 2019 年 2 月 20 日  | 更新为 docs.microsoft.com 格式                                       |
| 1.5     | 2019 年 2 月 12 日  | 更新了多个依赖项的应用季度刷新                    |
| 1.4     | 2018年11月8日   | 更新了 Graph Java SDK 以应用于 GA v1 & 季度刷新                |
| 1.3     | 2018 年 9 月 12 日 | 将 Graph Android SDK 替换为 Graph Java SDK & 应用季度刷新 |
| 1.2     | 2018年6月28日      | 添加了截屏视频。                                                          |
| 1.1     | 2018年6月22日      | 重写以使用最新的指南。                                          |
| 1.0     | 约2017年11月24日 | 添加与 Microsoft Graph 相关的产品 breakouts。                             |

## <a name="disclaimer"></a>免责声明

**此代码_按_原样提供，无需任何明示或暗示的担保，包括对特定目的适用性、适销性或不侵权的任何暗示担保。**

<!-- markdownlint-disable MD033 -->
<img src="https://telemetry.sharepointpnp.com/msgraph-training-android" />
