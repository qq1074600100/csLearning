# C++细节知识

### extern "C"

- 功能

  让被修饰的代码以C语言方式编译

- 用途

  开发或使用C语言编译的第三方框架/库，

  > - 问题
  >
  >   例如math.c以C语言方式编译，
  >
  >   math.h在C++项目中以C++方式编译函数声明
  >
  >   于是两种函数名不同，解析符号错误解决方案
  >
  > - 解决方案
  >
  >   以extern “C” 包含math.h中的声明(但这样只能C++引用，C不能引用)
  >
  >   ***进一步用预编译命令(#ifdef __cplusplus   该宏是C++默认定义的宏)将extern “C”包裹 

- 用法

  1. 修饰函数（注意：声明与实现分离时，需要标注于声明上）

     ![image-20200410133228612](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410133228612.png)

  2. 修饰代码块

     ![image-20200410133036868](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410133036868.png)

### 默认参数

- 用法

  1. void func(int a, int b=10)

     必须放在参数列表最后

     必须放在声明中

### 重复引用问题

- 重复引用头文件或文件间的循环引用

- 解决方法：

  > 1. #ifndef  #define  #endif (规范宏命名"__文件名")
  >
  > 2. #pargma once (需要编译器支持，老编译器不可用)

### 栈空间默认值

- 默认填充0xCCCCCCCC

  > 原因：
  >
  > ​		汇编指令CC ==> 对应int 3指令，代表中断，防止执行到该部分数据时发生不可预料的严重错误。

### 析构函数

-  通过malloc分配的对象free的时候不会调用析构函数 

-  对象内部申请的堆空间，由对象内部回收 

  ![image-20200410195717236](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410195717236.png)

- 虚析构函数

  ​		如果存在父类指针指向子类对象的情况，应该将析构函数声明为虚函数（虚析构函数），这样， 在delete父类指针时，才会调用子类的析构函数，保证析构的完整性。

### 命名空间

- 默认命名空间

  ![image-20200410195932380](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410195932380.png)

### 继承

- 内存布局：父类成员在前
- 子类调用父类成员函数：父类名::函数名(...)
- 多继承：会对每个有虚函数的父类产生一张虚表，成员变量在内存中的顺序由继承顺序决定
- 菱形继承：通过虚继承解决

### 初始化列表

- 只能写在函数实现中

- 是调用其它构造函数的方法

  ![image-20200410200936871](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410200936871.png)

### 虚函数

- 原理：虚表(存放实际调用的函数地址)，通过this绑定实际对象

### 静态(static)

- 静态成员变量必须在类外初始化，并且初始化不带static
- 静态成员函数声明和实现分离时，实现不能带static

### 隐式构造

![image-20200410202755506](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410202755506.png)

### 模板

- 模板使用

  >  template\<typename T, ...\>
  >
  > -  模板没有被使用时，是不会被实例化出来的 
  > -  模板的声明和实现如果分离到.h和.cpp中，会导致链接错误 
  > -  一般将模板的声明和实现统一放到一个.hpp文件中 

### 类型转换

 使用格式：xx_cast\<type\>(expression) 

- static_cast

  ![image-20200410203950190](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410203950190.png)

- dynamic_cast

  ![image-20200410203936313](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410203936313.png)

- reinterpret_cast

  ![image-20200410204006204](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410204006204.png)

- const_cast 

  ![image-20200410203857704](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410203857704.png)

### Lambda表达式

 __[capture list] (params list) mutable exception-> return type { function body }__  

![image-20200410204239802](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410204239802.png)

- 外部变量捕获

  ![image-20200410204347934](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410204347934.png)

### 异常

- 拦截所有类型

  由于C++没有类似Java中的Object基类，所以无法捕获Exception，而要用catch(...)

  - 标准异常

  ![image-20200410204716957](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410204716957.png)

### 智能指针

- auto_ptr

- shared_ptr

  > 多个指针指向同一对象，到最后一个shared_ptr释放时对象才会释放
  >
  > - 循环引用问题，导致两个对象均存在引用，所以无法正常释放
  >
  >   ![image-20200410205101284](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410205101284.png)
  >
  >   - 解决方法：weak_ptr

- unique_ptr

  > 确保只有一个指针指向对象
  >
  > 可以使用std::move函数转移所有权
  >
  > ![image-20200410205249842](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200410205249842.png)

dynamic_cast

reinterpret_cast

const_cast 