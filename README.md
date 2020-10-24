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

# 迭代数组 iter()
我们可以使用 iter() 函数为数组生成一个迭代器。

然后就可以使用 for in 语法来迭代数组。

fn main(){

let arr:[i32;4] = [10,20,30,40];
   println!("array is {:?}",arr);
   println!("array size is :{}",arr.len());

   for val in arr.iter(){
      println!("value is :{}",val);
   }
}
编译运行以上 Rust 代码，输出结果如下

array is [10, 20, 30, 40]
array size is :4
value is :10
value is :20
value is :30
value is :40

# 可变数组,也就是元素的值可以改变
使用 let 声明的变量，默认是只读的，数组也不例外。也就是说，默认情况下，数组是不可变的。

fn main(){
   let arr:[i32;4] = [10,20,30,40];
   arr[1] = 0;
   println!("{:?}",arr);
}
上面的代码运行会出错，错误信息如下

error[E0594]: cannot assign to `arr[_]`, as `arr` is not declared as mutable
 --> src/main.rs:3:4
  |
2 |    let arr:[i32;4] = [10,20,30,40];
  |        --- help: consider changing this to be mutable: `mut arr`
3 |    arr[1] = 0;
  |    ^^^^^^^^^^ cannot assign

error: aborting due to previous error
数组的不可变，表现为两种形式：变量不可重新赋值为其它数组、数组的元素不可以修改。

如果要让数组的元素可以修改，就需要添加 mut 关键字。例如

let mut arr:[i32;4] = [10,20,30,40];

我们将刚刚错误的代码修改下

fn main(){
   let mut arr:[i32;4] = [10,20,30,40];
   arr[1] = 0;
   println!("{:?}",arr);
}
就可以正常运行，输出结果如下

[10, 0, 30, 40]

# 数组作为函数参数
数组可以作为函数的参数。而传递方式有 传值传递 和 引用传递 两种方式。

传值传递 就是传递数组的一个副本给函数做参数，函数对副本的任何修改都不会影响到原来的数组。

引用传递 就是传递数组在内存上的位置给函数做参数，因此函数对数组的任何修改都会影响到原来的数组。

## 范例：传值传递
下面的代码，我们使用传值方式将数组传递给函数做参数。函数对参数的任何修改都不会影响到原来的数组。

fn main() {
   let arr = [10,20,30];
   update(arr);

   println!("Inside main {:?}",arr);
}
fn update(mut arr:[i32;3]){
   for i in 0..3 {
      arr[i] = 0;
   }
   println!("Inside update {:?}",arr);
}
编译运行以上 Rust 代码，输出结果如下

Inside update [0, 0, 0]
Inside main [10, 20, 30]

## 范例2: 引用传递
下面的代码，我们使用引用方式将数组传递给函数做参数。函数对参数的任何修改都会影响到原来的数组

fn main() {
   let mut arr = [10,20,30];
   update(&mut arr);
   println!("Inside main {:?}",arr);
}
fn update(arr:&mut [i32;3]){
   for i in 0..3 {
      arr[i] = 0;
   }
   println!("Inside update {:?}",arr);
}
编译运行以上 Rust 代码，输出结果如下

Inside update [0, 0, 0]
Inside main [0, 0, 0]
# Rust 切片 slice
一个 切片（ slice ） 就是指向一段 内存 的指针。

因此 切片 可用于访问内存块中 连续区间内的数据。

一般情况下，能够在内存中连续区间存储数据的 数据结构 有: 数组 array、向量 vector、字符串 string。

也就是说，切片 可以和数组、向量、字符串一起使用，它使用 数字索引 （类似于数组的下标索引）来访问它所指向的数据。

例如，切片 可以和字符串一起使用，切片 可以指向字符串中连续的一部分。这种 字符串切片 实际上是指向字符串的指针。因为是指向字符串的连续区间，所以我们要指定字符串的开始和结束位置。

访问切片内容的时候，下标索引是从 0 开始的。

切片 的大小是运行时才可知的，并不是数组那种编译时就必须告知的。

定义切片的语法
经过上面晦涩难懂的解释，我们知道切片就是指向数组、向量、字符串的连续区间。

定义一个切片的语法格式如下

let sliced_value = &data_structure[start_index..end_index]
定义切片时的几个注意事项：

