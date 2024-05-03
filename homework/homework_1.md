# 1. 四种启动方式的生命周期

## 1.1 standard

![standard](/homework/asset/homeworkImage_1/standard.png)

- Activity的默认启动模式,每启动一个Activity就会在栈顶创建一个新的实例

## 1.2 singleTop

![singleTop](/homework/asset/homeworkImage_1/singleTop.png)

- 判断要启动的Activity实例是否位于栈顶，如果位于栈顶直接复用，否则创建新的实例。

## 1.3 singleTask

![singleTask](/homework/asset/homeworkImage_1/singleTask.png)

- 使Activity在整个应用程序中只有一个实例。每次启动Activity时系统首先检查栈中是否存在当前Activity实例，如果存在则直接复用，并把当前Activity之上所有实例全部栈。

## 1.4 singleInstance

![singleInstance](/homework/asset/homeworkImage_1/singleInstance.png)

- 该模式的Activity会启动一个新的任务栈来管理Activity实例，并且该实例在整个系统中只有一个。无论从那个任务栈中启动该Activity，都会是该Activity所在的任务栈转移到前台，从而Activity显示。

# 2. Service生命周期

## 2.1 startService

![startService](/homework/asset/homeworkImage_1/startService.png)

## 2.2 bindService

![bindService](/homework/asset/homeworkImage_1/bindService.png)

## 2.3 总结
- startService：
  
可以多次调用，但是onCreate()只执行一遍，也就是Service只会创建一次，每次调用onStartCommand都会被调用。该方式Service的生命周期为onCreate() -> onStartCommand()->onDestroy()。

- bindService:

只有第一次调用会创建Service,执行onCreate()和onBind()，连续多次调用并不会执行onCreate()和onBind()；生命周期为onCreate()->onBind()->onUnBind()->onDestroy()。

# 3. 广播

## 3.1 静态广播

3.1.1 创建广播接收器

![MyReceiver](/homework/asset/homeworkImage_1/MyReceiver.png)

3.1.2 在清单中注册广播接收器

![register](/homework/asset/homeworkImage_1/registerReceiver.png)

3.1.3 发送广播

![sendbroadcast](/homework/asset/homeworkImage_1/sendbroadcast.png)

实操成果:

![staitcresult](/homework/asset/homeworkImage_1/staticresult.png)

## 3.2 动态广播

3.2.1 创建广播接收器

![register](/homework/asset/homeworkImage_1/register.png)

3.2.2 增加发送按钮

![sendButton](/homework/asset/homeworkImage_1/sendButton.png)

3.2.3 注册广播并发送

![send](/homework/asset/homeworkImage_1/dynamicsend.png)

实操成果:

![dynamicresult](/homework/asset/homeworkImage_1/dynamicresult.png)

# 4. AIDL通信
4.1 使用AIDL定义接口

![AIDL](/homework/asset/homeworkImage_1/AIDL.png)

4.2 在服务端实现AIDL接口

![AIDLImplement](/homework/asset/homeworkImage_1/AIDLImplement.png)

4.3 绑定服务，获取接口实例

![BindAIDL](/homework/asset/homeworkImage_1/BindAIDL.png)

4.4 按钮实现远程方法

![AIDLButton](/homework/asset/homeworkImage_1/AIDLConnection.png)

实操成果：

![AIDLService](/homework/asset/homeworkImage_1/AIDLService.png)
