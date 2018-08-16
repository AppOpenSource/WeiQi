
## studio报错及处理     

1、问题一：       
Error:Execution failed for task ':app:preDebugAndroidTestBuild'. > Conflict with dependency 'com.android.support:support-annotations' in project ':app'. Resolved versions for app (26.1.0) and test app (27.1.1) differ. See https://d.android.com/r/tools/test-apk-dependency-conflicts.html for details.

解决办法：      
在app下的build.gradle文件中的dependences {}中添加如下代码：       
    androidTestCompile('com.android.support:support-annotations:26.1.0') {         
        force = true         
    }        
    
参考文献：       
[关于android studio 出现Error:Execution failed for task ':app:preDebugAndroidTestBuild'. 的解决办法](https://blog.csdn.net/fighting_2017/article/details/80244982)


