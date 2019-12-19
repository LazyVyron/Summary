# 系统总结一下进程间通信的几个方法

## 1. volatile
    volatile的原理
    是每次读被volatile修饰的变量，都要从主内存区去读，而不是直接从该线程的工作区直接读。每次volatile变量的写，都要马上更新主内存区里的该变量值。
## 2. wait()与notify()
    wait与notify的作用。
    wait表示当前线程挂起，不再占用CPU，wait是释放锁的。notify表示唤醒线程，唤醒意味着开始占用CPU，但是notify并不释放锁。
## 3. Concurrent包以及CountDownLatch
    CountDownLatch是一个线程倒计时器，构造方法只有一个，传入一个count表示存有的线程数，当这个数目为0时，被上锁的线程开始执行。await释放锁，进入等待countdownLatch为0，countDown意味着count减1，当count为0时，await的被唤醒。
    demo：
````
public class TestSync {
    public static void main(String[] args) {
        CountDownLatch countDownLatch = new CountDownLatch(1);
        List<String>  list = new ArrayList<>();
        // 实现线程A
        Thread threadA = new Thread(() -> {
            for (int i = 1; i <= 10; i++) {
                list.add("abc");
                System.out.println("线程A向list中添加一个元素，此时list中的元素个数为：" + list.size());
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                if (list.size() == 5)
                    countDownLatch.countDown();
            }
        });
        // 实现线程B
        Thread threadB = new Thread(() -> {
            while (true) {
                if (list.size() != 5) {
                    try {
                        countDownLatch.await();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                System.out.println("线程B收到通知，开始执行自己的业务...");
                break;
            }
        });
        //　需要先启动线程B
        threadB.start();
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 再启动线程A
        threadA.start();
    }
}
````
    打印结果是1、2、3、4、5、6，线程B收到通知，7、8、9、10
