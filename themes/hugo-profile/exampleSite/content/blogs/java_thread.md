---
title: "Thread và Multithread trong Java"
date: 2018-02-12T12:00:00+07:00
summary: Khi phát triển ứng dụng Java, đôi khi bạn cần thực hiện các tác vụ đồng thời hoặc xử lý nhiều công việc cùng lúc mà không làm gián đoạn tiến trình của nhau. Điều này có thể giúp cải thiện hiệu suất của ứng dụng, đặc biệt là khi làm việc với các tác vụ nặng hoặc đòi hỏi thời gian chờ đợi như I/O (đọc/ghi tệp, kết nối mạng, v.v.). Trong bài viết này, chúng ta sẽ tìm hiểu về Thread và Multithreading trong Java, cách sử dụng chúng và các kỹ thuật tối ưu hiệu suất khi làm việc với đa luồng.
image: /images/post/java_thread.jpg 
---

# Thread và Multithread trong Java: Xử lý đồng thời trong ứng dụng Java

Khi phát triển ứng dụng Java, đôi khi bạn cần thực hiện các tác vụ đồng thời hoặc xử lý nhiều công việc cùng lúc mà không làm gián đoạn tiến trình của nhau. Điều này có thể giúp cải thiện hiệu suất của ứng dụng, đặc biệt là khi làm việc với các tác vụ nặng hoặc đòi hỏi thời gian chờ đợi như I/O (đọc/ghi tệp, kết nối mạng, v.v.). Trong bài viết này, chúng ta sẽ tìm hiểu về Thread và Multithreading trong Java, cách sử dụng chúng và các kỹ thuật tối ưu hiệu suất khi làm việc với đa luồng.

## Thread là gì?

Thread (luồng) là đơn vị thực thi nhỏ nhất trong một tiến trình (process). Mỗi tiến trình có thể có một hoặc nhiều luồng. Trong Java, luồng cho phép một chương trình thực hiện nhiều tác vụ đồng thời (concurrent tasks). Mỗi luồng có thể thực thi một đoạn mã riêng biệt, cho phép chương trình thực hiện các công việc song song mà không cần phải chờ đợi lẫn nhau.

Khi bạn khởi động một ứng dụng Java, chương trình đó sẽ bắt đầu với một luồng chính (main thread). Tuy nhiên, bạn có thể tạo ra các luồng phụ (child threads) để thực hiện các tác vụ khác nhau trong nền.

## Tạo và quản lý Thread trong Java

Java cung cấp hai cách chính để tạo và quản lý luồng: Kế thừa lớp `Thread` và Triển khai giao diện `Runnable`.

### 1. Kế thừa lớp Thread

Cách đơn giản để tạo một luồng là kế thừa lớp `Thread` và ghi đè phương thức `run()` của lớp này. Phương thức `run()` chứa mã mà luồng sẽ thực thi.

**Ví dụ:**

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Luồng con đang thực thi...");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start();  // Khởi động luồng con
    }
}
```

Khi bạn gọi phương thức `start()`, luồng con sẽ được khởi động và phương thức `run()` sẽ được gọi để thực thi công việc của luồng.

### 2. Triển khai giao diện Runnable

Cách thứ hai là triển khai giao diện `Runnable`. Giao diện này có một phương thức `run()` tương tự như trong lớp `Thread`, nhưng bạn cần phải khởi tạo một đối tượng `Thread` và truyền đối tượng `Runnable` vào đó.

**Ví dụ:**

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Luồng con đang thực thi...");
    }
}

public class Main {
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();
        Thread thread = new Thread(myRunnable);
        thread.start();  // Khởi động luồng con
    }
}
```

Trong trường hợp này, `Runnable` cung cấp tính linh hoạt hơn, vì bạn có thể triển khai nó trong các lớp đã kế thừa một lớp khác mà không cần phải kế thừa lớp `Thread`.

## Quản lý nhiều luồng (Multithreading)

Multithreading trong Java cho phép nhiều luồng chạy đồng thời, chia sẻ tài nguyên và thực thi các tác vụ mà không gây xung đột. Java cung cấp một số công cụ và phương thức để làm việc với nhiều luồng cùng lúc, như việc đồng bộ hóa các luồng, quản lý sự kiện đồng bộ và xử lý các vấn đề liên quan đến dữ liệu chung.

