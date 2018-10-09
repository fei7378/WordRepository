使用java读取properties文件
方法一：
//新建Properties对象
Properties prop = new Properties();
//获取值的对象
String value = new String();
//文件路径package/classname.properties
prop=PropertiesLoaderUtils.loadAllProperties("config/config.properties");
//在properties中的key值
value = prop.getProperty("FEI");
方法二：
Properties prop = new Properties();
String value = null;
try {
// 通过输入缓冲流进行读取配置文件
InputStream InputStream = new BufferedInputStream(new FileInputStream(newFile("src/main/java/config/config.properties")));
// 加载输入流
prop.load(InputStream);
// 根据关键字获取value值
value = prop.getProperty("FEI");
//第三种方式
	/**
	 * 第三种读取方法 根据key读取value
	 *
	 * @Title: getProperties_3 @Description: 第三种方式： 相对路径，
	 *         properties文件需在classpath目录下， 比如：config.properties在包com.test.config下，
	 *         路径就是/com/test/config/config.properties @param filePath @param
	 *         keyWord @return @return String @throws
	 */
InputStream inputStream = TestProperties.class.getResourceAsStream(filePath);
prop.load(inputStream);
value = prop.getProperty(keyWord);
