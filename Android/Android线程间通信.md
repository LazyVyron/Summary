# 线程间通信

## 1.共享内存
    volitate
## 2.Java 管道
    PipedInputStream从PipedOutputStream中读取数据。消费者-生产者问题。
    //生产者
    while(true){
        wait(room);
        wait(mutex);
        进行生产
        signal(mutex);
        signal(items);
    }
    //消费者
    while(true){
        wait(items);
        wait(mutex);
        进行消费
        signal(mutex);
        signal(items);
    }
## 3.Handler
    Handler异步通信机制，4和5的底层也是用了handler。
    
**拓展问题：两个子进程如何通信？**

## 4.view.post
    直接tv_name.post(new Runnable())即可。
## 5.runOnUiThread
    直接在run方法里面写tv_name.setText("lwc")即可。
## 6.AsyncTask
    在OnPostExecute里写tv_name.setText("lwc")即可