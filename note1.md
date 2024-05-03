# 四大组件生命周期

## 1. Activity

### 1.1 Activity概念

Activity 是一个可视化的用户界面，负责创建一个屏幕窗口，放置 UI 组件，供用户交互。

### 1.2 Activity创建

右击包名——New——Activity——Empty Activity，会看到类似于下面的界面，输入Activity和布局的名字，☑️Generate a Layout 后，Android系统会自动为我们创建布局，且在AndroidManifest.xml文件中自动注册当前Activity。

![activity](/image_day_1/activity.png)

### 1.3 Activity生命周期

![lifecycle](/image_day_1/lifecycle.jpeg)

### 1.4 Activity四种启动方式

1. Standard 标准启动模式

这种模式下每开启一个新的Activity，都会被放置在任务栈的栈顶，不存在复用。

![standard](/image_day_1/standard.png)

2. SingleTop 启动模式

这种模式下，如果栈顶已经存在了要开启的Activity，系统就不会重复创建了，而是利用这个已经存在的Activity，只复用栈顶的Activity。

![standard](/image_day_1/singletop.png)

3. SingleTask 启动模式

这种模式下，它要求当前Activity只会在任务栈存在一个实例，如果要开启的 Activity已经在任务栈中，系统会直接复用这个已经存在的Activity，并清空这个 Activity上面所有的栈引用，复用所有已存在的Activity。


![singleTask](/image_day_1/singletask.png)

4. SingleInstance 启动模式

这种模式下，系统会创建一个单独的任务栈，这个任务栈里只有它自己，并且在整个手机操作系统内存里，它是唯一的。比如打电话时的通话界面，全局唯一。
![singleinstance](/image_day_1/singleinstance.png)

### 1.5 Intent

Intent是Activity，Service和BroadcastReceiver这三个应用组件之间进行通信的信使。

1. 显式Intent

    通过组件名指定启动的目标组件,比如startActivity(new Intent(A.this,B.class)); 每次启动的组件只有一个

2. 隐式Intent

    不指定组件名,而指定Intent的Action,Data,或Category,当我们启动组件时, 会去匹配AndroidManifest.xml相关组件的Intent-filter,逐一匹配出满足属性的组件,当不止一个满足时, 会弹出一个让我们选择启动哪个的对话框

![intent](/image_day_1/intentstart.png)

![intent](/image_day_1/intent.png)

## 2. Service

### 2.1 Service概述

Service(服务)是一个一种可以在后台执行长时间运行操作而没有用户界面的应用组件。服务可由其他应用组件启动（如Activity），服务一旦被启动将在后台一直运行，即使启动服务的组件（Activity）已销毁也不受影响。 此外，组件可以绑定到服务，以与之进行交互，甚至是执行进程间通信 (IPC)。

### 2.2 启动Service及其生命周期

1. 创建MyService子类，必须继承Service类，然后重写onBind()方法，在此方法的实现中，必须返回 一个IBinder 接口的实现类，供客户端用来与服务进行通信。无论是启动状态还是绑定状态，此方法必须重写，但在启动状态的情况下直接返回 null。

![myservice](/image_day_1/myservice.png)

2. 在AndroidManifest.xml中声明

![servicemanifest](/image_day_1/servicemanifest.png)

3. 在程序中启动Service或停止

![startservice](/image_day_1/startservice.png)

4. 生命周期

![startservicelifecycle](/image_day_1/startservicelifecycle.png)

### 2.3 绑定Service及其生命周期

绑定服务是Service的另一种变形，当Service处于绑定状态时，其代表着客户端-服务器接口中的服务器。当其他组件（如 Activity）绑定到服务时（有时我们可能需要从Activity组建中去调用Service中的方法，此时Activity以绑定的方式挂靠到Service后，我们就可以轻松地方法到Service中的指定方法），组件（如Activity）可以向Service（也就是服务端）发送请求，或者调用Service（服务端）的方法，此时被绑定的Service（服务端）会接收信息并响应，甚至可以通过绑定服务进行执行进程间通信 (即IPC，这个后面再单独分析)。与启动服务不同的是绑定服务的生命周期通常只在为其他应用组件(如Activity)服务时处于活动状态，不会无限期在后台运行，也就是说宿主(如Activity)解除绑定后，绑定服务就会被销毁。

