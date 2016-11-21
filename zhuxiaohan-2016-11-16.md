 # 2016-11-16工作日报
==================
1. 应完成工作
2. 工作内容
      * public class MainActivity extends AppCompatActivity {

    private static final String TAG = "MainActivity";
    private List<View> list = new ArrayList<View>();
    private List<String> listTitle = new ArrayList<String>();

    private ViewPager viewPager;
    private PagerAdapter pagerAdapter = new PagerAdapter() {

        @Override
        public int getCount() {
            return list.size();
        }

        @Override
        public boolean isViewFromObject(View view, Object object) {
            return view == object;
        }

        @Override
        public Object instantiateItem(ViewGroup container, int position) {
            View view = list.get(position);
            container.addView(view);
            return view;
            // return super.instantiateItem(container, position);
        }

        @Override
        public void destroyItem(ViewGroup container, int position, Object object) {
            //super.destroyItem(container, position, object);
            View view = list.get(position);
            container.removeView(view);
        }

        @Override
        public CharSequence getPageTitle(int position) {
            return listTitle.get(position);
        }
    };
    private ViewPager.OnPageChangeListener listener = new ViewPager.OnPageChangeListener() {

        // 此方法是在页面滑动的时候调用
        // arg0:当前页面，及你点击滑动的页面
        // arg1:当前页面偏移的百分比
        // arg2:当前页面偏移的像素位置

        @Override
        public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {
            Log.d(TAG, "onPageScrolled() called with: position(当前页面，及你点击滑动的页面) = [" + position + "], positionOffset(当前页面偏移的百分比) = [" + positionOffset + "], positionOffsetPixels(当前页面偏移的像素位置) = [" + positionOffsetPixels + "]");
        }

        // 此方法是页面跳转完成后得到调用
        // arg0:当前选中的页面的position(位置编号)
        @Override
        public void onPageSelected(int position) {
            Log.d(TAG, "onPageSelected() called with: position(当前选中的页面的position(位置编号)) = [" + position + "]");
        }

        // 此方法是在状态改变的时候调用
        // arg0==1的时候表示正在滑动
        // arg0==2的时候表示滑动完毕了
        // arg0==0的时候表示什么都没做
        @Override
        public void onPageScrollStateChanged(int state) {

            String str = "";
            switch (state) {
                case 1:
                    str = "1的时候表示正在滑动";
                    break;
                case 2:
                    str = "2的时候表示滑动完毕了";
                    break;
                case 3:
                    str = "0的时候表示什么都没做";
                    break;
            }
            Log.d(TAG, "onPageScrollStateChanged() called with: state = [" + state + "]" + str);
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        viewPager = (ViewPager) findViewById(R.id.main_viewpager);

        View view1 = new LinearLayout(this);
        view1.setBackgroundColor(Color.RED);

        View view2 = new LinearLayout(this);
        view2.setBackgroundColor(Color.YELLOW);

        View view3 = new LinearLayout(this);
        view3.setBackgroundColor(Color.GREEN);

        list.add(view1);
        list.add(view2);
        list.add(view3);

        listTitle.add("红色");
        listTitle.add("黄色");
        listTitle.add("绿色");

        viewPager.setAdapter(pagerAdapter);

        viewPager.addOnPageChangeListener(listener);
    }
}

3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
