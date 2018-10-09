Android_安卓为按钮控件绑定事件的五种方式
一、写在最前面
　　　　本次，来介绍一下安卓中为控件--Button绑定事件的五种方式。
二、具体的实现
　　　　第一种：直接绑定在Button控件上：
　　　　　　　　步骤1.在Button控件上设置android:onClick="，其中这个属性的属性值对应的是MainActivity类中的方法名字（自己创建的方法）：
　　　　　　　　　　　　 
　　　　　　　　 步骤2.在MainActivity类中创建相对应的方法：
    public void demo(View view){
            Toast.makeText(MainActivity.this, "第二个按钮被点击了",Toast.LENGTH_SHORT).show();
    }

  　　　　

　　　　 第二种：使用匿名内部类的方式：
　　　　　　　　　步骤1.首先需要获取到 layout 中布局页面的Button控件中指定的Id：
　　　　　　　　　步骤2.之后为这样按钮绑定监听器，使用匿名内部类的方式，代码如下：

 　　　　button = (Button)findViewById(R.id.button1);
        button.setOnClickListener(new OnClickListener() {

            @Override
            public void onClick(View view) {

                    Toast.makeText(MainActivity.this, "通过匿名内部类：第一个按钮被点击了",Toast.LENGTH_SHORT).show();

            }
        });


　　　　　　　
　　　　　
　　　　　第三种：使用外部类的方式
　　　　　　　　　　步骤1.需要获取到 layout 布局页面中的Button控件中指定的Id（在MainActivity中）：　
           　　　　　　　　
　　　　　　　　　　步骤2.创建一个类，并且实现 OnClickListener 接口，重写这个接口中的 OnClick 方法，并且为这个方法创建一个 Context 属性（之后的Toast需要使用到），使用构造器设置这个属性值：

package com.mqz.android_event_test;

import android.content.Context;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Toast;

public class BtnTest implements OnClickListener {

    private Context context;
    public BtnTest(Context context){
        this.context=context;
    }

    @Override
    public void onClick(View view) {

            Toast.makeText(context, "通过外部类实现OnClickListener接口：第一个按钮被点击了",Toast.LENGTH_SHORT).show();


    }


}


　　　　　　　　　　步骤3.为获取到的按钮绑定事件，并且把当前对象传入
　　　　　　　　　　　　　

　　　　　
 　　　　  第四种：使用MainActivity直接实现OnClickListener接口的方式
　　　　　　　　　　步骤1.在 MainActivity 中实现 OnClickListener 接口，并且重写 OnClick 方法：
　　　　　　　　　　步骤2.绑定button按钮相对应的监听，把当前对象传入：
　　　　　　　　
　　　　　　　　  特点：
            　　　　         1.这样是的MainActivity类成为了监听器类，这样的方式十分简洁
            　　　　         2.但是这样容易引起结构的混乱，因为MainActivity类主要职责来初始化界面的，这加入了事件处理器的方法，引起混乱。
 　　　　                    3.界面类需要实现监听器的方法，有点不伦不类。    　　
　　　　　　　　　　

package com.mqz.android_event_test;

import android.app.Activity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.Toast;


public class MainActivity extends Activity implements OnClickListener{


    private Button button;


    @Override
    public void onClick(View view) {


            Toast.makeText(MainActivity.this, "通过MainActivity实现OnClickListener接口：第一个按钮被点击了",Toast.LENGTH_SHORT).show();

    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button = (Button)findViewById(R.id.button2);
        button.setOnClickListener(this);

    }

}


　　　　
 　　　　　第五种：使用成员内部类的方式来实现button按钮事件的绑定
　　　　　　　　　步骤1.获取 layout 布局文件中的Button控件的 Id：
　　　　　　　　　　　　　　
　　　　　　　　　步骤2.在 MainActivity 类中创建一个成员内部类，并且实现 OnClickListener 接口，重写 OnClick 方法：
　　　　　　　　　

class BtnTest1 implements OnClickListener{
        @Override
        public void onClick(View view) {

                Toast.makeText(MainActivity.this, "通过成员内部类：第二个按钮被点击了",Toast.LENGTH_SHORT).show();

        }

    }

　　　　　　　　   步骤3、在这个按钮中绑定相关的事件，new 内部类()即可，不需要传入上下文对象，因为这个类是当前类的内部类：
　　　　　                 　
　　　　　　　　　好处：
               　　　　　　    1.成员内部监听器的方式可以访问外部类的中的所有属性，所以在new OnClickListener实现类 对象的时候不需要传入当前对象
             　　　　　　      2.成员内部监听器可以让外部类重复使用，因为成员内部监听器是外部类的内部类　
