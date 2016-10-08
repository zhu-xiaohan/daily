# io流
===================

* 流的概念
	
	* 流是一组有顺序的，有起点和终点的字节集合，是对数据传输的总称或抽象。
	
	* 所谓的IO就是指流的读(input输入)与写(output输出)操作的简称。
	
	* Java对数据的操作是通过流的方式
	
    * IO流用来处理设备之间的数据传输
	
    * 注意：Java用于操作流的对象都在IO包中
	
* 流的分类
   
    * 根据数据流向不同分为： 程序中需要根据待传输数据的不同特性而使用不同的流
	
		1. 输入流（intput）对输入流只能进行读操作
		
		2. 输出流（output），对输出流只能进行写操作 
		
	* 根据处理数据类型的不同分为：字节流和字符流
	
		1. 字节流 ：InputStream是所有字节输入流的祖先，而OutputStream是所有字节输出流的祖先。
		
		2. 字符流： Reader是所有读取字符串输入流的祖先，而Writer是所有输出字符串的祖先。
		
		3. 字节流和字符流的操作都是采用如下的步骤完成： 
		
			1. 找到一个要操作的资源，可能是文件，可能是其他的位置 
			
			2. 根据字节流或字符流的子类，决定输入及输出的位置 
			
			3. 进行读或写的操作 
			
			4. 关闭 


* File类

	在File类中包含了大部分和文件操作的功能方法，
	该类的对象可以代表一个具体的文件或文件夹，
	所以以前曾有人建议将该类的类名修改成FilePath，
	因为该类也可以代表一个文件夹，更准确的说是可以代表一个文件路径。
* 字节流的缓冲区
* FileReader fr = new FileReader("d:" + File.separator + "test.txt");
	// 为了提高效率。加入缓冲技术。将字符读取流对象作为参数传递给缓冲对象的构造函数。
	BufferedReader bufr = new BufferedReader(fr);
	String line = null;
	while ((line = bufr.readLine()) != null) {
		System.out.print(line);
	}
	bufr.close();
* FileWriter fw = new FileWriter("d:" + File.separator + "test.txt");
	  BufferedWriter bufw = new BufferedWriter(fw);
	  for (int x = 1; x < 5; x++) {
		bufw.write("abcd" + x);
		bufw.newLine();
		bufw.flush();
	  }
  	 // 记住，只要用到缓冲区，就要记得刷新。
   	bufw.close();
* 字符编码
* 字符流的出现为了方便操作字符。 
  更重要是的加入了编码转换。 
  通过子类转换流来完成。
	InputStreamReader
	OutputStreamWriter
  在两个对象进行构造的时候可以加入字符集。

  


	
