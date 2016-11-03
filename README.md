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
```xml
半透明<Button android:background="#e0000000" ... /> 

透明<Button android:background="#00000000" ... />
```

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


41.TextView跑马灯效果

TextView中可以设置一个ellipsize属性,作用是当文字长度超过textview宽度时的显示方式:

例如，"encyclopedia"显示, 只是举例，以实际显示为准：）

```xml
android:ellipsize=”start”—–省略号显示在开头 "...pedia"
android:ellipsize=”end”——省略号显示在结尾  "encyc..."
android:ellipsize=”middle”—-省略号显示在中间 "en...dia"
android:ellipsize=”marquee”–以横向滚动方式显示(需获得当前焦点时)
 ```
对于使用marquee即滚动显示方式的，需要当前textview获得焦点才会滚动。

所以有时可能因为实际需要，textview未获得焦点或者需要多个textview都同时滚动显示时，可以采用以下办法：

因为判断textview是否处于focused状态是通过它本身isFocused()方法，这样只要此方法返回为true时，即认为处于focused的状态，就可以滚动啦。

所以可以通过继承TextView类，并override isFocused()方法来控制是否滚动咯



42.设置RadioGroup选中与没有选中时的颜色(背景色)或者是图片

首先新建一个res/下新建一个color的目录,新建一个radiogroup_selecked_bg.xm文件
```xml
<?xml version="1.0" encoding="utf-8"?>  
<selector xmlns:android="http://schemas.android.com/apk/res/android">  
  
    <item android:state_checked="true" android:color="@color/conversion_item_bg_checked"/>  
    <item android:state_checked="false" android:color="@color/conversion_item_bg_unchecked"/>  
  
</selector>  
```
注意后面的@color必须在res/values/color.xml中定义好,不能直接写
```xml
android:color = "#ffffff"这样写是不会有效果的  
然后再RadioGroup中加入属性:android:background = "@color/radiogroup_selecked_bg(就是一开始建立的文件的名字)"  
```

43.ListView的分割线  

```xml
android:divider="@color/conversion_item_divider"  
android:dividerHeight="1dp"  
//注意这两个要一起用,如果没有第二个,默认是0dp,即没有效果  
android:cacheColorHint="#00000000"  //设置拖动背景色为透明  
android:dividerHeight="30px"         //listview item之间的高度
android:divider="@drawable/ic_launcher"    //listview item之间的背景或者说是颜色
android:fadingEdge="vertical"         //上边和下边有黑色的阴影      值为none的话就没有阴影
android:scrollbars="horizontal|none"   //只有值为horizontal|vertical的时候，才会显示滚动条，并且会自动影藏和显示
android:fastScrollEnabled="true"        //快速滚动效果，配置这个属性，在快速滚动的时候旁边会出现一个小方块的快速滚动效果，自动隐藏和显示，
android:scrollbarStyle="outsideInset"  //四个值的含义如下
1>outsideInset :  该ScrollBar显示在视图(view)的边缘,增加了view的padding. 如果可能的话,该ScrollBar仅仅覆盖这个view的背景.
2>outsideOverlay :  该ScrollBar显示在视图(view)的边缘,不增加view的padding,该ScrollBar将被半透明覆盖
3>insideInset :该ScrollBar显示在padding区域里面,增加了控件的padding区域,该ScrollBar不会和视图的内容重叠.
4>insideOverlay : 该ScrollBar显示在内容区域里面,不会增加了控件的padding区域,该ScrollBar以半透明的样式覆盖在视图(view)的内容上.
```

44.android 锁定横屏
    
    要实现这个目的，只需要在AndroidManifest.xml里声明Activity的时候加上一个属性：
　　```xml
　　android:screenOrientation，属性取值landscape为固定横屏、portrait为固定纵屏幕。
　　```
　　代码：
　　```java
　　setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE););//强制为横屏
　　setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT);//竖屏
　　```
　　============延伸========
　　
　　屏幕会自动切换时，默认状态的应用程序，会重新调用onCreate，相当于重新启动了一次应用程序。
　　
　　同时，layout可能因为横屏带来不能合理适配的问题。
　　
　　为了解决旋屏和键盘切换引起的程序重启问题，还需要增加一个属性：android:configChanges。
　　
　　这个属性可以理解为一个监听器，它将拦截旋屏和键盘切换事件，阻止程序重启而变为回调onConfigurationChanged方法。
　　
　　这里常用的属性取值为：keyboardHidden|orientation。


45.设置标志位1和-1,true和false
```java
if(flag){  
flag = false;}  
else{  
flag = true;}  
  
//只需要这样  
flag = flag != true;  
  
//同样,1和-1可以通过这样  
i =  i*-1;  
```

46.设置button主动被点击

怎么触发onclicklistener呢?可以用这个方法:
```java
button.perfromClick();  
```


47.Intent跳转到另外一个应用的Activity
```java
intent.setComponent(new ComponentName(  
                            "要跳转的应用的包名",  
                            "要跳转的应用的包名加类名"));  
```
```java
intent.setComponent(new ComponentName(  
                            "com.siyehua.test.otherapp",  
                            "com.siyehua.test.otherapp.SpaceActivity"));  
```

同时:必须在目标的应用里设置Activity的Actioon和catoery

```xml
<activity  
            android:name="com.siyehua.test.otherapp.SpaceActivity">
            <intent-filter>  
                <action android:name="com.siyehuazhilian.abc" />  
  
                <category android:name="android.intent.category.LAUNCHER" />  
            </intent-filter>  
        </activity>  
```

48.检测手机里时候包含该应用
```java
    private boolean getInstallFlag(String appPackageName) {  
        List<PackageInfo> list = getPackageManager().getInstalledPackages(  
                PackageManager.GET_PERMISSIONS);  
        for (PackageInfo packageInfo : list) {  
            if (packageInfo.packageName.equals(appPackageName)) {  
                return true;  
            }  
        }  
  
        Toast.makeText(this, "检测到您的手机不存在闪购客户端,现在为您跳转到应用商店下载", 1000).show();  
        Uri uri = Uri.parse("market://search?q=" + "123");  
        Intent it = new Intent(Intent.ACTION_VIEW, uri);  
        startActivity(it);  
        return false;  
    }  
```

49.在java代码中设置控件的大小和位置
```java
GridView mGrid= (GridView) findViewById(R.id.gridview);   
LinearLayout.LayoutParams linearParams = (LinearLayout.LayoutParams) mGrid.getLayoutParams(); // 取控件mGrid当前的布局参数  
linearParams.height = 75;// 当控件的高强制设成75象素  
mGrid.setLayoutParams(linearParams); // 使设置好的布局参数应用到控件mGrid2  
比如
TextView mTextView = new TextView(context);
mTextView.setPadding(left, top, right, bottom);// 通过自定义坐标来放置你的控件
或者
TextView mTextView = new TextView(context);
RelativeLayout.LayoutParams params = (RelativeLayout.LayoutParams)xxxx.getLayoutParams();
params.setMargins(left, top, right, bottom));// 通过自定义坐标来放置你的控件
mTextView .setLayoutParams(params);
注意LayoutParams可能是LinearLayout,也可能是RelativeLayout,要看当前控件的父控件是哪个
```

50.设置可见动画

注意该属性是设置在parent group中gone
```xml
android:animateLayoutChanges="true"
```

51.刷新某个文件的uri
```java
public static void scanPhotos(String filePath, Context context) {  
        Intent intent = new Intent(Intent.ACTION_MEDIA_SCANNER_SCAN_FILE);  
        Uri uri = Uri.fromFile(new File(filePath));  
        intent.setData(uri);  
        context.sendBroadcast(intent);  
    }  
```

52.设置对话框的位置Dialog
```java
requestWindowFeature(Window.FEATURE_NO_TITLE);  
        DisplayMetrics display = new DisplayMetrics();  
        getWindowManager().getDefaultDisplay().getMetrics(display);  
        int width = display.widthPixels;  
        int height = display.heightPixels;  
        Window dialogWindow = this.getWindow();  
        WindowManager.LayoutParams lp = dialogWindow.getAttributes();  
        dialogWindow.setGravity(Gravity.CENTER);  
        lp.width = width; // 宽度  
        lp.height = (int) (height * 0.6); // 高度  
        lp.x = 0; // 新位置X坐标  
        lp.y = lp.height; // 新位置Y坐标  
        dialogWindow.setAttributes(lp);  
```

53.EditeText模仿输入法删除EditeText的文本
```java
//动作按下  
        int action = KeyEvent.ACTION_DOWN;  
        //code:删除，其他code也可以，例如 code = 0  
        int code = KeyEvent.KEYCODE_DEL;  
        KeyEvent event = new KeyEvent(action, code);  
        searchEditText.onKeyDown(KeyEvent.KEYCODE_DEL, event); //抛给系统处理了  
```


