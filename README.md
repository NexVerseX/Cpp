# **面向对象与C++程序设计**
***
***

# 2基本数据类型与输入/输出
# 2.1字符集与保留字
保留字 keyword
表2.1
在程序中用到的其他名字不能与C/C++的关键字有相同的拼法和大小写

# 2.2基本数据类型
对所有数据都必须指定其数据类型
程序中所用到（表达）的数据亦应有名字，或为*变量*或为*常量*，它们都对应某个*内存*空间。
数据类型的作用之一，是希望通过每个代表数据名字的性质来归类，不同数据类型之间不能进行混算，内部表达不同，空间占用不同，这都是编译器查错的重要依据。

>内存的概念
像以下的integer1, integer2和 sum这样的变量名实际上对应着计算机内存中的单元。
每个变量都有一个名字、一个数据类型和一个值。

# 2.3变量定义
在程序运行中其值可以改变的量称为*变量*。一个变量应该有一个名字，在内存中占据一定的存储单元。在该存储单元中存放该变量的值。
*注意：变量名与变量值的区别*
+ 变量名（一个符号地址，在对程序编译时系统分配给它一个内存地址）
+ 变量值（在程序中对变量取值，实际上是通过变量名找到相应内存地址，从其存储单元中读取数据）


# 2.4字面量
代表数据的文字
+ 整型数：如12，0，－3等（不带有小数）；
+ 实型数：如4.6，－1.23等；
+ 字符：如‘a’，‘d’等；
+ 字符串：如“abc”
# 2.5常量
程序运行保持不变的实体数据，用一个名字表示，该名字称为*常量*，在定义中加修饰const

常量在定义时必须初始化，常量名不能放在赋值语句的左边 例如：

    const int a=123;
    a = 12;  //error

*变量的定义必须放在执行语句之前*；
如果在执行语句中遇到一个变量，但是该变量还没有被定义，那么编译器会报语法错误 例如：

    int  a =3;
    c = a+1;  // error  c没有定义

*每一个变量被指定为一确定数据类型，在编译时就能为其分配相应的存储单元*；
制定每一变量属于一个类型，这就便于在编译时，据此检查该变量所进行的运算是否合法。

C/C++语言中的变量名可以是任何有效的标识符。
标识符可以是由字母、数字和下划线(_)组成的一系列字符。
例如： integer1, integer2, sum

# 2.6I/O流控制
1. I/O的书写格式

I/O作为流的操作特征

    cin>>a>>b;
    cout<<a<<b;

2. 使用控制符

控制符嵌在流操作中，表2-4 例如：

    cout<<hex<<a;  // 将整数a以16进制输出

3. 控制浮点数值显示

*普通格式*：独立使用setprecision(n)表示有效位数n 例如：

    cout<<setprecision(3)<<12.2675;
    //显示：12.3

*定点表示格式*：fixed与setprecision(n)配合，表示小数精度n位 例如：
  
    double a = 123.56789;
    cout<<fixed<<setprecision(3)<<a*1000<<"\n";
    //显示：123567.890

*科学表示格式*：scientific与setprecision(n)配合，表示小数精度n位 例如：

    cout<<scientific<<a*1000<<"\n";
    //显示：1.236e+05

4. 设置值的输出宽度
设置值的输出宽度和填充字符很有用，但要和#include<iomanip.h>一起用

setw(n)是一次性的 例如：

    cout<<setfill('%')<<setw(5)<<10<<20<<"\n";
    //显示：%%%1020
    //后面的20没有宽度格式控制
例如：

    cout<<10<<setw(5)<<20<<"\n";
    //显示：10   20

若要显示的内容超setw(n)中的n,则设置无效 例如：

    cout<<setw(3)<<12345<<"\n";
    //显示：12345

5. 输出八进制和十六进制数

6. 设置填充字符

7. 左右对齐输出

8. 强制显示小数点和符号

# 2.7printf与scanf
printf和scanf输出入格式是C的输入出方式，它输入出已有的C类型的数据。例如，int,double等


