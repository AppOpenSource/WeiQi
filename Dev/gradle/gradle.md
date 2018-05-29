
# Gradle

## api和implementation区别      
1、完全等同于compile指令，没区别，你将所有的compile改成api，完全没有错       
2、这个指令的特点就是，对于使用了该命令编译的依赖，    
对该项目有依赖的项目将无法访问到使用该命令编译的依赖中的任何程序，       
也就是将该依赖隐藏在内部，而不对外部公开。      
简单的说，就是使用implementation指令的依赖不会传递。     

### 建议
在GoogleIO相关话题的中提到了一个建议，就是依赖首先应该设置为implementation的，     
如果没有错，那就用implementation，如果有错，那么使用api指令。   
使用implementation会使编译速度有所增快。    

## Gradle3.0新特性
首先compile被废弃了，而是分成了两个：implementation和api，
其中api与之前的compile功能基本一致，不再赘述；
implementation就比较高级了，其作用就是，
使用implementation添加的依赖不会再编译期间被其他组件引用到，但在运行期间是完全可见的。
这也是一种代码隔离。


## 参考文献
1、[Android彻底组件化—代码和资源隔离](https://www.jianshu.com/p/c7459b59dcd5)   

