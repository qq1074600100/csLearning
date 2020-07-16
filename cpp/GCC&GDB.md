# GCC & GDB

### GCC

> - -g/-ggdb :调试
> - -On：youhuajibie
> - -o filename
> - -Wall
> - -Werror
> - -I：include路径
> - -L：lib路径
> - -E：生成*.i
> - -S：生成*.s
> - -C：生成*.o

### gdb

![image-20200528221248912](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200528221248912.png)

![image-20200528222412463](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200528222412463.png)

- print \<expr\>：展示当前值
  - print x=8：修改x的值为8
- display \<expr\>：设置自动显示
  - info display：查看当前自动显示
  - undisplay：删除自动显示
  - enable/unenable：激活自动显示
- disassemble func：反汇编
- return [expr]：指定expr为返回值

![image-20200528224007262](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200528224007262.png)![image-20200528224821634](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200528224821634.png)![image-20200528224853101](C:\Users\10746\AppData\Roaming\Typora\typora-user-images\image-20200528224853101.png)