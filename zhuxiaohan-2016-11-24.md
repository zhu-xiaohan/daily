#2016-11-24工作日报
==================
1. 应完成工作
2. 已完成工作
      * package com.feicuiedu.android.expressage;

import android.content.Context;
import android.os.Bundle;
import android.os.Handler;
import android.os.Message;
import android.support.v7.app.AppCompatActivity;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.AdapterView;
import android.widget.BaseAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListAdapter;
import android.widget.ListView;
import android.widget.Spinner;
import android.widget.SpinnerAdapter;
import android.widget.TextView;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.ProtocolException;
import java.net.URL;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class MainActivity extends AppCompatActivity {

    private static final String TAG = "MainActivity";

    private Context context;

    private EditText edOrder;
    private Spinner spCompany;
    private Button btnQuery;
    private ListView lvData;

    private  String orderNo;

    private List<Map<String,String>> lstData = new ArrayList<>();
    private Handler handler = new Handler() {
        @Override
        public void handleMessage(Message msg) {

            if (msg.what == 1) {
                String strJson = (String) msg.obj;
                Log.d(TAG, "handleMessage: "+strJson);

                try {
                    JSONObject jsonObject = new JSONObject(strJson);
                    JSONArray array= jsonObject.getJSONArray("data");
                    for (int i = 0; i < array.length(); i++) {
                        JSONObject obj = array.getJSONObject(i);
                        String time = obj.getString("time");
                        String ftime = obj.getString("ftime");
                        String context = obj.getString("context");

                        Map<String,String> tmpMap = new HashMap<>();
                        tmpMap.put("time", time);
                        tmpMap.put("ftime", ftime);
                        tmpMap.put("context", context);

                        lstData.add(tmpMap);

                        lvData.setAdapter(lvAdapter);
                    }
                } catch (JSONException e) {
                    e.printStackTrace();
                }
            }
        }
    };

    private ListAdapter lvAdapter = new BaseAdapter() {

        @Override
        public int getCount() {
            return lstData.size();
        }

        @Override
        public Map<String,String> getItem(int position) {
            return lstData.get(position);
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {

            LayoutInflater lif = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
            convertView = lif.inflate(R.layout.listview_item_layout, null);

            TextView tvTime = (TextView) convertView.findViewById(R.id.tv_time);
            TextView tvFTime = (TextView) convertView.findViewById(R.id.tv_ftime);
            TextView tvContent = (TextView) convertView.findViewById(R.id.tv_content);

            Map<String,String> map = getItem(position);
            String time = map.get("time");
            String ftime = map.get("ftime");
            String context = map.get("context");

            tvTime.setText(time);
            tvFTime.setText(ftime);
            tvContent.setText(context);


            return convertView;
        }
    };

    private List<Map<String, String>> lstCompany = new ArrayList<>();

    private String selectedCompany;
    private SpinnerAdapter spAdapter = new BaseAdapter() {
        @Override
        public int getCount() {
            return lstCompany.size();
        }

        @Override
        public Map<String, String> getItem(int position) {
            return lstCompany.get(position);
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {

            LayoutInflater lif = (LayoutInflater) getSystemService(Context.LAYOUT_INFLATER_SERVICE);
            convertView = lif.inflate(R.layout.spinner_item_layout, null);
            TextView tvCompanyName = (TextView) convertView.findViewById(R.id.tv_company_name);
            Map<String, String> map = getItem(position);
            String value = "";
            for (Map.Entry<String, String> entry : map.entrySet()) {
                value = entry.getValue();
            }

            tvCompanyName.setText(value);
            return convertView;
        }
    };
    private View.OnClickListener btnOcl = new View.OnClickListener() {

        @Override
        public void onClick(View v) {
            orderNo = String.valueOf(edOrder.getText());

//            MyAsyncTask mat = new MyAsyncTask(lvData,context);
//            mat.execute(orderNo,selectedCompany);

            new Thread() {
                @Override
                public void run() {
                    String company = selectedCompany;

                    String strUrl = "http://www.kuaidi100.com/query";
                    String strParams = "type="+company+"&postid="+orderNo;

                    String result = null;
                    URL url = null;
                    try {
                        url = new URL(strUrl);
                        HttpURLConnection httpURLConnection = (HttpURLConnection) url.openConnection();
                        httpURLConnection.setConnectTimeout(5000);

                        httpURLConnection.setDoOutput(true);
                        httpURLConnection.setDoInput(true);

                        httpURLConnection.setRequestMethod("POST");
                        // httpURLConnection.setRequestMethod("POST");

                        // 获取输出流
                        OutputStream out = httpURLConnection.getOutputStream();
                        out.write(strParams.getBytes());
                        out.flush();

                        if (httpURLConnection.getResponseCode() == 200) {

                            InputStream is = httpURLConnection.getInputStream();

                            byte[] data = read(is);
                            result = new String(data, "UTF-8");
                        }
                    } catch (MalformedURLException e) {
                        e.printStackTrace();
                    } catch (ProtocolException e) {
                        e.printStackTrace();
                    } catch (IOException e) {
                        e.printStackTrace();
                    } catch (Exception e) {
                        e.printStackTrace();
                    }

                    Message message = new Message();
                    message.obj = result;
                    message.what = 1;

                    handler.sendMessage(message);
                }
            }.start();

        }
    };
    private AdapterView.OnItemSelectedListener spOisl = new AdapterView.OnItemSelectedListener() {

        @Override
        public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
            Map<String, String> map = lstCompany.get(position);
            String key = "";
            for (Map.Entry<String, String> entry : map.entrySet()) {
                key = entry.getKey();
            }

            selectedCompany = key;

            // Toast.makeText(context,"当先选择中的快递公司为:"+selectedCompany,Toast.LENGTH_SHORT).show();
        }

        @Override
        public void onNothingSelected(AdapterView<?> parent) {

        }
    };


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        context = this;
        initView();
        initData();

        spCompany.setAdapter(spAdapter);
        spCompany.setOnItemSelectedListener(spOisl);
        btnQuery.setOnClickListener(btnOcl);
    }

    private void initView() {

        edOrder = (EditText) findViewById(R.id.ed_order);
        spCompany = (Spinner) findViewById(R.id.sp_company);
        btnQuery = (Button) findViewById(R.id.btn_query);
        lvData = (ListView) findViewById(R.id.lv_data);
    }

    private void initData() {
        lstCompany = getCompanys();

    }

    private List<Map<String, String>> getCompanys() {
        List<Map<String, String>> result = new ArrayList<>();

        Map<String, String> map = new HashMap<>();
        map.put("shentong", "申通");
        result.add(map);

        map = new HashMap<>();
        map.put("ems", "EMS");
        result.add(map);


        map = new HashMap<>();
        map.put("shunfeng", "顺丰");
        result.add(map);

        map = new HashMap<>();
        map.put("yuantong", "圆通");
        result.add(map);

        map = new HashMap<>();
        map.put("zhongtong", "中通");
        result.add(map);

        map = new HashMap<>();
        map.put("yunda", "韵达");
        result.add(map);

        map = new HashMap<>();
        map.put("tiantian", "天天");
        result.add(map);

        map = new HashMap<>();
        map.put("huitongkuaidi", "汇通");
        result.add(map);

        map = new HashMap<>();
        map.put("quanfengkuaidi", "全峰");
        result.add(map);

        map = new HashMap<>();
        map.put("debangwuliu", "德邦");
        result.add(map);

        map = new HashMap<>();
        map.put("zhaijisong", "宅急送");
        result.add(map);

        return result;
    }

    // 从流中读取数据
    public byte[] read(InputStream inStream) throws Exception {
        ByteArrayOutputStream outStream = new ByteArrayOutputStream();
        byte[] buffer = new byte[1024];
        int len = 0;
        while ((len = inStream.read(buffer)) != -1) {
            outStream.write(buffer, 0, len);
        }
        inStream.close();
        return outStream.toByteArray();
    }
}

3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
