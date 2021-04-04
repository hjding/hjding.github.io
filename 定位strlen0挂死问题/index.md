# 定位strlen(0)挂死问题


## 背景

在自测OLT应支持通过SNMP来实现对user account的创建、删除、修改时，下发修改用户角色，使能密码123456，导致agent挂死问题

![](D:\Hugo\my_website\content\images\1_定位strlen(0)挂死问题.png)

## 分析现象

查看调用栈发现任务是挂载strlen这里，常见的问题就是strlen参数为0等非法字符串指针，是被libfhsp.so的um_check_pass_legal的+0x44汇编代码调用导致，注意这里的+44是16进制

排查过程：
1. 挂死的时候会记录调用栈，打印一下

  ```
  Admin(diagnose)# enter bep
  username:diag
  password:
  FiberHome>enable
  FiberHome#show haltsinfo district 0
  ```

  

2. 进入linux，gdb运行对应的.so，反汇编查看代码

  ```
  Admin(diagnose)# dangerous_shell
  fsl61280 login: root
  Password: root
  [root@/mnt/work/hsud/bin]# gdb ./mnt/work/hsud/bin/libfhsp.so
  disassemble um_check_pass_legal
  ```

3. 寄存器信息r0~r3是io参数，0x44对应的是第+68， 从r0去加载数据， 但是寄存器r0是0，问题搞定~

## 总结

1. 在定位问题时，学会使用汇编和反汇编，常常事半功倍，高效

2. 在coding时候，像strlen这些，应注意加判空保护
