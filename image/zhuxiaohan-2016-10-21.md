#2016-10-21工作日报
==================

1. 已完成工作 
    * 使用android studio完成日报页面跳转
2. 工作内容
    * package com.example.listviewdemo;
      import android.os.Bundle;
      import android.support.annotation.Nullable;
      import android.support.v7.app.AppCompatActivity;
      import android.view.View;
      import android.view.ViewGroup;
      import android.widget.AdapterView;
      import android.widget.BaseAdapter;
      import android.widget.ListView;
      import android.widget.TextView;
      import android.widget.Toast;
      
      import java.util.ArrayList;
      import java.util.HashMap;
      import java.util.List;
      import java.util.Map;
      
      /**
       * Created by Administrator on 2016/10/21.
       */
      
      public class MainAcitivity extends AppCompatActivity {
      
          private ListView listView1;
          private List<Map<String,String>>list;
      
          @Override
          protected void onCreate(@Nullable Bundle savedInstanceState) {
              super.onCreate(savedInstanceState);
              setContentView(R.layout.main_layout);
      
              listView1 = (ListView)findViewById(R.id.listView1);
              list = getData();
              listView1.setAdapter(baseAdapter);
              listView1.setOnItemClickListener(oicl);
          }
      
          private AdapterView.OnItemClickListener oicl = new AdapterView.OnItemClickListener(){
      
              @Override
              public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                  Toast.makeText(MainAcitivity.this,"position="+position+",id="+id,Toast.LENGTH_LONG).show();
              }
          };
      
          private List<Map<String,String>>getData(){
      
              List<Map<String,String>>tmp = new ArrayList<>();
      
              for (int i = 1; i < 30; i++){
                  Map<String,String>map = new HashMap<>();
                  map.put("id",i+"");
                  map.put("createDate","2016-10-"+i);
                  map.put("name","2016-10-"+i+"日报");
                  tmp.add(map);
              }
              return tmp;
          }
      
          private BaseAdapter baseAdapter = new BaseAdapter(){
      
              //定义数据个数
              @Override
              public int getCount() { return list.size(); }
      
              //定义每行数据的对象
              @Override
              public Map<String, String> getItem(int position) { return list.get(position); }
      
              //定义每行id的值
              @Override
              public long getItemId(int position) { return position; }
      
              //定义每行都是什么样的布局，如何展示数据
              @Override
              public View getView(int position, View convertView, ViewGroup parent) {
                  Map<String,String> tmpMap = getItem(position);
      
                  String id = tmpMap.get("id");
                  String createDate = tmpMap.get("createDate");
                  String name = tmpMap.get("name");
      
                  View view = getLayoutInflater().inflate(R.layout.main_item_layout,null);
