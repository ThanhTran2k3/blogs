---
title: "Stream API và Lambda Expressions trong Java 8"
date: 2023-02-23T12:00:00+07:00
summary: Java đã có một chặng đường dài kể từ khi ra đời, và phiên bản Java 8 đánh dấu một bước ngoặt lớn với việc giới thiệu Stream API và Lambda Expressions. Những tính năng này đã thay đổi cách chúng ta viết mã Java, đặc biệt là trong việc xử lý dữ liệu và tối ưu hóa các tác vụ phức tạp. Trong bài viết này, chúng ta sẽ cùng tìm hiểu chi tiết về Stream API và Lambda Expressions, những tính năng đột phá trong Java 8, và cách chúng giúp đơn giản hóa mã nguồn, tăng tính hiệu quả và dễ bảo trì.
image: /images/post/java_8.jpg 
---

# Stream API và Lambda Expressions trong Java: Cách mạng hóa lập trình hàm

Java đã có một chặng đường dài kể từ khi ra đời, và phiên bản Java 8 đánh dấu một bước ngoặt lớn với việc giới thiệu Stream API và Lambda Expressions. Những tính năng này đã thay đổi cách chúng ta viết mã Java, đặc biệt là trong việc xử lý dữ liệu và tối ưu hóa các tác vụ phức tạp. Trong bài viết này, chúng ta sẽ cùng tìm hiểu chi tiết về Stream API và Lambda Expressions, những tính năng đột phá trong Java 8, và cách chúng giúp đơn giản hóa mã nguồn, tăng tính hiệu quả và dễ bảo trì.

## Lambda Expressions: Viết Mã Ngắn Gọn và Dễ Dàng Hơn

### Lambda là gì?
Lambda Expressions là một khái niệm đến từ lập trình hàm (Functional Programming), cho phép bạn định nghĩa các hàm vô danh (anonymous functions) mà không cần phải tạo các class hay phương thức riêng biệt. Trước khi Java 8 ra đời, để sử dụng một hàm kiểu function, bạn phải định nghĩa một class ẩn danh, điều này khá phức tạp và làm mã nguồn dài dòng. Lambda Expressions giúp đơn giản hóa quá trình này.
### Cú pháp cơ bản của Lambda:
```java
(parameters) -> expression
```

### Ví dụ về Lambda Expression
Giả sử bạn có một danh sách các số nguyên và muốn in ra các số chẵn trong danh sách đó. Trước khi Java 8, bạn sẽ phải sử dụng một vòng lặp như sau:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
for (Integer number : numbers) {
    if (number % 2 == 0) {
        System.out.println(number);
    }
}
```

Với Lambda Expressions, mã nguồn trở nên ngắn gọn và dễ đọc hơn:

```java
numbers.stream()
       .filter(n -> n % 2 == 0)
       .forEach(System.out::println);
```

Ở đây, `n -> n % 2 == 0` là Lambda Expression, giúp lọc các số chẵn trong danh sách, và `System.out::println` là một cách tham chiếu phương thức (method reference) để in kết quả.

## Stream API: Xử Lý Dữ Liệu Linh Hoạt và Hiệu Quả

### Stream là gì?
Stream API trong Java cung cấp một cách thức mới và mạnh mẽ để xử lý các bộ dữ liệu (collections), đặc biệt là với các tác vụ như lọc, map, reduce và thao tác song song. Điều này giúp bạn xử lý dữ liệu theo cách khai báo (declarative style), thay vì phải viết các vòng lặp và điều kiện.

Một Stream không phải là một dữ liệu trong bộ sưu tập mà là một chuỗi các thao tác có thể thực hiện trên bộ sưu tập đó. Các thao tác trên Stream thường được chia thành hai loại:

- **Các thao tác trung gian (Intermediate operations):** Các thao tác này tạo ra một stream mới và có thể kết hợp lại với nhau.
- **Các thao tác kết thúc (Terminal operations):** Các thao tác này sẽ kích hoạt các phép toán thực tế trên Stream, ví dụ như `forEach`, `collect`, `reduce`.

### Ví dụ về Stream API
Giả sử bạn có một danh sách các số nguyên và muốn tính tổng của các số chẵn trong danh sách. Trước Java 8, bạn sẽ phải viết một vòng lặp và điều kiện phức tạp:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
int sum = 0;
for (Integer number : numbers) {
    if (number % 2 == 0) {
        sum += number;
    }
}
System.out.println(sum);
```

Với Stream API, bạn có thể làm điều này ngắn gọn hơn:

```java
int sum = numbers.stream()
                  .filter(n -> n % 2 == 0)
                  .mapToInt(Integer::intValue)
                  .sum();
System.out.println(sum);
```

Ở đây:
- `filter(n -> n % 2 == 0)` lọc ra các số chẵn.
- `mapToInt(Integer::intValue)` chuyển đổi các đối tượng Integer thành kiểu int để tính toán.
- `sum()` tính tổng các giá trị.

### Các Tính Năng Nổi Bật Của Stream API

1. **Lọc (filter):** Lọc các phần tử trong Stream theo một điều kiện cho trước.
   ```java
   List<Integer> evenNumbers = numbers.stream()
                                      .filter(n -> n % 2 == 0)
                                      .collect(Collectors.toList());
   ```

2. **Chuyển đổi (map):** Chuyển đổi các phần tử trong Stream thành các giá trị mới.
   ```java
   List<Integer> doubledNumbers = numbers.stream()
                                         .map(n -> n * 2)
                                         .collect(Collectors.toList());
   ```

3. **Tính tổng (reduce):** Thực hiện các phép toán (như cộng, nhân) trên các phần tử trong Stream.
   ```java
   int sum = numbers.stream()
                    .reduce(0, Integer::sum);
   ```

4. **Xử lý song song (parallel):** Stream API hỗ trợ xử lý song song, giúp tăng hiệu suất trong các ứng dụng đa lõi.
   ```java
   int sum = numbers.parallelStream()
                    .filter(n -> n % 2 == 0)
                    .mapToInt(Integer::intValue)
                    .sum();
   ```

## Kết hợp Lambda Expressions và Stream API
Sự kết hợp giữa Lambda Expressions và Stream API tạo ra một cách tiếp cận cực kỳ mạnh mẽ và linh hoạt để xử lý dữ liệu trong Java. Lambda giúp giảm độ phức tạp khi định nghĩa các hàm, còn Stream API giúp thao tác dữ liệu một cách khai báo và dễ dàng, đồng thời hỗ trợ các phép toán song song hiệu quả.

Dưới đây là ví dụ kết hợp giữa Lambda và Stream API để tìm kiếm các số chẵn trong danh sách, sau đó nhân đôi giá trị của chúng và tính tổng:

```java
int result = numbers.stream()
                    .filter(n -> n % 2 == 0)
                    .map(n -> n * 2)
                    .reduce(0, Integer::sum);
System.out.println(result);
```

## Kết luận
Lambda Expressions và Stream API là hai tính năng nổi bật trong Java 8, thay đổi hoàn toàn cách chúng ta xử lý dữ liệu và viết mã. Sự kết hợp của chúng giúp Java không chỉ trở thành một ngôn ngữ mạnh mẽ mà còn linh hoạt và dễ bảo trì hơn, đặc biệt trong các ứng dụng yêu cầu xử lý dữ liệu phức tạp.

Nếu bạn chưa sử dụng Lambda và Stream trong các dự án của mình, đây chính là thời điểm tuyệt vời để bắt đầu làm quen và ứng dụng chúng, giúp mã nguồn trở nên ngắn gọn, dễ hiểu và hiệu quả hơn.
