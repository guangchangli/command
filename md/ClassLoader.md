## 记录学习java类加载 做了什么， 加载一个类的过程

[TOC]

#### 1.类什么时候会被jvm加载

当我们主动使用类的时候，类才会被加载。

**主动使用类包括**

        1.创建类的实例
        2.访问类或类接口的静态变量/给静态变量赋值
        3.调用类的静态方法
        4.反射 class.forName("") 
        5.初始化一个类的子类  
        6.Java虚拟机启动时被标明为启动类的类（包含Main方法）
**那么不会加载初始化类的动作包括**

        1.子类引用父类的静态字段
        2.调用类的常量（常量在编译阶段存入了调用类的常量池中）
        3.通过数组定义来引用类
#### **2.类的生命周期**

**加载->链接(验证->准备->解析)->初始化->使用->卸载**
**加载：**

          1.通过类的全限定名 package.className 获取到类的二进制字节流
          2.将字节流转换为方法区的动态存储结构
          3. 在内存(堆)中生成一个代表这个类的java.lang.Class对象，作为方法区这个类的各种数据的访问入口
          4.加载完成后二进制字节流按照虚拟机所需要的格式存储在方法区中

 

**验证**：确保Class文件的字节流中包含的信息符合当前虚拟机的要求。

           1.文件格式验证：验证字节流是否符合Class文件格式的规范，并且能被当前版本的虚拟机处理。
           2.元数据验证：对字节码描述的信息进行语义分析，以确保其描述的信息符合java语言规范的要求。
           3.字节码验证：这个阶段的主要工作是进行数据流和控制流的分析。任务是确保被验证类的方法在运行时不会做出危害虚拟机安全的行为。
          4.符号引用验证：这一阶段发生在虚拟机将符号引用转换为直接引用的时候（解析阶段），主要是对类自身以外的信息进行匹配性的校验。目的是确保解析动作能够正常执行。

**准备**：准备阶段是正式为变量分配内存并设置初始值，这些内存都将在方法区中进行分配，这里的变量仅包括类标量不包括实例变量。

**解析**：虚拟机将常量池的符号引用替换为直接引用的过程。

            1.符号引用：符号引用以一组符号来描述所引用的目标，符号可以是任意形式的字面量，只要使用时能无歧义地定位到目标即可。符号引用与虚拟机实现的内存布局无关，引用的目标并不一定已经加载到内存中。
            2.直接引用：直接引用可以是直接指向目标的指针，相对偏移量或是一个能间接定位到目标的句柄。直接饮用是与内存布局相关的。
            3.类或接口的解析
            4.字段的解析
            5.类方法解析
            6.接口方法解析

**初始化**：执行类构造器< clinit >()方法，由编译器自动收集类中的所有类变量的赋值动作和静态语句块（static{}块）中的语句合并产生的，编译器收集的顺序是由语句在源文件中出现的顺序所决定的，静态语句块中只能访问到定义在静态语句块之前的变量，定义在它之后的变量，在前面的静态语句块能赋值，但是不能访问
类加载器

#### 3.jvm启动，默认使用三种类装入器

**启动（Bootstrap）类加载器**：引导类装入器是用本地代码实现的类装入器，它负责将 /lib 下面的类库加载到内存中。由于引导类加载器涉及到虚拟机本地实现细节，开发者无法直接获取到启动类加载器的引用，所以不允许直接通过引用进行操作。

**标准扩展（Extension）类加载器**：扩展类加载器是由 Sun 的 ExtClassLoader（sun.misc.Launcher$ExtClassLoader） 实现的。它负责将< Java_Runtime_Home >/lib/ext 或者由系统变量 java.ext.dir 指定位置中的类库加载到内存中。开发者可以直接使用标准扩展类加载器。

**系统（System）类加载器**：系统类加载器是由 Sun 的 AppClassLoader（sun.misc.Launcher$AppClassLoader）实现的。它负责将系统类路径（CLASSPATH）中指定的类库加载到内存中。开发者可以直接使用系统类加载器。

```java
a. Bootstrap ClassLoader/启动类加载器

主要负责jdk_home/lib目录下的核心 api 或 -Xbootclasspath 选项指定的jar包装入工作.

b. Extension ClassLoader/扩展类加载器

主要负责jdk_home/lib/ext目录下的jar包或 -Djava.ext.dirs 指定目录下的jar包装入工作

c. System ClassLoader/系统类加载器

主要负责java -classpath/-Djava.class.path所指的目录下的类与jar包装入工作.

d. User Custom ClassLoader/用户自定义类加载器(java.lang.ClassLoader的子类)

在程序运行期间, 通过java.lang.ClassLoader的子类动态加载class文件, 体现java动态实时类装入特性.
```

