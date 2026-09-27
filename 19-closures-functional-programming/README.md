# Rust Tutorial Project — Principles of Programming Languages

> **กลุ่มที่:** 19
> **Topic No.:** 19
> **Topic Name:** Closures & Functional Programming
> **ประเด็นหลักที่ควรครอบคลุม:** closures, parameters, capture, higher-order functions และ functional programming

---

## 1. Members

| # | Name | Student ID | GitHub Username | Main Responsibility |
|---|---|---|---|---|
| 1 | นายก้องภพ คุณดำรงชัย | 670710639 | `@[กรอก GitHub username]` | Concept + Short Code Illustration (สรุปแนวคิดหลัก + โค้ดตัวอย่างสั้น) |
| 2 | นายคีรเทพ ก้องสุวรรณ | 670710641 | `@[กรอก GitHub username]` | Detailed Code + Live Demo (โค้ดเชิงลึก + สาธิตสด) |
| 3 | นางสาวจิณณพัต แหล่งหล้า | 670710642 | `@[กรอก GitHub username]` | Rust vs Other Language + PPL Analysis (เปรียบเทียบภาษา + วิเคราะห์เชิง PPL) |
| 4 | นางสาวจุฑารัตน์ รู้วงษ์ | 670710643 | `@[กรอก GitHub username]` | Exercises + Common Mistakes + Challenge (แบบฝึกหัด + ข้อผิดพลาดที่พบบ่อย + คำถามท้าทาย) |

> แก้ไข GitHub Username ของแต่ละคนให้ตรงกับบัญชีจริงก่อนเริ่มทำงาน (ผู้สอนจะใช้คอลัมน์นี้เชิญเป็น collaborator ของ repository)

---

## 2. Learning Objectives

หลังจากศึกษา Topic นี้แล้ว ผู้เรียนสามารถ:

1. `[อธิบายแนวคิดสำคัญได้]`
2. `[เขียนโปรแกรม Rust ที่เกี่ยวข้องได้]`
3. `[วิเคราะห์พฤติกรรม/กฎของภาษาได้]`
4. `[เปรียบเทียบ Rust กับภาษาอื่นได้]`

---

## 3. Introduction

`[เขียนเนื้อหาที่นี่ — ใช้โครงสร้างเดียวกับ rust_tutorial_template.md ฉบับเต็มที่ผู้สอนแจกให้]`

---

*โครงสร้างเอกสารฉบับเต็ม (Key Concepts, Runnable Code Examples, Common Mistakes, Exercises, PPL Perspective, Rust vs Other Language, References, AI Usage Declaration, GitHub Contribution, Final Checklist) ให้ทำต่อจากจุดนี้ตาม Template หลักของวิชา (`rust_tutorial_template.md`) ที่แนบมากับใบมอบหมายงาน*

## 9. PPL Perspective

Closures เป็นฟีเจอร์ของ Rust ที่เกี่ยวข้องกับแนวคิดของ Programming Language หลายด้าน เช่น Syntax, Semantics, Type System, Memory Management และ Functional Programming

### 9.1 Syntax

Closure ใน Rust ใช้เครื่องหมาย | | สำหรับกำหนด parameter และตามด้วย expression หรือ body ของ Closure
let add = |x| x + 10;
ในตัวอย่าง |x| x + 10 คือ Closure โดย x เป็น parameter และ x + 10 เป็นการทำงานของ Closure
Rust สามารถอนุมานชนิดข้อมูลของ parameter และ return value ของ Closure ได้จากบริบท ทำให้สามารถเขียน Closure ได้สั้นกว่า function ในบางกรณี

### 9.2 Semantics / Behavior

Closure สามารถ capture ตัวแปรจาก environment ที่มันถูกสร้างขึ้นมาได้ ซึ่งเป็นพฤติกรรมสำคัญที่แตกต่างจาก regular function ใน Rust
let n = 10;
let add_n = |x| x + n;
ในตัวอย่าง Closure สามารถนำ n ซึ่งเป็นตัวแปรภายนอกมาใช้งานได้ โดย Rust จะกำหนดวิธีการ capture ให้เหมาะสมกับการใช้งาน เช่น การยืมแบบ immutable reference, mutable reference หรือการย้าย ownership
แนวคิดนี้เกี่ยวข้องกับ Scope, Environment และ Binding เพราะ Closure สามารถเก็บความสัมพันธ์กับตัวแปรที่อยู่ใน environment ของมันไว้ได้

### 9.3 Type System

Closure แต่ละตัวใน Rust จะมี anonymous type ที่เป็นเอกลักษณ์ของตัวเอง และไม่สามารถระบุชนิดของ Closure ด้วยชื่อ type ทั่วไปได้โดยตรง
Rust ใช้ Closure Traits เพื่อกำหนดลักษณะการเรียกใช้งาน Closure ได้แก่
Fn เรียกใช้งานซ้ำได้โดยไม่แก้ไขค่าที่ capture
FnMut เรียกใช้งานซ้ำได้ และสามารถแก้ไขค่าที่ capture ได้
FnOnce Closure ที่อาจนำค่าที่ capture ออกไปใช้จนไม่สามารถเรียกซ้ำได้
Closure จะ implement trait เหล่านี้ตามลักษณะการใช้งานค่าที่ capture ภายใน body ของ Closure

### 9.4 Memory / Resource Management

Closures ใน Rust ทำงานร่วมกับระบบ Ownership และ Borrowing ของภาษา
เมื่อ Closure ใช้ตัวแปรจากภายนอก Rust จะตรวจสอบว่าควร capture ตัวแปรนั้นในรูปแบบใด โดยทั่วไปจะเลือกวิธีที่จำเป็นน้อยที่สุดก่อน เช่น การยืมค่า และสามารถใช้ move เพื่อบังคับให้ Closure capture ค่าโดยการย้ายหรือคัดลอกค่าเข้าไป
ดังนั้น Closure จึงเกี่ยวข้องโดยตรงกับการจัดการ ownership และ lifetime ของข้อมูลที่ถูก capture

