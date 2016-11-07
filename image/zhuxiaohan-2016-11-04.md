#2016-11-04工作日报
===================

1. 应完成工作
2. 工作内容
    * package com.db;
      import android.content.Context;
      
      import com.Utils.LogoUtil;
      
      import java.io.BufferedInputStream;
      import java.io.BufferedOutputStream;
      import java.io.File;
      import java.io.FileOutputStream;
      import java.io.IOException;
      import java.io.InputStream;
      
      /**
       * Created by Administrator on 2016/11/1.
       */
      
      public class AssetsDBManager {
      
      
      
          public static void copyAssetsFileToFile(Context context, String path, File toFile)throws IOException {
              LogoUtil.d("AssetsDBManager","copyAssetsFileToFile start");
              LogoUtil.d("AssetsDBManager","file path:" + path);
              LogoUtil.d("AssetsDBManager","toFile path:" + toFile.getAbsolutePath());
              InputStream inStream = null;
              //输出流（用来读取当前项目的Assets内的db文本）
              BufferedInputStream bufferedInputStream = null;
              //输出流（用来将读取到的db信息写到指定目录文件toFile中去）
              BufferedOutputStream bufferedOutputStream = null;
              try{
                  inStream = context.getAssets().open(path);
                  bufferedInputStream = new BufferedInputStream(inStream);
                  bufferedOutputStream = new BufferedOutputStream(
                          new FileOutputStream(toFile, false));
                  //IO操作
                  int len = 0;
                  byte[] buff = new byte[2 * 1024];
                  while ((len = bufferedInputStream.read(buff)) != -1){
                      bufferedOutputStream.write(buff, 0, len);
                  }
                  bufferedOutputStream.flush();
              }catch(IOException e){
                  //TODO:handle exception
                  throw  e;
              }finally {
                  //IO关闭
                  bufferedOutputStream.close();
                  bufferedInputStream.close();
                  inStream.close();
                  LogoUtil.d("AssetsDBManager", "copyAssetsFileToFile end");
              }
          }
      }
3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
