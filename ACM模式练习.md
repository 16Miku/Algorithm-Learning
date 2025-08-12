



# 牛客ACM输入输出练习

<https://www.nowcoder.com/exam/oj?page=1&tab=%E7%AE%97%E6%B3%95%E7%AC%94%E9%9D%A2%E8%AF%95%E7%AF%87&topicId=372>


# PIO1 只有输出

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-08-22.png)


```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        // 注意 hasNext 和 hasNextLine 的区别
        // while (in.hasNextInt()) { // 注意 while 处理多个 case
        //     int a = in.nextInt();
        //     int b = in.nextInt();
        //     System.out.println(a + b);
        // }


        System.out.println("Hello Nowcoder!");
    }
}
```




---

# PIO2 单组_A+B

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-11-47.png)



```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
public class Main {
    // public static void main(String[] args) {
    //     Scanner in = new Scanner(System.in);
    //     // 注意 hasNext 和 hasNextLine 的区别
    //     while (in.hasNextInt()) { // 注意 while 处理多个 case
    //         int a = in.nextInt();
    //         int b = in.nextInt();
    //         System.out.println(a + b);
    //     }
    // }

    public static void main( String[] args ) {


        Scanner in = new Scanner( System.in );


        while( in.hasNextInt() ) {


            int a = in.nextInt();

            int b = in.nextInt();

            System.out.println( a+b );
            
        }



    }
}
```







# PIO3 多组_A+B_EOF形式

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-12-28.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        // 注意 hasNext 和 hasNextLine 的区别
        while (in.hasNextInt()) { // 注意 while 处理多个 case
            int a = in.nextInt();
            int b = in.nextInt();
            System.out.println(a + b);
        }
    }
}
```






---



# PIO4 多组_A+B_T组形式

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-13-01.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
public class Main {
    // public static void main(String[] args) {
    //     Scanner in = new Scanner(System.in);
    //     // 注意 hasNext 和 hasNextLine 的区别
    //     while (in.hasNextInt()) { // 注意 while 处理多个 case
    //         int a = in.nextInt();
    //         int b = in.nextInt();
    //         System.out.println(a + b);
    //     }
    // }


    public static void main( String[] args ) {

        Scanner in = new Scanner( System.in );

        int t = in.nextInt();


        for( int i=0; i < t; i++ ) {


            int a = in.nextInt();

            int b = in.nextInt();

            System.out.println( a+b );



        }



    }
}
```




# PIO5 多组_A+B_零尾模式

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-14-15.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
public class Main {
    // public static void main(String[] args) {
    //     Scanner in = new Scanner(System.in);
    //     // 注意 hasNext 和 hasNextLine 的区别
    //     while (in.hasNextInt()) { // 注意 while 处理多个 case
    //         int a = in.nextInt();
    //         int b = in.nextInt();
    //         System.out.println(a + b);
    //     }
    // }


    public static void main( String[] args ) {


        Scanner in = new Scanner( System.in );


        while( in.hasNextInt() ) {


            int a = in.nextInt();

            int b = in.nextInt();


            if( a == 0 && b == 0 ) {

                break;

            } else {

                System.out.println( a+b );


            }


        }


    }




}
```





---

# PIO6 单组_一维数组

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-14-41.png)


```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }





public class Main {


    public static void main( String[] args ) {



        Scanner in = new Scanner( System.in );


        int n = in.nextInt();


        int[] a = new int[n];

        long sum=0;

        for( int i=0; i < n; i++ ) {


            a[i] = in.nextInt();


            sum += a[i];


        }




        System.out.println(sum);


    }




}
```














# PIO7 多组_一维数组_T组形式

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-15-44.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }




public class Main {



    public static void main( String[] args ) {



        Scanner in = new Scanner( System.in );


        int t = in.nextInt();


        for( int i=0; i < t; i++ ) {


            int n = in.nextInt();

            int[] a = new int[n];

            long sum=0;


            for( int j=0; j < n; j++ ) {



                a[j] = in.nextInt();


                sum += a[j];

            }


            System.out.println(sum);


            



        }


    }








}

```














---

# PIO8 单组_二维数组


![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-16-41.png)


```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }





public class Main {




    public static void main( String args[] ) {



        Scanner in = new Scanner( System.in );



        int n = in.nextInt( );

        int m = in.nextInt();

        int[][] a = new int[n][m];


        long sum=0;

        for( int i=0; i < n; i++ ) {



            for( int j=0; j < m; j++ ) {


                a[i][j] = in.nextInt();


                sum += a[i][j];


            }


        }



        System.out.println( sum );



    }




}
```


