#### 4.双亲委派机制

jvm加载类时默认采用双亲委派机制

##### 4.1什么是双亲委派

```
双亲委派机制有4种类加载器为：
自定义类加载器(UserClassLoader)->应用/系统(App/SystemClassLoader)->扩展类(ExtClassLoader)->启动(BootstrapClassLoader)类加载器。
加载过程
加载某个类.class(需要编译即javac Xx.java>>Xx.class)的时候，不会直接去加载，而是自定义会委托应用/系统，应用/系统会委托扩展，扩展会委托启动类加载器尝试去加载，如果启动类加载器不加载这个，就交给扩展，扩展不行就应用/系统，一层层的下去，然后最终加载到这个.class类。
加载不是一次性加载，而是按需动态加载
```

##### 4.2双亲委派优点

  1.安全，可避免用户自己编写的类动态替换Java的核心类，如java.lang.String

  2.避免全限定命名的类重复加载(使用了findLoadClass()判断当前类是否已加载)

ClassLoader常用方法

```java
//加载指定名称（包括包名）的二进制类型，供用户调用的接口  
public Class loadClass(String name)throws ClassNotFoundException{//…}  

//加载指定名称（包括包名）的二进制类型，同时指定是否解析（但是，这里的resolve参数不一定真正能达到解析的效果，供继承用  
protected synchronized Class loadClass(String name,boolean resolve)throws ClassNotFoundException{//…}  

//findClass方法一般被loadClass方法调用去加载指定名称类，供继承用  
protected Class findClass(String name)throws ClassNotFoundException {}  

//定义类型，一般在findClass方法中读取到对应字节码后调用，可以看出不可继承（说明：JVM已经实现了对应的具体功能，解析对应的字节码，产生对应的内部数据结构放置到方法区，所以无需覆写，直接调用就可以了）  
protected final Class defineClass(String name,byte[] b,int off,int len)  throws ClassFormatError{//…} 
```
##### 4.3双亲委派过程 向上委托 向下查找

```java
public Class<?> loadClass(String name)throws ClassNotFoundException {  
       return loadClass(name,false);  
}  
protectedsynchronized Class<?> loadClass(String name,boolean resolve)  
           throws ClassNotFoundException {  
       //首先判断该类型是否已经被加载  
        Class c = findLoadedClass(name);  
       if (c ==null) {  
           //如果没有被加载，就委托给父类加载或者委派给启动类加载器加载  
           try {  
               if (parent !=null) {  
//如果存在父类加载器，就委派给父类加载器加载  
                    c = parent.loadClass(name,false);  
                }else {  
//如果不存在父类加载器，就检查是否是由启动类加载器加载的类，通过调用本地方法native Class findBootstrapClass(String name)  
                    c = findBootstrapClass0(name);  
                }  
            }catch (ClassNotFoundException e) {  
       //如果父类加载器和启动类加载器都不能完成加载任务，才调用自身的加载功能  
                c = findClass(name);  
            }  
        }  
       if (resolve) {  
            resolveClass(c);  
        }  
       return c;  
    }  
```

##### 4.5自定义类加载器 只需要重写findClass()

```java
public class MyClassLoader extends ClassLoader {

        public MyClassLoader() {
        }
  
        public MyClassLoader(ClassLoader parent) {
            super(parent);
        }
  
        @Override
        protected Class<?> findClass(String name) throws ClassNotFoundException
        {
            File file = new File("/Users/jasmine/Desktop/User.class");
            try{
                byte[] bytes = getClassBytes(file);
                //defineClass方法可以把二进制流字节组成的文件转换为一个java.lang.Class
                Class<?> c = this.defineClass(name, bytes, 0, bytes.length);
                return c;
            }
            catch (Exception e)
            {
                e.printStackTrace();
            }

            return super.findClass(name);
        }

        private byte[] getClassBytes(File file) throws Exception
        {
            // 这里要读入.class的字节，因此要使用字节流
            FileInputStream fis = new FileInputStream(file);
            FileChannel fc = fis.getChannel();
            ByteArrayOutputStream baos = new ByteArrayOutputStream();
            WritableByteChannel wbc = Channels.newChannel(baos);
            ByteBuffer by = ByteBuffer.allocate(1024);

            while (true){
                int i = fc.read(by);
                if (i == 0 || i == -1){
                    break;}
                by.flip();
                wbc.write(by);
                by.clear();
            }
            fis.close();
            return baos.toByteArray();
        }
    }

```

#### 5.线程上下文(待续)