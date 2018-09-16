1、可移植性
    C program can run on other systems.
2、源代码、目标代码、可执行代码
    content written in C language
    include machine langeage code
3、long long占64位，long占32位，short占16位，ing占16位或32位
4、基本数据类型
    11个关键字：int,long,short,unsigned,char,float,double,signed,_Bool,_Complex,_Imaginary.
5、scanf()返回成功读取项的个数 
    输入由字符组成，但是scanf()可以把输入转换成整数值或浮点数值。使用转换说明（如%d或%f）限制了可接受的字符类型，而getchar()和
    使用%c的scanf()接受所有字符
6、递归：C允许函数调用它自己
7、处理非整数输入
    scanf("%*s")跳至下一个空白字符
8、指针
    指针加一指的是增加一个储存单元
    C只保证指向数组任意元素的指针和指向数组后面第1个位置的指针有效。
    不要解引用未初始化的指针。
    两个不同类型的指针不能互相赋值
    相同声明
        typedef int arr4[4];//arr4是一个内含4个int的数组
        typedef arr4 arr3x4[3];//arr3x4是一个内含3个arr4的数组
        int sum2(arr3x4 ar, int rows);
        int sum2(int ar[3][4], int rows);
        int sum2(int ar[][4], int rows);
        int sum2(int (*ar)[4], int rows);
9、const
    可以把const和非const数据指向const指针，不可以把const数据指向普通指针。
10、数组
    复合字面量：(int [2])(10, 20)
    好处：把信息传入函数前不必先创建数组
    C99/C11新增了边长数组，可以用变量表示数组大小。这意味着边长数组的大小延迟到程序运行时才确定。
11、字符串
    以空字符（\0）结尾的char类型数组
    puts()函数只显示字符串，而且自动在显示的字符串末尾加上换行符。
    const char * pt1 = "How to learning?"
    const char ar1[] = "How to learning?"
    初始化数组吧静态存储区的字符拷贝到数组中，而初始化指针只把字符串的地址拷贝给指针，两者主要区别：数组名是常量，而指针名是变量
