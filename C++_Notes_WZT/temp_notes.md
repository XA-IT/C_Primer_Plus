### C++ general learning
#### 函数
- 含有可变参数的函数
  - 所有实参类型相同，使用`initializer_list<T> lst;`模板初始化，<T>表元素类型，对象元素永远为常量值
  - 类型不同，使用可变参数模板
- 内联函数
  - 不能含有循环与switch语句
  - 定义需在调用之前
  - 不能进行异常接口声明
- constexpr函数
  - 由编译器校验是否为常量表达式
  - 仅能用于字面值类型， 对于指针，constexpr表示常量指针，为顶层const
- 