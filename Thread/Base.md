# 线程基础

## 线程的几种状态：
    new -> runnable -> running -> blocked -> dead
    新建      就绪       运行       阻塞       死

    runnable获得CPU的时间片，进入到running，时间片用完后又回到了runnable。或者是wait，或者是block。wait会释放CPU，block不释放。

![QQ图片20191219234651.png](https://i.loli.net/2019/12/19/icdqbxsIWzD9Beu.png)