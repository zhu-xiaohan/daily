#2016-10-17
============

* 应完成工作

  新版工作日报 的生成
  
  public class Main {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        UserControl userControl = new UserControl();

        String userId = null;
        while (true) {
            System.out.println("翡翠欢迎你");
            System.out.println("请选择你的操作");
            System.out.println("1:登录");
            System.out.println("2:注册");

            int selected = scanner.nextInt();

            if (selected == 1) {
                Map<String, String> resultMap = userControl.showLogin();

                String result = resultMap.get("result");

                if (result.equals("success")) {
                    userId = resultMap.get("userId");
                    break;
                }
                else {
                    System.out.println("登录失败");
                }

            }
            else if (selected == 2){
                userControl.showRegister();
            }
            else {
                System.out.println("这就是乱输入的代价！！！");
                System.exit(0);
            }
        }

        if (userId != null ) {

            DailyControl dailyControl = new DailyControl();

            do {
                System.out.println("请选择你的操作");
                System.out.println("1:查看当前日报");
                System.out.println("2:新增日报");

                int selected = scanner.nextInt();

                if (selected == 1) {
                   dailyControl.showDaliyByUser(userId);


                } else
                    if (selected == 2) {
                        dailyControl.writeDaily(userId);
                    } else {
                        System.out.println("这就是乱输入的代价！！！");
                        System.exit(0);
                    }
            }while (true);
        }
    }
}

public class DailyControl {

    public void showDaliyByUser(String userId) {

        DailyService dailyService = new DailyService();

        Map<String,Object> resultMap = dailyService.showDailyByUser(userId);

        for (Daily daily:(List<Daily>)resultMap.get("list")) {
            System.out.println(daily);
        }

    }

    public void writeDaily(String userId) {

        DailyService dailyService = new DailyService();

        Scanner scanner = new Scanner(System.in);

        do {
            System.out.println("请输入日报名称:");
            String name = scanner.next();

            System.out.println("应完成工作:");
            String shouldFinishedWork = scanner.next();

            System.out.println("已完成工作:");
            String haveFinishedWork = scanner.next();

            System.out.println("未完成原因:");
            String unFinishedWorkReason = scanner.next();

            System.out.println("遇到问题&解决方案:");
            String questionAndAnswer = scanner.next();

            System.out.println("明日计划:");
            String nextDayPlan = scanner.next();

            Map<String,String> resultMap = dailyService.wirteDaily(name,
                    userId,
                    shouldFinishedWork,
                    haveFinishedWork,
                    unFinishedWorkReason,
                    questionAndAnswer,
                    nextDayPlan);

            String result = resultMap.get("result");

            if (result.equals("success")) {
                showDaliyByUser(userId);
            }
            else {
                break;
            }
        } while (true);
    }
}

public class UserControl {

    public Map<String,String> showLogin() {

        UserService userService = new UserService();

        Scanner scanner = new Scanner(System.in);

        System.out.println("请输入登录账号:");
        String loginName = scanner.next();
        System.out.println("请输入登录密码:");
        String password = scanner.next();

        Map<String,String> resultMap = userService.login(loginName,password);

       /* String result = resultMap.get("result");
        String userId = null;
        if (result.equals("success")) {
            userId = resultMap.get("userId");
        }*/
        return resultMap;
    }

    public void showRegister() {

        UserService userService = new UserService();

        Scanner scanner = new Scanner(System.in);

        do {
            System.out.println("请输入登录账号:");
            String loginName = scanner.next();

            System.out.println("请输入登录密码:");
            String password = scanner.next();

            System.out.println("请输入确认密码:");
            String rePassword = scanner.next();

            System.out.println("请输入姓名:");
            String name = scanner.next();

            System.out.println("请输入出生日期(yyyy-MM-dd):");
            String strBirthday = scanner.next();

            System.out.println("请输入性别(0:女，1:男):");
            String sex = scanner.next();

            System.out.println("请输入个人描述:");
            String description = scanner.next();

            Date birthday = Date.valueOf(strBirthday);

            if (password.equals(rePassword)) {
                userService.register(
                        name,
                        sex,
                        birthday,
                        loginName,
                        password,
                        description
                );

                break;
            }
        } while (true);
    }
}

public class DailyDao {

