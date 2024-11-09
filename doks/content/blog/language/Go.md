---
title: Go
categories:
  - language
contributors:
  - shenzaoyi
date: 2024-08-29
draft: false
---
## 编译流程
### Go的自举
[[Go 1.3+ Compiler Overhaul 1.pdf]]
hint: 如果需要直接展示pdf,前面加上!，和图片非常像。

## go path
[如何正确处理 Go 项目中关于文件路径的问题](https://www.poloxue.com/posts/2024-02-23-get-filepath-in-golang/)
## GPM模型
![image.png](https://raw.githubusercontent.com/shenzaoyi/phot0_bed/main/img_windows20240927083112.png)
- N:M的多对多
![image.png](https://raw.githubusercontent.com/shenzaoyi/phot0_bed/main/img_windows20240927083808.png)
- 每个M都会维护一个P, 用来调度G0 
**  抽象的协程有自己的堆栈？如何虚拟化实现的 **
如何观察：

## [go内存模型](https://liupzmin.com/2022/04/26/theory/stack-insight-03/)
## [Go汇编](https://go.cyub.vip/go-assembly/)
[Go汇编](https://github.com/go-internals-cn/go-internals/blob/master/chapter1_assembly_primer/README.md)
Go 编译器会输出一种抽象可移植的汇编代码，这种汇编并不对应某种真实的硬件架构。Go 的汇编器会使用这种伪汇编，再为目标硬件生成具体的机器指令
## 并发
并发执行时，多进程，多线程，多协程为了同步引发出了一系列问题，进程协作，死锁，临界区，非确定性。
### 锁
#### 自旋锁 & 阻塞锁 & 信号量
原子操作 - stop the world
1. 自旋锁 CPU占用率高
2. 阻塞锁 有上下文切换开销
3. 信号量  

可以看到，我们的goroutine是被封装成了sudog的结构，然后根据addr（也就是mutex中的sema变量）添加到了一个全局的平衡二叉树中，然后调用gopark方法阻塞，gopark方法是比较重要的方法，gopark底层会调用dropg方法，该方法会解除g与m的关联（可以参考golang的GPM模型，gopark的实现比较复杂，感兴趣的可以自行查询），m（machine）是操作系统的线程，解除关联后，g就没有运行的线程，我们goroutine的表现就是阻塞了。


## Gin

## [go by example](https://gobyexample-cn.github.io/)
### switch
```go
a := 1
// 不带表达式的switch
switch {
	case a < 2:
		fmt.Print("smaller") 
	default:
		fmt.Print("others")
}
```
### [slice](https://go.dev/blog/slices-intro)