54.通过uri得到文件路径(文件属性)
```java
// 保存选择的铃声Uri  
        Uri pickedUri = data  
                .getParcelableExtra(RingtoneManager.EXTRA_RINGTONE_PICKED_URI);  
  
        String[] proj = { MediaStore.Audio.Media.DATA };  
  
        Cursor actualimagecursor = managedQuery(pickedUri, proj, null, null,  
                null);  
  
        int actual_image_column_index = actualimagecursor  
                .getColumnIndexOrThrow(MediaStore.Audio.Media.DATA);  
  
        actualimagecursor.moveToFirst();  
  
        String img_path = actualimagecursor  
                .getString(actual_image_column_index);  
  
        File file = new File(img_path);  
```

57.打开系统铃声
```java
// 打开系统铃声设置  
        Intent intent = new Intent(RingtoneManager.ACTION_RINGTONE_PICKER);  
        // 设置铃声类型和title  
        intent.putExtra(RingtoneManager.EXTRA_RINGTONE_TYPE,  
                RingtoneManager.TYPE_ALARM);  
        intent.putExtra(RingtoneManager.EXTRA_RINGTONE_TITLE, "设置闹铃铃声");  
        // 当设置完成之后返回到当前的Activity  
        startActivityForResult(intent, 10086);  
```

58. 让ListView滚动到最底部
```java
// msgListView是ListView控件  
// adapter是ListView绑定的Adapter，如果不方便直接使用，也可以通过ListView的getAdapter()方法获取到，前提是你已经绑定了适配器哦  
// 里面的参数就很熟悉了吧，其实这个方法的主要作用是选中listview的指定列，选中了，自然就得让这个item可见，自然就滚动咯  
msgListView.setSelection(adapter.getCount()-1);  
//还要必须设置selection为true  
msgListView.selection(true);  
还可以在ListView标签中加入如下两个属性，动态添加元素后，列表会自动滚动到底部：  
android:stackFromBottom="true"  
android:transcriptMode="alwaysScroll"  
```

59,限制EditText只能输入数字
```java
小数请使用android:numeric="decimal" 属性  
然后gettext后进行类型转换  
其实还有很多办法解决。  
可以添加TextChangedListener 监听器 进行字符判断。  
android:digits 属性 输入规则  
例如：android:digits=“0123456789” 表示只能输入数字。  
android:digits=“0123456789.” 表示可以输入数字和小数点  
```

60.EditText 的inputType详解

在开发的过程中，通常会用到EditText，如何让虚拟键盘来适应输入框中内容的类型，通常我们都会在xml文件中加入
```xml
android:inputType=""
android:inputType="none"
android:inputType="text"
android:inputType="textCapCharacters"
android:inputType="textCapWords"//单词首字母大小  
android:inputType="textCapSentences"//仅第一个字母大小  
android:inputType="textAutoCorrect"android:inputType="textAutoComplete"//前两个自动完成  
android:inputType="textMultiLine"//多行输入  
android:inputType="textImeMultiLine"//输入法多行（不一定支持）  
android:inputType="textNoSuggestions"//不提示  
android:inputType="textUri"//URI格式  
android:inputType="textEmailAddress"//电子邮件地址格式  
android:inputType="textEmailSubject"//邮件主题格式  
android:inputType="textShortMessage"//短消息格式  
android:inputType="textLongMessage"android:inputType="textPersonName"//人名格式  
android:inputType="textPostalAddress"//邮政格式  
android:inputType="textPassword"//密码格式  
android:inputType="textVisiblePassword"//密码可见格式  
android:inputType="textWebEditText"//作为网页表单的文本格式  
android:inputType="textFilter"//文本筛选格式  
android:inputType="textPhonetic"//拼音输入格式  
android:inputType="number"//数字格式  
android:inputType="numberSigned"//有符号数字格式  
android:inputType="numberDecimal"//可以带小数点的浮点格式  
android:inputType="phone"//拨号键盘  
android:inputType="datetime"android:inputType="date"//日期键盘  
android:inputType="time"//时间键盘
```


61.得到当前应用的版本号,版本名字
```
private int getVersionCode() throws Exception {  
        // 获取packagemanager的实例  
        PackageManager packageManager = getPackageManager();  
        // getPackageName()是你当前类的包名，0代表是获取版本信息  
        PackageInfo packInfo = packageManager.getPackageInfo(getPackageName(),  
                0);  
        return packInfo.versionCode;  
    }  
```

62.获取手机内存大小
```java
 /**
     * 获取系统总内存
     *
     * @param context 可传入应用程序上下文。
     * @return 总内存大单位为M。
     */
    public static long getTotalMemorySize(Context context) {
        String dir = "/proc/meminfo";
        try {
            FileReader fr = new FileReader(dir);
            BufferedReader br = new BufferedReader(fr, 2048);
            String memoryLine = br.readLine();
            String subMemoryLine = memoryLine.substring(memoryLine.indexOf("MemTotal:"));
            br.close();
            return Long.parseLong(subMemoryLine.replaceAll("\\D+", "")) / 1024l;
        } catch (IOException e) {
            e.printStackTrace();
        }
        return 0;
    }
```


63.Activity,Context,Application

如果我们在Activity A中或者其他地方使用Foo.getInstance()时，我们总是会顺手写一个『this』或者『mContext』（这个变量也是指向this）。

试想一下，当前我们所用的Foo是单例，意味着被初始化后会一直存在与内存中，以方便我们以后调用的时候不会在此次创建Foo对象。

但Foo中的 『mContext』变量一直都会持有Activity A中的『Context』，导致Activity A即使执行了onDestroy方法，也不能够将自己销毁。

但『applicationContext』就不同了，它一直伴随着我们应用存在（中途也可能 会被销毁，但也会自动reCreate），所以就不用担心Foo中的『mContext』会持有某Activity的引用，让其无法销毁。

看使用的周期是否在activity周期内，如果超出，必须用application；常见的情景包括：AsyncTask，Thread，第三方库初始化等等。

还有些情景，只能用activity：比如，对话框，各种View，需要startActivity的等。

Activity.this 返回当前的Activity实例，如果是UI控件需要使用Activity作为Context对象，但是默认的Toast实际上使用ApplicationContext也可以。

![Image](/_063.jpg)


大家注意看到有一些NO上添加了一些数字，其实这些从能力上来说是YES，但是为什么说是NO呢？下面一个一个解释：

数字1：启动Activity在这些类中是可以的，但是需要创建一个新的task。一般情况不推荐。

数字2：在这些类中去layout inflate是合法的，但是会使用系统默认的主题样式，如果你自定义了某些样式可能不会被使用。

数字3：在receiver为null时允许，在4.2或以上的版本中，用于获取黏性广播的当前值。（可以无视）

注：ContentProvider、BroadcastReceiver之所以在上述表格中，是因为在其内部方法中都有一个context用于使用。

好了，这里我们看下表格，重点看Activity和Application，可以看到，和UI相关的方法基本都不建议或者不可使用Application，并且，前三个操作基本不可能在Application中出现。

实际上，只要把握住一点，凡是跟UI相关的，都应该使用 Activity做为Context来处理；

其他的一些操作，Service,Activity,Application等实例都可以，当然了，注意 Context引用的持有，防止内存泄漏。

64.回到桌面Home
```java
    private void goHome() {  
        Intent i = new Intent(Intent.ACTION_MAIN);  
        i.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);  
        i.addCategory(Intent.CATEGORY_HOME);  
        startActivity(i);  
    }  
```

65.验证手机号码
```java
public static boolean phoneNumberIfRight(String phoneNumber) {  
        if (phoneNumber != null) {  
            if (phoneNumber.length() == 11) {  
                for (int i = 0; i < phoneNumber.length(); i++) {  
                    char c = phoneNumber.charAt(i);  
                    if (!(c >= '0' && c <= '9')) {  
                        return false;  
                    }  
                }  
                return true;  
            }  
        }  
        return false;  
    }  
```

66.WebView Settins常用方法
```java
setJavaScriptEnabled(true) ;//支持js脚本  
setPluginsEnabled(true) ;//支持插件  
setUserWideViewPort(false) ;//将图片调整到适合webview的大小  
setSupportZoom(true) ;//支持缩放  
setLayoutAlgorithm(LayoutAlgrithm.SINGLE_COLUMN) ;//支持内容从新布局  
supportMultipleWindows() ;//多窗口  
setCacheMode(WebSettings.LOAD_CACHE_ELSE_NETWORK) ;//关闭webview中缓存  
setAllowFileAccess(true) ;//设置可以访问文件  
setNeedInitialFocus(true) ;//当webview调用requestFocus时为webview设置节点  
setjavaScriptCanOpenWindowsAutomatically(true) ;//支持通过JS打开新窗口  
setLoadsImagesAutomatically(true) ;//支持自动加载图片  
setBuiltInZoomControls(true);  
//支持缩放  
webView.setInitialScale(35);  
//设置缩放比例  
webView.setScrollBarStyle(View.SCROLLBARS_OUTSIDE_OVERLAY);  
//设置滚动条隐藏   
webView.getSettings().setGeolocationEnabled(true);  
//启用地理定位  
webView.getSettings().setRenderPriority(RenderPriority.HIGH);  
//设置渲染优先级  
String dir = "/sdcard/temp";//设置定位的数据库路径   
webView.getSettings().setGeolocationDatabasePath(dir);  
```


