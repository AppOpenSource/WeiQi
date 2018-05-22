
# Gradle

## Gradle3.0新特性
首先compile被废弃了，而是分成了两个：implementation和api，
其中api与之前的compile功能基本一致，不再赘述；
implementation就比较高级了，其作用就是，
使用implementation添加的依赖不会再编译期间被其他组件引用到，但在运行期间是完全可见的。
这也是一种代码隔离。


## 参考文献
1、[Android彻底组件化—代码和资源隔离](https://www.jianshu.com/p/c7459b59dcd5)   

