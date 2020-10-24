# learnRust

# rust 基本语法
# <a href="https://play.rust-lang.org/">rust在线工具</a>
# <a href="https://laplacedemon.gitbooks.io/-rust/content/">快学Rust</a>
# <a href="https://www.runoob.com/rust/rust-tutorial.html">Rust菜鸟教程</a>
# <a href="https://gitee.com/755157298/panda-zoo">rust数据库demo</a>
# rust 函数实例
fn main() {
       let x=10;
       let y=20;
       
      println!("{}+{}={}",x,y,add(x,y));
    }
fn add(x:i32,y:i32) -> i32{ //rust中用->i32表示函数返回值，函数可以在调用语句后面声明
    return x+y;
}  
# rust元组的基本使用

fn main() {
   let tup=(1,"hello",12.2);
     
     println!("{:?}",tup); //输出元组所有元素需要用到{:?}占位符
    }
  
# 访问元组中的单个元素
我们可以使用 元组名.索引数字 来访问元组中相应索引位置的元素。索引从 0 开始。

例如下面这个拥有 3 个元素的元组

let tuple:(i32,f64,u8) = (-325,4.9,22);
我们可以通过下面的方式访问各个元素

tuple.0  // -325

tuple.1  // 4.9

tuple.2  // 22
# 元组解构赋值 ( destructing ) =
解构赋值 ( destructing ) 就是把 元组 ( tuple ) 中的每一个元素按照顺序一个一个赋值给变量。

元组解构赋值 ( destructing ) 语法格式
元组解构赋值 ( destructing ) 的语法格式如下

(age,is_male,cgpa) = (30,true,7.9);
上面这种赋值操作称之为 元组解构赋值，它会把 等号 ( = ) 右边的元组的元素按照顺序一个一个赋值给等号左边元组里的变量。

赋值完成后，左边的各个变量的值为

age      = 30;
is_male  = true;
cgpa     = 7.9;
解构 操作是 Rust 语言的一个特性，最新的 JavaScript 语言也有解构操作。

范例
fn main(){
   let b:(i32,bool,f64) = (30,true,7.9);
   print(b);
}
fn print(x:(i32,bool,f64)){
   println!("Inside print method");
   let (age,is_male,cgpa) = x; //assigns a tuple to 
   distinct variables
   println!("Age is {} , isMale? {},cgpa is 
   {}",age,is_male,cgpa);
}
编译运行以上 Rust 代码，输出结果如下

Inside print method
Age is 30 , isMale? true,cgpa is 7.9

# Rust 数组的操作
 fn main() {
   let arr:[i32;4] = [10,20,30,40];   
     println!("{:?}",arr);
    }
  结果：[10, 20, 30, 40]
  
 # 声明和初始化数组
Rust 语言为数组的声明和初始化提供了 3 中语法

最基本的语法，指定每一个元素的初始值

let variable_name:[dataType;size] = [value1,value2,value3];
例如

let arr:[i32;4] = [10,20,30,40];
省略数组类型的语法

因为指定了每一个元素的初始值，所以可以从初始值中推断出数组的类型

let variable_name = [value1,value2,value3];
例如

fn main() {
   let arr = [10,20,30,40];   
     println!("{:?}",arr);
    }
  
指定默认初始值的语法，这种语法有时候称为 默认值初始化。

如果不想为每一个元素指定初始值，则可以为所有元素指定一个默认的初始值。

let variable_name:[dataType;size] = [default_value_for_elements,size];
例如下面的代码为每一个元素指定初始值为 -1
fn main() {
   let arr:[i32;4] = [-1;4];
     println!("{:?}",arr);
    }
  结果：[-1, -1, -1, -1]
  # Rust 还提供了 len() 方法则用于返回数组的长度，也就是元素的格式。

fn main(){
   let arr:[i32;4] = [10,20,30,40];
   println!("array is {:?}",arr);
   println!("array size is :{}",arr.len());
}
编译运行以上 Rust 代码，输出结果如下

array is [10, 20, 30, 40]
array size is :4

# Rust 利用for循环来遍历输出数组元素
fn main() {
   let arr =[10,20,45,60];
   for i in 0..arr.len(){
       println!("the {} of arr is {}",i+1,arr[i]);
    }
      
  }
  结果：
the 1 of arr is 10
the 2 of arr is 20
the 3 of arr is 45
the 4 of arr is 60
  