    // 新增一笔user_资料

    public void saveDaily(Daily daily) throws
            SQLException,
            IOException,
            ClassNotFoundException {


        StringBuilder sql = new StringBuilder();
        sql.append(" insert into ");
        sql.append("    daily_ ");
        sql.append("        (id,name,create_time,create_id,should_finished_work,");
        sql.append("         have_finished_work,unfinished_work_reason,question_and_answer,");
        sql.append("         next_day_plan)  ");
        sql.append("    values");
        sql.append("         ('" + daily.getId() + "','" + daily.getName() + "',");
        sql.append("          '" + daily.getCreateTime() + "','" + daily.getCreateId() + "',");
        sql.append("          '" + daily.getShouldFinishedWork() + "',");
        sql.append("          '" + daily.gethaveFinishedWork() + "',");
        sql.append("          '" + daily.getunFinishedWorkReason() + "',");
        sql.append("          '" + daily.getQuestionAndAnswer() +"',");
        sql.append("          '" + daily.getNextDayPlan() + "')");

        DBUtils.modifyTable(sql.toString());
    }

    // 根据条件 返回user资料集合
    public List<Daily> getDailyByCondition(Daily daily) {

        StringBuilder sb = new StringBuilder();
        sb.append(" select ");
        sb.append("     * ");
        sb.append(" from ");
        sb.append("     daily_ ");
        sb.append(" where 1=1 ");

        if (daily.getId() != null) {

            sb.append(" and    id = '" + daily.getId()+ "'");
        }

        if (daily.getName() != null) {

            sb.append(" and  name = '" + daily.getName()+ "'");
        }

        if (daily.getCreateTime() != null) {

            sb.append(" and  create_time = '" + daily.getCreateTime()+ "'");
        }

        if (daily.getCreateId() != null) {

            sb.append(" and  create_id = '" + daily.getCreateId()+ "'");
        }

        if (daily.getShouldFinishedWork() != null) {

            sb.append(" and  should_finished_work = '" + daily.getShouldFinishedWork()+ "'");
        }

        if (daily.gethaveFinishedWork() != null) {

            sb.append(" and  have_finished_work = '" + daily.gethaveFinishedWork()+ "'");
        }

        if (daily.getunFinishedWorkReason() != null) {

            sb.append(" and  unfinished_work_reason = '" + daily.getunFinishedWorkReason()+ "'");
        }

        if (daily.getQuestionAndAnswer() != null) {

            sb.append(" and  question_and_answer = '" + daily.getQuestionAndAnswer()+ "'");
        }

        if (daily.getNextDayPlan() != null) {

            sb.append(" and  next_day_plan = '" + daily.getNextDayPlan()+ "'");
        }
        sb.append(" order by create_time desc ");

        System.out.println(sb.toString());
        List<Daily> listDaily = new ArrayList<Daily>();

        List<Map<String, Object>> list = DBUtils.queryTable(sb.toString());

        for (Map<String, Object> map : list) {

            Long id = (Long) map.get("id");
            String name = (String) map.get("name");
            Timestamp createTime = (Timestamp) map.get("create_time");
            Long createId = (Long) map.get("create_id");
            String shouldFinishedWork = (String) map.get("should_finished_work");
            String haveFinishedWork = (String) map.get("have_finished_work");
            String unfinishedWorkReason = (String) map.get("unfinished_work_reason");
            String questionAndAnswer = (String) map.get("question_and_answer");
            String nextDayPlan = (String) map.get("next_day_plan");


            Daily tmpDaily = new Daily();

            tmpDaily.setId(new BigInteger(id + ""));
            tmpDaily.setName(name);

            tmpDaily.setCreateTime(createTime);
            tmpDaily.setCreateId(new BigInteger(createId + ""));

            tmpDaily.setShouldFinishedWork(shouldFinishedWork);
            tmpDaily.sethaveFinishedWork(haveFinishedWork);
            tmpDaily.setunFinishedWorkReason(unfinishedWorkReason);
            tmpDaily.setQuestionAndAnswer(questionAndAnswer);
            tmpDaily.setNextDayPlan(nextDayPlan);

            listDaily.add(tmpDaily);
        }

        return listDaily;
    }
}

public class UserDao {

