---
title: cheat engine
categories:
  - blog
contributors:
  - shenzaoyi
date: 2024-09-18
draft: false
---
## Tutorial
1. 已知初始值的查找
2. 未知初始值的查找
3. 查找 float & double 型数据
4. 程序中变量位置动态变化的查找
5. tepm
6. 指针（未完成）
7. to be ...
## 原理
1. 查看内存块信息
2. 跨进程读取
3. 字符串模式匹配算法定位


## 源码解读
## 暴力搜索
```c
DWORD AOBScan(HANDLE hProcess, const char* pattern, const char* mask, uint64_t start, uint64_t end, int inc, int protection,uint64_t * match_addr) {

	RegionInfo rinfo;
	uint64_t tmp = start;
	uint64_t tmp2 = tmp;

	char* MemoryBuff = (char*)malloc(4096);
	int patternLength = (int)strlen(mask);

	int result_count = 0;

	while (tmp < end) {
		VirtualQueryEx(hProcess, (void*)tmp, &rinfo, NULL);
		if (rinfo.size == 0) {
			return -1;
		}
		if((rinfo.protection & protection) != 0)
		{
			tmp2 = tmp;
			while (tmp2 < tmp + rinfo.size)
			{
				if (!ReadProcessMemory(hProcess, (void*)tmp2, MemoryBuff, 4096)) {
					break;
				}

				for (int i = 0; i < 4096; i += inc)
				{ 
					for (int k = 0; k < patternLength; k++)
					{

						if (!(mask[k] == '?' || pattern[k] == (MemoryBuff[k])))
						{
							goto label;

						}
					}
					match_addr[result_count] = tmp2;
					result_count++;
					if (result_count >= MAX_HIT_COUNT)return result_count;
					
				label:
					tmp2 += inc; MemoryBuff += inc;
				}
				MemoryBuff -= 4096;
			}
		}
		tmp += rinfo.size;
	}

return result_count;
}
```
### CE驱动机制 DBVM
DBVM驱动允许 Cheat Engine 在 Windows 操作系统中访问和操作内核级别的内存和系统结构


### [VEH](https://en.wikipedia.org/wiki/Microsoft-specific_exception_handling_mechanisms#Vectored_Exception_Handling)

### [x64dbg](https://help.x64dbg.com/en/latest/)
仅仅是一个GUI
### [TitanEngine](https://github.com/x64dbg/TitanEngine)
核心

## 内存扫描器


## 进程
\_EProcess
Thread
Handles
Memory
	Modules

Initialize address space
- Map KUSER_SHARED_DATA : like time...
- Map the executable
- Map ntdll.dll : similar to ld in linux
- Allocate PEB 
Portable Executable (PE) --- ELF
- Sections
- Imports
- Exports
- Relocations
- AddressOfEntryPoint
- Subsytem
- ......
DLLMain/ TLS Callbacks
- Notification of thread of thread start/end
- Used for initailization
- DLLS vs Executables
- Loader lock


## Reference
[模仿Cheat Engine内存搜索——（Sunday算法）](https://blog.haiya360.com/archives/1588.html)
[内存修改器原理揭秘（上）](https://www.bilibili.com/video/BV1ud4y1B7rW/?share_source=copy_web&vd_source=a113b92ed718cca34d96624b08d107d3)
[csdn](https://download.csdn.net/download/lyshark_csdn/87893347)
[代码](https://www.lyshark.com/post/7ab1f162.html)
[ms](https://learn.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-readprocessmemory)
[进程基质](https://www.cnblogs.com/Leo_wl/p/3147381.html)
[32 & 64](https://www.cnblogs.com/zjuhaohaoxuexi/p/16210800.html)
```
 git log --since="2009-010-24" --until="2009-10-25"
```