# Rust Tutorial Project — Principles of Programming Languages

> **กลุ่มที่:** 19
> **Topic No.:** 19
> **Topic Name:** Closures & Functional Programming
> **ประเด็นหลักที่ควรครอบคลุม:** closures, parameters, capture, higher-order functions และ functional programming

---

## 1. Members

| # | Name | Student ID | GitHub Username | Main Responsibility |
|---|---|---|---|---|
| 1 | นายก้องภพ คุณดำรงชัย | 670710639 | `@[670710639]` | Concept + Short Code Illustration (สรุปแนวคิดหลัก + โค้ดตัวอย่างสั้น) |
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

Functional Programming เป็นแนวคิดการเขียนโปรแกรมที่เน้นการใช้ฟังก์ชันในการประมวลผลข้อมูลและแบ่งการทำงานออกเป็นส่วนย่อย ๆ เพื่อให้โค้ดสามารถนำกลับมาใช้ซ้ำได้

Closure เป็นฟังก์ชันรูปแบบหนึ่งที่สามารถกำหนดขึ้นภายในโปรแกรม และสามารถเข้าถึงตัวแปรจากบริบทภายนอกได้ ใน Rust Closure สามารถนำมาใช้ร่วมกับแนวคิด Functional Programming เพื่อเขียนโค้ดให้กระชับและจัดการข้อมูลได้สะดวกขึ้น เช่น การใช้ map และ filter

---

*โครงสร้างเอกสารฉบับเต็ม (Key Concepts, Runnable Code Examples, Common Mistakes, Exercises, PPL Perspective, Rust vs Other Language, References, AI Usage Declaration, GitHub Contribution, Final Checklist) ให้ทำต่อจากจุดนี้ตาม Template หลักของวิชา (`rust_tutorial_template.md`) ที่แนบมากับใบมอบหมายงาน*

## 4. Key Concepts

### 4.1 `[Functional Programming]`

**คำอธิบาย**

`Functional Programming เป็นแนวคิดการเขียนโปรแกรมที่เน้นการใช้ฟังก์ชันในการประมวลผลข้อมูล และแบ่งการทำงานออกเป็นส่วนย่อย ๆ เพื่อให้โค้ดสามารถนำกลับมาใช้ซ้ำได้`

**ตัวอย่าง**

```rust
fn add(a: i32, b: i32) -> i32 {
    a + b
}

fn main() {
    let result = add(5, 3);
    println!("{}", result);
}
```

**Explanation**

`ฟังก์ชัน add รับค่าจำนวนเต็ม 2 ค่า คือ a และ b จากนั้นนำค่าทั้งสองมาบวกกันและคืนค่าผลลัพธ์กลับมา เมื่อเรียก add(5, 3) จะได้ผลลัพธ์เป็น 8 และนำไปแสดงด้วย println!`

---

### 4.2 `[Closure]`

**คำอธิบาย**

`[Closure คือฟังก์ชันรูปแบบหนึ่งที่สามารถกำหนดขึ้นภายในโปรแกรม โดยมีรูปแบบการเขียนที่กระชับ และสามารถนำไปเก็บไว้ในตัวแปรเพื่อเรียกใช้งานได้]`

**ตัวอย่าง**

```rust
fn main() {
    let add = |a, b| a + b;

    let result = add(5, 3);
    println!("{}", result);
}
```

**Explanation**

`|a, b| a + b คือ Closure ที่รับค่า a และ b แล้วนำมาบวกกัน จากนั้นเก็บ Closure นี้ไว้ในตัวแปร add เมื่อเรียก add(5, 3) จะได้ผลลัพธ์เป็น 8 แล้วเก็บไว้ในตัวแปร result ก่อนนำไปแสดงผล`

---

### 4.3 `[Closure Capture]`

**คำอธิบาย**

`[Closure ใน Rust สามารถเข้าถึงตัวแปรที่อยู่นอกขอบเขตของ Closure ได้ ความสามารถนี้เรียกว่า Closure Capture]`

**ตัวอย่าง**

```rust
fn main() {
    let x = 10;

    let add_x = |n| n + x;

    println!("{}", add_x(5));
}
```

**Explanation**

`ตัวแปร x ถูกสร้างขึ้นภายนอก Closure และมีค่าเป็น 10 จากนั้น Closure add_x รับค่า n และนำไปบวกกับ x เมื่อเรียก add_x(5) ค่า n จะเป็น 5 และ Closure สามารถเข้าถึง x ที่อยู่ภายนอกได้ จึงคำนวณ 5 + 10 และแสดงผลเป็น 15`

---

### 4.4 `[Iterator และ Closure]`

**คำอธิบาย**

`[Closure สามารถนำมาใช้ร่วมกับ Iterator เพื่อประมวลผลข้อมูลใน Collection ได้ เช่น การใช้ map เพื่อเปลี่ยนแปลงข้อมูลของสมาชิกแต่ละตัว]`

**ตัวอย่าง**

```rust
fn main() {
    let numbers = vec![1, 2, 3, 4, 5];

    let result: Vec<i32> = numbers
        .iter()
        .map(|x| x * 2)
        .collect();

    println!("{:?}", result);
}
```

**Explanation**

`numbers เป็น Vector ที่มีค่า 1 ถึง 5 จากนั้น .iter() ใช้สร้าง Iterator สำหรับเข้าถึงสมาชิกใน Vector และ .map(|x| x * 2) นำ Closure ไปใช้กับสมาชิกแต่ละตัว โดยคูณแต่ละค่าด้วย 2 จากนั้น .collect() นำผลลัพธ์มารวมเป็น Vec<i32> จึงได้ผลลัพธ์เป็น [2, 4, 6, 8, 10]`

---

### 4.5 `[Higher-Order Functions]`

**คำอธิบาย**

`[Higher-Order Function คือฟังก์ชันที่สามารถรับฟังก์ชันหรือ Closure เป็นพารามิเตอร์ หรือคืนฟังก์ชัน/Closure กลับมาเป็นผลลัพธ์ได้ แนวคิดนี้ช่วยให้สามารถส่งพฤติกรรมการทำงานเข้าไปให้ฟังก์ชันจัดการได้]`

**ตัวอย่าง**

```rust
fn apply<F>(value: i32, operation: F) -> i32
where
    F: Fn(i32) -> i32,
{
    operation(value)
}

fn main() {
    let double = |x| x * 2;

    let result = apply(5, double);

    println!("{}", result);
}
```

**Explanation**

`ฟังก์ชัน apply รับพารามิเตอร์ 2 ตัว คือ value และ operation โดย operation เป็น Closure ที่รับ i32 และคืนค่า i32ใน main สร้าง Closure double ที่นำค่าที่รับเข้ามาคูณด้วย 2 จากนั้นส่ง 5 และ double เข้าไปใน apply
เมื่อ apply(5, double) ทำงาน Closure double จะถูกนำไปใช้กับค่า 5 จึงคำนวณ 5 × 2 และได้ผลลัพธ์เป็น 10`

---
