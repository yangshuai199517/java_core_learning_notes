Qestions



|      | description                                | done |
| ---- | ------------------------------------------ | ---- |
|      | 重载 overloading  同名函数，不同参数的实现 | 是   |
|      | 覆盖 overriding，对超类方法的重新实现。    |      |
|      | mysql索引                                  |      |
|      | Comparator(Arrays.sort) 接口的多种实现     |      |
|      | 如何写内部类的构造函数                     |      |
|      | 代理                                       |      |
|      | 反射                                       |      |
|      |                                            |      |
|      |                                            |      |





















## Notes

+ Comparator<String> comp = (String a, String b)->{return a.length()-b.length()} 无需指定lambda表达式的返回类型。对于只有一个方法的接口，需要这种接口的对象时，就可以提供一个lambda表达式，这种接口成为函数式接口。

+ 使用接口时，先申明一个接口，然后创建一个函数，这个函数中某一个参数是接口类型的，然后再调用这个函数时使用lambda表达式。(简单来说，就是要有接口，还要有使用接口中函数的函数，才能使lambda表达式)

  ~~~java
  //interface stated
  interface IntConsumer{
      void accept(int value);
  }
  //create a function with parameter of the interface stated type
  public  static void repeat(int n,IntConsumer action){
          for(int i=0;i<n;i++){action.accept(i);}
      }
  //call the repeat function
  ~~~

  

  

+ java有一个限制，无法构造泛型类型的数组。

+ 内部类可以访问自身的数据域，也可以访问创建他们的外围类对象的数据域。

+ 同一个类中，public 或private 都可见（针对实现而言，都可以直接写代码调用）；同一个包中，public和非public的类可在main中使用，且其public数据域或者方法可以直接使用；不同包中只有public类可直接在main中使用，非public类不能使用。对于非main函数中的使用，也是如此。

+ 只有内部类是私有类，而常规类只有包可见性和公有可见性。

+ 内部类中声明的静态域必须是final的，但是不能有静态方法。

+ 局部类不能用public或private进行声明，它的作用域被限定在声明这个局部类的块中。

  ~~~java
  public void start(){
      class TimePrinter implements ActionListener{
          public int a =...;
          ...;
      }
      ActionListener listener = new TimePrinter();
      Time t = new Timer(interval,listener);
      t.start()
  }
  ~~~



+ 以下重写类了，达到比较的次数的目的。

  ~~~java
   Date[] dates = new Date[100];
       int[] counter = new int[1];
       for(int i= 0;i<dates.length;i++){
           dates[i] = new Date(){
               public int compareTo(Date other){
                   counter[0]++;
                   return super.compareTo(other);
               }
           };
       }
       Arrays.sort(dates);
          System.out.println(Arrays.toString(counter));
  ~~~

+ 假如只创建一个类的对象，就不必命名了，这种类被称为匿名内部类。下面就是例子。

  ~~~java
  /*创建一个实现接口ActionListener的类的对象，需要实现的方法actionPerformed定义在\{}内。
  通常的语法格式为
  new SuperType(construction paremeter){
  inner class methods and data
  }
  SuperClass 可以为接口（实现）或者类（继承）
  */
  public static void start(int interval,boolean beep){
      ActionListener listener = new ActionListener(){
          public void actionPerformed(action event){
              System.out.println("at the tone,the time is"+new Date());
              if(beep)Toolkit.getDefaulTollkit().beep();
          }
      };
      Timer t = new Time(interval,listener);
      t.start();
      
  }
  
  
  ~~~

  

+ 即使将arrays声明为final，其中的元素也是可以被改变的；但是被声明为final的基本类型就不可以被改变了。

+ 目前来说接口有两种实现方式，匿名内部类和lambda表达式。

+ 类的实例域的初始化是可以在声明中调用函数实现的。

+ 

+ ~~~java
  //关于构造函数
  class E{
      public   int[] aaa = {1,2} ;
      public  int aaaa = 10000;
      private  int a = 100;
      public int x;
  
      public E(){
          x = 10000;
          aaa =new int[]{3,4};
      }
  //实例之后，aaa的值为{3,4}
      
    class E{
      public   int[] aaa = {1,2} ;
      public  int aaaa = 10000;
      private  int a = 100;
      public int x;
  
    }
  //实例之后，aaa的值为{1,2}
      
  class E{
      public   int[] aaa = {1,2} ;
      public  int aaaa = 10000;
      private  int a = 100;
      public int x;
  
      public E(int[u]){
          x = 10000;
          aaa = u;
      }
  //实例 E e1 = new E(new int[]{100,99});之后，aaa的值为{100,99}
  //定义为final的在构造函数外赋值后，就不能再构造函数内赋值了
  //对于声明为public final的arrays，其在main中还可以被赋值修改，如e1.aaa[0] = -100可行
  //但是public final 的基本类型的变量就不能再main中被赋值了。
  
    
  ~~~

+ 在内部类不需要访问外围类对象的时候，就应该使用静态内部类。（详细见java核心6.4.6）
+ 关于代理的实验记录。静态代理，就是重写一个类，让域中的某一个成员为被代理类的实例对象，然后将同样的方法覆盖一下@override，以下主要记载动态代理。突然发现没有什么好弄的。就看一下java中的下载好的那个博客就行了。