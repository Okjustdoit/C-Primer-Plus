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
9、ANSI C类型限定符
    const类型限定符
        可以把const和非const数据指向const指针，不可以把const数据指向普通指针。
        const float * pf;
        float * const pf;
        const放在*左侧任意位置，限定了指针指向的数据不能改变，const放在*右侧，限定指针本身不能改变，也就是指针指向的地址不能改变
    volatile 类型限定符
    restrict 类型限定符
        允许编译器优化某部分代码以更好地支持计算，它只能用于指针，表明该指针是访问数据对象的唯一且初始的方式
    _Atomic 类型限定符
        并发程序设计吧程序执行分成可以同时执行的多个线程，当一个线程对一个原子类型的对象执行原子操作时，其他线程不能访问该对象
10、数组
    复合字面量：(int [2])(10, 20)
    好处：把信息传入函数前不必先创建数组
    C99/C11新增了边长数组，可以用变量表示数组大小。这意味着边长数组的大小延迟到程序运行时才确定。
非自动数组大小应该死整形常量表达式（整形常量组合，枚举常量和sizeof表达式），不包括const声明的值
11、字符串
    以空字符（\0）结尾的char类型数组
    puts()函数只显示字符串，而且自动在显示的字符串末尾加上换行符。
    const char * pt1 = "How to learning?"
    const char ar1[] = "How to learning?"
    初始化数组吧静态存储区的字符拷贝到数组中，而初始化指针只把字符串的地址拷贝给指针，两者主要区别：数组名是常量，而指针名是变量
    读取字符串函数：scanf(), gets()和 fgets()
        fgets(words, STLEN，stdin);
    输出字符串函数：printf(), puts()和 fputs()
        fputs(words, stdout);
    strlen()函数用于统计字符串长度
    strcat()函数用于拼接字符串
    strcmp()函数比较的是字符串，不是字符，参数是字符串
12、空字符和空指针
    空字符（或'\0'）是用于标记C字符串末尾的字符，其对应字符编码是0，是整数类型
    空指针（或NULL）有一个值，该值不会与任何数据的有效地址对应，是指针类型
13、作用域、链接、存储期
    块作用域、函数作用域、函数原型作用域、文件作用域
    外部链接（全局链接）、内部链接（文件作用域）、无链接
    静态存储期、线程存储期、自动存储期、动态分配存储期
    
    寄存器变量 register int quick;
        由于寄存器变量存储在寄存器中而非内存中，所以无法获取寄存器变量的地址
    静态变量（static variable）
        静态的意思是该变量在内存在原地不动，不是说它的值不变
    C有6个关键字作为存储类别说明符：auto, register, static, extern, _Thread_local, typedef
14、分配内存：malloc()/calloc和free()
    #include <stdlib.h>
    创建一维数组
        double * ptd;
        ptd = (double *) malloc(30 * sizeof(double));
    创建二维数组
        int (* p2)[6];
        int (* p3)[m];
        p2 = (int *) malloc(n * 6 * sizeof(int));//nx6 数组
        p3 = (int *) malloc(n * m * sizeof(int));//nxm 数组(要求支持边长数组）
15、文件
    文件指针fp并不指向实际的文件，它指向一个包含文件信息的数据对象，其中包含操作文件的I/O函数所用的缓冲区信息。因为标准库中的
    I/O函数使用缓冲区，所用他们不仅要知道缓冲区的位置，还要知道缓冲区被填充的程度以及操作哪一个文件
    getc()和putc()函数与getchar()和putchar()函数类似，不同的是要告诉getc()和putc()函数使用哪一个文件
    ch = getchar();//从标准输入中获取一个字符
    ch = getc(fp);//从fp指定的文件中获取一个字符
    putc(ch, stdout)与putchar(ch)的作用相同
    fseek()和ftell()工作原理
        fseek(fp, 0L, SEEK_SET);//定位至文件开始处
        fseek(fp, 2L, SEEK_CUR);//从文件当前位置前移2个字节
        fseek(fp, -10L, SEEK_END);//从文件尾处回退10个字节
        
        last = ftell(fp);
        ftell()函数的返回类型是long,它返回的是当前位置，通过返回距文件开始处的字节数来确定文件的位置
    标准I/O机理
        fopen()函数“打开一个流”，如果以文本文件打开该文件，就获得一个文本流，如果以二进制模式打开该文件，就获得一个二进制流
        输入函数: fscanf(), getc(), fgets()
    //以二进制格式把数组写入文件
    /*
    *写入地址：numbers
    *数据块数量：ARSIZE
    *指定代写入的文件：iofile
    */
	fwrite(numbers, sizeof(double), ARSIZE, iofile);
	fclose(iofile);
    
    fread(&value, sizeof(double), 1, iofile);
16、结构体
    指向结构体的指针struct guy *him;
    传递结构的地址double sum(const struct funds * money)
	传递结构double sum(struct funds moolah)
    16.1malloc()
    void getinfo (struct namect * pst)
    {
        char temp[SLEN];
        s_gets(temp, SLEN);
        //分配内存储存名
        pts->fname = (char *)malloc(strlen(temp) + 1);
        //把名拷贝到已分配的内存
        strcpy(pst->fname, temp);
    }
    16.2复合字面量和结构
    /*
     *函数名：rect_area
     *结构名：rect
    */
    area = rect_area( (struct rect) {10.5,20.0}
    163.伸缩型数组成员
    伸缩型数组成员必须是结构的最后一个成员
	结构中必须至少有一个成员
	伸缩数组的声明类似普通数组，只是它的方括号中是空的
	struct flex
	{
		int count;
		double average;
		double scores[];//伸缩型数组成员
	}
	16.4匿名结构
17、联合union
	联合是一种数据类型，它能在同一个内存空间中储存不同的数据类型（不是同时储存）
	union hold{
		int digit;
		double bigfl;
		char letter;
	}
18、枚举
	声明符号名称来表示常量，使用enum关键字
	enum spectrum {red, orange, yellow, green, blue, biolet};
	enum spectrum color;
19、typedef
	为某一类型自定义名称
	与#define有3处不同
	typedef创建的符号名只受限于类型，不能用于值
	typedef由编译器解释，不是处理器
	在其受限范围内，typedef不#define更灵活
20、优先级
	[]和()具有相同的优先级，它们比*的优先级高
21、函数和指针
	void (*fp)(char *);//fp是一个指向函数的指针
	void ToUpper(char *);
	pf = ToUpper;
22、移位运算符
	左移：左侧运算对象移出左末端位的值丢失，在右端用0填充
	number << n; //number乘2的n次幂
	number >> n; //如果number为非负，则用number除以2的n次幂
	
	位字段：
	是一个signed int或unsigned int类型变量中的一组相邻的位，位字段通过一个结构声明来建立，该结构声明为每个字段提供标签，并确定该字段的宽度
	声明建立一个4个1位的字段
	struct{
		unsigned int autfd : 1;
		unsigned int bldfc : 1;
		unsigned int undln : 1;
		unsigned int itals : 1;
	}prnt;
	赋值
	prnt.itals = 0;
	prnt.undln = 1;
