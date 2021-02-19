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