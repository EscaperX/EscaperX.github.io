---
title: The First Article by Cyc
date: 2022-09-18 16:49:18
draft: true
tags:
categories: [Diary]
---

reports for project 1.
<!--more-->

# Project1: Deque - Data Structures

## 0. 反思

下面的问题是Lab5-Peer Code Review的内容。就是TA先讲一下他们的code思路，然后几个同学一组交流自己写的code。都是很值得我去想的问题，每个问题都击中了我的心巴。

Some suggested questions are listed below:

1. What was the most annoying bug you had and how did you fix it? Did you use the debugger? Did you fix it by adding special cases? Did you do any change-and-pray (where you make a tiny change and hope the AG approves)?
2. Did you end up cutting anything out to make your code simpler? If so, what?
3. Do you have any special cases in your code?
4. Do you have any private helper methods?
5. Does your code repeat itself anywhere? Would private helper methods have helped?
6. Were you able to call or reuse code anywhere?

## 1. Project Review

一句话概括，这个项目是让我们用list/array来实现Deque，在此基础上应用这个Deque做一些有趣的事。主要内容分为两块：

1、**the data structure portion:** 实现Deque。

在这一部分，需要创建两个java files：`LinkedListDeque.java` and `ArrayDeque.java`, with public methods listed below. You will be verifying the correctness of these data structures yourself using the randomized and timing test skills you gained from Lab 3.

2、**the application portion:** 应用Deque。

在这一部分，you’ll create a Java file `MaxArrayDeque.java` as well as use your package to ultimately implement a sound synthesizer （一个声音合成器？）capable of playing music from Guitar Hero. You must test your `MaxArrayDeque`, but we’ll provide the tests for sound synthesizer.

## 2. the Deque API

首先，Deque的 <mark>定义</mark>：

> Deque (usually pronounced like “deck”) is an irregular acronym of double-ended queue. Double-ended queues are sequence containers with dynamic sizes that can be expanded or contracted on both ends (either its front or its back).

Deque和之前lecture里讲过的SLList和AList结构上其实非常类似。

具体来说，**any deque implementation must have exactly the following operations**:

- `public void addFirst(T item)`: Adds an item of type `T` to the front of the deque. You can assume that `item` is never `null`.
- `public void addLast(T item)`: Adds an item of type `T` to the back of the deque. You can assume that `item` is never `null`.
- `public boolean isEmpty()`: Returns `true` if deque is empty, `false` otherwise.
- `public int size()`: Returns the number of items in the deque.
- `public void printDeque()`: Prints the items in the deque from first to last, separated by a space. Once all the items have been printed, print out a new line.
- `public T removeFirst()`: Removes and returns the item at the front of the deque. If no such item exists, returns `null`.
- `public T removeLast()`: Removes and returns the item at the back of the deque. If no such item exists, returns `null`.
- `public T get(int index)`: Gets the item at the given index, where 0 is the front, 1 is the next item, and so forth. If no such item exists, returns `null`. Must not alter the deque!

此外，在这个项目中，we also want our two Deques to **implement these two special methods**:

（今天刚学完iter的内容，来写一下这部分。8月2日）

- `public Iterator<T> iterator()`: The Deque objects we’ll make are iterable (i.e. `Iterable<T>`) so we must provide this method to return an iterator.

  <font color = green>ArrayDeque的写法和lecture里面ArraySet这个例子差不多。LinkedListDeque的写法也是基于这个class本身的结构。我自己写了一个test通过了，但是不知道事实上如何。等这部分都写完再去ag里面提交。 </font>

  <font color = red>这个部分，自己写的时候犯的错误是，在ArrayDeque里返回的next是items[i]，但其实应该是get(i)噢。因为在Deque里第一个元素不一定是物理位置上的下一个下标。感觉这个错误其实也违反了abstraction barrier来着？挠挠挠挠挠头。</font>

