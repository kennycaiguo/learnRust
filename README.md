# learnRust

# rust 基本语法
# <a href="https://play.rust-lang.org/">rust在线工具</a>
# <a href="https://laplacedemon.gitbooks.io/-rust/content/">快学Rust</a>
# <a href="https://www.runoob.com/rust/rust-tutorial.html">Rust菜鸟教程</a>
# <a href="https://gitee.com/755157298/panda-zoo">rust数据库demo</a>
# rust条件判断
我们写一个范例，使用 if 语句来模拟 如果数字大于 0 则输出 正数。
## 实例1
fn main(){
   let num:i32 = 5;
   if num > 0 {
      println!("正数");
   }
}
编译运行以上 Rust 代码，输出结果如下

正数
## 条件实例2
，使用 if else 语句来判断一个数是否偶数或奇数，如果是偶数则输出 偶数 如果是奇数则输出 奇数

fn main() {
   let num = 12;
   if num % 2==0 {
      println!("偶数");
   } else {
      println!("奇数");
   }
}
编译运行以上 Rust 代码，输出结果如下

偶数

## if可以嵌套，但是注意使用嵌套 if 语句，也就是 if...else if... 语句时需要牢记几个点：

任何一个 if 或者嵌套 if 语句可以有 0 个或 1 个 else 语句，但 else 语句必须出现在 if else 后面，也就是出现在最后。

任何一个 if 或者嵌套 if 语句可以有 0 个或多个 if else 语句，但所有的 if else 语句都必须出现在 else 语句之前。

一旦某个 else if 中的条件 boolean_expression1 返回 true，那么后面的 else if 和 else 语句都不会运行。
## 条件实例3
我们使用嵌套 if 语句来写一段代码，判断某个值是 大于、小于、等于 0。

fn main() {
   let num = 2 ;
   if num > 0 {
      println!("{} is positive",num);
   } else if num < 0 {
      println!("{} is negative",num);
   } else {
      println!("{} is neither positive nor negative",num) ;
   }
}
编译运行以上 Rust 代码，输出结果如下

2 is positive
# match 语句
match 语句用于检查 某个当前的值 是否匹配 一组/列值 中的某一个。

如果放到现实生活中，那么 match 语句类似于 老师点名 或者 银行叫号。当老师叫一个名字，比如 小明 时，叫 小明 的那个人就会应答，比如说 到。

如果你会 C 语言，那么 Rust 中的 match 表达式则类似于 C 语言中的 switch 语句。

对 match 语句有了个大概的印象之后，我们来看看 Rust 中的 switch 语句的语法格式

match 语句语法格式
Rust 中一个基本的 match 语句语法格式如下

match variable_expression {
   constant_expr1 => {
      // 语句;
   },
   constant_expr2 => {
      // 语句;
   },
   _ => {
      // 默认
      // 其它语句
   }
};
match 语句有返回值，它把 匹配值 后执行的最后一条语句的结果当作返回值。


let expressionResult = match variable_expression {
   constant_expr1 => {
      // 语句;
   },
   constant_expr2 => {
      // 语句;
   },
   _ => {
      // 默认
      // 其它语句
   }
};

## 注意：首先要说明的是 match 关键字后面的表达式不必括在括号中。也就是 variable_expression 不需要用一对 括号(()) 括起来。

其次，match 语句在执行的时候，会计算 variable_expression 表达式的值，然后把计算后的结果和每一个 constant_exprN 匹配，使用的是 全等于 也就是 === 来匹配。如果匹配成功则执行 => {} 里面的语句。

如果 variable_expression 表达式的值没有和任何一个 constant_exprN 匹配，那么它会默认匹配 _。

因此，当没有匹配时，默认会执行 _ => {} 中的语句。

match 语句有返回值，它把 匹配值 后执行的最后一条语句的结果当作返回值。

_ => {} 语句是可选的，也就是说 match 语句可以没有它。

如果只有一条语句，那么每个 constant_expr2 => {} 中的 {} 是可以省略的。
## match实例
范例
看起来 match 语句有点复杂，我们直接拿几个范例来说明下

fn main(){
   let state_code = "MH";
   let state = match state_code {
      "MH" => {println!("Found match for MH"); "Maharashtra"},
      "KL" => "Kerala",
      "KA" => "Karnadaka",
      "GA" => "Goa",
      _ => "Unknown"
   };
   println!("State name is {}",state);
}
编译运行以上 Rust 代码，输出结果如下

Found match for MH
State name is Maharashtra
### 上面的范例中，state_code 对应着语法中的 variable_expression，MH、KL、KA、GA 对应这语法中的 constant_expr1 、constant_expr2 等等。

