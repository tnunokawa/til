---
layout: post
title: "Java Bronze 要点"
date: 2025-10-18
last_modified_at: 2025-10-18
categories: [Java]
tags: [Java Bronze, 試験対策]
---


# java Bronze要点

## オーバーライド
**コード**

```java
public class A {
	public void speak() {
		System.out.println("Hello.");
	}
}

public class B extends A {
	public void speak() {
		System.out.println("Good morning.");
	}
}

public class Hello {

	public static void main(String[] args) {
		// オーバーライドと実行結果
		// 実行時の型に従う
		A a = new B();
		a.speak();
    }
}
```

**実行結果**

```
Good morning.
```

**解説**
- オーバーライドとは、スーパークラス（親クラス）のメソッドをサブクラス（子クラス）で再定義すること。
- オーバーライドされたメソッドは、実行時のオブジェクトの型に基づいて呼び出される。
- 上記の例では、`A a = new B();` により、変数 `a` は型 `A` だが、実際のオブジェクトは型 `B` であるため、`B` クラスの `speak` メソッドが呼び出される。
- これにより、ポリモーフィズム（多態性）が実現され、同じメソッド呼び出しが異なる動作をすることが可能になる。
- まとめると、オーバーライドされたメソッドは、変数の型ではなく、実際のオブジェクトの型に基づいて決定される。

## オーバーロード

**コード**

```java
public class C {
	void hello(String name) {
		System.out.println("Hello " + name);
	}

	void hello(int times) {
		for (int i = 0; i < times; i++) {
			System.out.println("Hello");
		}
	}
}

public class Hello {

	public static void main(String[] args) {
        		//　オーバーロード
		C c = new C();
		c.hello("Taro");
		c.hello(3);
	}

}
```
**実行結果**

```
Hello Taro
Hello
Hello
Hello
``` 
**解説**
- オーバーロードとは、同じ名前のメソッドを複数定義すること。
- メソッドの引数の型や数が異なる場合に、同じ名前のメソッドを定義できる。
- 上記の例では、`hello` メソッドが2つ定義されており、1つは `String` 型の引数を受け取り、もう1つは `int` 型の引数を受け取る。
- メソッド呼び出し時に、引数の型や数に基づいて適切なメソッドが選択される。
- まとめると、オーバーロードは同じ名前のメソッドを異なる引数で定義し、呼び出し時に適切なメソッドが選ばれる仕組みである。


## クラスやメソッドのアクセス範囲（アクセス修飾子）
**アクセス修飾子**
| 修飾子 | アクセスできる範囲 |
| :-- | :-- |
| `public` | どこからでもOK（全クラスからアクセス可能） |
| `protected` | 同じパッケージ内、またはサブクラスからアクセス可能 |
| (デフォルト) | 同じパッケージ内からのみアクセス可能 |
| `private` | 同じクラス内からのみアクセス可能 |

**クラスにつけられる修飾子**
- トップレベルのクラス（＝ファイル直下のクラス）
  - `public`またはデフォルト(修飾子なし)のみ

```java
public class A {}   // OK
class B {}          // OK（デフォルト）
private class C {}  // ❌ エラー（トップレベルクラスには使えない）
```

- 内部クラス（クラスの中に定義されるクラス）
  - すべてのアクセス修飾子`public`, `protected`, `private`が使用可能

```java
public class A {
    class B {}          // OK（デフォルト）
    public class C {}   // OK
    protected class D {}// OK
    private class E {}  // OK
}
```

**メソッドやフィールドにつけられる修飾子**
- すべてのアクセス修飾子`public`, `protected`, `private`が使用可能

```java
public class A {
    public int x;        // どこからでもアクセス可能
    protected int y;     // サブクラス or 同じパッケージからアクセス可能
    int z;               // 同じパッケージ内だけアクセス可能（デフォルト）
    private int w;       // 同じクラス内だけアクセス可能

    public void method1() {}        
    protected void method2() {}     
    void method3() {}               
    private void method4() {}   
}
```

**試験でよく出るポイント**
- `private`は同じクラス内からのみアクセス可能。
```java
class A {
    private int x = 10;
}

class B {
    void show() {
        A a = new A();
        System.out.println(a.x); // ❌ エラー！
    }
}
```
- `protected`は同じパッケージ内、またはサブクラスからアクセス可能。
```java
package pkg1;
public class A {
    protected int x = 10;
}
package pkg2;
import pkg1.A;
public class B extends A {
    void show() {
        System.out.println(x); // OK（サブクラスだから）
    }
}
package pkg2;
import pkg1.A;
public class C {
    void show() {
        A a = new A();
        System.out.println(a.x); // ❌ エラー！（サブクラスじゃないし、パッケージも違う）
    }
}
```

- トップレベルクラスには private / protected は使えない
```java
private class A {} // ❌ エラー！
protected class B {} // ❌ エラー！
```

## 不正な代入によるコンパイルエラー

- byte型は-128から127までの整数を表現できる。
- short型は-32,768から32,767までの整数を表現できる。
- int型は-2,147,483,648から2,147,483,647までの整数を表現できる。
- long型は-9,223,372,036,854,775,808から9,223,372,036,854,775,807までの整数を表現できる。
- float型は約7桁の精度で小数を表現できる。

```java
public class Test {
    public static void main(String[] args) {
        byte b = 128; // ❌ エラー！ byteの範囲を超えている
        short s = 40000; // ❌ エラー！ shortの範囲を超えている
        int i = 3.14; // ❌ エラー！ int型に小数は代入できない
        long l = 2147483648; // ❌ エラー！ intの範囲を超えている（long型のリテラルにはLをつける）
        long l2 = 2147483648L; // OK
        float f = 3.14; // ❌ エラー！ float型のリテラルにはfをつける
        flaot f2 = 3.14f; // OK

    }
}
``` 

## switch文のcaseラベルに使える型
- switch文のcaseラベルには、以下の型が使用可能
  - `int`型およびそのラッパークラス`Integer`
  - `char`型およびそのラッパークラス`Character`
  - `String`型
  - `enum`型
- `long`型、`float`型、`double`型、`boolean`型、およびそれらのラッパークラスは使用できない。
```java
public class Test { 
    public static void main(String[] args) {
        long l = 10L;
        switch (l) { // ❌ エラー！ long型は使えない
            case 10L:
                System.out.println("Ten");
                break;
            default:
                System.out.println("Other");
                break;
        }
    }
}
```

## メモ
 - `this();` は コンストラクタの中で、同じクラス内の別のコンストラクタを呼び出すためのもの。
 - `this();` は 必ず1行目に書かないとコンパイルエラーになる。
 - `super();` は スーパークラス（親クラス）のコンストラクタを呼び出すためのもの。
 - `super();` も 必ず1行目に書かないとコンパイルエラーになる。
 - staticなメソッドからは非staticなメソッドやフィールドにアクセスできない。
 - Javaの関係演算子のなかに、英単語の「and」や「or」はない。`&&`や`||`を使う。
 - 条件式のなかに「=」は原則使えないが`if (flag = true)`のように書くと、`flag`に`true`を代入したうえで、その値（true）を条件式として評価するので、コンパイルエラーにはならない。ただし、これはバグのもとになるので避けるべき。
