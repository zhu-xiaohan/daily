 #2016-10-24
 =============================
 
1. 应完成工作
    * 
2. 未完成工作
    * MainAcitivity
         * package com.example.sqlitedemo;           
           import android.content.Context;
           import android.content.Intent;
           import android.database.Cursor;
           import android.database.sqlite.SQLiteDatabase;
           import android.os.Bundle;
           import android.support.annotation.Nullable;
           import android.support.v7.app.AppCompatActivity;
           import android.view.LayoutInflater;
           import android.view.View;
           import android.view.ViewGroup;
           import android.widget.AdapterView;
           import android.widget.ListView;
           import android.widget.TextView;
           import android.widget.Toast;
           
           import java.util.ArrayList;
           import java.util.List;
           
           /**
            * Created by Administrator on 2016/10/25.
            */
           
           public class MainAcitivity extends AppCompatActivity {
           
               private ListView listClass;
           
               private List<ClassInfo> listData = null;
           
               private ViewAdapter va = new ViewAdapter<ClassInfo>(){
           
                   @Override
                   public View getView(int position, View convertView, ViewGroup parent){
           
                       LayoutInflater lif = (LayoutInflater) getSystemService(Context.LAYOUT_INFLATER_SERVICE);
           
                       View view = lif.inflate(R.layout.class_item_layout,null);
                       TextView tvName = (TextView) view.findViewById(R.id.tv_class_name);
                       tvName.setText(getItem(position).getName());
                       return view;
                   }
               };
           
               private  AdapterView.OnItemClickListener ocl = new AdapterView.OnItemClickListener(){
           
                   public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                       Toast.makeText(MainAcitivity.this,"你点击的分类的idx是" + listData.get(position).getIdx(),Toast.LENGTH_LONG).show();
           
                       Long sex = listData.get(position).getIdx();
           
                       Intent intent = new Intent();
                       intent.putExtra("sex",sex);
           
                       intent.setClass(MainAcitivity.this,DetailActivity.class);
                       seartActivity(intent);
                   }
               };
           
               private void seartActivity(Intent intent) {
               }
           
               @Override
               protected void onCreate(@Nullable Bundle savedInstanceState) {
                   super.onCreate(savedInstanceState);
                   setContentView(R.layout.acitivity_main);
           
                   //获取对象
                   listClass = (ListView) findViewById(R.id.list_class);
           
                   //获取显示数据？？？
                   listData = getdata();
           
                   //绑定适配器
                   va.setListDate(listData);
           
                   listClass.setAdapter(va);
           
                   //设置监听
                   listClass.setOnItemClickListener(ocl);
               }
           
               private List<ClassInfo>getdata(){
           
                   SQLiteDabseHandle handle = new SQLiteDabseHandle(this);
                   SQLiteDatabase database = handle.getSQLits();
           
                   StringBuilder sbSql = new StringBuilder();
                   sbSql.append("  select  ");
                   sbSql.append(" idx,name ");
                   sbSql.append("  from    ");
                   sbSql.append("  classlist ");
           
                   Cursor cursor = database.rawQuery(sbSql.toString(),null);
           
                   List<ClassInfo>result = new ArrayList<ClassInfo>();
                   while(cursor.moveToNext()){
                       Long idx = cursor.getLong(0);
                       String name = cursor.getString(1);
           
                       ClassInfo classInfo = new ClassInfo(idx,name);
                       result.add(classInfo);
                   }
           
                   return result;
               }
           }
           
    * DetailActivity
         * package com.example.sqlitedemo;           
           import android.content.Context;
           import android.database.Cursor;
           import android.database.sqlite.SQLiteDatabase;
           import android.os.Bundle;
           import android.support.annotation.Nullable;
           import android.support.v7.app.AppCompatActivity;
           import android.view.LayoutInflater;
           import android.view.View;
           import android.view.ViewGroup;
           import android.widget.ListView;
           import android.widget.TextView;
           
           import java.util.ArrayList;
           import java.util.List;
           
           /**
            * Created by Administrator on 2016/10/25.
            */
           
           public class DetailActivity extends AppCompatActivity {
           
               private ListView listClass;
           
               private List<TableInfo>listData = null;
               private ViewAdapter va = new ViewAdapter<TableInfo>(){
           
                   @Override
                   public View getView(int position, View convertView, ViewGroup parent){
           
                       LayoutInflater lif = (LayoutInflater) getSystemService(Context.LAYOUT_INFLATER_SERVICE);
           
                       View view = lif.inflate(R.layout.detail_item_layout,null);
                       TextView tvName = (TextView)view.findViewById(R.id.tv_detail_name);
                       TextView tvNumber = (TextView)view.findViewById(R.id.tv_detail_number);
                       tvName.setText(getItem(position).getName());
                       tvNumber.setText(getItem(position).getNumber());
                       return view;
                   }
               };
               private View.OnClickListener ocl;
           
               @Override
               protected void onCreate(@Nullable Bundle savedInstanceState) {
                   super.onCreate(savedInstanceState);
                   setContentView(R.layout.acitivity_main);
                   Long idx = getIntent().getLongExtra("idx",-1);
           
                   //获取对象
                   listClass = (ListView) findViewById(R.id.list_class);
           
                   //获取显示数据？？？
                   listData = getData(idx);
           
                   //绑定适配器
                   va.setListDate(listData);
                   listClass.setAdapter(va);
           
                   //设置监听
                   listClass.setOnClickListener(ocl);
               }
           
               private List<TableInfo>getData(Long idx){
           
                   SQLiteDabseHandle handle = new SQLiteDabseHandle(this);
                   SQLiteDatabase database = handle.getSQLits();
           
                   StringBuilder sbSql = new StringBuilder();
                   sbSql.append("  select   ");
                   sbSql.append("  _id,name,number  ");
                   sbSql.append("  from  ");
                   sbSql.append("  table" + idx);
           
                   Cursor cursor = database.rawQuery(sbSql.toString(),null);
           
                   List<TableInfo> result = new ArrayList<>();
                   while (cursor.moveToNext()){
                       Long _id = cursor.getLong(0);
                       String name = cursor.getString(1);
                       String number = cursor.getString(2);
           
                       TableInfo tableInfo = new TableInfo( _id, name, number);
                       result.add(tableInfo);
                   }
           
                   // database.execSQL("update table set nember = ? where _id = ? ,new String[]{"100","1"}");
           
                   // update table1 set number = 100 where _id = 1
           
                   return result;
               }
           }
           
    * ClassInfo
         * package com.example.sqlitedemo;
           /**
            * Created by Administrator on 2016/10/25.
            */
           
           public class ClassInfo {
           
               private Long idx;
           
               private String name;
           
               public ClassInfo(Long idx,String name){
                   this.idx = idx;
                   this.name = name;
               }
           
               public void setIdx(Long idx) {
                   this.idx = idx;
               }
           
               public void setName(String name) {
                   this.name = name;
               }
           
               public String getName() {
                   return name;
               }
           
               public Long getIdx() {
                   return idx;
               }
           }
           
    * SQLiteDabseHandle
         * package com.example.sqlitedemo;           
           import android.content.Context;
           import android.content.res.AssetManager;
           import android.database.sqlite.SQLiteDatabase;
           
           import java.io.File;
           import java.io.FileNotFoundException;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.OutputStream;
           
           /**
            * Created by Administrator on 2016/10/25.
            */
           
           public class SQLiteDabseHandle {
           
               private Context context;
           
               public SQLiteDabseHandle(Context context){ this.context = context;}
           
               //把assets/db下的commonnum.db文件复制到/data/data/packagename/db目录下
           
               //文件复制
               /*
                       1.找到源文件名称，原路径 目标文件名称，目标路径
                */
           
               private File copyDabaseFile(){
           
                   String res_file_name = "commonnum.db";
                   String res_file_path = "db";
           
                   String target_file_name = "num.db";
                   String target_file_path = "/data/data/" + context.getPackageName() + "/db";
           
                   File file_target_path = null;
                   File file_target_file = null;
           
                   // 读取原路径下，源文件，使用文件构建字节输入流 InputStream
                   // 在目标路径创建目标文件，使用目标文件构建字节输出流 OutputStream
                   // 从输入流中读取字节文件写入到输出流中
           
                   try{
           
                       //判断目标路径是否存在，如果不存在则创建
                       file_target_path = new File(target_file_path);
           
                       if (!file_target_path.exists()){
                           file_target_path.mkdirs();
                       }
           
                       //判断目标文件是否存在，如果不存在则创建
                       file_target_file = new File(file_target_path,target_file_name);
           
                       if (!file_target_file.exists()){
                           file_target_file.mkdirs();
                       }
           
                       AssetManager assetManager = context.getAssets();
           
                       InputStream is = assetManager.open(res_file_path + File.separator + res_file_name);
                       OutputStream os = new FileOutputStream(new File(target_file_path,target_file_name));
           
                       int tmp = 0;
           
                       while ((tmp = is.read()) != -1){
                           os.write(tmp);
                       }
           
                       os.flush();
                       os.close();
                       is.close();
           
                   } catch (FileNotFoundException e){
                       e.printStackTrace();
                   } catch (IOException e){
                       e.printStackTrace();
                   }
           
                   return file_target_file;
               }
           
               public SQLiteDatabase getSQLits(){
                   SQLiteDatabase database = null;
                   File dbFile = copyDabaseFile();
           
                   if (dbFile != null && dbFile.exists()){
                       database = SQLiteDatabase.openOrCreateDatabase(dbFile, null);
                   }
           
                   return database;
               }
           
           
           }
    * TableInfo
        * package com.example.sqlitedemo;          
          /**
           * Created by Administrator on 2016/10/25.
           */
          
          public class TableInfo {
          
              private Long _id;
              private String name;
              private String number;
          
              public TableInfo(Long id, String name, String number) {
          
              }
          
              public void set_id(Long _id) {
                  this._id = _id;
              }
          
              public void setName(String name) {
                  this.name = name;
              }
          
              public void setNumber(String number) {
                  this.number = number;
              }
          
              public Long get_id() {
                  return _id;
              }
          
              public String getName() {
                  return name;
              }
          
              public String getNumber() {
                  return number;
              }
          
          }
          
    * ViewAdapter
        * package com.example.sqlitedemo;
          import android.widget.BaseAdapter;
          import java.util.ArrayList;
          import java.util.List;
          
          /**
           * Created by Administrator on 2016/10/25.
           */
          
          public abstract class ViewAdapter<T> extends BaseAdapter {
          
              private List<T>listDate = new ArrayList<T>();
          
              public ViewAdapter(){
              }
          
              @Override
              public int getCount() {
                  return listDate.size();
              }
          
              @Override
              public long getItemId(int position) {
                  return position;
              }
          
              @Override
              public T getItem(int position) {
                  return listDate.get(position);
              }
          
              public List<T> getListDate(){
                  return listDate;
              }
          
              public void setListDate(List<T>listDate){
                  this.listDate = listDate;
              }
          
          
          }

3. 工作内容

4. 未完成原因

5. 遇到问题及解析
