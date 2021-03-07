# Rust常用面试题

<details>

  <summary>Copy和Clone的区别？</summary>
  要实现Copy,必须先实现Clone
  
  Copy表示这个struct可以以类似与memcpy的方式Clone
  
  一个自定义struct,必须所有元素都是Copy,整个struct才能copy

</details>

