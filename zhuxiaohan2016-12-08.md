#2016-12-08工作日志
1.已完成工作
  * package com.feicuiedu.android.servicesdemo;

import android.content.ComponentName;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.support.v7.app.AppCompatActivity;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    private static final String TAG = "MainActivity";
    private Button btnStart;
    private Button btnStop;

    private Button btnBinnerStart;
    private Button btnBinnerStop;

    private TextView tvResult;
    private MyBinderService.MyBiner binner;


    private View.OnClickListener ocl = new View.OnClickListener() {
        @Override
        public void onClick(View v) {

            int index = 0;
            Intent serviceIntent = new Intent();
            serviceIntent.setAction("mybinderservice");
            serviceIntent.putExtra("index",index);

            // android 5以后需要加上这个 Android 5 以后要 显示调用service
            serviceIntent.setPackage(getPackageName());
            if (v.getId() == R.id.btn_start) {
                startService(serviceIntent);
            }
            else if (v.getId() == R.id.btn_stop) {
                stopService(serviceIntent);
            }
            else if (v.getId() == R.id.btn_binner_start) {

                bindService(serviceIntent,connection,BIND_AUTO_CREATE);
            }
            else if (v.getId() == R.id.btn_binner_stop) {
                unbindService(connection);
                tvResult.setText(binner.getIndex()+"");
            }
        }
    };

    private ServiceConnection connection = new ServiceConnection() {

        @Override
        public void onServiceConnected(ComponentName name, IBinder service) {

            binner = (MyBinderService.MyBiner) service;



        }

        @Override
        public void onServiceDisconnected(ComponentName name) {

        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btnStart = (Button) findViewById(R.id.btn_start);
        btnStop = (Button) findViewById(R.id.btn_stop);

        btnBinnerStart = (Button) findViewById(R.id.btn_binner_start);
        btnBinnerStop = (Button) findViewById(R.id.btn_binner_stop);

        tvResult = (TextView) findViewById(R.id.tv_resullt);

        btnStart.setOnClickListener(ocl);
        btnStop.setOnClickListener(ocl);

        btnBinnerStart.setOnClickListener(ocl);
        btnBinnerStop.setOnClickListener(ocl);
    }


}

2.未完成工作
3.未完成工作的原因
4.遇到问题及解决方案
