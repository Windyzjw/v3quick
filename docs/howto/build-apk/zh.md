# build apk功能及使用相关说明

> build_apk.sh 和build_apk.bat 可以将 quick 工程编译成可安装运行的 Android 的 apk 文件。

### 环境：
需要配置好 QUICK_V3_ROOT、ANDROID_SDK_ROOT、ANDROID_NDK_ROOT 三个环境变量。
Windows 下还需要配置 JAVA_HOME 环境变量( JDK 的目录)，并将 JDK 的 bin 目录加到 PATH 环境变量中。
如果环境未搭建好或者未配置好，运行时会在命令行报相关错误提示并返回非0的错误码。

### 运行：
build_apk 脚本必须在工程的 proj.android 目录下运行。
如果运行成功，将在 proj.android/bin 目录下生成 quickgame.apk ，并返回一个0值表示成功。
运行失败，将会返回一个非0的错误码。

### 可选参数：

    -classpath <路径>            指定查找用户类文件和注释处理程序的位置

如果有额外的第三方 jar 包需要集成可能会需要添加此参数。默认情况下不需要指定此参数。

    -jv <版本号>        指定要使用的 JDK 版本号
    
默认参数为1.6。如果使用其他版本的 JDK， 可能需要指定此参数与要使用的 JDK 版本相一致。

    -api <版本号>       指定要使用的 Android 的 api 版本号
    
默认参数为19，即使用 android-19 。

    -bt  <版本号>       指定要使用的 ADT 的 build tools的版本号

一般不需要指定此参数，脚本运行时会自动到 ANDROID_SDK_ROOT/build-tools 目录下查找可用的版本。如果此目录下有多个版本，例如有 android-4.4.2 和 android-4.3 ，则可以通过 “-bt 4.4.2” 来强制指定其中的4.4.2版本，但即使不指定也会找到其中一个来使用。

    -k  <文件路径>     指定要用于签名的密匙库文件
    -kp <口令>         指定用于密钥库完整性的口令
    -ksa <密匙库名称>  指定密匙库名称
    
以上参数可以让用户使用自己的密匙文件给自己的apk文件签名。如果不指定，将会使用 quick 提供的测试用的密匙文件进行签名。

### 注意事项
- JDK 1.7以上的版本，在签名时需要指定时间戳，此脚本现在未做处理，因此在签名时会有警告信息，并且打包出来的apk在真机上运行时会报错。