67.小数点精确到后两位
```java
private static String formatPrice(float price) {
        String priceStr = price + "";
        if (priceStr.length() > 0) {
            int index = priceStr.indexOf(".");
            if (index == -1) {//没有小数点
                priceStr += ".00";
            } else {//有小数点
                if (priceStr.length() > index + 2 + 1) {//小数点大于两位(再加1因为index从0开始算)
                    priceStr = priceStr.substring(0, index + 2 + 1);
                } else if (priceStr.length() < index + 2 + 1) {//小数点小于两位
                    for (int i = 0; i < index + 2 + 1 - priceStr.length(); i++) {
                        priceStr += "0";
                    }
                }
            }
        }
        return priceStr;
    }
```

68.获取应用签名(MD5)
```java
/**
     * 获取应用签名信息
     *
     * @param paramContext Context
     * @param paramString  packget name
     * @return
     */
    private String getRawSignature(Context paramContext, String paramString) {
        if ((paramString == null) || (paramString.length() == 0)) {
            return null;
        }
        PackageManager localPackageManager = paramContext.getPackageManager();
        PackageInfo localPackageInfo;
        try {
            localPackageInfo = localPackageManager.getPackageInfo(paramString, 64);
            if (localPackageInfo == null) {
                return null;
            }
        } catch (PackageManager.NameNotFoundException localNameNotFoundException) {
            return null;
        }
        Signature[] arrayOfSignature = localPackageInfo.signatures;
        if (arrayOfSignature == null || arrayOfSignature.length == 0) return null;
        String contentStr = "";
        int i = arrayOfSignature.length;
        for (int j = 0; j < i; j++)
            contentStr += MD5.getMessageDigest(arrayOfSignature[j].toByteArray());
        return contentStr;
    }
    ```

其中MD5方法

```java
public static String getMessageDigest(byte[] paramArrayOfByte) {
        char[] arrayOfChar1 = {48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 97, 98, 99, 100, 101, 102};
        try {
            MessageDigest localMessageDigest = MessageDigest.getInstance("MD5");
            localMessageDigest.update(paramArrayOfByte);
            byte[] arrayOfByte = localMessageDigest.digest();
            int i = arrayOfByte.length;
            char[] arrayOfChar2 = new char[i * 2];
            int j = 0;
            int k = 0;
            while (true) {
                if (j >= i) return new String(arrayOfChar2);
                int m = arrayOfByte[j];
                int n = k + 1;
                arrayOfChar2[k] = arrayOfChar1[(0xF & m >>> 4)];
                k = n + 1;
                arrayOfChar2[n] = arrayOfChar1[(m & 0xF)];
                j++;
            }
        } catch (Exception localException) {
        }
        return null;
    }
    ```

69.设置屏幕长亮
```java
///常亮  
view.setKeepScreenOn(true)  
  getWindow().addFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:keepScreenOn="true">
    ...
</RelativeLayout>
getWindow().clearFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON)//清除屏幕长亮标志
CPU长期工作
<uses-permission android:name="android.permission.WAKE_LOCK" />
PowerManager powerManager = (PowerManager) getSystemService(POWER_SERVICE);
Wakelock wakeLock = powerManager.newWakeLock(PowerManager.PARTIAL_WAKE_LOCK,
        "MyWakelockTag");
wakeLock.acquire();
To release the wake lock, call wakelock.release().
为了保证后台任务能够顺利的进行.还必须请求CPU长期的工作
<receiver android:name=".MyWakefulReceiver"></receiver>
public class MyWakefulReceiver extends WakefulBroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        // Start the service, keeping the device awake while the service is
        // launching. This is the Intent to deliver to the service.
        Intent service = new Intent(context, MyIntentService.class);
        startWakefulService(context, service);
    }
}
public class MyIntentService extends IntentService {
    public static final int NOTIFICATION_ID = 1;
    private NotificationManager mNotificationManager;
    NotificationCompat.Builder builder;
    public MyIntentService() {
        super("MyIntentService");
    }
    @Override
    protected void onHandleIntent(Intent intent) {
        Bundle extras = intent.getExtras();
        // Do the work that requires your app to keep the CPU running.
        // ...
        // Release the wake lock provided by the WakefulBroadcastReceiver.
        MyWakefulReceiver.completeWakefulIntent(intent);
    }
}
```


70.设置滚动条的样式
```xml
android:scrollbarTrackVertical="@drawable/aaa"  
android:scrollbarThumbVertical="@drawable/bbb"  
android:scrollbarTrackVertical设置滚动条短的style  
android:scrollbarThumbVertical设置滚动条长的style
```

aaa和bbb放图片和xml都可以，可以在xml里结合shap设置样式 

```xml
<style name="scroll">  
       <item name="android:scrollbarThumbVertical">@drawable/seek_bar_thumb</item>  
       <item name="android:scrollbarTrackVertical">@drawable/scroll</item>  
       <item name="android:scrollbarThumbHorizontal">@drawable/scrollbar_handle</item>  
       <item name="android:scrollbarTrackHorizontal">@drawable/scrollbar_track</item>  
       <item name="android:scrollbarFadeDuration">0</item>  
       <item name="android:scrollbarAlwaysDrawVerticalTrack">true</item>  
  
   </style>  
```

71.获得状态栏高度
  
闲暇写了个单本小说阅读的应用。中间碰到了需要获取状态栏高度的问题。  
  
就像android后期版本，无法直接退出一样。找了一些方法来获取状态栏高度，结果都是为0.  
  
还好，牛人是很多的，当时，找到一段代码，能够有效的获取状态栏的高度。特此记录，备忘，以及供大家参考。  

```java  
Class<?> c = null;  
Object obj = null;  
Field field = null;  
int x = 0, sbar = 0;  
try {  
    c = Class.forName("com.android.internal.R$dimen");  
    obj = c.newInstance();  
    field = c.getField("status_bar_height");  
    x = Integer.parseInt(field.get(obj).toString());  
    sbar = getResources().getDimensionPixelSize(x);  
} catch(Exception e1) {  
    loge("get status bar height fail");  
    e1.printStackTrace();  
}
```



72.AndroidMainFest.xml中输入法适配
```xml
android:screenOrientation="landscape"是限制此页面横屏显示，  
  
android:screenOrientation="portrait"是限制此页面数竖屏显示。

如果没有设置,则横竖屏都可以,这个时候的Activity会被重新执行,需要添加这一行代码阻止执行

AndroidManifest.xml中设置android:configChanges="orientation|screenSize“
键盘输入问题,当我们不需要输入法的时候,希望它可以自动隐藏

 android:windowSoftInputMode="stateHidden"

 android:windowSoftInputMode="stateHidden|adjustPan"可以把输入框推到上面
```


73.得到控件的绝对位置

控件的绝对位置必须在控件绘制完毕后获得,可以使用ViewTreeHolder来监听

然后时候方法mOptions2.getGlobalVisibleRect(rect);来获得控件在屏幕了的绝对位置


74,Android debug.keystore 密码
```java
打开keySotre密码:android
key alias:androiddebugkey
key password:android
```

75.EditText把光标定位到末尾
```java
mEditName.setSelection(mEditName.getEditableText().toString().length());// 将光标移至文字末尾  
```


76.代码设置TextView的drawabletoleft
```java
Drawable d = getResources().getDrawable(R.drawable.q_shaixuan2);// 找图片  
            d.setBounds(0, 0, d.getMinimumWidth(), d.getMinimumHeight());  
            pb_screening.setCompoundDrawables(d, null, null, null);  
```

77.取消正在播放的动画
```java
view.clearAnimation();
```


78.// 判断是否是应用界面
```java
public static boolean isApplicationFirst(final Context context){  
          
        ActivityManager am = (ActivityManager) context.getSystemService(Context.ACTIVITY_SERVICE);  
        List<RunningTaskInfo> tasks = am.getRunningTasks(1);  
        if (!tasks.isEmpty()) {  
            ComponentName topActivity = tasks.get(0).topActivity;  
            if (topActivity.getPackageName().equals(context.getPackageName())) {  
                return true;  
            }  
        }  
          
        return false;  
    }   
```

