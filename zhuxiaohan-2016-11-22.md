#2016-11-22工作日报
===================
1. 应完成工作
2. 已完成工作
      * package com.feicuiedu.android.gridviewlayout;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.widget.GridView;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class MainActivity extends AppCompatActivity {

    private GridView gv1;
    private List<Map<Integer,String>> listData = null;

    private GridViewAdapter gva;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 控件 数据源 适配器

        gv1 = (GridView) findViewById(R.id.gv_1);

        // listData = getData();
        gva = new GridViewAdapter(this);
        gv1.setAdapter(gva);


    }

    @Override
    protected void onResume() {
        super.onResume();
        listData = getData();
        gva.setListData(listData);

        gva.notifyDataSetChanged();
    }

    private List<Map<Integer,String>> getData() {
        List<Map<Integer,String>> result = new ArrayList<>();

        Map<Integer,String> map = new HashMap<>();
        map.put(R.drawable.icon_archive,"app1");
        result.add(map);

        map = new HashMap<>();
        map.put(R.drawable.icon_bmp,"app2");
        result.add(map);

        map = new HashMap<>();
        map.put(R.drawable.icon_c_h,"app3");
        result.add(map);

        map = new HashMap<>();
        map.put(R.drawable.icon_css,"app4");
        result.add(map);

        map = new HashMap<>();
        map.put(R.drawable.icon_archive,"app5");
        result.add(map);

        map = new HashMap<>();
        map.put(R.drawable.icon_archive,"app6");
        result.add(map);

        map = new HashMap<>();
        map.put(R.drawable.icon_archive,"app7");
        result.add(map);

        map = new HashMap<>();
        map.put(R.drawable.icon_archive,"app8");
        result.add(map);

        map = new HashMap<>();
        map.put(R.drawable.icon_archive,"app9");
        result.add(map);

        /*map = new HashMap<>();
        map.put(R.drawable.icon_archive,"app1");
        result.add(map);*/
        return result;
    }
}

3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
