>强引用最常见，只要把一个对象赋给一个引用变量，这个引用变量就是一个强引用。
>
>==强引用：只要对象没有被置null，在GC时就不会被回收。==

>软引用需要继承`SoftReference`。
>
>==软引用：如果内存不足了，只有软引用指向的对象就会被回收。==

>弱引用又更弱了，需要继承`WeekReference`。
>
>==弱引用：只要发生GC，只要弱引用指向的对象会被回收。==

>虚引用需要继承`PhantomReference`。
>
>==虚引用的主要作用：跟踪对象垃圾回收的状态，当回收时通过引用队列做些通知类的工作。==

