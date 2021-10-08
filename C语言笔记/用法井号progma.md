使用#progma once
#pragma once  
// Code placed here is included only once per translation unit 

使用宏定义方式
#ifndef HEADER_H_ 
#define HEADER_H_  
// Code placed here is included only once per translation unit  
#endif // HEADER_H_  


![[pragma的常用方法讲解.pdf]]
引用：

![[未命名/#pragma的常用方法讲解_YoungYangD的博客-CSDN博客_#pragma.html]]

引用：
//keil中默认是不支持匿名结构体的，需要编译指令#pragma anon_unions指名。

#pragma anon_unions    
typedef union {    
        unsigned int num;    
        struct {    
                unsigned int nLow        :8;    
                unsigned int nHigh         :8;    
        };    
} Test;    
    
void func(void)    
{    
    Test test;    
    test.num=99;    
    test.nLow=10;    
}

[keil4 #pragma anon_unions](http://www.bubuko.com/infodetail-2669392.html "keil4  #pragma anon_unions,bubuko.com")

原文：https://www.cnblogs.com/liangbo-1024/p/9257920.html



/keil中默认是不支持匿名结构体的，需要编译指令#pragma anon_unions指名。

#pragma anon_unions 
typedef union { 
        unsigned int num; 
        struct { 
                unsigned int nLow        :8; 
                unsigned int nHigh         :8; 
        }; 
} Test; 
 
void func(void) 
{ 
    Test test;  
    test.num=99;  
    test.nLow=10; 
}
————————————————
版权声明：本文为CSDN博主「AndyCheng_hgcc」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/chengde6896383/article/details/72529241