    // 新增一笔user_资料

    public void saveUser(User user) throws
            SQLException,
            IOException,
            ClassNotFoundException {


        StringBuilder sql = new StringBuilder();
        sql.append(" insert into ");
        sql.append("    user_ ");
        sql.append("        (id,login_name,name,sex,birthday,password,description)  ");
        sql.append("    values");
        sql.append("         ('" + user.getId() + "','" + user.getLoginName() + "','" + user.getName() + "','" + user.getSex() + "',");
        sql.append("          '" + user.getBirthday() + "','" + user.getPassword() + "','" + user.getDescription() + "')");

        DBUtils.modifyTable(sql.toString());
    }

    // 根据条件 返回user资料集合
    public List<User> getUserByCondition(User user) {

        StringBuilder sb = new StringBuilder();
        sb.append(" select ");
        sb.append("     * ");
        sb.append(" from ");
        sb.append("     user_ ");
        sb.append(" where 1=1 ");

        if (user.getId() != null) {

            sb.append(" and    id = '" + user.getId() + "'");
        }

        if (user.getName() != null) {

            sb.append(" and  name = '" + user.getName() + "'");
        }

        if (user.getBirthday() != null) {

            sb.append(" and  birthday = '" + user.getBirthday()+ "'");
        }

        if (user.getSex() != null) {

            sb.append(" and  sex = '" + user.getSex()+ "'");
        }

        if (user.getLoginName() != null) {

            sb.append(" and  login_name = '" + user.getLoginName()+ "'");
        }

        if (user.getDescription() != null) {

            sb.append(" and  description = '" + user.getDescription()+ "'");
        }

        if (user.getPassword() != null) {

            sb.append(" and  password = '" + user.getPassword()+ "'");
        }

        System.out.println(sb.toString());
        List<User> listUser = new ArrayList<User>();

        List<Map<String, Object>> list = DBUtils.queryTable(sb.toString());

        for (Map<String, Object> map : list) {

            Long id = (Long) map.get("id");
            String name = (String) map.get("name");
            String loginName = (String) map.get("login_name");
            String sex = (String) map.get("sex");
            Date birthday = (Date) map.get("birthday");
            String password = (String) map.get("password");
            String description = (String) map.get("description");


            User tmpUser = new User();

            tmpUser.setId(new BigInteger(id + ""));
            tmpUser.setName(name);
            tmpUser.setLoginName(loginName);
            tmpUser.setSex(sex);
            tmpUser.setBirthday(birthday);
            tmpUser.setPassword(password);
            tmpUser.setDescription(description);
            listUser.add(tmpUser);
        }

        return listUser;
    }
}

public class DBConn {

    private static DBConn dbConn;

    private DBConn() {

    }

    public static DBConn getInstance() {

        if (dbConn == null) {
            dbConn = new DBConn();
        }

        return dbConn;
    }


    public Connection getConneciton() throws
            IOException,
            ClassNotFoundException,
            SQLException {

        Properties properties = new Properties();

        InputStream inputStream = DBConn.class.getResourceAsStream("/config.properties");
        Connection connection = null;

        properties.load(inputStream);
        String driver = properties.getProperty("driver");
        String url = properties.getProperty("url");
        String userName = properties.getProperty("userName");
        String userPassword = properties.getProperty("userPassword");


        Statement st = null;
        ResultSet rs = null;

        // 注册驱动
        Class.forName(driver);

        // 根据驱动获得连接
        connection = DriverManager.getConnection(url,
                userName,
                userPassword);


        return connection;
    }
}

public class DBUtils {

    // 新增，修改，删除的操作
    public static void modifyTable(String strSql) throws
            SQLException,
            IOException,
            ClassNotFoundException {
        Connection connection = null;

        connection = DBConn.getInstance().getConneciton();
        Statement st = null;
        st = connection.createStatement();
        st.executeUpdate(strSql);

    }

