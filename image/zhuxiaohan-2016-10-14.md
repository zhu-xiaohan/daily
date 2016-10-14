2016-10-14
================================
1.应完成工作
  *  日报查看 新增 退出
2.已完成工作
 * package com.feicuiedu;

   import com.feicuiedu.daily.controller.UserController;
   import com.feicuiedu.daily.uitl.DBUtils;
   import daily.control.chakan;

   import java.util.List;
   import java.util.Map;
   import java.util.Scanner;

   /**
    * Created by chenyan on 2016/10/10.
    */
   public class Main {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        UserController userController = new UserController(scanner);

        String filePath = "D:\\develop\\java_demoribao\\daily\\src\\main\\resources";

        String fileName = "welcome.txt";

        userController.showSelectItem(filePath, fileName);

        int selected = userController.selectedItem();

        boolean loginResult = false;

        if (1 == selected) {

            // 登录
            loginResult = userController.login();

        } else {

            // 注册
            userController.register();
        }

        // 登录成功后的操作
        if (loginResult) {

            fileName = "operate_item.txt";

            userController.showSelectItem(filePath, fileName);

            selected = userController.selectedItem();


        } else {

        }

        switch (selected) {
            case 1:
                // 查看日报
                String srcSql = "select birthday from User order by id";
                List<Map<String, Object>> lstMap;
               new chakan().chakan();
                break;

            case 2:

                // 新增日报

               /* String srcSql = "insert User values (@name,@sex,@birthday,@passwd,@id)";
                DBUtils.modifyTable(srcSql);*/


                break;

            case 3:

                // 退出
                System.exit(-1);
                break;


            default:
                System.out.println("系统错误");
                System.exit(-1);
          }
      }
   }


     package daily.control;

     //import daily.util.DBUtils;

     import java.util.ArrayList;
     import java.util.List;
     import java.util.Map;
     import java.util.Scanner;

     /**
     * Created by  on 2016/10/12.
     */
     public class chakan {

     // 查询日志
     public  void chakan() {

        String sql = "select * from user_ ";
        List<Map<String,Object>> list = com.feicuiedu.daily.uitl.DBUtils.queryTable(sql);




        System.out.println("日报明细：");
        System.out.println("id      name");
        for (Map<String, Object> map : list) {

            for (Map.Entry<String, Object> entry : map.entrySet()) {
                String key = entry.getKey();
                Object value = entry.getValue();

                System.out.print(value + "      ");
            }
            System.out.println();
        }

        System.out.println("选择下一步: (1 : 继续     2: 退出 )");
        Scanner sc = new Scanner(System.in);
        int input = sc.nextInt();

        if (input == 1) {

            Confirmed.confirmed();
        } else {
            System.exit(-1);
        }
       }
  

    }


3.未完成工作



4.未完成工作原因


5.工作成功


6.遇到的问题和解决原因
