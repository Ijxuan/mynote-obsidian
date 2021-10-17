只有这几个优先级了


![[Pasted image 20211017155025.png]]
![[Pasted image 20211017155206.png]]


这个问题已经过去很久了。但我还是写一下答案吧。有机会自己写一篇。  
在cmsis-rtos v1中是通过下面这个函数来转化优先级的：  

1.  /* Convert from CMSIS type osPriority to FreeRTOS priority number */  
    
2.  static unsigned portBASE_TYPE makeFreeRtosPriority (osPriority priority)  
    
3.  {  
    
4.    unsigned portBASE_TYPE fpriority = tskIDLE_PRIORITY;  
    
5.      
    
6.    if (priority != osPriorityError) {  
    
7.      fpriority += (priority - osPriorityIdle);  
    
8.    }  
    
9.      
    
10.    return fpriority;  
    
11.  }

_复制代码_

翻译一下就是在freeRTOS中的优先级fpriority = tskIDLE_PRIORITY + priority - osPriorityIdlepriority的值是什么呐？在cmsis.os.c中有一段代码：  

1.  typedef enum  {  
    
2.    osPriorityIdle          = -3,          ///< priority: idle (lowest)  
    
3.    osPriorityLow           = -2,          ///< priority: low  
    
4.    osPriorityBelowNormal   = -1,          ///< priority: below normal  
    
5.    osPriorityNormal        =  0,          ///< priority: normal (default)  
    
6.    osPriorityAboveNormal   = +1,          ///< priority: above normal  
    
7.    osPriorityHigh          = +2,          ///< priority: high  
    
8.    osPriorityRealtime      = +3,          ///< priority: realtime (highest)  
    
9.    osPriorityError         =  0x84        ///< system cannot determine priority or thread has illegal priority  
    
10.  } osPriority;

_复制代码_

可以看出osPriorityNormal是0，可以看作一个基准。对于osPriorityNormal来说在freeRTOS的优先级是tskIDLE_PRIORITY - osPriorityIdle  
那么在task.h中规定了它的值。比如stm32cubemx生成的f0的工程中默认取值是：  

1.  /**  
    
2.  * Defines the priority used by the idle task.  This must not be modified.  
    
3.  *  
    
4.  * \ingroup TaskUtils  
    
5.  */  
    
6.  #define tskIDLE_PRIORITY                        ( ( UBaseType_t ) 0U )

_复制代码_

而osPriorityIdle在上面的取值是-3.所以可以看到实际上真正的几种实际上是osPriorityIdle（因为tskIDLE_PRIORITY + osPriorityIdle - osPriorityIdle = tskIDLE_PRIORITY）。  
对于osPriorityNormal来说。这个取值在freeRTOS中的优先级是：tskIDLE_PRIORITY+3  
而osPriorityIdle的优先级就是tskIDLE_PRIORITY 这样保证了freeRTOS和cmsis-RTOS的idle优先级的一致。  
这一点在优先级较多的时候还行。但对于CM0那种可设置优先级只有4个的任务来说，害死人。（这一点还没有查看代码中有没有保险措施，但如果不加保护，优先级就会乱套。）  
  
  
但freeRTOS的优先级还不是在真正的优先级。这部分可以查看一下其他人关于freeRTOS的描述。  
  
  
下面是深入篇。如果你在调试的时候发现显示的优先级和自己设置的不同，不要奇怪。比如keil上面显示的是内核优先级。具体计算可以看下面说明。  
另外对于M0内核和M3/M4内核的STM32产品内核优先级的计算是不同的。M0的内核优先级是8位中的高2位可配置。而M3和M4是高4位可配置。  
  
这是core_cm0.h的代码（其中__NVIC_PRIO_BITS的宏定义是2）：  

1.  __STATIC_INLINE void NVIC_SetPriority(IRQn_Type IRQn, uint32_t priority)  
    
2.  {  
    
3.    if ((int32_t)(IRQn) < 0)  
    
4.    {  
    
5.      SCB->SHP[_SHP_IDX(IRQn)] = ((uint32_t)(SCB->SHP[_SHP_IDX(IRQn)] & ~(0xFFUL << _BIT_SHIFT(IRQn))) |  
    
6.         (((priority << (8U - __NVIC_PRIO_BITS)) & (uint32_t)0xFFUL) << _BIT_SHIFT(IRQn)));  
    
7.    }  
    
8.    else  
    
9.    {  
    
10.      NVIC->IP[_IP_IDX(IRQn)]  = ((uint32_t)(NVIC->IP[_IP_IDX(IRQn)]  & ~(0xFFUL << _BIT_SHIFT(IRQn))) |  
    
11.         (((priority << (8U - __NVIC_PRIO_BITS)) & (uint32_t)0xFFUL) << _BIT_SHIFT(IRQn)));  
    
12.    }  
    
13.  }

_复制代码_

其中  

1.  #define _BIT_SHIFT(IRQn)         (  ((((uint32_t)(int32_t)(IRQn))         )      &  0x03UL) * 8UL)

_复制代码_

  
  
这是core_cm4.h的代码（其中__NVIC_PRIO_BITS的宏定义是4）：  

1.  __STATIC_INLINE void NVIC_SetPriority(IRQn_Type IRQn, uint32_t priority)  
    
2.  {  
    
3.    if ((int32_t)(IRQn) < 0)  
    
4.    {  
    
5.      SCB->SHP[(((uint32_t)(int32_t)IRQn) & 0xFUL)-4UL] = (uint8_t)((priority << (8U - __NVIC_PRIO_BITS)) & (uint32_t)0xFFUL);  
    
6.    }  
    
7.    else  
    
8.    {  
    
9.      NVIC->IP[((uint32_t)(int32_t)IRQn)]               = (uint8_t)((priority << (8U - __NVIC_PRIO_BITS)) & (uint32_t)0xFFUL);  
    
10.    }  
    
11.  }

_复制代码_

m0的处理非常复杂，基本上最终的优先级是中断号和可配置中断的组合计算。  
m4的简单一点，可以看出对于优先级不小于0的中断来说就是将优先级前移4位。  
  
另外在F0的工程中发现没有configLIBRARY_MAX_SYSCALL_INTERRUPT_PRIORITY和configLIBRARY_LOWEST_INTERRUPT_PRIORITY的定义。在cubemx的配置中应该是无效的（但后者可以影响mx自动设置一些中断的优先级。还是要设置。）：  
![st-img](https://shequ.stmicroelectronics.cn/data/attachment/forum/201903/31/184140qtld7do3yxysqc3y.jpg)  
具体情况看能否找到官方文档再说。