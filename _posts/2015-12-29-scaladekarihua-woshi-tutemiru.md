---
layout: post
title: Scalaでカリー化を使ってみる
description: Scalaでカリー化を使ってみる
---
## 1.実装するプログラム

URLのパスを作るプログラムを作ってみたいと思います。
/親1/親2/子供というパスで、子供が沢山いるパターンです。

親1を*a*、親2を*b*としてみます。

## 2.カリー化を使わない方法

```
object PathCreator {
  def main(args: Array[String]) {
    val parent1 = "a"
    val parent2 = "b"
    val children = Seq("1.png", "2.png", "3.png")

    val paths = pathCreator(parent1, parent2, children)
    paths.foreach(println)
  }

  def pathCreator(parent1: String, parent2: String, children: Seq[String]): Seq[String] =
    children.map(child => pathCreate(parent1, parent2, child))

  def pathCreate(parent1: String, panret2: String, child: String) =
    s"/$parent1/$panret2/$child"
}
```

次のように書くことになり、処理すべき対象である*children*がわかりづらくなります。
```
val paths = pathCreator(parent1, parent2, children)
```
```
children.map(child => pathCreate(parent1, parent2, child))
```

## 3.親1と親2を受け取って、子供を処理する関数を使う方法

```
object PathCreator {
  def main(args: Array[String]) {
    val parent1 = "a"
    val parent2 = "b"
    val children = Seq("1.png", "2.png", "3.png")

    val paths = pathCreator(parent1, parent2)(children)
    paths.foreach(println)
  }

  val pathCreator = (parent1: String, parent2: String) =>
    (children: Seq[String]) => children.map(child => pathCreate(parent1, parent2, child))

  def pathCreate(parent1: String, panret2: String, child: String) =
    s"/$parent1/$panret2/$child"
}
```

次のように書くことができて、処理すべき対象が*children*だということがわかりやすくなります。

```
val paths = pathCreator(parent1, parent2)(children)
```

## 4.カリー化して書いてみる

3.のようなことをやる場合は、カリー化を使うことができます。

```
object PathCreator {

  def main(args: Array[String]) {
    val parent1 = "a"
    val parent2 = "b"
    val children = Seq("1.png", "2.png", "3.png")

    val paths = pathCreator(parent1, parent2)(children)
    paths.foreach(println)
  }

  def pathCreator(parent1: String, parent2: String)(children: Seq[String]) =
    children.map(child => pathCreate(parent1, parent2, child))

  def pathCreate(parent1: String, panret2: String, child: String) =
    s"/$parent1/$panret2/$child"

}
```

変わっているのは*pathCreator*関数だけです。よりシンプルにわかりやすく書くことができますね。
