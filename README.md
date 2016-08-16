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