1. 创建MyService子类并在AndroidManifest.xml声明，提供一个 IBinder接口的实现类，该类用以提供客户端用来与服务进行交互的编程接口，该接口可以通过三种方法定义接口(同上)。

2. 在客户端中创建一个ServiceConnection对象，该代表与服务的连接，它只有两个方法， onServiceConnected和onServiceDisconnected，其含义如下：

- onServiceConnected(ComponentName name, IBinder service)

系统会调用该方法以传递服务的　onBind() 方法返回的 IBinder。其中service便是服务端返回的IBinder实现类对象，通过该对象我们便可以调用获取LocalService实例对象，进而调用服务端的公共方法。而ComponentName是一个封装了组件(Activity, Service, BroadcastReceiver, or ContentProvider)信息的类，如包名，组件描述等信息，较少使用该参数。

- onServiceDisconnected(ComponentName name)

Android 系统会在与服务的连接意外中断时（例如当服务崩溃或被终止时）调用该方法。注意:当客户端取消绑定时，系统“绝对不会”调用该方法。

![serviceconnection](/image_day_1/serviceconnection.png)

3. 绑定服务到当前Activity上，绑定服务是通过通过bindService()方法，解绑服务则使用unbindService()方法，这两个方法解析如下：

- bindService(Intent service, ServiceConnection conn, int flags)

该方法执行绑定服务操作，其中Intent是我们要绑定的服务(也就是LocalService)的意图，而ServiceConnection代表与服务的连接，它只有两个方法，flags则是指定绑定时是否自动创建Service。0代表不自动创建、BIND_AUTO_CREATE则代表自动创建。

- unbindService(ServiceConnection conn)

该方法执行解除绑定的操作，其中ServiceConnection代表与服务的连接。

![bindservice](/image_day_1/bindservice.png)

4. 生命周期

![bindservicelifecycle](/image_day_1/bindservicelifecycle.png)

## 3. BroadcastReceiver

### 3.1 BroadcastReceiver介绍

BroadcastReceiver（广播接收器）是一种用于接收和相应广播消息的组件。广播消息可以由系统、应用程序或其他组件发送，而BroadcastReceiver负责接收并处理这些消息。

### 3.2 BroadcastReceiver注册方式

广播接收器使用分为两部分:

1. 注册广播接收器:在 AndroidManifest.xm 文件中声明广播接收器，或者通过代码动态注册广播接收器。这样系统或其他应用程序发送匹配的广播时，广播接收器就会被激活。

2. 处理广播:广播接收器在接收到广播时，会调用其onReceive(Context context,Intentintent)方法。在这个方法中，可以处理接收到的广播，例如读取广播中的数据、执行特定操作或触发其他组件的响应。

### 3.3 BroadcastReceiver使用

1. 静态注册:

    静态注册是在 AndroidManifest.xml 文件中声明广播接收器。这意味着广播接收器在应用程序安装时就被注册，不需要在运行时手动注册或注销。

    静态注册适用于监听全局广播或在应用程序的整个生命周期内都需要接收广播的场景。当应用程序处于非运行状态时静态注册的广播接收器仍然可以接收到广播。

* 创建receiver类
![staticregister](/image_day_1/staticregister.png)
* 在清单文件中声明
![staticreceivermanifest](/image_day_1/staticreceiverregister.png)
* 发送广播
![sendstaticbroadcast](/image_day_1/sendstaticbroadcast.png)

2. 动态注册:

    动态注册是在代码中通过 Java 来注册广播接收器。这意味着广播接收器在运行时需要手动注册和注销，通常是在特定的时刻注册或在特定的页面/组件中注册。
        
    动态注册适用于临时性的广播接收需求，比如只在特定条件下监听广播，或者在特定 Activity/Fragment 中监听广播。