79.判断应用是否切换到了后台
```
/** 
     * 程序是否在前台运行 
     *  
     * @return 
     */  
    public boolean isAppOnForeground() {  
        // Returns a list of application processes that are running on the  
        // device  
  
        ActivityManager activityManager = (ActivityManager) getApplicationContext().getSystemService(Context.ACTIVITY_SERVICE);  
        String packageName = getApplicationContext().getPackageName();  
  
        List<RunningAppProcessInfo> appProcesses = activityManager.getRunningAppProcesses();  
        if (appProcesses == null)  
            return false;  
  
        for (RunningAppProcessInfo appProcess : appProcesses) {  
            // The name of the process that this object is associated with.  
            if (appProcess.processName.equals(packageName) && appProcess.importance == RunningAppProcessInfo.IMPORTANCE_FOREGROUND) {  
                return true;  
            }  
        }  
        return false;  
    }  
 ```

80.判断数据表是否存在(用于同一个数据库添加第二张表)
```java
public boolean tabIsExist(SQLiteDatabase database, String tabName) {
		boolean result = false;
		if (tabName == null) {
			return false;
		}
		Cursor cursor = null;
		try {
			String sql = "select count(*) as c from sqlite_master where type ='table' and name ='"
					+ tabName.trim() + "' ";
			cursor = database.rawQuery(sql, null);
			if (cursor.moveToNext()) {
				int count = cursor.getInt(0);
				if (count > 0) {
					result = true;
				}
			}
		} catch (Exception e) {
		}
		return result;
	}
```

81.最近应用

在AndroidManiFest.xml里面的 Activity的参数中加上一句：android:excludeFromRecents="true"

这样程序就不会在系统长按HOME键出现的最近打开的应用列表里面了，同时也就不会被关闭最近打开的应用这个可恶的系统功能给关闭了！

82.得到控件的的宽度或者高度
```java
 ViewTreeObserver observer = linearLayout.getViewTreeObserver();
        observer.addOnPreDrawListener(new OnPreDrawListener() {

            @Override
            public boolean onPreDraw() {
                if(linearLayout.height() > height){
                  height = linearLayout.height();
                }
                return true;
            }
        });
```

83.多次点击有多个Toast时
```java
package com.xmn.util.other;
import android.content.Context;
import android.widget.Toast;
/**
 * 要用的时候调用ToastHelper.showToast(context, msg, duration);
 *
 * 完美实现Toast快速切换
 *
 * @author li'si
 *
 * **/
public class ToastHelper {
	private static Toast mToast;
	public static void showToast(Context context, String msg, int duration) {
		if (mToast == null) {
			mToast = Toast.makeText(context, msg, duration);
		} else {
			mToast.setText(msg);
		}
		mToast.show();
	}
}
```

84.手机分辨率,密度

在一个Activity的onCreate方法中，编写以下代码：
```java
      DisplayMetrics metric = new DisplayMetrics();
      getWindowManager().getDefaultDisplay().getMetrics(metric);
      int width = metric.widthPixels;  // 宽度（PX）
      int height = metric.heightPixels;  // 高度（PX）
      float density = metric.density;  // 密度（0.75 / 1.0 / 1.5）
      int densityDpi = metric.densityDpi;  // 密度DPI（120 / 160 / 240）
```
   需要注意的是，在一个低密度的小屏手机上，仅靠上面的代码是不能获取正确的尺寸的。

   比如说，一部240x320像素的低密度手机，如果运行上述代码，获取到的屏幕尺寸是320x427。

   因此，研究之后发现，若没有设定多分辨率支持的话，

   Android系统会将240x320的低密度（120）尺寸转换为中等密度（160）对应的尺寸，

   这样的话就大大影响了程序的编码。

   所以，需要在工程的AndroidManifest.xml文件中，加入supports-screens节点,如下：
   ```xml
        <supports-screens
            android:smallScreens="true"
            android:normalScreens="true"
            android:largeScreens="true"
            android:resizeable="true"
            android:anyDensity="true" />
   ```
   这样当前的Android程序就支持了多种分辨率，那么就可以得到正确的物理尺寸了。

85.TextView字体大小

使用如下代码时，发现字号不会变大，反而会变小：
```java
size = (int) mText.getTextSize() + 1;
mText.setTextSize(size);
```
后来发现getTextSize返回值是以像素(px)为单位的，而setTextSize()是以sp为单位的，两者单位不一致才造成这样的结果。

这里可以用setTextSize()的另外一种形式，可以指定单位：
```java
setTextSize(int unit, int size)
TypedValue.COMPLEX_UNIT_PX : Pixels
TypedValue.COMPLEX_UNIT_SP : Scaled Pixels
TypedValue.COMPLEX_UNIT_DIP : Device Independent Pixels
```
下面这样就正常了：
```java
size = (int) mText.getTextSize() + 1;
mText.setTextSize(TypedValue.COMPLEX_UNIT_PX, size);
```

86.应用图标大小

应用程序图标 （Icon）应当是一个 Alpha 通道透明的32位 PNG 图片。

由于安卓设备众多，一个应用程序图标需要设计几种不同大小，如：

LDPI (Low Density Screen，120 DPI)，其图标大小为 36 x 36 px。

MDPI (Medium Density Screen, 160 DPI)，其图标大小为 48 x 48 px。

HDPI (High Density Screen, 240 DPI)，其图标大小为 72 x 72 px。

xhdpi (Extra-high density screen, 320 DPI)，其图标大小为 96 x 96 px。

建议在设计过程中，在四周空出几个像素点使得设计的图标与其他图标在视觉上一致，例如，

96 x 96 px 图标可以画图区域大小可以设为 88 x 88 px， 四周留出4个像素用于填充（无底色）。

72 x 72 px 图标可以画图区域大小可以设为 68 x 68 px， 四周留出2个像素用于填充（无底色）。

48 x 48 px 图标可以画图区域大小可以设为 46 x 46 px， 四周留出1个像素用于填充（无底色）。

36 x 36 px 图标可以画图区域大小可以设为 34 x 34 px， 四周留出1个像素用于填充（无底色）。


87.TextView下划线效果

如果是在资源文件里：
```xml
 <resources>
    <string name="hello"><u>phone:0123456</u></string>
    <string name="app_name">MyLink</string>
</resources>
```
如果是代码里：
```java
TextView textView = (TextView)findViewById(R.id.tv_test);
textView.setText(Html.fromHtml("<u>"+"0123456"+"</u>"));
```
代码也可以这样：
```java
tvTest.getPaint().setFlags(Paint. UNDERLINE_TEXT_FLAG ); //下划线
tvTest.getPaint().setAntiAlias(true);//抗锯齿
```


88.Activity恢复现场

注意,如果在onCreate()方法中得到Bunble值,需要判断它是否为空.因为第一次启动的时候onCreate()的Bunble为空.


89.检测Intent,查看当前手机是否有应用可以接受发送的Intent
```java
PackageManager packageManager = getPackageManager();
List<ResolveInfo> activities = packageManager.queryIntentActivities(intent, 0);
boolean isIntentSafe = activities.size() > 0;
```

90.显示分享列表(尽管用户已经选择了默认的列表)
```java
Intent intent = new Intent(Intent.ACTION_SEND);
...
// Always use string resources for UI text.
// This says something like "Share this photo with"
String title = getResources().getString(R.string.chooser_title);
// Create intent to show chooser
Intent chooser = Intent.createChooser(intent, title);
// Verify the intent will resolve to at least one activity
if (intent.resolveActivity(getPackageManager()) != null) {
    startActivity(chooser);
}
```


91.接受其他应用传过来的Intent设置
```xml
<activity android:name="ShareActivity">
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="text/plain"/>
        <data android:mimeType="image/*"/>
    </intent-filter>
</activity>
```

92.监听EdtiText输入
```
edtCorMolnum.addTextChangedListener(new TextWatcher() {
			@Override
			public void onTextChanged(CharSequence s, int start, int before,
					int count) {
			}
			@Override
			public void beforeTextChanged(CharSequence s, int start, int count,
					int after) {
			}
			@Override
			public void afterTextChanged(Editable s) {
				if (s.toString().length() == 11) {// 输入了11位数字
					if (phoneNumberIfRight(edtCorMolnum.getEditableText()
							.toString().trim()))
						phoneNumberIfRepeat(edtCorMolnum.getEditableText()
								.toString().trim());// 检查手机号码是否可用
					else
						LogUitls.print("手机号码不正确",
								phoneNumberIfRight(edtCorMolnum
										.getEditableText().toString().trim()));
				}
			}
		});
```

93.总是显示分享列表
```java
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.putExtra(Intent.EXTRA_TEXT, "This is my text to send.");
sendIntent.setType("text/plain");
startActivity(Intent.createChooser(sendIntent, getResources().getText(R.string.send_to)));
```

94.Intent分享多条数据
```java
ArrayList<Uri> imageUris = newArrayList<Uri>();
imageUris.add(imageUri1); // Add your image URIs here
imageUris.add(imageUri2);
Intent shareIntent = newIntent();
shareIntent.setAction(Intent.ACTION_SEND_MULTIPLE);
shareIntent.putParcelableArrayListExtra(Intent.EXTRA_STREAM, imageUris);
shareIntent.setType("image/*");
startActivity(Intent.createChooser(shareIntent, "Share images to.."));
```

