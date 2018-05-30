
## AppDevMemo

### 在线编辑器
1、[在线MarkDown编辑器MaHua](http://mahua.jser.me/)    
2、[不错的在线富文本编辑器Slate](http://slatejs.org/#/rich-text), [项目地址](https://github.com/ianstormtaylor/slate)       

### 快速开发
1、[Android-ZBLibrary](https://github.com/TommyLemon/Android-ZBLibrary)   
2、

### Logger
Simple, pretty and powerful logger for android

#### Setup
Download
```groovy
implementation 'com.orhanobut:logger:2.2.0'
```
Initialize
```java
Logger.addLogAdapter(new AndroidLogAdapter());
```
And use
```java
Logger.d("hello");
```

### Butter Knife
#### Setup
Download
```groovy
dependencies {
  implementation 'com.jakewharton:butterknife:8.8.1'
  annotationProcessor 'com.jakewharton:butterknife-compiler:8.8.1'
}
```
Sample
```java
class ExampleActivity extends Activity {
  @BindView(R.id.user) EditText username;
  @BindView(R.id.pass) EditText password;

  @BindString(R.string.login_error) String loginErrorMessage;

  @OnClick(R.id.submit) void submit() {
    // TODO call server...
  }

  @Override public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.simple_activity);
    ButterKnife.bind(this);
    // TODO Use fields...
  }
}
```


### 参考文献
1、[Android ADB命令](https://www.jianshu.com/p/56fd03f1aaae)  

