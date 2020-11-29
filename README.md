# c-

const 加在成员函数后面表示该函数不会修改任何数据成员


dynamic_cast在将父类cast到子类时，父类必须要有虚函数，否则编译器会报错。

在类层次间进行上行转换时，dynamic_cast和static_cast的效果是一样的；
在进行下行转换时，dynamic_cast具有类型检查的功能，比static_cast更安全。
当dynamic_cast进行下行转换时，若转换对象实际指向父类指针，则报错bad_cast返回NULL
