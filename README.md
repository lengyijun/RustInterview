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
