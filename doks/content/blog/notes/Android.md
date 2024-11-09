## Activity
gradle build --build-cache --configuration-cache --parallel

```java
public class FirstActivity extends AppCompatActivity {  
    @Override  
    protected void onCreate(Bundle savedInstanceState){  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.first_layout); // 加载布局
    }  
}
```
继承自Activity, 覆写方法；

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <Button
        android:id="@+id/button_1"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:text="Hello World">
    </Button>
</androidx.constraintlayout.widget.ConstraintLayout>
```
android:id - 定义唯一标识符：
- @+id/button_1 : 在xml中定义一个资源
- @id:/button_1 : 在xml引用资源
在AndroidMainifest文件中注册
### Tosat
