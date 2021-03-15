# Rust常用面试题

<details>

  <summary>Copy和Clone的区别？</summary>
  要实现Copy,必须先实现Clone
  
  Copy表示这个struct可以以类似与memcpy的方式Clone
  
  一个自定义struct,必须所有元素都是Copy,整个struct才能copy
</details>
<details>
  <summary> `let a=&*t`是什么意思？</summary>
  `&*t` 表示对t解引用。 相当于 `t.deref()`
  
  `a`的类型和`t`不同
  
  不过也要看情况。比如
  ```
  let a:* const u8;
  let b:&u8=&* a;
  ```
    ```
  let a:* mut u8;
  let b:&mut u8=&* a;
  ```
</details>  

<details>
   <summary>`let a=*&t`是什么意思？</summary>
   `*&t` 表示先取引用，再Copy一份。`t`必须是Copy的
  
   `a`的类型和`t`相同
</details>

<details>
   <summary> `let a:T=b` 在T类型不同时，分别是什么语义？</summary>
  T：Clone + ！Copy  => move 
  
  T：Clone + Copy    => copy
  
  T: !Clone         => move
</details>

<details>
  <summary>`let a:Box<u8>=b` 语义是复制还是move？</summary>
    `Box<T>` 是独占指针，是move
</details>

<details>
  <summary>lifetime 自动推导规则</summary>
  todo!()
 </details>
 
 <details>
  <summary>如何实现一个drop函数</summary>
 fn drop<T>(_x: T) {}
  </details>
  
  <details>
  <summary>HashMap与BTreeMap有什么区别？ BTreeMap为什么没有with_capacity() 方法？</summary>
  todo!()
  </details>
  
  <details>
  <summary>HashMap与HashSet的区别？</summary>
  HashSet是值为 () 的HashMap
  </details>
  
```
let mut a=[0;8];
let mut b=[1;8];
a=b;
println!("{:?}",a);
println!("{:?}",b);
```
  <details>
  <summary>以上代码能否编译？结果是多少</summary>
  可以编译。实现的是复制语义
  </details>
  
  <details>
    <summary> 举一个需要用到Rc的场景 </summary>
   图的表示。每个节点有一个列表，维护邻居节点的指针
  </details>
  
<details>
    <summary>  Rc默认分配的内存在堆上还是stack上？ </summary> 
  stack上
  要让Rc指向堆，要这么写
  `Rc<Box<T>>  `
</details>

  <details>
  <summary>什么是Send Trait,Sync Trait</summary>
  T:Send -> T 可以安全的move到另一个线程
  T:Sync -> 多个线程持有 &T 是安全的
  </details>
  
<details>
  <summary>为什么Rc没有Send Trait？</summary>
  因为Rc中的计数器没有用原子操作，不是线程安全的
  而Arc中的计数器用了原子操作，是线程安全的
  </details>
  
  <details>
  <summary>为什么RefCell没有Sync Trait？</summary>
  因为RefCell里有读计数器和写计数器。这两个计数器没有用
  </details>
  
<details>
      <summary>const与static的相同点和区别？</summary>
      相同点：
      1. 写的时候要标注类型
      2.  只能被 constant functions and values赋值
      
      不同点：
      static可修改，const 
</details>

<details>
<summary>static变量做什么用？</summary>
可以声明在函数中，用来统计函数的访问次数。
就算函数退出，也不会释放
```
fn ff() {
    static mut a: u32 = 1;
    unsafe {
        a += 1;
        println!("{}", a);
    }
}

fn main() {
    ff();
    ff();
    ff();
}

```
</details>

