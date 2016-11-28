#2016-11-23工作日报
==================
1. 应完成工作
2. 已完成工作
      * package com.feicuiedu.android.gridviewlayout;

import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.ImageView;
import android.widget.TextView;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;

/**
 * Created by chenyan on 2016/11/16.
 */

public class GridViewAdapter extends BaseAdapter {

    public void setListData(List<Map<Integer, String>> listData) {
        this.listData = listData;
    }

    private void clearData() {
        listData.clear();
    }

    private List<Map<Integer, String>> listData = new ArrayList<>();

    private Context context;

    public GridViewAdapter(Context context) {
        this.context = context;
    }

    @Override
    public int getCount() {
        return listData.size();
    }

    @Override
    public Map<Integer, String> getItem(int position) {
        return listData.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {

        LayoutInflater lif = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);

        convertView = lif.inflate(R.layout.activity_main_item, null);

        ImageView iv1 = (ImageView) convertView.findViewById(R.id.iv1);
        TextView tv1 = (TextView) convertView.findViewById(R.id.tv1);

        Map<Integer,String> map = getItem(position);

        int key = 0;
        String value = "";

        for (Map.Entry<Integer,String> entry:map.entrySet()) {
            key = entry.getKey();
            value = entry.getValue();
        }

        iv1.setImageResource(key);
        tv1.setText(value);

        return convertView;
    }
}

3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
