#2016-10-18工作日报
====================

1. 已完成工作
    * androidStudio 按钮事件
2. 工作内容
    * Button控件
      * package com.eric.day1018;

import android.app.Activity;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends Activity{
//public class MainActivity extends Activity implements View.OnClickListener{

    private Button mybutton_btn = null;

    /**
     * 点击时间的方法
     * 一: 匿名内部类
     * 二:内部类
     * 三:实现onclicklistener接口
     * 四: 按钮onclick属性
     * */
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main_activity);
        mybutton_btn = (Button)findViewById(R.id.mybutton_btn);
//        mybutton_btn.setOnClickListener(this);

//        mybutton_btn.setOnClickListener(new View.OnClickListener() {
//            @Override
//            public void onClick(View v) {
//                Toast.makeText(getApplicationContext(),"点击事件一",Toast.LENGTH_LONG).show();
//            }
//        });

//        mybutton_btn.setOnClickListener(listener);

    }

//    @Override
//    public void onClick(View v) {
//        if(v == mybutton_btn){
//            Toast.makeText(this,"马宁  别  BB",Toast.LENGTH_LONG).show();
//        }
//    }


    public void onClick2(View v){
        Toast.makeText(this,"点击按钮四",Toast.LENGTH_LONG).show();
    }

//    View.OnClickListener listener = new View.OnClickListener() {
//        @Override
//        public void onClick(View v) {
//            Toast.makeText(getApplicationContext(),"点击事件二",Toast.LENGTH_LONG).show();
//        }
//    };


}

3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
