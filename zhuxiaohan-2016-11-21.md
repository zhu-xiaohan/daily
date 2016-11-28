#2016-11-21工作日报
===================
1. 应完成工作
2. 已完成工作
      * package com.feicuiedu.fragmentdemo;

import android.app.FragmentManager;
import android.app.FragmentTransaction;
import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.FrameLayout;
import android.widget.TextView;

import java.util.Map;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {

    //UI Object
    private TextView txt_topbar;
    private TextView txt_channel;
    private TextView txt_message;
    private TextView txt_better;
    private TextView txt_setting;
    private FrameLayout ly_content;

    //Fragment Object
    private MyFragment fg1;
    private MyFragment fg2;
    private MyFragment fg3;
    private MyFragment fg4;

    private FragmentManager fManager;

    private String rtnMsg;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        fManager = getFragmentManager();
        bindViews();
        txt_channel.performClick();
    }

    //UI组件初始化与事件绑定
    private void bindViews() {
        txt_topbar = (TextView) findViewById(R.id.txt_topbar);
        txt_channel = (TextView) findViewById(R.id.txt_channel);
        txt_message = (TextView) findViewById(R.id.txt_message);
        txt_better = (TextView) findViewById(R.id.txt_better);
        txt_setting = (TextView) findViewById(R.id.txt_setting);
        ly_content = (FrameLayout) findViewById(R.id.ly_content);

        txt_channel.setOnClickListener(this);
        txt_message.setOnClickListener(this);
        txt_better.setOnClickListener(this);
        txt_setting.setOnClickListener(this);
    }

    //重置所有文本的选中状态
    private void setSelected() {
        txt_channel.setSelected(false);
        txt_message.setSelected(false);
        txt_better.setSelected(false);
        txt_setting.setSelected(false);
    }

    //隐藏所有Fragment
    private void hideAllFragment(FragmentTransaction fragmentTransaction) {
        if (fg1 != null) {
            fragmentTransaction.hide(fg1);
        }
        if (fg2 != null) {
            fragmentTransaction.hide(fg2);
        }
        if (fg3 != null) {
            fragmentTransaction.hide(fg3);
        }
        if (fg4 != null) {
            fragmentTransaction.hide(fg4);
        }
    }

    @Override
    public void onClick(View v) {
        // FragmentTransaction只能使用一次
        FragmentTransaction ft = fManager.beginTransaction();
        hideAllFragment(ft);
        Bundle param = new Bundle();
        switch(v.getId()){
            case R.id.txt_channel:
                setSelected();

                // 给fragment传参
                param.putString("content","channel fragment");
                param.putInt("index",0);

                txt_channel.setSelected(true);
                if (fg1 == null) {
                    fg1 = new MyFragment();

                    ft.add(R.id.ly_content,fg1);
                    // 非fragmeng传递参数
                    fg1.setArguments(param);
                }
                else {
                    ft.show(fg1);
                }

                // 获取fargment传递过来的参数
                fg1.rtnData(new MyFragment.IResult() {
                    @Override
                    public void getResult(Map<String, Object> map) {
                        rtnMsg = (Integer)map.get("rtnIndex")+(String)map.get("rtnContent");
                        txt_topbar.setText(rtnMsg);
                    }
                });
                break;
            case R.id.txt_message:
                setSelected();
                param.putString("content","message fragment");
                param.putInt("index",1);
                txt_message.setSelected(true);
                if (fg2 == null) {
                    fg2 = new MyFragment();

                    ft.add(R.id.ly_content,fg2);
                    fg2.setArguments(param);
                }
                else {
                    ft.show(fg2);
                }



                fg2.rtnData(new MyFragment.IResult() {
                    @Override
                    public void getResult(Map<String, Object> map) {
                        rtnMsg = (Integer)map.get("rtnIndex")+(String)map.get("rtnContent");
                        txt_topbar.setText(rtnMsg);
                    }
                });
                break;
            case R.id.txt_better:
                setSelected();

                param.putString("content","better fragment");
                param.putInt("index",2);

                txt_better.setSelected(true);
                if (fg3 == null) {
                    fg3 = new MyFragment();
                    ft.add(R.id.ly_content,fg3);
                    fg3.setArguments(param);
                }
                else {
                    ft.show(fg3);
                }



                fg3.rtnData(new MyFragment.IResult() {
                    @Override
                    public void getResult(Map<String, Object> map) {
                        rtnMsg = (Integer)map.get("rtnIndex")+(String)map.get("rtnContent");
                        txt_topbar.setText(rtnMsg);
                    }
                });
                break;
            case R.id.txt_setting:
                setSelected();

                param.putString("content","setting fragment");
                param.putInt("index",3);
                txt_setting.setSelected(true);
                if (fg4 == null) {
                    fg4 = new MyFragment();
                    ft.add(R.id.ly_content,fg4);
                    fg4.setArguments(param);
                }
                else {
                    ft.show(fg4);
                }



                fg4.rtnData(new MyFragment.IResult() {
                    @Override
                    public void getResult(Map<String, Object> map) {
                        rtnMsg = (Integer)map.get("rtnIndex")+(String)map.get("rtnContent");
                        txt_topbar.setText(rtnMsg);
                    }
                });
                break;
        }
        ft.commit();


    }
}

3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
