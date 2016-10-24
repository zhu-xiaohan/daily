#2016-10-19工作日报
=================================================
 * 计算器
  * package com.feicuiedu.myapplication;

import android.graphics.Canvas;
import android.graphics.Color;
import android.os.Build;
import android.os.Bundle;
import android.support.annotation.RequiresApi;
import android.support.v7.app.AppCompatActivity;
import android.view.Gravity;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.EditText;
import android.widget.RelativeLayout;

/**
 * Created by Asus on 2016/10/19.
 */

public class MainActivitty  extends AppCompatActivity {
    @RequiresApi(api = Build.VERSION_CODES.JELLY_BEAN_MR1)
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main_acitivity);

        RelativeLayout r1 = new RelativeLayout(this);
        ViewGroup.LayoutParams vp= new ViewGroup.LayoutParams(
                ViewGroup.LayoutParams.MATCH_PARENT,
                ViewGroup.LayoutParams.MATCH_PARENT
        );
        r1.setLayoutParams(vp);
        r1.setBackgroundColor(Color.GREEN);

        EditText editText= new EditText(this);
        RelativeLayout.LayoutParams editTextparams = new RelativeLayout.LayoutParams(
                RelativeLayout.LayoutParams.MATCH_PARENT,
                RelativeLayout.LayoutParams.WRAP_CONTENT
        );
        editText.setLayoutParams(editTextparams);
        editText.setGravity(Gravity.RIGHT);
        editText.setId(View.generateViewId());

        r1.addView(editText);

        RelativeLayout.LayoutParams btnparams7=new RelativeLayout.LayoutParams(
                RelativeLayout.LayoutParams.WRAP_CONTENT,
                RelativeLayout.LayoutParams.WRAP_CONTENT
        );
        btnparams7.addRule(RelativeLayout.BELOW, editText.getId());

        Button btn7= new Button(this);
        btn7.setLayoutParams(btnparams7);
        btn7.setId(View.generateViewId());
        btn7.setText("7");

        RelativeLayout.LayoutParams btnparams8=new  RelativeLayout.LayoutParams(
                RelativeLayout.LayoutParams.WRAP_CONTENT,
                RelativeLayout.LayoutParams.WRAP_CONTENT

        );
       // btnparams7.addRule(RelativeLayout.BELOW, editText.getId());
        btnparams8.addRule(RelativeLayout.RIGHT_OF,btn7.getId());
        btnparams8.addRule(RelativeLayout.ALIGN_TOP,btn7.getId());
        Button btn8= new Button(this);
        btn8.setLayoutParams(btnparams8);
        btn8.setId(View.generateViewId());
        btn8.setText("8");

        RelativeLayout.LayoutParams btnparams9=new  RelativeLayout.LayoutParams(
                RelativeLayout.LayoutParams.WRAP_CONTENT,
                RelativeLayout.LayoutParams.WRAP_CONTENT

        );
        btnparams8.addRule(RelativeLayout.RIGHT_OF,btn8.getId());
        btnparams8.addRule(RelativeLayout.ALIGN_TOP,btn8.getId());

        Button btn9=new Button(this);
        btn8.setLayoutParams(btnparams9);
        btn8.setId(View.generateViewId());
        btn8.setText("9");

        r1.addView(btn7);
        r1.addView(btn8);
        r1.addView(btn9);


        setContentView(r1);


    }
}
