  # 2016-11-15工作日志
============================
 1. 应完成工作
 2. 已完成工作
  * public class LeadActivity extends AppCompatActivity {

    private ImageView[] icons = new ImageView[3];
    private TextView tv_skip;
    private ViewPager viewPager;
    private BasePagerAdapter leadPagerAdapter;
    private ViewPager.OnPageChangeListener pageChangeListener = new ViewPager.OnPageChangeListener() {
        @Override
        public void onPageSelected(int arg0) {
            // 到达最后一个page时，显示出skip文本
            tv_skip.setVisibility(View.INVISIBLE);
            if (arg0 >= 2) {
                tv_skip.setVisibility(View.VISIBLE);
            }
            // 更新下标图标
            for (int i = 0; i < icons.length; i++) {
                icons[i].setImageResource(R.drawable.adware_style_default);
            }
            icons[arg0].setImageResource(R.drawable.adware_style_selected);
        }

        @Override
        public void onPageScrolled(int arg0, float arg1, int arg2) {
        }

        @Override
        public void onPageScrollStateChanged(int arg0) {
        }
    };

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.lead_activity);
        initLeadIcon();
        initViewPager();
        initPagerData();
    }

    private void initLeadIcon() {
        icons[0] = (ImageView) findViewById(R.id.icon1);
        icons[1] = (ImageView) findViewById(R.id.icon2);
        icons[2] = (ImageView) findViewById(R.id.icon3);
        icons[0].setImageResource(R.drawable.adware_style_selected);
        tv_skip = (TextView) findViewById(R.id.tv_skip);
        tv_skip.setVisibility(View.INVISIBLE);
        //tv_skip.setOnClickListener(this);
    }

    /**
     * 初始化ViewPager
     */
    private void initViewPager() {
        viewPager = (ViewPager) findViewById(R.id.viewpager);
        leadPagerAdapter = new BasePagerAdapter(this);
        viewPager.setAdapter(leadPagerAdapter);
        // viewPager.setOnPageChangeListener(pageChangeListener);
    }

    /**
     * 初始化页面信息
     */
    private void initPagerData() {
        ImageView imageView = null;
        imageView = (ImageView) getLayoutInflater().inflate(R.layout.activity_lead_item, null);
        imageView.setImageResource(R.drawable.adware_style_applist);
        leadPagerAdapter.addViewToAdapter(imageView);
        imageView = (ImageView) getLayoutInflater().inflate(R.layout.activity_lead_item, null);
        imageView.setImageResource(R.drawable.adware_style_banner);
        leadPagerAdapter.addViewToAdapter(imageView);
        imageView = (ImageView) getLayoutInflater().inflate(R.layout.activity_lead_item, null);
        imageView.setImageResource(R.drawable.adware_style_creditswall);
        leadPagerAdapter.addViewToAdapter(imageView);
        leadPagerAdapter.notifyDataSetChanged();
    }
}

 3. 未完成工作
 4. 未完成工作原因
 5. 遇到问题及解决方案
