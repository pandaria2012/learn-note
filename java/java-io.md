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
    
```