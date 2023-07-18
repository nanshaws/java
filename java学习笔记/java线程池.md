## 1.FixedThreadPool

创建一个固定大小的线程池，可控制并发的线程数，超出的线程会在队列中等待。

使用示例如下：

```java
public static void fixedThreadPool() {
    // 创建 2 个数据级的线程池
    ExecutorService threadPool = Executors.newFixedThreadPool(2);

    // 创建任务
    Runnable runnable = new Runnable() {
        @Override
        public void run() {
            System.out.println("任务被执行,线程:" + Thread.currentThread().getName());
        }
    };

    // 线程池执行任务(一次添加 4 个任务)
    // 执行任务的方法有两种:submit 和 execute
    threadPool.submit(runnable);  // 执行方式 1:submit
    threadPool.execute(runnable); // 执行方式 2:execute
    threadPool.execute(runnable);
    threadPool.execute(runnable);
}
```

## 2.CachedThreadPool

创建一个可缓存的线程池，若线程数超过处理所需，缓存一段时间后会回收，若线程数不够，则新建线程。

使用示例如下：

```java
public static void cachedThreadPool() {
    // 创建线程池
    ExecutorService threadPool = Executors.newCachedThreadPool();
    // 执行任务
    for (int i = 0; i < 10; i++) {
        threadPool.execute(() -> {
            System.out.println("任务被执行,线程:" + Thread.currentThread().getName());
            try {
                TimeUnit.SECONDS.sleep(1);
            } catch (InterruptedException e) {
            }
        });
    }
}
```

## 3.SingleThreadExecutor

创建单个线程数的线程池，它可以保证先进先出的执行顺序。

使用示例如下：

```java
public static void singleThreadExecutor() {
    // 创建线程池
    ExecutorService threadPool = Executors.newSingleThreadExecutor();
    // 执行任务
    for (int i = 0; i < 10; i++) {
        final int index = i;
        threadPool.execute(() -> {
            System.out.println(index + ":任务被执行");
            try {
                TimeUnit.SECONDS.sleep(1);
            } catch (InterruptedException e) {
            }
        });
    }
}
```

## 4.ScheduledThreadPool

创建一个可以执行延迟任务的线程池。

使用示例如下：

```java
public static void scheduledThreadPool() {
    // 创建线程池
    ScheduledExecutorService threadPool = Executors.newScheduledThreadPool(5);
    // 添加定时执行任务(1s 后执行)
    System.out.println("添加任务,时间:" + new Date());
    threadPool.schedule(() -> {
        System.out.println("任务被执行,时间:" + new Date());
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
        }
    }, 1, TimeUnit.SECONDS);
}
```

## 5.SingleThreadScheduledExecutor

创建一个单线程的可以执行延迟任务的线程池。

使用示例如下：

```java
public static void SingleThreadScheduledExecutor() {
    // 创建线程池
    ScheduledExecutorService threadPool = Executors.newSingleThreadScheduledExecutor();
    // 添加定时执行任务(2s 后执行)
    System.out.println("添加任务,时间:" + new Date());
    threadPool.schedule(() -> {
        System.out.println("任务被执行,时间:" + new Date());
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
        }
    }, 2, TimeUnit.SECONDS);
}
```

## 6.newWorkStealingPool

创建一个抢占式执行的线程池（任务执行顺序不确定），注意此方法只有在 JDK 1.8+ 版本中才能使用。

使用示例如下：

```java
public static void workStealingPool() {
    // 创建线程池
    ExecutorService threadPool = Executors.newWorkStealingPool();
    // 执行任务
    for (int i = 0; i < 10; i++) {
        final int index = i;
        threadPool.execute(() -> {
            System.out.println(index + " 被执行,线程名:" + Thread.currentThread().getName());
        });
    }
    // 确保任务执行完成
    while (!threadPool.isTerminated()) {
    }
}
```

## 7.ThreadPoolExecutor

最原始的创建线程池的方式，它包含了 7 个参数可供设置。

使用示例如下：

```java
public static void myThreadPoolExecutor() {
    // 创建线程池
    ThreadPoolExecutor threadPool = new ThreadPoolExecutor(5, 10, 100, TimeUnit.SECONDS, new LinkedBlockingQueue<>(10));
    // 执行任务
    for (int i = 0; i < 10; i++) {
        final int index = i;
        threadPool.execute(() -> {
            System.out.println(index + " 被执行,线程名:" + Thread.currentThread().getName());
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });
    }
}
```

