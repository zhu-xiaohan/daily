# 2016-9-26工作日志
========================

 1. 应完成工作
 * 常用类
 
 *  定义:Random类中实现的随机算法是伪随机，也就是有规则的随机，它可以产生int、long、float、double等类型的随机数。
   作用：生成随机数
   Random对象的生成
   public  random():该构造方法使用一个和当前系统时间对应的相对时间有Math类表示的是数学的计算操作。
   public random(long seed):该构造方法可以通过制定一个种子数进行创建。
   
 * Math类表示的是数学的计算操作。
   Math的方法介绍
   Math.abs(double d):  求绝对值
   Math.ceil(double d)：返回不小于参数的最小整数
   Math.random():返回一个大于或者等于0.0小于不等于1.0的随机数 
   Math.sqrt(int i)：计算参数的平方根
  
  * String和StringBuffer
  
  * 掌握基本数据类型用法
    掌握String的基本用法
    会使用==和equals()比较字符串
    会使用StringBuffer类方法对字符串进行操作
    StringBuilder和StringBuffer的区别




 
 2. 已完成工作
  * 注册
     *  public class zhuce {
        public static void main(String[] arge){
        Scanner input =new Scanner(System.in);
        String uname,pwd;
        System.out.println("请输入用户名");
        uname=input.next();
        System.out.println("请输入密码");
        uname=input.next();
        System.out.println("请再次输入密码");
        //if (name.length() )
        pwd= input.next();
        if(uname.equals("")&& pwd.equals("1234567")){
            System.out.println("登录成功");


        }
        else{
            System.out.println("注册成功！");

        }

      }
      }
  * java中垃圾回收
  * public static long round(double d):四舍五入
   public class DemoMath{
      public static void main(String [] args){
		System.out.println(Math.round(123.356));
  	}
   }  
   * public class Test {
	private static Test test=null;
	private int num;
	public void method(){
		System.out.println("测试。。。");}	
	public static void main(String[] args) throws InterruptedException 	{
		new Test();//对象进入去活状态
		System.gc();
		Thread.sleep(2000);
		test.method();}
	@Override
	protected void finalize() throws Throwable {
		//当系统来清理资源时，让test引用到该对象，复活
		test=this;}}
    
![2](Random.png)
* 字符串常用提取方法
* //检查Java文件名
    int index = fileName.lastIndexOf(".");
    if(index!=-1 && index!=0 && 
          fileName.substring(index+1, fileName.length()).equals("java")){   
	 fileCorrect = true;
     }else{
	System.out.println("文件名无效.");
     }
//检查你的邮箱格式
    if (email.indexOf('@') !=- 1 && email.indexOf('.')  > 
    email.indexOf('@')){
	 emailCorrect = true;
    }else{
  System.out.println("Email无效。");}
*![3](符串拆分.png)
* public class Lyric {
    	public static void main(String[] args) {
        String words="长亭外 古道边 芳草碧连天 晚风扶 柳
		   笛声残 夕阳山外山";
        String[] printword=new String[100];		
        System.out.println("***原歌词格式***\n"+words);
        System.out.println("\n***拆分后歌词格式***");
        printword=words.split(" "); 
		   for(int i=0;i<printword.length;i++){
        		System.out.println( printword[i] );}	}}


 3. 未完成工作
 4. 未完成原因
 5. 工作成功
 6. 遇到的问题和解决方法
 ![1](时间错误.png)
 * 没解决
 * ![2](Random.png)
