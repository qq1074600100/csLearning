# C++  STL

### STL六大组件

1. 容器***
2. 算法***
3. 迭代器***
4. 仿函数 **（重载了括号运算符的对象）
5. 适配器
6. 空间配置管理

### 遍历方式

1. 语法
   - for
   - while/do-while
   - 增强for
2. 迭代器
3. for_each(begin, end, func)

### string

​	__使用时需要#include\<string\>__

1. 构造方式:

   - string()

     string(const string *s)

   - string(const string &str)

   - string(int n, char c)

2. 赋值方式:

   - operator=
   - assign()

   **返回值均为引用，可以继续操作**

3. 拼接:

   - operator+=
   - append()

   **返回值均为引用，可以继续操作**

4. 查找和替换

   - 查找：返回下标，不存在返回-1

     - find()
     - rfind()：从右往左查找

   - 替换

     replace()

5. 字符读写

   - operator[]
   - str.at(int n)

6. 字串

   - string substr(int pos, int n)

### vector

​	__使用时需要#include\<vector\>__

1. 构造方式:

   - vector<>()
   - vector<>(iter begin, iter end)
   - vector\<T\>(int n, T elem)
   - vector<>(const vector &vec)

2. 容量和大小

   - empty()

   - capacity()：容量

   - size()：大小

   - resize()：改变大小，以默认值(0)填充

     resize(int num)：改变大小，以指定值填充

3. 插入和删除

   - push_back(T elem)

   - pop_back()

   - insert(iter pos, T elem)

     insert(iter pos, int n, T elem)

   - erase(iter pos)

     erase(iter begin, iter end)

   - clear()：清空

4. 容器元素互换

   - vec1.vector(vec2)

   - 用途：

     > 收缩vector容量，erase/resize只改变size，不能缩减capacity，造成空间浪费
     >
     > vector<T>(v).swap(v)：等价于用v初始化一个匿名对象，其capacity合理，交换后，匿名对象被销毁

5. 预留空间

   - reserve(int len)

     已知数据长度时，提前预留空间，以防止多次动态扩展带来的复制开销

### deque

- 工作原理：

  两端进出
  
  deque内部有一个中控器，维护几个缓冲区指针，缓冲区实际存放数据，保持头尾插入均不需要移动元素。但因此访问速度较vector慢。

- API类似vector，无capacity（有size）

### stack

- 一端进出

- 不允许遍历，因为stack只允许访问栈顶元素

### queue（队列）

- 一端进一端出
- 不允许遍历，只允许访问两端

### list

​	双向循环链表，双向迭代器（不是随机迭代器）

- 插入删除快速，扩展空间容易

- 遍历速度慢，占用空间较大

- API类似

- reverse()：反转

  sort()：排序（由于不支持随机迭代器，所以不能用标准sort算法，用对象的成员方法sort）

### set/multiset

​	__需要#include\<set\>__

- 底层用**二叉树**实现，**自动排序**

- set不允许重复元素，而multiset允许

- 查找和统计

  - find(key)：找到返回迭代器，否则返回end()迭代器
  - count(key)：统计个数

- 插入

  - set::insert()：返回pair\<iter, bool\>，bool值标志插入是否成功
  - multiset::insert()：返回iter，不做插入检查

- 内置类型改变排序规则（仿函数）

  > 1. 创建仿函数对象，重载()操作符，指定排序规则
  > 2. 初始化set时指定比较器

- 自定义类型指定排序规则（必须指定排序规则）

  - 仿函数，同上
  - 重载>, <, ==等运算符

### map/multimap

- 键值对，默认排序（可以自定义排序规则）
- API与set类似

### pair（对组）

- 创建

  - pair< , >()
  - make_pair()

- 访问

  first/second

### Algorithm

​	__需要#include\<algorithm\>__

- 排序

  - sort(iter begin, iter end [, 比较器对象/函数])：默认从小到大

  - random_shuffle(iter begin, iter end)：洗牌，打乱顺序

  - merge(iter begin1, iter end1, iter begin2, iter end2, iter dest)：合并两容器

    > 两容器必须有序且排序规则一致，合并完依然有序
    >
    > 目标容器需要提前分配空间

  - reverse(iter begin, iter end)：反转

- 查找

  ​	**自定义类型需要重载 ”==“ 运算符**

  - find(iter begin, iter end, T elem)
  - find_if(iter begin, iter end, 一元谓词)
  - adjacent_find(iter begin, iter end)：查找相邻重复元素
  - binary_search(iter begin, iter end, T elem)：二分查找
  - count(iter begin, iter end, T elem)：统计元素个数
  - count_if(iter begin, iter end, 一元谓词)：条件统计

- 遍历

  - for_each(iter begin, iter end, _func)

  - transform(iter sourceBegin, iter sourceEnd, iter targetBegin, _func)

    > 搬运到另一个容器，目标容器需要提前分配空间

- 拷贝和替换

  - copy(iter begin1, iter end1, iter begin2)
  - replace(iter begin, iter end, oldValue, newValue)
  - replace_if(iter begin, iter end, _func, newValue)
  - swap(collections c1, collections c2)

- 生成算法

  **需要#include\<numeric\>**

  - acumulate(iter begin, iter end, value)：累加，value为开始时的累加值
  - fill(iter begin, iter end, value)：填充，value为填充值

- 集合算法

  - set_intersection(iter begin1, iter end1, iter begin2, iter end2, iter dest)：交集
  - set_union(iter begin1, iter end1, iter begin2, iter end2, iter dest)：并集
  - set_differenceiter begin1, iter end1, iter begin2, iter end2, iter dest)：差集

##### C++内置仿函数

​	__需要#include\<functional\>__

1. 算术仿函数

   >plus\<T\>()    minus\<T\>()   negate\<T\>()......

2. 关系仿函数

   > 用于实现关系对比
   >
   > greater\<T\>()     less\<T\>()  .......

3. 逻辑仿函数

   > 实现逻辑运算
   >
   > logical_and\<T\>()    logical_or\<T\>()   logical_not\<T\>() .......