* 创建receiver类
![dynamicregister](/image_day_1/dynamicregister.png)
* 动态注册
![dynamicreveiverregister](/image_day_1/dynamicreceiverregister.png)
* 发送广播
![senddynamicbroadcast](/image_day_1/senddynamicbroadcast.png)

### 3.4 BroadcastReceiver避坑指南

- 如果不需要向应用以外的组件发送广播，则可以使用支持库中提供的LocalBroadcastManager 来收发本地广播。LocalBroadcastManager 效率更高(无需进行进程间通信)，并且您无需考虑其他应用在收发您的广播时带来的任何安全问题。

- 许多应用在其清单中注册接收相同的广播，可能会导致系统启动大量应用，从而对设备性能和用户体验造成严重影响。为避免发生这种情况，谱优先使用动态注册而不是静态注册。

- 由于接收器的 onReceive(Context,Intent)方法在主线程上运行，因此它会快速执行并返回。如果您需要执行长时间运行的工作，请谨慎生成线程或启动后台服务，因为系统可能会在onBeceive()返回后终止整个进程.

## 4. ContentProvider

### 4.1 ContentProvider简介

Content Provider(内容提供者)是一种用于管理应用程序数据的组件。ContentProvider允许应用程序共享数据给其他应用程序，并提供了一种标准化的接口，用于对数据进行查询、插入、更新和删除等
    操作。

### 4.2 Uri介绍

- 通用资源标志符（Universal Resource Identifier，简称"URI"）。

- Uri代表要操作的数据，Android上可用的每种资源、图像、视频片段等都可以用Uri来表示。
    
- 从概念上来讲，URI包括URL。

### 4.3 Uri组成

- URI主要分三个部分：scheme，authority 和 path。

- 其中authority又分为host和port。格式如下sheme://host:port/path

![uri组成](/image_day_1/uri.png)

### 4.4 ContentResolver常用方法

ContentResolver负贵与ContentProvider进行通信:

查询数据:

- query(Uri uri, Stringl projection, String selection，String[] selectionArgs, String sortOrder): 查询指定URI的数据，并返回一个Cursor对象，可以通过Cursor来遍历查询结果。

- query(Uri uri, Stringl projection, Bundle queryArgs, CancellationSignal cancellationSignal): 支持使用Bundle参数和取消信号进行查询。

插入数据:

- insert(Uri uri, ContentValues values): 向指定URI插入一条新数据，并返回新插入数据的URI。

- bulkInsert(Uri uri,ContentValues[]values): 批量插入多条数据。

查询数据:

- update(Uri uri, ContentValues values,String selection,Stringl selectionArgs):更新指定URI的数据，并返回受影响的行数。

删除数据:

- delete(Uri uri,String selection,String selectionArgs):删除指定URI的数据，并返回受影响的行数。

注册和发送:

- registerContentObserver(Uri uri, boolean notifyForDescendants, ContentObserver observer): 注册一个ContentObserver对象，用于监听指定URI数据的变化。

- unregisterContentObserver(ContentObserver observer):取消注册ContentObserver对象。

- notifyChange(Uri uri, ContentObserver observer,boolean syncToNetwork):发送指定URI数据变化的通知。

### 4.5 ContentResolver避坑指南

**权限申请**: 要访问联系人数据，需要在清单文件中请求相应的权限，例如READ_CONTACTS。在 Android 6.0(API级别23)及更高版本中，可能需要在运行时请求这些权限。

**异步加载**: 联系人数据的读取可能是一个耗时的操作，特别是在通讯录中包含大量联系人的情况下。建议使用异步加载机制(例如 AsyncTask或 Loader)来在后台线程中加载数据，以避免主线程的阻塞。

**Cursor生命周期**: 确保正确地处理Cursor对象的生命周期，及时关闭它，以避免内存泄漏和不必要的资源占用。

**缓存结果**: 如果你的应用频繁读取相同的联系人数据，考虑使用缓存来避免多次查询。这可以提高性能并减少对数据库的访问次数。

**错误处理**: 对于读取联系人数据的操作，要适当地处理错误情况。例如，在使用ContentResolver 查询时，要检查返回的 Cursor 是否为 null。