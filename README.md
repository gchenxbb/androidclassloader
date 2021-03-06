Android的ClassLoader
加载的是dex文件。

技术文档

[双亲委派模型](https://www.jianshu.com/p/74685bdddf22)

#### 系统加载器
BootClassLoader，Java实现，同一个包才可以访问，App无法访问
DexClassLoader，继承BaseDexClassLoader，加载dex文件，apk，jar文件。最终都是要加载dex文件。
参数optimizedDirectory是解压dex文件的内部存储路径，私有路径/data/data/<Package Name>/..,
PathClassLoader，继承BaseDexClassLoader，默认参数optimizedDirectory是/data/dalvik_cache，加载已安装的apk的dex文件，存储在该路径。

凡是apk中用户定义的类，MainActivity.class,Hello.class的加载器都是PathClassLoader。
路径是
dalvik.system.PathClassLoader[DexPathList[[zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/base.apk", 
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_dependencies_apk.apk",
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_0_apk.apk", 
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_1_apk.apk",
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_2_apk.apk", 
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_3_apk.apk", 
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_4_apk.apk", 
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_5_apk.apk", 
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_6_apk.apk",
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_7_apk.apk", 
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_8_apk.apk",
zip file "/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/split_lib_slice_9_apk.apk"],
nativeLibraryDirectories=[/data/app/com.pa.chen.classloader-YA45x9vXJeZnGEbKV2Cm5w==/lib/arm64, /system/lib64, /vendor/lib64]]]

凡是系统类，Activity.class，Context.class，System.class的加载器都是BootClassLoader。

android源码26api，ClassLoader静态内部类SystemClassLoader中存储的加载器loader是PathClassLoader。父类加载器是BootClassLoader。

ContextImpl内部加载器来自LoadedApk的getClassLoader。LoadApk是空则来自ClassLoader内部SystemClassLoader。



# memory

统计当前app节点对象。


Shallow Size
对象本身占有内存大小，不包含其引用的对象，，

20字节

3个4字节基础类型  12


4byte(对象头) + 4byte(类型指针) 代表什么



在 sdk21以后 也就是Android5.0系统以后，GOOGLE在Object类中加入了2个字段

*   private transient Class<?> shadow$_klass_;  
*   private transient int shadow$_monitor_;  

native size：8.0之后的手机会显示，主要反应Bitmap所使用的像素内存（8.0之后，转移到了native）
