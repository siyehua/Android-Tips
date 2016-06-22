# Android-Tips

1.设置内边距与外边距
```xml
<android:panddingandroid:pandding = "5dp"  
android:magin = "5dp"/>  
```


2.字体单位用sp,控制长宽高,使用dp


3.把一个RadioButton按键设置成没有圆圈的样式
```xml
<android:button = "@/null"/>   
```


4.按照比例来设置控件的大小
```xml
<android:layout_weight  = "数值"/>  
```
注意:这个属性只有在父控件或者本身是LinearLayout的时候才会有该属性


5.用Toast显示一句话
```java
Toast.makeText(context, "要显示的文字",时间毫秒).show();  
```
注意Toast不要放在子线程中


6.如果继承了ListViewActivity,则布局文件中不可以在加上@+id属性


7.把ProgressBar控件设置成水平方向上的进度条
```xml
style = "?android:attr/progressBarStyleHorizontal"  
```

8.设置ProgressBar的进度
```java
//设置第一进度条  
setProgress(i);  
  
//设置第二进度条  
setSecondaryProgress(i)  
```


9.把一个控件设置成是不可见的
```xml
<android:visibility = "gone"/>  
```
重新设置为可见的
```java
findViewById(R.id.控件).setVisibility(View.VISIBLE);  
```


10.把一个Activity设置成对话框模式,可以在AndroidMainfest.xml中添加一个样式
```xml
android:theme = "@android:style/Theme.Dialog"  
```


11.弹出一个对话框
```java
AlertDialog.Builder dialog = new AlertDialog.Builder(this);  
        dialog.setTitle("设置标题");  
        dialog.setMessage("显示的内容");  
        dialog.show();//把这个dialog显示出来  
```
或者
```java
new AlertDialog.Builder(this).setTitle("标题").setMessage("内容").show();  
```


12.当组件超过手机的屏幕时,可以使用ScrollView来滚动视图
    * ScrollView默认是垂直滚动的,想要水平滚动,可以使用:HorizontalScorllView
    * ScrollView只能有一个子元素
    * <android:scrollview = "none"/>可以隐藏滚动条,加入具体数值可以设置滚动条的长度


13.RatingBar

设置星星个数:
```xml
<android:numberStars = "10"/>  
```
设置RatingBar为不一个指示器,就是说用户不可以更改的
```xml
android:inIndicator = "true"  
//或者  
style = "?android:attr/ratingBarStyleIndicator"  
```


14.把一个Activity或者一个apk应用设置成没有标题,或者全屏

//没有标题  
```xml
android:theme="@android:style/Theme.Light.NoTitleBar"  
```
//全屏
```xml
android:theme="@android:style/Theme.Light.NoTitleBar.Fullscreen"  
```
或者在Activity这么设置:
```java
// If the Android version is lower than Jellybean, use this call to hide
        // the status bar.
        if (Build.VERSION.SDK_INT < 16) {
            getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
                    WindowManager.LayoutParams.FLAG_FULLSCREEN);
        }else{
            View decorView = getWindow().getDecorView();
            // Hide the status bar.
            int uiOptions = View.SYSTEM_UI_FLAG_FULLSCREEN;
            decorView.setSystemUiVisibility(uiOptions);
            // Remember that you should never show the action bar if the
            // status bar is hidden, so hide that too if necessary.
            ActionBar actionBar = getActionBar();
            actionBar.hide();
        }
        setContentView(R.layout.activity_main);
```


15.动态获得屏幕的宽度和高度
```java
screenWidth = ((WindowManager) context  
                .getSystemService(Context.WINDOW_SERVICE)).getDefaultDisplay()  
                .getWidth();  
        screenHeight = ((WindowManager) context  
                .getSystemService(Context.WINDOW_SERVICE)).getDefaultDisplay()  
                .getHeight();  
```
或者:
```java
DisplayMetrics display = new DisplayMetrics();  
        getWindowManager().getDefaultDisplay().getMetrics(display);  
        int width = display.widthPixels;  
        int height = display.heightPixels;  
```

16.让应用程序自动适应屏幕

当手机横屏的时候应用程序也自动横屏(重力感应)

AndroidManifest.xml→Application→Activity类→Screen orientation→sensor

或者在Activity中增加:
```xml
android:screenOrientation= "sensro"  
```


17.利用反射动态获得drawable目录下的图片
```java
Field[] fields = R.drawable.class.getDeclaredFields();  
        //获得文件名  
        fields[i].getName();  
        //获得drawable的ID  
        fields[i].getInt(R.drawable.class);  
```


18.Andorid Studio 快捷打开文件:双击Shift


19.滚动
```java
private ScrollView scrollView = null;  
  
//向上滚动  
scrollView.scrollBy(0, -5);  
//向下滚动  
scrollView.scrollBy(0, 5);  
//向左滚动  
scrollView.scrollBy(-5, 0);  
//向右滚动  
scrollView.scrollBy(5, 0);  
//滚动到一个绝对的位置(只能滚动一次)  
scrollView.scrollTo(0, 100);  
//滚动到一个指定的控件的下面  
scrollView.scrollBy(0, kongjian.getBotton());  
```


20.如果在自定义View中重写了onTounchEvent()方法,则应该返回true,否则该事件消失,下次无法在接收事件

同时,必须重写Activity中的onTounchEvent()方法

