#2016-10-20工作日报
====================

1. 已完成工作
      * 在android studio中实现页面跳转
2. 工作内容
      * 由页面一跳转到页面二
      * 跳转代码
              * private View.OnClickListener ocl = new View.OnClickListener(){
                      @Override
                      public void onClick(View v) {
                          Intent intent = new Intent();
                          intent.setClass(MainActivity.this, InputActivity.class);
                          startActivityForResult(intent, 99);
                      }
                 };
      * 页面一
          * package com.example.intentdemo;
          * import android.content.Intent;
          * import android.os.Bundle;
          * import android.support.annotation.Nullable;
          * import android.support.v7.app.AppCompatActivity;
          * import android.support.v7.widget.VectorEnabledTintResources;
          * import android.view.View;
          * import android.widget.Button;
          * import android.widget.TextView;
            /**
             * Created by Administrator on 2016/10/21.
             */            
            public class MainActivity extends AppCompatActivity {
            
                private Button btuCal;
                private TextView txtCalResultValue;
            
                @Override
                protected void onCreate(@Nullable Bundle savedInstanceState) {
                    super.onCreate(savedInstanceState);
                    setContentView(R.layout.main_layout);
            
                    txtCalResultValue = (TextView) findViewById(R.id.txtCalResultValue);
            
                    btuCal = (Button)findViewById(R.id.btuCal);
                    btuCal.setOnClickListener(ocl);
                }
                //跳转
                private View.OnClickListener ocl = new View.OnClickListener(){
            
                    @Override
                    public void onClick(View v) {
                        Intent intent = new Intent();
                        intent.setClass(MainActivity.this, InputActivity.class);
                        startActivityForResult(intent, 99);
                    }
                };
            
            //    @Override
            //    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            //        super.onActivityResult(requestCode, resultCode, data);
            
            
                @Override
                protected void onActivityResult(int requestCode, int resultCode, Intent data) {
                    super.onActivityResult(requestCode, resultCode, data);
            
                int param1 = data.getIntExtra("param1",-1);
                    int param2 = data.getIntExtra("param2",-1);
            
                    int result = param1 + param2;
                    txtCalResultValue.setText(String.valueOf(result));
                }
            }

      * 页面二
           * package com.example.intentdemo;
           * import android.content.Intent;
           * import android.os.Bundle;
           * import android.support.annotation.Nullable;
           * import android.support.v7.app.AppCompatActivity;
           * import android.view.View;
           * import android.widget.Button;
           * import android.widget.EditText;
            
            /**
             * Created by Administrator on 2016/10/21.
             */
            
            public class InputActivity extends AppCompatActivity {
            
                private EditText param1;
                private EditText param2;
                private Button btnClose;
            
                @Override
                protected void onCreate(@Nullable Bundle savedInstanceState) {
                    super.onCreate(savedInstanceState);
                    setContentView(R.layout.input_layout);
            
                    param1 = (EditText) findViewById(R.id.edit_param1);
                    param2 = (EditText) findViewById(R.id.edit_param2);
                    btnClose = (Button) findViewById(R.id.btnClose);
                    btnClose.setOnClickListener(ocl);
                }
            
                private View.OnClickListener ocl = new View.OnClickListener() {
                    @Override
                    public void onClick(View v) {
                        String strParam1 = String.valueOf(param1.getText());
                        String strParam2 = String.valueOf(param2.getText());
            
                        Intent intent = new Intent();
                        intent.putExtra("param1", Integer.valueOf(strParam1));
                        intent.putExtra("param2", Integer.valueOf(strParam2));
            
                        setResult(100, intent);
            
                        InputActivity.this.finish();
                    }
                };
            }

3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
