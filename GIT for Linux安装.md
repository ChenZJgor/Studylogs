## GIT for Linux安装

因为最近在做CONTIKI系统应用的开发，要用到GIT。在Ubuntu上安装GIT时遇到一个问题，编译的时候报错

    Writing perl.mak for Git
    make[2]: *** [perl.mak] Error 1
    make[1]: *** [instlibdir] Error 2
    make: *** [git-add--interactive] Error 2

一开始以为是缺少环境，几次检查后确定没有问题。最后发现是系统时间设置错误，系统的时间早于版本的时间，在时间正确设置后，问题解决。