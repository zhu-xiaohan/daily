2016-10-12
====================================
1.应完成工作
 *  计算器页面
 *  日报登录页面


2.已完成工作
 *   <?xml version="1.0" encoding="utf-8"?>
     <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
     android:orientation="vertical" android:layout_width="match_parent"
     android:layout_height="match_parent">

       <Button
        android:text="text1"
        android:layout_width="match_parent"
        android:layout_height="200dp"
        android:id="@+id/button" />

        <Button
        android:id="@+id/b2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="+/-"
        android:layout_alignParentBottom="true"
         />
        <Button
        android:id="@+id/b3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="0"
        android:layout_alignParentBottom="true"
        android:layout_toRightOf="@id/b2"
        />
        <Button
        android:id="@+id/b4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="."
        android:layout_alignParentBottom="true"
        android:layout_toRightOf="@id/b3"
        />
        <Button
        android:id="@+id/b5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="="
        android:layout_alignParentBottom="true"
        android:layout_toRightOf="@id/b4"
        />
       <Button
        android:id="@+id/b6"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="1"
        android:layout_above="@+id/b2"

        />
        <Button
        android:id="@+id/b7"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="2"
        android:layout_toRightOf="@id/b6"
        android:layout_above="@id/b3"/>
        <Button
        android:id="@+id/b8"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="3"
        android:layout_toRightOf="@id/b7"
        android:layout_above="@id/b3"/>
        <Button
        android:id="@+id/b9"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="+"
        android:layout_toRightOf="@id/b8"
        android:layout_above="@id/b5"/>
        <Button
        android:id="@+id/b10"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="4"

        android:layout_above="@id/b6"/>
        <Button
        android:id="@+id/b11"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="5"
        android:layout_toRightOf="@id/b6"
        android:layout_above="@id/b9"/>
        <Button
        android:id="@+id/b12"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="6"
        android:layout_toRightOf="@id/b11"
        android:layout_above="@id/b9"/>

        <Button
        android:id="@+id/b13"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="-"
        android:layout_toRightOf="@id/b12"
        android:layout_above="@id/b9"/>
        <Button
        android:id="@+id/b14"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="7"

        android:layout_above="@id/b10"/>
        <Button
        android:id="@+id/b15"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="8"
        android:layout_toRightOf="@id/b14"
        android:layout_above="@id/b11"/>
        <Button
        android:id="@+id/b16"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="9"
        android:layout_toRightOf="@id/b15"
        android:layout_above="@id/b11"/>
        <Button
        android:id="@+id/b17"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="*"
        android:layout_toRightOf="@id/b16"
        android:layout_above="@id/b11"/>

        <Button
        android:id="@+id/b18"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="ce"

        android:layout_above="@id/b14"/>
       <Button
        android:id="@+id/b19"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="c"
        android:layout_toRightOf="@id/b18"
        android:layout_above="@id/b15"/>
        <Button
        android:id="@+id/b20"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="delete"
        android:layout_toRightOf="@id/b15"
        android:layout_above="@id/b16"/>
        <Button
        android:id="@+id/b21"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="/"
        android:layout_toRightOf="@id/b16"
        android:layout_above="@id/b17"/>

        </RelativeLayout>
    * ![1](jisuanqi02.png)
    
    
===================================================================   
 *   <?xml version="1.0" encoding="utf-8"?>
     <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
     android:orientation="vertical" android:layout_width="match_parent"
     android:layout_height="match_parent">

        <Button
        android:text="Button"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/button" />
        <Button
        android:id="@+id/button1"
        android:text="登录"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"/>
        <Button
        android:id="@+id/button3"
        android:text="注册"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:layout_toRightOf="@id/button1"
        android:layout_alignParentBottom="true" />
        <TextView
        android:text="用户注册：______________________________________"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/button"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:layout_marginLeft="38dp"
        android:layout_marginStart="38dp"
        android:layout_marginTop="50dp"
        android:id="@+id/textView" />
        <TextView
        android:text="         密码:_______________________________________"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/textView"
        android:layout_alignLeft="@+id/textView"
        android:layout_alignStart="@+id/textView"
        android:layout_marginTop="87dp"
        android:id="@+id/textView2" />
        <CheckBox
        android:text="记住密码"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/textView2"
        android:layout_alignLeft="@+id/textView2"
        android:layout_alignStart="@+id/textView2"
        android:layout_marginTop="56dp"
        android:id="@+id/checkBox" />
        <TextView
        android:text="忘记密码"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/textView3"
        android:layout_alignBaseline="@+id/checkBox"
        android:layout_alignBottom="@+id/checkBox"
        android:layout_toRightOf="@+id/button1"
        android:layout_toEndOf="@+id/button1" />
        </RelativeLayout>
    * ![2](denglu01.png)
    
        
        
3.未完成
 *    
4.未完成原因
 *    
5.工作成功
 *    
6.遇到的问题和解决方案
