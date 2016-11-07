#2016-11-03工作日报
===================

1. 应完成工作
2. 工作内容
      * package com.main;
        import android.content.DialogInterface;
        import android.content.Intent;
        import android.media.browse.MediaBrowser;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.annotation.Nullable;
        import android.support.v7.app.AlertDialog;
        import android.support.v7.app.AppCompatActivity;
        
        import android.view.View;
        import android.widget.AdapterView;
        import android.widget.ListView;
        
        import com.adapter.TellistAdapter;
        import com.db.DBReader;
        import com.example.administrator.feicui_android1.R;
        
        /**
         * Created by Administrator on 2016/11/2.
         */
        
        //通讯大全电话号码浏览页面
        public class TellistActivity extends AppCompatActivity implements AdapterView.OnItemClickListener{
            //全局定义ListView
            private ListView listView;
            //全局定义TellistAdapter
            private TellistAdapter adapter;
            private int idx = 0;
        
            @Override
            protected void onCreate(@Nullable Bundle savedInstanceState) {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.activity_tellist);
                //获取数据用来判断是显示哪一种分类的电话号码列表
                idx = getIntent().getLongExtra("idx", -1);
                //初始控件
                listView = (ListView) findViewById(R.id.listview);
                adapter = new TellistAdapter(this);
                listView.setOnItemClickListener(this);
                listView.setAdapter(adapter);
            }
        
            //重写onItemClick()方法
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                String name = adapter.getItem(position).name;
                String number = adapter.getItem(position).number;
                showCallDiaLog(name, number);
            }
        
            //重写onResume()方法
            @Override
            protected void onResume() {
                super.onResume();
                //添加数据
                try{
                    adapter.addDataToAdapter(DBReader.readTeldbTable(idx));
                }catch (Exception e){
                    e.printStackTrace();
                }
                adapter.notifyDataSetChanged();
            }
        
            //点击item出现Dialog显示拨打电话，并拨打电话
            private void showCallDiaLog(String name, final String number) {
                AlertDialog.Builder builder = new AlertDialog.Builder(this);
                builder.setTitle("警号");
                builder.setMessage("是否开始拨打" + name + "电话 ?\n\nTEL:" + number);
                builder.setNegativeButton("取消", null);
                builder.setPositiveButton("拨号", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        //电话拨打
                        Intent intent = new Intent(Intent.ACTION_CALL);
                        intent.setData(Uri.parse("tel://" + number));
                        startActivity(intent);
                    }
                });
                builder.show();
            }
        }
3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
