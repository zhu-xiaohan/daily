#2016-12-06工作日志
=======================
1.已完成工作
* package com.feicuiedu.android.contentproviderdemo;

import android.content.ContentResolver;
import android.database.Cursor;
import android.net.Uri;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.LinearLayout;
import android.widget.ListView;
import android.widget.TextView;

import java.io.File;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class MainActivity extends AppCompatActivity {


    private ListView lv1;
    private List<Map<String,String>> listData = new ArrayList<>();

    private BaseAdapter ba = new BaseAdapter() {
        @Override
        public int getCount() {
            return listData.size();
        }

        @Override
        public Map<String,String> getItem(int position) {
            return listData.get(position);
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {

            Map<String,String> tmpMap = getItem(position);

            LinearLayout ll = new LinearLayout(MainActivity.this);

            ll.setOrientation(LinearLayout.HORIZONTAL);
            TextView tvName = new TextView(MainActivity.this);

            tvName.setText(tmpMap.get("name"));

            TextView tvNumber = new TextView(MainActivity.this);

            tvNumber.setText(tmpMap.get("number"));

            LinearLayout.LayoutParams llp = new LinearLayout.LayoutParams(
                    LinearLayout.LayoutParams.WRAP_CONTENT,
                    LinearLayout.LayoutParams.MATCH_PARENT

            );

            ll.addView(tvName,llp);
            ll.addView(tvNumber,llp);

            return ll;
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        lv1 = (ListView) findViewById(R.id.lv1);

        listData = getContacts();
        lv1.setAdapter(ba);

    }


    private List<Map<String,String>> getContacts(){

        List<Map<String,String>> result = new ArrayList<>();

        //①查询raw_contacts表获得联系人的id
        ContentResolver resolver = getContentResolver();


        Uri uri = ContactsContract.CommonDataKinds.Phone.CONTENT_URI;

        //查询联系人数据
        Cursor cursor = resolver.query(uri, null, null, null, null);

        while(cursor.moveToNext()) {

            //获取联系人姓名,手机号码
            String cName = cursor.getString(cursor.getColumnIndex("display_name"));
            String cNum = cursor.getString(cursor.getColumnIndex("data1"));
            System.out.println("姓名:" + cName);
            System.out.println("号码:" + cNum);
            System.out.println("======================");

            Map<String,String> map = new HashMap<>();
            map.put("name",cName);
            map.put("number",cNum);
            result.add(map);
        }

        cursor.close();

        return result;
    }
}
2.未完成工作
3未完成工作的原因
4.遇到问题及解决方案
