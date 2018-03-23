### 输入输出

* 标准输入输出流

```
** 标准输入流 **
* Scanner类
// 构造一个 Scanner 并与标准输入流 System.in关联
Scanner in = new Scanner(System.in);
// 使用Scanner的各种方法实现输入操作
// nextLine()将输入一行
System.out.print("what is your name?");
String name = in.nextLine();
// 如果想以空格作为分隔符
String firstName = in.next();
// 如果想要读取一个整数
// nextDouble() 获取下一个浮点数
System.out.print("How old are you");
int age = in.nextInt();

* Console类
Console cons = System.console();
String username = cons.readLine("User name: ");
char[] passwd = cons.readPassword("Password: ");
// Console对象每次只能读取一行输入，不能读取一个单词或一个数值的方法

// Scanner API （java.util.Scanner 5.0）
* Scanner(InputStream in)
    用给定的输入流创建一个Scanner对象。
* String nextLine()
    读取输入的下一行内容。
* String next()
    读取输入的下一个单词（以空格作为分隔符）
* int nextInt()
* double nextDouble()
    读取并转换下一个表示整数或浮点数的字符序列
* boolean hasNext()
    检测输入中是否还有其他单词。
* boolean hasNextInt()
* boolean hasNextDouble()
    检测是否还有表示整数或浮点数的下一个字符序列。
    
// Console API （java.lang.System.Console 1.0）
* static Console console()
    对于任何一个通过控制台窗口启动的程序，都可以使用Console对象
// java.io.Console 6
* static char[] readPassword(String prompt, Object...args)
* static String readLine(String prompt, Object...args)
    显示字符串prompt并且读取用户输入，直到输入行结束。args参数可以用来
    提供输入格式。
    
** 格式化输出 **
* System.out.print(x);
    以x对应的数据类型所允许的最大非0数字位数打印输出x到控制台上。
* System.out.printf("%8.2f", x);
    用8个字符的宽度和小数点后两个字符的精度打印x。
    printf函数以%字符开始的格式都用相应的参数替换。
    ex: %f浮点数， %s字符， %d表示十进制整数
    类似c函数。
* tips：
    可以使用s转换符格式化任意的对象。对于任意实现了Formattable接口的对象
    都将调用formatTo方法；否则将调用toString方法，它可以将对象转换为
    字符串。
* String message = String.format("Hello, %s. Next year, you'll be %d", name, age);
```

* 文件输入与输出

```
// 构建一个文件输入流，将File对象构造一个Scanner对象
// "c:\\path\\to\\file.txt" 反斜杠的路径，反斜杠后再额外加一个反斜杠；
// Scanner构造参数不能使用字符串，会被当做数据流传入。
Scanner in = new Scanner(Paths.get("file.txt"));
// 写入文件，构造一个PrintWriter对象。
// 如果文件不存在，创建该文件。可以像System.out一样使用print、println、printf命令。
PrintWriter out = new PrintWriter("file.txt");

tips:
    如果用一个不存在的文件构造一个Scanner，或者用一个不能被创建的文件名构造
    一个PrintWriter，就会发生异常。

* API：
// java.util.Scanner 5.0
* Scanner(File f)
// 构造一个从给定文件读取数据的Scanner。
* Scanner(String data)
// 构造一个从给定字符串读取数据的Scanner。

// java.io.PrintWriter 1.1
* PrintWriter(String fileName)
// 构造一个将数据写入文件的PrintWriter。文件名由参数指定。

// java.nio.file.Paths 7 
* static Path get(String pathname)
// 根据给定的路径名构造一个Path。
```