### ThreadPoolExecutor 参数介绍

ThreadPoolExecutor 最多可以设置 7 个参数，如下代码所示：

```java
 public ThreadPoolExecutor(int corePoolSize,
                           int maximumPoolSize,
                           long keepAliveTime,
                           TimeUnit unit,
                           BlockingQueue<Runnable> workQueue,
                           ThreadFactory threadFactory,
                           RejectedExecutionHandler handler) {
     // 省略...
 }
```

7 个参数代表的含义如下：

#### 参数 1：corePoolSize

核心线程数，线程池中始终存活的线程数。

#### 参数 2：maximumPoolSize

最大线程数，线程池中允许的最大线程数，当线程池的任务队列满了之后可以创建的最大线程数。

#### 参数 3：keepAliveTime

最大线程数可以存活的时间，当线程中没有任务执行时，最大线程就会销毁一部分，最终保持核心线程数量的线程。

#### 参数 4：unit:

单位是和参数 3 存活时间配合使用的，合在一起用于设定线程的存活时间 ，参数 keepAliveTime 的时间单位有以下 7 种可选：

- TimeUnit.DAYS：天
- TimeUnit.HOURS：小时
- TimeUnit.MINUTES：分
- TimeUnit.SECONDS：秒
- TimeUnit.MILLISECONDS：毫秒
- TimeUnit.MICROSECONDS：微妙
- TimeUnit.NANOSECONDS：纳秒

#### 参数 5：workQueue

一个阻塞队列，用来存储线程池等待执行的任务，均为线程安全，它包含以下 7 种类型：

- ArrayBlockingQueue：一个由数组结构组成的有界阻塞队列。
- LinkedBlockingQueue：一个由链表结构组成的有界阻塞队列。
- SynchronousQueue：一个不存储元素的阻塞队列，即直接提交给线程不保持它们。
- PriorityBlockingQueue：一个支持优先级排序的无界阻塞队列。
- DelayQueue：一个使用优先级队列实现的无界阻塞队列，只有在延迟期满时才能从中提取元素。
- LinkedTransferQueue：一个由链表结构组成的无界阻塞队列。与SynchronousQueue类似，还含有非阻塞方法。
- LinkedBlockingDeque：一个由链表结构组成的双向阻塞队列。

较常用的是 `LinkedBlockingQueue` 和 `Synchronous`，线程池的排队策略与 `BlockingQueue` 有关。

#### 参数 6：threadFactory

线程工厂，主要用来创建线程，默认为正常优先级、非守护线程。

#### 参数 7：handler

拒绝策略，拒绝处理任务时的策略，系统提供了 4 种可选：

- AbortPolicy：拒绝并抛出异常。
- CallerRunsPolicy：使用当前调用的线程来执行此任务。
- DiscardOldestPolicy：抛弃队列头部（最旧）的一个任务，并执行当前任务。
- DiscardPolicy：忽略并抛弃当前任务。

默认策略为 `AbortPolicy`。

### 线程池的执行流程

ThreadPoolExecutor 关键节点的执行流程如下：

- 当线程数小于核心线程数时，创建线程。

- 当线程数大于等于核心线程数，且任务队列未满时，将任务放入任务队列。

- 当线程数大于等于核心线程数，且任务队列已满：若线程数小于最大线程数，创建线程；若线程数等于最大线程数，抛出异常，拒绝任务。

  ```java
   TimeUnit.MICROSECONDS.sleep(100000000);//跟线程sleep是一个意思，不过更精确
  ```
  
  ```java
   public static final Connection createConnection(){
          return (Connection) Proxy.newProxyInstance(ConnectionDriver.class.getClassLoader(),
                  new Class<?>[]{Connection.class},new ConnectionHandler());
      }
  
    public static final Runnable createConnection(){
          return (Runnable) Proxy.newProxyInstance(ConnectionDriver.class.getClassLoader(),
                  new Class<?>[]{Runnable.class},new ConnectionHandler());
      }
  
  
  public static Object newProxyInstance(ClassLoader loader,
                                            Class<?>[] interfaces,//接口数组,可以包含子接口
                                            InvocationHandler h) {
  
  //new Class[] {String.class }
  //就是创建一个数组并且填入元素 String.class，就相当于 new int[]{666}
  ```
  
  