[start_index..end_index] 是一个左闭又开区间 [start_index,end_index)

要注意区间的语法两个点 .. 。

start_index 的最小值为 0，这是因为数组、向量、字符串它们的下标访问方式也是从 0 开始的。

end_index 的最大值是数组、向量、字符串的长度。

end_index 所表示的索引的字符并不包含在切片里面。

## 切片实例
← Rust 借用所有权 Borrowing / 引用Rust 结构体 →
Rust 切片 slice
一个 切片（ slice ） 就是指向一段 内存 的指针。

因此 切片 可用于访问内存块中 连续区间内的数据。

一般情况下，能够在内存中连续区间存储数据的 数据结构 有: 数组 array、向量 vector、字符串 string。

也就是说，切片 可以和数组、向量、字符串一起使用，它使用 数字索引 （类似于数组的下标索引）来访问它所指向的数据。

例如，切片 可以和字符串一起使用，切片 可以指向字符串中连续的一部分。这种 字符串切片 实际上是指向字符串的指针。因为是指向字符串的连续区间，所以我们要指定字符串的开始和结束位置。

访问切片内容的时候，下标索引是从 0 开始的。

切片 的大小是运行时才可知的，并不是数组那种编译时就必须告知的。

定义切片的语法
经过上面晦涩难懂的解释，我们知道切片就是指向数组、向量、字符串的连续区间。

定义一个切片的语法格式如下

let sliced_value = &data_structure[start_index..end_index]
定义切片时的几个注意事项：

[start_index..end_index] 是一个左闭又开区间 [start_index,end_index)

要注意区间的语法两个点 .. 。

start_index 的最小值为 0，这是因为数组、向量、字符串它们的下标访问方式也是从 0 开始的。

end_index 的最大值是数组、向量、字符串的长度。

end_index 所表示的索引的字符并不包含在切片里面。

切片图例
数组、向量、字符串在内存中是连续存储的，一个字符串 Tutorials 在内存中的存储类似于下图

String Tutorials

从图中很直观的可以看出，字符串 Tutorials 的长度为 9，第一个字符的下标索引为 0，最后一个字符的下标索引为 8。

如果我们想访问字符串 Tutorials 中第 4 个字符开始的连续 5 个字符，使用切片，我们可以这么做
## 切片实例1
fn main() {
   let mystr="Tutorials".to_string();
   let myslice=&mystr[2..7];
   println!("{:?}",myslice);
     
  }
## 切片实例2，切片转为函数参数  
fn main() {
   let n1 = "Tutorials".to_string();
   println!("length of string is {}",n1.len());
   let c1 = &n1[4..9]; 

   // fetches characters at 4,5,6,7, and 8 indexes
   println!("{}",c1);
}

编译运行以上 Rust 代码，输出结果如下

length of string is 9
rials
## 切片实例3 从数组中获取切片并且利用iter()迭代器循环输出切片的元素
fn main() {
   let arr=[1,2,3,4,5,6,7];
   let arrslice=&arr[2..6];
   for val in arrslice.iter(){
       println!("value is {}",val);
   }
     
  }
 ### 结果：
 value is 3
value is 4
value is 5
value is 6

# 可变更切片
默认情况下 切片 是不可变更的。

虽然，看起来切片是指向原数据，但是默认情况下我们并不能改变切片的元素。

也就说默认情况下不能通过更改切片的元素来影响原数据。

但这不是绝对的，如果我们声明的原数据是可变的，同时定义切片的时候添加了 &mut 关键字，那么我们就可以通过更改切片的元素来影响原数据。

fn main(){
   let mut data = [10,20,30,40,50];
   use_slice(&mut data[1..4]);
   // passes references of 
   20, 30 and 40
   println!("{:?}",data);
}
fn use_slice(slice:&mut [i32]) {
   println!("切片的长度为：{:?}",slice.len());
   println!("{:?}",slice);
   slice[0] = 1010; // replaces 20 with 1010
}
编译运行以上 Rust 代码，输出结果如下

切片的长度为：3
[20, 30, 40]
[10, 1010, 30, 40, 50]
从上面的代码中可以看出，只要原数据是可变的，且切片声明时添加了 &mut 关键字，那么切片就是可变更的。


