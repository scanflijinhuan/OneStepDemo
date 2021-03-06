# OneStepDemo
这是一个适配Smartisan OS一步Demo，实现文字、链接、单图、多图拖拽功能，打破应用边界，操作更便捷。

This is a one-step demo for Smartisan OS. It implements text, link, single-picture, multi-picture drag and drop functions, breaks application boundaries and makes operation more convenient.



### 软件截图

| ![首页](./pics/1.png) | ![文字拖拽](./pics/2.png) | ![多图拖拽](./pics/3.png) | ![链接拖拽](./pics/4.png) |
| ---------------------- | -------------------------- | -------------------------- | -------------------------- |
|                        |                            |                            |                            |

## Demo视频演示

[优酷视频播放地址](http://v.youku.com/v_show/id_XMzgyMzQyMTM0OA==.html?spm=a2h3j.8428770.3416059.1)

<video id="video" controls="" preload="none">
  <source id="mp4  src="http://player.youku.com/player.php/sid/XMzgyMzQyMTM0OA==/v.swf">
</video>

<embed src='http://player.youku.com/player.php/sid/XMzgyMzQyMTM0OA==/v.swf'
allowFullScreen='true' quality='high' width='480' height='400' align='middle' allowScriptAccess='always' type='application/x-shockwave-flash'>
</embed>

### 使用教程

##### 1、初始化OneStepHelper

将[smartisanos-api-1.0.2.jar](https://github.com/codeccc/OneStepDemo/blob/master/app/libs/smartisanos-api-1.0.2.jar) 添加到你的项目 `/libs` 目录下,添加依赖并同步

##### 2、初始化OneStepHelper

```java
OneStepHelper mOneStepHelper = OneStepHelper.getInstance(OnestepDragActivity.this);
```

##### 3、设置view长按事件,在onLongClick中设置拖拽

```java
 views[i].setOnLongClickListener(this);
```

```java
@Override
public boolean onLongClick(View view){
    switch (view.getId()){
       case R.id.txt_link_style:
       //链接类型
       if (mOneStepHelper.isOneStepShowing()){
           mOneStepHelper.dragLink(view, mBinding.txtLinkStyle.getText().toString().trim());
       }
       break;
}
```



#### **基础API:**

##### 1、文字类型

```java
mOneStepHelper.dragText(View view, CharSequence text)
```

##### 2、链接类型

```java
mOneStepHelper.dragLink(View view, CharSequence link)
```

##### 3、单图类型

```java
mOneStepHelper.dragImage(View view, File file, String mimeType)
```

##### 4、多图类型

```java
mOneStepHelper.dragMultipleImages(View view, File[] files, String[] mimeTypes)
```

##### 5、文件类型

```java
mOneStepHelper.dragFile(View view, File file, String mimeType, String displayname)
```



#### 高级自定义API:

##### 1、文字类型自定义拖拽缩略图

```java
mOneStepHelper.dragText(View view, CharSequence text, Bitmap background, Bitmap content, Bitmap avatar)
```

##### 2、文件类型自定义拖拽缩略图

```java
mOneStepHelper.dragFile(View view, File file, String mimeType, Bitmap background, Bitmap content, Bitmap avatar)
```

##### 3、单图类型自定义拖拽缩略图

```java
mOneStepHelper.dragImage(View view, Bitmap content, File file, String mimeType)
```

##### 4、自定义气泡显示位置

```java
mOneStepHelper.showDragPopupText(View view, OnDragListener dragListener, String content, int x, int y)
```



#### 注意事项:

##### 1、进行图片拖拽、文件拖拽时,请在`AndroidManifest.xml`申请权限

```java
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

##### 2、进行图片拖拽分享时,请先将图片保存到本地 , 测试保存代码示例:

```java
/**
 * 保存目录
 */
private static final String SAMPLE_FILE_DIR
        = Environment.getExternalStorageDirectory() + "/OneStepDemo/";
/**
 * 创建文件
 * @param filename 文件名称
 * @return
 */
private File createTestFileIfNotExists(String filename)
{
    File testFile = new File(SAMPLE_FILE_DIR, filename);
    if (!testFile.exists())
    {
        try
        {
            testFile.createNewFile();
        } catch (IOException e)
        {
            e.printStackTrace();
        }
    }
    return testFile;
}
```

```java
/**
 * 将图片从assets中拷贝到sd卡中
 * @param assetFile 文件
 * @return
 */
private void copyAssetFile2Sdcard(String assetFile)
{
    InputStream inputStream = null;
    OutputStream outputStream = null;
    try
    {
        inputStream = getAssets().open(assetFile);
        String destFilePath = createTestFileIfNotExists(assetFile).getAbsolutePath();
        File f = new File(destFilePath);
        outputStream = new FileOutputStream(f);
        byte[] buf = new byte[1024 * 4];
        int len = 0;
        while ((len = inputStream.read(buf)) > 0)
        {
            outputStream.write(buf, 0, len);
        }
        outputStream.flush();
    } catch (IOException e)
    {
        e.printStackTrace();
    } finally
    {
        try
        {
            if (outputStream != null)
            {
                outputStream.close();
            }
            if (inputStream != null)
            {
                inputStream.close();
            }
        } catch (IOException e)
        {
            e.printStackTrace();
        }
    }
}
```



#### TODO

- [ ] 接收拖拽的图片、文字、链接、文件;





**官方GITHUB主页:**   [https://github.com/SmartisanTech/SmartisanOS-SDK](https://github.com/SmartisanTech/SmartisanOS-SDK)


### MIT License

```
MIT License

Copyright (c) 2018 codewang

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
