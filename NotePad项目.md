## NotePad项目

### 一. 实验目的

​	软件项目实践

### 二. 实验环境

​	装有Android Studio的电脑

### 三. 实验内容及要求

	1. 导入NotePad项目到Android Studio中并运行
 	2. 在NotePad列表中添加时间戳

### 四. 实验记录

##### （1）导入实验项目

​		1.下载项目压缩包，并打开

​		2.打开AS并导入项目

​		3.更改两个文件中的参数

![image-20210520131731736](C:\Users\Hp\AppData\Roaming\Typora\typora-user-images\image-20210520131731736.png)

​		4.点击运行，并根据提示下载环境，成功显示

##### （2）添加时间戳

​		1.在noteslist_item.xml添加一个用于显示时间戳的TextView

```java
	<TextView
        android:id="@+id/text1_date"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:textSize="17dp"
        android:paddingLeft="5dip"
    />

```

​		2.接着在它的java文件NoteList.java中关于显示Note的函数里加上时间的显示

```java
	private static final String[] PROJECTION = new String[] {
            NotePad.Notes._ID, // 0
            NotePad.Notes.COLUMN_NAME_TITLE, // 1
            NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE //日期
    };
    private static final int COLUMN_INDEX_TITLE = 1;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setDefaultKeyMode(DEFAULT_KEYS_SHORTCUT);
        Intent intent = getIntent();
        if (intent.getData() == null) {
            intent.setData(NotePad.Notes.CONTENT_URI);
        }
        getListView().setOnCreateContextMenuListener(this);
        Cursor cursor = managedQuery(
            getIntent().getData(),            // Use the default content URI for the provider.
            PROJECTION,                       // Return the note ID and title for each note.
            null,                             // No where clause, return all records.
            null,                             // No where clause, therefore no where column values.
            NotePad.Notes.DEFAULT_SORT_ORDER  // Use the default sort order.
        );
        String[] dataColumns = {
                NotePad.Notes.COLUMN_NAME_TITLE,
                NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE
        } ;
        int[] viewIDs = {
                android.R.id.text1,
                R.id.text1_date
        };
        SimpleCursorAdapter adapter
            = new SimpleCursorAdapter(
                      this,                             // The Context for the ListView
                      R.layout.noteslist_item,          // Points to the XML for a list item
                      cursor,                           // The cursor to get items from
                      dataColumns,
                      viewIDs
              );
        setListAdapter(adapter);
    }

```

​		3.NoteEditor.java里也添加获取时间的功能

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200531010115926.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pvZTMzNzM0Nzg4OQ==,size_16,color_FFFFFF,t_70)

​		

##### （3） 效果截图

![image-20210520133806731](C:\Users\Hp\AppData\Roaming\Typora\typora-user-images\image-20210520133806731.png)