### 9.5 Abstraction / Other PPL Concepts

Closure เป็นตัวอย่างของ Higher-Order Function เนื่องจากสามารถส่ง Closure เป็น argument ให้กับ function หรือ method อื่นได้
ตัวอย่างเช่น map() สามารถรับ Closure เพื่อกำหนดว่าต้องการเปลี่ยนข้อมูลแต่ละตัวอย่างไร
let numbers = vec![1, 2, 3];
let doubled: Vec<_> = numbers.iter().map(|x| x * 2).collect();
แนวคิดนี้เกี่ยวข้องกับ Functional Programming เพราะสามารถนำ function หรือ Closure มาใช้เป็นข้อมูลและนำไปประกอบกับการประมวลผลข้อมูล เช่น map() และ filter()

### 9.6 Why Rust

Rust ออกแบบ Closures ให้ทำงานร่วมกับระบบ Type System, Ownership และ Borrowing ของภาษา
ข้อดีคือ compiler สามารถตรวจสอบการใช้งานตัวแปรที่ Closure capture รวมถึงชนิดของข้อมูลและการเข้าถึง memory ได้ตั้งแต่ compile time
นอกจากนี้ Closures และ Iterators ยังเป็น abstraction ระดับสูงที่ช่วยให้เขียนโค้ดแบบ Functional Programming ได้กระชับ โดย Rust มุ่งเน้นให้ abstraction เหล่านี้มีประสิทธิภาพโดยไม่เพิ่ม runtime overhead ที่ไม่จำเป็น

---

## 10. Rust vs Other Language
| Aspect                   | Rust                                                                                        | Python                                                                         | Java                                                                                                                | C++                                                                               |
| ------------------------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **Syntax**               | ใช้ `\|x\| x + 10` สำหรับ Closure                                                           | ใช้ `lambda x: x + 10`                                                         | ใช้ Lambda เช่น `x -> x + 10`                                                                                       | ใช้ Lambda เช่น `[n](int x) { return x + n; }`                                    |
| **Semantics / Behavior** | Closure สามารถ **capture ตัวแปรจาก environment** และ Rust จะกำหนดวิธี capture ตามการใช้งาน  | Lambda สามารถเข้าถึงตัวแปรจาก scope ภายนอกได้                                  | Lambda สามารถ capture ตัวแปรจาก scope ภายนอกได้ แต่ตัวแปร local ที่ capture ต้องเป็น `final` หรือ effectively final | Lambda สามารถ capture ตัวแปรภายนอกได้ โดยกำหนดวิธี capture ได้                    |
| **Type System**          | Static type system และ Closure แต่ละตัวมี type เฉพาะของตัวเอง พร้อม `Fn`, `FnMut`, `FnOnce` | Dynamic typing และ Lambda เป็น object                                          | Static type system และ Lambda ใช้งานผ่าน Functional Interface                                                       | Static type system และ Lambda มี unnamed closure type                             |
| **Memory Management**    | ใช้ **Ownership, Borrowing และ `move`** ในการจัดการค่าที่ capture                           | ใช้ Garbage Collection / การจัดการ memory อัตโนมัติ                            | ใช้ **Garbage Collection**                                                                                          | ใช้ RAII และสามารถจัดการ memory แบบ explicit ได้                                  |
| **Safety**               | Compiler ตรวจสอบ Type, Ownership และ Borrowing ช่วยป้องกัน memory-related errors            | มีการตรวจสอบแบบ runtime และ Garbage Collection แต่ไม่มีระบบ Ownership แบบ Rust | มี Static Type Checking และ Garbage Collection                                                                      | มี Static Type Checking และ RAII แต่ต้องจัดการ lifetime / pointer อย่างระมัดระวัง |

### Rust Example
```rust
fn main() {
    let n = 10;
    let add_n = |x| x + n;

    println!("{}", add_n(5)); // 15
}
```
### Python Example
```py
n = 10
add_n = lambda x: x + n

print(add_n(5))  # 15
```
### Java Example
```java
import java.util.function.Function;

public class Main {
    public static void main(String[] args) {
        int n = 10;
        Function<Integer, Integer> addN = x -> x + n;

        System.out.println(addN.apply(5)); // 15
    }
}
```

### C++ Example
```cpp
#include <iostream>
using namespace std;

int main() {
    int n = 10;

    auto addN = [n](int x) {
        return x + n;
    };

    cout << addN(5) << endl; // 15
}
```
### Analysis
แม้ Rust, Python, Java และ C++ จะสามารถสร้าง Closure หรือ Lambda ที่ทำงานคล้ายกันได้ แต่แต่ละภาษามีแนวทางการออกแบบที่แตกต่างกัน
* Rust เน้นความปลอดภัยของ Memory โดย Closure ทำงานร่วมกับระบบ Ownership, Borrowing และ Closure Traits (Fn, FnMut, FnOnce)

* Python มี Syntax ที่สั้นและยืดหยุ่น และจัดการ Memory ให้อัตโนมัติ แต่ไม่มีระบบ Ownership และ Borrowing แบบ Rust

* Java ใช้ Lambda Expression ร่วมกับ Functional Interface และมีกฎเรื่องตัวแปรที่ถูก capture ต้องเป็น final หรือ effectively final

* C++ ให้ Programmer กำหนดวิธีการ Capture ได้อย่างชัดเจน เช่น Capture แบบ Value หรือ Reference

---