95.得到数据库所有的表
```java
Cursor cursor = db.rawQuery("select name from sqlite_master where type='table' order by name", null);
  while(cursor.moveToNext()){
   //遍历出表名
   String name = cursor.getString(0);
   Log.i("System.out", name);
  }
```

96.监听音量键,媒体键盘,监听多媒体键
    * 注册广播
    ```xml
<receiver android:name=".RemoteControlReceiver">
    <intent-filter>
        <action android:name="android.intent.action.MEDIA_BUTTON" />
    </intent-filter>
</receiver>
```

    * 在广播中监听

    ```java
public class RemoteControlReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if (Intent.ACTION_MEDIA_BUTTON.equals(intent.getAction())) {
            KeyEvent event = (KeyEvent)intent.getParcelableExtra(Intent.EXTRA_KEY_EVENT);
            if (KeyEvent.KEYCODE_MEDIA_PLAY == event.getKeyCode()) {
                // Handle key press.
            }
        }
    }
}
//KeyEvent包括许多类型的按键,例如such as KEYCODE_MEDIA_PLAY_PAUSE and KEYCODE_MEDIA_NEXT.

监听音量键
AudioManager am = mContext.getSystemService(Context.AUDIO_SERVICE);
...
// Start listening for button presses
am.registerMediaButtonEventReceiver(RemoteControlReceiver);
...
// Stop listening for button presses
am.unregisterMediaButtonEventReceiver(RemoteControlReceiver);
注意取消注册广播最好是监听Audio Foucs,如果App失去了Audio Foucs,则就取消注册广播
```

97.得到声音焦点

    * 请求一段持久性的声音
```java
AudioManager am = mContext.getSystemService(Context.AUDIO_SERVICE);
...
// Request audio focus for playback
int result = am.requestAudioFocus(afChangeListener,
                                 // Use the music stream.
                                 AudioManager.STREAM_MUSIC,
                                 // Request permanent focus.
                                 AudioManager.AUDIOFOCUS_GAIN);//第二个参数表示请求一个持久性的Foucs

if (result == AudioManager.AUDIOFOCUS_REQUEST_GRANTED) {//如果请求成功,就注册声音监听广播
    am.registerMediaButtonEventReceiver(RemoteControlReceiver);
    // Start playback.
}
```
    * 请求一段短暂的声音
    ```java
// Request audio focus for playback
int result = am.requestAudioFocus(afChangeListener,
                             // Use the music stream.
                             AudioManager.STREAM_MUSIC,
                             // Request permanent focus.
                             AudioManager.AUDIOFOCUS_GAIN_TRANSIENT_MAY_DUCK);

if (result == AudioManager.AUDIOFOCUS_REQUEST_GRANTED) {
    // Start playback.
}
//如果音乐切换到后来,需要告诉系统,这个时候允许任何APP打断你的播放

// Abandon audio focus when playback complete
am.abandonAudioFocus(afChangeListener);
```

98.监听声音焦点的变化
```java
OnAudioFocusChangeListener afChangeListener = new OnAudioFocusChangeListener() {
    public void onAudioFocusChange(int focusChange) {
        if (focusChange == AUDIOFOCUS_LOSS_TRANSIENT
            // Pause playback
        } else if (focusChange == AudioManager.AUDIOFOCUS_GAIN) {
            // Resume playback
        } else if (focusChange == AudioManager.AUDIOFOCUS_LOSS) {
            am.unregisterMediaButtonEventReceiver(RemoteControlReceiver);
            am.abandonAudioFocus(afChangeListener);
            // Stop playback
        }else if(focusChange == AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK){
            // Lower the volume
        }
    }
};
```

99.监听耳机是否拔出,蓝牙,可穿戴设备是否断开连接
```java
private class NoisyAudioStreamReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if (AudioManager.ACTION_AUDIO_BECOMING_NOISY.equals(intent.getAction())) {
            // Pause the playback
        }
    }
}
private IntentFilter intentFilter = new IntentFilter(AudioManager.ACTION_AUDIO_BECOMING_NOISY);
private void startPlayback() {
    registerReceiver(myNoisyAudioStreamReceiver(), intentFilter);
}
private void stopPlayback() {
    unregisterReceiver(myNoisyAudioStreamReceiver);
}
```

100.拍照
```java
//检测相机是否可用hasSystemFeature(PackageManager.FEATURE_CAMERA).
```
```xml
<manifest ... >
    <uses-feature android:name="android.hardware.camera"
                  android:required="true" />
    ...
</manifest>
```
拍照
```java
String mCurrentPhotoPath;
private File createImageFile() throws IOException {
    // Create an image file name
    String timeStamp = new SimpleDateFormat("yyyyMMdd_HHmmss").format(new Date());
    String imageFileName = "JPEG_" + timeStamp + "_";
    File storageDir = Environment.getExternalStoragePublicDirectory(
            Environment.DIRECTORY_PICTURES);
    File image = File.createTempFile(
        imageFileName,  /* prefix */
        ".jpg",         /* suffix */
        storageDir      /* directory */
    );
    // Save a file: path for use with ACTION_VIEW intents
    mCurrentPhotoPath = "file:" + image.getAbsolutePath();
    return image;
}
static final int REQUEST_TAKE_PHOTO = 1;
private void dispatchTakePictureIntent() {
    Intent takePictureIntent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
    // Ensure that there's a camera activity to handle the intent
    if (takePictureIntent.resolveActivity(getPackageManager()) != null) {
        // Create the File where the photo should go
        File photoFile = null;
        try {
            photoFile = createImageFile();
        } catch (IOException ex) {
            // Error occurred while creating the File
            ...
        }
        // Continue only if the File was successfully created
        if (photoFile != null) {
            takePictureIntent.putExtra(MediaStore.EXTRA_OUTPUT,
                    Uri.fromFile(photoFile));
            startActivityForResult(takePictureIntent, REQUEST_TAKE_PHOTO);
        }
    }
}
```
刷新图片的Uri
```java
private void galleryAddPic() {
    Intent mediaScanIntent = new Intent(Intent.ACTION_MEDIA_SCANNER_SCAN_FILE);
    File f = new File(mCurrentPhotoPath);
    Uri contentUri = Uri.fromFile(f);
    mediaScanIntent.setData(contentUri);
    this.sendBroadcast(mediaScanIntent);
}
```

101.录像

    * 请求权限

```xml
<manifest ... >
    <uses-feature android:name="android.hardware.camera"
                  android:required="true" />
    ...
</manifest>
```
    * 检测相机是否可用
    ```java
 hasSystemFeature(PackageManager.FEATURE_CAMERA)
 ```

    * 启动相机
    ```java
static final int REQUEST_VIDEO_CAPTURE = 1;
private void dispatchTakeVideoIntent() {
    Intent takeVideoIntent = new Intent(MediaStore.ACTION_VIDEO_CAPTURE);
    if (takeVideoIntent.resolveActivity(getPackageManager()) != null) {
        startActivityForResult(takeVideoIntent, REQUEST_VIDEO_CAPTURE);
    }
}
```
    * 得到录像的Uri
    ```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == REQUEST_VIDEO_CAPTURE && resultCode == RESULT_OK) {
        Uri videoUri = intent.getData();
        mVideoView.setVideoURI(videoUri);
    }
}
```

102.操作相机
```java
private boolean safeCameraOpen(int id) {
    boolean qOpened = false;

    try {
        releaseCameraAndPreview();
        mCamera = Camera.open(id);
        qOpened = (mCamera != null);
    } catch (Exception e) {
        Log.e(getString(R.string.app_name), "failed to open Camera");
        e.printStackTrace();
    }
    return qOpened;
}
private void releaseCameraAndPreview() {
    mPreview.setCamera(null);
    if (mCamera != null) {
        mCamera.release();
        mCamera = null;
    }
}
class Preview extends ViewGroup implements SurfaceHolder.Callback {
    SurfaceView mSurfaceView;
    SurfaceHolder mHolder;
    Preview(Context context) {
        super(context);
        mSurfaceView = new SurfaceView(context);
        addView(mSurfaceView);
        // Install a SurfaceHolder.Callback so we get notified when the
        // underlying surface is created and destroyed.
        mHolder = mSurfaceView.getHolder();
        mHolder.addCallback(this);
        mHolder.setType(SurfaceHolder.SURFACE_TYPE_PUSH_BUFFERS);
    }
...
}
```

