#2016-10-26工作日报
===================

1. 应完成工作
2. 工作内容
      * package com.feicuiedu.android.listviewdemo;
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
         * Created by chenyan on 2016/10/20.
         */
        
        public class MainAcitivity extends AppCompatActivity {
        
            private ListView listView1;
            private List<Map<String,String>> list;
        
            @Override
            protected void onCreate(@Nullable Bundle savedInstanceState) {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main_layout);
        
                listView1 = (ListView) findViewById(R.id.listView1);
                list = getData();
        
                // 绑定适配器
                listView1.setAdapter(baseAdapter);
        
                // 监听事件
                listView1.setOnItemClickListener(oicl);
            }
        
            private AdapterView.OnItemClickListener oicl = new AdapterView.OnItemClickListener() {
                @Override
                public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                    Toast.makeText(MainAcitivity.this,"position="+position+",id="+id,Toast.LENGTH_LONG).show();
                }
            };
        
            private List<Map<String,String>> getData() {
        
                List<Map<String,String>> tmp = new ArrayList<Map<String,String>>();
        
                for (int i = 0; i < 20; i++) {
                    Map<String,String> map = new HashMap<String,String>();
                    map.put("id",i+"");
                    map.put("createDate","2016-10-"+i);
                    map.put("name","2016-10-"+i+"日报");
                    tmp.add(map);
                }
        
                return tmp;
            }
        
            private BaseAdapter baseAdapter = new BaseAdapter() {
        
                // 定义数据的个数
                @Override
                public int getCount() {
                    return list.size();
                }
        
                // 定义每行数据的对象
                @Override
                public Map<String,String> getItem(int position) {
                    return list.get(position);
                }
        
                // 定义每行的id值
                @Override
                public long getItemId(int position) {
                    return position;
                }
        
                // 定义每行都 是什么样的布局,如何展示数据
                @Override
                public View getView(int position, View convertView, ViewGroup parent) {
                    Map<String,String> tmpMap = getItem(position);
        
                    String id = tmpMap.get("id");
                    String createDate = tmpMap.get("createDate");
                    String name = tmpMap.get("name");
        
        
                    View view = getLayoutInflater().inflate(R.layout.main_item_layout,null);
        
                    TextView tvId = (TextView) view.findViewById(R.id.tvId);
                    TextView tvName= (TextView) view.findViewById(R.id.tvName);
                    TextView tvDate = (TextView) view.findViewById(R.id.tvDate);
        
                    tvId.setText(id);
                    tvDate.setText(createDate);
                    tvName.setText(name);
        
                    return view;
                }
            };
        
        
        }
3. 未完成工作
4. 未完成原因
5. 遇到问题 及解析
