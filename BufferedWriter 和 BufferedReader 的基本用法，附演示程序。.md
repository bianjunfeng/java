# BufferedWriter 和 BufferedReader 的基本用法，附演示程序。

​		使用Scanner来取得使用者的输入很方便，但是它以空白来区隔每一个输入字串，在某些时候并不适用，因为使用者可能输入一个字串，中间会包括空白字元，而您希望取得完整的字串。
​		您可以使用**BufferedReader**类别，它是**java.io**套件中所提供的一个类别，所以使用这个类别时必须先import java.io套件；使用BufferedReader物件的readLine()方法必须处理**IOException**例外（exception），例外处理机制是Java提供给程式设计人员捕捉程式中可能发生的错误所提供的机制，现阶段您处理IOException的方法是在main()方法后，加上**throws** IOException，这在以后会再详细讨论为何要这么作。
​		BufferedReader在建构时接受一个**Reader**物件，在读取标准输入串流时，会使用**InputStreamReader**，它继承了Reader类别，您使用以下的方法来为标准输入串流建立缓冲区物件：
​				`BufferedReader buf = new BufferedReader(  new InputStreamReader(System.in));`
​		"new"关键字表示您要建构一个物件为您所用，BufferedReader buf表示宣告一个型态为BufferedReader的物件变数，而new BufferedReader()表示以BufferedReader类别建构一个物件，new InputStreamReader(System.in)表示接受一个System.in物件来建构一个InputStreamReader物件。
​		您可以在学过物件导向观念之后再来看这段，现阶段若您比较难理解，就记得上面的缓冲区读取物件建立方式，通常要使用BufferedReader来取得使用者的输入都是这么写的。
下面这个程式可以在文字模式下取得使用者输入（可包括空白字元输入），并重新显示在主控台中：

```java
import java.io.*;
public class Echo {
    public static void main(String[] args) throws IOException {
        BufferedReader buf = new BufferedReader( new InputStreamReader(System.in));
        
        System.out.print("请输入一列文字: ");  
        
        String text = buf.readLine();      
        
        System.out.println("您输入的文字: " + text);     
    } 
}
```



**一、BufferedWriter 类**
构造方法：bufferedWriter bf = new bufferedWriter(Writer out );

主要方法：void write(char ch);//写入单个字符。

```java
              void write(char []cbuf,int off,int len)//写入字符数据的某一部分。

              void write(String s,int off,int len)//写入字符串的某一部分。

              void newLine()//写入一个行分隔符。

              void flush();//刷新该流中的缓冲。将缓冲数据写到目的文件中去。

              void close();//关闭此流，再关闭前会先刷新他。
```
```java
	package Buffered;

	import java.io.BufferedWriter;
	import java.io.FileWriter;
	import java.io.IOException;

	public class BufferedWriterDemo {
		public static void main(String[] args) throws IOException {
			FileWriter fw = new FileWriter("Buffered.txt");
//			fw.write("ok168");
//			fw.close();
			/**
			 * 为了提高写入的效率，使用了字符流的缓冲区。
			 * 创建了一个字符写入流的缓冲区对象，并和指定要被缓冲的流对象相关联。
			 */
			BufferedWriter bufw = new BufferedWriter(fw);
		
        //使用缓冲区中的方法将数据写入到缓冲区中。
        bufw.write("hello world !");
        bufw.newLine();
        bufw.newLine();
        bufw.write("!hello world !");
        bufw.write("!hello world !");
        //使用缓冲区中的方法，将数据刷新到目的地文件中去。
        bufw.flush();
        //关闭缓冲区,同时关闭了fw流对象
        bufw.close();	
    	}
    }
```
**二、BufferedReader类。**
构造方法：BufferedReader br = new BufferReader(Reader in);

主要方法：

```java
int read();//读取单个字符。
int read(char[] cbuf,int off,int len);
//将字符读入到数组的某一部分。返回读取的字符数。达到尾部 ，返回-1。

              String readLine();      //读取一个文本行。

              void close();           //关闭该流。并释放与该流相关的所有资源。

```

```java
	package Buffered;

    import java.io.BufferedWriter;
    import java.io.FileWriter;
    import java.io.IOException;

    public class BufferedWriterDemo {
        public static void main(String[] args) throws IOException {
            FileWriter fw = new FileWriter("Buffered.txt");
    //		fw.write("ok168");
    //		fw.close();
    	/**

			- 为了提高写入的效率，使用了字符流的缓冲区。
 			- 创建了一个字符写入流的缓冲区对象，并和指定要被缓冲的流对象相关联。
    */
    BufferedWriter bufw = new BufferedWriter(fw);
        //使用缓冲区中的方法将数据写入到缓冲区中。
        bufw.write("hello world !");
        bufw.newLine();
        bufw.newLine();
        bufw.write("!hello world !");
        bufw.write("!hello world !");
        //使用缓冲区中的方法，将数据刷新到目的地文件中去。
        bufw.flush();
        //关闭缓冲区,同时关闭了fw流对象
        bufw.close();	
    }
}
```

**自定义的一个myBufferedReader类。**


```java
package Buffered;

import java.io.FileReader;
import java.io.IOException;

public class MyBufferedReader {
    private FileReader fr;
    private char []buf = new char[1024];
    private int count = 0;
    private int pos = 0;
    public MyBufferedReader(FileReader f){
        this.fr = f;		
    }
    public int myRead() throws IOException{
        if(count == 0){
            count = fr.read(buf);
            pos = 0;
        }
        if(count<0)
            return -1;
        int ch = buf[pos++];
        count--;
        return ch; 
    }

    public String myReadLine() throws IOException{
        StringBuilder sb = new StringBuilder();
        int ch = 0;
        while ((ch = myRead()) != -1) {
            if (ch == '\r')
                continue;
            if (ch == '\n')
                return sb.toString();
            sb.append((char) ch);
            if(count == 0)
                return sb.toString();			
        }
        return null;
    }
    public void myClose() throws IOException {
        fr.close();
    }
}
```

**使用bufferedReader 和bufferWriter方法写的一个复制文本的小程序。**



```java
package IOtest;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class TextCopyByBuf {
/**
 * 首先创建读取字符数据流对象关联所要复制的文件。
 * 创建缓冲区对象关联流对象。
 * 从缓冲区中将字符创建并写入到要目的文件中。
 * @throws IOException 
 */
public static void main(String[] args) throws IOException {
	FileReader fr = new FileReader("C:\\demo.txt");
	FileWriter fw = new FileWriter("D:\\love.txt");
	BufferedReader bufr = new BufferedReader(fr);
	BufferedWriter bufw = new BufferedWriter(fw);
	//一行一行的寫。
	String line = null;
	while((line = bufr.readLine()) != null){
		bufw.write(line);
		bufw.newLine();
		bufw.flush();
	}
/*	一個字節一個字節的寫。
    int ch = 0;
	while((ch = bufr.read())!=-1){
		bufw.write(ch);
	}*/
	bufr.close();
	bufw.close();
}
}
```


