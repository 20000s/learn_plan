# 2.16

清理了一下github,开始在github上写自己的计划把，，博客太水了

## 多媒体

用摄像头,mp3啥的，比较简单不写了

通知是新学的

```
val manager = getSystemService(Context.NOTIFICATION_SERVICE) as NotificationManager
        if(Build.VERSION.SDK_INT >=  Build.VERSION_CODES.O){
            val channel = NotificationChannel("normal","Normal",NotificationManager.IMPORTANCE_DEFAULT)
            manager.createNotificationChannel(channel)
        }
  创建一个notificationmanager,再创建一个通知渠道
   val notification = NotificationCompat.Builder(this,"normal")
                    .setContentTitle("This is content title")
                    .setContentText("This is content text")
                    .setSmallIcon(R.drawable.small_icon)
                    .setLargeIcon(BitmapFactory.decodeResource(resources,R.drawable.large_icon))
                    .build()
            manager.notify(1,notification)
   创建一个通知
pendingIntent 延迟执行的intent
val intent = Intent(this,::java.class)
val pi = PendingIntent.getActivity(this,0,intent,0)
```

## android多线程

异步信息处理：1.Messager,Handler,MessageQueue,Looper

子进程创建一个message 通过handler发出去，被加到messagequeue等待处理，，looper从messagequeue提取message给handlede handlermessage处理

kotlin 多线程 thread{ } ，asyncTask对异步的封装 onPreExecute()初始化，doInBackground主要操作(publishProgress到主线程的操作，ui>)，onPostExecute（（publishprogress的操作），onPostExecute收尾

# 2.17

主要学了service

这个控件主要用于后台操作，可以单独创建，也可以与activity通信，service的生命周期,intentservice service中用多线程

