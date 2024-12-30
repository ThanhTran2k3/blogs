---
title: "JVM, JDK, JRE trong Java là gì?"
date: 2019-10-04T12:00:00+07:00
summary: Trong Java, ba khái niệm cơ bản mà bạn thường nghe đến là JVM (Java Virtual Machine), JDK (Java Development Kit) và JRE (Java Runtime Environment). Mặc dù chúng có liên quan chặt chẽ với nhau, nhưng mỗi thành phần này có vai trò và chức năng riêng biệt. Dưới đây là một cái nhìn chi tiết hơn về từng thành phần và sự khác biệt giữa chúng.
image: /images/post/jdk.jpg 
---

# JVM, JDK, JRE trong Java là gì?

Trong Java, ba khái niệm cơ bản mà bạn thường nghe đến là JVM (Java Virtual Machine), JDK (Java Development Kit) và JRE (Java Runtime Environment). Mặc dù chúng có liên quan chặt chẽ với nhau, nhưng mỗi thành phần này có vai trò và chức năng riêng biệt. Dưới đây là một cái nhìn chi tiết hơn về từng thành phần và sự khác biệt giữa chúng.

## 1. JVM (Java Virtual Machine)

**Chức năng:**

- JVM là một máy ảo dùng để chạy mã bytecode của Java. Đây là nơi chuyển đổi mã bytecode thành mã máy phù hợp với hệ điều hành cụ thể.

**Vai trò:**

- Thực thi mã bytecode.
- Quản lý bộ nhớ bằng Garbage Collection.
- Xử lý ngoại lệ.

**Lưu ý:**

- JVM không hoạt động độc lập mà cần các tài nguyên khác từ JRE.

## 2. JRE (Java Runtime Environment)

**Chức năng:**

- JRE cung cấp môi trường để chạy các ứng dụng Java, bao gồm:
  - JVM.
  - Các thư viện lớp Java.
  - Các tệp hỗ trợ khác.

**Vai trò:**

- JRE được sử dụng bởi người dùng cuối để chạy ứng dụng Java mà không cần công cụ phát triển.

**Không bao gồm:**

- Trình biên dịch và công cụ phát triển.

## 3. JDK (Java Development Kit)

**Chức năng:**

- JDK là bộ công cụ phát triển phần mềm Java, bao gồm mọi thứ cần thiết để viết, biên dịch và chạy ứng dụng Java.

**Thành phần:**

- JRE (bao gồm JVM).
- Trình biên dịch (javac).
- Công cụ gỡ lỗi và các công cụ phát triển khác.

**Vai trò:**

- JDK dành cho lập trình viên Java để xây dựng và kiểm thử ứng dụng.
