#2016-11-01工作日报
==================

1. 应完成工作
    * 安卓管家欢迎界面
2. 工作内容
    * 布局
        * RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:tools="http://schemas.android.com/tools"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:background="@color/white"
          tools:context="com.main.LogoActivity">
          <ImageView
              android:id="@+id/iv_Logo"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:layout_centerHorizontal="true"
              android:layout_centerVertical="true"
              android:src="@drawable/logo_2"/>
    * 代码
        * package com.main;
          import android.content.Intent;
          import android.os.Bundle;
          import android.support.annotation.Nullable;
          import android.support.v7.app.AppCompatActivity;
          import android.view.View;
          import android.view.animation.Animation;
          import android.view.animation.AnimationUtils;
          
          import com.example.administrator.feicui_android1.R;
          
          /**
           * Created by Administrator on 2016/11/1.
           */
          
          public class LogoActivity extends AppCompatActivity {
          
              private View img_Logo;
              private Animation animation;
          
              @Override
              protected void onCreate(@Nullable Bundle savedInstanceState) {
                  super.onCreate(savedInstanceState);
                  setContentView(R.layout.activity_logo);
                  //初始控件及动画
                  img_Logo = findViewById(R.id.iv_Logo);
                  animation = AnimationUtils.loadAnimation(this,R.anim.anim_logo);
                  animation.setAnimationListener(animationListener);
                  //Logo图像控件及动画
                  img_Logo.startAnimation(animation);
              }
          
              private Animation.AnimationListener animationListener = new Animation.AnimationListener() {
                  //动画开始
                  @Override
                  public void onAnimationStart(Animation animation) {
          
                  }
          
                  //动画结束
                  @Override
                  public void onAnimationEnd(Animation animation) {
          
                      Intent intent = new Intent(LogoActivity.this,TelmsgActivity.class);
                      startActivity(intent);
                      finish();
                  }
          
                  //动画重复
                  @Override
                  public void onAnimationRepeat(Animation animation) {
          
                  }
              };
          }
3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
