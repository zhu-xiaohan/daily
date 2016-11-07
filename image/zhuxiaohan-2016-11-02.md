#2016-11-02工作日报
===================

1. 应完成工作
    * 获取电话列表
2. 工作内容
    * resources>
      <color name="Primary">#3F51B5</color>
      <color name="PrimaryDark">#303F9F</color>
      <color name="Accent">#FF4081</color>
      <color name="white">#FFF</color>
      <color name="black">#000</color>
      <color name="transparent">#0000</color>
    * <dimen name="activity_horizontal_margin">16dp</dimen>
      <dimen name="activity_vertical_margin">16dp</dimen>
      <!-- 通讯大全 -->
      <dimen name="tel_show_height">140dp</dimen>
      <dimen name="tel_show_textsize">20sp</dimen>
      <dimen name="tel_item_height">60dp</dimen>
      <dimen name="tel_listitem_height">30dp</dimen>
    * LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      tools:context="com.main.TelmsgActivity"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:orientation="vertical">
      <TextView
          style="@style/tel_showtext"
          android:layout_width="match_parent"
          android:layout_height="@dimen/tel_show_height"
          android:layout_weight="0"
          android:id="@+id/textView" />
      <ListView
          android:id="@+id/listview"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:layout_weight="1"
          android:cacheColorHint="@color/transparent">
    * package com.main;
      import android.content.Intent;
      import android.os.Bundle;
      import android.support.annotation.Nullable;
      import android.support.v7.app.AppCompatActivity;
      import android.view.View;
      import android.widget.AdapterView;
      import android.widget.ListView;
      import android.widget.Toast;
      
      import com.Utils.ToastUtil;
      import com.adapter.TelclassAdapter;
      import com.db.AssetsDBManager;
      import com.db.DBReader;
      import com.entity.TelclassInfo;
      import com.example.administrator.feicui_android1.R;
      
      import java.io.IOException;
      
      /**
       * Created by Administrator on 2016/11/1.
       */
      
      public class TelmsgActivity extends AppCompatActivity implements AdapterView.OnItemClickListener {
      
          //全局定义ListView控件
          private ListView listView;
          //全局定义TelclassAdapter
          private TelclassAdapter adapter;
      
          @Override
          protected void onCreate(@Nullable Bundle savedInstanceState) {
              super.onCreate(savedInstanceState);
              setContentView(R.layout.activity_telmsg);
              //初始控件
              listView = (ListView) findViewById(R.id.listview);
              adapter = new TelclassAdapter(this);
              ListView.setAdapter(adapter);
              listView.setOnItemClickListener(this);
          }
          //initAppDBFile()方法：初始化数据库文件
          private void initAppDBFile(){
              //检测是否存在通讯大全DB文件
              if (!DBReader.isExistsTeldbFile()){
                  try{
                      //将本地项目中的Assets/db/commonnum.db文件复制写出到DBRead.telFile文件中
                      AssetsDBManager.copyAssetsFileToFile(getApplicationContext(),"db/commonnum.db", DBReader.telFile);
                  }catch (IOException e){
                      ToastUtil.show(this,"初始通讯大全数据库文件异常", Toast.LENGTH_LONG);
                  }
              }
          }
          //重写onResume（）方法中初始化展示的数据
          @Override
          protected void onResume() {
              super.onResume();
              //适配数据
              initAppDBFile();
              adapter.clearDataTOAdapter();
              adapter.addDataToAdapter(new TelclassInfo("本地电话", 0));
              //本地电话分类
              try{
                  adapter.addDataToAdapter(DBReader.readTeldbClassList());
              } catch (Exception e) {
                  //TODO Auto-generated catch block
                  e.printStackTrace();
              }
              //db库内的电话分类
              adapter.notifyDataSetChanged();
          }
      
          @Override
          public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
              //本地通话
              if (position == 0){
                  Intent intent = new Intent();
                  intent.setAction(Intent.ACTION_DIAL);
                  startActivity(intent);
                  return;
              }
              //取出当前选择的选项实体内容
              TelclassInfo classInfo = adapter.getItem(position);
              //跳转至电话浏览页面，且传入idx，并且根据idx跳转
              Intent intent = new Intent(this, TellistActivity.class);
              intent.putExtra("idx", classInfo.idx);
              startActivity(intent);
          }
      }
3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
