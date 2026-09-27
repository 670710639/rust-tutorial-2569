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
| 2 | นายคีรเทพ ก้องสุวรรณ | 670710641 | `@[670710641]` | Detailed Code + Live Demo (โค้ดเชิงลึก + สาธิตสด) |
| 3 | นางสาวจิณณพัต แหล่งหล้า | 670710642 | `@[670710642]` | Rust vs Other Language + PPL Analysis (เปรียบเทียบภาษา + วิเคราะห์เชิง PPL) |
| 4 | นางสาวจุฑารัตน์ รู้วงษ์ | 670710643 | `@[670710643]` | Exercises + Common Mistakes + Challenge (แบบฝึกหัด + ข้อผิดพลาดที่พบบ่อย + คำถามท้าทาย) |

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

`Closure คือฟังก์ชันแบบไม่ระบุชื่อที่สามารถกำหนดขึ้นภายในโปรแกรม โดยมีรูปแบบการเขียนที่กระชับ และสามารถนำไปเก็บไว้ในตัวแปรเพื่อเรียกใช้งานได้`

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

### 4.3 `[Closure Parameters]`

**คำอธิบาย**

`Closure Parameters คือพารามิเตอร์ที่ใช้รับค่าที่ส่งเข้ามาเมื่อเรียกใช้งาน Closure โดยสามารถกำหนดชนิดข้อมูลของพารามิเตอร์ และนำค่าที่รับมาไปประมวลผลภายใน Closure ได้`

**ตัวอย่าง**

```rust
fn main() {
    let add = |x: i32, y: i32| x + y;

    let result = add(5, 3);

    println!("{}", result);
}
```

**Explanation**

`ใน main สร้าง Closure add ที่รับพารามิเตอร์ 2 ตัว คือ x และ y โดยกำหนดให้ทั้งสองตัวเป็นชนิด i32 จากนั้นนำค่าทั้งสองมาบวกกันและคืนผลลัพธ์ออกมา เมื่อเรียก add(5, 3) จะนำค่า 5 และ 3 เข้าไปเป็นพารามิเตอร์ของ Closure จึงคำนวณ 5 + 3 และได้ผลลัพธ์เป็น 8`

---

### 4.4 `[Closure Capture]`

**คำอธิบาย**

`Closure ใน Rust สามารถเข้าถึงตัวแปรที่อยู่นอกขอบเขตของ Closure ได้ ความสามารถนี้เรียกว่า Closure Capture`

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

### 4.5 `[Higher-Order Functions]`

**คำอธิบาย**

`Higher-Order Function คือฟังก์ชันที่สามารถรับฟังก์ชันหรือ Closure เป็นพารามิเตอร์ หรือคืนฟังก์ชัน/Closure กลับมาเป็นผลลัพธ์ได้ แนวคิดนี้ช่วยให้สามารถส่งพฤติกรรมการทำงานเข้าไปให้ฟังก์ชันจัดการได้`

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