***
# 11.1 从结构到类
+ C语言中的数据类型—数据组织与存储
    自带类型：int系、double系
    构造类型：指针、数组
    自定义类型：结构、（枚举、联合）    
+ C++重新强化类型概念
    数据类型含三要素：数据组织、表达范围、数据操作
+ C++自定义类型
1. C中的struct结构 仅含数据组织

.

    struct Point{ int x;  int y; };

2. C++中的struct结构 可定义数据组织、数据操作

.

    struct Point{ 
        int x; int y;
        void print(){  cout<<'('<<x<<','<<y<<')'; }
    };

3. C++中用class扩充类,可定义数据组织、数据操作

.

    class Point{ 
        int x; int y;
    public:
        void print(){  cout<<'('<<x<<','<<y<<')'; }
    };

# 11.2 软件方法的发展必然

# 11.3 定义成员函数
*在类内定义成员函数*

    #include<iostream>
    using namespace std;
    //---------------------
    class Tdate{
    public://用public说明公有访问
        void Set(int m,int d,int y){   
            month=m; day=d; year=y;
        }
        int IsLeapYear(){              
            return (year%4==0 && year%100!=0)||(year%400==0);
        }
        void Print(){                  
            cout<<month<<"/"<<day<<"/"<<year<<endl;
        }
    private://用private说明私有访问(限制访问)
        int month;
        int day;
        int year;
    };//-------------------
    //类定义结束的分号必须要有
    int main(){
        Tdate a;
        a.Set(2,4,1998);
        a.Print();
    }//--------------------

*在类外定义成员函数*

    #include<iostream>
    using namespace std;
    class Tdate{
    public:            //用public说明公有访问
        void set(int m,int d,int y);   //类中成员函数声明
        int isLeapYear();
        void print();
    private:           //用private说明私有访问
        int month, day, year;
    };//类定义结束的分号
    void Tdate::set(int m,int d,int y){ //类外定义成员函数,函数名前类名::
        month=m; day=d; year=y;
    }
    int Tdate::isLeapYear(){                         
        return (year%4==0&&year%100!=0)||(year%400==0);
    }
    void Tdate::print(){                 
        cout <<month <<"/" <<day <<"/" <<year <<endl;
    }  
    int main(){         
        Tdate a;
        a.set(2,4,1998);   //a对象调用公有成员函数set,置a中日期
        a.print();         //a对象调用公有成员函数print,输出a中日期  
    }

## 类定义与程序编排
+ 类定义,类外定义成员函数,主应用编程,三者可以拆分,合成程序工程

*头文件Tdate.h——类定义,成员函数声明*

    class Tdate{
        int month, day, year;  //默认为private
    public: 
        void set(int m,int d,int y);   
        int isLeapYear();      
        void print();
    };// 类定义结束的分号

*源代码文件Tdate.cpp——成员函数定义*

    #include”Tdate.h”     //用到Tdate类
    #include<iostream>    //用到cout
    using namespace std;
    void Tdate::set(int m,int d,int y){ month=m; day=d; year=y; }
    int Tdate::isLeapYear(){ return (year%4==0&&year%100!=0)||(year%400==0); }
    void Tdate::print(){ cout<<month<<"/"<<day<<"/"<<year<<endl; }  

*源代码文件app.cpp——主函数*

    #include”Tdate.h”    //用到Tdate类
    int main(){          
        Tdate a;           //定义Tdate类对象a
        a.set(2,4,1998);   //a对象调用公有成员函数set,置a中日期
        a.print();         //a对象调用公有成员函数print,输出a中日期
    }  


# 11.4 调用成员函数
+ 除了一般的成员函数调用（前面已经介绍），还有指针与引用方式调用

+ 对象是数据实体,可以有指针和引用,常常在函数中传递对象指针和引用

+ 以前面的程序编排为蓝本,修改app.cpp,调用一个函数,传递对象指针,实现成员函数调用

//源代码文件app.cpp

    #include"tdate.h"
    #include<iostream>
    using namespace std;
    void someFunc(Tdate* pS){
        pS->print();  //pS指针调用成员函数
        if(pS->isLeapYear())
            cout<<"oh oh\n";
        else
            cout<<"right\n";
    }
    int main(){
        Tdate s;
        s.set(2,15,1998);
        someFunc(&s);    //传递对象地址
    }

