# 2016-9-21工作日志
========================
1. 应完成工作
* 掌握多态的优势和应用场合
  掌握父类和子类之间的类型转换
  理解里氏替换原则（LSP）
  掌握instanceof运算符的使用
  
* 打印机
* 需求说明：
  在前面汽车租赁系统的基础上，实现计算多种车辆总租金的功能
  现在有客户租用：
  2辆宝马
  1辆别克商务舱
  1辆金龙（34）座
  租5天共多少租金？



2. 已完成工作
   * 里氏替换原则和多态
   * 里氏替换原则（LSP）
   * 在一个软件系统中，子类对象可以替换所有使用的父类对象，且程序行为没有变化
  
  * 测试instanceof运算符的使用。

    public class TestPoly2 {
    
    public static void main(String[] args) {
    
    // Pet pet = new Penguin("楠楠", "Q妹");
    
    Pet pet = new Dog("欧欧", "雪娜瑞");
    
    pet.eat();
    if (pet instanceof Dog) {
    
    Dog dog = (Dog) pet;
    dog.catchingFlyDisc();
    }
    
    else if (pet instanceof Penguin) {
    Penguin pgn = (Penguin) pet;
    
    pgn.swimming();
  }
 * 打印机
 
   abstract class Printer(){
   
   void print(String str);
  
   }
   class ColorPrinter (){
   
    void print(String str) {
    
    System.out.println("输出彩色的"+str);
    }
}
    class BlackPrinter (){
    
    void print(String str) {
    
    System.out.println("输出黑白的"+str);
    }
}
    public static void main(String[] args) {
    
    Printer p = new ColorPrinter();
    
    p.print();
    
    p = new BlackPrinter();
    
    p.print();
}
* 在前面汽车租赁系统的基础上，实现计算多种车辆总租金的功能
  现在有客户租用：
  MotoVehile[] motos = new MotoVehile[4];
  
  motos[0] = new Car("宝马550i","京NY28588");
  
  motos[1] = new Car("宝马550i","京NNN328");
  
  motos[2] = new Car("别克林荫大道","京NY28588");
  
  motos[3] = new Bus("金龙",34);
  
  CalcTotalRent(MotoVehile[] motos){
  
    double totalRent = 0.0D; 
    
    for(int i=0;i<motos.length;++i){
    
        totalRent += motos[i].CalRent(5);
    } 
    return totalRent;
 }

* 面向对象的三大特性
* 封装：隐藏内部实现，稳定外部接口  

* 继承：子类继承父类成员，实现代码复用    

* 多态：不同子类对同一个消息作出不同的反映   

* 什么是接口
接口有比抽象类更好的特性：
1.可以被多继承
2.设计和实现完全分离
3.更自然的使用多态
4.更容易搭建程序框架
5.更容易更换实现
 …… 



3. 未完成工作

4. 未完成原因

5. 工作成功


6. 遇到的问题及解决方法
