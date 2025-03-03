## 生产者-消费者问题
     - **核心矛盾**：缓冲区空/满时的线程阻塞与唤醒。
     - **解决方法**：通过 **PV 操作**（信号量）实现互斥与同步。
     
     ### 伪代码示例
     ```java
     Semaphore mutex = 1; // 互斥信号量
     Semaphore empty = N; // 缓冲区空槽数
     Semaphore full = 0;  // 缓冲区数据数
     
     // 生产者
     void producer() {
         while(true) {
             生产数据();
             P(empty); // 申请空槽
             P(mutex);
             放入缓冲区();
             V(mutex);
             V(full);  // 增加数据数
         }
     }
     
     // 消费者
     void consumer() {
         while(true) {
             P(full);  // 申请数据
             P(mutex);
             取出数据();
             V(mutex);
             V(empty); // 释放空槽
             消费数据();
         }
     }
[[进程同步]]
[[信号量机制]]

