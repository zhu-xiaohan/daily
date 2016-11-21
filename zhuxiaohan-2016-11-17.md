 # 2016-11-17工作日报
==================
1. 应完成工作
2. 工作内容
      * public class ClearArcView extends View {

    private final int START_ANGLE = -90;
    private Paint paint = new Paint();
    private RectF oval;
    private int sweepAngle = 0;
    private int state = 0; // 0: 回退 ；1:前进
    private int arcColor = 0xFFFF8C00;
    private int[] back = new int[]{-6, -6, -10, -10, -10, -12};
    private int backIndex;
    private int[] goon = new int[]{12, 12, 12, 12, 10, 10, 10, 8, 8, 8,
            6};
    private int goonIndex;
    private boolean isRuning = false;


    public ClearArcView(Context context) {
        super(context);
    }

    public ClearArcView(Context context, AttributeSet attrs) {
        super(context, attrs);

        //设置初始扫描角度
        setAngle(360);

        //获取一键清理圆环颜色
        arcColor = context.getResources().getColor(R.color.clear_arc_color);
    }

    public ClearArcView(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    private void setAngle(int angle) {
        sweepAngle = angle;

        // invalidate();
        postInvalidate();

        isRuning = false;
    }

    public void setAngleWithAnim(final int angle) {

        if (isRuning) {
            return;
        }

        isRuning = true;
        state = 0; // 回退
        final Timer timer = new Timer();
        final TimerTask timerTask = new TimerTask() {

            @Override
            public void run() {
                switch (state) {
                    case 0:
                        sweepAngle += back[backIndex++];
                        if (backIndex >= back.length) {
                            backIndex = back.length - 1;
                        }
                        postInvalidate();
                        if (sweepAngle <= 0) {
                            sweepAngle = 0;
                            state = 1;
                            backIndex = 0;
                        }
                        break;
                    case 1:
                        sweepAngle += goon[goonIndex++];
                        if (goonIndex >= goon.length) {
                            goonIndex = goon.length - 1;
                        }
                        postInvalidate();
                        if (sweepAngle >= angle) {
                            sweepAngle = angle;
                            timer.cancel();
                            goonIndex = 0;
                            isRuning = false;
                        }
                        break;
                }
            }
        };

        timer.schedule(timerTask, 24, 24);
    }

    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {

        //根据父控件传入的宽高规范，获取设定的控件的宽高
        int viewWidth = MeasureSpec.getSize(widthMeasureSpec);
        int viewHeight = MeasureSpec.getSize(heightMeasureSpec);
        oval = new RectF(0, 0, viewWidth, viewHeight); // 旋转圆形大小
        setMeasuredDimension(viewWidth, viewHeight);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        // super.onDraw(canvas);

        paint.setColor(arcColor);
        paint.setAntiAlias(true);
        canvas.drawArc(oval, START_ANGLE, sweepAngle, true, paint);

    }
}
3. 未完成工作
4. 未完成原因
5. 遇到问题及解析
