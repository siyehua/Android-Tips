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


21.得到一个布局的方法
```java
private LayoutInflater inflater;   
inflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);  
```
或者: 
```java
LayoutInflaer.from(this).inflate(R.layout.xmlName, null);  
```
或者:
```java
getLayoutInflater(this).inflate(R.layout.xmlName, null);  
```

22:通知Notification

defalut 属性: DEFAULT_ALL 使用所有默认值,包括声音,震动,闪光灯

DEFAULT_LIGHT 使用闪光灯

DEFAULT_SOUNDS 使用声音

 DEFAULT_VIBRATE 使用振动
 
(注意在使用ALL 和ViBrate的时候,要给apk加入震动的权限 )

```xml
<uses-permission  android:name = "android.permission.VIBRATE"/>  
```



23.通过文件名得到对应的ID
```java
 getResources().getIdentifier("文件名", "drawable", getActivity().getApplication().getPackageName());  
//getActivity()碎片中使用//第一个参数:文件名  
//第二个参数:文件类型:drawable,layout  
//第三个参数:文件包名  
```

24.得到SDCard的路径
```java
Environment.getExternalStorageDirectory().toString();  
```

25.得到一个目录下的文件列表(带过滤器)
```java
File[] files= new File("文件路径").listFiles(new FileFilter() {  
              
            @Override  
            public boolean accept(File pathname) {  
                // TODO Auto-generated method stub  
                return false;  
            }  
        });  
```


26.把下载下来的模拟器安装到模拟器上
  
  * 进入到apk的文件夹
  * adb install 名字.apk (可以使用Tab键自动填充名字)



27.自定义SeekBar,PrgoressBar等进度条的背景层等
```xml
<?xml version="1.0" encoding="utf-8"?>  
<layer-list xmlns:android="http://schemas.android.com/apk/res/android" >  
 <!-- 背景层 --> <item android:id="@android:id/background" android:drawable="@drawable/seek_bg"/>   
<!-- 第二进度层 --> <item android:id="@android:id/secondaryProgress" android:drawable="@drawable/second_pro_bg"/>  
 <!-- 第一进度层 --> <item android:id="@android:id/progress" android:drawable="@drawable/first_pro_bg"/></layer-list>  
```
```xml
<?xml version="1.0" encoding="utf-8"?>  
<selector xmlns:android="http://schemas.android.com/apk/res/android">  
  
    <item android:drawable="@drawable/seek_thumb_normal" android:state_pressed="false"/>  
    <item android:drawable="@drawable/seek_thumb_pressed" android:state_pressed="true"/>  
  
</selector> 
```
```xml
<SeekBar  
            android:id="@+id/m_seek"  
            android:layout_width="match_parent"  
            android:layout_height="wrap_content"  
            android:progressDrawable="@drawable/seek_bar_drawable"   
            android:thumb="@drawable/seek_thumb"/>  
```


28.使用手机系统默认的软件打开音频,视频等
```java
/* 播放录音文件 */  
    private void playMusic(File file) {  
        Intent intent = new Intent();  
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);  
        intent.setAction(android.content.Intent.ACTION_VIEW);  
        /* 设置文件类型 */  
        intent.setDataAndType(Uri.fromFile(file), "audio");  
        startActivity(intent);  
    }  
```



29.透明,半透明

Button或者ImageButton的背景设为透明或者半透明

半透明<Button android:background="#e0000000" ... /> 

透明<Button android:background="#00000000" ... />


30.时间View的监听

```java
new TimePickerDialog(this, null, hourOfDay, minute, true).show();//其中null为选择器的监听,true表示是24小时制
```


31.静态注册广播接收器
```xml
<application  
        android:allowBackup="true"  
        android:icon="@drawable/app_icon"  
        android:label="@string/app_name"  
        android:theme="@android:style/Theme.Light.NoTitleBar" >  
        <activity  
            android:name="com.siyehuazhilian.musicplay.MainActivity"  
            android:label="@string/app_name" >  
            <intent-filter>  
                <action android:name="android.intent.action.MAIN" />  
  
                <category android:name="android.intent.category.LAUNCHER" />  
            </intent-filter>  
            <intent-filter>  
                <action android:name="android.intent.action.VIEW" />  
  
                <category android:name="android.intent.category.DEFAULT" />  
  
                <data android:mimeType="audio/*" />  
            </intent-filter>  
        </activity>  
    </application>  
```