### 1. Tạo nhiều luồng

Bạn có thể tạo nhiều luồng trong cùng một chương trình để thực hiện các tác vụ song song. 

**Ví dụ:**

```java
class MyRunnable implements Runnable {
    private String task;

    public MyRunnable(String task) {
        this.task = task;
    }

    @Override
    public void run() {
        System.out.println(task + " đang thực thi...");
    }
}

public class Main {
    public static void main(String[] args) {
        MyRunnable task1 = new MyRunnable("Tác vụ 1");
        MyRunnable task2 = new MyRunnable("Tác vụ 2");

        Thread thread1 = new Thread(task1);
        Thread thread2 = new Thread(task2);

        thread1.start();  // Khởi động luồng 1
        thread2.start();  // Khởi động luồng 2
    }
}
```

Trong ví dụ trên, hai luồng sẽ chạy đồng thời và thực hiện hai tác vụ khác nhau.

### 2. Đồng bộ hóa các luồng (Synchronization)

Khi nhiều luồng chia sẻ dữ liệu hoặc tài nguyên chung, bạn có thể gặp phải vấn đề xung đột (data race). Java cung cấp cơ chế đồng bộ hóa để đảm bảo rằng chỉ có một luồng có thể truy cập vào tài nguyên chung tại một thời điểm.

Bạn có thể sử dụng từ khóa `synchronized` để đảm bảo tính đồng bộ khi truy cập các tài nguyên chia sẻ:

**Ví dụ:**

```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public synchronized int getCount() {
        return count;
    }
}

public class Main {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        Thread thread1 = new Thread(task);
        Thread thread2 = new Thread(task);

        thread1.start();
        thread2.start();

        thread1.join();
        thread2.join();

        System.out.println("Giá trị cuối cùng của count: " + counter.getCount());
    }
}
```

### 3. Quản lý luồng với Executor Framework

Thay vì tự mình quản lý các luồng, bạn có thể sử dụng **Executor Framework** trong Java để quản lý các luồng một cách hiệu quả. `ExecutorService` là một trong các interface phổ biến trong framework này, giúp bạn tạo và quản lý các luồng với ít mã nguồn hơn.

**Ví dụ:**

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);  // Tạo một nhóm luồng với 2 luồng

        Runnable task1 = () -> System.out.println("Tác vụ 1 đang thực thi...");
        Runnable task2 = () -> System.out.println("Tác vụ 2 đang thực thi...");

        executor.submit(task1);
        executor.submit(task2);

        executor.shutdown();  // Đóng ExecutorService khi tất cả tác vụ hoàn thành
    }
}
```

### 4. Thread Safety và Deadlock

- **Thread Safety:** Để đảm bảo một ứng dụng Java hoạt động chính xác khi có nhiều luồng, bạn cần phải đảm bảo tính an toàn của luồng (thread safety) cho các tài nguyên và dữ liệu chia sẻ.
- **Deadlock:** Deadlock xảy ra khi hai hoặc nhiều luồng bị mắc kẹt trong một tình huống mà chúng không thể tiếp tục thực thi. Điều này có thể xảy ra khi hai luồng đều cần tài nguyên mà luồng kia đang giữ và không giải phóng.

## Kết luận

Multithreading trong Java là một công cụ mạnh mẽ giúp cải thiện hiệu suất ứng dụng, đặc biệt là trong các ứng dụng yêu cầu xử lý nhiều tác vụ đồng thời. Bằng cách sử dụng `Thread`, `Runnable`, `ExecutorService`, và các kỹ thuật đồng bộ hóa, bạn có thể xây dựng các ứng dụng hiệu quả và dễ dàng quản lý các tác vụ song song.

Tuy nhiên, khi làm việc với đa luồng, bạn cần lưu ý đến các vấn đề như Thread Safety, Deadlock và Race Condition để đảm bảo ứng dụng hoạt động chính xác và không gặp phải các lỗi khó khắc phục.
