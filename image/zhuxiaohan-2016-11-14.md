 #2016-11-14工作日志
==============================================
1. 完成工作
2. 已完成工作
 * public class BasePagerAdapter extends PagerAdapter {

    protected Context context;
    private ArrayList<View> viewList = new ArrayList<View>();
    private ArrayList<String> tabtitleList = new ArrayList<String>();

    public BasePagerAdapter(Context context) {
        this.context = context;
    }

    public ArrayList<View> getViewList() {
        return viewList;
    }

    public void addViewToAdapter(View view) {
        viewList.add(view);
    }

    public void addTabToAdapter(String title) {
        tabtitleList.add(title);
    }

    @Override
    public CharSequence getPageTitle(int position) {
        return tabtitleList.get(position);
    }

    @Override
    public void destroyItem(ViewGroup container, int position, Object object) {
        View view = viewList.get(position);
        container.removeView(view);
    }

    @Override
    public Object instantiateItem(ViewGroup container, int position) {
        View view = viewList.get(position);
        container.addView(view);
        return view;
    }

    @Override
    public int getCount() {
        return viewList.size();
    }

    @Override
    public boolean isViewFromObject(View arg0, Object arg1) {
        return arg0 == arg1;
    }
}

3. 未完成工作
4. 未完成工作原因
5. 遇到问题及决绝方案
