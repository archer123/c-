# c-
### const
const 加在成员函数后面表示该函数不会修改任何数据成员

### dynamic_cast
dynamic_cast在将父类cast到子类时，父类必须要有虚函数，否则编译器会报错。

在类层次间进行上行转换时，dynamic_cast和static_cast的效果是一样的；

在进行下行转换时，dynamic_cast具有类型检查的功能，比static_cast更安全。

当dynamic_cast进行下行转换时，若转换对象实际指向父类指针，则报错bad_cast返回NULL

### 重写，重载，重定义

-重载：函数名相同，函数的参数个数、参数类型或参数顺序三者中必须至少有一种不同。函数返回值的类型可以相同，也可以不相同。发生在一个类内部。
-重定义：也叫做隐藏，子类重新定义父类中有相同名称的非虚函数 ( 参数列表可以不同 ) ，指派生类的函数屏蔽了与其同名的基类函数。可以理解成发生在继承中的重载。
-重写：也叫做覆盖，一般发生在子类和父类继承关系之间。子类重新定义父类中有相同名称和参数的虚函数。(override)

### 数组的特点
- 在内存中，数组是一块连续的区域。 拿上面的看电影来说，这几个人在电影院必须坐在一起。
- 数组需要预留空间，在使用前要先申请占内存的大小，可能会浪费内存空间。 比如看电影时，为了保证10个人能坐在一起，必须提前订好10个连续的位置。这样的好处就是能保证10个人可以在一起。但是这样的缺点是，如果来的人不够10个，那么剩下的位置就浪费了。如果临时有多来了个人，那么10个就不够用了，这时可能需要将第11个位置上的人挪走，或者是他们11个人重新去找一个11连坐的位置，效率都很低。如果没有找到符合要求的作为，那么就没法坐了。
- 插入数据和删除数据效率低，插入数据时，这个位置后面的数据在内存中都要向后移。删除数据时，这个数据后面的数据都要往前移动。 比如原来去了5个人，然后后来又去了一个人要坐在第三个位置上，那么第三个到第五个都要往后移动一个位子，将第三个位置留给新来的人。 当这个人走了的时候，因为他们要连在一起的，所以他后面几个人要往前移动一个位置，把这个空位补上。
随机读取效率很高。因为数组是连续的，知道每一个数据的内存地址，可以直接找到给地址的数据。
- 并且不利于扩展，数组定义的空间不够时要重新定义数组。

### 链表的特点
- 在内存中可以存在任何地方，不要求连续。 在电影院几个人可以随便坐。
- 每一个数据都保存了下一个数据的内存地址，通过这个地址找到下一个数据。 第一个人知道第二个人的座位号，第二个人知道第三个人的座位号……
- 增加数据和删除数据很容易。 再来个人可以随便坐，比如来了个人要做到第三个位置，那他只需要把自己的位置告诉第二个人，然后问第二个人拿到原来第三个人的位置就行了。其他人都不用动。
- 查找数据时效率低，因为不具有随机访问性，所以访问某个位置的数据都要从第一个数据开始访问，然后根据第一个数据保存的下一个数据的地址找到第二个数据，以此类推。 要找到第三个人，必须从第一个人开始问起。
- 不指定大小，扩展方便。链表大小不用定义，数据随意增删。


### 僵尸进程
一个进程在调用exit命令结束自己的生命的时候，其实它并没有真正的被销毁，而是留下一个称为僵尸进程（Zombie）的数据结构（系统调用exit，它的作用是使进程退出，但也仅仅限于将一个正常的进程变成一个僵尸进程，并不能将其完全销毁）。

在Linux进程的状态中，僵尸进程是非常特殊的一种，它已经放弃了几乎所有内存空间，没有任何可执行代码，也不能被调度，仅仅在进程列表中保留一个位置，记载该进程的退出状态等信息供其他进程收集，除此之外，僵尸进程不再占有任何内存空间。

它需要它的父进程来为它收尸，如果他的父进程没安装SIGCHLD信号处理函数调用wait或waitpid（）等待子进程结束，又没有显式忽略该信号，那么它就一直保持僵尸状态，如果这时父进程结束了，那么init进程自动会接手这个子进程，为它收尸，它还是能被清除的。但是如果父进程是一个循环，不会结束，那么子进程就会一直保持僵尸状态，这就是为什么系统中有时会有很多的僵尸进程。

用命令ps，可以看到有标记为Z的进程就是僵尸进程。

