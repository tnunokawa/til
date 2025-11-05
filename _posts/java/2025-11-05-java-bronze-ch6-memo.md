---
layout: post
title: "Java Bronze 黒本 第6章 メモ"
date: 2025-11-05
last_modified_at: 2025-11-05
categories: [Java]
tags: [Java Bronze, 試験対策, 黒本]
---

現在1周

# 🧩 Java Bronze 黒本 6章1周目 結果

---

## No.1
**選択肢:** A,D×A,B  
**結果:** ×  
**ポイント:**
クラス名の1文字目以降は、Unicodeの文字、_(アンダースコア)、$のいずれかでなければならない。2文字目以降はこれに加え数字も使用できる。

---

## No.2
**選択肢:** A,B,C  
**結果:** 〇  
**ポイント:**

---

## No.3
**選択肢:** D  
**結果:** 〇  
**ポイント:**

---

## No.4
**選択肢:** B  
**結果:** 〇  
**ポイント:**

---

## No.5
**選択肢:** C  
**結果:** 〇  
**ポイント:**

---

## No.6
**選択肢:** A  
**結果:** 〇  
**ポイント:**

---

## No.7
**選択肢:** A  
**結果:** 〇  
**ポイント:**

---

## No.8
**選択肢:** D   
**結果:** 〇  
**ポイント:**  

---

## No.9
**選択肢:** C,D,E,F×A,D,E,G  
**結果:** ×  
**ポイント:**
メソッドのシグニチャに含まれるものは、メソッド名、引数の数、引数の型、引数の順番。シグニチャとは、メソッドを一意に特定するための情報のこと。アクセス修飾子、戻り値の型、例外情報は含まれない。シグネチャに含まれる情報が1つでも違えば別メソッド（オーバーロードも含む）としてみなされる。

---

## No.10
**選択肢:** B,C  
**結果:** 〇  
**ポイント:**

---

## No.11
**選択肢:** C  
**結果:** 〇  
**ポイント:**

---

## No.12
**選択肢:** B  
**結果:** 〇  
**ポイント:**

---

## No.13
**選択肢:** B×C  
**結果:** ×  
**ポイント:**
コンストラクタを明示的に記述した場合は、デフォルトコンストラクタは自動的には生成されない。コンストラクタを1つも記述しなかった場合に限り、引数なしのデフォルトコンストラクタが自動生成される。
```java
public static void main(String[] args) {
    Sample sample = new Sample(); // コンパイルエラー
}

public class Sample {
    // コンストラクタを明示的に記述
    public Sample(int value) {
        // 処理
    }
}  
```   

---

## No.14
**選択肢:** C  
**結果:** 〇  
**ポイント:**

---

## No.15
**選択肢:** B  
**結果:** 〇  
**ポイント:**

---

## No.16
**選択肢:** A  
**結果:** 〇  
**ポイント:**

---

## No.17
**選択肢:** B  
**結果:** 〇  
**ポイント:**

---

## No.18
**選択肢:** A,D  
**結果:** 〇  
**ポイント:**

---

## No.19
**選択肢:** D   
**結果:** 〇  
**ポイント:**  

---

## No.20
**選択肢:** D×B  
**結果:** ×  
**ポイント:**
staticフィールドはインスタンスを生成しなくて利用できるフィールド。すべてのインスタンスで共有される。  
クラス名.メンバー名でアクセスする対象はstaticメンバーでないとコンパイルエラーになる。  
```java
public class Main {
    public static void main(String[] args) {
        System.out.println(ClassA.str);
    }
}

class ClassA {
    static String str = "Hello"; // staticフィールド
}
```
※同じパッケージ内（ソースファイル内）にあるクラスはpublic修飾子がなくてもアクセス可能。

---

## No.21
**選択肢:** B  
**結果:** 〇  
**ポイント:**

---

## No.22
**選択肢:** B×C  
**結果:** ×  
**ポイント:**
staticフィールドはすべてのインスタンスで共有される。
```java
public class Main {
    public static void main(String[] args) {
        P p1 = new P();
        P p2 = new P();
        p1.c = 1;
        System.out.println(p2.c);
    }
}
class P {
    public static int c = 0; // staticフィールド
}
```
↓
```
1
```
↑のような書き方は非推奨。staticフィールドはクラス名.フィールド名でアクセスするのが一般的。

---

## No.23
**選択肢:** D  
**結果:** 〇  
**ポイント:**
クラス名.メンバー名でアクセスする対象はstaticメンバーでないとコンパイルエラーになる。メソッドも同様。
```java
public class Main {
    public static void main(String[] args) {
        MyClass.myMethod();
    }
}
class MyClass {
    public static void myMethod() {
        System.out.println("Hello");
    }
}
```  

---

## No.24
**選択肢:** B  
**結果:** 〇  
**ポイント:**

---

## No.25
**選択肢:** B×C  
**結果:** ×  
**ポイント:**
staticメソッド内では、インスタンスフィールドやインスタンスメソッドに直接アクセスできない
```java
public class Main {
    public static void main(String[] args) {
        MyClass.myStaticMethod();
    }
}

class MyClass {
    public int myField = 0; // インスタンスフィールド
    public static void myStaticMethod() {
        System.out.println(myField); // コンパイルエラー
    }
}
```

---

## No.26
**選択肢:** A×C  
**結果:** ×  
**ポイント:**
staticフィールドはすべてのインスタンスで共有される。


---

### ✅ 1週目結果
正答率: 73% (19/26問)  
**傾向メモ:**
 - staticメンバー関連でミスが多い
 - シグニチャの理解があいまい
 - コンストラクタの挙動を再確認必要