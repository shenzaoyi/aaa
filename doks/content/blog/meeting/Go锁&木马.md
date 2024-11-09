## 锁[[Go]]
GPM模型


## 锁
1. 互斥锁： 阻塞goroutine
2. 自旋锁： 循环访问，占用CPU资源
3. 信号量
	1. FIFO，并不完美，新来的goroutine明明可以直接运行，却需要和已经挂起的(上下文有开销)竞争
	2. 直接给到新来的goroutine
	3. 引入一个标识，防止惊群效应，减少不必要的竞争
go汇编
为什么要-1
效率的比较？运行1000次，测试cpu占用率这些参数
并发起源于操作系统
channel is better
乐观锁？
### stop the world
go源码展示
go版本展示

### trace包和性能比较
### Mutex & channel
## 木马
更高级的自保：如何不被杀毒软件扫描的到
删除本体

## Reference
[Go: How to Reduce Lock Contention with the Atomic Package](https://medium.com/a-journey-with-go/go-how-to-reduce-lock-contention-with-the-atomic-package-ba3b2664b549)
> A data race can occur when two or more goroutines access the same memory location concurrently, and at least one of them is writing. While the maps have a native mechanism to protect against data races, a simple structure does not have any, making it vulnerable to data races.

1. why map?