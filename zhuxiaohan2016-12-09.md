#2016-12-09工作日报
1.已完成工作
* package com.feicuiedu.android.servicesdemo;

import android.app.Service;
import android.content.Intent;
import android.os.Binder;
import android.os.IBinder;
import android.util.Log;

import java.util.Timer;
import java.util.TimerTask;

/**
 * Created by chenyan on 2016/12/7.
 */

public class MyBinderService extends Service {

    private static final String TAG = "MyBinderService";

    private int index;

    public MyBiner biner = new MyBiner();

    public class MyBiner extends Binder {

        public int getIndex() {
            return index;
        }
    }

    @Override
    public IBinder onBind(Intent intent) {
        index = intent.getIntExtra("index",-1);

        Timer timer = new Timer();
        timer.schedule(new TimerTask() {
            @Override
            public void run() {
                index ++;
                Log.d(TAG, "onBind: index="+index);
            }
        },0,1000);



        return biner;
    }

    @Override
    public void onCreate() {
        Log.d(TAG, "onCreate: ");
        super.onCreate();

    }

    @Override
    public void onDestroy() {
        Log.d(TAG, "onDestroy: ");
        super.onDestroy();
    }


}

2.未完成工作
3.未完成工作的原因
4.遇到问题及解决方案