一个app有许多个Activity,一个Activity有许多个<intent-filter>,一个<intent-filter>有一个<action>,一个<category>,一个<data>

```xml
<action>表示要执行的动作,常用的标准动作：

ACTION_MAIN，他的值我们比较熟悉：“android.intent.action.MAIN”这个值我们在每个AndroidManifest.xml文档中都可以看到。他标记当前Activity作为一个程序的入口。

ACTION_VIEW,将数据显示给用户。ACTION_VIEW通常和特定的data相配合使用，用于给用户显示数据。

ACTION_DIAL，用于描述给用户打电话的动作，通过和data配合使用将会触发给特定的data的用户打电话。

ACTION_PICK,从特定的一组数据中进行选择数据操作。

ACTION_EDIT,编辑特定的数据。

ACTION_DELETE,删除特定的数据。
```

<category>
```xml
android.intent.category.LAUNCHER表示用快捷方式启动

android.intent.category.DEFAULT表示用默认方式启动,比如说我们打开.doc后缀的格式文件,就会默认用Word打开,如果设置了用WPS.怎默认用WPS.如果没有设置,则选择让用户自己选择一个打开 

android.intent.category.HOME表示在桌面打开
```


<data>表示能容纳的类型

audio/*表示所有的音频

mepg/*表示视频等等


32.使用Intent调用浏览器,电话,短信等
```java
Uri uri = Uri.parse("http://www.baidu.com");  
                        Intent intent = new Intent(Intent.ACTION_VIEW, uri);  
                        startActivity(intent);  
```

33.截屏
```java
View view = getWindow().getDecorView();  
        view.setDrawingCacheEnabled(true);  
        view.buildDrawingCache();  
        Bitmap b1 = view.getDrawingCache();  
        Bitmap bitmap = Bitmap.createBitmap(b1, 0, 0, b1.getWidth(),  
                b1.getHeight());  
        view.destroyDrawingCache();  
```



34,发送图片,彩信,分享的微信朋友圈,QQ说说,新浪微博等
```java
Uri mUri = Uri.parse(("file://"  
                    + Environment.getExternalStorageDirectory() + "/"  
                    + currentDay + ".png"));  
            Intent intent = new Intent(Intent.ACTION_SEND);  
            intent.putExtra(Intent.EXTRA_STREAM, mUri);  
            intent.setType("image/png");  
            startActivity(intent);  
```

35.Message发送一个对象
```java
// Message msg = new Message();  
                    // msg.what = MSG_UPDATE;  
                    // msg.obj = newPro;  
                    // mHandler.sendMessage(msg);  
  
                    Message msg = mHandler.obtainMessage(MSG_UPDATE, newPro);  
                    msg.sendToTarget();  
```


36.GridView宽度不够铺满整个屏幕,可以使用一下方法
```java
android:stretchMode = "columnWidth"  
```

37.设置ImageView的缩放方式,可以平铺.拉伸,适应等
```xml
android:scaleType = "方式"  
```

38.如果一个ImageView始终无法铺满整个屏幕,可以尝试一下方法
  * 看看父控件是否包含这个,如果有,可以删除
  ```xml
    android:paddingBottom="@dimen/activity_vertical_margin"  
    android:paddingLeft="@dimen/activity_horizontal_margin"  
    android:paddingRight="@dimen/activity_horizontal_margin"  
    android:paddingTop="@dimen/activity_vertical_margin"  
  ```
  * 设置图片的缩放方式,因为有可能你的图片比例和屏幕的比例不一样

39.字体加粗
  * 英文字体加粗:在xml文件中使用android:textStyle="bold" 
  * 中文不能通过xml文件将中文设置成粗体，将中文设置成粗体的方法:
    ```java
    TextView tv = (TextView)findViewById(R.id.TextView01); 
    TextPaint tp = tv.getPaint(); 
    tp.setFakeBoldText(true); 
    ```


40.Intent传递对象,可以通过Bundle来传递(前提是Book已经序列化)
```java
Intent intent = new Intent(this,BookView.class);  
Book book = new Book();  
book.setName("manmonth");  
book.setTime("1975");  
book.setAuthor("Brooks");  
Bundle bundle = new Bundle();  
bundle.putParcelable("book", book);  
intent.putExtras(bundle);  
startActivity(intent);  
```