    // 查询的操作
    public static List<Map<String, Object>> queryTable(String strSql) {

        Connection connection = null;
        List<Map<String, Object>> lstResult = new ArrayList<Map<String, Object>>();
        try {
            connection = DBConn.getInstance()
                    .getConneciton();
            List<String> lstColumnNames = new ArrayList<String>();

            ResultSet rs = connection.createStatement()
                    .executeQuery(strSql);

            ResultSetMetaData rsm = rs.getMetaData();

            int colCount = rsm.getColumnCount();
            for (int i = 0; i < colCount; i++) {

                String columnName = rsm.getColumnName(i + 1);
                lstColumnNames.add(columnName.toLowerCase());
            }

            while (rs.next()) {

                LinkedHashMap<String, Object> resMap = new LinkedHashMap<String, Object>();
                for (String columnName : lstColumnNames) {
                    Object obj = rs.getObject(columnName);
                    resMap.put(columnName,
                            obj);
                }

                lstResult.add(resMap);
            }
        }
        catch (IOException e) {
            e.printStackTrace();
        }
        catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        catch (SQLException e) {
            e.printStackTrace();
        }


        return lstResult;
    }

}

public class Daily {

    // 日报主键
    private BigInteger id;

    // 日报名称
    private String name;

    // 日报的创建时间
    private Timestamp createTime;

    // 创建人
    private BigInteger createId;

    // 应完成工作
    private String shouldFinishedWork;

    // 已经完成工作
    private String haveFinishedWork;

    // 未完成工作原因
    private String unFinishedWorkReason;

    // 遇到问题和解决方案
    private String questionAndAnswer;

    // 明日计划
    private String nextDayPlan;

    public Daily() {

    }

    public Daily(String name,
                 String shouldFinishedWork,
                 String haveFinishedWork,
                 String unFinishedWorkReason,
                 String questionAndAnswer,
                 String nextDayPlan) {
        this.name = name;
        this.shouldFinishedWork = shouldFinishedWork;
        this.haveFinishedWork = haveFinishedWork;
        this.unFinishedWorkReason = unFinishedWorkReason;
        this.questionAndAnswer = questionAndAnswer;
        this.nextDayPlan = nextDayPlan;
    }

    public BigInteger getId() {
        return id;
    }

    public void setId(BigInteger id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Timestamp getCreateTime() {
        return createTime;
    }

    public void setCreateTime(Timestamp createTime) {
        this.createTime = createTime;
    }

    public BigInteger getCreateId() {
        return createId;
    }

    public void setCreateId(BigInteger createId) {
        this.createId = createId;
    }

    public String getShouldFinishedWork() {
        return shouldFinishedWork;
    }

    public void setShouldFinishedWork(String shouldFinishedWork) {
        this.shouldFinishedWork = shouldFinishedWork;
    }

    public String gethaveFinishedWork() {
        return haveFinishedWork;
    }

    public void sethaveFinishedWork(String haveFinishedWork) {
        this.haveFinishedWork = haveFinishedWork;
    }

    public String getunFinishedWorkReason() {
        return unFinishedWorkReason;
    }

    public void setunFinishedWorkReason(String unFinishedWorkReason) {
        this.unFinishedWorkReason = unFinishedWorkReason;
    }

    public String getQuestionAndAnswer() {
        return questionAndAnswer;
    }

    public void setQuestionAndAnswer(String questionAndAnswer) {
        this.questionAndAnswer = questionAndAnswer;
    }

    public String getNextDayPlan() {
        return nextDayPlan;
    }

    public void setNextDayPlan(String nextDayPlan) {
        this.nextDayPlan = nextDayPlan;
    }

    @Override
    public String toString() {
        return "Daily{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", createTime=" + createTime +
                ", createId=" + createId +
                ", shouldFinishedWork='" + shouldFinishedWork + '\'' +
                ", haveFinishedWork='" + haveFinishedWork + '\'' +
                ", unFinishedWorkReason='" + unFinishedWorkReason + '\'' +
                ", questionAndAnswer='" + questionAndAnswer + '\'' +
                ", nextDayPlan='" + nextDayPlan + '\'' +
                '}';
    }
}


public class User {

    // user主键
    private BigInteger id;

    // 姓名
    private String name;

    // 登录名称
    private String loginName;

    // 性别 0：女 1：男
    private String sex;

    // 出生日期
    private Date birthday;

    // 密码
    private String password;

    // 个人描述
    private String description;

    public User() {

    }

    public User(String loginName,
                String password) {
        this.loginName = loginName;
        this.password = password;
    }

