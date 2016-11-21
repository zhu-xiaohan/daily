 # 2016-11-18工作日报
==================
1. 应完成工作
2. 工作内容
      * public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout_homescore);
        TextView tv_score = (TextView) findViewById(R.id.tv_score);
        ClearArcView cav = (ClearArcView) findViewById(R.id.homeclear_arc);
        cav.setAngleWithAnim(100);
        tv_score.setText("100");
    }
}
3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