103.查看缓存是否需要更新
```java
long currentTime = System.currentTimeMillis());
HttpURLConnection conn = (HttpURLConnection) url.openConnection();
long expires = conn.getHeaderFieldDate("Expires", currentTime);
long lastModified = conn.getHeaderFieldDate("Last-Modified", currentTime);
setDataExpirationDate(expires);
if (lastModified < lastUpdateTime) {
  // Skip update
} else {
  // Parse update
}
```

104.android:scrollbarStyle属性
```java
android:scrollbarStyle可以定义滚动条的样式和位置，可选值有insideOverlay、insideInset、outsideOverlay、outsideInset四种。
其中inside和outside分别表示是否在view的padding区域内，overlay和inset表示覆盖在view上或是插在view后面，所以四种值分别表示：
insideOverlay：默认值，表示在padding区域内并且覆盖在view上
insideInset：表示在padding区域内并且插入在view后面
outsideOverlay：表示在padding区域外并且覆盖在view上，推荐这个
outsideInset：表示在padding区域外并且插入在view后面
```

105.刷新View
```java
public void setShowText(boolean showText) {
   mShowText = showText;
   invalidate();
   requestLayout();
}
```

106.淡化状态栏与系统导航栏
```java
findViewById(R.id.content).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (flag) {
                    flag = false;
                    getWindow().getDecorView().setSystemUiVisibility(View.SYSTEM_UI_FLAG_LOW_PROFILE);
                } else {
                    flag = true;
                    getWindow().getDecorView().setSystemUiVisibility(0);
                }
            }
        });
```

108.EditText
```java
 android:inputType 可设置输入类型
android:inputType=
        "textCapSentences|textAutoCorrect" 设置这个属性可自动提醒和完成
android:imeOptions 可设置输入框的确定按钮"actionSend" or "actionSearch"
EditText editText = (EditText) findViewById(R.id.search);
editText.setOnEditorActionListener(new OnEditorActionListener() {
    @Override
    public boolean onEditorAction(TextView v, int actionId, KeyEvent event) {
        boolean handled = false;
        if (actionId == EditorInfo.IME_ACTION_SEND) {
            sendMessage();
            handled = true;
        }
        return handled;
    }
});
```

109.显示输入法
```java
public void showSoftKeyboard(View view) {
    if (view.requestFocus()) {
        InputMethodManager imm = (InputMethodManager)
                getSystemService(Context.INPUT_METHOD_SERVICE);
        imm.showSoftInput(view, InputMethodManager.SHOW_IMPLICIT);
    }
}
```

120.闹钟例子

Wake up the device to fire the alarm in 30 minutes, and every 30 minutes after that:

// Hopefully your alarm will have a lower frequency than this!
```java
alarmMgr.setInexactRepeating(AlarmManager.ELAPSED_REALTIME_WAKEUP,
        AlarmManager.INTERVAL_HALF_HOUR,
        AlarmManager.INTERVAL_HALF_HOUR, alarmIntent);
Wake up the device to fire a one-time (non-repeating) alarm in one minute:

private AlarmManager alarmMgr;
private PendingIntent alarmIntent;
...
alarmMgr = (AlarmManager)context.getSystemService(Context.ALARM_SERVICE);
Intent intent = new Intent(context, AlarmReceiver.class);
alarmIntent = PendingIntent.getBroadcast(context, 0, intent, 0);

alarmMgr.set(AlarmManager.ELAPSED_REALTIME_WAKEUP,
        SystemClock.elapsedRealtime() +
        60 * 1000, alarmIntent);
RTC examples

Here are some examples of using RTC_WAKEUP.

Wake up the device to fire the alarm at approximately 2:00 p.m., and repeat once a day at the same time:

// Set the alarm to start at approximately 2:00 p.m.
Calendar calendar = Calendar.getInstance();
calendar.setTimeInMillis(System.currentTimeMillis());
calendar.set(Calendar.HOUR_OF_DAY, 14);

// With setInexactRepeating(), you have to use one of the AlarmManager interval
// constants--in this case, AlarmManager.INTERVAL_DAY.
alarmMgr.setInexactRepeating(AlarmManager.RTC_WAKEUP, calendar.getTimeInMillis(),
        AlarmManager.INTERVAL_DAY, alarmIntent);
Wake up the device to fire the alarm at precisely 8:30 a.m., and every 20 minutes thereafter:

private AlarmManager alarmMgr;
private PendingIntent alarmIntent;
...
alarmMgr = (AlarmManager)context.getSystemService(Context.ALARM_SERVICE);
Intent intent = new Intent(context, AlarmReceiver.class);
alarmIntent = PendingIntent.getBroadcast(context, 0, intent, 0);

// Set the alarm to start at 8:30 a.m.
Calendar calendar = Calendar.getInstance();
calendar.setTimeInMillis(System.currentTimeMillis());
calendar.set(Calendar.HOUR_OF_DAY, 8);
calendar.set(Calendar.MINUTE, 30);

// setRepeating() lets you specify a precise custom interval--in this case,
// 20 minutes.
alarmMgr.setRepeating(AlarmManager.RTC_WAKEUP, calendar.getTimeInMillis(),
        1000 * 60 * 20, alarmIntent);
开启启动闹钟
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
public class SampleBootReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if (intent.getAction().equals("android.intent.action.BOOT_COMPLETED")) {
            // Set the alarm here.
        }
    }
}
<receiver android:name=".SampleBootReceiver"
        android:enabled="false">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"></action>
    </intent-filter>
</receiver>
变成设置开机启动
ComponentName receiver = new ComponentName(context, SampleBootReceiver.class);
PackageManager pm = context.getPackageManager();
pm.setComponentEnabledSetting(receiver,
        PackageManager.COMPONENT_ENABLED_STATE_ENABLED,
        PackageManager.DONT_KILL_APP);
取消开机启动
ComponentName receiver = new ComponentName(context, SampleBootReceiver.class);
PackageManager pm = context.getPackageManager();
pm.setComponentEnabledSetting(receiver,
        PackageManager.COMPONENT_ENABLED_STATE_DISABLED,
        PackageManager.DONT_KILL_APP);
```


121.新建一个新的进程
```xml
<service android:name=".PlaybackService"
         android:process=":background" />
```

122.为App申请更大的内存

manifest的application标签下添加largeHeap=true的属性

利用Android Framework里面优化过的容器类，例如SparseArray, SparseBooleanArray, 与 LongSparseArray。

用来代替HashMap等


123.颜色值转换
开发中 将 十六进制 颜色代码 转换为  int   类型数值 方法  :
```java
 Color.parseColor("#00CCFF") 返回 int 数值 ;
```

124.JSON遍历所有的key
```java
Iterator a = listJsonObject.keys();//得到所有的key
								while (a.hasNext()) {
									LogUitls.print("siyehua-关注key", a.next()
											.toString());
								}
```

125.播放简单的声音,播放游戏声音
```java
private SoundPool soundPool;
if (soundPool == null)// 参数详解(允许同时播放的声音的最大数量,音频类型:默认AudioManager.STREAM_MUSIC,采样率:即播放质量,0为默认)
	soundPool = new SoundPool(20, AudioManager.STREAM_MUSIC, 0);
final int a = soundPool.load(MainActivity.this,R.raw.goalsound, 1);
soundPool.setOnLoadCompleteListener(new OnLoadCompleteListener() {
	@Override
	public void onLoadComplete(SoundPool soundPool,int sampleId, int status) {
		playSound(a, 0);// 参数详解(上下问对象,需要播放的音频的ID,优先级:当前没有用到,默认1)return:一个ID,这个id可以用于播放/停止对应的音频
	}
});
/**
	 * @方法名: playSound
	 * @功能描述: 播放声音
	 * @param sound
	 *            需要播放的声音源:ID,这个ID由load方法返回得到
	 * @param loop
	 *            重复次数
	 * @return void
	 * @throws
	 */
	public void playSound(int sound, int loop) {
		AudioManager mgr = (AudioManager) this
				.getSystemService(Context.AUDIO_SERVICE);
		float streamVolumeCurrent = mgr
				.getStreamVolume(AudioManager.STREAM_MUSIC);
		float streamVolumeMax = mgr
				.getStreamMaxVolume(AudioManager.STREAM_MUSIC);
		float volume = streamVolumeCurrent / streamVolumeMax;
		soundPool.play(sound, 1.0f, 1.0f, 1, loop, 1.0f);
		// 参数：1、Map中取值 2、左声道 3、右声道 4、优先级:默认为1 5、重播次数 6、播放速度
	}
```

126.把字符串复制到剪切板
```java
private void copyToClipBoard() {
		if (Build.VERSION.SDK_INT < 11)
			return;
		String deviceToken = mPushAgent.getRegistrationId();
		if (!TextUtils.isEmpty(deviceToken)) {
			ClipboardManager clipboard = (ClipboardManager) getSystemService(CLIPBOARD_SERVICE);
			clipboard.setText(deviceToken);
			toast("DeviceToken已经复制到剪贴板了");
		}
	}
```

