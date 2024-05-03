# Fragment使用与避坑指南

## Activity弊端

- 复杂业务代码量巨大，Activity愈发臃肿，难以维护
- 页面模块难以复用，不适应大屏设备，开发效率低
- 启动Activity消耗资源多

## Fragment简介

- Fragment可以说是轻量级的Activity，是Android3.0新增的概念。

- Fragment不能独立存在，必须嵌入到Activity中，一个Activity可以嵌入多个Fragment。

- Fragment具有自己的生命周期，接收它自己的事件，并可以在Activity运行时被添加或删除。

- Fragment的生命周期直接受所在的Activity的影响。如：当Activity暂停时，它拥有的所有Fragment们都暂停。

## Fragment生命周期

- onAttach(): 当Fragment与Activity发生关联时调用。
- onCreate(): 创建Fragment时被回调。
- onCreatView(): 每次创建、绘制该Fragment的View组件时回调该方法。
- onActivityCreated(): 当Fragment所在的Activity被启动完成后回调该方法。
- onStart(): 启动Fragment时被回调，此时Fragment可见。
- onResume(): 恢复Fragment时被回调，获取焦点时回调。
- onPause(): 暂停Fragment时被回调，失去焦点时回调。
- onStop(): 停止Fragment时被回调，Fragment不可见时回调。
- onDestroyView(): 销毁与Fragment有关的视图，但为与Activity解除绑定。
- onDestory(): 销毁Fragment时被回调。
- onDetach(): 与onAttach()相对应，当Fragment与Activity关联被取消时调用。

## Fragment不同添加方式

### 1. 静态添加Fragment

- 创建Fragment子类，实现onCreatView()方法

![staticfragmentcreate](/image_day_2/staticfragmentcreate.png)

- 在layout文件夹下建立该Fragment对应的布局文件，并在第一步中引入布局

![staticfragmentlayout](/image_day_2/staticfragmentlayout.png)

### 2. 动态添加Fragment

- 创建Fragment子类，实现onCreatView()方法

![dynamicfragmentcreate](/image_day_2/dynamicfragmentcreate.png)

- 在layout文件夹下建该Fragment对应的布局文件，并在第一步中引入布局

![dynamicfragmentlayout](/image_day_2/dynamicfragmentlayout.png)

- 在Activity的XML布局文件中创建一个带id的布局管理器，用于动态创建Fragment时容纳Fragment

![fragmentcontainer](/image_day_2/fragmentcontainer.png)

- 在Activity里动态创建Fragment

![dynamicfragment](/image_day_2/dynamicfragment.png)

## FragmentTransaction

- FragmentManager提交的每组Fragment更改称为一个“事务”，可以使用 FragmentTransaction类提供的API指定在事务内需执行何种操作(add/remove/hide/show...)。

- 通过调用 beginTransaction()从FragmentManager 获取FragmentTransaction实例。

- 每个FragmentTransaction上的最终调用必须提交事务。commit()调用会向FragmentManager 发出信号，指明所有操作均已添加到事务中。

## Fragment事务操作类型

- add/remove: 添加和移除

- show/hide: 显示和隐藏，改变可见性而不影响生命周期

- replace: 替换

- attach/detach: 附加到Activity/从Activity分离，不改变Fragment状态

- setCustomAnimations: 设置过渡动画

- addToBackStack: 允许返回键回退事务

- commit/commitNow: 提交事务等待执行/立即执行

## 事务异常case

### 错误信息1：
- Can not perfomr this action after onSaveInstanceState

### 原因：
- 在错误的生命周期中调用了 commit 方法

### Fragment commit注意事项
- 不能在 onSaveInstanceState 之后的生命周期里面commit fragment
- 不要在子线程中 commit fragment，有可能发生已经走完 onSaveInstanceState 的情况

### 错误信息2：
- java.lang.llegalStateException: FragmentManager is already executing transactions

### 原因：
- 在事务执行过程中执行新的事务，onResume处于事务执行过程中
### Fragment commit注意事项
- 使用commit替代commitNow
- 手动将commitNow发送到主线程队列中

## Fragment事务操作
- add
    - 不会删除容器内已存在的Fragment
    - 原Fragment生命周期不受影响
    - 原Fragment会被保存和自动恢复
    - 内存占用多
    - 搭配hide/show使用
- replace
    - 删除容器内已存在的Fragment
    - 原Fragment被销毁
    - 原Fragment状态无法恢复
    - 内存占用少

## 事务提交的几种方式
- commit：非立刻执行，将消息发送到主线程队列等待执行需要立刻执行时配合executePendingTransactions将队列中所有事务全部执行

- commitNow：立刻仅执行当前事务，不能与addToBackStack同时使用

- commitAllowingStateLoss：onDestroy时提交不再抛出IegalStateException，而是丢弃提交的Fragment

- commitNowAllowingStateLoss：立刻执行

## Fragment与Activity通信

1. 在Fragment中定义一个回调接口

![fragmentinterface](/image_day_2/fragmentinterface.png)

2. 运行时获取借口实现

![fragmentinterface2](/image_day_2/fragmentinterface2.png)

3. Activity实现接口

![activityiimplement](/image_day_2/Activityiimplement.png)

## 构建滑动视图

1. Activity中创建viewpager布局

![viewpagercontent](/image_day_2/viewpagercontent.png)

2. 创建要切换的Fragment，增加文字描述

![viewpagerfragment](/image_day_2/viewpagerfragment.png)

3. 创建适配器来提供ViewPager显示的内容

![adapter](/image_day_2/adapter.png)

4. 在Activity中设置适配器

![setadapter](/image_day_2/setadapter.png)
