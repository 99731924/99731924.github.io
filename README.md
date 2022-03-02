
# 马努的头发


# 0 什么是回归？
假设线性回归是个黑盒子，那按照程序员的思维来说，这个黑盒子就是个函数，然后呢，我们只要往这个函数传一些参数作为输入，就能得到一个结果作为输出。那回归是什么意思呢？其实说白了，就是这个黑盒子输出的结果是个连续的值。如果输出不是个连续值而是个离散值那就叫分类。那什么叫做连续值呢？非常简单，举个栗子：比如我告诉你我这里有间房子，这间房子有40平，在地铁口，然后你来猜一猜我的房子总共值多少钱？这就是连续值，因为房子可能值80万，也可能值80.2万，也可能值80.111万。再比如，我告诉你我有间房子，120平，在地铁口，总共值180万，然后你来猜猜我这间房子会有几个卧室？那这就是离散值了。因为卧室的个数只可能是1， 2， 3，4，充其量到5个封顶了，而且卧室个数也不可能是什么1.1， 2.9个。所以呢，对于ML萌新来说，你只要知道我要完成的任务是预测一个连续值的话，那这个任务就是回归。是离散值的话就是分类。（PS:目前只讨论监督学习）

# 1 线性回归
OK，现在既然已经知道什么是回归，那现在就要来聊一聊啥叫线性。其实这玩意也很简单，我们在上初中的时候都学过直线方程对不对？来来来，我们来回忆一下直线方程是啥？
y = k x + b y=kx+b
y=kx+b

喏，这就是初中数学老师教我们的直线方程。那上过初中的同学都知道，这个式子表达的是，当我知道k（参数）和b（参数）的情况下，我随便给一个x我都能通过这个方程算出y来。而且呢，这个式子是线性的，为什么呢？因为从直觉上来说，你都知道，这个式子的函数图像是条直线。。。。从理论上来说，这式子满足线性系统的性质。（至于线性系统是啥，我就不扯了，不然没完没了）那有的同学可能会觉得疑惑，这一节要说的是线性回归，我扯这个low逼直线方程干啥？其实，说白了，线性回归无非就是在N维空间中找一个形式像直线方程一样的函数来拟合数据而已。比如说，我现在有这么一张图，横坐标代表房子的面积，纵坐标代表房价。