127.圆角背景
```xml
<?xml version="1.0" encoding="UTF-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android" >
    <!-- 背景 -->
    <solid android:color="@color/v_50FFFFFF" />
    <!-- 边框 -->
    <stroke
        android:width="1dp"
        android:color="@color/v_00FFFFFF" />
    <!-- 圆角 -->
    <corners
        android:bottomLeftRadius="@dimen/_54px"
        android:bottomRightRadius="@dimen/_54px"
        android:topLeftRadius="@dimen/_54px"
        android:topRightRadius="@dimen/_54px" />
</shape>
```

128.查看当前Activity的栈情况

adb shell dumpsys activity


129.替换换行符
[\t\n\r]//注意需要选择正则规则选项

130.gif播放:
````
使用方法:http://my.oschina.net/u/1175746/blog/288258?p=1#comments
项目地址:android-gif-drawable
private GifDrawable drawable;
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
				WindowManager.LayoutParams.FLAG_FULLSCREEN);// 设置为全屏
		GifImageView gifImageView = new GifImageView(mContext);// 得到一个Gif View
		try {
			drawable = new GifDrawable(getResources(), R.drawable.start);// 设置需要播放的图片
			drawable.setLoopCount(1);// 设置播放次数
			gifImageView.setImageDrawable(drawable);// 把图片设置到Gif View中
			gifImageView.setScaleType(ScaleType.FIT_XY);// 设置缩放模式
			setContentView(gifImageView);// 设置View
		} catch (NotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
		findView();
		initilizeViewAndData();
		setOnListener();
	}
如果Activityfinish了,要记得回收
drawable.recycle();
```

131.禁止ViewPager销毁碎片
```java
	viewPager.setOffscreenPageLimit(10);//参数表示在当前的界面外最多允许有几个界面
```

132.自动生成Json解析方法
```java
private static String getParseMethod(Class<?> model, int classType,
			String lastObjectName, String lastJsonUitlName) {
		String className = (model.getName().contains("$") ? model.getName()
				.substring(model.getName().indexOf("$") + 1) : model.getName())
				+ " ";
		String tmpObjectName = " m" + className;// 变量名
		String reslut = "";// 结果集
		String tmpJsonUtil = " m" + className.trim() + "JsonUtil ";// Json变量
		String tmpJsonArray = " m" + className.trim() + "JsonArray ";// JsonArray变量
		if (classType == 1) {
			reslut = "public static " + className + " parseJson(JsonUtil "
					+ tmpJsonUtil + " )  throws JSONException {" + className
					+ tmpObjectName + " = new " + className + "();";
		} else if (classType == 2) {
			reslut = "\n\n JsonUtil " + tmpJsonUtil + " =" + "new JsonUtil ("
					+ lastJsonUitlName + ".getString(\""
					+ className.trim().toLowerCase().substring(0, 1)
					+ className.trim().substring(1) + "\").toString());"
					+ className + tmpObjectName + "= new "
					+ lastObjectName.replace(" m", "") + "().new " + className
					+ "();";
		} else if (classType == 3) {
			reslut = "\n\n  ArrayList<" + className + "> m" + className.trim()
					+ "List = new ArrayList<"
					+ lastObjectName.replace(" m", "") + "." + className
					+ ">(); JSONArray " + tmpJsonArray + " = new JSONArray("
					+ lastJsonUitlName.trim() + ".getString(\""
					+ className.trim().toLowerCase().substring(0, 1)
					+ className.trim().substring(1)
					+ "\")); for (int i = 0; i < " + tmpJsonArray
					+ ".length(); i++) { JsonUtil " + tmpJsonUtil + " ="
					+ "new JsonUtil (" + tmpJsonArray + ".get(i).toString());"
					+ className + tmpObjectName + "= new "
					+ lastObjectName.replace(" m", "") + "().new " + className
					+ "();";
		}
		Field[] field = model.getDeclaredFields(); // 获取实体类的所有属性，返回Field数组
		for (int j = 0; j < field.length; j++) { // 遍历所有属性
			String type = field[j].getGenericType().toString(); // 获取属性的类型
			// System.out.println(type + "   " + field[j].getName());
			if (type.equals("class java.lang.String")) { // 如果type是类类型，则前面包含"class "，后面跟类名
				reslut += tmpObjectName + "." + field[j].getName() + "="
						+ tmpJsonUtil + ".getString(\"" + field[j].getName()
						+ "\");"; // 获取属性的名字
			} else if (type.equals("class java.lang.Integer")
					|| type.equals("int")) {
				reslut += tmpObjectName + "." + field[j].getName() + "="
						+ tmpJsonUtil + ".getInt(\"" + field[j].getName()
						+ "\");"; // 获取属性的名字
			} else if (type.equals("class java.lang.Boolean")
					|| type.equals("boolean")) {
				reslut += tmpObjectName + "." + field[j].getName() + "="
						+ tmpJsonUtil + ".getBoolean(\"" + field[j].getName()
						+ "\");"; // 获取属性的名字
			} else if (type.equals("class java.lang.Float")
					|| type.equals("float")) {
				reslut += tmpObjectName + "." + field[j].getName() + "="
						+ tmpJsonUtil + ".getFloat(\"" + field[j].getName()
						+ "\");"; // 获取属性的名字
			} else if (type.equals("class java.lang.Double")
					|| type.equals("double")) {
				reslut += tmpObjectName + "." + field[j].getName() + "="
						+ tmpJsonUtil + ".getDouble(\"" + field[j].getName()
						+ "\");"; // 获取属性的名字
			} else if (type.equals("class " + className.trim() + "$"
					+ field[j].getName().toUpperCase().substring(0, 1)
					+ field[j].getName().substring(1))) {// 如果是一个类
				reslut += getParseMethod(field[j].getType(), 2, tmpObjectName,
						tmpJsonUtil);
			} else if (type.equals("java.util.ArrayList<" + className.trim()
					+ "$" + field[j].getName().toUpperCase().substring(0, 1)
					+ field[j].getName().substring(1) + ">")
					|| type.equals("java.util.List<" + className.trim() + "$"
							+ field[j].getName().toUpperCase().substring(0, 1)
							+ field[j].getName().substring(1) + ">")) {
				try {
					Class class1 = Class
							.forName(field[j]
									.getGenericType()
									.toString()
									.substring(
											field[j].getGenericType()
													.toString().indexOf("<") + 1)
									.replace(">", ""));
					reslut += getParseMethod(class1, 3, tmpObjectName,
							tmpJsonUtil);
				} catch (ClassNotFoundException e) {
					e.printStackTrace();
				}
			}
		}
		if (classType == 1) {
			reslut += "return " + tmpObjectName + ";}";
		} else if (classType == 2) {
			reslut += lastObjectName.trim() + "."
					+ className.trim().toLowerCase().substring(0, 1)
					+ className.trim().substring(1) + " = " + tmpObjectName
					+ ";\n";
		} else if (classType == 3) {
			reslut += "m" + className.trim() + "List.add(" + tmpObjectName
					+ ");}" + lastObjectName.trim() + "."
					+ className.trim().toLowerCase().substring(0, 1)
					+ className.trim().substring(1) + " = " + "m"
					+ className.trim() + "List" + ";\n";
		}
		return reslut;
	}
```

133:去除TextView的上下边距
```java
includeFontPadding="false"
```

134:解决ADT大量出现"Unexpected value from nativeGetEnabledTags: 0"的问题

需要过滤其他的字段同样可以这样处理

在logcat的过滤器的log message字段中输入以下过滤串。

^(?!.*(nativeGetEnabledTags)).*$


135:沉浸式

android4.4也就是api19~所以我们在res文件夹下新建一个values-v19,然后再新建一个style.xml文件。

在style上写以下代码：

指定style为noactionbar而且半透明
```xml
<resources xmlns:android="http://schemas.android.com/apk/res/android">
    <style name="AppBaseTheme" parent="android:Theme.Holo.Light.NoActionBar.TranslucentDecor" >
    </style>
</resources>
```

然后运行程序可以看到，状态栏与app顶部颜色是一致的，但是如果布局文件的顶部写有其它内容的话会发现布局文件上的内容会与状态栏上的内容重合~~这肯定是不允许的。
有没有方法解决呢？

在使用了沉浸式状态栏的布局文件上写上以下两句话：

```xmml
android:clipToPadding="true"
android:fitsSystemWindows="true"
```

136.ViewPager滑动事件被item吸收

item设置的内容为 center .并且设置了singleline = "true"

去掉其中一个属性即可


137.重启应用
```java
@SuppressWarnings("deprecation")
	private void restart() {
		Intent intent = new Intent(mContext.getApplicationContext(),
				TestActivity.class);
		PendingIntent restartIntent = PendingIntent.getActivity(
				mContext.getApplicationContext(), 0, intent,
				Intent.FLAG_ACTIVITY_NEW_TASK);
		AlarmManager mgr = (AlarmManager) mContext
				.getSystemService(Context.ALARM_SERVICE);
		mgr.set(AlarmManager.RTC, System.currentTimeMillis() + 1000,
				restartIntent); // 1秒钟后重启应用
		// 退出应用
		int currentVersion = android.os.Build.VERSION.SDK_INT;
		if (currentVersion > android.os.Build.VERSION_CODES.ECLAIR_MR1) {
			Intent startMain = new Intent(Intent.ACTION_MAIN);
			startMain.addCategory(Intent.CATEGORY_HOME);
			startMain.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
			mContext.startActivity(startMain);
			System.exit(0);
		} else {// android2.1
			ActivityManager am = (ActivityManager) mContext
					.getSystemService(Context.ACTIVITY_SERVICE);
			am.restartPackage(mContext.getPackageName());
		}
	}