+ 引用参数实施成员函数调用

//源代码文件app.cpp

    #include"tdate.h"
    #include<iostream>
    using namespace std;
    void someFunc(Tdate& rS){
        rS.print();  //rS是引用
        if(rS.isLeapYear())
            cout<<"oh oh\n";
        else
            cout<<"right\n";
    }
    int main(){
        Tdate s;
        s.set(2,15,1998);
        someFunc(s);    //对象引用传递
    }


# 11.5 保护成员

# 11.6 屏蔽类的内部实现
+ 程序中,类内是一个世界,类外是一个世界

+ 类内数据由成员函数来设置和修改,不允许类外直接修改数据成员(private),保护类内世界的清静,数据错误由成员函数担责
  
+ 类外是调用该类成员函数的应用程序,无须也不允许关心类的细节

.

    class Student{
        int semesHour;
        float gpa;
    public:
        float addCourse(int hours, float grade){
            gpa = semesHour*gpa+grade*hours;  //总分
            semesHour += hours;               //调整学时
            gpa /= semesHour;                 //调整平均成绩
        }
        float grade(){ return gpa; }        //获取平均成绩
        int hours(){ return semesHour; }    //获取学时
    };
    int main(){
        Student s;
        s.addCourse(3, 4.5);    //通过该成员函数修改数据成员
        cout<<s.gpa;            //错:不该直接取用
        cout<<s.grade();
        s.semesHour += 1;       //错:类外不允许访问类内私有数据
    }

+ 类编程:设计类(类定义和类实现)
+ 分离类编程: 提供公有成员函数为应用编程所用,屏蔽私有数据,使内部实现高度灵活,并对操作正确性负责

//用到sqrt(), atan()函数

    #include<iostream>
    #include<cmath>   
    using namespace std;
    class Point{        //定义坐标点类, *第一种实现*
    public:
        void set(double ix, double iy) { x=ix;  y=iy; }     //设置坐标
        double xOffset() { return x; }                      //取y轴坐标分量
        double yOffset() { return y; }                      //取x轴坐标分量
        double angle() { return (180/3.14159)*atan2(y,x); } //取点的极坐标
        double radius() { return sqrt(x*x+y*y); }           //取点的极坐标半径
    private:
        double  x, y;      //x,y轴分量
    } p;   //创建p对象
    int main(){
        for(double x,y; cin>>x>>y && x>=0; ){ //重复输入x和y轴分量,直到x分量小于0
            p.set(x,y);
            cout<<"angle="<<p.angle()<<",radius="<<p.radius()
            <<",x offset="<<p.xOffset()<<",y offset="<<p.yOffset()<<endl;
      }
    }


+ 应用编程者任凭类编程如何修改,对使用类的代码都无需修改

//用到sqrt(),atan2(),cos(),sin()

    #include<iostream>
    #include<cmath>   
    Using namespace std;
    class Point{        //定义坐标点类, *第二种实现*
    public:
        void set(double ix, double iy) { //设置坐标
            a=atan2(iy, ix); 
            r=sqrt(ix*ix+iy*iy); 
        }
        double xOffset() { return r*cos(a); }      //取y轴坐标分量
        double yOffset() { return r*sin(a); }      //取x轴坐标分量
        double angle() { return (180/3.14159)*a; } //取点的极坐标
        double radius() { return r; }              //取点的极坐标半径
    private:
        double  a, r;      //极坐标弧度,半径
    } p;      //创建p对象
    int main(){ //使用类者代码(main函数)不需要作任何修改
        for(double x,y; cin>>x>>y && x>=0; ){ //输入x和y轴分量,直到x分量值小于0
            p.set(x,y);
            cout<<"angle="<<p.angle()<<",radius="<<p.radius()
            <<",x offset="<<p.xOffset()<<",y offset="<<p.yOffset()<<endl;
      }
    }

# 11.7 再论程序结构
