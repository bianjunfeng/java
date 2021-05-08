# 使用BufferedReader 取得输入

使用Scanner来取得使用者的输入很方便，但是它以空白来区隔每一个输入字串，在某些时候并不适用，因为使用者可能输入一个字串，中间会包括空白字元，而您希望取得完整的字串。
您可以使用**BufferedReader**类别，它是**java.io**套件中所提供的一个类别，所以使用这个类别时必须先import java.io套件；使用BufferedReader物件的readLine()方法必须处理**IOException**例外（exception），例外处理机制是Java提供给程式设计人员捕捉程式中可能发生的错误所提供的机制，现阶段您处理IOException的方法是在main()方法后，加上**throws** IOException，这在以后会再详细讨论为何要这么作。
BufferedReader在建构时接受一个**Reader**物件，在读取标准输入串流时，会使用**InputStreamReader**，它继承了Reader类别，您使用以下的方法来为标准输入串流建立缓冲区物件：
BufferedReader buf = new BufferedReader(
                           new InputStreamReader(System.in));
"new"关键字表示您要建构一个物件为您所用，BufferedReader buf表示宣告一个型态为BufferedReader的物件变数，而new BufferedReader()表示以BufferedReader类别建构一个物件，new InputStreamReader(System.in)表示接受一个System.in物件来建构一个InputStreamReader物件。
您可以在学过物件导向观念之后再来看这段，现阶段若您比较难理解，就记得上面的缓冲区读取物件建立方式，通常要使用BufferedReader来取得使用者的输入都是这么写的。
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