# PIO9 多组_二维数组_T组形式

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-17-27.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }





public class Main {




    public static void main( String[] args ) {




        Scanner in = new Scanner( System.in );


        int t = in.nextInt();


        for ( int k = 0; k < t; k++ ) {



            int n = in.nextInt( );

            int m = in.nextInt();

            int[][] a = new int[n][m];


            long sum = 0;

            for ( int i = 0; i < n; i++ ) {



                for ( int j = 0; j < m; j++ ) {


                    a[i][j] = in.nextInt();


                    sum += a[i][j];


                }


            }



            System.out.println( sum );






        }



    }




}
```


















---

# PIO10 单组_字符串


![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-18-06.png)


```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }









public class Main {
    


    public static void main( String[] args ) {



        Scanner in = new Scanner( System.in );


        int n = in.nextInt();


        String s = in.next();


        StringBuilder sb = new StringBuilder(s);


        sb.reverse();


        s = sb.toString();

        System.out.println(s);



    }






}
```








# PIO11 多组_字符串_T组形式

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-18-55.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }






public class Main {



    public static void main( String[] args ) {



        Scanner in = new Scanner( System.in );


        int t = in.nextInt();


        for ( int i = 0; i < t; i++ ) {



            int n = in.nextInt();


            String s = in.next();


            StringBuilder sb = new StringBuilder(s);


            sb.reverse();


            s = sb.toString();

            System.out.println(s);






        }




    }




}
```





---

# PIO12 单组_二维字符数组

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-19-39.png)


```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }










public class Main {
    public static void main(String[] args) {



        Scanner in = new Scanner(System.in);



        int n = in.nextInt();

        int m = in.nextInt();


        char[][] a = new char[n][m];



        for ( int i = 0; i < n; i++ ) {

            String str = in.next();


            for ( int j = 0; j < m; j++  ) {

                

                a[i][j] = str.charAt( j );



            }


        }




        for ( int i = n - 1; i >= 0; i-- ) {



            for ( int j = m - 1; j >= 0; j--  ) {



                System.out.print( a[i][j] );


            }

            System.out.println("");


        }








    }
}
```








# PIO13 多组_带空格的字符串_T组形式

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-20-22.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }











public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        
        int t = in.nextInt();




        for( int i=0; i < t; i++ ) {



            int n = in.nextInt();

            in.nextLine();
            //注意：用nextLine()进行换行，默认到下一个Enter下


            String s = in.nextLine();
            //此时才能正确读取一行的字符串内容


            StringBuilder sb = new StringBuilder();

            for( int j = n-1 ; j >= 0 ; j-- ) {

                if( s.charAt(j) != ' ' ) {

                    sb.append( s.charAt(j) );

                }
                


            }


            System.out.println( sb.toString() );




        }



    }
}
```











---

# PIO14 单组_保留小数位数

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-21-18.png)


```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }





public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        
        double n = in.nextDouble();


        System.out.printf( "%.3f",n );




    }
}

```









# PIO15 单组_补充前导零

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-22-02.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }





public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        


        int n = in.nextInt();


        System.out.printf( "%09d",n  );









    }
}
```












---

# PIO16 单组_spj判断YES与NO

![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-22-44.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }





public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        

        int n = in.nextInt();


        if( n % 2 == 0  ) {


            System.out.println("NO");

        } else {


            System.out.println("YES");
        }





    }
}
```











# PIO17 单组_spj判断浮点误差


![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-23-30.png)


```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }





public class Main {
    public static void main(String[] args) {
        
        

        Scanner in = new Scanner( System.in );



        int r = in.nextInt();


        double s = Math.PI * r *r;

        System.out.printf( "%.6f",s );










    }
}

```
















---

# PIO18 单组_spj判断数组之和


![alt text](image-ACM模式练习/Snipaste_2025-08-12_23-24-22.png)

```java
import java.util.Scanner;

// 注意类名必须为 Main, 不要有任何 package xxx 信息
// public class Main {
//     public static void main(String[] args) {
//         Scanner in = new Scanner(System.in);
//         // 注意 hasNext 和 hasNextLine 的区别
//         while (in.hasNextInt()) { // 注意 while 处理多个 case
//             int a = in.nextInt();
//             int b = in.nextInt();
//             System.out.println(a + b);
//         }
//     }
// }





public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        
        int n = in.nextInt();

        int m = in.nextInt();

        for( int i=0; i < n-1; i++ ) {


            System.out.println( 1 + " ");



        }

        long lastElement = m - (n-1);


        System.out.println( lastElement);


        in.close();

    }
}
```





---