```

138.重命名360打包文件
```java
public static void reName(String directoryPath, String startName) {
		File file = new File(directoryPath);
		if (file.isDirectory()) {
			File[] files = file.listFiles();
			for (int i = 0; i < files.length; i++) {
				System.out.println(files[i].getParentFile().getPath());
				files[i].renameTo(new File(
						files[i].getParentFile().getPath()
								+ "/"
								+ files[i]
										.getName()
										.replace("com.caiyu.qqsd.encrypted.",
												startName)
										.replace("_signed_Aligned", "")
										.replace("UMENG_CHANNEL.", "")
										.replace("source", "Web")));
			}
		}
	}
```

139.代码设置应用名/图标

首先在AndroidManifest.mxl中配置别名
```xml
 <activity-alias
            android:enabled="true"
            android:label="新的应用名"
            android:name=".MainActivity-Emblem"
            android:targetActivity=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity-alias>
```
接着在targetActivity中设置新的应用名和图标
```
 private void a(Activity abc) {
        PackageManager pm = getApplicationContext().getPackageManager();
        pm.setComponentEnabledSetting(abc.getComponentName(), PackageManager
                .COMPONENT_ENABLED_STATE_DISABLED, PackageManager.DONT_KILL_APP);//设置当前的应用图标不可用
        pm.setComponentEnabledSetting(new ComponentName(getBaseContext(), getPackageName() + "" +
                        ".MainActivity-Emblem"), PackageManager.COMPONENT_ENABLED_STATE_ENABLED,
                PackageManager.DONT_KILL_APP);//使用新的文件名和图标
    }
```

140.得到文件的md5

可根据文件的md5来判断是否是同一个文件,文件名改变,路径改变不影响其md5值.

hashcode仅仅和文件的路径有关,不能作为文件的唯一标准
```java
public static String getMd5ByFile(File file) throws FileNotFoundException {
        String value = null;
        FileInputStream in = new FileInputStream(file);
        try {
            MappedByteBuffer byteBuffer = in.getChannel().map(FileChannel.MapMode.READ_ONLY, 0,
                    file.length());
            MessageDigest md5 = MessageDigest.getInstance("MD5");
            md5.update(byteBuffer);
            BigInteger bi = new BigInteger(1, md5.digest());
            value = bi.toString(16);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (null != in) {
                try {
                    in.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
        return value;
    }
```

141.获得和设置系统音量,设置音量
```java
 AudioManager mAudioManager = (AudioManager) getSystemService(Context.AUDIO_SERVICE);
        //////////////获得音量//////////////////////
        //通话音量
        int max = mAudioManager.getStreamMaxVolume(AudioManager.STREAM_VOICE_CALL);
        int current = mAudioManager.getStreamVolume(AudioManager.STREAM_VOICE_CALL);
        Log.d("VIOCE_CALL", "max: " + max + " current : " + current);

        //系统音量
        max = mAudioManager.getStreamMaxVolume(AudioManager.STREAM_SYSTEM);
        current = mAudioManager.getStreamVolume(AudioManager.STREAM_SYSTEM);
        Log.d("SYSTEM", "max : " + max + " current : " + current);
        //铃声音量
        max = mAudioManager.getStreamMaxVolume(AudioManager.STREAM_RING);
        current = mAudioManager.getStreamVolume(AudioManager.STREAM_RING);
        Log.d("RING", "max : " + max + " current : " + current);
        //音乐音量
        max = mAudioManager.getStreamMaxVolume(AudioManager.STREAM_MUSIC);
        current = mAudioManager.getStreamVolume(AudioManager.STREAM_MUSIC);
        Log.d("MUSIC", "max : " + max + " current : " + current);
        //提示声音音量
        max = mAudioManager.getStreamMaxVolume(AudioManager.STREAM_ALARM);
        current = mAudioManager.getStreamVolume(AudioManager.STREAM_ALARM);
        Log.d("ALARM", "max : " + max + " current : " + current);
        //////////////设置音量//////////////////////
        //        mAudioManager.setStreamVolume(AudioManager.STREAM_MUSIC, 音量大小, 0);
```

148. 渐变Progress
```xml
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">

<item android:id="@android:id/background">
    <shape>
        <corners android:radius="5dip" />
        <gradient
                android:startColor="#ff9d9e9d"
                android:centerColor="#ff5a5d5a"
                android:centerY="0.75"
                android:endColor="#ff747674"
                android:angle="0"
        />
    </shape>
</item>

<item android:id="@android:id/secondaryProgress">
    <clip>
        <shape>
            <corners android:radius="5dip" />
            <gradient
                    android:startColor="#80ffd300"
                    android:centerColor="#80ffb600"
                    android:centerY="0.75"
                    android:endColor="#a0ffcb00"
                    android:angle="0"
            />
        </shape>
    </clip>
</item>
<item android:id="@android:id/progress">
    <clip>
        <shape>
            <corners
                android:radius="5dip" />
            <gradient
                android:startColor="#80ff0000"
                android:endColor="#8000ff00"
                android:angle="0" />
        </shape>
    </clip>
</item>

</layer-list>

```
```xml
<ProgressBar
    android:id="@+id/progressBar1"
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    style="?android:attr/progressBarStyleHorizontal"
    android:max="100"
    android:progress="80"
    android:secondaryProgress="90"
    android:progressDrawable="@drawable/progress_bar"
    />
```


149.获取键盘高度

键盘的高度不可以直接获取,可以通过监听键盘弹出的变化.获取当前窗体的高度变化来计算出键盘的高度
```java
    Rect r = new Rect();
                    View rootview = MainActivity.this.getWindow().getDecorView(); // this = activity
                    rootview.getWindowVisibleDisplayFrame(r);
```

150.Activity Dialog有白色背景,白色边框,设置为透明背景,圆角
```xml
<style name="activity_dialog" parent="@android:style/Theme.Dialog">

        <!-- 窗口边框 -->
        <item name="android:windowFrame">@null</item>
        <!-- 窗口是否浮动在Activity上 -->
        <item name="android:windowIsFloating">true</item>
        <!-- 半透明 -->
        <item name="android:windowIsTranslucent">false</item>
        <!-- 没有标题栏 -->
        <item name="android:windowNoTitle">true</item>
        <!-- 背景 -->
        <!--<item name="android:background">@android:color/white</item>-->
        <item name="android:windowBackground">@color/_00000000</item>

        <!-- 背景模糊 -->
        <item name="android:backgroundDimEnabled">true</item>

        <!--禁止点击屏幕之外关闭Dialog-->
        <item name="android:windowCloseOnTouchOutside">false</item>
    </style>
```
```java
假设Activity的布局设置了背景,不管是什么颜色,包括透明,成为Dialog后都会自动添加一个白色的背景,
导致无法有白色的边框,或b无法显示圆角问题
需要用代码重新把Dialog的背景重新设置为透明
 getWindow().setBackgroundDrawable(new ColorDrawable(android.graphics.Color.TRANSPARENT));
```


151.监听主线程是否完成了绘制
```java
Looper.myQueue().addIdleHandler(idleHandler = new MessageQueue.IdleHandler() {
            @Override
            public boolean queueIdle() {
                Log.e("siyehua", "onCreate -> idle : " + (SystemClock.uptimeMillis() - time));
                handler.sendEmptyMessageDelayed(a++, 1500);
                return false;
            }
        });
```


152.Retofit添加统一head
```java
HttpLoggingInterceptor httpLoggingInterceptor = new HttpLoggingInterceptor(new HttpLoggingInterceptor.Logger() {
	 @Override
 	public void log(String message) {
 		Log.i("RestLogging", message);
 	}
});
httpLoggingInterceptor.setLevel(HttpLoggingInterceptor.Level.BODY);
OkHttpClient client = new OkHttpClient.Builder()
 .addInterceptor(httpLoggingInterceptor)
 .addNetworkInterceptor(commonParamsInterceptor)
 .retryOnConnectionFailure(true)
 .connectTimeout(15, TimeUnit.SECONDS)
 .build();
return client;
```