frida做了看雪的三道题，我感觉我这个人都升华了。。感觉悟了(loaddex ,反调试，遍历 nb!

# 2.19

学习了frida对数据库的处理，，，【flagsystem】

做了几道题，巩固了so先执行jni_onload 以及发现so不同于elf没start函数 ，那init_array在哪执行的，引出问题：init_array在哪里执行，怎么在jni_onload init_array下段 ，里面有反调试怎么处理？（这个其中一个方法是frida 看雪做过） 安卓8.0找不到。。都是过时文章。。。对于这个问题 ，还是静态patch吧。。。  突然做题的时候发现分析so文件jni结构体时可以用插件分析，woc...这么nb的吗jni-helpe...好吧 问了一下yenkoc师傅。。原来ida7.5可以自动导入android库，不过我没写过native jni,等我学了再说( linker执行init_array 8.0找不到。。。。吐了。。。）

在开发上：学习了retrofit 抄代码的事情，比较简单

近期j计划：

1.看完第一行代码

2.学习android native jni编写

3.frida的继续练习（ctf题）

# 2.20

安卓开发上学了jetpack, viewmodel用于保存看的见的数据，，，周期持久,lifecycles感知activity生命周期,livedata nb 可以 发生变化自动进行流程

room 艹 比 sqlite方便多了。。。

看了ollvm的bcf hook掉函数中的函数，加快效率，angr符号执行，把没执行的块nop掉，，angr 以块为执行单位，可以理解为 起始地址到 call jmp jnz之类的

妈的 看作者angr脚本 看了n久，边对照angr的官方文档边看，看的nm自我感觉angr都悟了

ollvm项目会放到github上 还差个平坦化。。要怎么搞。。。

# 2.21

第一行代码只差最后一章实战了。。。审核还没通过，通过后就可以把项目放在github上，争取最近写完。。。

审视了android有ndk jni so层面 ollvm posed frida app加固方面 抓包要学习，去找资料了 

艹 52的帖子是真的多，可以在上面看看 跟着复现 (今天效率有点差 ， 摸鱼了， 当作是 定方向把)

# 2.22

第一行代码写了一半，快写完了，今天最大的收获是会写so了，不过也太复杂了吧，，，，假如真要在so中写逻辑，疯狂env-> 要死了

才 原来ida可以导入jnienv,还可以强制转换 才太nb了吧，我是废物，不过和jni-helper有啥区别啊。。。。。太怪了吧。。。。。看了一下，好，我选择

jni-helper(兔子脸)，更加全面,明显更加全面 ,(看了一下脚本 找到java_ 就对于改了)对于反调试，要么nop(00 00 00 00),要么（push pop），然后改签名

,算是把会飞的丑小鸭的安卓逆向的帖给看完了吧，（途中找了谷歌jni ndk开发文档  要不看一下学习一下ndk jni的开发 今天学会的写so 不过是照葫芦画瓢）

在52上找到一个案例，终于会调init_array了 还有jni_onload





# 2.23

艹 ide崩溃了。。。。花了一个早上时间修，原来是插件问题。。。吐了

中午 看了一大堆ndk的资料。。。都发现是怎么操作，都不讲为什么，我始终不知道怎么写啊，看了两个就发现有两种写法，为什么啊。。。。发现资料没有 书没有 只能去找找视频学习去了。。也太少了吧 艹原来昨天照葫芦画瓢的方法太老了。。。。现在都是cmake 了。。。。我看看 看了一下b站的ndk视频，感觉还不错，跟了，每天看两节，跟着实践一下，学会写ndk 今天的话 学习了ndk写md5 还有签名校验（感觉效率有点低 还是晚上看课吧  ）

# 2.24

中午 用frida解题 对于动态注册 的函数 还是原来的名字 以及 安卓8.0不能由应用写入sd卡 吐了。。。

以及对于jni-helper 动态注册的函数不会重命名 （因为它内部是以j搜索ava_），得自己重写一下

在52上复现了两道题  反调试影响加深了  ，明天应该自己去写一写 怎么反调试的了  ，以及不清楚为什么ida会有时arm反编译不出来呢》   不清楚原理 ，尝试用frida解了一下题  艹 send console.log() 怎么有时一个能输出 一个不能啊 艹 frida bug真多 好菜啊。。。ndk今天没时间看了 明天一定看1



# 2.25

天气预报快写完了

中午 在看雪看到有人用frida解我昨天那道题 我去看看，顺便看一下别人整理的frida的脚本仓库,真的好 学到了很多frida脚本

艹 看雪上看到面试问题，我蒙了 ，太难了吧。。。。得努力学习。。。了 妈的 又咕了 看了好多要学习写的frida脚本  这几天争取把frida看完把。。。

抄了一遍别人的脚本 葫芦娃的fridadexdump先不看了 安卓加固没看 我的知识储备不支持我看这个(把roysue 的frida -dump写了一遍)

之后 看ndk 还有 自己写一下17种反调试



frida -> ndk开发 -> 自己写反编译-> frida反编译 -> 安卓加固->自己写壳-> frida脱壳->其他方式脱壳->so的加固->抓包-> frida抓包

xposed把frida功能全部实现 理解xposed的原理    实战 实战 (我tm学的真乱。。。)

# 2.26

终于把第一行代码写完了。。。。艹 。。。后面蒙了 ，没看懂

把frida的脚本写完了 ，还把那道题给写了。。。找到了frida bug rpc不行啊  我还是直接调用frida脚本..

# 2.27

摸鱼

# 2.28

看完了ndk数字签名，packagermanager->packageinfo->signautes->cString()

loadLibrary：加载apk的libs的so库

load: 具体路径的so库 惊了 c++和c的env还不是同一个东西

jni的一般开发流程：.定义好本地的native方法2.javac -h  .h头文件3.拷贝xxx.h

4.实现我们native的方法5.dll动态 java引入即可

写bug专用户， 写了半天 发现app运行不成功。。才知道加载so不需要名称加so...adb logcat *:Ee 看了半天。。。

学会了ndk改属性 调用方法 ，以及找java的类

GetObjectfield findclass newObject callObjectmethod 

感觉ndk一般的开发流程 我懂了 从明天开始写github上的ndk demo

开了个坑 （主要写frida对我的种种折磨）

用frida做了一道以前动态注册的题

明日任务：

早上：ndk demo写两个

中午：学习apk保护策略

剩余时间：看雪 52复现

# 2.29

艹 demo的版本太老了 不能写 艹。。。就学习apk保护策略吧。。看了一下 没什么好看的 干脆写反调试去了

# 3.1-3.3

摸鱼了，快开学了，找以前同学玩了 ，以及牙齿手术

# 3.4

反调试写完了

# 3.5

fridacontainer nb 早上装完了它 脚本真tm的全 代码补全太爽了  以后写ts脚本了

看了一眼 antifrida fridaserver 使用 D-Bus 协议通信 一个是检验d-bus  发送AUTH 有反应的是frida 第二个是在内存中找LIBFRIDA字段

# 3,6 ~3.8 

回学校整理东西,没怎么学习，不过得看看程序员的自我修养，尝试去面面试

# 3.9

想了想，这几天得复习复习，然后尝试去投投简历，挨一下社会得毒打，看看面试是怎么样的

在写elf解析器，在52上看到比较好的一个帖子,决定跟着写

看了一下noname那道题，了解一下android的动态加载机制，nb,以前开发没写过，原来是这个原理，懂了，自定义application会先启动 

jeb垃圾，反编译出错了

# 3.10

程序员的自我修养 一遍快滚完了

调试器快写完了

# 3.11

调试器写完

pe结构又回顾了一遍

这几天老是打游戏，状态有点差。。。要重新振作

# 3.12

早上看了看看雪和52的帖子，没发现什么好帖。。。看一下电子书《android应用安全》，回顾一下安卓知识，顺便复习了一波花指令, 不可调试，可调试

# 3.13

今天 研究了一下异常 seh veh c++的_try _exception，基本理解了异常的过程 kiDispatchexception分发用户级别的异常的花->KiUserExceptionDispatcher->

RtlDispatchException 找到用户的处理函数,先veh后seh  后zwcontinue 进0环再3环

# 3.14

看了一下windows反调试(10种)和密码学

# 3.15

复习了一下android文件结构，感觉要写一下解析器，，，dex有点nb,,,,,，原本想看一下明日方舟。。好像ll2cpp加密了，，，，

# 3.16

java的代码 资源混淆没什么好看的，知道了一个backup，又看了一般try{}_except{} ，我来说一下过程，怕又忘了 编译器在处理try{}_except{}时，使用了cppeh结构，包括 oldesp,exc_ptr,eh3_registation_record,其中eh3是seh结构的扩展，包涵了next,try_level,handler3异常处理函数，以及最重要的scopable数组，包括

previoistry_level,filter,handler函数,程序在执行try{}except{}，是按照以下流程，先得到当前的try_levle，就先将这个try_level放入结构体中，如果碰到异常，就先根据当前的try_level到scopable中找filter,如果不存在，判断位try{}finallt{},如果存在，执行filter,根据返回值分流，0，向上递归，直到prevouis_try_levle为-1,

1的话，就执行handler函数，然后再返回原来地址，当然过程中有什么栈展开就没说了，就太复杂了。。。。。

# 3.17

原来frida可以hook寄存器。。。第一次见。。。address是汇编地址

Interprector.attach(address, {

onEnter: function(args){

​    this.context.x11(寄存器)

}

});

# 3.23

第一代壳写（抄）好了，但是不明白原理，正在补习原理（动态加载），明白了双亲委派，原来就是不断的递归超类找mclassloader，看有没有加载dex文件，其中pathclassloader是apk自带的，dexclassloader是自己导入的（动态加载的核心）,但是从原理上来说，dexclassloader,pathclassloader的源码并无差别，都是调用basedexclassloader，唯独dexclassloader多一个参数，就是自己存放的dex文件的路径，其中findclass主要是dexpathlist的findclass,一个个遍历dexelement,以及在理解的情况下写一下动态加载替换https://blog.csdn.net/suyimin2010/article/details/80958712

loadedapk是负责加载一个apk的,activitythread中有自己的static对象,还有arraymap<name,loadedapk>,

1.使用反射修改类加载器 

 （一）替换LoadedApk中的mClassLoader

原理就是得到activitythread的aarraymap来改它的loadedapk的classloader

呵呵，死活实现不了，明白原理，要怎么操作啊。。。。（死活没成功，要么android系统的锅，要么我函数放的位置不对，之后碰到再看看，就算是明白原理，先咕了）

（二）合并element(我看的热修复就是这个。。)

  艹，也不行，，，原理明白了。。得找几篇文章，详细操作的看看

2.静态代理



# 3.24

今天学习写第二代壳，内存加载dex,jni实现 

# 3.26-3.30

纵横杯

# 3,31

星阑面试 过了。。。

# 4.1

写了篇动态加载的文章，

# 4.2~4.3

摸鱼

# 4.4~4.5

红名谷杯，虎符，都进线下名次了。。。

# 4.6

写第2代壳，jni加载dex,不落地

# 4.7

实习，写android漏洞文档