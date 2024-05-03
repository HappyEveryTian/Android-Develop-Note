# 使用Fragment组成复杂界面

## 搭建App首页，一个Activity有多个Fragment，点击底部Tab切换Fragment，Fragment只显示一个文本即可，点击按钮跳转到另一个Fragment。

1. 在Activity中创建所需的跳转按钮和FragmentLayout容器

![layout](/homework/asset/homeworkImage_2/layout.png)

2. 创建要跳转到的Fragment，增加文字描述

![fragmentcontent](/homework/asset/homeworkImage_2/fragmentcontent.png)

3. 为跳转按钮设计Fragment切换效果，实现只有一个Fragment显示

![fragmentbutton](/homework/asset/homeworkImage_2/fragmentbutton.png)

### 成果展示：

点击addFragment1按钮，显示第一个Fragment

![addfragment1](/homework/asset/homeworkImage_2/addfragment1.png)

然后点击addFragment2按钮，隐藏第一个Fragment或者代替第一个Fragment，显示第二个Fragment

![addfragment2](/homework/asset/homeworkImage_2/addfragment2.png)

## 使用ViewPager实现Fragment左右滑动

1. Activity中创建viewpager布局

![viewpagercontent](/homework/asset/homeworkImage_2/viewpagercontent.png)

2. 创建要切换的Fragment，增加文字描述

![viewpagerfragment](/homework/asset/homeworkImage_2/viewpagerfragment.png)

3. 创建适配器来提供ViewPager显示的内容

![adapter](/homework/asset/homeworkImage_2/adapter.png)

4. 在Activity中设置适配器

![setadapter](/homework/asset/homeworkImage_2/setadapter.png)

### 成果展示

点击viewPager按钮，显示第一个Fragment

![viewpagerfragment1](/homework/asset/homeworkImage_2/viewpagerfragment1.png)

水平滑动屏幕，切换到第二个viewpagerFragment2，再次反方向滑动可以切换回viewpagerFragment1

![viewpagerfragment2](/homework/asset/homeworkImage_2/viewpagerfragment2.png)