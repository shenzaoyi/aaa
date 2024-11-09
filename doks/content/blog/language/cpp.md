## [input&output with files](https://cplusplus.com/doc/tutorial/files/)
#### << 和 >>
```cpp
<< ： 流插入运算符
>> :  流提取运算符
```
#### open & close a file
```cpp
// open(filename, mode);
// mode can be combined using |, for example
ofstream myfile;
myfile.open("example.txt",ios::in|ios::out);
// or constructor
ofstream myfile("example", ios::in|ios::binary);
// to check
if (myfile.is_open()) {} // return true is opened
// to close
myfile.close();

```
filemode: 
![image.png](https://raw.githubusercontent.com/shenzaoyi/phot0_bed/main/img_windows20241022210249.png)
#### Text files
使用">>" 和 "<<" 读取文本文件
```cpp
int main() {
    fstream file("a.txt",ios::in|ios::out);
    if (!file.is_open()) {
        cout<<"Open file error"<<endl;
    }
    // 使用<<， 将字符串插入流中
    file << "hello \n";
    file << "nice to meet you \n";
    string buffer = " ";
    // 设置文件当前指针指向开头，因为前面的操作让指针已经到末尾了
    file.seekg(ios::beg);
    // 流提取，从流中提取字符，每次遇到空格就返回一个file流对象
    // 但是这个file流对象是不可被赋值的
	// 如：basic_istream new_file = file>>buffer;是不允许的
    while(file >> buffer) {
        cout<<buffer<<endl;
    }
    // 但是更常用的做法是： getline函数读取
    while (getline(file,buffer)) {
        cout<<buffer<<endl;
    }
    file.close();
    return 0;
}
```
#### check the state
The following member functions exist to check for specific states of a stream (all of them return a `bool` value):  
`bad()`
Returns `true` if a reading or writing operation fails. For example, in the case that we try to write to a file that is not open for writing or if the device where we try to write has no space left.
`fail()`
Returns `true` in the same cases as `bad()`, but also in the case that a format error happens, like when an alphabetical character is extracted when we are trying to read an integer number.
`eof()`
Returns `true` if a file open for reading has reached the end.
`good()`
It is the most generic state flag: it returns `false` in the same cases in which calling any of the previous functions would return `true`. Note that `good` and `bad` are not exact opposites (`good` checks more state flags at once).
The member function `clear()` can be used to reset the state flags.
#### get & put stream position
每个stream内部都维持了一个position，用来保存当前的location(或下一次读取的起始地址)
istream : 维持一个get position
ostream: put position
fstream : both
1. 无参函数tellg & tellp： 返回当前的position，tellg -- istream tellp -- ostream
2. seekp & seekg
	1. seekp(position) & seekg(position): 设置position值，返回值为**std::streampos**类型
	2. seekp(offset, direction) & seekg(offset, direction) : offset 是偏移，可以为负值，direction为基地址，定义如下
3. ![image.png](https://raw.githubusercontent.com/shenzaoyi/phot0_bed/main/img_windows20241022215401.png)
```cpp
int main() {
    fstream file("a.txt",ios::in|ios::out);
    if (!file.is_open()) {
        cout<<"Open file error"<<endl;
    }
    streampos start = file.tellg();
    streamoff off = 0;
    file.seekg(off,ios::end);
    streampos end = file.tellg();
    streampos size = end - start;
    cout<<"size is : "<<size<<endl;
    return 0;
}
```
![image.png](https://raw.githubusercontent.com/shenzaoyi/phot0_bed/main/img_windows20241022220146.png)
#### binary files
对于没有格式需求的二进制文件的读取，不必使用流提取和插入运算符以及getline函数，新的选择是： write& read
```cpp
write ( memory_block, size );  
read ( memory_block, size ); // memory_block : char* 
fstream file("temp0",ios::in|ios::out|ios::binary);
    char* s = new char[6];
    strncpy(s,"hello",6);
    file.write(s,6);
    file.seekp(0,ios::end);
    streampos size = file.tellp();
    file.seekp(0,ios::beg);
    char* buffer = new char[size];
    file.read(buffer,size);
    cout<<buffer<<endl;
    file.close();
    delete[] buffer;
    return 0;
``` 
#### 缓冲区和同步
见参考