# 计算机基础
### 进程、线程、协程对比
1. **进程（Process）**<font style="color:rgb(55, 65, 81);">：</font>
    - **定义：**<font style="color:rgb(55, 65, 81);"> 进程是计算机中运行的程序的实例。每个进程都有自己的地址空间、系统资源和状态。</font>
    - **技术原理：**<font style="color:rgb(55, 65, 81);"> 进程之间相互独立，通过操作系统的调度器进行管理。进程间通信的开销较大，因为它们通常需要通过进程间通信的机制来交换数据。</font>
    - **区别：**<font style="color:rgb(55, 65, 81);"> 进程之间是独立的，一个进程的崩溃不会影响其他进程。</font>
2. **线程（Thread）**<font style="color:rgb(55, 65, 81);">：</font>
    - **定义：**<font style="color:rgb(55, 65, 81);"> 线程是进程内的执行单元，共享同一进程的地址空间和系统资源，但有独立的执行流。</font>
    - **技术原理：**<font style="color:rgb(55, 65, 81);"> 线程由操作系统调度，共享进程的资源，线程之间的切换开销相对较小。多线程可以提高程序的并发性。</font>
    - **区别：**<font style="color:rgb(55, 65, 81);"> 线程共享相同的地址空间，因此线程之间的通信和数据共享更容易，但同时也更容易出现竞争条件和死锁。</font>
3. **协程（Coroutine）**<font style="color:rgb(55, 65, 81);">：</font>
    - **定义：**<font style="color:rgb(55, 65, 81);"> 协程是一种用户态的轻量级线程，可以在同一线程中实现多任务并发。协程有自己的执行流程，但在执行过程中可以主动让出控制权。</font>
    - **技术原理：**<font style="color:rgb(55, 65, 81);"> 协程是由程序员显式控制的，不同于由操作系统调度的线程。协程可以通过 yield 和 resume 操作进行状态切换，实现协作式多任务。</font>
    - **区别：**<font style="color:rgb(55, 65, 81);"> 协程通常比线程更轻量，开销更小。协程的切换由程序员控制，更适用于某些特定场景，如异步编程。</font>

### 协程底层如何实现
##### Python Coroutine:
<font style="color:rgb(55, 65, 81);">Python 使用生成器（generator）来实现协程。在 Python 中，协程通常通过 </font>**async def**<font style="color:rgb(55, 65, 81);"> 定义，使用 </font>**await**<font style="color:rgb(55, 65, 81);"> 来进行协程的挂起和恢复。</font>

<font style="color:rgb(55, 65, 81);">底层实现主要涉及以下两个概念：</font>

1. **生成器（Generator）：**<font style="color:rgb(55, 65, 81);"> Python 中的生成器是一种特殊的迭代器，通过 </font>**yield**<font style="color:rgb(55, 65, 81);"> 关键字实现挂起和恢复执行。生成器函数被调用时，不会立即执行，而是返回一个生成器对象。</font>
2. **事件循环（Event Loop）：**<font style="color:rgb(55, 65, 81);"> Python 使用事件循环机制来调度协程的执行。事件循环负责协程的调度和管理，通过 </font>**asyncio**<font style="color:rgb(55, 65, 81);"> 库提供支持。</font>

##### Go Goroutine:
<font style="color:rgb(55, 65, 81);">Go 使用轻量级线程，称为 goroutine，来实现并发。Goroutine 是 Go 运行时（runtime）管理的，与操作系统线程无直接映射关系，一个操作系统线程可以同时运行多个 goroutine。</font>

<font style="color:rgb(55, 65, 81);">底层实现涉及以下几个方面：</font>

1. **Go Runtime：**<font style="color:rgb(55, 65, 81);"> Go 运行时系统负责管理和调度 goroutine。它会将多个 goroutine 映射到少量的操作系统线程上。</font>
2. **信道（Channel）：**<font style="color:rgb(55, 65, 81);"> Goroutine 之间通过信道进行通信和数据传递。信道是 Go 提供的一种同步原语，用于避免数据竞争和协调不同 goroutine 的执行。</font>

##### Python 和 Go 协程对比：
1. **调度机制：**
    - <font style="color:rgb(55, 65, 81);">Python 协程的调度由事件循环管理，使用 </font>**await**<font style="color:rgb(55, 65, 81);"> 和 </font>**asyncio**<font style="color:rgb(55, 65, 81);"> 实现协作式调度。</font>
    - <font style="color:rgb(55, 65, 81);">Go Goroutine 由 Go 运行时系统进行调度，通过信道进行通信。</font>
2. **语法和关键字：**
    - <font style="color:rgb(55, 65, 81);">Python 使用 </font>**async def**<font style="color:rgb(55, 65, 81);">、</font>**await**<font style="color:rgb(55, 65, 81);"> 等关键字来定义和控制协程。</font>
    - <font style="color:rgb(55, 65, 81);">Go 使用 </font>**go**<font style="color:rgb(55, 65, 81);"> 关键字启动 goroutine，并通过信道进行通信。</font>
3. **并发模型：**
    - <font style="color:rgb(55, 65, 81);">Python 协程通常通过单线程的事件循环实现并发。</font>
    - <font style="color:rgb(55, 65, 81);">Go Goroutine 则利用多个操作系统线程来实现并发。</font>
4. **数据传递：**
    - <font style="color:rgb(55, 65, 81);">Python 协程通常使用 </font>**await**<font style="color:rgb(55, 65, 81);"> 表达式进行异步的数据传递。</font>
    - <font style="color:rgb(55, 65, 81);">Go Goroutine 通过信道进行数据传递，确保数据安全的同时实现协程间的同步。</font>

##### <font style="color:rgb(55, 65, 81);">go 协程</font>
```go
package main

import (
	"fmt"
	"time"
)

func printNumbers() {
	for i := 1; i <= 5; i++ {
		time.Sleep(100 * time.Millisecond) // 模拟一些计算或耗时操作
		fmt.Printf("%d ", i)
	}
}

func printLetters() {
	for char := 'a'; char <= 'e'; char++ {
		time.Sleep(100 * time.Millisecond) // 模拟一些计算或耗时操作
		fmt.Printf("%c ", char)
	}
}

func main() {
	go printNumbers()
	go printLetters()

	// 等待一段时间，确保 goroutine 有足够时间执行
	time.Sleep(1 * time.Second)

	fmt.Println("Main function exits.")
}

```

##### Python coroutine
```python
import asyncio

async def print_numbers():
    for i in range(1, 6):
        await asyncio.sleep(0.1)  # 模拟一些计算或耗时操作
        print(i, end=' ')

async def print_letters():
    for char in 'abcde':
        await asyncio.sleep(0.1)  # 模拟一些计算或耗时操作
        print(char, end=' ')

async def main():
    task1 = asyncio.create_task(print_numbers())
    task2 = asyncio.create_task(print_letters())

    # 等待任务完成
    await asyncio.gather(task1, task2)

    print("Main function exits.")

# Python 3.7 之前的版本需要使用以下语句运行协程
# asyncio.run(main())

# Python 3.7 及以后版本可以直接运行协程
asyncio.run(main())

```

### 线程可以无限创建吗？
~~我说不可以，受制于内存，多个线程共享内存，面试官说既然多个线程共享内存，为何不可以？我。。~~

线程的创建数量是有限的，受限于系统资源和操作系统的限制。每个线程都需要分配一些系统资源，包括内存、线程栈、寄存器等，因此创建过多的线程会导致系统资源的耗尽。

影响线程数量的因素包括：

+ 内存： 每个线程都需要分配一定的内存空间，包括线程栈和其他线程控制结构。当线程数量增多时，系统的内存消耗会相应增加。
+ 线程栈大小： 每个线程都有自己的栈空间，用于存储局部变量、函数调用信息等。如果线程栈的大小设置过大，会增加每个线程的内存消耗，从而限制线程的数量。
+ 系统调度器： 操作系统的调度器需要维护和调度每个线程的状态，当线程数量非常庞大时，调度器的负担会增加，可能影响系统的性能。
+ 硬件资源： 系统的硬件资源，如处理器核心数量，也是限制线程数量的一个因素。过多的线程可能导致竞争条件，降低性能。

虽然理论上线程数量是有限的，但实际上，根据系统的不同，可支持的线程数量也会有所不同。在现代操作系统中，通常会有一些配置参数或限制来控制线程的数量，而开发者也应该在设计应用程序时考虑系统资源的限制，避免创建过多的线程导致性能下降或系统崩溃。

linux操作系统中，以下参数可以对资源进行限制:

1. **ulimit 命令：**
    - **ulimit**<font style="color:rgb(55, 65, 81);"> 命令用于查看和设置 shell 的资源限制。通过 </font>**ulimit -a**<font style="color:rgb(55, 65, 81);"> 命令可以查看当前的资源限制，其中包括线程相关的参数。</font>
    - <font style="color:rgb(55, 65, 81);">例如，</font>**ulimit -u**<font style="color:rgb(55, 65, 81);"> 可以用来设置或显示用户可创建的最大线程数。</font>

 ulimit 参数

```shell
[root@k8s ~]# ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 30811
max locked memory       (kbytes, -l) unlimited
max memory size         (kbytes, -m) unlimited
open files                      (-n) 100001
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes 最大用户线程数    (-u) 30811
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```

2. **/proc 文件系统：**
    - <font style="color:rgb(55, 65, 81);">在 Linux 中，可以通过 </font>**/proc**<font style="color:rgb(55, 65, 81);"> 文件系统中的一些文件查看和修改系统参数。</font>
    - **/proc/sys/kernel/threads-max**<font style="color:rgb(55, 65, 81);"> 文件包含了系统允许的最大线程数量。可以通过修改这个文件来调整系统的线程限制。</font>
3. **/etc/security/limits.conf 文件：**
    - **/etc/security/limits.conf**<font style="color:rgb(55, 65, 81);"> 文件用于配置用户和用户组的资源限制。可以在该文件中设置与线程相关的参数，如 </font>**nproc**<font style="color:rgb(55, 65, 81);">。</font>
4. **pthreads 库参数：**
    - <font style="color:rgb(55, 65, 81);">在使用 pthreads 库创建线程时，可以通过 </font>**pthread_attr_setstacksize**<font style="color:rgb(55, 65, 81);"> 函数设置线程栈的大小，从而影响线程数量的限制。</font>
    - <font style="color:rgb(55, 65, 81);">另外，</font>**pthread_create**<font style="color:rgb(55, 65, 81);"> 函数的返回值可以用来判断线程创建是否成功。</font>
5. **内核参数：**
    - <font style="color:rgb(55, 65, 81);">一些与线程相关的内核参数可以通过 </font>**/proc/sys/kernel/**<font style="color:rgb(55, 65, 81);"> 目录下的文件进行调整。</font>
    - <font style="color:rgb(55, 65, 81);">例如，</font>**/proc/sys/kernel/pid_max**<font style="color:rgb(55, 65, 81);"> 文件指定了最大的 PID（进程/线程标识符）值，从而影响了线程的数量限制。</font>

### 共享内存有了解吗
~~我说 mmap，具体怎么实现的~~

[Linux共享内存](https://www.cnblogs.com/linuxbug/p/4882776.html)

##### 共享内存方式:
+ **mmap 调用：**<font style="color:rgb(0, 0, 0);">mmap()系统调用使得进程之间通过映射同一个普通文件实现共享内存。普通文件被映射到进程地址空间后，进程可以像访问普通内存一样对文件进行访问，不必再调用read()，write（）等操作。</font>
+ **POSIX 共享内存：**
    1. <font style="color:rgb(0, 0, 0);">通过shm_open创建或打开一个POSIX共享内存对象</font>
    2. <font style="color:rgb(0, 0, 0);">调用mmap将它映射到当前进程的地址空间</font>
    3. <font style="color:rgb(0, 0, 0);">和通过内存映射文件进行通信的使用上差别在于，mmap描述符参数获取方式不一样：通过open或shm_open</font>
    4. <font style="color:rgb(0, 0, 0);">POSIX共享内存和POSIX消息队列，有名信号量一样都是具有</font><font style="color:rgb(255, 0, 0);">随内核持续性的特点</font><font style="color:rgb(0, 0, 0);">。在Linux 2.6.x中，</font><font style="color:rgb(255, 0, 0);">对于POSIX信号量和共享内存的名字会在/dev/shm下建立对应的路径名。</font>
+ **System V 共享内存：**<font style="color:rgb(0, 0, 0);">系统调用 mmap()通过映射一个普通文件实现共享内存。</font>**<font style="color:rgb(0, 0, 0);">System V 则是通过映射特殊文件系统 shm 中的文件实现进程间的共享内存通信</font>**<font style="color:rgb(0, 0, 0);">。也就是说，每个共享内存区域对应特殊文件系统shm中的一个文件（这是通过shmid_kernel结构联系起来的）。进程间需要共享的数据被放在一个叫做IPC共享内存区域的地方，所有需要访问该共享区域的进程都要把该共享区域映射到本进程的地址空间中去。System V共享内存通过shmget获得或创建一个IPC共享内存区域，并返回相应的标识符。内核在保证shmget获得或创建一个共享内存区，初始化该共享内存区相应的shmid_kernel结构注同时，还将在特殊文件系统shm中，创建并打开一个同名文件，并在内存中建立起该文件的相应dentry及inode结构，新打开的文件不属于任何一个进程（任何进程都可以访问该共享内存区）。所有这一切都是系统调用shmget完成的。</font>

<font style="color:rgb(0, 0, 0);">共享内存是最快的IPC形式，在开发中，我们一定要充分利用好共享内存的特性，取得事半功倍的效果。</font>

| **<font style="color:rgb(0, 0, 0);">类型</font>** | **<font style="color:rgb(0, 0, 0);">原理</font>** | **<font style="color:rgb(0, 0, 0);">易失性</font>** |
| :--- | :--- | :--- |
| <font style="color:rgb(0, 0, 0);">mmap</font> | <font style="color:rgb(0, 0, 0);">利用文件</font><font style="color:rgb(0, 0, 0);">(open)</font><font style="color:rgb(0, 0, 0);">映射共享内存区域</font> | <font style="color:rgb(0, 0, 0);">会保存在磁盘上，不会丢失</font> |
| <font style="color:rgb(0, 0, 0);">Posix shared memory</font> | <font style="color:rgb(0, 0, 0);">利用</font><font style="color:rgb(0, 0, 0);">/dev/shm</font><font style="color:rgb(0, 0, 0);">文件系统</font><font style="color:rgb(0, 0, 0);">(mmap)</font><font style="color:rgb(0, 0, 0);">映射共享内存区域</font> | <font style="color:rgb(0, 0, 0);">随内核持续，内核自举后会丢失</font> |
| <font style="color:rgb(0, 0, 0);">SystemV shared memory</font> | <font style="color:rgb(0, 0, 0);">利用/dev/shm文件系统(shmat)</font><font style="color:rgb(0, 0, 0);">映射共享内存区域</font> | <font style="color:rgb(0, 0, 0);">随内核持续，内核自举后会丢失</font> |


##### 共享内存方式区别:
1. **mmap：**
    - **实现方式：****mmap** 是一种将文件或匿名内存映射到进程地址空间的方式。可以通过打开一个文件或使用 **MAP_ANONYMOUS** 标志来创建共享内存区域。
    - **可移植性：mmap** 是 POSIX 标准的一部分，具有较好的可移植性，可以在各种 UNIX-like 系统上使用。
    - **文件关联性：** 在文件关联的情况下，**mmap** 可以通过读写文件来进行数据的传递。而在匿名内存映射中，没有文件关联，只是创建了一块共享的匿名内存。
2. **POSIX 共享内存：**
    - **实现方式：** POSIX 共享内存通过 **shm_open** 和 **mmap** 实现，它允许创建一个具有名字的共享内存区域，通过 **mmap** 映射到进程地址空间。
    - **可移植性：** POSIX 共享内存是基于 POSIX 标准的，因此在符合 POSIX 的系统上具有良好的可移植性。
    - **文件关联性：** 与 **mmap** 类似，POSIX 共享内存也可以关联到一个具有名字的文件。
3. **System V 共享内存：**
    - **实现方式：** System V 共享内存是通过 **shmget**、**shmat** 等 System V IPC 函数实现的。它使用键（key）来唯一标识共享内存区域。
    - **可移植性：** System V 共享内存不如 **mmap** 和 POSIX 共享内存具有良好的可移植性，因为 System V IPC 不是 POSIX 标准的一部分，不同系统的实现可能有差异。
    - **文件关联性：** System V 共享内存通常不与文件关联，而是通过键值来进行标识。

总的来说，这三种方式都允许多个进程之间共享一块内存区域，但它们的实现方式、接口和可移植性有所不同。选择使用哪种方式通常取决于具体的应用需求和系统环境。 POSIX 共享内存相对于 System V 共享内存而言，更为现代且易用，而 **mmap** 适用于需要与文件关联的场景。

##### mmap
<font style="color:rgb(31, 35, 40);">mmap的作用，在应用这一层，是让你把文件的某一段，当作内存一样来访问。将文件映射到物理内存，将进程虚拟空间映射到那块内存。这样，进程不仅能像访问内存一样读写文件，多个进程映射同一文件，还能保证虚拟空间映射到同一块物理内存，达到内存共享的作用。</font>

**<font style="color:rgb(31, 35, 40);">共享内存访问同步方式: </font>****<font style="color:rgb(36, 41, 46);">斥锁、条件变量、读写锁、纪录锁、信号灯</font>**

<font style="color:rgb(31, 35, 40);">mmap就是将文件映射到内存上，进程直接对内存进行读写，然后就会反映到磁盘上</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706239686546-50fc4e6f-0cc0-449e-a75a-2835c767f39b.png)

+ <font style="color:rgb(31, 35, 40);">虚拟空间获取到一段连续的地址</font>
+ <font style="color:rgb(31, 35, 40);">在没有读写的时候，这个地址指向不存在的地方（所以，上图中起始地址和终止地址是还没分配给进程的）</font>
+ <font style="color:rgb(31, 35, 40);">好了，根据偏移量，进程要读文件数据了，数据占在两个页当中（物理内存着色部分）</font>
+ <font style="color:rgb(31, 35, 40);">这时，进程开始使用内存了，所以OS给这两个页分配了内存（即缺页异常）（其余部分还是没有分配）</font>
+ <font style="color:rgb(31, 35, 40);">然后刚分配的页内是空的，所以再将相同偏移量的文件数据拷贝到物理内存对应页上。</font>

###### 内存映射的实现过程：
1. **调用 ****mmap**** 函数：**<font style="color:rgb(55, 65, 81);"> 应用程序通过调用 </font>**mmap**<font style="color:rgb(55, 65, 81);"> 函数来请求内存映射。函数的参数包括文件描述符、映射的长度、映射的起始地址等。如果起始地址设置为 </font>**NULL**<font style="color:rgb(55, 65, 81);">，操作系统会自动选择一个合适的地址。</font>

```c

void *mmap(void *addr, size_t length, int prot, int flags, int fd, off_t offset);
```

2. **操作系统分配虚拟内存：**<font style="color:rgb(55, 65, 81);"> 当 </font>**mmap**<font style="color:rgb(55, 65, 81);"> 被调用时，操作系统会分配一段虚拟内存空间，并建立虚拟内存和文件之间的映射关系。映射关系的建立可能涉及到磁盘 I/O 操作，但此时并不会将整个文件全部加载到内存中。</font>
3. **访问映射区域：**<font style="color:rgb(55, 65, 81);"> 应用程序可以像访问普通内存一样，通过指针来访问映射的区域。操作系统会根据需要将文件的内容逐段加载到内存中。</font>
4. **数据修改：**<font style="color:rgb(55, 65, 81);"> 如果应用程序在映射的区域中进行写操作，修改的数据首先被写入进程的内存中。此时，操作系统会将修改的数据标记为脏页（Dirty Page）。</font>
5. **同步到文件：**<font style="color:rgb(55, 65, 81);"> 操作系统会定期或在某些条件下将脏页的数据同步回磁盘。这个过程通常称为页面回写（Page Writeback）。具体的同步时机可以由操作系统的页面回写策略决定。</font>

###### 将修改的数据写入磁盘：
1. **写时复制（Copy-on-Write）：**<font style="color:rgb(55, 65, 81);"> 当某个进程修改映射区域的内容时，操作系统并不立即写回文件，而是先将修改的数据复制到进程的私有空间。只有当这个数据被多个进程中的任意一个进程修改时，操作系统才会将这部分数据写回文件。</font>
2. **定期刷新：**<font style="color:rgb(55, 65, 81);"> 操作系统可能会定期检查脏页，并将修改的数据写回文件。这个定期刷新的频率可以由操作系统的策略和配置决定。</font>
3. **手动调用 ****msync****：**<font style="color:rgb(55, 65, 81);"> 应用程序可以通过手动调用 </font>**msync**<font style="color:rgb(55, 65, 81);"> 函数将脏页的数据刷新回磁盘，以确保数据的一致性。</font>

<font style="color:rgb(55, 65, 81);">需要注意的是，</font>**mmap**<font style="color:rgb(55, 65, 81);"> 并不保证文件的实时同步，因此在需要强制同步的情况下，应用程序可能需要显式地调用 </font>**msync**<font style="color:rgb(55, 65, 81);"> 或 </font>**fsync**<font style="color:rgb(55, 65, 81);"> 等函数。此外，对于需要频繁修改的大文件，</font>**mmap**<font style="color:rgb(55, 65, 81);"> 可能并不是最优选择，因为它会导致整个文件或文件的一部分被加载到内存中，占用大量系统资源。</font>

### 协程可以无限创建吗？协程和线程区别？
不能无限创建，每个协程会占用一定内存、CPU资源

受限于:

1. **可用内存：**<font style="color:rgb(55, 65, 81);"> 每个协程都会占用一定的内存资源，包括栈空间等。因此，可用内存的大小限制了协程的数量。</font>
2. **操作系统线程数目：**<font style="color:rgb(55, 65, 81);"> Go 协程是由 Go 运行时系统调度到底层的操作系统线程上执行的。操作系统对于线程数目有一定的限制，当达到这个限制时，无法再创建新的线程和协程。</font>
3. **Go 运行时系统设置：**<font style="color:rgb(55, 65, 81);"> Go 运行时系统会有一些配置参数，例如 </font>**GOMAXPROCS**<font style="color:rgb(55, 65, 81);">，它指定了可以同时执行的最大操作系统线程数。这个设置也会影响到协程的创建数量。</font>
4. **系统资源限制：**<font style="color:rgb(55, 65, 81);"> 操作系统本身可能对于进程或线程的数量有一定的限制，这也会影响协程的创建。</font>
5. <font style="color:rgb(55, 65, 81);"> </font>**上下文切换开销：**<font style="color:rgb(55, 65, 81);"> 协程之间的切换涉及到上下文的保存和恢复，这会产生一定的开销。尽管 Go 协程的切换开销相对较小，但在大量协程存在时，上下文切换仍然是一个需要考虑的因素。</font>

协程和线程区别

1. **调度方式：**
    - **线程：**<font style="color:rgb(55, 65, 81);"> 线程是由操作系统内核调度和管理，也称为内核线程。线程的创建、切换和销毁都由操作系统负责。</font>
    - **协程：**<font style="color:rgb(55, 65, 81);"> 协程是由用户空间的调度器（Coroutine Scheduler）进行管理的，也称为用户线程。协程的创建、切换和销毁由应用程序自身进行控制，不依赖操作系统调度。</font>
2. **并发性：**
    - **线程：**<font style="color:rgb(55, 65, 81);"> 线程在多核系统上可以并行执行，每个线程都可以在不同的处理器上运行。</font>
    - **协程：**<font style="color:rgb(55, 65, 81);"> 协程通常运行在单一线程之中，它们并不会在多个处理器上同时执行。协程通过协作式调度来实现并发，即一个协程执行一段时间后主动让出控制权，切换到其他协程执行。</font>
3. **切换开销：**
    - **线程：**<font style="color:rgb(55, 65, 81);"> 线程的切换是由操作系统内核负责的，因此切换开销相对较高。</font>
    - **协程：**<font style="color:rgb(55, 65, 81);"> 协程的切换是由用户空间的调度器负责的，通常比线程切换的开销小很多。</font>
4. **内存占用：**
    - **线程：**<font style="color:rgb(55, 65, 81);"> 操作系统为每个线程分配独立的内存空间，线程之间不共享栈。</font>
    - **协程：**<font style="color:rgb(55, 65, 81);"> 协程通常共享相同线程的地址空间，它们使用相同的栈。</font>
5. **通信机制：**
    - **线程：**<font style="color:rgb(55, 65, 81);"> 线程之间的通信通常通过共享内存或消息传递进行。</font>
    - **协程：**<font style="color:rgb(55, 65, 81);"> 协程之间通信通常通过直接调用函数或使用特定的通道（Channel）进行。</font>
6. **错误处理：**
    - **线程：**<font style="color:rgb(55, 65, 81);"> 线程的错误处理相对复杂，需要使用锁等机制来确保线程安全。</font>
    - **协程：**<font style="color:rgb(55, 65, 81);"> 协程的错误处理通常更为简单，因为它们运行在单一线程中，不存在多线程竞争的问题。</font>
7. **编程模型：**
    - **线程：**<font style="color:rgb(55, 65, 81);"> 编写多线程程序时，需要考虑线程同步、锁、死锁等并发编程问题。</font>
    - **协程：**<font style="color:rgb(55, 65, 81);"> 编写协程程序时，通常更关注协程之间的协同工作，不需要过多考虑锁和同步的问题。</font>

<font style="color:rgb(55, 65, 81);">协程更轻量、更容易使用，适用于高并发、IO密集型的应用场景。</font>

<font style="color:rgb(55, 65, 81);">线程更适合CPU密集型的任务。在一些语言和框架中，协程和线程的特性可以灵活组合使用，以兼顾并发和并行的需求。</font>

<font style="color:rgb(55, 65, 81);">同一进程内的多个线程共享相同的地址空间</font>

1. **线程的独立栈：**<font style="color:rgb(55, 65, 81);"> 每个线程都有自己的栈，用于存储局部变量和函数调用信息。</font>**<font style="color:rgb(55, 65, 81);">栈是线程私有</font>**<font style="color:rgb(55, 65, 81);">的，一个线程的栈不会被其他线程访问或修改。</font>
2. **共享地址空间：**<font style="color:rgb(55, 65, 81);"> 线程共享进程地址空间，包括代码段、全局变量和堆内存。一个线程对进程中的全局变量的修改会影响其他线程。</font>
3. **独立堆：**<font style="color:rgb(55, 65, 81);"> 每个线程有自己的栈，但它们</font>**<font style="color:rgb(55, 65, 81);">共享进程的堆</font>**<font style="color:rgb(55, 65, 81);">。</font>**<font style="color:rgb(55, 65, 81);">堆是在运行时动态分配内存的地方</font>**<font style="color:rgb(55, 65, 81);">，多个线程可以通过堆进行数据共享。</font>

### 进程、线程、协程优缺点？
#### 进程：
##### 优点：
1. **独立性：**<font style="color:rgb(55, 65, 81);"> 进程之间拥有独立的地址空间，互不影响，有自己的独立内存空间。</font>
2. **安全性：**<font style="color:rgb(55, 65, 81);"> 进程间的数据相互隔离，一个进程崩溃不会影响其他进程。</font>
3. **多核利用：**<font style="color:rgb(55, 65, 81);"> 进程可以在多个处理器上并行执行，充分利用多核系统。</font>

##### 缺点：
1. **开销大：**<font style="color:rgb(55, 65, 81);"> 进程的创建和切换开销较大，涉及到独立的地址空间、文件描述符等资源。</font>
2. **通信复杂：**<font style="color:rgb(55, 65, 81);"> 进程间通信需要采用复杂的机制，如管道、消息队列、共享内存等。</font>
3. **启动慢：**<font style="color:rgb(55, 65, 81);"> 进程的启动通常比较慢，涉及到复杂的初始化过程。</font>

#### 线程：
##### 优点：
1. **资源共享：**<font style="color:rgb(55, 65, 81);"> 线程共享进程的地址空间和资源，线程间通信较为简便。</font>
2. **启动快：**<font style="color:rgb(55, 65, 81);"> 线程的创建和切换开销较小，启动速度较快。</font>
3. **并发性高：**<font style="color:rgb(55, 65, 81);"> 多线程可以更好地利用多核系统，提高并发性。</font>

##### 缺点：
1. **安全性问题：**<font style="color:rgb(55, 65, 81);"> 线程间共享内存，需要使用锁等同步机制来确保对共享资源的访问是安全的。</font>
2. **难以控制：**<font style="color:rgb(55, 65, 81);"> 多线程程序更容易出现竞态条件、死锁等问题，调试和维护较为复杂。</font>

#### 协程：
##### 优点：
1. **轻量级：**<font style="color:rgb(55, 65, 81);"> 协程是用户空间的轻量级线程，创建和切换开销小。</font>
2. **简单：**<font style="color:rgb(55, 65, 81);"> 协程的编程模型相对简单，不需要像线程那样复杂的同步机制。</font>
3. **高并发：**<font style="color:rgb(55, 65, 81);"> 协程可以在同一个线程内并发执行，充分发挥单线程的多任务能力。</font>

##### 缺点：
1. **无法利用多核：**<font style="color:rgb(55, 65, 81);"> 协程在单个线程内执行，无法充分利用多核系统。</font>
2. **依赖调度器：**<font style="color:rgb(55, 65, 81);"> 协程的调度需要一个协程调度器，需要程序员显式地管理调度，不够透明。</font>

### 进程上下文切换的是什么？
Linux 是一个多任务系统，每个任务运行前，<font style="color:rgb(59, 67, 81);">CPU 都需要知道任务从哪里加载、又从哪里开始运行，也就是说，需要系统事先帮它设置好</font><font style="color:rgb(59, 67, 81);"> </font>**<font style="color:rgb(59, 67, 81);">CPU 寄存器和程序计数器</font>**<font style="color:rgb(59, 67, 81);">（Program Counter，PC）。</font>

<font style="color:rgb(59, 67, 81);">CPU 寄存器，是 CPU 内置的容量小、但速度极快的内存。而程序计数器，则是用来存储 CPU 正在执行的指令位置、或者即将执行的下一条指令位置。它们都是 CPU 在运行任何任务前，必须的依赖环境，因此也被叫做 </font>**<font style="color:rgb(59, 67, 81);">CPU 上下文</font>**<font style="color:rgb(59, 67, 81);">。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706254029580-81727cd5-770c-47bc-90f8-6015198a0a94.png)

<font style="color:rgb(59, 67, 81);">CPU 上下文切换，就是先把前一个任务的 </font>**<font style="color:rgb(59, 67, 81);">CPU 上下文（也就是 CPU 寄存器和程序计数器）</font>**<font style="color:rgb(59, 67, 81);">保存起来，然后加载新任务的上下文到这些寄存器和程序计数器，最后再跳转到程序计数器所指的新位置，运行新任务。</font>

<font style="color:rgb(59, 67, 81);">而这些保存下来的上下文，会存储在系统内核中，并在任务重新调度执行时再次加载进来。这样就能保证任务原来的状态不受影响，让任务看起来还是连续运行。</font>

<font style="color:rgb(59, 67, 81);">任务就是进程，或者说任务就是线程。是的，进程和线程正是最常见的任务。但是除此之外，还有没有其他的任务呢？</font>

<font style="color:rgb(59, 67, 81);">不要忘了，硬件通过触发信号，会导致中断处理程序的调用，也是一种常见的任务。</font>

<font style="color:rgb(59, 67, 81);">根据任务的不同，CPU 的上下文切换可以分为几个不同的场景</font>

+ **<font style="color:rgb(59, 67, 81);">进程上下文切换</font>**
+ **<font style="color:rgb(59, 67, 81);">线程上下文切换</font>**
+ **<font style="color:rgb(59, 67, 81);">中断上下文切换</font>**

#### 进程上下文切换
<font style="color:rgb(59, 67, 81);">Linux 按照特权等级，把进程的运行空间分为内核空间和用户空间，分别对应着下图中， CPU 特权等级的 Ring 0 和 Ring 3。</font>

+ <font style="color:rgb(59, 67, 81);">内核空间（Ring 0）具有最高权限，可以直接访问所有资源；</font>
+ <font style="color:rgb(59, 67, 81);">用户空间（Ring 3）只能访问受限资源，不能直接访问内存等硬件设备，必须通过系统调用陷入到内核中，才能访问这些特权资源。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706254208866-87e8c32c-8d64-4be5-877d-88c2555627fd.png)

<font style="color:rgb(59, 67, 81);">进程既可以在用户空间运行，又可以在内核空间中运行。进程在用户空间运行时，被称为进程的用户态，而陷入内核空间的时候，被称为进程的内核态。</font>

<font style="color:rgb(59, 67, 81);">从用户态到内核态的转变，需要通过</font>**<font style="color:rgb(59, 67, 81);">系统调用</font>**<font style="color:rgb(59, 67, 81);">来完成。比如，当我们查看文件内容时，就需要多次系统调用来完成：首先调用 open() 打开文件，然后调用 read() 读取文件内容，并调用 write() 将内容写到标准输出，最后再调用 close() 关闭文件。</font>

<font style="color:rgb(59, 67, 81);">那么，系统调用的过程有没有发生 CPU 上下文的切换呢？答案自然是肯定的。</font>

<font style="color:rgb(59, 67, 81);">CPU 寄存器里原来用户态的指令位置，需要先保存起来。接着，为了执行内核态代码，CPU 寄存器需要更新为内核态指令的新位置。最后才是跳转到内核态运行内核任务。</font>

<font style="color:rgb(59, 67, 81);">而系统调用结束后，CPU寄存器需要</font>**<font style="color:rgb(59, 67, 81);">恢复</font>**<font style="color:rgb(59, 67, 81);">原来保存的用户态，然后再切换到用户空间，继续运行进程。所以，</font>**<font style="color:rgb(59, 67, 81);">一次系统调用的过程，其实是发生了两次 CPU 上下文切换</font>**<font style="color:rgb(59, 67, 81);">。</font>

<font style="color:rgb(59, 67, 81);">系统调用过程中，并不会涉及到虚拟内存等进程用户态的资源，也不会切换进程。这跟我们通常所说的进程上下文切换是不一样的：</font>

+ **<font style="color:rgb(59, 67, 81);">进程上下文切换，是指从一个进程切换到另一个进程运行。</font>**
+ **<font style="color:rgb(59, 67, 81);">而系统调用过程中一直是同一个进程在运行</font>**<font style="color:rgb(59, 67, 81);">。</font>

<font style="color:rgb(59, 67, 81);">所以，</font>**<font style="color:rgb(59, 67, 81);">系统调用过程通常称为特权模式切换，而不是上下文切换</font>**<font style="color:rgb(59, 67, 81);">。但实际上，系统调用过程中，CPU 的上下文切换还是无法避免的。</font>

<font style="color:rgb(59, 67, 81);">那么，进程上下文切换跟系统调用又有什么区别呢？</font>

<font style="color:rgb(59, 67, 81);">首先，你需要知道，</font>**<font style="color:rgb(59, 67, 81);">进程是由内核来管理和调度的，进程的切换只能发生在内核态</font>**<font style="color:rgb(59, 67, 81);">。所以，</font>**<font style="color:rgb(59, 67, 81);">进程的上下文不仅包括了虚拟内存、栈、全局变量等用户空间的资源，还包括了内核堆栈、寄存器等内核空间的状态</font>**<font style="color:rgb(59, 67, 81);">。</font>

<font style="color:rgb(59, 67, 81);">因此，进程的上下文切换就比系统调用时多了一步：</font>**<font style="color:rgb(59, 67, 81);">在保存当前进程的内核状态和CPU寄存器之前，需要先把该进程的虚拟内存、栈等保存下来；而加载了下一进程的内核态后，还需要刷新进程的虚拟内存和用户栈。</font>**

<font style="color:rgb(59, 67, 81);">如下图所示，保存上下文和恢复上下文的过程并不是“免费”的，需要内核在 CPU 上运行才能完成。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706254275045-09d2fc58-e4b2-4f86-a2b7-97276a3c6b90.png)

<font style="color:rgb(59, 67, 81);">根据</font><font style="color:rgb(59, 67, 81);"> </font>[Tsuna](https://blog.tsunanet.net/2010/11/how-long-does-it-take-to-make-context.html)<font style="color:rgb(59, 67, 81);"> </font><font style="color:rgb(59, 67, 81);">的测试报告，每次上下文切换都需要几十纳秒到数微秒的 CPU 时间。这个时间还是相当可观的，特别是在进程上下文切换次数较多的情况下，很容易导致 CPU 将大量时间耗费在寄存器、内核栈以及虚拟内存等资源的保存和恢复上，进而大大缩短了真正运行进程的时间。这也正是上一节中我们所讲的，导致平均负载升高的一个重要因素。</font>

<font style="color:rgb(59, 67, 81);">Linux 通过 TLB（Translation Lookaside Buffer）来管理虚拟内存到物理内存的映射关系。当虚拟内存更新后，TLB 也需要刷新，内存的访问也会随之变慢。特别是在多处理器系统上，缓存是被多个处理器共享的，刷新缓存不仅会影响当前处理器的进程，还会影响共享缓存的其他处理器的进程。</font>

<font style="color:rgb(59, 67, 81);">知道了进程上下文切换潜在的性能问题后，我们再来看，究竟什么时候会切换进程上下文。</font>

<font style="color:rgb(59, 67, 81);">显然，</font>**<font style="color:rgb(59, 67, 81);">进程切换时才需要切换上下文，换句话说，只有在进程调度的时候，才需要切换上下文</font>**<font style="color:rgb(59, 67, 81);">。Linux 为每个 CPU 都维护了一个就绪队列，将活跃进程（即正在运行和正在等待CPU的进程）按照优先级和等待 CPU 的时间排序，然后选择最需要 CPU 的进程，也就是优先级最高和等待CPU时间最长的进程来运行。</font>

<font style="color:rgb(59, 67, 81);">那么，进程在什么时候才会被调度到 CPU 上运行呢？</font>

<font style="color:rgb(59, 67, 81);">最容易想到的一个时机，就是进程执行完终止了，它之前使用的CPU会释放出来，这个时候再从就绪队列里，拿一个新的进程过来运行。其实还有很多其他场景，也会触发进程调度。</font>

##### <font style="color:rgb(59, 67, 81);">进程调度场景</font>
1. <font style="color:rgb(59, 67, 81);">为了保证所有进程可以得到公平调度，CPU时间被划分为一段段的时间片，这些时间片再被轮流分配给各个进程。这样，当某个进程的时间片耗尽了，就会被系统挂起，切换到其它正在等待 CPU 的进程运行。</font>
2. <font style="color:rgb(59, 67, 81);">进程在系统资源不足（比如内存不足）时，要等到资源满足后才可以运行，这个时候进程也会被挂起，并由系统调度其他进程运行。</font>
3. <font style="color:rgb(59, 67, 81);">当进程通过睡眠函数 sleep 这样的方法将自己主动挂起时，自然也会重新调度。</font>
4. <font style="color:rgb(59, 67, 81);">当有优先级更高的进程运行时，为了保证高优先级进程的运行，当前进程会被挂起，由高优先级进程来运行。</font>
5. <font style="color:rgb(59, 67, 81);">发生硬件中断时，CPU上的进程会被中断挂起，转而执行内核中的中断服务程序。</font>

<font style="color:rgb(59, 67, 81);">了解这几个场景是非常有必要的，因为一旦出现上下文切换的性能问题，它们就是幕后凶手。</font>

#### <font style="color:rgb(59, 67, 81);">线程上下文切换</font>
<font style="color:rgb(59, 67, 81);">线程与进程最大的区别在于，</font>**<font style="color:rgb(59, 67, 81);">线程是调度的基本单位，而进程则是资源拥有的基本单位</font>**<font style="color:rgb(59, 67, 81);">。说白了，所谓内核中的任务调度，实际上的调度对象是线程；而进程只是给线程提供了虚拟内存、全局变量等资源。所以，对于线程和进程，我们可以这么理解：</font>

+ <font style="color:rgb(59, 67, 81);">当进程只有一个线程时，可以认为进程就等于线程。</font>
+ <font style="color:rgb(59, 67, 81);">当进程拥有多个线程时，这些线程会共享相同的虚拟内存和全局变量等资源。这些资源在上下文切换时是不需要修改的。</font>
+ <font style="color:rgb(59, 67, 81);">另外，线程也有自己的私有数据，比如栈和寄存器等，这些在上下文切换时也是需要保存的。</font>

<font style="color:rgb(59, 67, 81);">线程的上下文切换分为两种情况：</font>

1. <font style="color:rgb(59, 67, 81);">前后两个线程属于不同进程。此时，因为资源不共享，所以切换过程就跟进程上下文切换是一样。</font>
2. <font style="color:rgb(59, 67, 81);">前后两个线程属于同一个进程。此时，因为虚拟内存是共享的，所以在切换时，虚拟内存这些资源就保持不动，只需要切换线程的私有数据、寄存器等不共享的数据。</font>

<font style="color:rgb(59, 67, 81);">虽然同为上下文切换，但</font>**<font style="color:rgb(59, 67, 81);">同进程内的线程切换，要比多进程间的切换消耗更少的资源</font>**<font style="color:rgb(59, 67, 81);">，而这，也正是多线程代替多进程的一个优势。</font>

#### <font style="color:rgb(59, 67, 81);">中断上下文切换</font>
<font style="color:rgb(59, 67, 81);">为了快速响应硬件的事件，</font>**<font style="color:rgb(59, 67, 81);">中断处理会打断进程的正常调度和执行</font>**<font style="color:rgb(59, 67, 81);">，转而调用中断处理程序，响应设备事件。而在打断其他进程时，就需要将进程当前的状态保存下来，这样在中断结束后，进程仍然可以从原来的状态恢复运行。</font>

<font style="color:rgb(59, 67, 81);">跟进程上下文不同，中断上下文切换并不涉及到进程的用户态。所以，即便中断过程打断了一个正处在用户态的进程，也不需要保存和恢复这个进程的虚拟内存、全局变量等用户态资源。中断上下文，其实只包括内核态中断服务程序执行所必需的状态，包括CPU 寄存器、内核堆栈、硬件中断参数等。</font>

**<font style="color:rgb(59, 67, 81);">对同一个 CPU 来说，中断处理比进程拥有更高的优先级</font>**<font style="color:rgb(59, 67, 81);">，所以中断上下文切换并不会与进程上下文切换同时发生。同样道理，由于中断会打断正常进程的调度和执行，所以大部分中断处理程序都短小精悍，以便尽可能快的执行结束。</font>

<font style="color:rgb(59, 67, 81);">另外，跟进程上下文切换一样，</font>**<font style="color:rgb(59, 67, 81);">中断上下文切换也需要消耗CPU，切换次数过多也会耗费大量的 CPU</font>**<font style="color:rgb(59, 67, 81);">，甚至严重降低系统的整体性能。所以，当你发现中断次数过多时，就需要注意去排查它是否会给你的系统带来严重的性能问题。</font>

#### <font style="color:rgb(59, 67, 81);">总结: </font>
1. **<font style="color:rgb(59, 67, 81);">CPU 上下文切换，是保证 Linux 系统正常工作的核心功能之一，一般情况下不需要我们特别关注。</font>**
2. **<font style="color:rgb(59, 67, 81);">但过多的上下文切换，会把CPU时间消耗在寄存器、内核栈以及虚拟内存等数据的保存和恢复上，从而缩短进程真正运行的时间，导致系统的整体性能大幅下降。</font>**

### 线程间共享的是什么?
#### 线程间独占资源
1. **线程特有的寄存器**： 每个线程都有自己的寄存器集，用于存储线程特有的局部变量和临时数据。这些寄存器在不同线程之间是独立的，切换线程时需要保存和恢复这些寄存器。
2. **栈空间**： 每个线程都有自己的栈空间，用于存储函数调用信息、局部变量等。线程的栈是线程私有的，不同线程之间的栈不共享。
3. **线程本地存储（Thread-Local Storage, TLS）**： 线程本地存储是一种线程私有的数据存储机制，每个线程都有自己的一份数据。它通常用于存储线程特有的全局变量或静态变量。
4. **线程 ID**： 每个线程都有一个唯一的线程 ID，可以用于在程序中区分不同的线程。
5. **寄存器上下文**： 在进行线程切换时，除了保存通用寄存器外，还需要保存线程的上下文信息，例如程序计数器（PC）等。
6. **线程局部变量**： 有些编程语言和库提供了线程局部变量的机制，用于在不同线程中保存各自的状态。

#### 线程间共享资源
1.  **代码区**: 进程地址空间中的代码区，保存的是我们写的代码，更准确的是编译后的可执行机器指令 
2. ** 数据区**: 进程地址空间中的数据区，存放的是所谓的全局变量,数据区中的全局变量有且仅有一个实例，所有的线程都可以访问到该全局变量。 
3.  **堆区**: 在C/C++中用 malloc 或者 new 出来的数据存放在这个区域，很显然，只要知道变量的地址，也就是指针，任何一个线程都可以访问指针指向的数据，因此堆区也是线程共享的属于进程的资源。 
4.  **栈区**: 从线程这个抽象的概念上来说，栈区是线程私有的,线程的栈区没有严格的隔离机制来保护，因此如果一个线程能拿到来自另一个线程栈帧上的指针，那么该线程就可以改变另一个线程的栈区，也就是说这些线程可以任意修改本属于另一个线程栈区中的变量。 
5.  **动态链接库**: **进程中的所有线程都可以使用动态链接库中的代码**。
    - 编译器在将可执行程序翻译成机器指令后，需要链接，链接完成后生成的才是可执行程序,完成链接这一过程的就是链接器。链接器可以有两种链接方式，这就是静态链接和动态链接。
    - 静态链接的意思是说把所有的机器指令一股脑全部打包到可执行程序中，动态链接的意思是我们不把动态链接的部分打包到可执行程序，而是在可执行程序运行起来后去内存中找动态链接的那部分代码，这就是所谓的静态链接和动态链接。
    - 动态链接一个显而易见的好处就是可执行程序的大小会很小，就像我们在Windows下看一个exe文件可能很小，那么该exe很可能是动态链接的方式生成的。而动态链接的部分生成的库就是我们熟悉的动态链接库，在Windows下是以DLL结尾的文件，在Linux下是以so结尾的文件。
    - **如果一个程序是动态链接生成的，那么其地址空间中有一部分包含的就是动态链接库，否则程序就运行不起来了，这一部分的地址空间也是被所有线程所共享的**。 
6.  **文件**: 如果程序在运行过程中打开了一些文件，那么进程地址空间中还保存有打开的文件信息，进程打开的文件也可以被所有的线程使用，这也属于线程间的共享资源。 
7. **TLS（线程局部存储）**：是指存放在该区域中的变量有两个含义：
    - 存放在该区域中的变量是全局变量，所有线程都可以访问
    - 虽然看上去所有线程访问的都是同一个变量，但该全局变量独属于一个线程，一个线程对此变量的修改对其他线程不可见。
    - 线程局部存储可以让你使用一个独属于线程的全局变量。也就是说，虽然该变量可以被所有线程访问，但该变量在每个线程中都有一个副本，一个线程对改变量的修改不会影响到其它线程。

**<font style="color:rgb(0, 0, 0);">进程是操作系统分配资源的单位，线程是调度的基本单位，线程之间共享进程资源。</font>**

**<font style="color:rgb(0, 0, 0);">线程运行的本质其实就是函数的执行</font>**<font style="color:rgb(0, 0, 0);">，函数的执行总会有一个源头，这个源头就是所谓的入口函数，CPU从入口函数开始执行从而形成一个执行流，只不过我们人为的给执行流起一个名字，这个名字就叫线程。</font>

<font style="color:rgb(0, 0, 0);">既然线程运行的本质就是函数的执行，那么函数执行都有哪些信息呢？</font>

<font style="color:rgb(0, 0, 0);">我们知道，函数运行时的信息保存在栈帧中，栈帧中保存了函数的返回值、调用其它函数的参数、该函数使用的局部变量以及该函数使用的寄存器信息，如图所示，假设函数A调用函数B：</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706258132024-da1c6508-c848-47fa-a109-97446baa1d92.png)

<font style="color:rgb(0, 0, 0);">此外，CPU执行指令的信息保存在一个叫做程序计数器的寄存器中，通过这个寄存器我们就知道接下来要执行哪一条指令。由于操作系统随时可以暂停线程的运行，因此我们保存以及恢复程序计数器中的值就能知道线程是从哪里暂停的以及该从哪里继续运行了。</font>

<font style="color:rgb(0, 0, 0);">由于线程运行的本质就是函数运行，函数运行时信息是保存在栈帧中的，因此每个线程都有自己独立的、私有的栈区。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706261006459-cf2f033e-bbd4-487a-9f8a-447e2c7c0c22.png)

<font style="color:rgb(0, 0, 0);">同时函数运行时需要额外的寄存器来保存一些信息，像部分局部变量之类，这些寄存器也是线程私有的，一个线程不可能访问到另一个线程的这类寄存器信息。</font>

<font style="color:rgb(0, 0, 0);">线程私有的是 -- </font>**<font style="color:rgb(0, 0, 0);">线程上下文（thread context）</font>**<font style="color:rgb(0, 0, 0);">： </font>

+ **<font style="color:rgb(0, 0, 0);">所属线程的栈区</font>**
+ **<font style="color:rgb(0, 0, 0);">程序计数器</font>**
+ **<font style="color:rgb(0, 0, 0);">栈指针</font>**
+ **<font style="color:rgb(0, 0, 0);">函数运行使用的寄存器</font>**<font style="color:rgb(0, 0, 0);">。</font>

<font style="color:rgb(0, 0, 0);">我们也说过操作系统调度线程需要随时中断线程的运行并且需要线程被暂停后可以继续运行，操作系统之所以能实现这一点，依靠的就是线程上下文信息。</font>

<font style="color:rgb(0, 0, 0);">现在你应该知道哪些是线程私有的了吧。</font>

<font style="color:rgb(0, 0, 0);">除此之外，剩下的都是线程间共享资源。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706261060901-c1463e61-adf1-4879-8a4c-c8529483e55b.png)

<font style="color:rgb(0, 0, 0);">这其实就是进程地址空间的样子，也就是说线程共享进程地址空间中除线程上下文信息中的所有内容，意思就是说线程可以</font>**<font style="color:rgb(0, 0, 0);">直接读取</font>**<font style="color:rgb(0, 0, 0);">这些内容。</font>

##### 代码区
<font style="color:rgb(0, 0, 0);">进程地址空间中的代码区，保存的是我们写的代码，</font>**<font style="color:rgb(0, 0, 0);">更准确的是编译后的可执行机器指令</font>**<font style="color:rgb(0, 0, 0);">。</font>

<font style="color:rgb(0, 0, 0);">那么这些机器指令又是从哪里来的呢？答案是从可执行文件中加载到内存的，可执行程序中的代码区就是用来初始化进程地址空间中的代码区的。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706263047873-099f3d63-fb5f-4e90-aab0-4fb672de2541.png)

<font style="color:rgb(0, 0, 0);">线程之间共享代码区，</font>**<font style="color:rgb(0, 0, 0);">这就意味着程序中的任何一个函数都可以放到线程中去执行，不存在某个函数只能被特定线程执行的情况。</font>**

##### 数据区
<font style="color:rgb(0, 0, 0);">进程地址空间中的数据区，这里存放的就是所谓的全局变量。</font>

<font style="color:rgb(0, 0, 0);">什么是全局变量？所谓全局变量就是那些你定义在函数之外的变量，在C语言中就像这样：</font>

```c
char c; // 全局变量

void func() {

}
```

<font style="color:rgb(0, 0, 0);">其中字符c就是全局变量，存放在进程地址空间中的数据区。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706263187438-7ca6a9b7-6aa8-4f71-8505-a67d6ccbbe1c.png)

<font style="color:rgb(0, 0, 0);">在程序员运行期间，也就是 run time，</font>**<font style="color:rgb(0, 0, 0);">数据区中的全局变量有且仅有一个实例，所有的线程都可以访问到该全局变量</font>**<font style="color:rgb(0, 0, 0);">。</font>

<font style="color:rgb(0, 0, 0);">值得注意的是，在C语言中还有一类特殊的“全局变量”，那就是用static关键词修饰过的变量，就像这样：</font>

```c
void func(){
    static int a = 10;
}
```

<font style="color:rgb(0, 0, 0);">注意到，</font>**<font style="color:rgb(0, 0, 0);">虽然变量a定义在函数内部，但变量a依然具有全局变量的特性</font>**<font style="color:rgb(0, 0, 0);">，也就是说变量a放在了进程地址空间的数据区域，</font>**<font style="color:rgb(0, 0, 0);">即使函数执行完后该变量依然存在</font>**<font style="color:rgb(0, 0, 0);">，而普通的局部变量随着函数调用结束和函数栈帧一起被回收掉了，但这里的变量a不会被回收，因为其被放到了数据区。</font><font style="color:rgba(0, 0, 0, 0.9);"></font>

<font style="color:rgb(0, 0, 0);">这样的变量对每个线程来说也是可见的，也就是说每个线程都可以访问到该变量。</font>

##### <font style="color:rgb(0, 0, 0);">堆区</font>
<font style="color:rgb(0, 0, 0);">堆区是程序员比较熟悉的，我们在C/C++中用 malloc 或者 new 出来的数据就存放在这个区域，很显然，</font>**<font style="color:rgb(0, 0, 0);">只要知道变量的地址，也就是指针，任何一个线程都可以访问指针指向的数据</font>**<font style="color:rgb(0, 0, 0);">，因此堆区也是线程共享的属于进程的资源。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706263276242-f9755394-745e-40cd-ad91-1a08c2a487d5.png)

##### 栈区
<font style="color:rgb(0, 0, 0);">唉，等等！刚不是说栈区是线程私有资源吗，怎么这会儿又说起栈区了？</font>

<font style="color:rgb(0, 0, 0);">确实，从线程这个抽象的概念上来说，栈区是线程私有的，然而从实际的实现上看，</font>**<font style="color:rgb(0, 0, 0);">栈区属于线程私有这一规则并没有严格遵守</font>**<font style="color:rgb(0, 0, 0);">，这句话是什么意思？</font>

<font style="color:rgb(0, 0, 0);">通常来说，注意这里的用词是</font>**<font style="color:rgb(0, 0, 0);">通常</font>**<font style="color:rgb(0, 0, 0);">，通常来说栈区是线程私有，既然有通常就有不通常的时候。</font>

<font style="color:rgb(0, 0, 0);">不通常是因为不像进程地址空间之间的严格隔离，线程的栈区没有严格的隔离机制来保护，因此如果一个线程能拿到来自另一个线程栈帧上的指针，</font>**<font style="color:rgb(0, 0, 0);">那么该线程就可以改变另一个线程的栈区</font>**<font style="color:rgb(0, 0, 0);">，也就是说这些线程可以任意修改本属于另一个线程栈区中的变量。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706263312366-8902ffd8-b925-4d5c-9701-b1d1372e85fa.png)

<font style="color:rgb(0, 0, 0);">这从某种程度上给了程序员极大的便利，但同时，这也会导致极其难以排查到的bug。</font>

<font style="color:rgb(0, 0, 0);">试想一下你的程序运行的好好的，结果某个时刻突然出问题，定位到出问题代码行后根本就排查不到原因，你当然是排查不到问题原因的，因为你的程序本来就没有任何问题，是别人的问题导致你的函数栈帧数据被写坏从而产生bug，这样的问题通常很难排查到原因，需要对整体的项目代码非常熟悉，常用的一些debug工具这时可能已经没有多大作用了。</font>

<font style="color:rgb(0, 0, 0);">说了这么多，那么同学可能会问，一个线程是怎样修改本属于其它线程的数据呢？</font>

<font style="color:rgb(0, 0, 0);">接下来我们用一个代码示例讲解一下。</font>

**<font style="color:rgb(0, 0, 0);">修改线程私有数据</font>**

```c
void thread(void* var) {
    int* p = (int*)var;
    *p = 2;
}

int main() {
    int a = 1;
    pthread_t tid;
    
    pthread_create(&tid, NULL, thread, (void*)&a);
    return 0;
}
```

<font style="color:rgb(0, 0, 0);">首先我们在主线程的栈区定义了一个局部变量，也就是 int a= 1这行代码，现在我们已经知道了，局部变量a属于主线程私有数据，但是，接下来我们创建了另外一个线程。</font>

<font style="color:rgb(0, 0, 0);">在新创建的这个线程中，我们将变量a的地址以参数的形式传给了新创建的线程，然后我来看一下thread函数。</font>

<font style="color:rgb(0, 0, 0);">在新创建的线程中，我们获取到了变量a的指针，然后将其修改为了2，也就是这行代码，我们在新创建的线程中修改了本属于主线程的私有数据。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706263388995-e4eb9f7f-583f-4119-aaab-cf89592af42e.png)

<font style="color:rgb(0, 0, 0);">现在你应该看明白了吧，尽管栈区是线程的私有数据，但由于栈区没有添加任何保护机制，一个线程的栈区对其它线程是可以见的，也就是说我们可以修改属于任何一个线程的栈区。</font>

<font style="color:rgb(0, 0, 0);">就像我们上文说得到的，这给程序员带来了极大便利的同时也带来了无尽的麻烦，试想上面这段代码，如果确实是项目需要那么这样写代码无可厚非，但如果上述新创建线程是因bug修改了属于其它线程的私有数据的话，那么产生问题就很难定位了，</font>**<font style="color:rgb(0, 0, 0);">因为bug可能距离问题暴露的这行代码已经很远了</font>**<font style="color:rgb(0, 0, 0);">，这样的问题通常难以排查。</font>

##### <font style="color:rgb(0, 0, 0);">动态链接库</font>
<font style="color:rgb(0, 0, 0);">进程地址空间中除了以上讨论的这些实际上还有其它内容，还有什么呢？</font>

<font style="color:rgb(0, 0, 0);">这就要从可执行程序说起了。</font>

<font style="color:rgb(0, 0, 0);">什么是可执行程序呢？在Windows中就是我们熟悉的exe文件，在Linux世界中就是ELF文件，这些可以被操作系统直接运行的程序就是我们所说的可执行程序。</font>

<font style="color:rgb(0, 0, 0);">那么可执行程序是怎么来的呢？</font>

<font style="color:rgb(0, 0, 0);">有的同学可能会说，废话，不就是编译器生成的吗？</font>

<font style="color:rgb(0, 0, 0);">实际上这个答案只答对了一半。</font>

<font style="color:rgb(0, 0, 0);">假设我们的项目比较简单只有几个源码文件，编译器是怎么把这几个源代码文件转换为最终的一个可执行程序呢？</font>

<font style="color:rgb(0, 0, 0);">原来，编译器在将可执行程序翻译成机器指令后，接下来还有一个重要的步骤，这就是链接，链接完成后生成的才是可执行程序。</font>

<font style="color:rgb(0, 0, 0);">完成链接这一过程的就是链接器。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706263446823-50034c87-d1ea-40c5-a54b-e3c7ca51311d.png)

<font style="color:rgb(0, 0, 0);">其中链接器可以有两种链接方式，这就是</font>**<font style="color:rgb(0, 0, 0);">静态链接</font>**<font style="color:rgb(0, 0, 0);">和</font>**<font style="color:rgb(0, 0, 0);">动态链接</font>**<font style="color:rgb(0, 0, 0);">。</font>

<font style="color:rgb(0, 0, 0);">静态链接的意思是说把所有的机器指令一股脑全部打包到可执行程序中，动态链接的意思是我们不把动态链接的部分打包到可执行程序，而是在可执行程序运行起来后去内存中找动态链接的那部分代码，这就是所谓的静态链接和动态链接。</font>

<font style="color:rgb(0, 0, 0);">动态链接一个显而易见的好处就是可执行程序的大小会很小，就像我们在Windows下看一个exe文件可能很小，</font>**<font style="color:rgb(0, 0, 0);">那么该exe很可能是动态链接的方式生成的</font>**<font style="color:rgb(0, 0, 0);">。</font>

<font style="color:rgb(0, 0, 0);">而动态链接的部分生成的库就是我们熟悉的动态链接库，在Windows下是以DLL结尾的文件，在Linux下是以so结尾的文件。</font>

<font style="color:rgb(0, 0, 0);">说了这么多，这和线程共享资源有什么关系呢？</font>

<font style="color:rgb(0, 0, 0);">原来如果一个程序是动态链接生成的，</font>**<font style="color:rgb(0, 0, 0);">那么其地址空间中有一部分包含的就是动态链接库</font>**<font style="color:rgb(0, 0, 0);">，否则程序就运行不起来了，这一部分的地址空间也是被所有线程所共享的。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706263476788-2d089412-97fc-45a0-a53e-9737119952f6.png)

<font style="color:rgb(0, 0, 0);">进程中的所有线程都可以使用动态链接库中的代码。</font>

##### <font style="color:rgb(0, 0, 0);">文件</font>
<font style="color:rgb(0, 0, 0);">最后，如果程序在运行过程中打开了一些文件，那么进程地址空间中还保存有打开的文件信息，进程打开的文件也可以被所有的线程使用，这也属于线程间的共享资源。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706263505852-4eea61a6-a2e7-435b-bb1f-113f65048308.png)

##### TLS（线程局部存储）
<font style="color:rgb(0, 0, 0);">线程局部存储，是指存放在该区域中的变量有两个含义：</font>

+ <font style="color:rgb(0, 0, 0);">存放在该区域中的变量是全局变量，所有线程都可以访问</font>
+ <font style="color:rgb(0, 0, 0);">虽然看上去所有线程访问的都是同一个变量，但该全局变量独属于一个线程，一个线程对此变量的修改对其他线程不可见。</font>

<font style="color:rgb(0, 0, 0);">我们先来看第一段代码：</font>

```c
int a = 1; // 全局变量

void print_a() {
    cout<<a<<endl;
}

void run() {
    ++a;
    print_a();
}

void main() {
    thread t1(run);
    t1.join();

    thread t2(run);
    t2.join();
}
```

<font style="color:rgb(0, 0, 0);">上述代码是用 C++11写的。</font>

+ <font style="color:rgb(0, 0, 0);">首先我们创建了一个全局变量a，初始值为1</font>
+ <font style="color:rgb(0, 0, 0);">其次我们创建了两个线程，每个线程对变量a加1</font>
+ <font style="color:rgb(0, 0, 0);">线程的join函数表示该线程运行完毕后才继续运行接下来的代码</font>

<font style="color:rgb(0, 0, 0);">这段代码的运行起来会打印什么呢？</font>

<font style="color:rgb(0, 0, 0);">全局变量a的初始值为1，第一个线程加1后a变为2，因此会打印2；第二个线程再次加1后a变为3，因此会打印3，让我们来看一下运行结果：</font>

```c
2
3
```

<font style="color:rgb(0, 0, 0);">看来我们分析的没错，全局变量在两个线程分别加1后最终变为3。</font>

<font style="color:rgb(0, 0, 0);">接下来我们对变量a的定义稍作修改，其它代码不做改动：</font>

```c
__thread int a = 1; // 线程局部存储
```

<font style="color:rgb(0, 0, 0);">我们看到全局变量a前面加了一个__thread关键词用来修饰，也就是说我们告诉编译器把变量a放在线程局部存储中，那这会对程序带来哪些改变呢？</font>

<font style="color:rgb(0, 0, 0);">简单运行一下就知道了：</font>

```c
2
2
```

<font style="color:rgb(0, 0, 0);">和你想的一样吗？有的同学可能会大吃一惊，为什么我们明明对变量a加了两次，但第二次运行为什么还是打印2而不是3呢？</font>

<font style="color:rgb(0, 0, 0);">原来，这就是线程局部存储的作用所在，</font>**<font style="color:rgb(0, 0, 0);">线程t1对变量a的修改不会影响到线程t2，线程t1在将变量a加到1后变为2，但对于线程t2来说此时变量a依然是1，因此加1后依然是2</font>**<font style="color:rgb(0, 0, 0);">。</font>

<font style="color:rgb(0, 0, 0);">因此，</font>**<font style="color:rgb(0, 0, 0);">线程局部存储可以让你使用一个独属于线程的全局变量</font>**<font style="color:rgb(0, 0, 0);">。也就是说，虽然该变量可以被所有线程访问，但该变量在每个线程中都有一个副本，一个线程对改变量的修改不会影响到其它线程。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706263687154-e794ed4d-5d86-4d39-8de0-1246fee48a87.png)

### 多进程、多线程、多协程之间的优缺点对比？
#### 多进程：
##### 优点：
1. **独立性：** 进程之间拥有独立的地址空间，互不影响，一个进程的崩溃不会影响其他进程。
2. **安全性：** 进程间的数据相互隔离，一个进程的错误不会对其他进程产生影响。
3. **多核利用：** 进程可以在多个处理器上并行执行，充分利用多核系统。

##### 缺点：
1. **开销大：** 进程的创建和切换开销较大，涉及到独立的地址空间、文件描述符等资源。
2. **通信复杂：** 进程间通信需要采用复杂的机制，如管道、消息队列、共享内存等。
3. **启动慢：** 进程的启动通常较慢，涉及到复杂的初始化过程。

#### 多线程：
##### 优点：
1. **资源共享：** 线程共享进程的地址空间和资源，线程间通信较为简便。
2. **启动快：** 线程的创建和切换开销较小，启动速度较快。
3. **并发性高：** 多线程可以更好地利用多核系统，提高并发性。

##### 缺点：
1. **安全性问题：** 线程间共享内存，需要使用锁等同步机制来确保对共享资源的访问是安全的。
2. **难以控制：** 多线程程序更容易出现竞态条件、死锁等问题，调试和维护较为复杂。

#### 多协程：
##### 优点：
1. **轻量级：** 协程是用户空间的轻量级线程，创建和切换开销小。
2. **简单：** 协程的编程模型相对简单，不需要像线程那样复杂的同步机制。
3. **高并发：** 协程可以在同一个线程内并发执行，充分发挥单线程的多任务能力。

##### 缺点：
1. **无法利用多核：** 协程在单个线程内执行，无法充分利用多核系统。
2. **依赖调度器：** 协程的调度需要一个协程调度器，需要程序员显式地管理调度，不够透明。

使用多进程、多线程还是多协程取决于具体的应用场景和需求。在某些情况下，可能需要结合使用这三者来充分发挥各自的优势。

### 进程间通信方式？
+ **管道： **
    - 单向传输，先进先出，通信方式效率低，不适合进程间频繁地交换数据
    - 匿名管道：**<font style="color:rgb(48, 79, 254);">通信范围是存在父子关系的进程</font>**
    - 命名管道：**<font style="color:rgb(48, 79, 254);">在不相关的进程间也能相互通信</font>**
+ **消息队列**
+ **共享内存**
+ **信号量**: PV操作
    - 互斥信号量
    - 同步信号量
+ **信号**
+ **Socket**

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706276439905-254ae6e9-33c7-4f62-bda7-8f8c749c6c05.png)

<font style="color:rgb(44, 62, 80);">每个进程的用户地址空间都是独立的，一般而言是不能互相访问的，但内核空间是每个进程都共享的，所以进程之间要通信必须通过内核。</font>

#### <font style="color:rgb(44, 62, 80);">管道</font>
```shell
$ ps auxf | grep mysql
```

<font style="color:rgb(44, 62, 80);">上面命令行里的「</font><font style="color:rgb(71, 101, 130);">|</font><font style="color:rgb(44, 62, 80);">」竖线就是一个</font>**<font style="color:rgb(48, 79, 254);">管道</font>**<font style="color:rgb(44, 62, 80);">，功能是将前一个命令（</font><font style="color:rgb(71, 101, 130);">ps auxf</font><font style="color:rgb(44, 62, 80);">）的输出，作为后一个命令（</font><font style="color:rgb(71, 101, 130);">grep mysql</font><font style="color:rgb(44, 62, 80);">）的输入，从这功能描述，可以看出</font>**<font style="color:rgb(48, 79, 254);">管道传输数据是单向的</font>**<font style="color:rgb(44, 62, 80);">，如果想相互通信，我们需要创建两个管道才行。</font>

<font style="color:rgb(44, 62, 80);">上面这种管道没有名字，所以「</font><font style="color:rgb(71, 101, 130);">|</font><font style="color:rgb(44, 62, 80);">」表示的管道称为</font>**<font style="color:rgb(48, 79, 254);">匿名管道</font>**<font style="color:rgb(44, 62, 80);">，用完了就销毁。</font>

<font style="color:rgb(44, 62, 80);">管道还有另外一个类型是</font>**<font style="color:rgb(48, 79, 254);">命名管道</font>**<font style="color:rgb(44, 62, 80);">，也被叫做</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FIFO</font><font style="color:rgb(44, 62, 80);">，因为数据是先进先出的传输方式。</font>

<font style="color:rgb(44, 62, 80);">在使用命名管道前，先需要通过 </font><font style="color:rgb(71, 101, 130);">mkfifo</font><font style="color:rgb(44, 62, 80);"> 命令来创建，并且指定管道名字：</font>

```shell
$ mkfifo myPipe
```

<font style="color:rgb(44, 62, 80);">myPipe 就是这个管道的名称，基于 Linux 一切皆文件的理念，所以管道也是以文件的方式存在，我们可以用 ls 看一下，这个文件的类型是 p，也就是 pipe（管道） 的意思：</font>

```shell
$ ls -l
prw-r--r--. 1 root    root         0 Jul 17 02:45 myPipe
```

<font style="color:rgb(44, 62, 80);">接下来，我们往 myPipe 这个管道写入数据：</font>

```shell
$ echo "hello" > myPipe  // 将数据写进管道
                         // 停住了 ...
```

<font style="color:rgb(44, 62, 80);">你操作了后，你会发现命令执行后就停在这了，这是因为</font>**<font style="color:rgb(44, 62, 80);">管道里的内容没有被读取，只有当管道里的数据被读完后，命令才可以正常退出</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">于是，我们执行另外一个命令来读取这个管道里的数据：</font>

```bash
$ cat < myPipe  // 读取管道里的数据
hello
```

<font style="color:rgb(44, 62, 80);">可以看到，管道里的内容被读取出来了，并打印在了终端上，另外一方面，echo 那个命令也正常退出了。</font>

<font style="color:rgb(44, 62, 80);"></font>**<font style="color:rgb(48, 79, 254);">管道这种通信方式效率低，不适合进程间频繁地交换数据</font>**<font style="color:rgb(44, 62, 80);">。当然，它的好处，自然就是简单，同时也我们很容易得知管道里的数据已经被另一个进程读取了。</font>

<font style="color:rgb(44, 62, 80);background-color:rgb(227, 242, 253);">那管道如何创建呢，背后原理是什么？</font>

<font style="color:rgb(44, 62, 80);">匿名管道的创建，需要通过下面这个系统调用：</font>

```c
int pipe(int fd[2])
```

<font style="color:rgb(44, 62, 80);">这里表示创建一个匿名管道，并返回了两个描述符，一个是管道的读取端描述符 </font><font style="color:rgb(71, 101, 130);">fd[0]</font><font style="color:rgb(44, 62, 80);">，另一个是管道的写入端描述符 </font><font style="color:rgb(71, 101, 130);">fd[1]</font><font style="color:rgb(44, 62, 80);">。注意，这个匿名管道是特殊的文件，只存在于内存，不存于文件系统中。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706360568499-143a67ee-5c70-45ff-9a83-df05ca14f5e4.png)

<font style="color:rgb(44, 62, 80);"></font>**<font style="color:rgb(48, 79, 254);">所谓的管道，就是内核里面的一串缓存</font>**<font style="color:rgb(44, 62, 80);">。从管道的一段写入的数据，是缓存在内核中的，另一端读取，也就是从内核中读取这段数据。另外，管道传输的数据是无格式的流且大小受限。</font>

<font style="color:rgb(44, 62, 80);">看到这，你可能会有疑问了，这两个描述符都是在一个进程里面，并没有起到进程间通信的作用，怎么样才能使得管道是跨过两个进程的呢？</font>

<font style="color:rgb(44, 62, 80);">我们可以使用 </font><font style="color:rgb(71, 101, 130);">fork</font><font style="color:rgb(44, 62, 80);"> 创建子进程，</font>**<font style="color:rgb(48, 79, 254);">创建的子进程会复制父进程的文件描述符</font>**<font style="color:rgb(44, 62, 80);">，这样就做到了两个进程各有两个「 </font><font style="color:rgb(71, 101, 130);">fd[0]</font><font style="color:rgb(44, 62, 80);"> 与 </font><font style="color:rgb(71, 101, 130);">fd[1]</font><font style="color:rgb(44, 62, 80);">」，两个进程就可以通过各自的 fd 写入和读取同一个管道文件实现跨进程通信了。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706360633510-dc63c4c4-43b2-48f6-bda1-192048706613.png)

<font style="color:rgb(44, 62, 80);">管道只能一端写入，另一端读出，所以上面这种模式容易造成混乱，因为父进程和子进程都可以同时写入，也都可以读出。那么，为了避免这种情况，通常的做法是：</font>

+ <font style="color:rgb(44, 62, 80);">父进程关闭读取的 fd[0]，只保留写入的 fd[1]；</font>
+ <font style="color:rgb(44, 62, 80);">子进程关闭写入的 fd[1]，只保留读取的 fd[0]；</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706360653338-6d100d09-1e4f-45fa-a593-b773b89b78b9.png)

<font style="color:rgb(44, 62, 80);">所以说如果需要双向通信，则应该创建两个管道。</font>

<font style="color:rgb(44, 62, 80);">到这里，我们仅仅解析了使用管道进行父进程与子进程之间的通信，但是在我们 shell 里面并不是这样的。</font>

<font style="color:rgb(44, 62, 80);">在 shell 里面执行 </font><font style="color:rgb(71, 101, 130);">A | B</font><font style="color:rgb(44, 62, 80);">命令的时候，A 进程和 B 进程都是 shell 创建出来的子进程，A 和 B 之间不存在父子关系，它俩的父进程都是 shell。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706360675407-131b0620-67eb-4687-bd91-62aa22de6815.png)

<font style="color:rgb(44, 62, 80);">所以说，在 shell 里通过「</font><font style="color:rgb(71, 101, 130);">|</font><font style="color:rgb(44, 62, 80);">」匿名管道将多个命令连接在一起，实际上也就是创建了多个子进程，那么在我们编写 shell 脚本时，能使用一个管道搞定的事情，就不要多用一个管道，这样可以减少创建子进程的系统开销。</font>

<font style="color:rgb(44, 62, 80);"></font>**<font style="color:rgb(48, 79, 254);">对于匿名管道，它的通信范围是存在父子关系的进程</font>**<font style="color:rgb(44, 62, 80);">。因为管道没有实体，也就是没有管道文件，只能通过 fork 来复制父进程 fd 文件描述符，来达到通信的目的。</font>

<font style="color:rgb(44, 62, 80);"></font>**<font style="color:rgb(48, 79, 254);">对于命名管道，它可以在不相关的进程间也能相互通信</font>**<font style="color:rgb(44, 62, 80);">。因为命令管道，提前创建了一个类型为管道的设备文件，在进程里只要使用这个设备文件，就可以相互通信。</font>

<font style="color:rgb(44, 62, 80);">不管是匿名管道还是命名管道，进程写入的数据都是缓存在内核中，另一个进程读取数据时候自然也是从内核中获取，同时通信数据都遵循</font>**<font style="color:rgb(48, 79, 254);">先进先出</font>**<font style="color:rgb(44, 62, 80);">原则，不支持 lseek 之类的文件定位操作。</font>

#### <font style="color:rgb(44, 62, 80);">消息队列</font>
<font style="color:rgb(44, 62, 80);">前面说到管道的通信方式是效率低的，因此管道不适合进程间频繁地交换数据。</font>

<font style="color:rgb(44, 62, 80);">对于这个问题，</font>**<font style="color:rgb(48, 79, 254);">消息队列</font>**<font style="color:rgb(44, 62, 80);">的通信模式就可以解决。比如，A 进程要给 B 进程发送消息，A 进程把数据放在对应的消息队列后就可以正常返回了，B 进程需要的时候再去读取数据就可以了。同理，B 进程要给 A 进程发送消息也是如此。</font>

<font style="color:rgb(44, 62, 80);"></font>**<font style="color:rgb(48, 79, 254);">消息队列是保存在内核中的消息链表</font>**<font style="color:rgb(44, 62, 80);">，在发送数据时，会分成一个一个独立的数据单元，也就是消息体（数据块），消息体是用户自定义的数据类型，消息的发送方和接收方要约定好消息体的数据类型，所以每个消息体都是固定大小的存储块，不像管道是无格式的字节流数据。如果进程从消息队列中读取了消息体，内核就会把这个消息体删除。</font>

<font style="color:rgb(44, 62, 80);">消息队列生命周期随内核，如果没有释放消息队列或者没有关闭操作系统，消息队列会一直存在，而前面提到的匿名管道的生命周期，是随进程的创建而建立，随进程的结束而销毁。</font>

<font style="color:rgb(44, 62, 80);">消息这种模型，两个进程之间的通信就像平时发邮件一样，你来一封，我回一封，可以频繁沟通了。</font>

<font style="color:rgb(44, 62, 80);">但邮件的通信方式存在不足的地方有两点，</font>**<font style="color:rgb(48, 79, 254);">一是通信不及时，二是附件也有大小限制</font>**<font style="color:rgb(44, 62, 80);">，这同样也是消息队列通信不足的点。</font>

**<font style="color:rgb(48, 79, 254);">消息队列不适合比较大数据的传输</font>**<font style="color:rgb(44, 62, 80);">，因为在内核中每个消息体都有一个最大长度的限制，同时所有队列所包含的全部消息体的总长度也是有上限。在 Linux 内核中，会有两个宏定义</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">MSGMAX</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">和</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">MSGMNB</font><font style="color:rgb(44, 62, 80);">，它们以字节为单位，分别定义了一条消息的最大长度和一个队列的最大长度。</font>

**<font style="color:rgb(48, 79, 254);">消息队列通信过程中，存在用户态与内核态之间的数据拷贝开销</font>**<font style="color:rgb(44, 62, 80);">，因为进程写入数据到内核中的消息队列时，会发生从用户态拷贝数据到内核态的过程，同理另一进程读取内核中的消息数据时，会发生从内核态拷贝数据到用户态的过程。</font>

#### 共享内存
<font style="color:rgb(44, 62, 80);">消</font><font style="color:rgb(44, 62, 80);">息队列的读取和写入的过程，都会有发生用户态与内核态之间的消息拷贝过程。那</font>**<font style="color:rgb(48, 79, 254);">共享内存</font>**<font style="color:rgb(44, 62, 80);">的方式，就很好的解决了这一问题。</font>

<font style="color:rgb(44, 62, 80);">现代操作系统，对于内存管理，采用的是虚拟内存技术，也就是每个进程都有自己独立的虚拟内存空间，不同进程的虚拟内存映射到不同的物理内存中。所以，即使进程 A 和 进程 B 的虚拟地址是一样的，其实访问的是不同的物理内存地址，对于数据的增删查改互不影响。</font>

**<font style="color:rgb(48, 79, 254);">共享内存：拿出一块虚拟地址空间来，映射到相同的物理内存中</font>**<font style="color:rgb(44, 62, 80);">。这样这个进程写入的东西，另外一个进程马上就能看到了，都不需要拷贝来拷贝去，传来传去，大大提高了进程间通信的速度。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706361566005-1ef8c75a-e124-4678-a5c2-1a602063bc6b.png)

#### 信号量
<font style="color:rgb(44, 62, 80);">共享内存通信方式带来的新问题，就是如果多个进程同时修改同一个共享内存，很有可能就冲突了。例如两个进程都同时写一个地址，那先写的那个进程会发现内容被别人覆盖了。</font>

<font style="color:rgb(44, 62, 80);">为了防止多进程竞争共享资源，而造成的数据错乱，所以需要保护机制，使得共享的资源，在任意时刻只能被一个进程访问。正好，</font>**<font style="color:rgb(48, 79, 254);">信号量</font>**<font style="color:rgb(44, 62, 80);">就实现了这一保护机制。</font>

**<font style="color:rgb(48, 79, 254);">信号量其实是一个整型的计数器，主要用于实现进程间的互斥与同步，而不是用于缓存进程间通信的数据</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">信号量表示资源的数量，控制信号量的方式有两种原子操作：</font>

+ <font style="color:rgb(44, 62, 80);">一个是</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">P 操作</font>**<font style="color:rgb(44, 62, 80);">，这个操作会把信号量减去 1，相减后如果信号量 < 0，则表明资源已被占用，进程需阻塞等待；相减后如果信号量 >= 0，则表明还有资源可使用，进程可正常继续执行。</font>
+ <font style="color:rgb(44, 62, 80);">另一个是</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">V 操作</font>**<font style="color:rgb(44, 62, 80);">，这个操作会把信号量加上 1，相加后如果信号量 <= 0，则表明当前有阻塞中的进程，于是会将该进程唤醒运行；相加后如果信号量 > 0，则表明当前没有阻塞中的进程；</font>

<font style="color:rgb(44, 62, 80);">P 操作是用在进入共享资源之前，V 操作是用在离开共享资源之后，这两个操作是必须成对出现的。</font>

<font style="color:rgb(44, 62, 80);">接下来，举个例子，如果要使得两个进程互斥访问共享内存，我们可以初始化信号量为 </font><font style="color:rgb(71, 101, 130);">1</font><font style="color:rgb(44, 62, 80);">。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706361615612-2ce659e6-e93c-4d3e-b113-ca2bfce6b9d9.png)

<font style="color:rgb(44, 62, 80);">具体的过程如下：</font>

+ <font style="color:rgb(44, 62, 80);">进程 A 在访问共享内存前，先执行了 P 操作，由于信号量的初始值为 1，故在进程 A 执行 P 操作后信号量变为 0，表示共享资源可用，于是进程 A 就可以访问共享内存。</font>
+ <font style="color:rgb(44, 62, 80);">若此时，进程 B 也想访问共享内存，执行了 P 操作，结果信号量变为了 -1，这就意味着临界资源已被占用，因此进程 B 被阻塞。</font>
+ <font style="color:rgb(44, 62, 80);">直到进程 A 访问完共享内存，才会执行 V 操作，使得信号量恢复为 0，接着就会唤醒阻塞中的线程 B，使得进程 B 可以访问共享内存，最后完成共享内存的访问后，执行 V 操作，使信号量恢复到初始值 1。</font>

<font style="color:rgb(44, 62, 80);">可以发现，信号初始化为</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">1</font><font style="color:rgb(44, 62, 80);">，就代表着是</font>**<font style="color:rgb(48, 79, 254);">互斥信号量</font>**<font style="color:rgb(44, 62, 80);">，它可以保证共享内存在任何时刻只有一个进程在访问，这就很好的保护了共享内存。</font>

<font style="color:rgb(44, 62, 80);">另外，在多进程里，每个进程并不一定是顺序执行的，它们基本是以各自独立的、不可预知的速度向前推进，但有时候我们又希望多个进程能密切合作，以实现一个共同的任务。</font>

<font style="color:rgb(44, 62, 80);">例如，进程 A 是负责生产数据，而进程 B 是负责读取数据，这两个进程是相互合作、相互依赖的，进程 A 必须先生产了数据，进程 B 才能读取到数据，所以执行是有前后顺序的。</font>

<font style="color:rgb(44, 62, 80);">那么这时候，就可以用信号量来实现多进程同步的方式，我们可以初始化信号量为 </font><font style="color:rgb(71, 101, 130);">0</font><font style="color:rgb(44, 62, 80);">。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706361661887-d0d7a7ee-5ef6-4c51-89a3-0e9b20918a10.png)

<font style="color:rgb(44, 62, 80);">具体过程：</font>

+ <font style="color:rgb(44, 62, 80);">如果进程 B 比进程 A 先执行了，那么执行到 P 操作时，由于信号量初始值为 0，故信号量会变为 -1，表示进程 A 还没生产数据，于是进程 B 就阻塞等待；</font>
+ <font style="color:rgb(44, 62, 80);">接着，当进程 A 生产完数据后，执行了 V 操作，就会使得信号量变为 0，于是就会唤醒阻塞在 P 操作的进程 B；</font>
+ <font style="color:rgb(44, 62, 80);">最后，进程 B 被唤醒后，意味着进程 A 已经生产了数据，于是进程 B 就可以正常读取数据了。</font>

<font style="color:rgb(44, 62, 80);">可以发现，信号初始化为 </font><font style="color:rgb(71, 101, 130);">0</font><font style="color:rgb(44, 62, 80);">，就代表着是</font>**<font style="color:rgb(48, 79, 254);">同步信号量</font>**<font style="color:rgb(44, 62, 80);">，它可以保证进程 A 应在进程 B 之前执行。</font>

#### <font style="color:rgb(44, 62, 80);">信号</font>
<font style="color:rgb(44, 62, 80);">上面说的进程间通信，都是常规状态下的工作模式。</font>**<font style="color:rgb(48, 79, 254);">对于异常情况下的工作模式，就需要用「信号」的方式来通知进程。</font>**

<font style="color:rgb(44, 62, 80);">信号跟信号量两者用途完全不一样。</font>

<font style="color:rgb(44, 62, 80);">在 Linux 操作系统中， 为了响应各种各样的事件，提供了几十种信号，分别代表不同的意义。我们可以通过 </font><font style="color:rgb(71, 101, 130);">kill -l</font><font style="color:rgb(44, 62, 80);"> 命令，查看所有的信号：</font>

```shell
$ kill -l
 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
63) SIGRTMAX-1  64) SIGRTMAX
```

<font style="color:rgb(44, 62, 80);">运行在 shell 终端的进程，我们可以通过键盘输入某些组合键的时候，给进程发送信号。例如</font>

+ <font style="color:rgb(44, 62, 80);">Ctrl+C 产生</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SIGINT</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">信号，表示终止该进程；</font>
+ <font style="color:rgb(44, 62, 80);">Ctrl+Z 产生</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SIGTSTP</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">信号，表示停止该进程，但还未结束；</font>

<font style="color:rgb(44, 62, 80);">如果进程在后台运行，可以通过</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">kill</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">命令的方式给进程发送信号，但前提需要知道运行中的进程 PID 号，例如：</font>

+ <font style="color:rgb(44, 62, 80);">kill -9 1050 ，表示给 PID 为 1050 的进程发送</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SIGKILL</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">信号，用来立即结束该进程；</font>

<font style="color:rgb(44, 62, 80);">所以，</font>**<font style="color:rgb(44, 62, 80);">信号事件的来源主要有硬件来源（如键盘 Cltr+C ）和软件来源（如 kill 命令）</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">信号是进程间通信机制中</font>**<font style="color:rgb(48, 79, 254);">唯一的异步通信机制</font>**<font style="color:rgb(44, 62, 80);">，因为可以在任何时候发送信号给某一进程，一旦有信号产生，我们就有下面这几种，用户进程对信号的处理方式。</font>

**<font style="color:rgb(48, 79, 254);">1.执行默认操作</font>**<font style="color:rgb(44, 62, 80);">。Linux 对每种信号都规定了默认操作，例如，上面列表中的 SIGTERM 信号，就是终止进程的意思。</font>

**<font style="color:rgb(48, 79, 254);">2.捕捉信号</font>**<font style="color:rgb(44, 62, 80);">。我们可以为信号定义一个信号处理函数。当信号发生时，我们就执行相应的信号处理函数。</font>

**<font style="color:rgb(48, 79, 254);">3.忽略信号</font>**<font style="color:rgb(44, 62, 80);">。当我们不希望处理某些信号的时候，就可以忽略该信号，不做任何处理。有两个信号是应用进程无法捕捉和忽略的，即 </font><font style="color:rgb(71, 101, 130);">SIGKILL</font><font style="color:rgb(44, 62, 80);"> 和 </font><font style="color:rgb(71, 101, 130);">SEGSTOP</font><font style="color:rgb(44, 62, 80);">，它们用于在任何时候中断或结束某一进程。</font>

#### <font style="color:rgb(44, 62, 80);">Socket</font>
<font style="color:rgb(44, 62, 80);">前面提到的管道、消息队列、共享内存、信号量和信号都是在同一台主机上进行进程间通信，那要想</font>**<font style="color:rgb(48, 79, 254);">跨网络与不同主机上的进程之间通信，就需要 Socket 通信了。</font>**

<font style="color:rgb(44, 62, 80);">实际上，Socket 通信不仅可以跨网络与不同主机的进程间通信，还可以在同主机上进程间通信。</font>

<font style="color:rgb(44, 62, 80);">我们来看看创建 socket 的系统调用：</font>

```c
int socket(int domain, int type, int protocal)
```

<font style="color:rgb(44, 62, 80);">三个参数分别代表：</font>

+ <font style="color:rgb(44, 62, 80);">domain 参数用来指定协议族，比如 AF_INET 用于 IPV4、AF_INET6 用于 IPV6、AF_LOCAL/AF_UNIX 用于本机；</font>
+ <font style="color:rgb(44, 62, 80);">type 参数用来指定通信特性，比如 SOCK_STREAM 表示的是字节流，对应 TCP、SOCK_DGRAM 表示的是数据报，对应 UDP、SOCK_RAW 表示的是原始套接字；</font>
+ <font style="color:rgb(44, 62, 80);">protocol 参数原本是用来指定通信协议的，但现在基本废弃。因为协议已经通过前面两个参数指定完成，protocol 目前一般写成 0 即可；</font>

<font style="color:rgb(44, 62, 80);">根据创建 socket 类型的不同，通信的方式也就不同：</font>

+ <font style="color:rgb(44, 62, 80);">实现 TCP 字节流通信： socket 类型是 AF_INET 和 SOCK_STREAM；</font>
+ <font style="color:rgb(44, 62, 80);">实现 UDP 数据报通信：socket 类型是 AF_INET 和 SOCK_DGRAM；</font>
+ <font style="color:rgb(44, 62, 80);">实现本地进程间通信： 「本地字节流 socket 」类型是 AF_LOCAL 和 SOCK_STREAM，「本地数据报 socket 」类型是 AF_LOCAL 和 SOCK_DGRAM。另外，AF_UNIX 和 AF_LOCAL 是等价的，所以 AF_UNIX 也属于本地 socket；</font>

<font style="color:rgb(44, 62, 80);">接下来，简单说一下这三种通信的编程模式。</font>

> <font style="color:rgb(44, 62, 80);">针对 TCP 协议通信的 socket 编程模型</font>
>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706362096190-bdd13583-9ecb-439c-a035-bf50211e8c30.png)

+ <font style="color:rgb(44, 62, 80);">服务端和客户端初始化</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">socket</font><font style="color:rgb(44, 62, 80);">，得到文件描述符；</font>
+ <font style="color:rgb(44, 62, 80);">服务端调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">bind</font><font style="color:rgb(44, 62, 80);">，将绑定在 IP 地址和端口;</font>
+ <font style="color:rgb(44, 62, 80);">服务端调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">listen</font><font style="color:rgb(44, 62, 80);">，进行监听；</font>
+ <font style="color:rgb(44, 62, 80);">服务端调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">accept</font><font style="color:rgb(44, 62, 80);">，等待客户端连接；</font>
+ <font style="color:rgb(44, 62, 80);">客户端调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">connect</font><font style="color:rgb(44, 62, 80);">，向服务器端的地址和端口发起连接请求；</font>
+ <font style="color:rgb(44, 62, 80);">服务端</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">accept</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">返回用于传输的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">socket</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">的文件描述符；</font>
+ <font style="color:rgb(44, 62, 80);">客户端调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">write</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">写入数据；服务端调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">read</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">读取数据；</font>
+ <font style="color:rgb(44, 62, 80);">客户端断开连接时，会调用 </font><font style="color:rgb(71, 101, 130);">close</font><font style="color:rgb(44, 62, 80);">，那么服务端 </font><font style="color:rgb(71, 101, 130);">read</font><font style="color:rgb(44, 62, 80);"> 读取数据的时候，就会读取到了 </font><font style="color:rgb(71, 101, 130);">EOF</font><font style="color:rgb(44, 62, 80);">，待处理完数据后，服务端调用 </font><font style="color:rgb(71, 101, 130);">close</font><font style="color:rgb(44, 62, 80);">，表示连接关闭。</font>

<font style="color:rgb(44, 62, 80);">这里需要注意的是，服务端调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">accept</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">时，连接成功了会返回一个已完成连接的 socket，后续用来传输数据。</font>

<font style="color:rgb(44, 62, 80);">所以，监听的 socket 和真正用来传送数据的 socket，是「</font>**<font style="color:rgb(48, 79, 254);">两个</font>**<font style="color:rgb(44, 62, 80);">」 socket，一个叫作</font>**<font style="color:rgb(48, 79, 254);">监听 socket</font>**<font style="color:rgb(44, 62, 80);">，一个叫作</font>**<font style="color:rgb(48, 79, 254);">已完成连接 socket</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">成功连接建立之后，双方开始通过 read 和 write 函数来读写数据，就像往一个文件流里面写东西一样。</font>

> <font style="color:rgb(44, 62, 80);background-color:rgb(227, 242, 253);">针对 UDP 协议通信的 socket 编程模型</font>
>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706362135548-c8f471a7-6812-4d48-a0ac-db584f973fcd.png)

<font style="color:rgb(44, 62, 80);">UDP 是没有连接的，所以不需要三次握手，也就不需要像 TCP 调用 listen 和 connect，但是 UDP 的交互仍然需要 IP 地址和端口号，因此也需要 bind。</font>

<font style="color:rgb(44, 62, 80);">对于 UDP 来说，不需要要维护连接，那么也就没有所谓的发送方和接收方，甚至都不存在客户端和服务端的概念，只要有一个 socket 多台机器就可以任意通信，因此每一个 UDP 的 socket 都需要 bind。</font>

<font style="color:rgb(44, 62, 80);">另外，每次通信时，调用 sendto 和 recvfrom，都要传入目标主机的 IP 地址和端口。</font>

> <font style="color:rgb(44, 62, 80);background-color:rgb(227, 242, 253);">针对本地进程间通信的 socket 编程模型</font>
>

<font style="color:rgb(44, 62, 80);">本地 socket 被用于在</font>**<font style="color:rgb(48, 79, 254);">同一台主机上进程间通信</font>**<font style="color:rgb(44, 62, 80);">的场景：</font>

+ <font style="color:rgb(44, 62, 80);">本地 socket 的编程接口和 IPv4 、IPv6 套接字编程接口是一致的，可以支持「字节流」和「数据报」两种协议；</font>
+ <font style="color:rgb(44, 62, 80);">本地 socket 的实现效率大大高于 IPv4 和 IPv6 的字节流、数据报 socket 实现；</font>

<font style="color:rgb(44, 62, 80);">对于本地字节流 socket，其 socket 类型是 AF_LOCAL 和 SOCK_STREAM。</font>

<font style="color:rgb(44, 62, 80);">对于本地数据报 socket，其 socket 类型是 AF_LOCAL 和 SOCK_DGRAM。</font>

<font style="color:rgb(44, 62, 80);">本地字节流 socket 和 本地数据报 socket 在 bind 的时候，不像 TCP 和 UDP 要绑定 IP 地址和端口，而是</font>**<font style="color:rgb(48, 79, 254);">绑定一个本地文件</font>**<font style="color:rgb(44, 62, 80);">，这也就是它们之间的最大区别。</font>

#### <font style="color:rgb(44, 62, 80);">总结</font>
<font style="color:rgb(44, 62, 80);">由于每个进程的用户空间都是独立的，不能相互访问，这时就需要借助内核空间来实现进程间通信，原因很简单，每个进程都是共享一个内核空间。</font>

<font style="color:rgb(44, 62, 80);">Linux 内核提供了不少进程间通信的方式，最简单的方式就是管道，管道分为「匿名管道」和「命名管道」。</font>

+ **<font style="color:rgb(48, 79, 254);">匿名管道</font>**<font style="color:rgb(44, 62, 80);">顾名思义，它没有名字标识，匿名管道是特殊文件只存在于内存，没有存在于文件系统中，shell 命令中的「</font><font style="color:rgb(71, 101, 130);">|</font><font style="color:rgb(44, 62, 80);">」竖线就是匿名管道，通信的数据是</font>**<font style="color:rgb(48, 79, 254);">无格式的流并且大小受限</font>**<font style="color:rgb(44, 62, 80);">，通信的方式是</font>**<font style="color:rgb(48, 79, 254);">单向</font>**<font style="color:rgb(44, 62, 80);">的，数据只能在一个方向上流动，如果要双向通信，需要创建两个管道，再来</font>**<font style="color:rgb(48, 79, 254);">匿名管道是只能用于存在父子关系的进程间通信</font>**<font style="color:rgb(44, 62, 80);">，匿名管道的生命周期随着进程创建而建立，随着进程终止而消失。</font>
+ **<font style="color:rgb(48, 79, 254);">命名管道</font>**<font style="color:rgb(44, 62, 80);">突破了匿名管道只能在亲缘关系进程间的通信限制，因为使用命名管道的前提，需要在文件系统创建一个类型为 p 的设备文件，那么毫无关系的进程就可以通过这个设备文件进行通信。另外，不管是匿名管道还是命名管道，进程写入的数据都是</font>**<font style="color:rgb(48, 79, 254);">缓存在内核</font>**<font style="color:rgb(44, 62, 80);">中，另一个进程读取数据时候自然也是从内核中获取，同时通信数据都遵循</font>**<font style="color:rgb(48, 79, 254);">先进先出</font>**<font style="color:rgb(44, 62, 80);">原则，不支持 lseek 之类的文件定位操作。</font>
+ **<font style="color:rgb(48, 79, 254);">消息队列</font>**<font style="color:rgb(44, 62, 80);">克服了管道通信的数据是无格式的字节流的问题，消息队列实际上是保存在内核的「消息链表」，消息队列的消息体是可以用户自定义的数据类型，发送数据时，会被分成一个一个独立的消息体，当然接收数据时，也要与发送方发送的消息体的数据类型保持一致，这样才能保证读取的数据是正确的。消息队列通信的速度不是最及时的，毕竟</font>**<font style="color:rgb(48, 79, 254);">每次数据的写入和读取都需要经过用户态与内核态之间的拷贝过程。</font>**
+ **<font style="color:rgb(48, 79, 254);">共享内存</font>**<font style="color:rgb(44, 62, 80);">可以解决消息队列通信中用户态与内核态之间数据拷贝过程带来的开销，</font>**<font style="color:rgb(48, 79, 254);">它直接分配一个共享空间，每个进程都可以直接访问</font>**<font style="color:rgb(44, 62, 80);">，就像访问进程自己的空间一样快捷方便，不需要陷入内核态或者系统调用，大大提高了通信的速度，享有</font>**<font style="color:rgb(48, 79, 254);">最快</font>**<font style="color:rgb(44, 62, 80);">的进程间通信方式之名。但是便捷高效的共享内存通信，</font>**<font style="color:rgb(48, 79, 254);">带来新的问题，多进程竞争同个共享资源会造成数据的错乱。</font>**
+ <font style="color:rgb(44, 62, 80);">那么，就需要</font>**<font style="color:rgb(48, 79, 254);">信号量</font>**<font style="color:rgb(44, 62, 80);">来保护共享资源，以确保任何时刻只能有一个进程访问共享资源，这种方式就是互斥访问。</font>**<font style="color:rgb(48, 79, 254);">信号量不仅可以实现访问的互斥性，还可以实现进程间的同步</font>**<font style="color:rgb(44, 62, 80);">，信号量其实是一个计数器，表示的是资源个数，其值可以通过两个原子操作来控制，分别是 </font>**<font style="color:rgb(48, 79, 254);">P 操作和 V 操作</font>**<font style="color:rgb(44, 62, 80);">。</font>
+ <font style="color:rgb(44, 62, 80);">与信号量名字很相似的叫</font>**<font style="color:rgb(48, 79, 254);">信号</font>**<font style="color:rgb(44, 62, 80);">，它俩名字虽然相似，但功能一点儿都不一样。信号是</font>**<font style="color:rgb(48, 79, 254);">异步通信机制</font>**<font style="color:rgb(44, 62, 80);">，信号可以在应用进程和内核之间直接交互，内核也可以利用信号来通知用户空间的进程发生了哪些系统事件，信号事件的来源主要有硬件来源（如键盘 Cltr+C ）和软件来源（如 kill 命令），一旦有信号发生，</font>**<font style="color:rgb(48, 79, 254);">进程有三种方式响应信号 1. 执行默认操作、2. 捕捉信号、3. 忽略信号</font>**<font style="color:rgb(44, 62, 80);">。有两个信号是应用进程无法捕捉和忽略的，即 </font><font style="color:rgb(71, 101, 130);">SIGKILL</font><font style="color:rgb(44, 62, 80);"> 和 </font><font style="color:rgb(71, 101, 130);">SIGSTOP</font><font style="color:rgb(44, 62, 80);">，这是为了方便我们能在任何时候结束或停止某个进程。</font>
+ <font style="color:rgb(44, 62, 80);">前面说到的通信机制，都是工作于同一台主机，如果</font>**<font style="color:rgb(48, 79, 254);">要与不同主机的进程间通信，那么就需要 Socket 通信了</font>**<font style="color:rgb(44, 62, 80);">。Socket 实际上不仅用于不同的主机进程间通信，还可以用于本地主机进程间通信，可根据创建 Socket 的类型不同，分为三种常见的通信方式，一个是基于 TCP 协议的通信方式，一个是基于 UDP 协议的通信方式，一个是本地进程间通信方式。</font>

<font style="color:rgb(44, 62, 80);">线程通信间的方式:</font>

<font style="color:rgb(44, 62, 80);">同个进程下的线程之间都是共享进程的资源，只要是共享变量都可以做到线程间通信，比如全局变量，所以对于线程间关注的不是通信方式，而是关注多线程竞争共享资源的问题，信号量也同样可以在线程间实现互斥与同步：</font>

+ <font style="color:rgb(44, 62, 80);">互斥的方式，可保证任意时刻只有一个线程访问共享资源；</font>
+ <font style="color:rgb(44, 62, 80);">同步的方式，可保证线程 A 应在线程 B 之前执行；</font>

### 网络IO模型: select poll、epoll 介绍、对比？(字节广告、得物、好未来)
+ **阻塞网络 I/O：**<font style="color:rgb(44, 62, 80);">最基础的 TCP 的 Socket 编程</font>**，只能一对一通信**
+ **多进程模型、多线程模型**
    - <font style="color:rgb(44, 62, 80);">每来一个客户端连接，就分配一个进程/线程，后续的读写都在对应的进程/线程，处理 100 个客户端没问题，但是当客户端增大到 10000 个时，10000 个进程/线程的调度、上下文切换以及它们占用的内存，都会成为瓶颈。</font>
+ **I/O 多路复用：**<font style="color:rgb(44, 62, 80);">可以在一个进程里处理多个文件的 I/O</font>
    - **select**
        * <font style="color:rgb(44, 62, 80);">select 使用固定长度的 BitsMap 表示文件描述符集合，而且所支持的文件描述符的个数是有限制的，在 Linux 系统中，由内核中的 FD_SETSIZE 限制， 默认最大值为 </font><font style="color:rgb(71, 101, 130);">1024</font><font style="color:rgb(44, 62, 80);">，只能监听 0~1023 的文件描述符。</font>
    - **poll**
        * <font style="color:rgb(44, 62, 80);">poll 不再用 BitsMap 来存储所关注的文件描述符，取而代之用动态数组，以链表形式来组织，突破了 select 的文件描述符个数限制，当然还会受到系统文件描述符限制。</font>
        * **<font style="color:rgb(48, 79, 254);">select 和 poll 都是使用「线性结构」存储进程关注的 Socket 集合，因此都需要遍历文件描述符集合来找到可读或可写的 Socket，时间复杂度为 O(n)，而且也需要在用户态与内核态之间拷贝文件描述符集合</font>**<font style="color:rgb(44, 62, 80);">，这种方式随着并发数上来，性能损耗会呈指数级增长。</font>
        * <font style="color:rgb(44, 62, 80);">在使用的时候，首先需要把关注的 Socket 集合通过 select/poll 系统调用从用户态拷贝到内核态，然后由内核检测事件，当有网络事件产生时，内核需要遍历进程关注 Socket 集合，找到对应的 Socket，并设置其状态为可读/可写，然后把整个 Socket 集合从内核态拷贝到用户态，用户态还要继续遍历整个 Socket 集合找到可读/可写的 Socket，然后对其处理。</font>
        * <font style="color:rgb(44, 62, 80);">select 和 poll 的缺陷在于，</font>**<font style="color:rgb(44, 62, 80);">当客户端越多，也就是 Socket 集合越大，Socket 集合的遍历和拷贝会带来很大的开销，因此也很难应对 C10K</font>**<font style="color:rgb(44, 62, 80);">。</font>
    - **epoll**
        * <font style="color:rgb(44, 62, 80);">epoll 在内核里使用「红黑树」来关注进程所有待检测的 Socket，红黑树是个高效的数据结构，增删改一般时间复杂度是 O(logn)，通过对这棵黑红树的管理，不需要像 select/poll 在每次操作时都传入整个 Socket 集合，减少了内核和用户空间大量的数据拷贝和内存分配。</font>
        * <font style="color:rgb(44, 62, 80);">epoll 使用事件驱动的机制，内核里维护了一个「链表」来记录就绪事件，只将有事件发生的 Socket 集合传递给应用程序，不需要像 select/poll 那样轮询扫描整个集合（包含有和无事件的 Socket ），大大提高了检测的效率。</font>
        * <font style="color:rgb(44, 62, 80);">epoll 支持</font>**<font style="color:rgb(44, 62, 80);">边缘触发</font>**<font style="color:rgb(44, 62, 80);">和</font>**<font style="color:rgb(44, 62, 80);">水平触发</font>**<font style="color:rgb(44, 62, 80);">的方式，而 select/poll 只支持水平触发，一般而言，边缘触发的方式会比水平触发的效率高</font>

#### 最基本的 Socket 模型
<font style="color:rgb(44, 62, 80);">要想客户端和服务器能在网络中通信，那必须得使用 Socket 编程，它是进程间通信里比较特别的方式，特别之处在于它是可以跨主机间通信。</font>

<font style="color:rgb(44, 62, 80);">Socket 的中文名叫作插口，咋一看还挺迷惑的。事实上，双方要进行网络通信前，各自得创建一个 Socket，这相当于客户端和服务器都开了一个“口子”，双方读取和发送数据的时候，都通过这个“口子”。这样一看，是不是觉得很像弄了一根网线，一头插在客户端，一头插在服务端，然后进行通信。</font>

<font style="color:rgb(44, 62, 80);">创建 Socket 的时候，可以指定网络层使用的是 IPv4 还是 IPv6，传输层使用的是 TCP 还是 UDP。</font>

<font style="color:rgb(44, 62, 80);">UDP 的 Socket 编程相对简单些，这里我们只介绍基于 TCP 的 Socket 编程。</font>

<font style="color:rgb(44, 62, 80);">服务器的程序要先跑起来，然后等待客户端的连接和数据，我们先来看看服务端的 Socket 编程过程是怎样的。</font>

<font style="color:rgb(44, 62, 80);">服务端首先调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">socket()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数，创建网络协议为 IPv4，以及传输协议为 TCP 的 Socket ，接着调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">bind()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数，给这个 Socket 绑定一个</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">IP 地址和端口</font>**<font style="color:rgb(44, 62, 80);">，绑定这两个的目的是什么？</font>

+ <font style="color:rgb(44, 62, 80);">绑定端口的目的：当内核收到 TCP 报文，通过 TCP 头里面的端口号，来找到我们的应用程序，然后把数据传递给我们。</font>
+ <font style="color:rgb(44, 62, 80);">绑定 IP 地址的目的：一台机器是可以有多个网卡的，每个网卡都有对应的 IP 地址，当绑定一个网卡时，内核在收到该网卡上的包，才会发给我们；</font>

<font style="color:rgb(44, 62, 80);">绑定完 IP 地址和端口后，就可以调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">listen()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数进行监听，此时对应 TCP 状态图中的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">listen</font><font style="color:rgb(44, 62, 80);">，如果我们要判定服务器中一个网络程序有没有启动，可以通过</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">netstat</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">命令查看对应的端口号是否有被监听。</font>

<font style="color:rgb(44, 62, 80);">服务端进入了监听状态后，通过调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">accept()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数，来从内核获取客户端的连接，如果没有客户端连接，则会阻塞等待客户端连接的到来。</font>

<font style="color:rgb(44, 62, 80);">那客户端是怎么发起连接的呢？客户端在创建好 Socket 后，调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">connect()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数发起连接，该函数的参数要指明服务端的 IP 地址和端口号，然后万众期待的 TCP 三次握手就开始了。</font>

<font style="color:rgb(44, 62, 80);">在 TCP 连接的过程中，服务器的内核实际上为每个 Socket 维护了两个队列：</font>

+ <font style="color:rgb(44, 62, 80);">一个是「还没完全建立」连接的队列，称为</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">TCP 半连接队列</font>**<font style="color:rgb(44, 62, 80);">，这个队列都是没有完成三次握手的连接，此时服务端处于</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">syn_rcvd</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">的状态；</font>
+ <font style="color:rgb(44, 62, 80);">一个是「已经建立」连接的队列，称为</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">TCP 全连接队列</font>**<font style="color:rgb(44, 62, 80);">，这个队列都是完成了三次握手的连接，此时服务端处于</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">established</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态；</font>

<font style="color:rgb(44, 62, 80);">当 TCP 全连接队列不为空后，服务端的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">accept()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数，就会从内核中的 TCP 全连接队列里拿出一个已经完成连接的 Socket 返回应用程序，后续数据传输都用这个 Socket。</font>

<font style="color:rgb(44, 62, 80);">注意，监听的 Socket 和真正用来传数据的 Socket 是两个：</font>

+ <font style="color:rgb(44, 62, 80);">一个叫作</font>**<font style="color:rgb(48, 79, 254);">监听 Socket</font>**<font style="color:rgb(44, 62, 80);"></font>
+ <font style="color:rgb(44, 62, 80);">一个叫作</font>**<font style="color:rgb(48, 79, 254);">已连接 Socket</font>**<font style="color:rgb(44, 62, 80);"></font>

<font style="color:rgb(44, 62, 80);">连接建立后，客户端和服务端就开始相互传输数据了，双方都可以通过</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">read()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">和</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">write()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数来读写数据。</font>

<font style="color:rgb(44, 62, 80);">至此， TCP 协议的 Socket 程序的调用过程就结束了，整个过程如下图：</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706437586133-e9b8cf47-068b-4367-8514-f27b0f9553a8.png)

<font style="color:rgb(44, 62, 80);">看到这，不知道你有没有觉得读写 Socket 的方式，好像读写文件一样。</font>

<font style="color:rgb(44, 62, 80);">是的，基于 Linux 一切皆文件的理念，在内核中 Socket 也是以「文件」的形式存在的，也是有对应的文件描述符。</font><font style="color:rgb(44, 62, 80);background-color:rgb(227, 242, 253);">  
</font><font style="color:rgb(44, 62, 80);">文件描述符的作用是什么？每一个进程都有一个数据结构 </font><font style="color:rgb(71, 101, 130);">task_struct</font><font style="color:rgb(44, 62, 80);">，该结构体里有一个指向「文件描述符数组」的成员指针。该数组里列出这个进程打开的所有文件的文件描述符。数组的下标是文件描述符，是一个整数，而数组的内容是一个指针，指向内核中所有打开的文件的列表，也就是说内核可以通过文件描述符找到对应打开的文件。</font>

<font style="color:rgb(44, 62, 80);">然后每个文件都有一个 inode，Socket 文件的 inode 指向了内核中的 Socket 结构，在这个结构体里有两个队列，分别是</font>**<font style="color:rgb(48, 79, 254);">发送队列</font>**<font style="color:rgb(44, 62, 80);">和</font>**<font style="color:rgb(48, 79, 254);">接收队列</font>**<font style="color:rgb(44, 62, 80);">，这个两个队列里面保存的是一个个</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">struct sk_buff</font><font style="color:rgb(44, 62, 80);">，用链表的组织形式串起来。</font>

<font style="color:rgb(44, 62, 80);">sk_buff 可以表示各个层的数据包，在应用层数据包叫 data，在 TCP 层我们称为 segment，在 IP 层我们叫 packet，在数据链路层称为 frame。</font>

<font style="color:rgb(44, 62, 80);">你可能会好奇，为什么全部数据包只用一个结构体来描述呢？协议栈采用的是分层结构，上层向下层传递数据时需要增加包头，下层向上层数据时又需要去掉包头，如果每一层都用一个结构体，那在层之间传递数据的时候，就要发生多次拷贝，这将大大降低 CPU 效率。</font>

<font style="color:rgb(44, 62, 80);">于是，为了在层级之间传递数据时，不发生拷贝，只用 sk_buff 一个结构体来描述所有的网络包，那它是如何做到的呢？是通过调整 sk_buff 中</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">data</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">的指针，比如：</font>

+ <font style="color:rgb(44, 62, 80);">当接收报文时，从网卡驱动开始，通过协议栈层层往上传送数据报，通过增加 skb->data 的值，来逐步剥离协议首部。</font>
+ <font style="color:rgb(44, 62, 80);">当要发送报文时，创建 sk_buff 结构体，数据缓存区的头部预留足够的空间，用来填充各层首部，在经过各下层协议时，通过减少 skb->data 的值来增加协议首部。</font>

<font style="color:rgb(44, 62, 80);">从下面这张图看到，当发送报文时 data 指针的移动过程。</font>

#### ![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706437634454-ab79c281-bd98-4d35-86c7-61a5197bbfba.png)<font style="color:rgb(44, 62, 80);background-color:rgb(227, 242, 253);">  
</font><font style="color:rgb(44, 62, 80);">如何服务更多的用户？</font>
<font style="color:rgb(44, 62, 80);">前面提到的 TCP Socket 调用流程是最简单、最基本的，它基本只能一对一通信，因为使用的是同步阻塞的方式，当服务端在还没处理完一个客户端的网络 I/O 时，或者读写操作发生阻塞时，其他客户端是无法与服务端连接的。</font>

<font style="color:rgb(44, 62, 80);">可如果我们服务器只能服务一个客户，那这样就太浪费资源了，于是我们要改进这个网络 I/O 模型，以支持更多的客户端。</font>

<font style="color:rgb(44, 62, 80);">在改进网络 I/O 模型前，我先来提一个问题，你知道服务器单机理论最大能连接多少个客户端？</font>

<font style="color:rgb(44, 62, 80);">相信你知道 TCP 连接是由四元组唯一确认的，这个四元组就是：</font>**<font style="color:rgb(48, 79, 254);">本机IP, 本机端口, 对端IP, 对端端口</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">服务器作为服务方，通常会在本地固定监听一个端口，等待客户端的连接。因此服务器的本地 IP 和端口是固定的，于是对于服务端 TCP 连接的四元组只有对端 IP 和端口是会变化的，所以</font>**<font style="color:rgb(48, 79, 254);">最大 TCP 连接数 = 客户端 IP 数×客户端端口数</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">对于 IPv4，客户端的 IP 数最多为 2 的 32 次方，客户端的端口数最多为 2 的 16 次方，也就是</font>**<font style="color:rgb(48, 79, 254);">服务端单机最大 TCP 连接数约为 2 的 48 次方</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">这个理论值相当“丰满”，但是服务器肯定承载不了那么大的连接数，主要会受两个方面的限制：</font>

+ **<font style="color:rgb(48, 79, 254);">文件描述符</font>**<font style="color:rgb(44, 62, 80);">，Socket 实际上是一个文件，也就会对应一个文件描述符。在 Linux 下，单个进程打开的文件描述符数是有限制的，没有经过修改的值一般都是 1024，不过我们可以通过 ulimit 增大文件描述符的数目；</font>
+ **<font style="color:rgb(48, 79, 254);">系统内存</font>**<font style="color:rgb(44, 62, 80);">，每个 TCP 连接在内核中都有对应的数据结构，意味着每个连接都是会占用一定内存的；</font>

<font style="color:rgb(44, 62, 80);">那如果服务器的内存只有 2 GB，网卡是千兆的，能支持并发 1 万请求吗？</font>

<font style="color:rgb(44, 62, 80);">并发 1 万请求，也就是经典的 C10K 问题 ，C 是 Client 单词首字母缩写，C10K 就是单机同时处理 1 万个请求的问题。</font>

<font style="color:rgb(44, 62, 80);">从硬件资源角度看，对于 2GB 内存千兆网卡的服务器，如果每个请求处理占用不到 200KB 的内存和 100Kbit 的网络带宽就可以满足并发 1 万个请求。</font>

<font style="color:rgb(44, 62, 80);">不过，要想真正实现 C10K 的服务器，要考虑的地方在于服务器的网络 I/O 模型，效率低的模型，会加重系统开销，从而会离 C10K 的目标越来越远。</font>

#### <font style="color:rgb(44, 62, 80);">多进程模型</font>
<font style="color:rgb(44, 62, 80);">基于最原始的阻塞网络 I/O， 如果服务器要支持多个客户端，其中比较传统的方式，就是使用</font>**<font style="color:rgb(48, 79, 254);">多进程模型</font>**<font style="color:rgb(44, 62, 80);">，也就是为每个客户端分配一个进程来处理请求。</font>

<font style="color:rgb(44, 62, 80);">服务器的主进程负责监听客户的连接，一旦与客户端连接完成，accept() 函数就会返回一个「已连接 Socket」，这时就通过</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">fork()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数创建一个子进程，实际上就把父进程所有相关的东西都</font>**<font style="color:rgb(48, 79, 254);">复制</font>**<font style="color:rgb(44, 62, 80);">一份，包括文件描述符、内存地址空间、程序计数器、执行的代码等。</font>

<font style="color:rgb(44, 62, 80);">这两个进程刚复制完的时候，几乎一模一样。不过，会根据</font>**<font style="color:rgb(48, 79, 254);">返回值</font>**<font style="color:rgb(44, 62, 80);">来区分是父进程还是子进程，如果返回值是 0，则是子进程；如果返回值是其他的整数，就是父进程。</font>

<font style="color:rgb(44, 62, 80);">正因为子进程会</font>**<font style="color:rgb(48, 79, 254);">复制父进程的文件描述符</font>**<font style="color:rgb(44, 62, 80);">，于是就可以直接使用「已连接 Socket 」和客户端通信了，</font>

<font style="color:rgb(44, 62, 80);">可以发现，子进程不需要关心「监听 Socket」，只需要关心「已连接 Socket」；父进程则相反，将客户服务交给子进程来处理，因此父进程不需要关心「已连接 Socket」，只需要关心「监听 Socket」。</font>

<font style="color:rgb(44, 62, 80);">下面这张图描述了从连接请求到连接建立，父进程创建生子进程为客户服务。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706437734110-c4611f70-5b06-4882-90e5-eeef61ee6a4b.png)

<font style="color:rgb(44, 62, 80);">另外，当「子进程」退出时，实际上内核里还会保留该进程的一些信息，也是会占用内存的，如果不做好“回收”工作，就会变成</font>**<font style="color:rgb(48, 79, 254);">僵尸进程</font>**<font style="color:rgb(44, 62, 80);">，随着僵尸进程越多，会慢慢耗尽我们的系统资源。</font>

<font style="color:rgb(44, 62, 80);">因此，父进程要“善后”好自己的孩子，怎么善后呢？那么有两种方式可以在子进程退出后回收资源，分别是调用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">wait()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">和</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">waitpid()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数。</font>

<font style="color:rgb(44, 62, 80);">这种用多个进程来应付多个客户端的方式，在应对 100 个客户端还是可行的，但是当客户端数量高达一万时，肯定扛不住的，因为每产生一个进程，必会占据一定的系统资源，而且进程间上下文切换的“包袱”是很重的，性能会大打折扣。</font>

<font style="color:rgb(44, 62, 80);">进程的上下文切换不仅包含了</font>**<font style="color:rgb(44, 62, 80);">虚拟内存、栈、全局变量</font>**<font style="color:rgb(44, 62, 80);">等用户空间的资源，还包括了</font>**<font style="color:rgb(44, 62, 80);">内核堆栈、寄存器</font>**<font style="color:rgb(44, 62, 80);">等内核空间的资源。</font>

#### 多线程模型
<font style="color:rgb(44, 62, 80);">既然进程间上下文切换的“包袱”很重，那我们就搞个比较轻量级的模型来应对多用户的请求 —— </font>**<font style="color:rgb(48, 79, 254);">多线程模型</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">线程是运行在进程中的一个“逻辑流”，单进程中可以运行多个线程，同进程里的线程可以共享进程的部分资源，比如文件描述符列表、进程空间、代码、全局数据、堆、共享库等，这些共享些资源在上下文切换时不需要切换，而只需要切换线程的私有数据、寄存器等不共享的数据，因此同一个进程下的线程上下文切换的开销要比进程小得多。</font>

<font style="color:rgb(44, 62, 80);">当服务器与客户端 TCP 完成连接后，通过</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">pthread_create()</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">函数创建线程，然后将「已连接 Socket」的文件描述符传递给线程函数，接着在线程里和客户端进行通信，从而达到并发处理的目的。</font>

<font style="color:rgb(44, 62, 80);">如果每来一个连接就创建一个线程，线程运行完后，还得操作系统还得销毁线程，虽说线程切换的上写文开销不大，但是如果频繁创建和销毁线程，系统开销也是不小的。</font>

<font style="color:rgb(44, 62, 80);">那么，我们可以使用</font>**<font style="color:rgb(48, 79, 254);">线程池</font>**<font style="color:rgb(44, 62, 80);">的方式来避免线程的频繁创建和销毁，所谓的线程池，就是提前创建若干个线程，这样当由新连接建立时，将这个已连接的 Socket 放入到一个队列里，然后线程池里的线程负责从队列中取出「已连接 Socket 」进行处理。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706437791422-0c802ab6-6b28-4ece-9078-7cb8684eaf8e.png)  
<font style="color:rgb(44, 62, 80);">需要注意的是，这个队列是全局的，每个线程都会操作，为了避免多线程竞争，线程在操作这个队列前要加锁。</font>

<font style="color:rgb(44, 62, 80);">上面基于进程或者线程模型的，其实还是有问题的。新到来一个 TCP 连接，就需要分配一个进程或者线程，那么如果要达到 C10K，意味着要一台机器维护 1 万个连接，相当于要维护 1 万个进程/线程，操作系统就算死扛也是扛不住的。</font>

#### <font style="color:rgb(44, 62, 80);">I/O 多路复用</font>
<font style="color:rgb(44, 62, 80);">既然为每个请求分配一个进程/线程的方式不合适，那有没有可能只使用一个进程来维护多个 Socket 呢？答案是有的，那就是 </font>**<font style="color:rgb(48, 79, 254);">I/O 多路复用</font>**<font style="color:rgb(44, 62, 80);">技术。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706437861366-b516a8e8-6aba-466f-ac7e-5e0d2a0138df.png)

<font style="color:rgb(44, 62, 80);">一个进程虽然任一时刻只能处理一个请求，但是处理每个请求的事件时，耗时控制在 1 毫秒以内，这样 1 秒内就可以处理上千个请求，把时间拉长来看，多个请求复用了一个进程，这就是多路复用，这种思想很类似一个 CPU 并发多个进程，所以也叫做时分多路复用。</font>

<font style="color:rgb(44, 62, 80);">我们熟悉的 select/poll/epoll 内核提供给用户态的多路复用系统调用，</font>**<font style="color:rgb(48, 79, 254);">进程可以通过一个系统调用函数从内核中获取多个事件</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">select/poll/epoll 是如何获取网络事件的呢？在获取事件时，先把所有连接（文件描述符）传给内核，再由内核返回产生了事件的连接，然后在用户态中再处理这些连接对应的请求即可。</font>

<font style="color:rgb(44, 62, 80);">select/poll/epoll 这是三个多路复用接口，都能实现 C10K 吗？接下来，我们分别说说它们。</font>

#### select / poll
<font style="color:rgb(44, 62, 80);">select 实现多路复用的方式是，将已连接的 Socket 都放到一个</font>**<font style="color:rgb(48, 79, 254);">文件描述符集合</font>**<font style="color:rgb(44, 62, 80);">，然后调用 select 函数将文件描述符集合</font>**<font style="color:rgb(48, 79, 254);">拷贝</font>**<font style="color:rgb(44, 62, 80);">到内核里，让内核来检查是否有网络事件产生，检查的方式很粗暴，就是通过</font>**<font style="color:rgb(48, 79, 254);">遍历</font>**<font style="color:rgb(44, 62, 80);">文件描述符集合的方式，当检查到有事件产生后，将此 Socket 标记为可读或可写， 接着再把整个文件描述符集合</font>**<font style="color:rgb(48, 79, 254);">拷贝</font>**<font style="color:rgb(44, 62, 80);">回用户态里，然后用户态还需要再通过</font>**<font style="color:rgb(48, 79, 254);">遍历</font>**<font style="color:rgb(44, 62, 80);">的方法找到可读或可写的 Socket，然后再对其处理。</font>

<font style="color:rgb(44, 62, 80);">所以，对于 select 这种方式，需要进行</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">2 次「遍历」文件描述符集合</font>**<font style="color:rgb(44, 62, 80);">，一次是在内核态里，一个次是在用户态里 ，而且还会发生</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">2 次「拷贝」文件描述符集合</font>**<font style="color:rgb(44, 62, 80);">，先从用户空间传入内核空间，由内核修改后，再传出到用户空间中。</font>

<font style="color:rgb(44, 62, 80);">select 使用固定长度的 BitsMap，表示文件描述符集合，而且所支持的文件描述符的个数是有限制的，在 Linux 系统中，由内核中的 FD_SETSIZE 限制， 默认最大值为</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">1024</font><font style="color:rgb(44, 62, 80);">，只能监听 0~1023 的文件描述符。</font>

<font style="color:rgb(44, 62, 80);">poll 不再用 BitsMap 来存储所关注的文件描述符，取而代之用动态数组，以链表形式来组织，突破了 select 的文件描述符个数限制，当然还会受到系统文件描述符限制。</font>

<font style="color:rgb(44, 62, 80);">但是 poll 和 select 并没有太大的本质区别，</font>**<font style="color:rgb(48, 79, 254);">都是使用「线性结构」存储进程关注的 Socket 集合，因此都需要遍历文件描述符集合来找到可读或可写的 Socket，时间复杂度为 O(n)，而且也需要在用户态与内核态之间拷贝文件描述符集合</font>**<font style="color:rgb(44, 62, 80);">，这种方式随着并发数上来，性能的损耗会呈指数级增长。</font>

#### <font style="color:rgb(44, 62, 80);">epoll</font>
<font style="color:rgb(44, 62, 80);">先复习下 epoll 的用法。如下的代码中，先用epoll_create 创建一个 epoll对象 epfd，再通过 epoll_ctl 将需要监视的 socket 添加到epfd中，最后调用 epoll_wait 等待数据。</font>

```c
int s = socket(AF_INET, SOCK_STREAM, 0);
bind(s, ...);
listen(s, ...)

int epfd = epoll_create(...);
epoll_ctl(epfd, ...); //将所有需要监听的socket添加到epfd中

while(1) {
    int n = epoll_wait(...);
    for(接收到数据的socket){
        //处理
    }
}
```

<font style="color:rgb(44, 62, 80);">epoll 通过两个方面，很好解决了 select/poll 的问题。</font>

1. <font style="color:rgb(44, 62, 80);">epoll 在内核里使用</font>**<font style="color:rgb(48, 79, 254);">红黑树来跟踪进程所有待检测的文件描述字</font>**<font style="color:rgb(44, 62, 80);">，把需要监控的 socket 通过 </font><font style="color:rgb(71, 101, 130);">epoll_ctl()</font><font style="color:rgb(44, 62, 80);"> 函数加入内核中的红黑树里，红黑树是个高效的数据结构，增删改一般时间复杂度是 </font><font style="color:rgb(71, 101, 130);">O(logn)</font><font style="color:rgb(44, 62, 80);">。而 select/poll 内核里没有类似 epoll 红黑树这种保存所有待检测的 socket 的数据结构，所以 select/poll 每次操作时都传入整个 socket 集合给内核，而 epoll 因为在内核维护了红黑树，可以保存所有待检测的 socket ，所以只需要传入一个待检测的 socket，减少了内核和用户空间大量的数据拷贝和内存分配。</font>
2. <font style="color:rgb(44, 62, 80);">epoll 使用</font>**<font style="color:rgb(48, 79, 254);">事件驱动</font>**<font style="color:rgb(44, 62, 80);">的机制，内核里</font>**<font style="color:rgb(48, 79, 254);">维护了一个链表来记录就绪事件</font>**<font style="color:rgb(44, 62, 80);">，当某个 socket 有事件发生时，通过</font>**<font style="color:rgb(48, 79, 254);">回调函数</font>**<font style="color:rgb(44, 62, 80);">内核会将其加入到这个就绪事件列表中，当用户调用 </font><font style="color:rgb(71, 101, 130);">epoll_wait()</font><font style="color:rgb(44, 62, 80);"> 函数时，只会返回有事件发生的文件描述符的个数，不需要像 select/poll 那样轮询扫描整个 socket 集合，大大提高了检测的效率。</font>

<font style="color:rgb(44, 62, 80);">从下图可以看到 epoll 相关的接口作用：</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706438066348-a94d03d6-f56a-4672-8483-dfa3c8df6cd3.png)  
<font style="color:rgb(44, 62, 80);">epoll 的方式即使监听的 Socket 数量越多的时候，效率不会大幅度降低，能够同时监听的 Socket 的数目也非常的多了，上限就为系统定义的进程打开的最大文件描述符个数。因而，</font>**<font style="color:rgb(48, 79, 254);">epoll 被称为解决 C10K 问题的利器</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">插个题外话，网上文章不少说，</font><font style="color:rgb(71, 101, 130);">epoll_wait</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">返回时，对于就绪的事件，epoll 使用的是共享内存的方式，即用户态和内核态都指向了就绪链表，所以就避免了内存拷贝消耗。</font>

<font style="color:rgb(44, 62, 80);">这是错的！看过 epoll 内核源码的都知道，</font>**<font style="color:rgb(48, 79, 254);">压根就没有使用共享内存这个玩意</font>**<font style="color:rgb(44, 62, 80);">。你可以从下面这份代码看到， epoll_wait 实现的内核代码中调用了 </font><font style="color:rgb(71, 101, 130);">__put_user</font><font style="color:rgb(44, 62, 80);"> 函数，这个函数就是将数据从内核拷贝到用户空间。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706438036895-c938100c-01bd-4da9-8923-ec5845d195d2.png)  
<font style="color:rgb(44, 62, 80);">epoll 支持两种事件触发模式，分别是</font>**<font style="color:rgb(48, 79, 254);">边缘触发（</font>**_**<font style="color:rgb(200, 73, 255);">edge-triggered，ET</font>**_**<font style="color:rgb(48, 79, 254);">）和水平触发（</font>**_**<font style="color:rgb(200, 73, 255);">level-triggered，LT</font>**_**<font style="color:rgb(48, 79, 254);">）</font>**<font style="color:rgb(44, 62, 80);">。</font>

+ <font style="color:rgb(44, 62, 80);">边缘触发模式：当被监控的 Socket 描述符上有可读事件发生时，</font>**<font style="color:rgb(48, 79, 254);">服务器端只会从 epoll_wait 中苏醒一次</font>**<font style="color:rgb(44, 62, 80);">，即使进程没有调用 read 函数从内核读取数据，也依然只苏醒一次，因此我们程序要保证一次性将内核缓冲区的数据读取完；</font>
+ <font style="color:rgb(44, 62, 80);">水平触发模式：当被监控的 Socket 上有可读事件发生时，</font>**<font style="color:rgb(48, 79, 254);">服务器端不断地从 epoll_wait 中苏醒，直到内核缓冲区数据被 read 函数读完才结束</font>**<font style="color:rgb(44, 62, 80);">，目的是告诉我们有数据需要读取；</font>

<font style="color:rgb(44, 62, 80);">举个例子，你的快递被放到了一个快递箱里，如果快递箱只会通过短信通知你一次，即使你一直没有去取，它也不会再发送第二条短信提醒你，这个方式就是边缘触发；如果快递箱发现你的快递没有被取出，它就会不停地发短信通知你，直到你取出了快递，它才消停，这个就是水平触发的方式。</font>

<font style="color:rgb(44, 62, 80);">这就是两者的区别，</font>**<font style="color:rgb(44, 62, 80);">水平触发的意思是只要满足事件的条件，比如内核中有数据需要读，就一直不断地把这个事件传递给用户；而边缘触发的意思是只有第一次满足条件的时候才触发，之后就不会再传递同样的事件了。</font>**

<font style="color:rgb(44, 62, 80);">如果使用水平触发模式，当内核通知文件描述符可读写时，接下来还可以继续去检测它的状态，看它是否依然可读或可写。所以在收到通知后，没必要一次执行尽可能多的读写操作。</font>

<font style="color:rgb(44, 62, 80);">如果使用边缘触发模式，I/O 事件发生时只会通知一次，而且我们不知道到底能读写多少数据，所以在收到通知后应尽可能地读写数据，以免错失读写的机会。因此，我们会</font>**<font style="color:rgb(48, 79, 254);">循环</font>**<font style="color:rgb(44, 62, 80);">从文件描述符读写数据，那么如果文件描述符是阻塞的，没有数据可读写时，进程会阻塞在读写函数那里，程序就没办法继续往下执行。所以，</font>**<font style="color:rgb(48, 79, 254);">边缘触发模式一般和非阻塞 I/O 搭配使用</font>**<font style="color:rgb(44, 62, 80);">，程序会一直执行 I/O 操作，直到系统调用（如</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">read</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">和</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">write</font><font style="color:rgb(44, 62, 80);">）返回错误，错误类型为</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">EAGAIN</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">或</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">EWOULDBLOCK</font><font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">一般来说，边缘触发的效率比水平触发的效率要高，因为边缘触发可以减少 epoll_wait 的系统调用次数，系统调用也是有一定的开销的的，毕竟也存在上下文的切换。</font>

**<font style="color:rgb(44, 62, 80);">select/poll 只有水平触发模式，epoll 默认的触发模式是水平触发，但是可以根据应用场景设置为边缘触发模式。</font>**

<font style="color:rgb(44, 62, 80);">另外，使用 I/O 多路复用时，最好搭配非阻塞 I/O 一起使用，Linux 手册关于 select 的内容中有如下说明：</font>

> <font style="color:rgb(44, 62, 80);">Under Linux, select() may report a socket file descriptor as "ready for reading", while nevertheless a subsequent read blocks. This could for example happen when data has arrived but upon examination has wrong checksum and is discarded. There may be other circumstances in which a file descriptor is spuriously reported as ready. Thus it may be safer to use O_NONBLOCK on sockets that should not block.</font>
>

翻译:

> <font style="color:rgb(44, 62, 80);">在Linux下，select() 可能会将一个 socket 文件描述符报告为 "准备读取"，而后续的读取块却没有。例如，当数据已经到达，但经检查后发现有错误的校验和而被丢弃时，就会发生这种情况。也有可能在其他情况下，文件描述符被错误地报告为就绪。因此，在不应该阻塞的 socket 上使用 O_NONBLOCK 可能更安全。</font>
>

<font style="color:rgb(44, 62, 80);">简单点理解，就是</font>**<font style="color:rgb(48, 79, 254);">多路复用 API 返回的事件并不一定可读写的</font>**<font style="color:rgb(44, 62, 80);">，如果使用阻塞 I/O， 那么在调用 read/write 时则会发生程序阻塞，因此最好搭配非阻塞 I/O，以便应对极少数的特殊情况。</font>

### 对磁盘结构了解吗？做对象存储需要了解存储的基本结构？机械磁盘的常见结构？读写请求到磁盘控制器，会做哪些事情？
机械磁盘主要组件构成：

1. **盘片（Platters）：** 机械磁盘内部有一个或多个盘片，通常由金属或玻璃制成，涂有磁性材料。数据被存储在盘片的表面上，通过磁场的变化来表示数据的 0 和 1。
2. **磁头（Read/Write Heads）：** 磁头是用于读取和写入数据的设备，位于盘片的顶部和底部。每个盘片都有一个或多个磁头，它们可以在盘片的表面上移动，读取和写入数据。
3. **磁道（Tracks）：** 盘片表面被划分为一系列同心圆，称为磁道。每个磁道上可以存储一定量的数据，磁头可以沿着磁道移动，从而读取或写入数据。
4. **扇区（Sectors）：** 每个磁道被划分为若干个扇区，每个扇区可以存储固定大小的数据块。扇区是磁盘的最小数据单元，通常大小为 512 字节或 4KB。

读写请求到磁盘控制器时，会经历以下几个步骤：

1. **请求调度（Request Scheduling）：** 磁盘控制器接收到读写请求后，会对请求进行调度，决定以什么顺序访问磁盘上的数据。请求调度算法的目标是尽量减少磁头的移动和等待时间，从而提高磁盘的访问性能。
2. **寻道（Seeking）：** 磁盘控制器根据请求调度的结果，将磁头移动到需要访问的磁道上。这个过程称为寻道操作，它会消耗一定的时间，取决于磁头的移动距离和磁盘的转速。
3. **旋转（Rotating）：** 磁盘控制器等待磁盘旋转到需要访问的扇区位置。一旦磁盘旋转到目标位置，磁头就可以开始读取或写入数据了。
4. **数据传输（Data Transfer）：** 磁盘控制器通过磁头从磁盘上读取或写入数据。读取数据时，磁盘控制器将数据传输到内存中；写入数据时，磁盘控制器将数据写入到磁盘上的相应扇区。
5. **完成请求（Completion）：** 一旦数据传输完成，磁盘控制器将完成请求，并通知请求的发起者。完成请求后，磁盘控制器可以处理下一个请求。

这些步骤中的每一个都会影响磁盘的访问性能和延迟。优化这些步骤，尤其是减少寻道和旋转延迟，是提高磁盘性能的关键。

# 网络
## 一个服务端进程最多能支持多少条 TCP 连接？
> **<font style="color:rgb(74, 74, 74);">如果在不考虑服务器的内存和文件句柄资源的情况下，理论上一个服务端进程最多能支持约为 </font>****<font style="color:rgb(100, 149, 237);">2</font>****<font style="color:rgb(74, 74, 74);"> 的 </font>****<font style="color:rgb(100, 149, 237);">48</font>****<font style="color:rgb(74, 74, 74);"> 次方（</font>****<font style="color:rgb(100, 149, 237);">2^32 (ip数) * 2^16 (端口数</font>****<font style="color:rgb(74, 74, 74);">），约等于两百多万亿！</font>**
>
> **<font style="color:rgb(74, 74, 74);">但是在实际中是支持不了这个数值的，每个 TCP 连接都是一个文件，会占用文件句柄资源，也会占用一定的内存空间。</font>**
>

TCP 连接本质上在内核里就是一个 socket 对象

```c
struct socket {  
    ....
    //INET域专用的一个socket表示, 提供了INET域专有的一些属性，比如 IP地址，端口等
    struct sock             *sk;  
    //TCP连接的状态：SYN_SENT、SYN_RECV、ESTABLISHED.....
    short                   type;  
    ....
};  

struct inet_sock {  
...
  __u32    daddr;   //IPv4的目标地址。  
  __u16    dport;   //目标端口。   
  __u32    saddr;   //源地址。  
  __u16    sport;   //源端口。  
...
};  

```

socket 对象也就是一个数据结构，里面包含了 TCP 四元组的信息：源IP、源端口、目标IP、目标端口。

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706447999961-ddf4379f-8c3a-4f4c-85e0-64ad1347beb9.png)

所以， 只要确认了【源IP、源端口、目标IP、目标端口】这四个信息，就能在内核中找到这个 socket 对象，也就能确定一条 TCP 连接。

一个服务端进程通常是监听 1 个端口号（当然也可能监听多个端口号，这里不考虑），例如 nginx 服务，就监听了 443 端口。

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706448032261-74cc6f6c-a08d-43ec-ad91-95d32990fd2d.png)

然后，服务端进程除了会固定监听某个一个端口之外，也通常会绑定 0.0.0.0 IP 地址。

这个IP地址是特殊的， 0.0.0.0 指的是本机上的所有IPV4地址，如果一个主机有两个 IP 地址，192.168.1.1 和 10.1.2.1，并且该主机上的一个服务监听的地址是0.0.0.0，那么通过两个 IP 地址都能够访问该服务。

所以一个服务端进程，意味着他的 IP地址和端口号是固定的（0.0.0.0:443）。

也就是当客户端与服务端建立一条 TCP 连接的时候，这个 TCP 连接的四元组信息中服务端的 IP地址和端口号是固定的，能产生变化的就是客户端的 IP 地址和端口号了。

因此，一个服务端进程最大能支持的 TCP 连接个数的计算公式如下：

> **最大TCP连接数 = 客户端 IP 数 * 客户端的端口数**
>

对 IPv4，客户端的 IP 数最多为 2 的 32 次方，客户端的端口数最多为 2 的 16 次方。

那么一个服务端进程理想情况下，最大的 TCP 连接数约为 2 的 48 次方（2^32 (ip数) * 2^16 (端口数），这数值是非常夸张的了，约等于两百多万亿！

当然，服务端进程最大能支持的 TCP 连接数远不能达到理论上限，还会受到**文件描述符、内存大小资源的限制**，毕竟 socket 在 Linux 的视角其实就是文件资源，而且一个 socket 对象也会占用一定的内存资源。

因此，会受以下因素影响：

+ 文件描述符限制，每个 TCP 连接都是一个文件，如果文件描述符被占满了，会发生 Too many open files。Linux 对可打开的文件描述符的数量分别作了三个方面的限制：
    - **系统级**：当前系统可打开的最大数量，通过 **cat /proc/sys/fs/file-max** 查看；
    - **用户级**：指定用户可打开的最大数量，通过 **cat /etc/security/limits.conf** 查看；
    - **进程级**：单个进程可打开的最大数量，通过 **cat /proc/sys/fs/nr_open** 查看；
+ **内存限制**，每个 TCP 连接都要占用一定内存，操作系统的内存是有限的，如果内存资源被占满后，会发生 OOM。

## 一台服务器最大最多能支持多少条 TCP 连接？
> <font style="color:rgb(74, 74, 74);">一台服务器是可以有多个服务端进程的，每个服务端进程监听不同的端口，当然所有65535个端口你都可以用来监听一遍。</font>
>
> <font style="color:rgb(74, 74, 74);">当然所有65535个端口你都可以用来监听一遍，这样理论上线就到了2的32次方（ip数）×2的16次方（port数）×2的16次方（服务器port数）个，这个基本相当于无穷个了。</font>
>
> <font style="color:rgb(74, 74, 74);">但是 Linux每维护一条TCP连接都要花费内存资源的，每一条静止状态（不发送数据和不接收数据）的 TCP 连接大约需要吃 3.44K 的内存，那么 8 GB 物理内存的服务器，最大能支持的 TCP 连接数=8GB/3.44KB=2,438,956（约240万）。</font>
>
> <font style="color:rgb(74, 74, 74);">实际过程中的 TCP 连接，还会进行发送数据和接收数据了，那么这些过程还是会额外消耗更多的内存资源的，并发很难达到百万级别。</font>
>

<font style="color:rgb(74, 74, 74);">前面分析是一个服务端进程的情况，理论上能最大支持约为 </font><font style="color:rgb(100, 149, 237);">2</font><font style="color:rgb(74, 74, 74);"> 的 </font><font style="color:rgb(100, 149, 237);">48</font><font style="color:rgb(74, 74, 74);"> 次方（</font><font style="color:rgb(100, 149, 237);">2^32 (ip数) * 2^16 (端口数</font><font style="color:rgb(74, 74, 74);">），约等于两百多万亿！</font>

<font style="color:rgb(74, 74, 74);">那到了一台服务器的视角就会有一点不一样。</font>

<font style="color:rgb(74, 74, 74);">一台服务器是可以有多个服务端进程的，每个服务端进程监听不同的端口，比如：ssh的22，Redis的6339，当然所有65535个端口你都可以用来监听一遍。</font>

```shell
[root@k8s ~]# netstat -natp | grep 0.0.0.0
tcp        0      0 169.254.25.10:9254      0.0.0.0:*               LISTEN      28580/node-cache
tcp        0      0 127.0.0.1:10248         0.0.0.0:*               LISTEN      726/kubelet
tcp        0      0 127.0.0.1:10249         0.0.0.0:*               LISTEN      10467/kube-proxy
tcp        0      0 127.0.0.1:9099          0.0.0.0:*               LISTEN      12253/calico-node
tcp        0      0 127.0.0.1:2379          0.0.0.0:*               LISTEN      1336/etcd
tcp        0      0 10.0.4.2:2379           0.0.0.0:*               LISTEN      1336/etcd
tcp        0      0 10.0.4.2:9100           0.0.0.0:*               LISTEN      10986/kube-rbac-pro
tcp        0      0 127.0.0.1:9100          0.0.0.0:*               LISTEN      10858/node_exporter
tcp        0      0 10.0.4.2:2380           0.0.0.0:*               LISTEN      1336/etcd
tcp        0      0 0.0.0.0:30001           0.0.0.0:*               LISTEN      4264/python
tcp        0      0 169.254.25.10:53        0.0.0.0:*               LISTEN      28580/node-cache
tcp        0      0 127.0.0.1:45653         0.0.0.0:*               LISTEN      726/kubelet
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1646/sshd
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1927/master
```

<font style="color:rgb(74, 74, 74);">当然所有65535个端口你都可以用来监听一遍，这样理论上限就到了</font>

`<font style="color:rgb(74, 74, 74);">2的32次方（ip数）×2的16次方（port数）×2的16次方（服务器port数）个</font>`

<font style="color:rgb(74, 74, 74);">感兴趣你可以算一下，这个基本相当于无穷个了。</font>

<font style="color:rgb(74, 74, 74);">不过理想和实际总是会有差距的！</font>

<font style="color:rgb(74, 74, 74);">因为Linux每维护一条TCP连接都要花费资源，处理连接请求，保活，数据的收发时需要消耗一些CPU，维持TCP连接主要消耗内存。</font>

<font style="color:rgb(74, 74, 74);">我们题目的问题是考虑最大多少个连接，所以我们先不考虑数据的收发，那么TCP在静止的状态下，就不怎么消耗 CPU了，主要消耗内存，而Linux上内存是有限的。</font>

<font style="color:rgb(74, 74, 74);">首先，我们要知道一条处于 ESTABLISH 状态的 TCP 连接具体占用多大内存？</font>

<font style="color:rgb(74, 74, 74);">一个 TCP 对象占用的大小，等于它所包含的一些数据结构占用大小的总和，也是就把上面这些数据结构的大小累加起来，就是一个 TCP 连接占用的大小了。</font>

<font style="color:rgb(74, 74, 74);">这里直接给大家一个结论，</font>**<font style="color:rgb(48, 79, 254);">一条处于 ESTABLISH 状态的 TCP 连接占用的大小是 3.44 KB</font>**<font style="color:rgb(74, 74, 74);">（0.81K+2.19K+0.19K+0.25K）。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706448588326-1af9ce0a-a19a-4d7f-a59b-ce5c7095d332.png)

<font style="color:rgb(74, 74, 74);">也就是，每一条静止状态的 TCP 连接大约需要吃 3.44K 的内存。</font>

<font style="color:rgb(74, 74, 74);">那么 </font>**<font style="color:rgb(48, 79, 254);">8 GB 物理内存的服务器，最大能支持的 TCP 连接数= 8GB/3.44 KB=2,438,956（约240万）</font>**<font style="color:rgb(74, 74, 74);">！</font>

<font style="color:rgb(74, 74, 74);">当然， 实际过程中的 TCP 连接，肯定不是静止状态的，还会进行发送数据和接收数据了，那么这些过程还是会额外消耗更多的内存资源的，并发很难达到百万级别。</font>

## 浏览器输入<font style="color:rgb(44, 62, 80);">网址到网页显示，期间发生了什么？</font>
+ HTTP URL 解析
+ DNS 域名解析
+ TCP 连接
+ IP 报文头部添加
+ MAC 报文头部添加
+ 网卡发送数据
+ 交换机转发
+ 路由器转发
+ 协议转换、解包
+ 前端渲染

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706683945231-2b6aca5b-76be-4932-8251-e5982ac4be5e.png)

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706693184184-7dad7f37-a612-43dd-b5fa-e83d2e239b85.png)

#### HTTP URL 解析
<font style="color:rgb(44, 62, 80);">浏览器做的第一步工作就是要对 </font><font style="color:rgb(71, 101, 130);">URL</font><font style="color:rgb(44, 62, 80);"> 进行解析，生成发送给 </font><font style="color:rgb(71, 101, 130);">Web</font><font style="color:rgb(44, 62, 80);"> 服务器的请求信息。</font>

<font style="color:rgb(44, 62, 80);">一条长长的 URL 里的各个元素的代表什么，见下图：</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706683983367-0a386699-7ce0-4303-9d8b-689654b5e5ae.png)

<font style="color:rgb(44, 62, 80);">URL 实际上是请求服务器里的文件资源，当蓝色部分 URL 元素都省略了，没有路径名时，就代表访问根目录下事先设置的</font>**<font style="color:rgb(48, 79, 254);">默认文件</font>**<font style="color:rgb(44, 62, 80);">，也就是 </font><font style="color:rgb(71, 101, 130);">/index.html</font><font style="color:rgb(44, 62, 80);"> 或者 </font><font style="color:rgb(71, 101, 130);">/default.html</font><font style="color:rgb(44, 62, 80);"> 这些文件，这样就不会发生混乱了。</font>

<font style="color:rgb(44, 62, 80);">对 </font><font style="color:rgb(71, 101, 130);">URL</font><font style="color:rgb(44, 62, 80);"> 进行解析之后，浏览器确定了 Web 服务器和文件名，接下来就是根据这些信息来生成 HTTP 请求消息了。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706684122267-0a9ed768-69ab-4a4d-a9c3-8e3b2fe623ba.png)

#### DNS 域名解析
<font style="color:rgb(44, 62, 80);">浏览器解析 URL 并生成 HTTP 消息后，需要委托操作系统将消息发送给 </font><font style="color:rgb(71, 101, 130);">Web</font><font style="color:rgb(44, 62, 80);"> 服务器。</font>

<font style="color:rgb(44, 62, 80);">但在发送之前，还有一项工作需要完成，那就是</font>**<font style="color:rgb(48, 79, 254);">查询服务器域名对应的 IP 地址</font>**<font style="color:rgb(44, 62, 80);">，因为委托操作系统发送消息时，必须提供通信对象的 IP 地址。</font>

<font style="color:rgb(44, 62, 80);">比如我们打电话的时候，必须要知道对方的电话号码，但由于电话号码难以记忆，所以通常我们会将对方电话号 + 姓名保存在通讯录里。</font>

<font style="color:rgb(44, 62, 80);">所以，有一种服务器就专门保存了 </font><font style="color:rgb(71, 101, 130);">Web</font><font style="color:rgb(44, 62, 80);"> 服务器域名与 </font><font style="color:rgb(71, 101, 130);">IP</font><font style="color:rgb(44, 62, 80);"> 的对应关系，它就是 </font>**<font style="color:rgb(71, 101, 130);">DNS</font>****<font style="color:rgb(44, 62, 80);"> 服务器</font>**<font style="color:rgb(44, 62, 80);">。</font>

> <font style="color:rgb(44, 62, 80);">域名的层级关系</font>
>

<font style="color:rgb(44, 62, 80);">DNS 中的域名都是用</font>**<font style="color:rgb(48, 79, 254);">句点</font>**<font style="color:rgb(44, 62, 80);">来分隔的，比如</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">www.server.com</font><font style="color:rgb(44, 62, 80);">，这里的句点代表了不同层次之间的</font>**<font style="color:rgb(48, 79, 254);">界限</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">在域名中，</font>**<font style="color:rgb(48, 79, 254);">越靠右</font>**<font style="color:rgb(44, 62, 80);">的位置表示其层级</font>**<font style="color:rgb(48, 79, 254);">越高</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">实际上域名最后还有一个点，比如</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">www.server.com.</font><font style="color:rgb(44, 62, 80);">，这个最后的一个点代表根域名。</font>

<font style="color:rgb(44, 62, 80);">也就是，</font><font style="color:rgb(71, 101, 130);">.</font><font style="color:rgb(44, 62, 80);">根域是在最顶层，它的下一层就是 </font><font style="color:rgb(71, 101, 130);">.com</font><font style="color:rgb(44, 62, 80);"> 顶级域，再下面是 </font><font style="color:rgb(71, 101, 130);">server.com</font><font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">所以域名的层级关系类似一个树状结构：</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706684417184-5576ae0a-4366-4247-affa-925bbeb678bd.png)

<font style="color:rgb(44, 62, 80);">根域的 DNS 服务器信息保存在互联网中所有的 DNS 服务器中。</font>

<font style="color:rgb(44, 62, 80);">这样一来，任何 DNS 服务器就都可以找到并访问根域 DNS 服务器了。</font>

<font style="color:rgb(44, 62, 80);">因此，客户端只要能够找到任意一台 DNS 服务器，就可以通过它找到根域 DNS 服务器，然后再一路顺藤摸瓜找到位于下层的某台目标 DNS 服务器。</font>

##### <font style="color:rgb(44, 62, 80);">域名解析过程</font>
1. <font style="color:rgb(44, 62, 80);">客户端首先会发出一个 DNS 请求，问 www.server.com 的 IP 是啥，并发给本地 DNS 服务器（也就是客户端的 TCP/IP 设置中填写的 DNS 服务器地址）。</font>
2. <font style="color:rgb(44, 62, 80);">本地域名服务器收到客户端的请求后，如果缓存里的表格能找到 www.server.com，则它直接返回 IP 地址。如果没有，本地 DNS 会去问它的根域名服务器：“老大， 能告诉我 www.server.com 的 IP 地址吗？” 根域名服务器是最高层次的，它不直接用于域名解析，但能指明一条道路。</font>
3. <font style="color:rgb(44, 62, 80);">根 DNS 收到来自本地 DNS 的请求后，发现后置是 .com，说：“www.server.com 这个域名归 .com 区域管理”，我给你 .com 顶级域名服务器地址给你，你去问问它吧。”</font>
4. <font style="color:rgb(44, 62, 80);">本地 DNS 收到顶级域名服务器的地址后，发起请求问“老二， 你能告诉我 www.server.com 的 IP 地址吗？”</font>
5. <font style="color:rgb(44, 62, 80);">顶级域名服务器说：“我给你负责 www.server.com 区域的权威 DNS 服务器的地址，你去问它应该能问到”。</font>
6. <font style="color:rgb(44, 62, 80);">本地 DNS 于是转向问权威 DNS 服务器：“老三，www.server.com对应的IP是啥呀？” server.com 的权威 DNS 服务器，它是域名解析结果的原出处。为啥叫权威呢？就是我的域名我做主。</font>
7. <font style="color:rgb(44, 62, 80);">权威 DNS 服务器查询后将对应的 IP 地址 X.X.X.X 告诉本地 DNS。</font>
8. <font style="color:rgb(44, 62, 80);">本地 DNS 再将 IP 地址返回客户端，客户端和目标建立连接。</font>

<font style="color:rgb(44, 62, 80);">至此，我们完成了 DNS 的解析过程。现在总结一下，整个过程我画成了一个图。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706684500702-3bacad20-de02-4a0e-b239-ae39276ee145.png)

<font style="color:rgb(44, 62, 80);">DNS 域名解析的过程蛮有意思的，整个过程就和我们日常生活中找人问路的过程类似，</font>**<font style="color:rgb(48, 79, 254);">只指路不带路</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">那是不是每次解析域名都要经过那么多的步骤呢？</font>

<font style="color:rgb(44, 62, 80);">当然不是了，还有缓存这个东西的嘛。</font>

<font style="color:rgb(44, 62, 80);">浏览器会先看自身有没有对这个域名的缓存，如果有，就直接返回，如果没有，就去问操作系统，操作系统也会去看自己的缓存，如果有，就直接返回，如果没有，再去 hosts 文件看，也没有，才会去问「本地 DNS 服务器」。</font>

##### 操作系统协议栈
<font style="color:rgb(44, 62, 80);">通过 DNS 获取到 IP 后，就可以把 HTTP 的传输工作交给操作系统中的</font><font style="color:rgb(48, 79, 254);">协议栈</font><font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">协议栈的内部分为几个部分，分别承担不同的工作。上下关系是有一定的规则的，上面的部分会向下面的部分委托工作，下面的部分收到委托的工作并执行。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706684795572-1c3efd91-8324-41dd-b38e-74ed4e0bea30.png)

<font style="color:rgb(44, 62, 80);">应用程序（浏览器）通过调用 Socket 库，来委托协议栈工作。协议栈的上半部分有两块，分别是负责收发数据的 TCP 和 UDP 协议，这两个传输协议会接受应用层的委托执行收发数据的操作。</font>

<font style="color:rgb(44, 62, 80);">协议栈的下面一半是用 IP 协议控制网络包收发操作，在互联网上传数据时，数据会被切分成一块块的网络包，而将网络包发送给对方的操作就是由 IP 负责的。</font>

<font style="color:rgb(44, 62, 80);">此外 IP 中还包括</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ICMP</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">协议和</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ARP</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">协议。</font>

+ <font style="color:rgb(71, 101, 130);">ICMP</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">用于告知网络包传送过程中产生的错误以及各种控制信息。</font>
+ <font style="color:rgb(71, 101, 130);">ARP</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">用于根据 IP 地址查询相应的以太网 MAC 地址。</font>

<font style="color:rgb(44, 62, 80);">IP 下面的网卡驱动程序负责控制网卡硬件，而最下面的网卡则负责完成实际的收发操作，也就是对网线中的信号执行发送和接收操作。</font>

#### <font style="color:rgb(44, 62, 80);">TCP 可靠传输</font>
<font style="color:rgb(44, 62, 80);">HTTP 是基于 TCP 协议传输的</font>

##### <font style="color:rgb(44, 62, 80);">TCP 报文头部格式</font>
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706685010779-fac3efad-2596-4a95-9ec2-41a1cebeccde.png)  
<font style="color:rgb(44, 62, 80);">首先，</font>**<font style="color:rgb(48, 79, 254);">源端口号</font>**<font style="color:rgb(44, 62, 80);">和</font>**<font style="color:rgb(48, 79, 254);">目标端口</font>**<font style="color:rgb(44, 62, 80);">号是不可少的，如果没有这两个端口号，数据就不知道应该发给哪个应用。</font>

<font style="color:rgb(44, 62, 80);">接下来有包的</font>**<font style="color:rgb(48, 79, 254);">序</font>**<font style="color:rgb(44, 62, 80);">号，这个是为了解决包乱序的问题。</font>

<font style="color:rgb(44, 62, 80);">还有应该有的是</font>**<font style="color:rgb(48, 79, 254);">确认号</font>**<font style="color:rgb(44, 62, 80);">，目的是确认发出去对方是否有收到。如果没有收到就应该重新发送，直到送达，这个是为了解决丢包的问题。</font>

<font style="color:rgb(44, 62, 80);">接下来还有一些</font>**<font style="color:rgb(48, 79, 254);">状态位</font>**<font style="color:rgb(44, 62, 80);">。例如</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SYN</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">是发起一个连接，</font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">是回复，</font><font style="color:rgb(71, 101, 130);">RST</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">是重新连接，</font><font style="color:rgb(71, 101, 130);">FIN</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">是结束连接等。TCP 是面向连接的，因而双方要维护连接的状态，这些带状态位的包的发送，会引起双方的状态变更。</font>

<font style="color:rgb(44, 62, 80);">还有一个重要的就是</font>**<font style="color:rgb(48, 79, 254);">窗口大小</font>**<font style="color:rgb(44, 62, 80);">。TCP 要做</font>**<font style="color:rgb(48, 79, 254);">流量控制</font>**<font style="color:rgb(44, 62, 80);">，通信双方各声明一个窗口（缓存大小），标识自己当前能够的处理能力，别发送的太快，撑死我，也别发的太慢，饿死我。</font>

<font style="color:rgb(44, 62, 80);">除了做流量控制以外，TCP还会做</font>**<font style="color:rgb(48, 79, 254);">拥塞控制</font>**<font style="color:rgb(44, 62, 80);">，对于真正的通路堵车不堵车，它无能为力，唯一能做的就是控制自己，也即控制发送的速度。不能改变世界，就改变自己嘛。</font>

##### <font style="color:rgb(44, 62, 80);">三次握手</font>
<font style="color:rgb(44, 62, 80);">在 HTTP 传输数据之前，首先需要 TCP 建立连接，TCP 连接的建立，通常称为</font>**<font style="color:rgb(48, 79, 254);">三次握手</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">这个所谓的「连接」，只是双方计算机里维护一个状态机，在连接建立的过程中，双方的状态变化时序图就像这样:</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706685919712-8e18ac15-588f-4c3a-bb0b-c60666122a0f.png)

+ <font style="color:rgb(44, 62, 80);">一开始，客户端和服务端都处于 </font><font style="color:rgb(71, 101, 130);">CLOSED</font><font style="color:rgb(44, 62, 80);"> 状态。先是服务端主动监听某个端口，处于 </font><font style="color:rgb(71, 101, 130);">LISTEN</font><font style="color:rgb(44, 62, 80);"> 状态。</font>
+ <font style="color:rgb(44, 62, 80);">然后客户端主动发起连接</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SYN</font><font style="color:rgb(44, 62, 80);">，之后处于</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SYN-SENT</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态。</font>
+ <font style="color:rgb(44, 62, 80);">服务端收到发起的连接，返回</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SYN</font><font style="color:rgb(44, 62, 80);">，并且</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">客户端的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SYN</font><font style="color:rgb(44, 62, 80);">，之后处于</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SYN-RCVD</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态。</font>
+ <font style="color:rgb(44, 62, 80);">客户端收到服务端发送的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SYN</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">和</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">之后，发送对</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">SYN</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">确认的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);">，之后处于</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ESTABLISHED</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态，因为它一发一收成功了。</font>
+ <font style="color:rgb(44, 62, 80);">服务端收到 </font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);"> 的 </font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);"> 之后，处于 </font><font style="color:rgb(71, 101, 130);">ESTABLISHED</font><font style="color:rgb(44, 62, 80);"> 状态，因为它也一发一收了。</font>

<font style="color:rgb(44, 62, 80);">三次握手目的是</font>**<font style="color:rgb(48, 79, 254);">保证双方都有发送和接收的能力。</font>**

##### TCP 连接状态查看
<font style="color:rgb(44, 62, 80);">在 Linux 可以通过 </font>`<font style="color:rgb(71, 101, 130);">netstat -napt</font>`<font style="color:rgb(44, 62, 80);"> 命令查看</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706686055500-aeb14c62-e814-4bb7-80d9-95419a8a03af.png)

```shell
[root@k8s ~]# netstat -napt
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 169.254.25.10:9254      0.0.0.0:*               LISTEN      28580/node-cache
tcp        0      0 127.0.0.1:10248         0.0.0.0:*               LISTEN      726/kubelet
tcp        0      0 127.0.0.1:10249         0.0.0.0:*               LISTEN      10467/kube-proxy
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1646/sshd
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1927/master
tcp        0      0 10.0.4.2:2379           10.0.4.2:34720          ESTABLISHED 1336/etcd
tcp        0      0 127.0.0.1:33072         127.0.0.1:9099          TIME_WAIT   -
tcp        0      0 10.0.4.2:2379           10.0.4.2:34214          ESTABLISHED 1336/etcd
tcp        0      0 127.0.0.1:58902         127.0.0.1:9100          ESTABLISHED 10986/kube-rbac-pro
tcp        0      0 10.0.4.2:2379           10.0.4.2:34722          ESTABLISHED 1336/etcd
tcp        0      0 169.254.25.10:34334     169.254.25.10:9254      TIME_WAIT   -
tcp        0      0 10.0.4.2:34074          10.0.4.2:2379           ESTABLISHED 42208/kube-apiserve
tcp        0      0 169.254.25.10:34662     169.254.25.10:9254      TIME_WAIT   -
tcp        0      0 10.0.4.2:35178          10.0.4.2:2379           ESTABLISHED 42208/kube-apiserve
tcp        0      0 10.0.4.2:34162          10.0.4.2:2379           ESTABLISHED 42208/kube-apiserve
tcp        0      0 10.0.4.2:34250          10.0.4.2:2379           ESTABLISHED 42208/kube-apiserve
tcp        0      0 169.254.25.10:34008     169.254.25.10:9254      TIME_WAIT   -
tcp        0      0 169.254.25.10:33930     169.254.25.10:9254      TIME_WAIT   -
tcp        0      0 10.0.4.2:2379           10.0.4.2:34426          ESTABLISHED 1336/etcd
tcp        0      0 10.0.4.2:35196          10.0.4.2:2379           ESTABLISHED 42208/kube-apiserve
tcp        0      0 10.0.4.2:2379           10.0.4.2:35168          ESTABLISHED 1336/etcd
tcp        0      0 169.254.25.10:34622     169.254.25.10:9254      TIME_WAIT   -
```

##### TCP 分割数据
<font style="color:rgb(44, 62, 80);">如果 HTTP 请求消息比较长，超过了 </font>**<font style="color:rgb(71, 101, 130);">MSS</font>**<font style="color:rgb(44, 62, 80);"> 的长度，这时 TCP 就需要把 HTTP 的数据拆解成一块块的数据发送，而不是一次性发送所有数据。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706686242742-8dbba3fc-ba3d-4a3f-af65-08d517f01087.png)

+ <font style="color:rgb(71, 101, 130);">MTU</font><font style="color:rgb(44, 62, 80);">：一个网络包的最大长度，以太网中一般为</font>**<font style="color:rgb(44, 62, 80);"> </font>****<font style="color:rgb(71, 101, 130);">1500</font>****<font style="color:rgb(44, 62, 80);"> 字节</font>**<font style="color:rgb(44, 62, 80);">。</font>
+ <font style="color:rgb(71, 101, 130);">MSS(</font><font style="color:rgb(51, 51, 51);">Maximum Segment Size</font><font style="color:rgb(71, 101, 130);">)</font><font style="color:rgb(44, 62, 80);">：除去IP和TCP头部之后,一个网络包所能容纳的 TCP 数据的最大长度。</font>

<font style="color:rgb(44, 62, 80);">数据会被以 </font><font style="color:rgb(71, 101, 130);">MSS</font><font style="color:rgb(44, 62, 80);"> 的长度为单位进行拆分，拆分出来的每一块数据都会被放进单独的网络包中。也就是在每个被拆分的数据加上 TCP 头信息，然后交给 IP 模块来发送数据。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706686262758-986bcfab-a53a-4e60-b67f-27ae1eae8ae5.png)

##### TCP 报文生成
<font style="color:rgb(44, 62, 80);">TCP 协议里面会有两个端口，一个是浏览器监听的端口（通常是随机生成的），一个是 Web 服务器监听的端口（HTTP 默认端口号是 </font><font style="color:rgb(71, 101, 130);">80</font><font style="color:rgb(44, 62, 80);">， HTTPS 默认端口号是 </font><font style="color:rgb(71, 101, 130);">443</font><font style="color:rgb(44, 62, 80);">）。</font>

<font style="color:rgb(44, 62, 80);">在双方建立了连接后，TCP 报文中的数据部分就是存放 HTTP 头部 + 数据，组装好 TCP 报文之后，就需交给下面的网络层处理。</font>

<font style="color:rgb(44, 62, 80);">至此，网络包的报文如下图</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706686318006-58ef671b-96eb-4ff5-928e-1bd837996882.png)

#### IP 协议数据包封装传输
<font style="color:rgb(44, 62, 80);">TCP 模块在执行连接、收发、断开等各阶段操作时，都需要委托 IP 模块将数据封装成</font>**<font style="color:rgb(48, 79, 254);">网络包</font>**<font style="color:rgb(44, 62, 80);">发送给通信对象。</font>

##### IP 报头格式
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706686454355-ac513695-31ba-4c55-91ce-e9ae6eed6f31.png)

<font style="color:rgb(44, 62, 80);">在 IP 协议里面需要有</font>**<font style="color:rgb(48, 79, 254);">源地址 IP</font>**<font style="color:rgb(44, 62, 80);"> 和 </font>**<font style="color:rgb(48, 79, 254);">目标地址 IP</font>**<font style="color:rgb(44, 62, 80);">：</font>

+ <font style="color:rgb(44, 62, 80);">源地址IP：客户端输出的 IP 地址</font>
+ <font style="color:rgb(44, 62, 80);">目标地址：通过 DNS 域名解析得到的 Web 服务器 IP</font>

<font style="color:rgb(44, 62, 80);">因为 HTTP 是经过 TCP 传输的，所以在 IP 包头的</font>**<font style="color:rgb(48, 79, 254);">协议号</font>**<font style="color:rgb(44, 62, 80);">，要填写为 </font><font style="color:rgb(71, 101, 130);">06</font><font style="color:rgb(44, 62, 80);">（十六进制），表示协议为 TCP。</font><font style="color:rgb(44, 62, 80);background-color:rgb(227, 242, 253);"></font>

##### <font style="color:rgb(44, 62, 80);">假设客户端有多个网卡，就会有多个 IP 地址，那 IP 头部的源地址应该选择哪个 IP 呢？</font>
<font style="color:rgb(44, 62, 80);">当存在多个网卡时，在填写源地址 IP 时，就需要判断到底应该填写哪个地址。这个判断相当于在多块网卡中判断应该使用哪个一块网卡来发送包。</font>

<font style="color:rgb(44, 62, 80);">这个时候就需要根据</font>**<font style="color:rgb(48, 79, 254);">路由表</font>**<font style="color:rgb(44, 62, 80);">规则，来判断哪一个网卡作为源地址 IP。</font>

<font style="color:rgb(44, 62, 80);">在 Linux 操作系统，我们可以使用 </font>`<font style="color:rgb(71, 101, 130);">route -n</font>`<font style="color:rgb(44, 62, 80);"> 命令查看当前系统的路由表。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706686647192-413a2acd-3d73-4875-ba26-790eeb41eb9b.png)

<font style="color:rgb(44, 62, 80);">举个例子，根据上面的路由表，我们假设 Web 服务器的目标地址是 </font><font style="color:rgb(71, 101, 130);">192.168.10.200</font><font style="color:rgb(44, 62, 80);">。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706686674416-780a836c-7bab-410e-96a7-48c87b838c0b.png)

1. <font style="color:rgb(44, 62, 80);">首先先和第一条目的子网掩码（</font><font style="color:rgb(71, 101, 130);">Genmask</font><font style="color:rgb(44, 62, 80);">）进行 </font>**<font style="color:rgb(48, 79, 254);">与运算</font>**<font style="color:rgb(44, 62, 80);">，得到结果为 </font><font style="color:rgb(71, 101, 130);">192.168.10.0</font><font style="color:rgb(44, 62, 80);">，但是第一个条目的 </font><font style="color:rgb(71, 101, 130);">Destination</font><font style="color:rgb(44, 62, 80);"> 是 </font><font style="color:rgb(71, 101, 130);">192.168.3.0</font><font style="color:rgb(44, 62, 80);">，两者不一致所以匹配失败。</font>
2. <font style="color:rgb(44, 62, 80);">再与第二条目的子网掩码进行</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">与运算</font>**<font style="color:rgb(44, 62, 80);">，得到的结果为</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">192.168.10.0</font><font style="color:rgb(44, 62, 80);">，与第二条目的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">Destination 192.168.10.0</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">匹配成功，所以将使用</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">eth1</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">网卡的 IP 地址作为 IP 包头的源地址。</font>

<font style="color:rgb(44, 62, 80);">那么假设 Web 服务器的目标地址是</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">10.100.20.100</font><font style="color:rgb(44, 62, 80);">，那么依然依照上面的路由表规则判断，判断后的结果是和第三条目匹配。</font>

<font style="color:rgb(44, 62, 80);">第三条目比较特殊，它目标地址和子网掩码都是 </font><font style="color:rgb(71, 101, 130);">0.0.0.0</font><font style="color:rgb(44, 62, 80);">，这表示</font>**<font style="color:rgb(48, 79, 254);">默认网关</font>**<font style="color:rgb(44, 62, 80);">，如果其他所有条目都无法匹配，就会自动匹配这一行。并且后续就把包发给路由器，</font><font style="color:rgb(71, 101, 130);">Gateway</font><font style="color:rgb(44, 62, 80);"> 即是路由器的 IP 地址。</font>

##### <font style="color:rgb(44, 62, 80);">IP 报文生成</font>
<font style="color:rgb(44, 62, 80);">网络包的报文如下图</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706687060489-5a7e97cd-86c0-4508-837f-7444e0f807b8.png)

#### MAC
<font style="color:rgb(44, 62, 80);">生成了 IP 头部之后，接下来网络包还需要在 IP 头部的前面加上 </font>**<font style="color:rgb(48, 79, 254);">MAC 头部</font>**<font style="color:rgb(44, 62, 80);">。</font>

##### <font style="color:rgb(44, 62, 80);">MAC 包头格式</font>
<font style="color:rgb(44, 62, 80);">MAC 头部是以太网使用的头部，它包含了接收方和发送方的 MAC 地址等信息。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706687558649-e2a6226a-1738-4f05-8212-21d24ce398bd.png)

<font style="color:rgb(44, 62, 80);">在 MAC 包头里需要</font>**<font style="color:rgb(48, 79, 254);">发送方 MAC 地址</font>**<font style="color:rgb(44, 62, 80);">和</font>**<font style="color:rgb(48, 79, 254);">接收方目标 MAC 地址</font>**<font style="color:rgb(44, 62, 80);">，用于</font>**<font style="color:rgb(48, 79, 254);">两点之间的传输</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">一般在 TCP/IP 通信里，MAC 包头的</font>**<font style="color:rgb(48, 79, 254);">协议类型</font>**<font style="color:rgb(44, 62, 80);">只使用：</font>

+ <font style="color:rgb(71, 101, 130);">0800</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">： IP 协议</font>
+ <font style="color:rgb(71, 101, 130);">0806</font><font style="color:rgb(44, 62, 80);"> ： ARP 协议</font>

##### <font style="color:rgb(44, 62, 80);">MAC 发送方和接收方如何确认?</font>
**<font style="color:rgb(48, 79, 254);">发送方</font>**<font style="color:rgb(44, 62, 80);">的 MAC 地址获取就比较简单了，MAC 地址是在网卡生产时写入到 ROM 里的，只要将这个值读取出来写入到 MAC 头部就可以了。</font>

**<font style="color:rgb(48, 79, 254);">接收方</font>**<font style="color:rgb(44, 62, 80);">的 MAC 地址就有点复杂了，只要告诉以太网对方的 MAC 的地址，以太网就会帮我们把包发送过去，那么很显然这里应该填写对方的 MAC 地址。</font>

<font style="color:rgb(44, 62, 80);">所以先得搞清楚应该把包发给谁，这个只要查一下</font>**<font style="color:rgb(48, 79, 254);">路由表</font>**<font style="color:rgb(44, 62, 80);">就知道了。在路由表中找到相匹配的条目，然后把包发给 </font><font style="color:rgb(71, 101, 130);">Gateway</font><font style="color:rgb(44, 62, 80);"> 列中的 IP 地址就可以了。</font>

##### <font style="color:rgb(44, 62, 80);">既然知道要发给谁，如何获取对方的 MAC 地址呢？</font>
<font style="color:rgb(44, 62, 80);"></font><font style="color:rgb(71, 101, 130);">ARP</font><font style="color:rgb(44, 62, 80);"> 协议帮我们找到路由器的 MAC 地址。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706687660490-8c14b1f3-ab7d-4d18-b5ef-b996c5937268.png)

<font style="color:rgb(44, 62, 80);">ARP 协议会在以太网中以</font>**<font style="color:rgb(48, 79, 254);">广播</font>**<font style="color:rgb(44, 62, 80);">的形式，对以太网所有的设备喊出：“这个 IP 地址是谁的？请把你的 MAC 地址告诉我”。</font>

<font style="color:rgb(44, 62, 80);">然后就会有人回答：“这个 IP 地址是我的，我的 MAC 地址是 XXXX”。</font>

<font style="color:rgb(44, 62, 80);">如果对方和自己处于同一个子网中，那么通过上面的操作就可以得到对方的 MAC 地址。然后，我们将这个 MAC 地址写入 MAC 头部，MAC 头部就完成了。</font>

##### <font style="color:rgb(44, 62, 80);">好像每次都要广播获取，这不是很麻烦吗？</font>
<font style="color:rgb(44, 62, 80);">放心，在后续操作系统会把本次查询结果放到一块叫做 </font>**<font style="color:rgb(48, 79, 254);">ARP 缓存</font>**<font style="color:rgb(44, 62, 80);">的内存空间留着以后用，不过缓存的时间就几分钟。</font>

<font style="color:rgb(44, 62, 80);">也就是说，在发包时：</font>

+ <font style="color:rgb(44, 62, 80);">先查询 ARP 缓存，如果其中已经保存了对方的 MAC 地址，就不需要发送 ARP 查询，直接使用 ARP 缓存中的地址。</font>
+ <font style="color:rgb(44, 62, 80);">而当 ARP 缓存中不存在对方 MAC 地址时，则发送 ARP 广播查询。</font>

<font style="color:rgb(44, 62, 80);">在 Linux 系统中，我们可以使用 </font>`<font style="color:rgb(71, 101, 130);">arp -a</font>`<font style="color:rgb(44, 62, 80);"> 命令来查看 ARP 缓存的内容。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706687770848-58a6040c-6f59-4c2c-bf32-01be6d94e4d3.png)

##### MAC 报文生成
<font style="color:rgb(44, 62, 80);">网络包的报文如下图：</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706687798950-bd584e4f-cdd5-4bd7-a6b7-d826064f54bb.png)

#### 网卡数据发送
<font style="color:rgb(44, 62, 80);">网络包只是存放在内存中的一串二进制数字信息，没有办法直接发送给对方。因此，我们需要将</font>**<font style="color:rgb(48, 79, 254);">数字信息转换为电信号</font>**<font style="color:rgb(44, 62, 80);">，才能在网线上传输，也就是说，这才是真正的数据发送过程。</font>

<font style="color:rgb(44, 62, 80);">负责执行这一操作的是</font>**<font style="color:rgb(48, 79, 254);">网卡</font>**<font style="color:rgb(44, 62, 80);">，要控制网卡还需要靠</font>**<font style="color:rgb(48, 79, 254);">网卡驱动程序</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">网卡驱动获取网络包之后，会将其</font>**<font style="color:rgb(48, 79, 254);">复制</font>**<font style="color:rgb(44, 62, 80);">到网卡内的缓存区中，接着会在其</font>**<font style="color:rgb(48, 79, 254);">开头加上报头和起始帧分界符，在末尾加上用于检测错误的帧校验序列</font>**<font style="color:rgb(44, 62, 80);">。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706688028710-facf8008-c14d-42d0-9a28-d91d8e86d9d9.png)

+ <font style="color:rgb(44, 62, 80);">起始帧分界符是一个用来表示包起始位置的标记</font>
+ <font style="color:rgb(44, 62, 80);">末尾的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FCS</font><font style="color:rgb(44, 62, 80);">（帧校验序列）用来检查包传输过程是否有损坏</font>

<font style="color:rgb(44, 62, 80);">最后网卡会将包转为电信号，通过网线发送出去。</font>

#### <font style="color:rgb(44, 62, 80);">交换机</font>
<font style="color:rgb(44, 62, 80);">下面来看一下包是如何通过交换机的。交换机的设计是将网络包</font>**<font style="color:rgb(48, 79, 254);">原样</font>**<font style="color:rgb(44, 62, 80);">转发到目的地。交换机工作在 MAC 层，也称为</font>**<font style="color:rgb(48, 79, 254);">二层网络设备</font>**<font style="color:rgb(44, 62, 80);">。</font>

##### <font style="color:rgb(44, 62, 80);">交换机的包接收操作</font>
<font style="color:rgb(44, 62, 80);">首先，电信号到达网线接口，交换机里的模块进行接收，接下来交换机里的模块将电信号转换为数字信号。</font>

<font style="color:rgb(44, 62, 80);">然后通过包末尾的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FCS</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">校验错误，如果没问题则放到缓冲区。这部分操作基本和计算机的网卡相同，但交换机的工作方式和网卡不同。</font>

<font style="color:rgb(44, 62, 80);">计算机的网卡本身具有 MAC 地址，并通过核对收到的包的接收方 MAC 地址判断是不是发给自己的，如果不是发给自己的则丢弃；相对地，交换机的端口不核对接收方 MAC 地址，而是直接接收所有的包并存放到缓冲区中。因此，和网卡不同，</font>**<font style="color:rgb(48, 79, 254);">交换机的端口不具有 MAC 地址</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">将包存入缓冲区后，接下来需要查询一下这个包的接收方 MAC 地址是否已经在 MAC 地址表中有记录了。</font>

<font style="color:rgb(44, 62, 80);">交换机的 MAC 地址表主要包含两个信息：</font>

+ <font style="color:rgb(44, 62, 80);">一个是设备的 MAC 地址，</font>
+ <font style="color:rgb(44, 62, 80);">另一个是该设备连接在交换机的哪个端口上。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706688395970-327658fb-efb4-41b2-b48b-81ce0a605024.png)

<font style="color:rgb(44, 62, 80);">举个例子，如果收到的包的接收方 MAC 地址为</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">00-02-B3-1C-9C-F9</font><font style="color:rgb(44, 62, 80);">，则与图中表中的第 3 行匹配，根据端口列的信息，可知这个地址位于</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">3</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">号端口上，然后就可以通过交换电路将包发送到相应的端口了。</font>

<font style="color:rgb(44, 62, 80);">所以，</font>**<font style="color:rgb(48, 79, 254);">交换机根据 MAC 地址表查找 MAC 地址，然后将信号发送到相应的端口</font>**<font style="color:rgb(44, 62, 80);">。</font>

##### <font style="color:rgb(44, 62, 80);">当 MAC 地址表找不到指定的 MAC 地址会怎么样？</font>
<font style="color:rgb(44, 62, 80);">地址表中找不到指定的 MAC 地址。这可能是因为具有该地址的设备还没有向交换机发送过包，或者这个设备一段时间没有工作导致地址被从地址表中删除了。</font>

<font style="color:rgb(44, 62, 80);">这种情况下，交换机无法判断应该把包转发到哪个端口，只能将包转发到除了源端口之外的所有端口上，无论该设备连接在哪个端口上都能收到这个包。</font>

<font style="color:rgb(44, 62, 80);">这样做不会产生什么问题，因为以太网的设计本来就是将包发送到整个网络的，然后</font>**<font style="color:rgb(48, 79, 254);">只有相应的接收者才接收包，而其他设备则会忽略这个包</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">有人会说：“这样做会发送多余的包，会不会造成网络拥塞呢？”</font>

<font style="color:rgb(44, 62, 80);">其实完全不用过于担心，因为发送了包之后目标设备会作出响应，只要返回了响应包，交换机就可以将它的地址写入 MAC 地址表，下次也就不需要把包发到所有端口了。</font>

<font style="color:rgb(44, 62, 80);">局域网中每秒可以传输上千个包，多出一两个包并无大碍。</font>

<font style="color:rgb(44, 62, 80);">此外，如果接收方 MAC 地址是一个</font>**<font style="color:rgb(48, 79, 254);">广播地址</font>**<font style="color:rgb(44, 62, 80);">，那么交换机会将包发送到除源端口之外的所有端口。</font>

<font style="color:rgb(44, 62, 80);">以下两个属于广播地址：</font>

+ <font style="color:rgb(44, 62, 80);">MAC 地址中的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FF:FF:FF:FF:FF:FF</font>
+ <font style="color:rgb(44, 62, 80);">IP 地址中的 </font><font style="color:rgb(71, 101, 130);">255.255.255.255</font>

#### 路由器
##### <font style="color:rgb(44, 62, 80);">路由器与交换机的区别</font>
<font style="color:rgb(44, 62, 80);">网络包经过交换机之后，现在到达了</font>**<font style="color:rgb(48, 79, 254);">路由器</font>**<font style="color:rgb(44, 62, 80);">，并在此被转发到下一个路由器或目标设备。</font>

<font style="color:rgb(44, 62, 80);">这一步转发的工作原理和交换机类似，也是通过查表判断包转发的目标。</font>

<font style="color:rgb(44, 62, 80);">不过在具体的操作过程上，路由器和交换机是有区别的。</font>

+ **<font style="color:rgb(48, 79, 254);">路由器：</font>**<font style="color:rgb(44, 62, 80);">基于 IP 设计，俗称</font>**<font style="color:rgb(48, 79, 254);">三层</font>**<font style="color:rgb(44, 62, 80);">网络设备，路由器的各个端口都具有 MAC 地址和 IP 地址；</font>
+ **<font style="color:rgb(48, 79, 254);">交换机：</font>**<font style="color:rgb(44, 62, 80);">基于以太网设计，俗称</font>**<font style="color:rgb(48, 79, 254);">二层</font>**<font style="color:rgb(44, 62, 80);">网络设备，交换机的端口不具有 MAC 地址。</font>

##### <font style="color:rgb(44, 62, 80);">路由器基本原理</font>
<font style="color:rgb(44, 62, 80);">路由器的端口具有 MAC 地址，因此它就能够成为以太网的发送方和接收方；同时还具有 IP 地址，从这个意义上来说，它和计算机的网卡是一样的。</font>

<font style="color:rgb(44, 62, 80);">当转发包时，首先路由器端口会接收发给自己的以太网包，然后</font>**<font style="color:rgb(48, 79, 254);">路由表</font>**<font style="color:rgb(44, 62, 80);">查询转发目标，再由相应的端口作为发送方将以太网包发送出去。</font>

##### <font style="color:rgb(44, 62, 80);">路由器的包接收操作</font>
<font style="color:rgb(44, 62, 80);">首先，电信号到达网线接口部分，路由器中的模块会将电信号转成数字信号，然后通过包末尾的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FCS</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">进行错误校验。</font>

<font style="color:rgb(44, 62, 80);">如果没问题则检查 MAC 头部中的</font>**<font style="color:rgb(48, 79, 254);">接收方 MAC 地址</font>**<font style="color:rgb(44, 62, 80);">，看看是不是发给自己的包，如果是就放到接收缓冲区中，否则就丢弃这个包。</font>

<font style="color:rgb(44, 62, 80);">总的来说，</font>**<font style="color:rgb(44, 62, 80);">路由器的端口都具有 MAC 地址，只接收与自身地址匹配的包，遇到不匹配的包则直接丢弃。</font>**

##### <font style="color:rgb(44, 62, 80);">查询路由表确定输出端口</font>
<font style="color:rgb(44, 62, 80);">完成包接收操作之后，路由器就会</font>**<font style="color:rgb(48, 79, 254);">去掉</font>**<font style="color:rgb(44, 62, 80);">包开头的 MAC 头部。</font>

**<font style="color:rgb(48, 79, 254);">MAC 头部的作用就是将包送达路由器</font>**<font style="color:rgb(44, 62, 80);">，其中的接收方 MAC 地址就是路由器端口的 MAC 地址。因此，当包到达路由器之后，MAC 头部的任务就完成了，于是 MAC 头部就会</font>**<font style="color:rgb(48, 79, 254);">被丢弃</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">接下来，路由器会根据 MAC 头部后方的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">IP</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">头部中的内容进行包的转发操作。</font>

<font style="color:rgb(44, 62, 80);">转发操作分为几个阶段，首先是查询</font>**<font style="color:rgb(48, 79, 254);">路由表</font>**<font style="color:rgb(44, 62, 80);">判断转发目标。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706688611014-ac917994-28e4-4a64-b4c1-a64abd273007.png)

<font style="color:rgb(44, 62, 80);">具体的工作流程根据上图，举个例子。</font>

<font style="color:rgb(44, 62, 80);">假设地址为</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">10.10.1.101</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">的计算机要向地址为</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">192.168.1.100</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">的服务器发送一个包，这个包先到达图中的路由器。</font>

<font style="color:rgb(44, 62, 80);">判断转发目标的第一步，就是根据包的接收方 IP 地址查询路由表中的目标地址栏，以找到相匹配的记录。</font>

<font style="color:rgb(44, 62, 80);">路由匹配和前面讲的一样，每个条目的子网掩码和</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">192.168.1.100</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">IP 做</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">& 与运算</font>**<font style="color:rgb(44, 62, 80);">后，得到的结果与对应条目的目标地址进行匹配，如果匹配就会作为候选转发目标，如果不匹配就继续与下个条目进行路由匹配。</font>

<font style="color:rgb(44, 62, 80);">如第二条目的子网掩码</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">255.255.255.0</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">与</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">192.168.1.100</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">IP 做</font><font style="color:rgb(44, 62, 80);"> </font>**<font style="color:rgb(48, 79, 254);">& 与运算</font>**<font style="color:rgb(44, 62, 80);">后，得到结果是</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">192.168.1.0</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">，这与第二条目的目标地址</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">192.168.1.0</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">匹配，该第二条目记录就会被作为转发目标。</font>

<font style="color:rgb(44, 62, 80);">实在找不到匹配路由时，就会选择</font>**<font style="color:rgb(48, 79, 254);">默认路由</font>**<font style="color:rgb(44, 62, 80);">，路由表中子网掩码为</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">0.0.0.0</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">的记录表示「默认路由」。</font>

##### <font style="color:rgb(44, 62, 80);">路由器的发送操作</font>
<font style="color:rgb(44, 62, 80);">接下来就会进入包的</font>**<font style="color:rgb(48, 79, 254);">发送操作</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">首先，我们需要根据</font>**<font style="color:rgb(48, 79, 254);">路由表的网关列</font>**<font style="color:rgb(44, 62, 80);">判断对方的地址。</font>

+ <font style="color:rgb(44, 62, 80);">如果网关是一个 IP 地址，则这个IP 地址就是我们要转发到的目标地址，</font>**<font style="color:rgb(48, 79, 254);">还未抵达终点</font>**<font style="color:rgb(44, 62, 80);">，还需继续需要路由器转发。</font>
+ <font style="color:rgb(44, 62, 80);">如果网关为空，则 IP 头部中的接收方 IP 地址就是要转发到的目标地址，也是就终于找到 IP 包头里的目标地址了，说明</font>**<font style="color:rgb(48, 79, 254);">已抵达终点</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">知道对方的 IP 地址之后，接下来需要通过 </font><font style="color:rgb(71, 101, 130);">ARP</font><font style="color:rgb(44, 62, 80);"> 协议根据 IP 地址查询 MAC 地址，并将查询的结果作为接收方 MAC 地址。</font>

<font style="color:rgb(44, 62, 80);">路由器也有 ARP 缓存，因此首先会在 ARP 缓存中查询，如果找不到则发送 ARP 查询请求。</font>

<font style="color:rgb(44, 62, 80);">接下来是发送方 MAC 地址字段，这里填写输出端口的 MAC 地址。还有一个以太类型字段，填写</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">0800</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">（十六进制）表示 IP 协议。</font>

<font style="color:rgb(44, 62, 80);">网络包完成后，接下来会将其转换成电信号并通过端口发送出去。这一步的工作过程和计算机也是相同的。</font>

<font style="color:rgb(44, 62, 80);">发送出去的网络包会通过</font>**<font style="color:rgb(48, 79, 254);">交换机</font>**<font style="color:rgb(44, 62, 80);">到达下一个路由器。由于接收方 MAC 地址就是下一个路由器的地址，所以交换机会根据这一地址将包传输到下一个路由器。</font>

<font style="color:rgb(44, 62, 80);">接下来，下一个路由器会将包转发给再下一个路由器，经过层层转发之后，网络包就到达了最终的目的地。</font>

<font style="color:rgb(44, 62, 80);">不知你发现了没有，</font>**<font style="color:rgb(44, 62, 80);">在网络包传输的过程中，</font>****<font style="color:rgb(48, 79, 254);">源 IP 和目标 IP 始终是不会变的，一直变化的是 MAC 地址</font>****<font style="color:rgb(44, 62, 80);">，因为需要 MAC 地址在以太网内进行</font>****<font style="color:rgb(48, 79, 254);">两个设备</font>****<font style="color:rgb(44, 62, 80);">之间的包传输</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">数据包通过多个路由器道友的帮助，在网络世界途经了很多路程，最终抵达了目的地的城门！城门值守的路由器，发现了这个小兄弟数据包原来是找城内的人，于是它就将数据包送进了城内，再经由城内的交换机帮助下，最终转发到了目的地了。数据包感慨万千的说道：“多谢这一路上，各路大侠的相助！”</font>

#### <font style="color:rgb(44, 62, 80);">服务端和客户端解包</font>
<font style="color:rgb(44, 62, 80);">数据包抵达了服务器，服务器高兴的不得了，于是开始扒数据包的皮！</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706689234365-9c59494c-28c3-40b7-a094-d894b841179c.png)

<font style="color:rgb(44, 62, 80);">数据包抵达服务器后，服务器会先扒开数据包的 MAC 头部，查看是否和服务器自己的 MAC 地址符合，符合就将包收起来。</font>

<font style="color:rgb(44, 62, 80);">接着继续扒开数据包的 IP 头，发现 IP 地址符合，根据 IP 头中协议项，知道自己上层是 TCP 协议。</font>

<font style="color:rgb(44, 62, 80);">于是，扒开 TCP 的头，里面有序列号，需要看一看这个序列包是不是我想要的，如果是就放入缓存中然后返回一个 ACK，如果不是就丢弃。TCP 头部里面还有端口号， HTTP 的服务器正在监听这个端口号。</font>

<font style="color:rgb(44, 62, 80);">于是，服务器自然就知道是 HTTP 进程想要这个包，于是就将包发给 HTTP 进程。</font>

<font style="color:rgb(44, 62, 80);">服务器的 HTTP 进程看到，原来这个请求是要访问一个页面，于是就把这个网页封装在 HTTP 响应报文里。</font>

<font style="color:rgb(44, 62, 80);">HTTP 响应报文也需要穿上 TCP、IP、MAC 头部，不过这次是源地址是服务器 IP 地址，目的地址是客户端 IP 地址。</font>

<font style="color:rgb(44, 62, 80);">穿好头部衣服后，从网卡出去，交由交换机转发到出城的路由器，路由器就把响应数据包发到了下一个路由器，就这样跳啊跳。</font>

<font style="color:rgb(44, 62, 80);">最后跳到了客户端的城门把守的路由器，路由器扒开 IP 头部发现是要找城内的人，于是又把包发给了城内的交换机，再由交换机转发到客户端。</font>

<font style="color:rgb(44, 62, 80);">客户端收到了服务器的响应数据包后，同样也非常的高兴，客户能拆快递了！</font>

<font style="color:rgb(44, 62, 80);">于是，客户端开始扒皮，把收到的数据包的皮扒剩 HTTP 响应报文后，交给浏览器去渲染页面，一份特别的数据包快递，就这样显示出来了！</font>

<font style="color:rgb(44, 62, 80);">最后，客户端要离开了，向服务器发起了 TCP 四次挥手，至此双方的连接就断开了。</font>

#### <font style="color:rgb(44, 62, 80);">前端渲染</font>
[面试官：浏览器输入URL后发生了什么？](https://mp.weixin.qq.com/s/DLq_GIkdnuOayThfi3jI0A)

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706690286245-9c86c5bd-d50f-4274-83f1-191b4f80c0db.png)

1. <font style="color:rgb(1, 1, 1);">渲染进程将 HTML 内容转换为能够读懂DOM 树结构。</font>
2. <font style="color:rgb(1, 1, 1);">渲染引擎将 CSS 样式表转化为浏览器可以理解的 styleSheets，计算出 DOM 节点的样式。</font>
3. <font style="color:rgb(1, 1, 1);">创建布局树，并计算元素的布局信息。</font>
4. <font style="color:rgb(1, 1, 1);">对布局树进行分层，并生成分层树。</font>
5. <font style="color:rgb(1, 1, 1);">为每个图层生成绘制列表，并将其提交到合成线程。合成线程将图层分图块，并栅格化将图块转换成位图。</font>
6. <font style="color:rgb(1, 1, 1);">合成线程发送绘制图块命令给浏览器进程。浏览器进程根据指令生成页面，并显示到显示器上。</font>

#### <font style="color:rgb(44, 62, 80);">QA</font>
##### <font style="color:rgb(44, 62, 80);">问：“笔记本的是自带交换机的吗？交换机现在我还不知道是什么”</font>
<font style="color:rgb(44, 62, 80);">笔记本不是交换机，交换机通常是2个网口以上。</font>

<font style="color:rgb(44, 62, 80);">现在家里的路由器其实有了交换机的功能了。交换机可以简单理解成一个设备，三台电脑网线接到这个设备，这三台电脑就可以互相通信了，交换机嘛，交换数据这么理解就可以。</font>

##### <font style="color:rgb(44, 62, 80);">问：“如果知道你电脑的 mac 地址，我可以直接给你发消息吗？”</font>
<font style="color:rgb(44, 62, 80);">Mac 地址只能是两个设备之间传递时使用的，如果你要从大老远给我发消息，是离不开 IP 的。</font>

##### <font style="color:rgb(44, 62, 80);">问：“请问公网服务器的 Mac 地址是在什么时机通过什么方式获取到的？我看 arp 获取 Mac 地址只能获取到内网机器的 Mac 地址吧？”</font>
<font style="color:rgb(44, 62, 80);">在发送数据包时，如果目标主机不是本地局域网，填入的 MAC 地址是路由器，也就是把数据包转发给路由器，路由器一直转发下一个路由器，直到转发到目标主机的路由器，发现 IP 地址是自己局域网内的主机，就会 arp 请求获取目标主机的 MAC 地址，从而转发到这个服务器主机。</font>

<font style="color:rgb(44, 62, 80);">转发的过程中，源IP地址和目标IP地址是不会变的（前提：没有使用 NAT 网络的），源 MAC 地址和目标 MAC 地址是会变化的。</font>

## TCP
问到的公司: 新浪微博、ucloud

[4.1 TCP 三次握手与四次挥手面试题](https://www.xiaolincoding.com/network/3_tcp/tcp_interview.html)

tcp三次握手介绍下？

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1709042278890-c1c39857-ba4b-473e-84c6-34cf6932ab3b.png)

### 为何需要三次握手？
+ **<font style="color:rgb(44, 62, 80);">三次握手才可以阻止重复历史连接的初始化（主要原因）</font>**
+ **<font style="color:rgb(44, 62, 80);">三次握手才可以同步双方的初始序列号</font>**
+ **<font style="color:rgb(44, 62, 80);">三次握手才可以避免资源浪费</font>**

###  tcp关闭过程？描述下tcp四次挥手？为何要四次挥手，建立连接时候不是三次吗？
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1709042351497-56188538-f583-4816-a12d-4e58f5c45dc2.png)

+ <font style="color:rgb(44, 62, 80);">客户端打算关闭连接，此时会发送一个 TCP 首部</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FIN</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">标志位被置为</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">1</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">的报文，也即</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FIN</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">报文，之后客户端进入</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FIN_WAIT_1</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态。</font>
+ <font style="color:rgb(44, 62, 80);">服务端收到该报文后，就向客户端发送</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">应答报文，接着服务端进入</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">CLOSE_WAIT</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态。</font>
+ <font style="color:rgb(44, 62, 80);">客户端收到服务端的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">应答报文后，之后进入</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FIN_WAIT_2</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态。</font>
+ <font style="color:rgb(44, 62, 80);">等待服务端处理完数据后，也向客户端发送</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FIN</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">报文，之后服务端进入</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">LAST_ACK</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态。</font>
+ <font style="color:rgb(44, 62, 80);">客户端收到服务端的</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">FIN</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">报文后，回一个</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">应答报文，之后进入</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">TIME_WAIT</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态</font>
+ <font style="color:rgb(44, 62, 80);">服务端收到了</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">ACK</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">应答报文后，就进入了</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">CLOSE</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态，至此服务端已经完成连接的关闭。</font>
+ <font style="color:rgb(44, 62, 80);">客户端在经过</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">2MSL</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">一段时间后，自动进入</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">CLOSE</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态，至此客户端也完成连接的关闭。</font>

<font style="color:rgb(44, 62, 80);">你可以看到，每个方向都需要</font>**<font style="color:rgb(48, 79, 254);">一个 FIN 和一个 ACK</font>**<font style="color:rgb(44, 62, 80);">，因此通常被称为</font>**<font style="color:rgb(48, 79, 254);">四次挥手</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">这里一点需要注意是：</font>**<font style="color:rgb(48, 79, 254);">主动关闭连接的，才有 TIME_WAIT 状态。</font>**

### time_wait 和 close_wait有了解吗？
#### time-wait
<font style="color:rgb(44, 62, 80);">主动发起关闭连接的一方，才会有</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(71, 101, 130);">TIME-WAIT</font><font style="color:rgb(44, 62, 80);"> </font><font style="color:rgb(44, 62, 80);">状态。</font>

<font style="color:rgb(44, 62, 80);">需要 TIME-WAIT 状态原因：</font>

+ **<font style="color:rgb(44, 62, 80);">防止历史连接中的数据，被后面相同四元组的连接错误的接收</font>**<font style="color:rgb(44, 62, 80);">；</font>
    - <font style="color:rgb(44, 62, 80);">TIME_WAIT 状态，状态会持续 </font><font style="color:rgb(71, 101, 130);">2MSL</font><font style="color:rgb(44, 62, 80);"> 时长，这个时间</font>**<font style="color:rgb(48, 79, 254);">足以让两个方向上的数据包都被丢弃，使得原来连接的数据包在网络中都自然消失，再出现的数据包一定都是新建立连接所产生的</font>**
+ **<font style="color:rgb(44, 62, 80);">保证「被动关闭连接」的一方，能被正确的关闭</font>**<font style="color:rgb(44, 62, 80);">；</font>
    - **<font style="color:rgb(48, 79, 254);">等待足够的时间以确保最后的 ACK 能让被动关闭方接收，从而帮助其正常关闭。</font>**

##### time-wait 过多危害
+ <font style="color:rgb(44, 62, 80);">占用系统资源，比如文件描述符、内存资源、CPU 资源、线程资源等；</font>
+ <font style="color:rgb(44, 62, 80);">占用端口资源</font>

##### time-wait 优化
+ <font style="color:rgb(44, 62, 80);">打开 net.ipv4.tcp_tw_reuse 和 net.ipv4.tcp_timestamps 选项；</font>
    - **<font style="color:rgb(48, 79, 254);">复用处于 TIME_WAIT 的 socket 为新的连接所用</font>**
    - **<font style="color:rgb(48, 79, 254);">tcp_tw_reuse 功能只能用客户端（连接发起方），因为开启了该功能，在调用 connect() 函数时，内核会随机找一个 time_wait 状态超过 1 秒的连接给新的连接复用</font>**
+ <font style="color:rgb(44, 62, 80);">net.ipv4.tcp_max_tw_buckets</font>
    - <font style="color:rgb(44, 62, 80);">默认为 18000，</font>**<font style="color:rgb(48, 79, 254);">当系统中处于 TIME_WAIT 的连接一旦超过这个值时，系统就会将后面的 TIME_WAIT 连接状态重置</font>**
+ <font style="color:rgb(44, 62, 80);">程序中使用 SO_LINGER ，应用强制使用 RST 关闭</font>
    - <font style="color:rgb(44, 62, 80);">设置 socket 选项，来设置调用 close 关闭连接行为</font>

**<font style="color:rgb(48, 79, 254);">如果服务端要避免过多的 TIME_WAIT 状态的连接，就永远不要主动断开连接，让客户端去断开，由分布在各处的客户端去承受 TIME_WAIT</font>**

##### <font style="color:rgb(48, 79, 254);">服务器出现大量 TIME_WAIT 状态原因</font>
<font style="color:rgb(44, 62, 80);">TIME_WAIT 状态是主动关闭连接方才会出现的状态，服务器出现大量的 TIME_WAIT 状态的 TCP 连接，说明服务器主动断开了很多 TCP 连接。</font>

<font style="color:rgb(44, 62, 80);"></font>**<font style="color:rgb(48, 79, 254);">什么场景下服务端会主动断开连接呢？</font>**

+ **<font style="color:rgb(44, 62, 80);">HTTP 没有使用长连接</font>**
    - <font style="color:rgb(44, 62, 80);">HTTP/1.0 默认没有长连接，必须在 header 添加 Connection: Keep-Alive。</font>
    - **<font style="color:rgb(48, 79, 254);">只要客户端和服务端任意一方的 HTTP header 中有 </font>****<font style="color:rgb(71, 101, 130);">Connection:close</font>****<font style="color:rgb(48, 79, 254);"> 信息，那么就无法使用 HTTP 长连接的机制</font>**
+ **<font style="color:rgb(44, 62, 80);">HTTP 长连接超时</font>**
    - <font style="color:rgb(44, 62, 80);">web 服务软件一般都会提供一个参数，用来指定 HTTP 长连接的超时时间，比如 nginx 提供的 keepalive_timeout 参数。</font>
    - <font style="color:rgb(44, 62, 80);">假设设置了 HTTP 长连接的超时时间是 60 秒，nginx 就会启动一个「定时器」，</font>**<font style="color:rgb(48, 79, 254);">如果客户端在完后一个 HTTP 请求后，在 60 秒内都没有再发起新的请求，定时器的时间一到，nginx 就会触发回调函数来关闭该连接，那么此时服务端上就会出现 TIME_WAIT 状态的连接。</font>**
    - <font style="color:rgb(44, 62, 80);">当服务端出现大量 TIME_WAIT 状态的连接时，如果现象是有大量的客户端建立完 TCP 连接后，很长一段时间没有发送数据，那么大概率就是因为 HTTP 长连接超时，导致服务端主动关闭连接，产生大量处于 TIME_WAIT 状态的连接。</font>
    - <font style="color:rgb(44, 62, 80);">往网络问题的方向排查，比如是否是因为网络问题，导致客户端发送的数据一直没有被服务端接收到，以至于 HTTP 长连接超时</font>
+ **<font style="color:rgb(44, 62, 80);">HTTP 长连接的请求数量达到上限</font>**
    - <font style="color:rgb(44, 62, 80);">Web 服务端通常会有个参数，来定义一条 HTTP 长连接上最大能处理的请求数量，当超过最大限制时，就会主动关闭连接。</font>
    - <font style="color:rgb(44, 62, 80);">比如 nginx 的 keepalive_requests 这个参数，这个参数是指一个 HTTP 长连接建立之后，nginx 就会为这个连接设置一个计数器，记录这个 HTTP 长连接上已经接收并处理的客户端请求的数量。</font>**<font style="color:rgb(48, 79, 254);">如果达到这个参数设置的最大值时，则 nginx 会主动关闭这个长连接</font>**<font style="color:rgb(44, 62, 80);">，那么此时服务端上就会出现 TIME_WAIT 状态的连接。keepalive_requests 参数的默认值是 100 ，意味着每个 HTTP 长连接最多只能跑 100 次请求，这个参数往往被大多数人忽略，因为当 QPS (每秒请求数) 不是很高时，默认值 100 凑合够用。</font>
    - <font style="color:rgb(44, 62, 80);">但是，</font>**<font style="color:rgb(48, 79, 254);">对于一些 QPS 比较高的场景，比如超过 10000 QPS，甚至达到 30000 , 50000 甚至更高，如果 keepalive_requests 参数值是 100，这时候就 nginx 就会很频繁地关闭连接，那么此时服务端上就会出大量的 TIME_WAIT 状态</font>**<font style="color:rgb(44, 62, 80);">。</font>
    - <font style="color:rgb(44, 62, 80);">针对这个场景下，解决的方式也很简单，调大 nginx 的 keepalive_requests 参数就行</font>

#### close-wait
<font style="color:rgb(44, 62, 80);">CLOSE_WAIT 状态是「被动关闭方」才会有的状态，而且如果「被动关闭方」没有调用 close 函数关闭连接，那么就无法发出 FIN 报文，从而无法使得 CLOSE_WAIT 状态的连接转变为 LAST_ACK 状态</font>

##### <font style="color:rgb(44, 62, 80);">服务器出现大量 CLOSE_WAIT 状态的原因有哪些</font>
**<font style="color:rgb(48, 79, 254);">当服务端出现大量 CLOSE_WAIT 状态的连接的时候，说明服务端的程序没有调用 close 函数关闭连接</font>**<font style="color:rgb(44, 62, 80);">。</font>

<font style="color:rgb(44, 62, 80);">先来分析一个普通的 TCP 服务端的流程：</font>

1. <font style="color:rgb(44, 62, 80);">创建服务端 socket，bind 绑定端口、listen 监听端口</font>
2. <font style="color:rgb(44, 62, 80);">将服务端 socket 注册到 epoll</font>
3. <font style="color:rgb(44, 62, 80);">epoll_wait 等待连接到来，连接到来时，调用 accpet 获取已连接的 socket</font>
4. <font style="color:rgb(44, 62, 80);">将已连接的 socket 注册到 epoll</font>
5. <font style="color:rgb(44, 62, 80);">epoll_wait 等待事件发生</font>
6. <font style="color:rgb(44, 62, 80);">对方连接关闭时，我方调用 close</font>

<font style="color:rgb(44, 62, 80);">可能导致服务端没有调用 close 函数的原因，如下。</font>

**<font style="color:rgb(48, 79, 254);">第一个原因</font>**<font style="color:rgb(44, 62, 80);">：第 2 步没有做，没有将服务端 socket 注册到 epoll，这样有新连接到来时，服务端没办法感知这个事件，也就无法获取到已连接的 socket，那服务端自然就没机会对 socket 调用 close 函数了。</font>

<font style="color:rgb(44, 62, 80);">不过这种原因发生的概率比较小，这种属于明显的代码逻辑 bug，在前期 read view 阶段就能发现的了。</font>

**<font style="color:rgb(48, 79, 254);">第二个原因</font>**<font style="color:rgb(44, 62, 80);">： 第 3 步没有做，有新连接到来时没有调用 accpet 获取该连接的 socket，导致当有大量的客户端主动断开了连接，而服务端没机会对这些 socket 调用 close 函数，从而导致服务端出现大量 CLOSE_WAIT 状态的连接。</font>

<font style="color:rgb(44, 62, 80);">发生这种情况可能是因为服务端在执行 accpet 函数之前，代码卡在某一个逻辑或者提前抛出了异常。</font>

**<font style="color:rgb(48, 79, 254);">第三个原因</font>**<font style="color:rgb(44, 62, 80);">：第 4 步没有做，通过 accpet 获取已连接的 socket 后，没有将其注册到 epoll，导致后续收到 FIN 报文的时候，服务端没办法感知这个事件，那服务端就没机会调用 close 函数了。</font>

<font style="color:rgb(44, 62, 80);">发生这种情况可能是因为服务端在将已连接的 socket 注册到 epoll 之前，代码卡在某一个逻辑或者提前抛出了异常。之前看到过别人解决 close_wait 问题的实践文章，感兴趣的可以看看：</font>[<font style="color:rgb(44, 62, 80);">一次 Netty 代码不健壮导致的大量 CLOSE_WAIT 连接原因分析(opens new window)</font>](https://mp.weixin.qq.com/s?__biz=MzU3Njk0MTc3Ng==&mid=2247486020&idx=1&sn=f7cf41aec28e2e10a46228a64b1c0a5c&scene=21#wechat_redirect)

**<font style="color:rgb(48, 79, 254);">第四个原因</font>**<font style="color:rgb(44, 62, 80);">：第 6 步没有做，当发现客户端关闭连接后，服务端没有执行 close 函数，可能是因为代码漏处理，或者是在执行 close 函数之前，代码卡在某一个逻辑，比如发生死锁等等。</font>

<font style="color:rgb(44, 62, 80);">可以发现，</font>**<font style="color:rgb(48, 79, 254);">当服务端出现大量 CLOSE_WAIT 状态的连接的时候，通常都是代码的问题，这时候我们需要针对具体的代码一步一步的进行排查和定位，主要分析的方向就是服务端为什么没有调用 close</font>**

**<font style="color:rgb(48, 79, 254);"></font>**

### tcp 怎么保证顺序？
**序号**（Sequence Number）： TCP 在每个数据段（TCP 报文段）上都标记了一个序号，表示该数据段在字节流中的位置。接收方根据这些序号来将接收到的数据段按照正确的顺序重新组装成完整的数据流。

确认应答（Acknowledgement）： TCP 使用确认应答机制来确认接收到的数据段。接收方会发送一个确认应答，表示已经成功接收到了某个序号之前的所有数据段。发送方在收到确认应答之后，会知道哪些数据段已经被成功接收，哪些还需要重新发送。

超时重传（Retransmission）： 如果发送方在一定时间内没有收到接收方的确认应答，它会假定数据段丢失了，并进行超时重传。通过不断重传丢失的数据段，发送方可以确保数据的可靠传输。

滑动窗口（Sliding Window）： TCP 使用滑动窗口机制来控制发送方和接收方之间的流量。发送方在发送数据时，会根据接收方返回的确认应答动态调整发送窗口大小，以确保不会发送过多的数据导致接收方缓冲区溢出。这样可以保证数据的顺序传输。

### 如何在 tcp上面做boarder边界？
在 TCP 上实现边界（boundary）的概念通常需要在应用层进行处理， TCP 是一种面向流的协议，它只提供了一个字节流的传输通道，并没有直接支持消息边界的概念。

有几种常见的方法可以在 TCP 上实现消息边界：

+ **固定长度消息**： 在传输数据之前，发送方将消息划分为固定长度的数据块，然后将这些固定长度的数据块作为 TCP 数据段发送给接收方。接收方在接收数据时，根据固定长度的消息大小来解析消息。
+ **特殊字符分隔符**： 使用特定的字符或者字符序列作为消息的分隔符，在消息的末尾添加分隔符来表示消息的结束。接收方在接收数据时，根据分隔符来辨别不同的消息。
+ **长度前缀**： 在传输数据之前，发送方先将消息的长度作为前缀添加到消息头部，然后将包含消息长度信息的数据包发送给接收方。接收方在接收数据时，首先读取消息的长度信息，然后根据长度信息来解析消息。
+ **消息头包含长度信息**： 在消息的头部添加一个字段，用于表示消息的长度。发送方在发送消息时，首先发送消息长度信息，然后发送实际的消息内容。接收方在接收数据时，先读取消息长度信息，然后根据长度信息来读取相应长度的消息内容。

### tcp上面有htp，http分请求，一个请求发了会发另一个请求，这两个请求如何做拆割?一个长连接里面发两个请求，如何区分这两个请求？(ucloud一面)
在 TCP 上面传输 HTTP 协议时，可以通过以下两种方式来区分多个 HTTP 请求：

+ **HTTP/1.1 持久连接（Keep-Alive）**：HTTP/1.1 协议引入了持久连接（Keep-Alive）机制，允许在同一个 TCP 连接上传输多个 HTTP 请求和响应。在持久连接中，每个 HTTP 请求和响应之间通过空行（CRLF，即\r\n\r\n）来分隔。因此，在接收端可以通过解析空行来判断每个 HTTP 请求的结束和下一个 HTTP 请求的开始。HTTP/1.1 的持久连接机制使得多个 HTTP 请求可以共享同一个 TCP 连接，并且减少了连接建立和关闭的开销。
+ **HTTP/2 多路复用（Multiplexing）**：HTTP/2 协议支持多路复用（Multiplexing）机制，允许在同一个 TCP 连接上同时传输多个 HTTP 请求和响应，并且无需按顺序进行处理。在 HTTP/2 中，每个 HTTP 请求和响应都会被分割成一个或多个帧（Frame），并且可以通过帧的标识符来重新组装成完整的请求或响应。

HTTP/2 的多路复用机制使得多个 HTTP 请求可以同时进行，不会被阻塞或串行化，从而提高了网络性能和效率。

### tcp 有很多处于 sync-sent状态的连接，是什么原因？
TCP 连接处于 SYN-SENT 状态通常是因为客户端向服务器端发起了连接请求，但是服务器端尚未发送 SYN-ACK 确认信号，导致连接处于半开放状态。这种情况可能由以下几个原因引起：

+ **网络延迟或故障**： 如果客户端发送了 SYN 包，但服务器端没有及时响应，可能是由于网络延迟或故障导致的。在这种情况下，客户端会重试连接请求，直到收到服务器端的响应。
+ **服务器端负载过高**： 如果服务器端负载过高，无法及时处理所有的连接请求，可能会导致一些连接处于 SYN-SENT 状态。在这种情况下，服务器端可能会拒绝一些连接请求，或者延迟发送 SYN-ACK 确认信号。
+ **防火墙或网络设备设置**： 如果在客户端和服务器端之间存在防火墙或其他网络设备，这些设备可能会过滤或延迟某些连接请求，导致连接处于 SYN-SENT 状态。
+ **服务器端监听队列满**： 如果服务器端的监听队列已满，无法接受新的连接请求，新的连接请求可能会被延迟处理，导致连接处于 SYN-SENT 状态。

### tcp拥塞控制和流量控制(ucloud二面)
#### 重传机制
+ 超时重传
+ 快重传
+ SACK 方法
+ Duplicate SACK 方法

####  滑动窗口
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1709044878698-481038e1-955c-449b-9ee4-5153a33d8b21.png)

#### 流量控制
**<font style="color:rgb(48, 79, 254);">TCP 提供一种机制可以让「发送方」根据「接收方」的实际接收能力控制发送的数据量，这就是所谓的流量控制</font>**

#### 拥塞控制
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1709044834780-466d5915-d237-4970-9c20-5db555de7a20.png)

+ 慢启动
+ 拥塞避免算法
+ 拥塞发生
+ 快速恢复

# 数据结构与算法
## 链表
### [判断链表是否有环](https://leetcode.cn/problems/linked-list-cycle/description/)（触宝一面、乐言三面）
#### 把每个节点存下来，有重复节点就是有环
```go
// 记录下每一个节点，后续遍历到重复节点了，就是有环
// 时间复杂度: O(N) 空间复杂度 O(N) 其中 N 是链表中的节点数
// 有环的会一直遍历下去，遇到重复节点
// 没环的会遍历到尾部，退出
func hasCycle(head *ListNode) bool {
    if head == nil {
        return false
    }
    m := make(map[*ListNode]*ListNode)
    for head != nil {
        if _, ok := m[head]; ok {
            return true
        }
        m[head] = head
        head = head.Next
    }
    return false
}
```

#### 快慢指针，类似龟兔赛跑，快的一次走两步，慢的走一步，进入环以后会相遇
```go
// 快慢指针
// 快的每次走两步，慢的走一步，走进环里面会相遇
func hasCycle2(head *ListNode) bool {
	if head == nil || head.Next == nil {
		return false
	}
	fast, slow := head.Next, head
	for slow != fast {
		// 当没有环时候退出，有环一定会出现 slow = fast
		if fast == nil || fast.Next == nil {
			return false
		}
		slow = slow.Next
		fast = fast.Next.Next
	}
	return true
}
```

### 单链表，build、insert、 delete
```go
package linkedlist

import "errors"

type ListNode struct {
	Val  int
	Next *ListNode
}

// BuildLinkedList 没有头节点的单链表
func BuildLinkedList(values []int) *ListNode {
	if len(values) == 0 {
		return nil
	}
	l := &ListNode{
		Val: values[0],
	}
	curr := l
	for _, val := range values[1:] {
		newNode := &ListNode{
			Val:  val,
			Next: nil,
		}
		curr.Next = newNode
		curr = curr.Next
	}
	return l
}

// InsertLinkedList 头插法，下标从0开始
func InsertLinkedList(head *ListNode, value, position int) (*ListNode, error) {
	newNode := &ListNode{
		Val:  value,
		Next: nil,
	}
	if head == nil || position == 0 {
		newNode.Next = head
		head = newNode
		return head, nil
	}
	current := head
	for i := 1; i < position; i++ {
		if current == nil {
			return nil, errors.New("找不到待插入节点")
		}
		if current.Next == nil && i == position-1 {
			break
		}
		current = current.Next
	}
	newNode.Next = current.Next
	current.Next = newNode
	return head, nil
}

// DeleteLinkedList 下标从0开始
func DeleteLinkedList(head *ListNode, position int) (*ListNode, error) {
	if head == nil {
		return head, nil
	}
	if position == 0 {
		if head.Next == nil {
			head = nil
			return nil, nil
		} else {
			head = head.Next
			return head, nil
		}
	}
	current := head
	pre := current
	for i := 0; i < position; i++ {
		if current == nil {
			return nil, errors.New("找不到待删除节点")
		}
		pre = current
		current = current.Next
	}
	pre.Next = current.Next
	current.Next = nil
	current = nil
	return head, nil
}

```

### [链表反转](https://leetcode.cn/problems/UHnkqh/description/)（新浪微博、B站）
#### 迭代法
```go
// ReverseList 迭代法: 记录前一个节点和后一个节点，遍历时候改为向前的指针，时间复杂度O(N)
func ReverseList(head *ListNode) *ListNode {
	var prev *ListNode
	curr := head
	for curr != nil {
		next := curr.Next
		curr.Next = prev
		prev = curr
		curr = next
	}
	return prev
}
```

#### 递归
```go
// ReverseList2 递归法
func ReverseList2(head *ListNode) *ListNode {
	if head == nil || head.Next == nil {
		return head
	}
	newHead := ReverseList2(head)
	head.Next.Next = head
	head.Next = nil
	return newHead
}
```

#### 头插法插入新链表
```go
// ReverseList3 头插法插入新链表
func ReverseList3(head *ListNode) *ListNode {
	var newHead *ListNode
	for head != nil {
		newNode := &ListNode{Val: head.Val}
		newNode.Next = newHead
		newHead = newNode
		head = head.Next
	}
	return newHead
}
```

### [删除链表倒数第k个节点](https://leetcode.cn/problems/SLwz0R/description/)
#### 计算链表长度后删除
```go
func getLength(head *ListNode) (length int) {
	for ; head != nil; head = head.Next {
		length++
	}
	return
}

func RemoveNthFromEnd(head *ListNode, n int) *ListNode {
	length := getLength(head)
	dummy := &ListNode{Next: head}
	curr := dummy
	for i := 0; i < length-n; i++ {
		curr = curr.Next
	}
	curr.Next = curr.Next.Next
	return dummy.Next
}
```

#### 栈：把节点入栈，第 length -n 个是待删除节点，第 length -n -1是前一个节点，前一个节点指向下一个节点的下一个就可以了
```go
// RemoveNthFromEnd2 我们也可以在遍历链表的同时将所有节点依次入栈。
// 根据栈「先进后出」的原则，我们弹出栈的第 n 个节点就是需要删除的节点， 
// 并且目前栈顶的节点就是待删除节点的前驱节点。这样一来，删除操作就变得十分方便了
func RemoveNthFromEnd2(head *ListNode, n int) *ListNode {
	var nodes []*ListNode
	dummy := &ListNode{Next: head}
	curr := dummy
	for ; curr != nil; curr = curr.Next {
		nodes = append(nodes, curr)
	}
	prev := nodes[len(nodes)-n-1]
	prev.Next = prev.Next.Next
	return dummy.Next
}
```

#### 双指针：first 先走n步，然后second再走，当first到尾部时，second位置的下一个就是待删除节点
```go
// RemoveNthFromEnd4 双指针，first 先走n步，然后second再走，
// 当first到尾部时，second位置的下一个就是待删除节点
// 时间复杂度: O(L), L 是链表长度
// 空间复杂度: O(1)
func RemoveNthFromEnd4(head *ListNode, n int) *ListNode {
	dummy := &ListNode{Next: head}
	first := head
	second := dummy
	for i := 0; i < n; i++ {
		first = first.Next
	}
	for ; first != nil; first = first.Next {
		second = second.Next
	}
	second.Next = second.Next.Next
	return dummy.Next
}
```

### 合并k个已排序的链表
<font style="color:rgb(90, 103, 111);">合并</font>_<font style="color:rgb(90, 103, 111);">k</font>_<font style="color:rgb(90, 103, 111);"> 个已排序的链表并将其作为一个已排序的链表返回。分析并描述其复杂度。 </font>

![](https://cdn.nlark.com/yuque/0/2021/png/543296/1622883115692-34fd550c-f33b-4d7e-a574-34e659f1ced4.png)

### [合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/description/)
给定两个升序的单链表的头节点 head1 和 head2，请合并两个升序链表，合并后的链表依然升序，并返回合并后链表的头节点。

输入描述:

两个升序的单链表的头节点 head1 和 head2

输出描述:

在给定的函数内返回新链表的头指针。

#### 递归：将两个链表中值较小的后续链表和另一个链表合并
```go
func MergeTwoLists(list1 *ListNode, list2 *ListNode) *ListNode {
	if list1 == nil {
		return list2
	} else if list2 == nil {
		return list1
	} else if list1.Val < list2.Val {
		list1.Next = MergeTwoLists(list1.Next, list2)
		return list1
	} else {
		list2.Next = MergeTwoLists(list1, list2.Next)
		return list2
	}
}
```

#### 新建一个链表，将两个链表合并过来
```go
func MergeTwoLists2(list1 *ListNode, list2 *ListNode) *ListNode {
	newList := &ListNode{}
	curr := newList
	for list1 != nil && list2 != nil {
		if list1.Val <= list2.Val {
			newNode := &ListNode{Val: list1.Val}
			curr.Next = newNode
			curr = curr.Next
			list1 = list1.Next
		} else {
			newNode := &ListNode{Val: list2.Val}
			curr.Next = newNode
			curr = curr.Next
			list2 = list2.Next
		}
	}
	// 遍历完只剩下一个链表不为空了
	if list1 != nil {
		curr.Next = list1
	} else {
		curr.Next = list2
	}
	return newList.Next
}
```

哈希表

## 哈希表
hashtable有了解吗？ hashtable实现有个负载因子，有了解过吗？作用是什么？当负载因子大于某个值后会如何？什么是哈希冲突？大于某个值，hash冲突概率会变高，而不是说会出现哈希冲突，hash表怎么扩容？

redis rehash有了解吗？怎么实现的？redis 做了哪些特殊优化了解吗？

## 二叉树
二叉树：**<font style="color:rgb(37, 41, 51);">每个节点最多有两个孩子节点</font>**

### 满二叉树和完全二叉树，区别是什么？
**<font style="color:rgb(37, 41, 51);">满二叉树：</font>**<font style="color:rgb(37, 41, 51);"> 一个二叉树所有的非叶子节点都存在左右两个孩子，并且所有叶子节点都在同一层级上，这样的树被称为满二叉树。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1708774623689-8dfd63ac-04e8-4f30-a11a-084de765c515.png)

**<font style="color:rgb(37, 41, 51);">完全二叉树：</font>**<font style="color:rgb(37, 41, 51);"> 对于一个有n个节点的二叉树，按照层级顺序来编号，则所有节点的编号为从1到n。如果这个树的所有节点和同样深度的满二叉树的编号为1到n的节点位置相同，则这个二叉树为完全二叉树。</font>

<font style="color:rgb(37, 41, 51);">完全二叉树的特点：叶子结点只能出现在最下层和次下层，且最下层的叶子结点集中在树的左部。需要注意的是，满二叉树肯定是完全二叉树，而完全二叉树不一定是满二叉树。</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1708774704017-206bf624-52a9-4de4-8ee4-f353a5e87f6f.png)



### 二叉树反转，递归的终止条件是什么
终止条件是根节点为空，即递归到叶子节点了。

```go
func invertTree(root *TreeNode) *TreeNode {
	if root == nil {
		return root
	} 
    left := root.Left
    root.Left = root.Right
    root.Right = left
    root.Left = invertTree(root.Left)
    root.Right = invertTree(root.Right)
	
	return root
}
```

### 中序遍历二叉树？
### go 实现二叉树转链表
### 找到二叉搜索树的第k个结点
<font style="color:rgb(136, 136, 136);background-color:rgb(245, 245, 245);">限定语言：Javascript_V8、Python、C++、C#、Java、Go、C、Javascript、Php、Python 3</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。</font>

![](https://cdn.nlark.com/yuque/0/2021/png/543296/1622883138311-832257f5-3494-4257-8450-ced9b8770e86.png)





## 字符串
### 给定一个字符串，求字符串中的最长回文字符串
### 字符串的序列
第一题

> **给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。**
>
> **换句话说，第一个字符串的排列之一是第二个字符串的 子串 。**
>
> **示例 1：**
>
> **输入: s1 = "ab" s2 = "eidbaooo"**
>
> **输出: True**
>
> **解释: s2 包含 s1 的排列之一 ("ba").**
>
> **示例 2：**
>
> **输入: s1= "ab" s2 = "eidboaoo"**
>
> **输出: False**
>
> **提示：**
>
> **输入的字符串只包含小写字母**
>
> **两个字符串的长度都在 [1, 10,000] 之间**
>
> 
>
> **来源：力扣（LeetCode）**
>
> **链接：**[**https://leetcode-cn.com/problems/permutation-in-string**](https://leetcode-cn.com/problems/permutation-in-string)
>

### 字符串匹配
假设有如下字符串匹配模式：

+ 表示匹配一个字符，

* 表示匹配任意多个（0个或多个）字符，

请编写一个函数满足这两种符号。如“x+1yz*z” 匹配 “xy1yzxyyz”。

### 给定一个字符串，按照字符出现次数进行降序排列
输入: abacab

输出: aaabbc

### 输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"
## 数组
### 二分查找，循环实现和递归实现
```go
package binary_search

// BinarySearch 二分查找循环实现
func BinarySearch(nums []int, target int) int {
	start := 0
	end := len(nums) - 1
	for start < end {
		mid := (start + end) / 2
		if nums[mid] == target {
			return mid
		} else if target > nums[mid] {
			start = mid
		} else {
			end = mid
		}
	}
	return -1
}

// BinarySearch2 递归实现二分查找
func BinarySearch2(nums []int, target int) int {
	return BinarySearchByRange(nums, target, 0, len(nums)-1)
}

func BinarySearchByRange(nums []int, target, left, right int) int {
	mid := (left + right) / 2
	if target > nums[mid] {
		return BinarySearchByRange(nums, target, mid+1, right)
	} else if target < nums[mid] {
		return BinarySearchByRange(nums, target, left, mid-1)
	} else {
		return mid
	}
}

```

### 数组拆分
arr = [1, 3, 2, 5, 1]

a = [] b= []

将 arr 拆分到 a、b两个数组里面，a、b两个数组的和尽可能相等

### python 求无序数组第k小的元素
### 给定一个数字，返回它在有序数组中出现的次数（百度大搜二面）
```go
// NumberPositionInSortedArray3 二分查找，找到左右边界 时间复杂度: O(log n)
func NumberPositionInSortedArray3(nums []int, target int) int {
	leftIdx := binarySearchFindPosition(nums, target, true)
	if leftIdx == len(nums) || nums[leftIdx] != target {
		return 0
	}
	rightIdx := binarySearchFindPosition(nums, target, false)
	return rightIdx - leftIdx
}

func binarySearchFindPosition(nums []int, target int, left bool) int {
	low, high := 0, len(nums)
	for low < high {
		mid := low + (high-low)/2
		if nums[mid] > target || (left && nums[mid] == target) {
			high = mid
		} else {
			low = mid + 1
		}
	}
	return low
}
```

### 在一个整数的无序数组里，除了两个数字以外，其他数字都出现了两次，找到这两个出现一次的数字（百度大搜二面）
```go
// DoubleNumber map记录出现次数，时间复杂度 O(log n)
func DoubleNumber(nums []int) []int {
	m := make(map[int]int)
	for _, num := range nums {
		if _, ok := m[num]; ok {
			m[num]++
		} else {
			m[num] = 1
		}
	}
	var res []int
	for k, v := range m {
		if v == 1 {
			res = append(res, k)
		}
	}

	return res
}
```

## 矩阵
### 螺旋矩阵
<font style="color:rgb(136, 136, 136);background-color:rgb(245, 245, 245);">限定语言：Kotlin、Typescript、Python、C++、Groovy、Rust、Java、Go、C、Scala、Javascript、Ruby、Swift、Php、Python 3</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">给定一个m x n大小的矩阵（m行，n列），按螺旋的顺序返回矩阵中的所有元素。  
</font><font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">例如，  
</font><font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">给出以下矩阵：  
</font><font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">你应该返回[1,2,3,6,9,8,7,4,5]。</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">[     [ 1, 2, 3 ],     [ 4, 5, 6 ],     [ 7, 8, 9 ] ]</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);"></font>

### 矩阵最小路径
<font style="color:rgb(51, 51, 51);">给定一个n*m 的矩阵 a，从左上角开始每次只能向右或者向下走，最后到达右下角的位置，路径上所有的数字累加起来就是路径和，输出所有的路径中最小的路径和。</font>

<font style="color:rgb(51, 51, 51);">示例1 输入输出示例仅供调试，后台判题数据一般不包含示例</font>

<font style="color:rgb(51, 51, 51);">输入</font>

<font style="color:rgb(51, 51, 51);">[[1,35,9],[8,1,3,4],[5,0,6, 1],[8 ,8,4, 0]]</font>

<font style="color:rgb(51, 51, 51);">输出</font>

<font style="color:rgb(51, 51, 51);">12</font>

## 求一个64进制数的2进制长度
## 快速排序（百度大搜二面）
```go
func QuickSort(nums []int) {
	if len(nums) < 2 {
		return
	}
	// 选择一个基准值
	pivot := nums[0]
	// 分区
	left, right := 0, len(nums)-1
	for i := 1; i <= right; {
		if nums[i] < pivot {
			nums[left], nums[i] = nums[i], nums[left]
			left++
			i++
		} else {
			nums[right], nums[i] = nums[i], nums[right]
			right--
		}
	}
	// 递归地对左右两个分区进行快速排序
	QuickSort(nums[:left])
	QuickSort(nums[left+1:])
}
```

## 跳台阶，一次可以跳一级或者两级，跳n阶有多少种跳法
```go
// map 记录中间结果
func climbStairs(n int) int {
    m := make(map[int]int)
    m[1] = 1
    m[2] = 2
    for i:=3;i<=n;i++ {
        m[i] = m[i-1] + m[i-2]
    }
    return m[n]
}

// 滚动数组
func climbStairs(n int) int {
    p,q,r := 0,0,1
    for i:=1;i<=n;i++ {
        p = q
        q = r
        r = p+q
    }
    return r
}
```

## go 实现 生产者消费者，交替打印0-10 （滴滴、华云数据）
```go
package main

import (
	"errors"
	"fmt"
	"sync"
	"time"
)

func Producer(c chan int, errChan chan error, wg *sync.WaitGroup) {
	defer wg.Done()
	counter := 0
	for {
		c <- counter
		fmt.Printf("send %d\n", counter)
		time.Sleep(1 * time.Second)
		if counter == 10 {
			errChan <- errors.New("send failed, stop")
			close(c)
			close(errChan)
			return
		}
		counter++
	}
}

func Consumer(c chan int, errChan chan error, wg *sync.WaitGroup) {
	defer wg.Done()
	for {
		select {
		case value, ok := <-c:
			if ok {
				fmt.Printf("received %d\n", value)
			}
		case err, ok := <-errChan:
			if ok {
				fmt.Printf("err %v\n", err)
				return
			}
		}
	}
}

func Scheduler() {
	c := make(chan int, 1)
	errChan := make(chan error, 1)
	wg := sync.WaitGroup{}
	wg.Add(2)
	go Producer(c, errChan, &wg)
	go Consumer(c, errChan, &wg)
	wg.Wait()
}

func main() {
	Scheduler()
}

```

## 常见推荐算法有了解吗？
## GBDT 介绍下？
## 括号匹配
1.在显示外国作者姓名时，豆瓣会按照惯例展示国籍，如 [奥] 卡夫卡，[日] 村上春树 等。用户添加作者数据时使用括号可能不规范或不匹配，

如【德】，惠特曼[美]，[英]等；也可能有多国籍的作者，如 [美][加]。

假设括号类型只有四种：()，[]，【】,〔〕，

请使用你熟悉的编程语言将国籍信息从作者姓名字符串中去除，

考虑前述及其他可能的特殊情况。

## two sum （比心、道远课堂）
#### 暴力枚举
```go
func twoSum(nums []int, target int) []int {
	for i := 0; i < len(nums)-1; i++ {
		for j := i + 1; j < len(nums); j++ {
			if nums[i]+nums[j] == target {
				return []int{i, j}
			}
		}
	}
	return nil
}
```

#### 哈希表记录另一个值
```go
func twoSum2(nums []int, target int) []int {
	hashTable := make(map[int]int)
	for i, val := range nums {
		if v, ok := hashTable[target-val]; ok {
			return []int{i, v}
		}
		hashTable[val] = i
	}
	return nil
}
```

## 手写栈实现，push,pop,min
## go 实现stack的push pop size
### 货币找钱
时间限制:C/C++ 1秒，其他语言 2秒

空间限制:C/C++ 32768K，其他语言 65536K64bit l0 Format: %lld

本题可使用本地IDE编码，不能使用本地已有代码，无跳出限制，编码后请点击“保存并调试”按钮进行代码提交。

题目描述

给定数组arr,arr中所有的值都为正整数且不重复,每个值代表一种面值的货币,每种面值的货币可以使用任意张,给定一个整数num代表要找的钱数,求组成num的最少货币数.

输入描述:

输入一个所有的值都为正整数且不重复的数组

输出描述:

组成num最少的货币数

### 合法的括号串
题目描述

对于一个字符串，请设计一个算法，判断其是否为一个合法的括号串。给定一个字符串A和它的长度n，请返回一个bool值代表它是否为一个合法的括号串。

一个合法的括号串定义为:1.只包括括号字符;2.左括号和右括号--对应测试样例:

"(()())”,6

返回:true

## LFU缓存结构设计
<font style="color:rgb(136, 136, 136);background-color:rgb(245, 245, 245);">限定语言：Kotlin、Typescript、Python、C++、Groovy、Rust、Java、Go、C、Scala、Javascript、Ruby、Swift、Php、Python 3</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">一个缓存结构需要实现如下功能。</font>

+ <font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">set(key, value)：将记录(key, value)插入该结构</font>
+ <font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">get(key)：返回key对应的value值</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">但是缓存结构中最多放K条记录，如果新的第K+1条记录要加入，就需要根据策略删掉一条记录，然后才能把新记录加入。这个策略为：在缓存结构的K条记录中，哪一个key从进入缓存结构的时刻开始，被调用set或者get的次数最少，就删掉这个key的记录；</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">如果调用次数最少的key有多个，上次调用发生最早的key被删除</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">这就是LFU缓存替换算法。实现这个结构，K作为参数给出</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">[要求]</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">set和get方法的时间复杂度为O(1)</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">若opt=1，接下来两个整数x, y，表示set(x, y)  
</font><font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">若opt=2，接下来一个整数x，表示get(x)，若x未出现过或已被移除，则返回-1</font>

<font style="color:rgb(51, 51, 51);background-color:rgb(245, 245, 245);">对于每个操作2，输出一个答案</font>

示例1

输入

[[1,1,1],[1,2,2],[1,3,2],[1,2,4],[1,3,5],[2,2],[1,4,4],[2,1]],3

输出

[4,-1] 

说明

在执行"1 2 4"后，"1 1 1"被删除。因此第二次询问的答案为-1

## go 实现 LRU


# Linux 系统
### 常用的linux命令？
du 

dh

top

head 

tail

vmstat

pidstat

### 管道输入输出，将一个文件的前30行写入另一个文件的末尾
```shell
head -30 a.txt >> b.txt
```

### 获取文件内容并获取文件行数
```shell
cat a.txt | wc -l
```

### linux 性能分析常用命令
### top 和 iotop
### lsof netstat iotop
### 查看 线程磁盘 IO 写入读取情况命令
```go
iotop -oP
PID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    COMMAND
39724 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % containerd-shim-~d/containerd.soc
43827 be/4 root        0.00 B/s   18.11 K/s  0.00 %  0.00 % containerd-shim-~d/containerd.soc
Total DISK READ :	0.00 B/s | Total DISK WRITE :	   14.65 K/s
Actual DISK READ:	0.00 B/s | Actual DISK WRITE:       0.00 B/s
```

### 有一个 service，端口被一个agent占用了，在不关掉agent不修改service端口情况下，如何启动这个service？
### linux熟悉吗？ 有个access.log, 用linux命令统计订单号出现的多少次？
```c
cat access.log | grep 'order_id' | wc -l
```

### 从A服务器copy文件到B服务器命令
```go
scp username@A_server:/file.txt username@B_server:/home/user/
```

# 编程语言
## Golang
### 基础数据结构
#### 数组
```shell
arr1 := [3]int{1, 2, 3} // 显式指定长度
arr2 := [...]int{1, 2, 3} // 编译器进行上限推导
```

<font style="color:rgb(0, 0, 0);">在不考虑逃逸分析的情况下，如果数组中元素的个数小于或者等于 4 个，那么所有的变量会直接在栈上初始化，如果数组元素大于 4 个，变量就会在静态存储区初始化然后拷贝到栈上，这些转换后的代码才会继续进入</font>[中间代码生成](https://draveness.me/golang/docs/part1-prerequisite/ch02-compile/golang-ir-ssa/)<font style="color:rgb(0, 0, 0);">和</font>[机器码生成](https://draveness.me/golang/docs/part1-prerequisite/ch02-compile/golang-machinecode/)<font style="color:rgb(0, 0, 0);">两个阶段，最后生成可以执行的二进制文件。</font>

<font style="color:rgb(0, 0, 0);">Go 对数组的访问和赋值需要同时依赖编译器和运行时，它的大多数操作在</font>[<font style="color:rgb(0, 0, 0);">编译期间</font>](https://draveness.me/golang/docs/part1-prerequisite/ch02-compile/golang-compile-intro/)<font style="color:rgb(0, 0, 0);">都会转换成直接读写内存，在中间代码生成期间，编译器还会插入运行时方法 </font>[<font style="color:rgb(0, 0, 0);">runtime.panicIndex</font>](https://draveness.me/golang/tree/runtime.panicIndex)<font style="color:rgb(0, 0, 0);"> 调用防止发生越界错误。</font>

### slice 介绍、原理、怎么扩容、底层实现
#### 数据结构
```go
type SliceHeader struct {
    Data uintptr
    Len  int
    Cap  int
}
```

+ <font style="color:rgb(0, 0, 0);">Data 是指向数组的指针;</font>
+ <font style="color:rgb(0, 0, 0);">Len</font><font style="color:rgb(0, 0, 0);"> </font><font style="color:rgb(0, 0, 0);">是当前切片的长度；</font>
+ <font style="color:rgb(0, 0, 0);">Cap 是当前切片的容量，即 Data 数组的大小：</font>

#### 切片扩容
<font style="color:rgb(0, 0, 0);">在分配内存空间之前需要先确定新的切片容量，运行时根据切片的当前容量选择不同的策略进行扩容：</font>

1. <font style="color:rgb(0, 0, 0);">如果期望容量大于当前容量的两倍就会使用期望容量；</font>
2. <font style="color:rgb(0, 0, 0);">如果当前切片的长度小于 1024 就会将容量翻倍；</font>
3. <font style="color:rgb(0, 0, 0);">如果当前切片的长度大于 1024 就会每次增加 25% 的容量，直到新容量大于期望容量；</font>

### go 比较两个slice是否相等
```go
func slicesEqual(slice1, slice2 []int) bool {
    // 使用反射库进行比较
    return reflect.DeepEqual(slice1, slice2)
}

func slicesEqual(slice1, slice2 []int) bool {
    // 首先比较两个 slice 的长度
    if len(slice1) != len(slice2) {
        return false
    }

    // 逐个比较每个元素的值
    for i := range slice1 {
        if slice1[i] != slice2[i] {
            return false
        }
    }

    return true
}
```

#### golang 比较字节数组是否相等
```go
import "bytes"

func main() {
    // 定义两个字节数组
    byteArray1 := []byte{1, 2, 3, 4}
    byteArray2 := []byte{1, 2, 3, 4}

    // 比较两个字节数组是否相等
    isEqual := bytes.Equal(byteArray1, byteArray2)
    if isEqual {
        fmt.Println("字节数组相等")
    } else {
        fmt.Println("字节数组不相等")
    }
}

```

#### go 字符串转换成 io.Reader
```go
package main

import (
	"fmt"
	"io"
	"strings"
)

func main() {
	str := "Hello, world!"
	// 将字符串转换为 io.Reader 接口
	reader := strings.NewReader(str)

	// 使用 reader 读取字符串内容
	buf := make([]byte, len(str))
	_, err := reader.Read(buf)
	if err != nil && err != io.EOF {
		// 处理读取错误
	}
	// 输出读取的内容
	fmt.Println(string(buf))
}

```

### new和make的区别：
二者都是内存的分配（堆上），但是make只用于slice、map以及channel的初始化（非零值）；而new用于类型的内存分配，并且内存置为零。

### go 内存分区
##### 栈区(Stack)
空间较小，要求数据读写性能高，数据存放时间较短暂。由编译器自动分配和释放，存放函数的参数值、函数的调用流程方法地址、局部变量等(局部变量如果产生逃逸现象，可能会挂在在堆区)

##### 堆区(heap):
空间充裕，数据存放时间较久。一般由开发者分配及释放(但是Golang中会根据变量的逃逸现象来选择是否分配到栈上或堆上)，启动Golang的GC由GC清除机制自动回收。

##### 全局区-静态全局变量区: 
全局变量的开辟是在程序在`main`之前就已经放在内存中。而且对外完全可见。即作用域在全部代码中，任何同包代码均可随时使用，在变量会搞混淆，而且在局部函数中如果同名称变量使用`:=`赋值会出现编译错误。全局变量最终在进程退出时，由操作系统回收。我们在开发的时候，尽量减少使用全局变量的设计

##### 全局区-常量区：
常量区也归属于全局区，常量为存放数值字面值单位，即不可修改。或者说的有的常量是直接挂钩字面值的。

### map、map 扩容原理、map底层实现
#### map 实现原理(不限制语言)
我说hash实现，通过hash函数进行再散列，然后问 HashMap 扩容缩容策略，如果满了，怎么解决？我说复制到新的内存块，或者用多个hash函数，这块了解不多。。

#### go map 和 sync.map 区别对比、实现原理（阿里、蜻蜓FM、高途、中国电信）
#### go sync包其他模块、sync包里面的sync.map WaitGroup 实现
#### 说下锁底层实现原理？
### channel 使用的业务场景、原理、协程调度模型、channel同步实现
#### 有缓存channel和无缓存channel区别？（英语流利说、高途、映客直播、中国电信）
+  给一个 nil channel 发送数据，造成永远阻塞 
+  从一个 nil channel 接收数据，造成永远阻塞 
+  给一个已经关闭的 channel 发送数据，引起 panic 
+  从一个已经关闭的 channel 接收数据，如果缓冲区中为空，则返回一个零值 
+  无缓冲的 channel 是同步的，而有缓冲的channel是非同步的 

**口诀: 空读写阻塞，写关闭异常，读关闭空零**

### 业务中处理过多个channel读写共享变量或者go实现同步方案？
1. **使用互斥锁（Mutex）：** 可以使用 **sync.Mutex** 来保护共享变量，确保在读写时只有一个 goroutine 能够访问变量。通过在读写操作前后使用锁来保护共享变量的读写操作。
2. **使用读写锁（RWMutex）：** 如果共享变量的读操作远远多于写操作，可以使用 **sync.RWMutex** 来实现读写分离。读取时使用读锁（**RLock()**），写入时使用写锁（**Lock()**），这样可以提高并发性能。
3. **使用通道进行同步：** 可以使用带缓冲的通道作为信号量或同步器。例如，可以使用一个通道来控制同时执行的 goroutine 数量，或者使用两个通道实现信号的发送和接收，来进行同步操作。
4. **使用 WaitGroup：** 可以使用 **sync.WaitGroup** 来等待一组 goroutine 完成执行。通过 **Add()** 方法增加计数器，**Done()** 方法减少计数器，**Wait()** 方法等待计数器归零，从而实现同步。
5. **使用原子操作（Atomic Operations）：** 如果共享变量是基本数据类型，可以使用 **sync/atomic** 包中的原子操作函数来进行读写操作，从而避免使用锁。原子操作是一种不需要加锁的线程安全操作。
6. **使用 Context：** 可以使用 **context.Context** 来实现多个 goroutine 之间的通信和同步。通过传递 Context 实例，可以控制 goroutine 的生命周期，并在需要时取消或超时。

### goroutine 并发有了解吗、原理
### go 并发控制有哪些？、go并发实现（新浪、ucloud、作业帮、云智慧、蜻蜓FM、中国电信）
### goroutine 调度模型(GPM)？（新浪微博一面和二面、蜻蜓FM、ucloud、英语流利说）
### go 协程阻塞后，会让出cpu吗
在 Go 语言中，如果一个协程被阻塞（例如因为等待 I/O 操作或者等待通道的数据），它**会让出 CPU 给其他协程执行，而不会占用 CPU 时间片。这是因为 Go 的调度器采用的是协作式调度（cooperative scheduling），而不是抢占式调度（preemptive scheduling）**。

协作式调度意味着协程在执行过程中需要显式地让出 CPU 时间片给其他协程，通常是在发生阻塞的情况下自动让出。当一个协程被阻塞时（例如等待 I/O 操作完成或者等待通道数据），Go 运行时会将该协程标记为不可运行状态，并将控制权转移到其他可运行的协程上。

这种调度方式的优势是避免了抢占式调度可能引入的上下文切换开销，因为协程只有在显式地让出 CPU 时间片时才会发生切换。然而，也有一个潜在的风险，即如果一个协程长时间不主动让出 CPU，可能会影响其他协程的执行，甚至导致整个程序的性能下降。

### golang 多层嵌套循环，如何跳出这个这层循环
标签（label）和 **goto** 语句来跳出多层嵌套的循环

```go
package main

import "fmt"

func main() {
OuterLoop:
	for i := 0; i < 5; i++ {
		for j := 0; j < 5; j++ {
			fmt.Printf("i: %d, j: %d\n", i, j)
			if i == 2 && j == 2 {
				break OuterLoop
			}
		}
	}
	fmt.Println("Finished")
}
```

### go gc 实现有了解吗，三色标记？（新浪微博、小米、阿里）
+ **GoV1.3- 普通标记清除**法，整体过程需要启动STW，效率极低。
+ **GoV1.5- 三色标记法， 堆空间启动写屏障**，栈空间不启动，全部扫描之后，需要重新扫描一次栈(需要STW)，效率普通
+ **GoV1.8-三色标记法，混合写屏障机制**， 栈空间不启动，堆空间启动。整个过程几乎不需要STW，效率较高。

**栈空间通常不需要启动垃圾回收，因为栈上的对象生命周期是可预测的，它们通常在函数调用结束时被销毁，而不需要垃圾回收器的介入**。

相比之下，**堆空间中的对象生命周期不可预测，它们的分配和释放由运行时系统动态管理。因此，垃圾回收器需要定期扫描堆空间**，标记哪些对象是可达的，哪些是不可达的，并释放不可达对象占用的内存空间。这样可以防止堆空间中的内存泄漏，并确保程序的内存使用效率。

#### 一、go v1.3 之前 标记-清除(mark and sweep)算法
##### 标记清除执行过程
+ 标记(Mark phase)
+ 清除(Sweep phase)
1. 暂停程序业务逻辑, 分类出可达和不可达的对象，然后做上标记。
2. 开始标记，程序找出它所有可达的对象，并做上标记。
3. 标记完了之后，然后开始清除未标记的对象，不可达对象被清理。
    1. **标记清除算法在执行的时候，需要程序暂停**！即 `STW(stop the world)`，**STW 的过程中，CPU不执行用户代码，全部用于垃圾回收**，这个过程的影响很大，所以STW也是一些回收机制最大的难题和希望优化的点。所以在执行第三步的这段时间，程序会暂定停止任何工作，卡在那等待回收执行完毕。
4. 停止暂停，让程序继续跑。然后循环重复这个过程，直到 process 程序生命周期结束

##### 标记-清除缺点
+ STW，stop the world；让程序暂停，程序出现卡顿 **(重要问题)**；
+ 标记需要扫描整个heap；
+ 清除数据会产生heap碎片

Go V1.3 做了简单的优化,将STW的步骤提前, 减少STW暂停的时间范围

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1709035178264-45f81560-1aac-4ef6-b584-9eaad63451eb.png)

上图主要是将STW的步骤提前了一步，因为在Sweep清除的时候，可以不需要STW停止，因为这些对象已经是不可达对象了，不会出现回收写冲突等问题。

但是无论怎么优化，Go V1.3都面临这个一个重要问题，就是**mark-and-sweep 算法会暂停整个程序** 。

#### 二、Go v1.5 三色并发标记法
Golang 中的垃圾回收主要应用三色标记法，GC过程和其他用户 goroutine 可并发运行，但需要一定时间的**STW(stop the world)**，**三色标记法**通过三个阶段的标记来确定清楚的对象都有哪些。我们来看一下具体的过程。

1. **每次新创建的对象，默认的颜色都是标记为“白色”**
2. **每次GC回收开始, 会从根节点开始遍历所有对象，把遍历到的对象从白色集合放入“灰色”集合**

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1709035416086-2195e106-339c-4776-9603-ec12f61c5274.png)

这里 要注意的是，本次遍历是一次遍历，非递归形式，是从程序抽次可抵达的对象遍历一层，如上图所示，当前可抵达的对象是对象1和对象4，那么自然本轮遍历结束，对象1和对象4就会被标记为灰色，灰色标记表就会多出这两个对象。

3. **遍历灰色集合，将灰色对象引用的对象从白色集合放入灰色集合，之后将此灰色对象放入黑色集合。**
    1. 这一次遍历是只扫描灰色对象，将灰色对象的第一层遍历可抵达的对象由白色变为灰色。
4. **重复第三步, 直到灰色中无任何对象。**
    1. 当我们全部的可达对象都遍历完后，灰色标记表将不再存在灰色对象，目前全部内存的数据只有两种颜色，黑色和白色。那么黑色对象就是我们程序逻辑可达（需要的）对象，这些数据是目前支撑程序正常业务运行的，是合法的有用数据，不可删除，白色的对象是全部不可达对象，目前程序逻辑并不依赖他们，那么白色对象就是内存中目前的垃圾数据，需要被清除。
5. **回收所有的白色标记表的对象**. 也就是回收垃圾。

这里面可能会有很多并发流程均会被扫描，执行并发流程的内存可能相互依赖，为了在GC过程中保证数据的安全，我们在开始三色标记之前就会加上STW，在扫描确定黑白对象之后再放开STW。但是很明显这样的GC扫描的性能实在是太低了。

#### 三、没有STW的三色标记法
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1709036403983-e8250877-45e4-4b9f-a5b0-1f780e8191f8.png)

在三色标记法中，下面的是不希望被发生的。

+ 条件1: 一个白色对象被黑色对象引用**(白色被挂在黑色下)**
+ 条件2: 灰色对象与它之间的可达关系的白色对象遭到破坏**(灰色同时丢了该白色)**  
如果当以上两个条件同时满足时，就会出现对象丢失现象!

并且，如图所示的场景中，如果示例中的白色对象3还有很多下游对象的话, 也会一并都清理掉。

为了防止这种现象的发生，最简单的方式就是STW，直接禁止掉其他用户程序对对象引用关系的干扰，但是**STW的过程有明显的资源浪费，对所有的用户程序都有很大影响**。那么是否可以在保证对象不丢失的情况下合理的尽可能的提高GC效率，减少STW时间呢？答案是可以的，我们只要使用一种机制，尝试去破坏上面的两个必要条件就可以了。

#### 四、屏障机制
GC回收器，满足下面两种情况之一时，即可保对象不丢失。  这两种方式就是“强三色不变式”和“弱三色不变式”。

##### “强-弱” 三色不变式
+ **强三色不变式：不存在黑色对象引用到白色对象的指针。**
    - 强制性的不允许黑色对象引用白色对象，这样就不会出现有白色对象被误删的情况

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1709036600243-e16b1fd5-e6a0-4a6c-8e35-20864df76ff3.png)

+ **弱三色不变式：所有被黑色对象引用的白色对象都处于灰色保护状态**
    - 黑色对象可以引用白色对象，但是这个白色对象必须存在其他灰色对象对它的引用，或者可达它的链路上游存在灰色对象。 这样实则是黑色对象引用白色对象，白色对象处于一个危险被删除的状态，但是上游灰色对象的引用，可以保护该白色对象，使其安全。

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1709036630134-cb594778-5d23-4619-a3d6-e2484035ad0f.png)

为了遵循上述的两个方式，GC算法演进到两种屏障方式，他们“插入屏障”, “删除屏障”

##### 插入屏障
`具体操作`: 在A对象引用B对象的时候，B对象被标记为灰色。(将B挂在A下游，B必须被标记为灰色)

`满足`: **强三色不变式**. (不存在黑色对象引用白色对象的情况了， 因为白色会强制变成灰色)

##### 1.3. 删除屏障 
`具体操作`: 被删除的对象，如果自身为灰色或者白色，那么被标记为灰色。

`满足`: **弱三色不变式**. (保护灰色对象到白色对象的路径不会断)

回收精度低，一个对象即使被删除了最后一个指向它的指针也依旧可以活过这一轮，在下一轮GC中被清理掉。

#### 五、Go v1.8 混合写屏障(hybrid write barrier)机制
插入写屏障和删除写屏障的短板：

+  插入写屏障：结束时需要STW来重新扫描栈，标记栈上引用的白色对象的存活； 
+  删除写屏障：回收精度低，GC开始时STW扫描堆栈来记录初始快照，这个过程会保护开始时刻的所有存活对象。 

Go V1.8版本引入了混合写屏障机制（hybrid write barrier），避免了对栈re-scan的过程，极大的减少了STW的时间。结合了两者的优点。

##### 混合写屏障规则
`具体操作`:

1、GC开始将栈上的对象全部扫描并标记为黑色(之后不再进行第二次重复扫描，无需STW)，

2、GC期间，任何在栈上创建的新对象，均为黑色。

3、被删除的对象标记为灰色。

4、被添加的对象标记为灰色。

`满足`: 变形的**弱三色不变式**.

注意混合写屏障是Gc的一种屏障机制，所以只是当程序执行GC的时候，才会触发这种机制

### 对 go 哪些方面有深入了解介绍下？
### context 有了解吗？应用场景？（英语流利说、ucloud、百度萝卜快跑一面）
#### 使用场景
+ **传递上下文信息**： 当一个操作涉及到多个 goroutine，并且这些 goroutine 需要共享上下文信息时，可以使用 context 包来传递上下文信息。
+ **控制取消操作**： context 包提供了一种机制来控制 goroutine 的取消操作。通过取消上下文，可以通知相关的 goroutine 停止执行任务，释放资源，以避免资源泄漏。
+ **超时和截止日期**： 可以使用 context 包来设置操作的超时时间或截止日期，以确保操作在一定时间内完成，避免长时间阻塞。

#### 接口实现
+ Deadline()： 用于获取上下文的截止时间。在超过这个时间后，相关操作应该停止执行。
+ Done()： 用于接收上下文的完成信号。当上下文被取消或者超时时，通过该通道可以接收到信号，从而及时停止执行相应的操作。
+ Err()： 用于获取导致上下文被取消的原因。通常情况下，会返回一个错误值，用于描述上下文被取消的具体原因。
+ Value()： 用于在上下文中传递请求范围的值。通过这个方法，可以将一些请求相关的信息传递给处理请求的各个 goroutine。

#### cancelFunc 
+ **手动取消上下文**： 在某些情况下，当某个任务已经完成或者出现了错误，我们可能希望取消与这个任务相关的所有操作。此时，可以调用 cancelFunc 函数来手动取消上下文，通知相关的 goroutine 停止执行。
+ **在 defer 中调用取消**： 在一些需要保证资源释放的场景中，可以在 defer 语句中调用 cancelFunc 函数，以确保在函数返回之前取消相应的上下文，释放资源。
+ **取消子上下文**： 在使用 context.WithCancel()、context.WithDeadline() 或 context.WithTimeout() 创建上下文时，返回的 cancelFunc 函数可以用来取消相应的子上下文。这样可以在需要时取消整个请求处理链中的某个子操作。
+ **错误处理**： 在处理某些特定错误时，可能会需要取消相关的操作。通过调用 cancelFunc 函数，可以及时取消相关的上下文，避免资源泄漏或者进一步的错误扩散。

### 用go实现 url路由参数？后面的参数解析
name=xxx&name=222&age=xxx&token=dsjsdhggf

### go实现字符串匹配算法
### python 和 go 多进程、多线程、协程实现原理，对比
### grpc 有了解吗？
### gprc有用吗，流式的还是？
### gprc 你们是用的什么场景，一次传输的数据量有多大？
## Python
### args kwargs 区别
### try catch else finally 
### 写个cached装饰器，可以传参 timeout
### list 和 tuple 区别
### class
```python
class A:
    num = 1
a = A()
a.num =10
A.num = ?
```

### 深拷贝浅拷贝
```python
l = [1,2,3,4]
l2 = l[:]
l3 = copy(l)
l4 = deepcopy(l)
执行 l = [1,1,1]
问 l2 l3 l4改变了吗
```

### celery、celery异步队列、应用场景
### Django源码看过吗，ORM的filter，是如何把filter里面的很多参数转化为sql的
### django看过哪些模块实现？flask 实现看过吗？介绍下django中间件，除了django看过其他实现吗，对比下django和flask
### 介绍下 django 请求过程，ORM和原生sql你们用的哪个？直接写sql会使用哪些方法？
### django rest framework
### flask Router wsgi 线程
### python 生成器
### 装饰器、[1,2,3] 装饰器实现 [1,4,9]、装饰器应用场景(乐言、新浪微博)
### 手写打印时间的 python 装饰器实现（b站）
### 迭代器
### python运算符重载
### django urls 请求经过哪些模块，怎么处理的
### django orm 和执行sql
### Python2 和 Python3 GIL 线程机制,GIL等待多长时间后会释放
### python coroutine 和 goroutine 区别
### python 协程 gevent库 
### python 垃圾回收机制
### python 进程、线程、协程 和go作对比
## Java
### java里面hashmap实现
## JavaScript 
### null 和undefined区别


# Web
## 通用
### GRPC 优点，为何轻量？
### 微服务和服务发现
### 前后端数据交互方式
### graphql 有了解吗，相比restapi有哪些好处？数据无限嵌套的数据，graphql有哪些优势？


### ORM n+1 查询
```python
from django.db import models
class User(models.Model):
    name = models.CharField(max_length=255)
class Post(models.Model):
    owner = models.ForeignKey(User)   # by the5fire
    title = models.CharField(max_length=255)
    content = models.TextField()
```

有10个用户，每个用户都写了一篇文章，需要分页查询文章。

我们有一个需求，展示一个文章列表页，列表页上展示的信息包括：文章标题，文章作者名称。就这两个字段，也不需要分页。

直观做法

```python
posts = Post.objects.all()  #  获取所有的文章数据，注意此时不会执行sql语句  by the5fire
result = []
for post in posts:   # 此时会执行select * from post的查询
    result.append({
        'title': post.title,
        'owner': post.owner.name,  # 此时会执行  select * from user where user_id = <post.user_id>
    })
```

上面代码会查询一次post，假设posts 有n个，就需要查询 n 次 user，执行 n +1 次查询

sql 实现上面需求

```sql
SELECT t1.title, t2.name from post as t1 
INNER JOIN user as t2 ON t2.id = t1.owner_id;
```

<font style="color:rgb(25, 27, 31);">在 Django中，对这类问题就是通过select_related来解决。上面的代码直接改造为:</font>

```python
posts_with_user = Post.objects.all().select_related('user')
```

<font style="color:rgb(25, 27, 31);">这样产生的语句就是上面的那个 JOIN 语句。当然ORM还提供了其他类似的方法，比如prefetch_related，又是用来处理其他的问题。</font>

[gorm]( https://gorm.io/zh_CN/docs/preload.html)<font style="color:rgb(25, 27, 31);"> 通过Preload 和 Joins解决这个问题</font>

```go
// Preload Orders with conditions
db.Preload("Orders", "state NOT IN (?)", "cancelled").Find(&users)
// SELECT * FROM users;
// SELECT * FROM orders WHERE user_id IN (1,2,3,4) AND state NOT IN ('cancelled');

db.Where("state = ?", "active").Preload("Orders", "state NOT IN (?)", "cancelled").Find(&users)
// SELECT * FROM users WHERE state = 'active';
// SELECT * FROM orders WHERE user_id IN (1,2) AND state NOT IN ('cancelled');
```

## 前端
### npm怎么装包，npm怎么装echarts包并且引入包，怎么清除缓存
装包

```shell
npm install echarts --save
```

引入包

```javascript
import * as echarts from 'echarts';
```

清除 npm 缓存

```shell
$ npm cache clean --force
```

### vue生命周期(得物、比心)
### js 跨域解决
### http method ，get post区别
### 前端发请求用什么，我说axios
+ http
    - fetch
    - Promise
+ websocket
+ sse(EventStream)

## 后端
### 微服务
### 微服务是怎样的概念？你们拆分粒度？
### 微服务间链路追踪有了解吗，一个请求过来，怎么追踪的，spanid有了解吗？
### http 
http 状态码 500是什么？

500 

501 

503

### nginx 熟悉吗？nginx负载均衡算法实现？
### http 和 rpc对比
### 你了解的负载均衡实现，有哪些区别？
# 数据库
## MySQL
### 数据结构
B树、B+树、AVL、红黑树

mysql innodb 引擎，数据存储达到多少条，性能急剧下降 2100多万条，因为树高度变高

你们数据库是什么？mysql了解多吗？mysql用的什么存储引擎？介绍下 InnoDB索引结构？

索引长度和B+树高度有关系吗？mysql 为何用B+树？什么是二叉查找树？什么是平衡二叉树？avl怎么实现的？B树原理？B+树实现原理？

#### mysql json 数据类型有了解吗，json数据类型可以建立索引吗？
在MySQL中，JSON数据类型是用于存储JSON格式数据的一种数据类型。JSON数据类型在MySQL 5.7及更高版本中引入。JSON字段可以包含合法的JSON数据，包括对象、数组、字符串、数字、布尔值和**null**。JSON数据类型的引入使得在MySQL中存储和查询JSON格式的数据更加方便。

至于索引，**MySQL 5.7及更新版本**开始支持对JSON列的索引。你可以在JSON列上创建普通索引、唯一索引、全文索引等，以提高查询性能。

MySQL 5.6及以下的不支持json数据类型创建索引

### 锁
mysql 有哪些锁，怎么实现事务隔离的，我说mvcc，介绍下mvcc

有哪些锁？乐观锁和悲观锁介绍下？

### 事务
mysql 事务是怎样的概念？事务隔离级别？幻读了解吗？原因？

讲下mysql事务？讲下可重复读在一个事务里面的一致性读是怎么实现的？事务里面的一致性是怎么实现的？原子性如何实现？对redo log binlog有了解吗？事务日志还有 undo log，介绍下，可以实现哪些功能，他是实现mvcc的原理

介绍下mysql mvcc

### 索引与优化
mysql 聚簇索引和非聚簇索引区别

索引下推和最左匹配原则

索引优化（云智慧、比心）

表A 有a,b,c字段，abc是联合索引

select xxx from table where b=xxx and c= aaa or a = xxx

sql执行效率，存在什么问题

建联合索引需要注意哪些？

讲讲索引结构类型？这些索引区别？

mysql 有哪些索引，哪些情况索引不会命中？ like 查询哪种情况可以命中索引？

mysql 主从复制了解吗，介绍下？主主复制有了解吗？分库分表的工具你们用的什么？DDL、DML相关工具有了解吗？面试官说 ghost， 主从复制过程中如果master宕机了，如何确保数据一致性？mysql InnoDB引擎实现，B+树介绍下？二级索引回表查询问题？

mysql 索引 f1 > ? AND f2 = ?f2 > ? AND f3 < ? 如何设计？

### 主从复制
#### 主从延迟常见原因
+ 主库和从库规格配置不一致(例如从库配置低，apply binlog较慢)
+ 主从刷脏页、落盘等参数不一致
+ 主库上有大事务执行(例如大表DDL)
+ mysql 版本较老，从库未使用多线程并发回放(5.6库级，5.7事务级)
+ mysql所在宿主机系统时钟问题
+ 从库上有慢 sql，占用大量计算资源，导致从库性能降低，无法 apply 主库binlog
+ 表没有主键，没有唯一键

IO延迟异常原因？

mysql binlog原理？

如何确保mysql 和es数据一致性？

mysql 是个主从集群，有三列，id,name age id 是从21 22 23 24 25，name是1,2,3,4,5

update set id=21 where name =3,讲下这个sql到mysql执行层面有哪些操作？

你说先写binlog，看你用过canal，那canal也是把自己伪装成slave，那此时是不是可以把binlog传入canal，如果此时在slave执行完了，假设redo log写失败了，binlog流到从库，这时候发现主从数据不一致，这个可以接受的吗？

再举个例子，就是redolog写失败了，下游slave能收到标志位，把update写进去了，这种怎么解决？

在失败情况下commit失败，读master读不到，读从读不到，如何解决？

mysql一主两从，假设主库挂了， 如何判断主库挂了，从库上线？如何判断主节点宕掉了？如果判断出来主节点挂掉了，直接写从，你感觉有问题吗？如何判断主节点是挂了还是主从连接不上？你刚才说刷脏页是2g刷，你确定吗？

### 性能优化
mysql 分页，页码很大，查询怎么优化？

我说分库分表，面试官说如果查询结果本身数据量就很大，怎么解决，我说加索引。。这块了解不多

如何定位数据库慢查询？具体介绍下你们场景实例？

你们对数据库有做分库分表，介绍下？分库分表后的优势和劣势？

说下sql优化，分库分表，读写分离，缓存

介绍下数据库查询优化具体怎么优化的？，单表两三亿数据为何不分库分表

数据库性能优化

介绍下分库分表

分表怎么做的？

你们sql查询校验怎么做的，直接执行吗？delete update 的危险操作，你们怎么校验的

OLAP、OLTP有了解吗，适用于哪些场景？你做过哪些针对性的优化？

你们mysql主要是哪些业务用

mysql 查询优化，分库分表，B树和B+树对比

## Redis 
### 数据结构
string、set、zset、hash、sortedset、geo

redis pipeline有了解吗？

redis 有了解吗，redis 查询怎么实现的

redis 事务

redis hash扩容有了解吗，hash装载因子？

redis为何这么快，执行效率高？多线程为何有锁？我说单线程是为了确保数据一致性。。。面试官问单线程怎么不能确保数据一致性了？数据一致性和单线程多线程没关系吧。。

介绍下redis 数据类型 string list set hash zset geo 说下zset做排行榜排名一样，怎么排名的，我说随机的。。zset怎么实现的？我说跳跃链表？

跳跃链表实现介绍下，设计思想？

Redis zset 实现，为啥用跳跃链表不用红黑树

redis geo 地理数据类型应用场景？如何实现坐标的范围查询？

redis sds数据结构有了解吗？ sds解决了什么问题？字符串溢出优化怎么做的

list 底层哪三种数据结构实现的？分别解决了什么问题？

### 部署架构
redis 哨兵模式

redis 集群方式？ 主从，哨兵实现原理

### 数据持久化
#### AOF
#### RDB
aof和rdb优劣对比

### 过期删除策略
redis过期键的删除策略有了解吗？redis 如何删除过期键？

redis数据满了会怎么处理？

我说sds数据结构，数据满了会lru进行缓存淘汰，面试官说如果业务数据很重要，redis本身有策略如何解决这个问题，我不太清楚。。

lru

lfu

LRU 和实现原理 ? 底层数据结构是什么，如果让你实现的话你怎么实现？

lru新来一个请求，你怎么处理？LFU ?

高并发情况下，redis qps很高，rdb fork 子进程会占用大量内存，怎么优化？

### 业务场景应用
#### Redis 分布式锁


#### Redis 缓存
##### 缓存穿透
##### 缓存击穿
##### 缓存雪崩


#### 如何确保 MySQL 数据库和Redis 缓存的数据一致性？
#### Redis 热点 key 如何解决？
<font style="color:rgb(85, 85, 85);">热key是服务端的常见问题，指一段时间内某个key的访问量远远超过其他的key，导致大量访问流量落在某一个redis实例中；或者是带宽使用率集中在特定的key（例如，对一个包含2000个field的hash key每秒发送大量的hgetall操作请求）；又或者是cpu使用时间占比集中在特定的key（例如，对一个包含10000个field的key每秒发送大量的zrange操作请求）。以被请求频率来定义是否是热key，没有固定经验值。某个key被高频访问导致系统稳定性变差，都可以定义为热key。</font>

<font style="color:rgb(85, 85, 85);">可能造成的问题</font>

<font style="color:rgb(85, 85, 85);">热点缓存会导致流量集中，redis缓存与数据库被击穿，从而引发系统雪崩。</font>

<font style="color:rgb(85, 85, 85);">请求分配不均，存在热key的节点面临较大的访问压力，可能出现该数据分片的连接数被耗尽甚至宕机。（即使采取扩容也会对资源有很大的浪费）</font>

**<font style="color:rgb(85, 85, 85);">发现方法</font>**

<font style="color:rgb(85, 85, 85);">由于热key发生对系统稳定性有巨大危害，所以需要上线前设立故障预案、建立监控和报警机制，以便快速响应故障。</font>

1. <font style="color:rgb(85, 85, 85);">根据业务经验，预估哪些是热key。  
</font><font style="color:rgb(85, 85, 85);">优点：简单直接。  
</font><font style="color:rgb(85, 85, 85);">缺点：但并不是所有业务都能预估出哪些key是热key。</font>
2. <font style="color:rgb(85, 85, 85);">在客户端收集。在操作redis之前，加上统计频次的逻辑，然后将统计数据发送给一个聚合计算的服务进行统计。  
</font><font style="color:rgb(85, 85, 85);">优点：方案简单。  
</font><font style="color:rgb(85, 85, 85);">缺点：无法支持大公司多语言环境的SDK，或者说多语言SDK对齐比较困难。此外SDK的维护升级成本会很高。</font>
3. <font style="color:rgb(85, 85, 85);">在proxy层收集。有些服务在请求redis之前会请求一个proxy服务，这种场景可以使用在proxy层收集热key数据，收集机制类似于在客户端收集。  
</font><font style="color:rgb(85, 85, 85);">优点：方案对使用方完全透明；没有SDK多语言异构和升级成本高的问题。（不理解这个地方的话，可以查看小辉之前的博客《通用能力抽象选择SDK组还是API服务？》）  
</font><font style="color:rgb(85, 85, 85);">缺点：并不是所有场景都会有proxy层。</font>
4. <font style="color:rgb(85, 85, 85);">redis集群监控。如果出现某个实例qps倾斜，说明可能存在热key。  
</font><font style="color:rgb(85, 85, 85);">优点：不需要额外开发。  
</font><font style="color:rgb(85, 85, 85);">缺点：每次发生状况需要人工排查，因为热key只是导致qps倾斜的一种可能。</font>
5. <font style="color:rgb(85, 85, 85);">redis 4.0版本之后热点key发现功能。执行redis-cli时加上–-hotkeys选项即可。  
</font><font style="color:rgb(85, 85, 85);">优点：不需要额外开发。  
</font><font style="color:rgb(85, 85, 85);">缺点：该参数在执行的时候，如果key比较多，执行耗时会非常长，由此导致查询结果的实时性并不好。</font>
6. <font style="color:rgb(85, 85, 85);">redis客户端使用TCP协议与服务端进行交互。通过脚本监听端口，解析网络包并进行分析。  
</font><font style="color:rgb(85, 85, 85);">优点：对原有的业务系统没有改造。  
</font><font style="color:rgb(85, 85, 85);">缺点：开发成本高，维护困难，有丢包可能性。</font>

##### <font style="color:rgb(85, 85, 85);">redis 热点key解决方案</font>
###### <font style="color:rgb(85, 85, 85);">服务端缓存</font>
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1708420659551-cb8c035d-95a9-4748-9e2c-c78df3ab78f3.png)

<font style="color:rgb(24, 24, 24);">首先Client会将请求发送至Server上，而Server又是一个多线程的服务，本地就具有一个基于Cache LRU策略的缓存空间。当Server本身就拥堵时，Server不会将请求进一步发送给DB而是直接返回，只有当Server本身畅通时才会将Client请求发送至DB，并且将该数据重新写入到缓存中。此时就完成了缓存的访问跟重建。</font>

<font style="color:rgb(24, 24, 24);">但该方案也存在以下问题：</font>

+ <font style="color:rgb(24, 24, 24);">缓存失效，多线程构建缓存问题</font>
+ <font style="color:rgb(24, 24, 24);">缓存丢失，缓存构建问题</font>
+ <font style="color:rgb(24, 24, 24);">脏读问题</font>

###### <font style="color:rgb(24, 24, 24);">使用Memcache、Redis方案</font>
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1708420739956-41af81f5-3599-4703-b654-8e8abab3e3da.png)

<font style="color:rgb(24, 24, 24);">该方案通过在客户端单独部署缓存的方式来解决热点Key问题。使用过程中Client首先访问服务层，再对同一主机上的缓存层进行访问。该种解决方案具有就近访问、速度快、没有带宽限制的优点，但是同时也存在以下问题。</font>

+ <font style="color:rgb(24, 24, 24);">内存资源浪费</font>
+ <font style="color:rgb(24, 24, 24);">脏读问题</font>

###### <font style="color:rgb(24, 24, 24);">使用本地缓存方案</font>
<font style="color:rgb(85, 85, 85);">使用LFU数据结构并结合上面的发现方法，将最热topN的key进行统计，然后在client端使用本地缓存，从而降低redis集群对热key的访问量</font>

<font style="color:rgb(24, 24, 24);"> 存在以下问题：</font>

+ <font style="color:rgb(24, 24, 24);">需要提前获知热点</font>
+ <font style="color:rgb(24, 24, 24);">缓存容量有限</font>
+ <font style="color:rgb(24, 24, 24);">不一致性时间增长，</font><font style="color:rgb(85, 85, 85);">需要保证本地缓存和redis数据的一致性</font>
+ <font style="color:rgb(24, 24, 24);">热点Key遗漏</font>
+ <font style="color:rgb(85, 85, 85);">如果对所有热key进行本地缓存，那么本地缓存是否会过大，从而影响应用程序本身的性能开销</font>

###### <font style="color:rgb(85, 85, 85);">单个热点key打散为多个key（</font><font style="color:rgb(88, 88, 88);">建议该方案用来解决临时棘手的问题</font><font style="color:rgb(85, 85, 85);">）</font>
<font style="color:rgb(85, 85, 85);">将热key加上前缀或者后缀，把热key的数量从1个变成实例个数，利用分片特性将这n个key分散在不同节点上，这样就可以在访问的时候，采用客户端负载均衡的方式，随机选择一个key进行访问，将访问压力分散到不同的实例中。这个方案有个明显的缺点，就是缓存的维护成本大：假如有n为100，则更新或者删除key的时候需要操作100个key。</font>

###### <font style="color:rgb(85, 85, 85);">读写分离解决热点读</font>
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1708421591583-3f5cd241-86ff-497f-9cab-90fca72eb2c6.png)

架构做成主从(master-slave)架构，一主多从，主负责写，并且将数据复制到其它的slave 节点，从节点负责读。所有的读请求全部走从节点。这样也可以很轻松实现水平扩容，支撑读高并发

<font style="color:rgb(24, 24, 24);">架构中各节点的作用如下：</font>

+ <font style="color:rgb(24, 24, 24);">SLB层做负载均衡</font>
+ <font style="color:rgb(24, 24, 24);">Proxy层做读写分离自动路由</font>
+ <font style="color:rgb(24, 24, 24);">Master负责写请求</font>
+ <font style="color:rgb(24, 24, 24);">ReadOnly节点负责读请求</font>
+ <font style="color:rgb(24, 24, 24);">Replica节点和Master节点做高可用</font>

<font style="color:rgb(24, 24, 24);">实际过程中Client将请求传到SLB，SLB又将其分发至多个Proxy内，通过Proxy对请求的识别，将其进行分类发送。例如，将同为Write的请求发送到Master模块内，而将Read的请求发送至ReadOnly模块。而模块中的只读节点可以进一步扩充，从而有效解决热点读的问题。读写分离同时具有可以灵活扩容读热点能力、可以存储大量热点Key、对客户端友好等优点。</font>

利用读写分离，通过主从复制的方式，增加slave节点来实现读请求的负载均衡。这个方案明显的缺点就是使用机器硬抗热key的数据，资源耗费严重；而且引入读写分离架构，增加节点数量，都会增加系统的复杂度降低稳定性。

###### 使用分布式锁更新热点key
当读取时发现key过期后，使用分布式锁锁住这个数据的key，在redis 中直接使用setnx操作即可，对于获取到这个锁的线程，从数据库查询最新数据更新缓存，更新到热key中，其他线程采用重试策略，避免多个线程同时更新导致数据不一致。

<font style="color:rgb(13, 13, 13);">在业务高并发场景下，会存在多个线程同时尝试获取同一个业务热点key 的问题，这可能导致竞争条件，即多个线程最终会获取到同一个锁。这就需要在设计分布式锁时考虑解决这个问题。</font>

<font style="color:rgb(13, 13, 13);">一种解决方法是使用 Redis 的 Lua 脚本来确保释放锁的原子性。在 Redis 中，执行 Lua 脚本是原子性的，可以保证多个命令的执行不会被其他客户端的命令所打断。</font>

<font style="color:rgb(13, 13, 13);">golang 代码实现: </font>

```go
package main

import (
	"context"
	"fmt"
	"strconv"
	"sync"
	"time"

	"github.com/go-redis/redis/v8"
)

type RedisLock struct {
	RedisClient *redis.Client
	// 热点key的锁，多个分布式锁的key名相同
	Key        string
	ExpireTime time.Duration
	// uuid，通常为当前时间的毫秒时间戳
	LockedToken string
}

func NewRedisClient() *redis.Client {
	redisClient := redis.NewClient(&redis.Options{
		Addr:     "localhost:6379",
		Password: "", // no password set
		DB:       0,  // use default DB
	})
	return redisClient
}

func NewRedisLock(redisClient *redis.Client, key string, expireTime time.Duration) *RedisLock {
	return &RedisLock{
		RedisClient: redisClient,
		Key:         key,
		ExpireTime:  expireTime,
	}
}

func (lock *RedisLock) AcquireLock(ctx context.Context) (bool, error) {
	lock.LockedToken = fmt.Sprintf("%d", time.Now().UnixNano())
	return lock.RedisClient.SetNX(ctx, lock.Key, lock.LockedToken, lock.ExpireTime).Result()
}

func (lock *RedisLock) ReleaseLock() error {
	// 获取指定键的值，并与传入的参数进行比较。这样做的目的是为了确保当前脚本所持有的锁与传入的参数相匹配，
	// 即当前脚本所持有的锁仍然有效。如果不进行比较，而是直接删除指定的键，那么就无法确保当前脚本所持有的锁是有效的，
	// 可能会导致错误释放锁。因此，为了确保安全释放锁，需要先验证当前脚本所持有的锁与传入的参数是否匹配，
	// 只有在匹配的情况下才执行删除操作。
	luaScript := `
		if redis.call("GET", KEYS[1]) == ARGV[1] then
			return redis.call("DEL", KEYS[1])
		else
			return 0
		end
	`
	return lock.RedisClient.Eval(context.Background(), luaScript, []string{lock.Key}, lock.LockedToken).Err()
}

func QueryAndUpdateHotKey(bizName, hotKey string, newValue string) error {
	redisClient := NewRedisClient()
	lockKey := hotKey + ":lock"
	lock := NewRedisLock(redisClient, lockKey, 30*time.Second)
	acquired, err := lock.AcquireLock(context.Background())
	if err != nil {
		fmt.Printf("biz %s failed to get lock\n", bizName)
		return err
	}
	if acquired {
		defer func(lock *RedisLock) {
			err := lock.ReleaseLock()
			if err != nil {
				fmt.Println(err)
			}
		}(lock)
		// 模拟更新热点 key 的操作
		fmt.Printf("%s Updating hot key: %s\n", bizName, hotKey)
		// 更新热点 key
		err := redisClient.Set(context.Background(), hotKey, newValue, 30*time.Minute).Err()
		if err != nil {
			return err
		}
		fmt.Printf("%s Finish update hot key.\n", bizName)
	}
	return nil
}

func bizUpdateHotKey(bizName, hotKey string) {
	newValue := time.Now().String()
	err := QueryAndUpdateHotKey(bizName, hotKey, newValue)
	if err != nil {
		fmt.Println("Error: ", err)
	}
}

func main() {
	hotKey := "cloudsky_user_info"
	var wg sync.WaitGroup
	for i := 0; i < 100; i++ {
		wg.Add(1)
		go func(i int) {
			defer wg.Done()
			bizUpdateHotKey(strconv.Itoa(i), hotKey)
		}(i)
	}
	wg.Wait()
}
```

<font style="color:rgb(85, 85, 85);">redis 本身并没有提供分布式锁相关的命令，但是setnx的特性非常接近：setnx在set的基础上进行一个判断，只有在key不存在的情况下才会进行正常set，返回成功；如果key存在返回失败。又setnx本身具有原子性，所以正常情况下可以保证互斥性；同时setnx还可以设置过期时间，达到过期时间则该值无效，从而满足了无死锁特性。  
</font><font style="color:rgb(85, 85, 85);">释放锁redis没有类似的命令，需要用两个命令来实现：get，del：</font>

```lua
if get(key) == value then
  del(key)
```

<font style="color:rgb(85, 85, 85);">两条指令就需要保证原子性，否则在get之后被别的线程抢占获取锁，再切换回来执行del会导致del掉新的锁。所以一般使用可以保证一致性的lua脚本执行释放锁的过程：</font>

```lua
if redis.call("get", key) == m_random_value then
    return redis.call("del", key)
else
    return 0
end
```

<font style="color:rgb(85, 85, 85);">lua实现：</font>

```lua
function _M.new(self, r, lock_name, lock_num, lock_time)
   return setmetatable({
      _redis = r,
      _lock_name = lock_name,
      _lock_num = lock_num,
      _lock_time = lock_time,
   },mt)
end

function _M._lock(self)
    local res, err = self._redis:set(self._lock_name, self._lock_num, "NX", "PX", self._lock_time)
    return res, err 
end

function _M._unlock(self)
    local res, err = self._redis:get(self._lock_name)
    if not res then
       return res, err
    end

    if self._lock_num == res then
       res, err = self._redis:del(self._lock_name)
       return res, err
    else
       return nil, "locked by other"
    end
    
end
```

<font style="color:rgb(85, 85, 85);">考虑一些异常情况：</font>

1. **<font style="color:rgb(85, 85, 85);">case1</font>**<font style="color:rgb(85, 85, 85);">: clientA获取锁setnx(key,value),设置过期时间1秒，0.9秒时clientA主动释放锁，但因为网络延迟该释放锁的请求在1.2秒才到达redis，在1秒到1.2秒这期间clientB获取锁setnx(key,value),设置过期时间1秒，这样在1.2秒时clientB获取的锁会被clientA延迟的释放锁命令所释放。  
</font>**<font style="color:rgb(85, 85, 85);">解决</font>**<font style="color:rgb(85, 85, 85);">：同一台机器或不同机器每一次获取锁时setnx的value必须不同，一般设置为以当前时间（毫秒时间戳）为种子所生成的随机数。</font>
2. **<font style="color:rgb(85, 85, 85);">case2</font>**<font style="color:rgb(85, 85, 85);">: clientA获取锁，设置过期时间3s，执行更新资源的网络操作时发生阻塞5s，当时间到达3s时过期，故clientA的锁自动释放，clientB获取锁成功更新资源，等clientA在5s后回来时又将clientB刚更新的资源更新，发生数据不一致。  
</font>**<font style="color:rgb(85, 85, 85);">解决</font>**<font style="color:rgb(85, 85, 85);">：这个case的解决需要看具体应用场景，网上有个方法是另外起一个线程来更新过期时间，确保过期时间大于业务执行时间。这样的缺点就是网络如果一直阻塞，别的请求就没法获得锁一直等待。我觉得如果是对先后请求顺序有要求的场景下，可以考虑在每次更新资源时进行两处判断：a:是否依旧持有锁。b:需要更新的资源是否已经被更新。如果依旧持有锁时，说明未发生上述case，可以正常更新资源。但是如果此时不持有锁了也不能立刻判断是已经被别的请求上锁，此时看下需要更新的资源是否已经被更新（可以记录更新时间戳），如果已经被更新则不要再写入覆盖；如果没有更新则进行写入。这样保证了先请求的不覆盖后请求的资源更新。当然也可以直接进行b判断，不用判断是否持有锁。</font>
3. **<font style="color:rgb(85, 85, 85);">case3</font>**<font style="color:rgb(85, 85, 85);">：clientA释放锁时，在get获取到锁的value和当前一致，发送del指令发生了网络延迟超过过期时间，超时锁自动释放，clientB获取锁进行相关逻辑，此时clientA的del指令到达，释放了clientB刚上的锁…  
</font>**<font style="color:rgb(85, 85, 85);">解决</font>**<font style="color:rgb(85, 85, 85);">：（猜想）可以使用redis脚本，将get与del写成一条redis脚本发送到redis服务器执行。</font>
4. **<font style="color:rgb(85, 85, 85);">case4</font>**<font style="color:rgb(85, 85, 85);">：clientA获取锁进行共享资源的操作，此时redis的master宕机，slave切换为新master，由于redis的数据同步是异步操作，在clientA的锁没有同步到slave时clientB向新的master获取锁，获取成功进行共享资源的操作，clientA和clientB同时获取到锁，违背互斥性。  
</font>**<font style="color:rgb(85, 85, 85);">解决</font>**<font style="color:rgb(85, 85, 85);">：redis集群分布式锁</font>

<font style="color:rgb(85, 85, 85);">顺便普及下redis的数据同步流程，分为两个步骤：</font>

1. <font style="color:rgb(85, 85, 85);">同步现有数据：此步骤发生在某个redis实例第一次成为某个master的slave时，master将现有数据状态后台打包生成rdb文件，从打包时刻起所有涉及修改数据的操作都放到一个命令缓冲区，rdb文件生成完毕发送到slave进行数据载入。然后master将缓冲区的指令发送到slave进行打包后数据修改的同步。</font>
2. <font style="color:rgb(85, 85, 85);">命令传播：第一步完成后，master收到所有涉及修改数据的指令都会发送到slave执行一遍，这里的“发送”就会经过网络，经过网络就有可能发送延时。master不可能确保每个slave都执行成功才返回结果给客户端，这样效率显然会很低，而且如果某个slave宕机或者网络延迟高，那客户端岂不是要等很久。所以这里的命令传播是异步操作，即master发送同步指令成功后就回复客户端执行结果，至于此时slave是否写完成客户端不关心。  
</font><font style="color:rgb(85, 85, 85);">case4就发生在命令传播的同步指令发出后且slave没有执行前。</font>

**<font style="color:rgb(85, 85, 85);">redis集群分布式锁（redlock）</font>**

<font style="color:rgb(85, 85, 85);">为了解决上述case4，产生了redis集群的分布式锁方法，思路为</font>**<font style="color:rgb(85, 85, 85);">准备N个redis的master实例，获取锁时必须大多数master（大于N/2,N为奇数）获取锁成功才算最终获取成功（感觉初衷有点像单master多slave下的手动完成同步并关心各slave同步结果）</font>**<font style="color:rgb(85, 85, 85);">。算法流程如下：</font>

1. <font style="color:rgb(85, 85, 85);">获取当前毫秒时间戳</font>
2. <font style="color:rgb(85, 85, 85);">同一请求使用相同的key和value对这N个master顺序进行获取锁操作，对于每个master实例上锁时需要定义一个操作的超时时间t，避免该master有问题还在傻等，该超时时间t应该小于锁的自动释放时间T（官方给出一个例子是锁失效时间为10s，那么每个实例操作的超时时间应该设为5-50ms，有点懵不知道怎么得出来的），超过t返回失败继续对下一个master进行上锁。</font>
3. <font style="color:rgb(85, 85, 85);">当且仅当一半以上的master成功获取锁并且总耗时小于锁的超时时间，则认为该请求成功获取锁。</font>
4. <font style="color:rgb(85, 85, 85);">每个master上锁的实际过期时间不同，因为对前面的master上锁以及等待回包都花时间，所以每个master上锁的实际时间是用预期过期时间减去前面几个master上锁所花费的时间。比如第一个master设置过期时间为3s，上锁花费100ms，第二个master上锁实际过期时间应设为3s-100ms，上锁花费150ms，第三个master上锁实际过期时间应为3s-100ms-150ms，以此类推。</font>
5. <font style="color:rgb(85, 85, 85);">如果最终获取锁失败（获取锁的master数量小于N/2），则应该立刻对所有master进行解锁，此外各请求还要各自delay一个随机时间后再来上锁。官方解释delay不同的随机值是为了避免相同时间后这么多请求再来竞争，尽量减少同时想获取锁的请求数，从而加大获取锁成功的概率。比如这一秒有100个请求来获取锁，然后失败，虽然接下来的每一秒都会有请求来获取锁，这一秒失败delay了不同的值，将这100个请求平均分配到了接下来的n秒上，但相比于delay相同的值效果会好很多。</font>
6. <font style="color:rgb(85, 85, 85);">解锁只需要对所有master发送解锁请求即可，不用判断是否获取锁成功，效果一样，全部发送写起来简单点。</font>

<font style="color:rgb(85, 85, 85);">回到case4，在锁已经被clientA获取的前提下，如果某个master挂掉了，clientB从salve升上来的新master处成功获得了锁，但是对于其他的N-1个master仍然获取失败，最终还是失败。不过为了防止case4的放大版（多台master同时挂掉）的发生，这N个master需要物理隔离，宕机与否彼此不受影响。</font>

######  永不过期
从缓存层面来看，确实没有设置过期时间，所以不会出现热点key过期 后产生的问题，也就是“物理”不过期。从功能层面来看，为每个value设置一个逻辑过期时间，当发现超过逻辑过期时间后，会使用单独的线程去构建缓存。

优缺点：由于没有设置真正的过期时间，实际上已经不存在热点key产生的一系列危害，但是会存在数据不一致的情况，同时代码复杂度会增大。

##### <font style="color:rgb(24, 24, 24);">热点数据解决方案</font>
![](https://cdn.nlark.com/yuque/0/2024/png/543296/1708427754334-eb3e0ab7-d744-4ce0-8700-aae7fe206bb4.png)

<font style="color:rgb(24, 24, 24);">该方案通过主动发现热点并对其进行存储来解决热点Key的问题。首先Client也会访问SLB，并且通过SLB将各种请求分发至Proxy中，Proxy会按照基于路由的方式将请求转发至后端的Redis中。</font>

<font style="color:rgb(24, 24, 24);">在热点key的解决上是采用在服务端增加缓存的方式进行。具体来说就是在Proxy上增加本地缓存，本地缓存采用LRU算法来缓存热点数据，后端db节点增加热点数据计算模块来返回热点数据。</font>

<font style="color:rgb(24, 24, 24);">Proxy架构的主要有以下优点：</font>

+ <font style="color:rgb(24, 24, 24);">Proxy本地缓存热点，读能力可水平扩展</font>
+ <font style="color:rgb(24, 24, 24);">DB节点定时计算热点数据集合</font>
+ <font style="color:rgb(24, 24, 24);">DB反馈 Proxy 热点数据</font>
+ <font style="color:rgb(24, 24, 24);">对客户端完全透明，不需做任何兼容</font>

<font style="color:rgb(24, 24, 24);">热点key处理</font>

<font style="color:rgb(24, 24, 24);">热点数据的读取</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1708427757273-5d474eb7-2767-44a5-863a-8ac6a9c7b232.png)

<font style="color:rgb(24, 24, 24);">在热点Key的处理上主要分为写入跟读取两种形式，在数据写入过程当SLB收到数据K1并将其通过某一个Proxy写入一个Redis，完成数据的写入。假若经过后端热点模块计算发现K1成为热点key后， Proxy会将该热点进行缓存，当下次客户端再进行访问K1时，可以不经Redis。最后由于proxy是可以水平扩充的，因此可以任意增强热点数据的访问能力。</font>

<font style="color:rgb(24, 24, 24);">热点数据的发现</font>

![](https://cdn.nlark.com/yuque/0/2024/png/543296/1708427755023-3bd7936a-0c4a-4e3c-b2a1-9dd525b6455f.png)

<font style="color:rgb(24, 24, 24);">对于db上热点数据的发现，首先会在一个周期内对Key进行请求统计，在达到请求量级后会对热点Key进行热点定位，并将所有的热点Key放入一个小的LRU链表内，在通过Proxy请求进行访问时，若Redis发现待访点是一个热点，就会进入一个反馈阶段，同时对该数据进行标记。</font>

<font style="color:rgb(24, 24, 24);">DB计算热点时，主要运用的方法和优势有：</font>

+ <font style="color:rgb(24, 24, 24);">基于统计阈值的热点统计</font>
+ <font style="color:rgb(24, 24, 24);">基于统计周期的热点统计</font>
+ <font style="color:rgb(24, 24, 24);">基于版本号实现的无需重置初值统计方法</font>
+ <font style="color:rgb(24, 24, 24);">DB 计算同时具有对性能影响极其微小、内存占用极其微小等优点</font>

###### <font style="color:rgb(24, 24, 24);">两种方案对比</font>
<font style="color:rgb(24, 24, 24);">通过上述对比分析可以看出，阿里云在解决热点Key上较传统方法相比都有较大的提高，无论是基于读写分离方案还是热点数据解决方案，在实际处理环境中都可以做灵活的水平能力扩充、都对客户端透明、都有一定的数据不一致性。此外读写分离模式可以存储更大量的热点数据，而基于Proxy的模式有成本上的优势。</font>

###### 阿里云redis 大key 和热 key 解决方案
[如何找出优化大Key与热Key,产生的原因和问题_云数据库 Redis 版(Redis)-阿里云帮助中心](https://help.aliyun.com/zh/redis/user-guide/identify-and-handle-large-keys-and-hotkeys)

[使用Redis搭建电商秒杀系统 - 云数据库 Redis - 阿里云](https://www.alibabacloud.com/help/zh/redis/use-cases/use-apsaradb-for-redis-to-build-a-business-system-that-can-handle-flash-sales?spm=a2c63.p38356.0.0.23141fbfN6BCCG)

#### 项目中redis用的多吗？redis 只做缓存数据吗？介绍下redis分布式锁实现？如果一定时间内没执行完成怎么办？
redis缓存雪崩、穿透、击穿，如何确保数据一致性(ucloud、饿了么、好未来、蜻蜓FM、B站2次)

redis 了解吗？

OLAP、OLTP

#### MongoDB


### tidb 介绍


### SQL
#### mysql 里面数据是以日为单位存储的，需要获取每个月数据与上个月数据的差值，怎么写sql
> <font style="color:rgb(221, 218, 214);background-color:rgb(27, 30, 31);">我们有一张表month_table记录了每月的销售冠军信息，这张表存储了每月销冠的id、name(姓名)、month_num(月份)，现在需要获取销冠次数超过2次的人以及其对应的做销冠次数。</font>
>
> <font style="color:rgb(221, 218, 214);background-color:rgb(27, 30, 31);">month_table表如下所示：</font>
>

> **id    name    month_num**
>
> **E002    王小凤    1**
>
> **E001    张文华    2**
>
> **E003    孙皓然    3**
>
> **E001    张文华    4**
>
> **E002    王小凤    5**
>
> **E001    张文华    6**
>
> **E004    李智瑞    7**
>
> **E002    王小凤    8**
>
> **E003    孙皓然    9**
>

> <font style="color:rgb(221, 218, 214);background-color:rgb(27, 30, 31);">写出sql</font>
>
> <font style="color:#000000;background-color:#fffffe;">select count(</font><font style="color:#0000ff;background-color:#fffffe;">id</font><font style="color:#000000;background-color:#fffffe;">) </font><font style="color:#0000ff;background-color:#fffffe;">as</font><font style="color:#000000;background-color:#fffffe;"> sale_num, m2.name </font><font style="color:#0000ff;background-color:#fffffe;">from</font><font style="color:#000000;background-color:#fffffe;"> month_table m1  </font>
>
> <font style="color:#000000;background-color:#fffffe;">left  join month_table m2 on m1.</font><font style="color:#0000ff;background-color:#fffffe;">id</font><font style="color:#000000;background-color:#fffffe;"> = m2.</font><font style="color:#0000ff;background-color:#fffffe;">id</font>
>
> <font style="color:#000000;background-color:#fffffe;">where m1.sale_num></font><font style="color:#098658;background-color:#fffffe;">2</font><font style="color:#000000;background-color:#fffffe;"> group by </font><font style="color:#0000ff;background-color:#fffffe;">id</font><font style="color:#000000;background-color:#fffffe;"> order by sale_num desc</font>
>

有一张学生表，name、age字段， 统计每个年龄段学生的数量，如10-20岁之间有多少学生，20-30有多少学生。。。一直到90-100岁



#### 2.豆瓣站内可以推荐各种内容到消息流中，例如日记、小组话题、长评等。
请设计推荐功能的数据表结构和索引，并给出以下操作的 SQL 语句：

(1) 查看某篇内容的所有推荐者；

(2) 查看某个用户的所有推荐，按时间倒序排列；

(3) 删除某篇内容及所有相关推荐。

#### NoSQL




#### etcd 使用场景
看你项目用了etcd，讲讲etcd选主过程？

#  中间件
### 消息队列
#### kafka
kafka 消息丢失、吞吐量

kafka 介绍下，副本数如何设置、zookeeper 在kafka中是什么作用，介绍下，raft协议有了解吗，介绍下

kafka了解过高性能原因吗，kafka做了哪些事情来保证性能？zookeeper如何保证数据一致性？raft协议介绍下？

Kafka用过吗，延迟队列实现

kafka和rabbitmq是什么，介绍下

#### ElasticSearch
Elasticsearch 数据几百万条，分页查询效率会很慢，es有两种模式支持分页查询，是什么模式

go-mysql-elasticsearch 如何实现的

es 分片，高并发处理

es 熟悉吗？ 两个字不是一个词，如何查出 如毛泽、东，查出来毛泽东，es如何做分词？

### <font style="color:#262626;">eureka 怎么实现注册，用什么语言，celery应用</font>
你们服务发现怎么做的，如何确保服务高可用

# 系统设计
## 高并发
php版本，服务器规模和配置，服务器是公有云吗，你们用户量规模，每日订单量和qps

看你之前公司用redis锁解决商品超卖问题，这个你怎么解决的

redis 反爬虫怎么做的，如何限制用户访问

比如服务器目前只支持1k并发，如何让他支持5k并发，你会考虑哪些方面？

## 分布式系统
分布式系统数据一致性有了解吗，我说有，raft 和paxos协议，介绍下 raft

raft 有一个节点断网后，过一段时间又恢复了，这个过程，是如何实现数据最终一致性的

一致性协议有了解吗？raft、paxos？介绍下选举过程

介绍下zookeeper

分布式事务里面有个CAP和Base理论，你知道吗？



## 限流算法
看你做过限流相关算法，简单介绍下？漏桶算法？令牌桶实现？

[常用限流算法的应用场景和实现原理](https://mp.weixin.qq.com/s/krrUFEHVBw4c-47ziXOK2w)

### 计数器
<font style="color:rgb(74, 74, 74);">在</font>**<font style="color:rgb(74, 74, 74);">固定时间窗口</font>**<font style="color:rgb(74, 74, 74);">内</font>**<font style="color:rgb(74, 74, 74);">对请求进行计数</font>**<font style="color:rgb(74, 74, 74);">，</font>**<font style="color:rgb(74, 74, 74);">与阀值进行比较判断是否需要限流</font>**<font style="color:rgb(74, 74, 74);">，一旦到了时间临界点，将计数器清零</font>

    - <font style="color:rgb(74, 74, 74);">存在问题: 计数器算法存在“时间临界点”缺陷, </font>**<font style="color:rgb(74, 74, 74);">无法承受突发流量</font>**<font style="color:rgb(74, 74, 74);">。</font>

```go
type LimitRate struct {
    rate  int           //阀值
    begin time.Time     //计数开始时间
    cycle time.Duration //计数周期
    count int           //收到的请求数
    lock  sync.Mutex    //锁
}

func (limit *LimitRate) Allow() bool {
    limit.lock.Lock()
    defer limit.lock.Unlock()

    // 判断收到请求数是否达到阀值
    if limit.count == limit.rate-1 {
        now := time.Now()
        // 达到阀值后，判断是否是请求周期内
        if now.Sub(limit.begin) >= limit.cycle {
            limit.Reset(now)
            return true
        }
        return false
    } else {
        limit.count++
        return true
    }
}

func (limit *LimitRate) Set(rate int, cycle time.Duration) {
    limit.rate = rate
    limit.begin = time.Now()
    limit.cycle = cycle
    limit.count = 0
}

func (limit *LimitRate) Reset(begin time.Time) {
    limit.begin = begin
    limit.count = 0
}
```

### <font style="color:rgb(74, 74, 74);">滑动窗口</font>
    - <font style="color:rgb(74, 74, 74);">滑动窗口算法</font>**<font style="color:rgb(74, 74, 74);">将一个大的时间窗口分成多个小窗口，每次大窗口向后滑动一个小窗口，并保证大的窗口内流量不会超出最大值</font>**<font style="color:rgb(74, 74, 74);">，这种实现比固定窗口的流量曲线更加平滑。</font>
    - <font style="color:rgb(74, 74, 74);">普通时间窗口有一个问题，比如窗口期内请求的上限是100，假设有100个请求集中在前1s的后100ms，100个请求集中在后1s的前100ms，其实在这200ms内就已经请求超限了，但是由于时间窗每经过1s就会重置计数，就无法识别到这种请求超限。</font>
    - <font style="color:rgb(74, 74, 74);">对于滑动时间窗口，我们可以把1ms的时间窗口划分成10个小窗口，或者想象窗口有10个时间插槽time slot, 每个time slot统计某个100ms的请求数量。每经过100ms，有一个新的time slot加入窗口，早于当前时间1s的time slot出窗口。窗口内最多维护10个time slot。</font>
    - <font style="color:rgb(74, 74, 74);">存在问题: 滑动窗口算法是固定窗口的一种改进，但从根本上并</font>**<font style="color:rgb(74, 74, 74);">没有真正解决固定窗口算法的临界突发流量</font>**<font style="color:rgb(74, 74, 74);">问题</font>

```go
type timeSlot struct {
 timestamp time.Time // 这个timeSlot的时间起点
 count     int       // 落在这个timeSlot内的请求数
}

// 统计整个时间窗口中已经发生的请求次数
func countReq(win []*timeSlot) int {
 var count int
 for _, ts := range win {
  count += ts.count
 }
 return count
}

type SlidingWindowLimiter struct {
 mu           sync.Mutex    // 互斥锁保护其他字段
 SlotDuration time.Duration // time slot的长度
 WinDuration  time.Duration // sliding window的长度
 numSlots     int           // window内最多有多少个slot
 windows      []*timeSlot
 maxReq       int // 大窗口时间内允许的最大请求数
}

func NewSliding(slotDuration time.Duration, winDuration time.Duration, maxReq int) *SlidingWindowLimiter {
 return &SlidingWindowLimiter{
  SlotDuration: slotDuration,
  WinDuration:  winDuration,
  numSlots:     int(winDuration / slotDuration),
  maxReq:       maxReq,
 }
}


func (l *SlidingWindowLimiter) validate() bool {
 l.mu.Lock()
 defer l.mu.Unlock()


 now := time.Now()
 // 已经过期的time slot移出时间窗
 timeoutOffset := -1
 for i, ts := range l.windows {
  if ts.timestamp.Add(l.WinDuration).After(now) {
   break
  }
  timeoutOffset = i
 }
 if timeoutOffset > -1 {
  l.windows = l.windows[timeoutOffset+1:]
 }

 // 判断请求是否超限
 var result bool
 if countReq(l.windows) < l.maxReq {
  result = true
 }

 // 记录这次的请求数
 var lastSlot *timeSlot
 if len(l.windows) > 0 {
  lastSlot = l.windows[len(l.windows)-1]
  if lastSlot.timestamp.Add(l.SlotDuration).Before(now) {
   // 如果当前时间已经超过这个时间插槽的跨度，那么新建一个时间插槽
   lastSlot = &timeSlot{timestamp: now, count: 1}
   l.windows = append(l.windows, lastSlot)
  } else {
   lastSlot.count++
  }
 } else {
  lastSlot = &timeSlot{timestamp: now, count: 1}
  l.windows = append(l.windows, lastSlot)
 }


 return result
}
```

### 漏桶算法
<font style="color:rgb(74, 74, 74);">想象有一个木桶，桶的容量是固定的。当有请求到来时先放到木桶中，处理请求的</font><font style="color:rgb(40, 202, 113);">worker</font><font style="color:rgb(74, 74, 74);">以固定的速度从木桶中取出请求进行相应。如果木桶已经满了，直接返回请求频率超限的错误码或者页面。</font>

    - ![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706080686950-a4c5ee02-009c-4c49-aae7-2969c8ff1e5c.png)
    - 适用场景: <font style="color:rgb(74, 74, 74);">漏桶算法是</font>**<font style="color:rgb(74, 74, 74);">流量最均匀的限流</font>**<font style="color:rgb(74, 74, 74);">实现方式，一般用于流量“整形”。例如保护数据库的限流，先把对数据库的访问加入到木桶中，worker再以db能够承受的qps从木桶中取出请求，去访问数据库。</font>
    - <font style="color:rgb(74, 74, 74);">存在问题: 木桶</font>**<font style="color:rgb(74, 74, 74);">流入请求速率不固定，流出速率恒定</font>**<font style="color:rgb(74, 74, 74);">。这样的话能保护系统资源不被打满，但是面对</font>**<font style="color:rgb(74, 74, 74);">突发流量时会有大量请求失败</font>**<font style="color:rgb(74, 74, 74);">，</font>**<font style="color:rgb(74, 74, 74);">不适合电商抢购和微博出现热点事件等场景的限流</font>**

### <font style="color:rgb(74, 74, 74);">令牌桶</font>
    - **<font style="color:rgb(74, 74, 74);">令牌桶是反向的"漏桶"</font>**<font style="color:rgb(74, 74, 74);">，它是以恒定的速度往木桶里加入令牌，木桶满了则不再加入令牌。服务收到请求时尝试从木桶中取出一个令牌，如果能够得到令牌则继续执行后续的业务逻辑。如果没有得到令牌，直接返回访问频率超限的错误码或页面等，不继续执行后续的业务逻辑。</font>
    - **<font style="color:rgb(74, 74, 74);">特点：由于木桶内只要有令牌，请求就可以被处理，所以令牌桶算法可以支持突发流量。</font>**
    - ![](https://cdn.nlark.com/yuque/0/2024/png/543296/1706085366250-16942361-0b31-40d7-9c07-c20c654d65d3.png)
    - <font style="color:rgb(74, 74, 74);">同时由于往木桶添加令牌的速度是恒定的，且木桶的容量有上限，所以单位时间内处理的请求书也能够得到控制，起到限流的目的。假设加入令牌的速度为 1token/10ms，桶的容量为500，在请求比较的少的时候（小于每10毫秒1个请求）时，木桶可以先"攒"一些令牌（最多500个）。当有突发流量时，一下把木桶内的令牌取空，也就是有500个在并发执行的业务逻辑，之后要等每10ms补充一个新的令牌才能接收一个新的请求。</font>
    - <font style="color:rgb(74, 74, 74);">参数设置: 木桶的容量  - 考虑业务逻辑的资源消耗和机器能承载并发处理多少业务逻辑。生成令牌的速度 - 太慢的话起不到“攒”令牌应对突发流量的效果。</font>
    - <font style="color:rgb(74, 74, 74);">适合电商抢购或者微博出现热点事件这种场景，因为在限流的同时可以应对一定的突发流量。如果采用漏桶那样的均匀速度处理请求的算法，在发生热点时间的时候，会造成大量的用户无法访问，对用户体验的损害比较大。</font>

```go
type TokenBucket struct {
   rate         int64 //固定的token放入速率, r/s
   capacity     int64 //桶的容量
   tokens       int64 //桶中当前token数量
   lastTokenSec int64 //上次向桶中放令牌的时间的时间戳，单位为秒

   lock sync.Mutex
}

func (bucket *TokenBucket) Take() bool {
   bucket.lock.Lock()
   defer bucket.lock.Unlock()

   now := time.Now().Unix()
   bucket.tokens = bucket.tokens + (now-bucket.lastTokenSec)*bucket.rate // 先添加令牌
   if bucket.tokens > bucket.capacity {
      bucket.tokens = bucket.capacity
   }
   bucket.lastTokenSec = now
   if bucket.tokens > 0 {
      // 还有令牌，领取令牌
      bucket.tokens--
      return true
   } else {
      // 没有令牌,则拒绝
      return false
   }
}

func (bucket *TokenBucket) Init(rate, cap int64) {
   bucket.rate = rate
   bucket.capacity = cap
   bucket.tokens = 0
   bucket.lastTokenSec = time.Now().Unix()
}
```

## 业务场景设计
设计一个推荐系统

乐观锁和悲观锁，应用场景

介绍下简历上说到的 redis 锁解决商品超卖问题，介绍下redis 分布式锁，在支付前还是支付后设置的？

TCC是什么，介绍下？

自动生成唯一id如何实现？一致性hash介绍下？一致性hash的其他应用？memcached之前没集群，如何实现一致性hash？

如何解决拼团超卖问题的？

如何确保每个用户只能抢到一个商品？

实现个百度热搜的热词榜？

设计个可以插队的排队系统？

数据同步框架实现方案，为何用多协程？

拼团超卖问题怎么解决的？

设计一个发红包系统

介绍下你说的redis锁解决拼团超卖问题

有个接口很慢，怎么排查

设计一个获取用户详情的接口，你会考虑哪些因素

Redis 解决商品超卖问题(逻辑思维、作业帮、百度、好未来、蜻蜓FM、b站、比心)

实现生产者消费者，从mq读数据，写入到数据库

```python
import pandas as pd
import threading
import retry


@retry
def long_time_task(data):
    # do some jobs
    # sleep 1
    # new handlers
    return data


def schedluer():
    for i in range(100):
        t = threading.Thread(args=consumer)
        t.start()
        t.join()


def read_data_from_mq():
    return data


def consumer():
    data = producer()
    result = log_time_task(data)
    write_to_mysql(result)


def producer():
    return read_data_from_mq()


def write_to_mysql(mq_data_list):
    mq_df = pd.DataFrame(mq_data_list)
    mq_df.to_sql(mysql_connection)
```

TCC事务介绍下？

有个上亿的数组，如何判断一个数是否在这个数组里面？除了布隆过滤器外有其他的吗？放redis 有没有更好的方法存进去？讲下布隆过滤器？

了解服务化吗？讲下微服务的好处，弊端？

分布式存储有了解吗？etcd实现原理

ceph 项目有了解吗？介绍下

### 百度大搜业务场景设计
#### 二面
设计一个服务，提供一个身份证查询，身份证md5查询，如何查询身份证的md5是否在库中，高并发海量数据，你怎么做查询和优化？



我说布隆过滤器，面试官问布隆过滤器key满足要求吗？

我说存储b+树中，面试官说场景是海量高并发，我说用大数据集群md5分散到多个服务器上，



假设有一个服务，平时qps很少，某段时间qps非常大，针对这种场景，你如何优化？



网关流量分发，k8s弹性扩缩容，还有其他优化点吗？



有个服务，对外提供依赖一些配置数据的字典，存储在内存中，优化性能，如何做字典的热更新？例如1h或者1day更新一次？



我说 apollo或者etcd watch，key更新后推送，面试官问推送到service后怎么做？线上在读，你在写key，这个过程如何实现？我说用锁，问用什么锁实现？我说用悲观锁实现，面试官说会影响到读，后面我又说用乐观锁。。面试官问有没有其他的机制？有了解过自旋锁吗？

有了解过设计原则？ solid 有了解吗？

一致性哈希听你刚提到，有了解过跳跃一致性哈希吗？

#### 三面
##### 让你设计一个搜索系统，你会如何设计？
我说设计海量数据爬取，瓶颈是网络IO、数据存储、使用es存储、大数据存储、实时分析、网络带宽会限制爬虫性能、通过hash算法计算文件md5，降低冗余文件存储空间、建立高效的文件系统、搜索检索相关还能想到哪些？如何做检索？一个query到返回结果需要实现哪些？

##### 平时了解搜索吗？
# 大数据
datax 数据同步方案

hive Impala 这些组件你是负责架构设计的还是使用的

你们数据实时同步和离线同步怎么实现的，用的哪些工具？datax、canal、maxwell

hive 同步到 mysql，你会把哪些数据同步到postgresql，另外介绍下hive和postgresql区别和架构

greenplum 介绍下基础架构

hive数据你怎么同步到greenplum实现的，数据是一条条查出写入的吗，数据同步流程介绍下，上游数据如果非常多，写入很慢，你怎么解决的

遇到greenplum写入性能 CPU 占用100%，你如何解决这块的性能

# 工具
### git merge 和rebase 对比


# DevOps
### Docker
如何实现资源隔离

docker 原理

docker 进程在宿主机上可以看到吗

如何知道一个进程是宿主机的还是docker容器的

docker entrypoint 和 cmd 区别

docker add 和copy区别

docker 镜像打包如何减小镜像体积、多阶段构建

docker 优势在哪里？ cgroups namespace 

docker 相关api熟悉吗？

docker 实现原理(华云数据、云智慧) 资源隔离和限制具体实现

### Kubernetes
k8s集群规模

k8s热更新

k8s 你了解的有哪些组件，滚动更新是怎么做的

k8s你熟悉哪些模块实现？

cni 有了解吗？

k8s你熟悉哪些模块？常用的api有了解吗？

k8s scheduler 实现原理

k8s 热更新实现，如何实现把一个pod调度到另一个pod

k8s 哪些数据库存储在etcd，哪些数据没存储在etcd

### CI &CD
docker 容器怎么部署的，容器升级cicd怎么做的

docker 项目是怎么部署的

docker 的 ci cd你们怎么做的

你提到docker k8s 你们是做docker k8s开发还是做devops ？

你们项目怎么部署的，devops怎么做的

你们cicd怎么做的，如何拉取代码部署的

runC实现 containerd OCI实现原理

# 测试
功能测试、UI测试有了解吗



