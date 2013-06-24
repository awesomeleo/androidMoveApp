<!--sublog
{
    "title":"android应用搬家的实现",
    "category":"android应用开发",
    "tags":"",
    "publish":"true",
    "blog_id":"3151705"
}
sublog-->

android手机上的应用搬家功能，具体的介绍和原理参考：

[系统目录及应用搬家的研究](http://hcq0618.blog.163.com/blog/static/17809035120132142829615/)

[应用搬家的实现](http://hcq0618.blog.163.com/blog/static/1780903512013214115241436/)

这里主要是作为一个补充，因为上面两篇文章虽然讲的挺好的，但是给出的例子不能直接运行，还是需要一些准备的。大概讲一下要点。

0. Pm.jar是android包管理命令pm的底层实现，源代码是一个java文件: [Pm.java](http://android.yongbok.net/repository/frameworks/base/cmds/pm/src/com/android/commands/pm/Pm.java)。注意这个版本不是最新的。关键就是在这个基础上添加应用搬家的功能。

0. 编译Pm.jar需要使用一些android不公开的api，所以需要将android framework的源代码放在工程的src目录下。[android / platform_frameworks_base](https://github.com/android/platform_frameworks_base/tree/master/core/java/android/content/pm)

0. 修改Pm.java，增加应用搬家功能：move [-l] pakcageName, -l表示从SD卡移到内存，项目主页：

0. 执行pm.jar的示例，先将pm.jar放到/sdcard下，然后执行下面的命令：

		shell \"su -c 'export CLASSPATH=/sdcard/pm.jar && export LD_LIBRARY_PATH=/vendor/lib:/system/lib && exec app_process /system/bin com.lxkj.move_app/Pm move [-l] pakcageName'\"