因为我们的 variable_expression 的值为 MH 和值为 MH 的第一个 constant_expr1 匹配，因此会执行 {println!("Found match for MH"); "Maharashtra"}。 然后将执行的最后一条语句的结果，也就是 "Maharashtra" 作为整个表达式的值返回。

这样，我们的 state 变量就被赋值为 Maharashtra。
# 上面这个范例是匹配的情况，如果不匹配，那么就会执行 _ => 语句

fn main(){
   let state_code = "MS";
   let state = match state_code {
      "MH" => {println!("Found match for MH"); "Maharashtra"},
      "KL" => "Kerala",
      "KA" => "Karnadaka",
      "GA" => "Goa",
      _ => "Unknown"
   };
   println!("State name is {}",state);
}
编译运行以上 Rust 代码，输出结果如下

Unknown
State name is Unknown
# Rust中的循环
Rust 语言中也有三种表示 循环 的语句：

loop 语句。一种重复执行且永远不会结束的循环。
while 语句。一种在某些条件为真的情况下就会永远执行下去的循环。
for 语句。一种有确定次数的循环。
三种语句都能实现循环功能，只不过侧重点不一样。

从上面的描述中，根据循环是否可能结束，我们把循环分为两大类

能确定次数的循环，比如 for 循环。
满足条件就是永动机的循环。比如 while 循环。
死循环。比如 loop 循环。
## Rust 中的 for 循环只有 for..in 这种格式（如果数据类型支持迭代，如数组，切片等等，还可以使用iter迭代器）
 循环语句的语法格式
for temp_variable in lower_bound..upper_bound {
   // action 要重复执行的代码
}
lower_bound..upper_bound 用于指定循环区间，是一个左闭又开的区间，比如 1..3 则只有 1 和 2 不包含 3

temp_variable 是循环迭代的每一个元素。

temp_variable 变量的作用域仅限于 for...in 语句，超出则会报错
## for实例
fn main(){
   for x in 1..11{
      println!("x is {}",x);
   }
}
## while循环
while 循环
while 语句是一种只要条件为真就一直会重复执行下去的循环。

while 循环会在每次重复执行前先判断条件是否满足，满足则执行，不满足则退出。

while 语句的语法格式
while ( condition ) {
    // action 要重复执行的代码
}
condition 是一个表达式，返回的结果会转换为 布尔类型。只要 condition 返回真，那么循环就会一直执行。

范例： 基本的 while 循环
下面的代码，使用 while 循环重写下上面的代码，重复输出 1 到 11 之间的数字（不包括 11 ）

fn main(){
   let mut x = 1;
   while x < 11{
      println!("inside loop x value is {}",x);
      x+=1;
   }
   println!("outside loop x value is {}",x);
}
编译运行以上 Rust 代码，输出结果如下

inside loop x value is 1
inside loop x value is 2
inside loop x value is 3
inside loop x value is 4
inside loop x value is 5
inside loop x value is 6
inside loop x value is 7
inside loop x value is 8
inside loop x value is 9
inside loop x value is 10
outside loop x value is 11
看到最后的 outside loop x value is 11 没，因为当 x 递增到 11 就不再满足条件 x < 11 了。

## loop循环
loop 循环
loop 语句代表着一种死循环。它没有循环条件，也没有循环次数，它就是一个永动机，只能按ctrl+c强制终止循环或和break结合使用
我们使用 break 语句改造下我们的 loop 循环，在 x 大于 11 就退出循环。

也就是使用 loop 循环实现 while 循环

fn main(){
   let mut x = 0;
   loop {
      x+=1;
      if x > 10 {
        break;
      }
      println!("x={}",x);
   }
}
编译运行以上 Rust 代码，输出结果如下

x=1
x=2
x=3
x=4
x=5
x=6
x=7
x=8
x=9
x=10

## 循环控制语句 continue
break 语句让我们尝到了甜头，有时候我们就会突发奇想，有没有另一个关键字，不像 break 语句那样直接退出整个循环，而仅仅是退出当前循环。也就是剩下的语句不执行了，开始下一个迭代。

创造了那些语言的前辈们，自然也会有这个想法，于是造出了 continue 语句。

continue 语句，简单的说，就是停止执行剩下的语句，直接进入下一个循环。
## continue范例
下面的代码，我们使用 for 循环输出 1 到 11 之间的数字，但是跳过数字 5

fn main(){
    for x in 1..11{
        if 5 == x {
            continue;
        }
        println!("x is {}",x);
    }
}
编译运行以上 Rust 代码，输出结果如下

x is 1
x is 2
x is 3
x is 4
x is 6
x is 7
x is 8
x is 9
x is 10
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