![Image text](https://img-blog.csdn.net/20180829213312304?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fsd18xMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

然后呢，线性回归就是要找一条直线，并且让这条直线尽可能地拟合图中的数据点。
那如果让1000个老铁来找这条直线就可能找出1000种直线来，比如这样

![Image text](https://img-blog.csdn.net/20180829213742884?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fsd18xMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

这样

![image text](https://img-blog.csdn.net/20180829213816880?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fsd18xMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
或者这样
![image text](https://img-blog.csdn.net/20180829213845176?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fsd18xMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

喏，其实找直线的过程就是在做线性回归，只不过这个叫法更有逼格而已。。。

# 2 损失函数
那既然是找直线，那肯定是要有一个评判的标准，来评判哪条直线才是最好的。OK，道理我们都懂，那咋评判呢？其实简单的雅痞。。。只要算一下实际房价和我找出的直线根据房子大小预测出来的房价之间的差距就行了。说白了就是算两点的距离。当我们把所有实际房价和预测出来的房价的差距（距离）算出来然后做个加和，我们就能量化出现在我们预测的房价和实际房价之间的误差。例如下图中我画了很多条小数线，每一条小数线就是实际房价和预测房价的差距（距离）

![image text](https://img-blog.csdn.net/20180829214719510?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fsd18xMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

然后把每条小竖线的长度加起来就等于我们现在通过这条直线预测出的房价与实际房价之间的差距。那每条小竖线的长度的加和怎么算？其实就是欧式距离加和，公式如下。（其中y(i)表示的是实际房价，y^(i)表示的是预测房价）
![image text](https://img-blog.csdn.net/2018082921503261?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fsd18xMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

这个欧氏距离加和其实就是用来量化预测结果和真实结果的误差的一个函数。在ML中称它为损失函数（说白了就是计算误差的函数）。那有了这个函数，我们就相当于有了一个评判标准，当这个函数的值越小，就越说明我们找到的这条直线越能拟合我们的房价数据。所以说啊，线性回归无非就是通过这个损失函数做为评判标准来找出一条直线。

刚刚我举的例子是一维的例子（特征只有房子大小），那现在我们假设我的数据中还有一个特征是楼间距，那图像可能就是酱紫了。

![image text](https://img-blog.csdn.net/20180829215651135?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fsd18xMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

从图我们可以看得出来，就算是在二维空间中，还是找一条直线来拟合我们的数据。所以啊，换汤不换药，损失函数还是这个欧式距离加和。

![image text](https://img-blog.csdn.net/20180829215824164?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Fsd18xMjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)



## 暴力
    class Solution {
    public:
    int search(vector<int>& nums, int target) {
        
        for(int i=0;i<nums.size();i++){
            if(nums[i]==target) return i;
        }
        return -1;
    }
};
                                        
## 暴力优化
                                        
    class Solution {
    public:
    int search(vector<int>& nums, int target) {        
        for(int i=0;i<nums.size();i++){
            if(nums[i]==target) return i;
            if(nums[i]>target) return -1;
        }
        return -1;
    }
};

                                        
# 二分
  
    class Solution {
    public:
    int search(vector<int>& nums, int target) {    
        int left=0;int right=nums.size()-1;    
        int mid;
        while(left<=right){
            mid=left+(right-left)/2;
            if(nums[mid]<target){
                left=mid+1;
            }
            else if(nums[mid]>target){
                right=mid-1;
            }
            else if(nums[mid]==target){
                return mid;
            }
        }
        return -1;
    }
};
  
##  要注意mid=起点+长度
    
    
##  双指针
https://leetcode-cn.com/problems/remove-element/submissions/
    
    class Solution {
    public:
    int removeElement(vector<int>& nums, int val) {
       int slow=0;
       for(int i=0;i<nums.size();i++){
           if(nums[i]!=val)
           nums[slow++]=nums[i];
       } 
       return slow;
    }
};
                                       
#  slow统计有效数字，i扫一遍

## 继续双指针

    https://leetcode-cn.com/problems/squares-of-a-sorted-array/submissions/          
    
    class Solution {
    public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> result(nums.size(),0);
        int end=nums.size()-1;
        int begin=0;
        int k=end;
        for(k=end;k>=0;k--){
            if(nums[end]*nums[end]>nums[begin]*nums[begin])result[k]=nums[end]*nums[end],end--;
            else result[k]=nums[begin]*nums[begin],begin++;
            cout<<k<<" ";
        }
        return result;
    }
};  
    
# 暴力全部求一边然后sort，但是没有利用到题目中的有序，负数也是有序的，头尾比较塞进去就好了
    
# 长度最小子串
    https://leetcode-cn.com/problems/minimum-size-subarray-sum/submissions/
    
    class Solution {
    public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int slow=0, fast=0;
        int minlen=10010, len=0;
        int total=0;
        int flag=0;
        for(;fast<nums.size();fast++){
            total+=nums[fast];            
            while(total>=target){
                flag++;
                len=fast-slow+1;
                minlen=min(minlen,len);               
                total-=nums[slow];
                slow++;                
            }
        }
        if(flag==0)minlen=0;

        return minlen;
    }
};

# 螺旋数组
### 难！
# https://leetcode-cn.com/problems/spiral-matrix-ii/

    class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>>res(n,vector<int>(n,0));
        int loop=n/2;
        int startx=0, starty=0;
        int offset=1;
        int count=1;
        int mid=n/2;
        int i,j;
        while(loop--){
            j=startx,i=starty;
            for(;j<startx+n-offset;j++)
            res[i][j]=count++;
            for(;i<starty+n-offset;i++)
            res[i][j]=count++;
            for(;j>startx;j--)
            res[i][j]=count++;
            for(;i>starty;i--)
            res[i][j]=count++;
            startx++,starty++;
            offset+=2;     
        }
        if(n%2){
                res[mid][mid]=count;
            }
        return res;
    }
};
                                       
## 常考知识
### 装饰器
- 装饰器可以理解为对函数的装饰，即在实现函数功能前先执行装饰器的函数。对于一些可复用的代码，例如鉴权功能或者打日志记录时间，可以使用装饰器
```python
    def zhuangshi(func):
        def hello(*args, **kwargs):
            print('hello')
            func(*args, **kwargs)
        return hello()
    
    @zhuangshi
    def hi():
        print('hi')
```
### 垃圾回收
- 通过引用计数进行垃圾回收，每一个对象内部有一个引用计数器，对象被创建/引用/作为参数会使引用计数器加一，对象被删除/离开作用域、所在容器被删除或被删除会使引用计数器减一，引用计数器为0时回收。高效、简单、实时。
- pyobject
```python
    typedef struct_object{
        int ob_refcnt; //引用计数器
        struct_typeobject *ob_type;
    }
```
- 循环引用: 列表/字典等容器对象会循环引用，python采用标志-清除算法和分代回收算法来回收。
### python的GIL(全局解释器锁)
- python的多线程是假的多线程，适合I/O密集型，不适合CPU密集型。因为同一时刻只有一个线程能执行，线程在执行前都需要获得一个GIL锁，获得锁的才能执行，线程运行完后，其它线程会争夺GIL锁。所以python的多线程是并发而不是并行，因为I/O密集型的场景主要时间都在网络传输所以适合使用多线程，CPU密集型的可以考虑多进程。
### 多进程多线程
- 进程：程序的一次执行，是一个动态的概念，是CPU资源分配和调度的基本单位
- 线程：一个进程可以包含多个线程，线程只有很少的资源，是cpu调度的最小单位。在一个进程内多个线程可以并发执行。
- 线程池：一般多线程方案为即时创建，即时销毁，但如果任务执行时间较短，而且比较频繁，那么服务器会处于不停创建和销毁线程的状态，开销比较大。线程池可以先创建N个线程，然后维护一个任务队列，每个线程都去队列中取任务，执行完后再继续取任务，知道任务队列为空，避免了线程的频繁创建和销毁。
- 线程池线程数设置：设本地计算时间为x，I/O等待时间为y，CPU核数为N，线程数=N*(x+y/x)，因为python全局GIL锁的问题，所以只能用到一个核，一般设N为1.
### 列表元组
### 生成器迭代器
## django
### ngnix
- 反向代理：通过代理服务器来接收请求，再由代理服务器将请求转发到服务器。ngnix采用单进程异步非阻塞的方式来实现高并发。通过ngnix还可以实现负载均衡。 
### 中间件
- 包含process_request, process_view, process_exception,process_template_responprocess, process_reponse这几种方法，可以实现对请求的鉴权，响应逻辑。

                                       
## c++
### (1) c和c++区别
- c是面向过程的语言，c++是面向对象的语言
- c++有类，结构体，两者区别是类的成员默认私有，结构体的成员默认公开
- c只有结构体，而且结构体没有方法
- c++支持函数重载，c不支持。因为例如一个函数 void func(int a, int b),c编译为 _func, c++编译为 _func_int_int,所以c++可以用不同类型的参数来区分函数。
### (2) 继承/多态/虚函数
- 继承：子类可以继承父类的属性和方法
- 多态：在父类中使用virtual关键字定义一个虚函数 ，然后在子类中实现。
### (3) 抽象类/纯虚函数
- 在一个类中定义一个纯虚函数，并且不实现而是在子类中实现，这个类就是抽象类
- 例：定义一个动物类，和一个纯虚函数“叫声”，然后子类不同的动物来实现“叫声”这个方法，因为不存在动物这种动物，所以它是抽象的。
### (4) static关键字
- 静态关键字
- 修饰全局变量：变为全局静态变量，存放在静态存储区，会自动初始化，对其它文件不可见。
- 修饰局部变量：变为局部静态变量，存放在静态存储区，会自动初始化，作用域仍为局部作用域，但是离开作用域后不会销毁，只是不能访问，直到再次调用该函数，值不变。
- 修饰函数：变为静态函数，正常函数的定义和声明默认都是extern的，但静态函数只能在本文件内使用，不会和其它文件的同名函数冲突。
- 修饰类的成员：静态成员是类中所有对象的共同成员，可以实现多个对象之间的数据共享。
- 修饰类的函数：静态成员函数，也是属于类，而不是属于对象，静态成员函数的实现不能引用类中的非静态成员。
### (5) 指针和引用区别
### (6) new/delete和malloc/free区别
- new/delete是C++的关键字，而malloc/free是C语言的库函数，malloc使用时需指定申请空间的大小，并且指针是void*型的，返回指针需要强制类型转换。
### (7) 内存
- 栈区：由编译器自动分配释放，存放局部变量，函数参数，返回数据，返回地址等。操作方式类似与数据结构中的栈。
- 堆区：由程序员分配释放，分配方式类似与链表。
- 全局区(静态区)：存放全局变量，静态数据，常量。程序结束，由系统释放。
- 文字常量区：存放常量字符串，程序结束后由系统释放。
- 程序代码区：存放函数体的二进制代码。
### (8) c++11新特性
- auto关键字：根据初始值自动推导类型，但是不能用于函数传参和数组类型的推导。
- nullptr关键字：空指针
- 智能指针
    重要的区别是它负责自动释放所指向的对象。标准库提供的两种智能指针的区别在于管理底层指针的方法不同，shared_ptr允许多个指针指向同一个对象，unique_ptr则“独占”所指向的对象。标准库还     定义了一种名为weak_ptr的伴随类，它是一种弱引用，指向shared_ptr所管理的对象，这三种智能指针都定义在memory头文件中。
- 新增STL容器array和tuple
- lambda表达式
### (9) include
- <>和" "的区别，" "先查找当前文件目录->编译器设置的头文件路径->系统变量指定的头文件路径。<>查找编译器设置的头文件路径->系统变量指定的头文件路径
## 数据结构
### (1) 数组和链表区别
- 数组随机访问速度快，链表只能顺序遍历访问。
- 创建数组需要在内存中开辟一段连续的内存空间，链表没有要求，所以链表的空间利用率比较高。
- 数组插入删除数据效率很低，链表插入删除效率高
### (1) 哈希表
- 将数据通过哈希函数哈希后存起来，查询速度O(1)
- 哈希冲突，两个数据哈希后的值一样，此时就产生了哈希冲突
- 开放寻址法：哈希冲突了就不断的往下一个位置找，直到找到一个为空的位置
- 拉链法：在有冲突的位置，加个链表，将数据存放在链表上。
### (2) 平衡二叉树
- 非叶子节点最多拥有两个子节点
- 非叶子节点值大于左边子节点，小于右边子节点
- 树的左右两边层级数相差不大于1
- 节点没有重复值
- 查询速度类似二分查找
### (3) B-tree
- 又名平衡多路查找树
- 关键字递增排序
- 非叶子节点的子节点数大于1
### (4) B+树
- B+树在B树的基础上，将所有数据保存在叶子节点，非叶子节点用作索引。B+树常用作数据库的索引，因为数据都在同一层所以查询相对稳定，而且B+树的叶子节点有用指针连接起来，方便遍历所有数据。
### (5) 红黑树
- 左根右，不红红，根叶黑，黑路同    
- 节点为黑色或红色
- 根节点是黑色
- 叶子节点是黑色
- 红色节点的两个子节点都是黑色
- 任意一结点到每个叶子结点的路径都包含数量相同的黑结点
- 如果一个结点存在黑子结点，那么该结点肯定有两个子结点
## 排序
### (1) 快排
- 设一个基准值(一般为第一个)，将数组中比基准值小的数据放在左边，将比基准值大的数据放在右边，然后再分别对左右两边递归的进行上面的操作。时间复杂度最差O(n^2),平均O(nLog2n)
### (2) 归并排序
- 分治，将数据不断拆分，然后两两归并成有序序列，递归的向上归并。
    
 ## 计网
### (1)三次握手(假设客户端发送连接请求)
- 客户端向服务端发送数据包，将SYN(同步标志位)置1，随机序号x，客户端进入SYN_SENt状态
- 服务端收到数据包后，向客户端发送数据包，将SYN、ACK(确认位)置1,ack设为x+1，随机序号y，服务端进入SYNC-RCVD状态
- 客户端收到后，向服务端发送数据包，将ACK置1，ack(确认号)设为y+1，序号设为x+1，此次可携带要发送的数据，客户端进入连接状态，服务端收到后进入连接状态
- 三次握手原因：通过三次握手确认客户端和服务端都有正常的发送和接收消息的能力。
- DOS攻击：通过大量虚假ip向服务端发送连接请求但不连接，导致服务器处于等待连接状态不可用。
### (2) 四次挥手(假设客户端发送断开连接请求)
- 客户端向服务端发送数据包，将FIN(终止标志位)置1，随机序号u，进入FIN-WAIT状态
- 服务端接收到后向客户端发送数据包，将ACK置1，随机序号V，ack设为u+1，进入CLOSE-WAIT状态，此时服务端可继续传输数据
- 服务端传输完数据，向客户端发送数据包，将FIN、ACK置1，随机序号w，ack设为u+1，进入LAST-ACK状态
- 客户端接收后向服务端发送数据包，将ACK置1，序号设为u+1，ack为w+1，然后进入TIME-WAIT状态，等待2MSL(最长报文段寿命)后,将连接关闭。服务端接收后关闭连接，若没接收到则重新执行上一步。
- TIME-WAIt，2MSL:防止最后一次挥手服务端没接收到，导致客户端已关闭连接，而服务端没关闭。
### (3) cookie
- 保存在客户端，不够安全。因为http是无状态的，所以需要cookie做用户验证。
### (4) session
- 保存在服务端，相对安全，但session过多会对服务器产生压力，session一般通过cookie实现，服务端会将session id保存在cookie中。如果cookie被禁用，也可以通过url传递session id
### (5) 七层/四层
- 七层：物理层，数据链路层 ，网络层，传输层，会话层，表示层，应用层
- 四层：网络接口层(MAV,VLAN)，网络层(IP,ARP,ICMP)，传输层(TCP,UDP)，应用层(HTTP,DNS,SMTP)
### (6) TCP
- TCP保证可靠传输，建立连接需要三次握手，断开连接需要四次挥手
- 慢开始：由小到大逐渐增大发送窗口，每经过一个传输轮次，就将cwnd(滑动窗口)翻倍，当cwnd超过门限后，采用拥塞控制算法，改为线性增长
- 快重传：接收方每次收到一个失序的报文段后就立即发送重复确认，发送方连续收到三个重复确认就立即重传
- 快恢复：当收到三个重复确认，就将慢开始的门限减半，采用拥塞控制算法。
- 滑动窗口/拥塞控制：发送方和接收方各维护一个窗口，分别为发送窗口和接收窗口。每经过一个往返时间RTT，cwnd就增长1。在慢开始和拥塞避免的过程中，一旦发现网络拥塞，就把慢开始门限设为当前值的一半，并且重新设置cwnd为1，重新慢开始。窗口大小就是无需等待确认而可以继续发送数据的最大值。
### (7) UDP
- 不保证可靠传输，尽最大努力去传输数据，适合像视频通话，视频会议等场景。
### (8) http
- 应用层协议，无状态，无连接，基于TCP协议，默认端口为80.
-  http状态码:2xx请求成功，3xx重定向，4xx客户端错误，5xx服务端错误。400请求参数有问题，403Forbidden，请求参数正确但服务端拒绝请求，404Not Found找不到资源，405请求方法错误。500服务器错误，502Bad Gateway网关问题，代理问题。
### (9) https
- 有加密算法和http协议相比，更加安全，但是服务端需要购买证书，浏览器端安装对应的根证书。默认端口443.
- 加密方式：服务器拥有非对称加密的公钥A和私钥A'，服务器将公钥A发送给浏览器，浏览器随机生成密钥X，并通过A加密，然后传回给服务端。服务端通过私钥解密(只有服务器有私钥)，得到密钥X。
### (10) 输入url到浏览器解析过程
- DNS协议解析域名，首先检查浏览器缓存和本地host文件是否有该域名，如果没有，则递归的向上级域名服务器查询，得到ip地址和端口号。
- ARP协议根据ip地址解析MAC地址，首先检查本地ARP缓存表是否有该ip，如果没有则在局域网内广播，如果不在同一局域网内则由路由器传递，然后对应机器收到广播会单播回去。
- TCP三次握手建立连接，如果用的是https协议，会先对数据进行加密。
- 浏览器解析数据，渲染页面
-  四次挥手，断开连接。
### (11) get和post区别
- get一般用于向服务端请求数据，post一般用于提交数据
- get请求参数放在url中，post请求参数放在request body中
- get请求参数只能进行url编码，post请求参数可以是任意类型
- url长度有限制，各浏览器长度限制不同，post请求参数长度无限制
- 因为get请求参数放在url中，所以参数信息会保存在浏览器历史里，不够安全。post请求不会保存在浏览器历史中。
## 操作系统
### (1) 进程和线程
- 进程是资源分配的最小单位，线程是系统调度的最小单位。进程切换开销大，线程切换开销相对较小。
- 死锁条件：资源互斥，请求和保持，不可剥夺，循环等待。
### (2) linux
## 数据库
### (1) 索引
- 索引是一种数据结构，可以理解为字典，用于加快查询速度，不过索引并非越多越好，创建和维护索引需要耗费额外的时间和空间。
- B+树索引：数据全部有序保存在叶子节点上，查询速度稳定O(logn)，并且叶子节点前后相连，方便遍历所有数据。
- 哈希索引：通过对key进行hash存储，无序，查询速度为O(1)。
### (2) 事务ACID特性
- 原子性：事务是一个整体，事务中的操作要么全部成功，要么失败回滚。
- 一致性：事务总是从一个状态转移到另一个状态。例：A有200元，B有300元，两人互相转账，无论怎样两人账户合都是500元。
- 隔离性：事务之间互不影响，一个事务的操作在提交前对另一个事务是不可见的。
- 持久性：一个事务提交成功，那么所作的修改会永远保存在数据库中。
### (3) 事务隔离级别
- 读未提交：一个事务在提交前，对其他事务是可见的，即事务可以读取到未提交的数据，存在脏读，不可重复读，幻读等问题。
- 读提交：事务在提交前，对其它事务是不可见的，存在不可重复读的问题(两次查询之间，有事务提交了修改，导致查询结果不同)，幻读问题。
- 可重复读：在同一事务中多次读取数据是一致的，解决了不可重复读的问题，存在幻读问题(两次查询之间，有事务插入或删除了记录，导致记录数不一致)。可重复读是Mysql的默认隔离级别。
- 串行化：事务一个一个的执行，牺牲了系统的并发性，可解决事务并发的所有问题。
### (4) 三大范式
- 第一范式：每一列数据都不可再分
- 第二范式：每一列属性都完全依赖于主键
- 第三范式：每一列属性直接依赖于主键，非传递依赖。例：(学号，专业，学院，学院大楼，学院电话)。学院大楼和学院电话实际上是依赖与学院的，属于传递依赖，需要拆分成两个表。
### (6) 乐观锁、悲观锁
- 乐观锁：假设数据修改一般不会发生冲突，在数据提交更新时，才会检测数据是否冲突，适用于读多写少的场景，一般用版本号实现。
- 悲观锁：对数据修改持悲观的态度，每次读取数据都假设其它线程会修改数据，所以需要加锁，主要通过读锁和写锁实现。
### (7) 左连接，右连接
- 左连接： 以左边的表为主
- 右连接： 以右边的表为主

