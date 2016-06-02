---
title: about me
date: 
---



# 个人信息


 - 技术博客：[http://www.jianshu.com/users/f543a4f0c9cc/latest_articles](http://www.jianshu.com/users/f543a4f0c9cc/latest_articles)
 - 个人网站：[http://never615.com](http://never615.com)
 - github：[https://github.com/never615](https://github.com/never615)



# 工作经历
任职时间 | 公司| 职责 
---|---|---
2015.09-至今 | [深圳墨兔科技有限公司](http://www.mall-to.com) | android客户端开发&后端开发
2015.07-2015.09 | [深圳市个联科技有限公司](http://igelian.com/)| androidSDK&客户端Demo开发
2014.12-2015.06 | [深圳市虾逛互动有限公司](http://baike.baidu.com/link?url=haAS96Am7c6H8GTcaXSSfU_eFg7T9ESsgx27II2scT3hpBFTzc1ISxufMgTGeIR5bZxHPW-zNOskgkE6vuOgCTfYkI_Q9rYQQxsvkF8wXkC) |android 客户端开发


## 深圳墨兔科技有限公司 

### 招呼app
[招呼android客户端](http://sj.qq.com/myapp/detail.htm?apkName=com.mallto.seaworld) 

此项目相关总结:[http://www.jianshu.com/p/8133f1e58371](http://www.jianshu.com/p/8133f1e58371)

我在此项目中主要负责了项目工作量的预估安排、项目架构的搭建和开发中问题的解决。功能模块主要负责地图、定位和导航模块等。项目的更详细总结请参考上方链接。熟悉整个项目的开发流程，能够有效推动项目的进行，协同同组开发人员。

自己实现了导航模块的相关最短路径算法，定位模块使用jni调用定位相关的c代码。UI相关如自己实现了地图上弹出气泡的的操作等。提供了跨层跨空间导航的实现思路，并完成相关的工具代码。

项目结构参考the clean architecture，分为表现层（使用MVP）、用例层和数据层。大量使用面向接口编程，在需要实现相关模块时，首先思考具体功能，使用抽象的方法完成所有表现层和具体业务层的逻辑，这样有助于理清思路，项目的结构也比较清晰，然后具体的实现可以分发给不同的人完成也可以很好的协同合作。

### SDK开发
进行室内定位、地图、导航SDK的设计，并大体完成定位SDK的封装、相关的开发文档、jcenter仓库的部署和使用docker搭建自己的私服仓库。因公司业务的需要，后续SDK暂时没有继续封装。

### 招呼后端和花园城微信后端开发

后端主要使用php开发，负责招呼客户端和后台管理端对应后台的部分功能开发、维护和定位、导航相关模块的java jar包的封装，使用gcc编译了linux平台下需要使用的定位so库，使用git配合钩子实现项目的不同环境的部署。

负责服务器环境的搭建和维护，负责花园城微端项目的后端开发，并对接协同第三方开发方并提供接口文档。


 
## 深圳市个联科技有限公司 

### androidSDK和Demo的开发
智能家居相关的项目，我主要负责androidSDK和客户端Demo的开发，主要使用socket通信、广播和进程间通信的相关知识，在局域网环境中可以直接控制设备、有网条件下可以通过移动网络经过服务器控制设备。此外还深入参与产品做法相关的讨论并提出了一种针对家庭和公司环境的技术设计方案。

Demo主要完成了用户的注册、登录、设备与用户账户的绑定与解绑。SmartConfig配置设备联网、扫描发现设备、对不同型号协议设备的局域网控制和经过服务器网络的进行控制。


## 深圳市虾逛互动有限公司

### 虾逛android客户端的开发
这个项目是我做的第一个商业项目同时也是我的毕设项目，所以我介绍多一点。

项目描述：
主要功能：
1. 商场室内地图查询2. 商场室内导航3. 停车场寻车4. 查询商场的活动、位置和热门店铺5. 查询店铺团购、独家优惠和店铺位置6. 离线地图管理
项目的用户用例图：

<img src="/res/用例图.png" title="a">

技术要点：
本系统根据三层架构（3-tier architecture）设计思想来构建系统，大体上分为显示层，业务逻辑层和数据访问层。主要技术难点在于室内定位和室内导航的部分。包括定位算法的的选择和处理，如使用基站法和三角定位的处理，信号的平滑处理等；导航方面的路径规划，也就是最短路径的算法的处理等。Android中的技术点，比如fragment的使用、上拉加载、屏幕适配等等应用层的基本技术点不一一描述了。
项目中的作用：
从最初项目架构的搭建、同组协同开发分配任务、到项目中众多难点的解决、路径规划算法的完成，到最后的测试发布，都是我负责的。


# 技术文章

- [使用Retrofit和Okhttp实现网络缓存。无网读缓存，有网根据过期时间重新请求](http://www.jianshu.com/p/9c3b4ea108a7)
- [android手机适配方案](http://www.cnblogs.com/never615/p/4444298.html) 

# 技能清单

以下均为我熟练使用的技能

- Web开发：PHP/java
- Web框架：Laravel/Dropwizard
- 前端开发：android
- android架构：clean架构/mvp/mvvm/领域驱动设计
- android库：Rxjava/dagger2/greendao/okhttp/retrofit/androidEventBus/glide等
- 数据库相关：PgSQL/SQLite
- 版本管理、文档和自动化部署工具：Svn/Git/git flow/API-Blueprint/Composer/gradle
- 云和开放平台：阿里云/微信应用开发
- 服务器:基本的linux命令/环境搭建/systemd使用等

android方面：

- 熟练使用LeanCloud、mapbox、友盟等各种第三方平台
- 熟悉toolbar、cardview、recyclerview、FAB和新的动画效果主题的使用
- 熟练掌握Android下的屏幕适配和百分比适配
- 熟练掌握Handler消息机制，进程间通信，AIDL的IPC机制调用远程服务
- 熟练掌握Android中事件的分发机制，viewpager和内部嵌套的view的事件交互规则
- 熟练掌握Android的JNI规范及其NDK的使用
- 熟练掌握自定义控件、状态选择器、自定义属性、四大组件、listview的优化、下拉刷新等等android基本知识
- java基础扎实，熟练掌握OOP思想，掌握集合框架、IO流、多线程、枚举、泛型、动态代理、反射、类加载器等

其他：

- 有技术总结的习惯，大量总结在为知笔记里
- 熟练使用思维导图、markdown等工具
- 有代码洁癖，良好的编码风格，喜欢追求简洁代码和代码效率

# 大学学习时项目
## 安全卫士
###项目描述： 
模仿360安全卫士，实现手机防盗，通讯卫士，软件管家，进程管理，流量统计，手机杀毒，缓存清理，程序锁，号码归属地查询，短信的备份和还原，常用号码查询，号码归属地显示。Github中附有代码和思维导图文件（mymap文件夹下）###技术要点：手机防盗：开机检查sim卡变化；通过广播接收者接受短信指令，实现播放报警音乐，手机定位，远程锁屏和清理手机数据（使用设备超级管理员DevicePolicyManager）
通讯卫士：实现对黑名单号码的短信电话拦截。在service中用代码开启短信广播接收者实现拦截短信；通过电话监听者监听电话状态，通过反射最终调用到系统底层的endCall()方法挂断电话，注册内容观察者删除通话记录。
软件管家：用listview显示手机上应用的安装位置大小信息，实现应用的设置，分享，启动，卸载。（listview的优化：复用不同item，家庭组容器）。
进程管理：listview显示进程，分系统进程和用户显示，提供清理，全选，反选，设置（是否显示系统应用，自动杀进程）功能。Weidget桌面插件，显示进程情况，实现一键清理。（通过在service中主动控制weidget的更新周期）。
缓存清理：通过反射调用系统中的getPackageSizeInfo()方法获得应用的缓存，利用系统的漏洞，给系统发送消息内存空间不够用，系统自动清理所有应用的缓存（通过反射调用freeStorageAndNotify()）。
归属地查询：自动监听输入框文本做查询显示，EditText为空时使用动画插入器抖动，手机震动。
短信备份：拿短信的内容提供者获取短信内容，xml序列化存储到本地。抽取接口编程，备份短信进度显示样式不确定，提供方法给调用者完成。抽取短信备份之前的回调方法和短信备份中的回调方法。调用者方便设置进度参数。
程序锁：上使用fragment显示加锁和未加锁界面，写看门狗服务监听最近的任务栈包名，检查是否加锁弹出密码界面。省电优化：注册广播接收者，锁屏时关闭看门狗服务。
号码归属地显示：监听电话状态和外拨电话，使用自定义toast显示归属地。
## 智慧北京  
### 项目描述：模仿智慧北京和网易新闻，github中有源码和简介。 
### 技术要点：1.	使用Xutils开源框架技术向服务器发送http请求访问某个页面2.	页面布局主要使用SlidingMenu，ViewPagerIndicator和fragment+ViewPager组合实现。3.	获取json数据后，通过Google开源的Gson解析获取到的json数据4.	ListView的头部是一个自定义可以轮播的ViewPager5.	listview优化：复用convertView，减少findViewById的次数；利用ViewHolder6.	数据的缓存处理7.	ViewPager和内部view的交互8.	使用模板设计模式抽取基类代码9.	使用开源项目PullToRefreshListView实现listView下拉刷新，上拉加载更多。10.	消息推送使用第三方推送平台：极光JPush推送平台,第三方登录使用：ShareSDK<img src="/res/智慧北京.png" title="a">

## 电子市场 
### 项目描述： 模仿谷歌电子市场，github中有源码和思维导图。
### 技术要点：1.	主界面使用指针+viewPager（使用FragmentPagerAdapter适配器）2.	抽取基类fragment，请求网络操作，显示界面操作由多种界面情况，抽取LoadingPage管理各种界面（错误界面，空界面…）。3.	抽取基类Holder，因为多个页面都要用到listview，需要使用holder4.	抽取基类BaseAdapter，面向holder编程（BaseHolder），使结构更加清晰5.	采用模板式封装框架基类，完成相应接口的回调，定义抽象方法，提高代码的复用性，降低耦合度。
## 通讯卫士
[http://www.wandoujia.com/apps/com.never.callsmssafe](http://www.wandoujia.com/apps/com.never.callsmssafe)
豌豆荚可以搜索到，这个是完成学校作业做得，用了一晚上，主要功能就是拦截电话和短信。然后体验了一下完成的上架市场流程。