    public User(String name,
                String loginName,
                String sex,
                Date birthday,
                String password,
                String description) {
        this.name = name;
        this.loginName = loginName;
        this.sex = sex;
        this.birthday = birthday;
        this.password = password;
        this.description = description;
    }

    public BigInteger getId() {
        return id;
    }

    public void setId(BigInteger id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public Date getBirthday() {
        return birthday;
    }

    public void setBirthday(Date birthday) {
        this.birthday = birthday;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public String getLoginName() {
        return loginName;
    }

    public void setLoginName(String loginName) {
        this.loginName = loginName;
    }

}

public class DailyService {


    public Map<String, Object> showDailyByUser(String userId) {

        Map<String, Object> resultMap = new HashMap<String, Object>();

        DailyDao dailyDao = new DailyDao();

        Daily paramDaily = new Daily();
        paramDaily.setCreateId(new BigInteger(userId));

        List<Daily> list = dailyDao.getDailyByCondition(paramDaily);

        if (!list.isEmpty()) {
            resultMap.put("result",
                    "success");
            resultMap.put("list",
                    list);
        } else {
            resultMap.put("result",
                    "failed");
        }

        return resultMap;
    }

    public Map<String, String> wirteDaily(String name,
                                          String userId,
                                          String shouldFinishedWork,
                                          String haveFinishedWork,
                                          String unFinishedWorkResaon,
                                          String questionAndAnswer,
                                          String nextDayPlan) {

        Map<String, String> resultMap = new HashMap<String, String>();

        long dailyId = System.currentTimeMillis();

        Daily daily = new Daily(
                name,
                shouldFinishedWork,
                haveFinishedWork,
                unFinishedWorkResaon,
                questionAndAnswer,
                nextDayPlan
        );

        BigInteger id = new BigInteger(dailyId+"");

        daily.setId(id);

        Timestamp createTime = new Timestamp(Calendar.getInstance().getTime().getTime());
        daily.setCreateTime(createTime);
        daily.setCreateId(new BigInteger(userId+""));

        DailyDao dailyDao = new DailyDao();
        try {
            dailyDao.saveDaily(daily);

            resultMap.put("result",
                    "success");
        }
        catch (SQLException e) {
            e.printStackTrace();

            resultMap.put("result",
                    "failed!" + e.getMessage());
        }
        catch (IOException e) {
            e.printStackTrace();

            resultMap.put("result",
                    "failed!" + e.getMessage());
        }
        catch (ClassNotFoundException e) {
            e.printStackTrace();

            resultMap.put("result",
                    "failed!" + e.getMessage());
        }

        return resultMap;
    }
}

public class UserService {


    public Map<String, String> login(String loginName,
                                     String password) {

        Map<String, String> resultMap = new HashMap<String, String>();

        UserDao userDao = new UserDao();

        User paramUser = new User(loginName,
                password);
        List<User> list = userDao.getUserByCondition(paramUser);

        if (!list.isEmpty()) {
            resultMap.put("result",
                    "success");
            resultMap.put("userId",
                    list.get(0)
                            .getId()
                            .toString());
        } else {
            resultMap.put("result",
                    "failed");
        }

        return resultMap;
    }

    public  Map<String, String> register(String name,
                         String sex,
                         Date birthday,
                         String loginName,
                         String password,
                         String description) {

        long userId = System.currentTimeMillis();

        Map<String, String> resultMap = new HashMap<String, String>();

        User user = new User(
                name,
                loginName,
                sex,
                birthday,
                password,
                description
        );

        BigInteger id = new BigInteger(userId+"");

        user.setId(id);
        UserDao userDao = new UserDao();
        try {
            userDao.saveUser(user);

            resultMap.put("result",
                    "success");
        }
        catch (SQLException e) {
            e.printStackTrace();

            resultMap.put("result",
                    "failed!"+e.getMessage());
        }
        catch (IOException e) {
            e.printStackTrace();

            resultMap.put("result",
                    "failed!"+e.getMessage());
        }
        catch (ClassNotFoundException e) {
            e.printStackTrace();

            resultMap.put("result",
                    "failed!"+e.getMessage());
        }

        return resultMap;
    }
}


* 未完成工作
* 未完成原因
* 工作成功
* 遇到的问题及解决方法