- `public boolean equals(Object o)`: Returns whether or not the parameter `o` is equal to the Deque. `o` is considered equal if it is a Deque and if it contains the same contents (as goverened by the generic `T`’s `equals` method) in the same order. (ADDED 2/12: You’ll need to use the `instance of` keywords for this. Read [here](https://www.javatpoint.com/downcasting-with-instanceof-operator) for more information)

  > **instanceof**: the java `instanceof` operator is used to test whether the object is an instance of the sepcified type (class or subclass or interface).
  >
  > The `instanceof` in java is also known as type *comparison* operator because it compares the instance with type. It returns either true or false. If we apply this operator with any variable that has null value, it returns false.
  >
  > <img src="image/Project1 Deque/image-20220802214354300.png" alt="image-20220802214354300" style="zoom:67%;" />

  <font color = green>这个方法我在LinkedListDeque和ArrayDeque里写得一样，就是写完一个然后复制过去的。挠头，有什么不需要copy一遍的方法吗？还是我的写法本身有问题捏？</font>

  <font color = red>AG一直说我deep equals failed。到底哪里有问题，我自己写的test是可以的呀。无语了，摸不着头脑…把我自己写的body部分删掉get(i) instanceof Deque这个部分，就可以我认可了，但是真的不知道二者有什么差别啊。。</font>

  <font color = red>aha,我突然领悟了？比如两个object是这样的，每个box中装的是Dog类的object，这样就会进入我写的第二个判断条件（else那里），但是对于object来说，==是不能满足我这里的目的的，应该用equals。</font>原来是这样，一时间悲喜交加，感到我还是挺聪明的，但是又很容易被当前的情境禁锢住，想当然地忽略了general的情景。

  ```java
  /* test failed! */
  public boolean equals(Object o) {
          if (o == null) { return false; }
          if (!(o instanceof Deque)) { return false; }
          if (o == this) { return true; }
          Deque<T> other = (Deque<T>) o;
          if (other.size() != this.size()) { return false; }

          for (int i = 0; i < size; i += 1) {
              if (this.get(i) instanceof Deque) {
                  if (!this.get(i).equals(other.get(i))) {
                      return false;
                  }
              } else {
                  if (this.get(i) != other.get(i)) {
                      return false;
                  }
              }
          }
          return true;
      }
  ```

  ```java
  /* test passed! */
  public boolean equals(Object o) {
          if (o == null) {
              return false;
          }
          if (!(o instanceof Deque)) { return false; }
          if (o == this) {
              return true;
          }
          Deque other = (Deque) o;
          if (other.size() != this.size()) {
              return false;
          }
          for (int i = 0; i < size; i += 1) {
              if (!this.get(i).equals(other.get(i))) {
                  return false;
              }
          }
          return true;
      }
  ```



**需要注意的几点**：

1.You should not have your `Deque` interface implement `Iterable` but rather just the two implementations `LinkedListDeque` and `ArrayDeque`. If you do the former, our autograder will give you API errors. （<font color = red>意思是，是由LinkedListDeque和ArrayDeque这两个class来implement `Iterable`这个接口？</font>）

2.Your class should accept any generic type (not just integers). For information on creating and using generic data structures, see [lecture 5](https://docs.google.com/presentation/d/19TTe3JgFscc4RLwokvQ_gOM72DSrfs9Y6ZST_fv3aQ4). Make sure to pay close attention to the rules of thumb on the last slide about generics.

3.In this project, you will provide two implementations for the Deque interface: one powered by a Linked List, and one by a resizing array.

## 3. 具体的project tasks：

### 1. Linked List Deque

基于Linked List实现deque（build the `LinkedListDeque` class）。

**Implement all the methods listed above in “The Deque API” section.**

Your operations are subject to the following rules:

- `add` and `remove` operations must not involve any looping or recursion. A single such operation must take “constant time”, i.e. execution time should not depend on the size of the deque. This means that you cannot use loops that go over all/most elements of the deque.
- `get` must use iteration, not recursion.
- `size` must take constant time.
- Iterating over the `LinkedListDeque` using a for-each loop should take time proportional to the number of items.
- Do not maintain references to items that are no longer in the deque. The amount of memory that your program uses at any given time must be proportional to the number of items. For example, if you add 10,000 items to the deque, and then remove 9,999 items, the resulting memory usage should amount to a deque with 1 item, and not 10,000. Remember that the Java garbage collector will “delete” things for us if and only if there are no pointers to that object.

此外，**you also need to implement:**

- `public LinkedListDeque()`: Creates an empty linked list deque.
- `public T getRecursive(int index)`: Same as get, but uses recursion.

While this may sound simple, there are many design issues to consider, and you may find the implementation more challenging than you’d expect. Make sure to consult the lecture on doubly linked lists, particularly the slides on sentinel nodes: [two sentinel topology](https://docs.google.com/presentation/d/1suIeJ1SIGxoNDT8enLwsSrMxcw4JTvJBsMcdARpqQCk/pub?start=false&loop=false&delayms=3000&slide=id.g829fe3f43_0_291), and [circular sentinel topology](https://docs.google.com/presentation/d/1suIeJ1SIGxoNDT8enLwsSrMxcw4JTvJBsMcdARpqQCk/pub?start=false&loop=false&delayms=3000&slide=id.g829fe3f43_0_376). I prefer the circular approach. **You are not allowed to use Java’s built in LinkedList data structure (or any data structure from `java.util.\*`) in your implementation** and the autograder will instantly give you a 0 if we detect that you’ve imported any such data structure.

### 2. Array Deque

**Implement all the methods listed above in “The Deque API” section.**

**For this implementation, your operations are subject to the following rules:**

- `add` and `remove` must take constant time, except during resizing operations.
- `get` and `size` must take constant time.
- The starting size of your array should be 8.
- The amount of memory that your program uses at any given time must be proportional to the number of items（意思是array中不能有太多空间是空的，利用率要大于25%）. For example, if you add 10,000 items to the deque, and then remove 9,999 items, you shouldn’t still be using an array of length 10,000ish. **For arrays of length 16 or more, your usage factor should always be at least 25%.** This means that ==before== performing a remove operation that will bring the number of elements in the array under 25% the length of the array, you should resize the size of the array down. For smaller arrays, your usage factor can be arbitrarily low.

**In addition, you also need to implement:**

- `public ArrayDeque()`: Creates an empty array deque.

==You will need to somehow keep track of what array indices hold the Deque’s front and back elements.== We *strongly recommend* that you treat your array as ==circular== for this exercise. In other words, if your front item is at position zero, and you `addFirst`, the new front should loop back around to the end of the array (so the new front item in the deque will be the last item in the underlying array). This will result in far fewer headaches than non-circular approaches. See the [project 1 demo slides](https://docs.google.com/presentation/d/1XBJOht0xWz1tEvLuvOL4lOIaY0NSfArXAvqgkrx0zpc/edit#slide=id.g1094ff4355_0_450) for more details.

Correctly ==resizing== your array is **very tricky**, and will require some deep thought（不要害怕！动动你优秀的小脑袋！🧠）. **Try drawing out various approaches by hand**. It may take you quite some time to come up with the right approach, and we encourage you to debate the big ideas with your fellow students or TAs. Make sure that your actual implementation **is by you alone**.

<font color =red>ArrayDeque，加上resize和resizeDown之后就一直有问题，连之前已经pass的get和add/remove也会出现问题。怎么会这样呢。感觉自己的code太长了，脑子也一团浆糊。看到tips里说，“Consider a helper function to do little tasks like compute array indices. For example, in my implementation of `ArrayDeque`, I wrote a function called `int minusOne(int index)` that computed the index immediately “before” a given index.”，但是我==不明白这样的helper function有什么意义==？不是只要写一下index-1就可以了吗？</font>

<font color = red>随便查了一下：Help function（辅助函数）本质上还是一个函数，其实没啥神秘的。就是把另外一个函数中的计算过程(比如取平均数，求方差等等)抽出来，单独写成的函数。你可能会问，为啥要如此多此一举？其实还是为了**可读性**，这样通过给相应的辅助函数一个清晰易理解的名字，能够帮助你更好的去读程序。还有一个好处是可以**方便复用**。</font>

==看了一下别人的code，发现自己之前写的resize太麻烦了（虽然还是不知道哪里有bug。。）==

我自己写的是：

> ```java
> System.arraycopy(items, 0, a, 0, nextLast);
> System.arraycopy(items, nextFirst + 1, a, a.length - (size - nextLast), size - nextLast);
> nextFirst = a.length - 1 - (size - nextLast);
> ```

在resizeDown里面更麻烦，还要考虑nextFirst/nextLast在不同位置的情况。主要是我自己之前没想过可以有不同的复制array的办法，一直在arrycopy…

还有一点很麻烦的是在remove的方法中，也要考虑nextFirst/nextLast在不同位置的情况，但是其实只需要：

```java
        T front;
//        if (nextFirst == items.length - 1) {
//            front = items[0];
//            items[0] = null;
//        } else {
//            front = items[nextFirst + 1];
//            items[nextFirst + 1] = null;
//        }
        front = items[loop(nextFirst + 1)];
        items[loop(nextFirst + 1)] = null;
```



### 3. (Extra Credit) Autograder

### 4. MaxArrayDeque

After you’ve fully implemented your `ArrayDeque` and tested its correctness, you will now build the `MaxArrayDeque`. A `MaxArrayDeque` has all of the methods that an `ArrayDeque` has, ==but it also has 2 additional methods and a new constructor==:

- `public MaxArrayDeque(Comparator<T> c)`: creates a `MaxArrayDeque` with the given `Comparator`.
- `public T max()`: returns the maximum element in the deque as governed by the previously given `Comparator`. If the `MaxArrayDeque` is empty, simply return `null`.
- `public T max(Comparator<T> c)`: returns the maximum element in the deque as governed by the parameter `Comparator c`. If the `MaxArrayDeque` is empty, simply return `null`.

==The `MaxArrayDeque` can either tell you the max element in itself by using the `Comparator<T>` given to it in the constructor, or an arbitrary `Comparator<T>` that is different from the one given in the constructor.==

We do not care about the `equals(Object o)` method of this class, so feel free to define it however you think is most appropriate. We will not test this method.

If you find yourself starting off by copying your entire `ArrayDeque` implementation in a `MaxArrayDeque` file, then you’re doing it wrong. **This is an exercise in clean code, and redundancy is one our worst enemies when battling complexity!** For a hint, re-read the second sentence of this section above.

There are no runtime requirements on these additional methods, we only care about the correctness of your answer. ==Sometimes, there might be multiple elements in the `MaxArrayDeque` that are all equal and hence all the max: in in this case, you can return any of them and they will be considered correct.==

You should write tests for this part as well! They do not need to be nearly as robust as your randomized and timing tests you created for the two Deque implementations above since the functionality you’re adding is fairly simple. ==You’ll likely be creating multiple `Comparator<T>` classes to test your code: this is the point! To get practice using `Comparator` objects to do something useful (find the maximum element) and to get practice writing your own `Comparator` classes.== You will not be turning in these tests, but we still highly suggest making them for your sake.

You will not use the `MaxArrayDeque` you made for the next part. It is it’s own isolated exercise.

<font color = green>怎么说呢，写起来确实是不难的。但是自己还是写了快四个小时？主要原因还是在于没有很好地理解class/method的调用？？反正就是没有彻底弄明白这个任务的意思，就开始写了。挠头。语言表达不出我的问题所在。</font>

<font color = red>这里在AG上有一个failed，说是time out. 然后我检查了一下自己写的，是这样的:</font>

```java
 public T max() {
        if (this.isEmpty()) { return null; }
        int maxPos = 0;
        for (int i = 0; i < this.size(); i += 1) {
            int cmp = defaultCpt.compare(this.get(i), this.get(maxPos));
            if (cmp > 0) { maxPos = i; }
        }
        return this.get(maxPos);
    }
```

<font color = red>然后改成下面的样子就可以了。我一开始觉得可能是foreach比for更快吗，但是查了一下发现二者速度的差别要很大的数量下才能体现。再看了一下code，发现如果按照我上面的写法，就还要加上get(i)这个步骤，那确实应该是要更慢一点的，挠头。</font>

```java
 public T max() {
        if (this.isEmpty()) {
            return null;
        }
        T maxItem = this.get(0);
        for (T i:this) {
            if (defaultCpt.compare(i, maxItem) > 0) {
                maxItem = i;
            }
        }
        return maxItem;
    }
```

———8月11日———proj1终于写完啦！🎇虽然还有extra credit的部分和just for fun的部分没写———

![image-20220811153139622](image/Project1 Deque/image-20220811153139622.png)

