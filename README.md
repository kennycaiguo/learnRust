# learnRust

# rust 基本语法
# <a href="https://play.rust-lang.org/">rust在线工具</a>
# <a href="https://laplacedemon.gitbooks.io/-rust/content/">快学Rust</a>
# <a href="https://www.runoob.com/rust/rust-tutorial.html">Rust菜鸟教程</a>
# <a href="https://gitee.com/755157298/panda-zoo">rust数据库demo</a>
# rust 格式化输出
格式化输出
打印操作由 std::fmt 里面所定义的一系列宏来处理，包括：

format!：将格式化文本写到字符串（String）。（译注：字符串是返 回值不是参数。）
print!：与 format! 类似，但将文本输出到控制台（io::stdout）。
println!: 与 print! 类似，但输出结果追加一个换行符。
eprint!：与 format! 类似，但将文本输出到标准错误（io::stderr）。
eprintln!：与 eprint! 类似，但输出结果追加一个换行符。
这些宏都以相同的做法解析（parse）文本。另外有个优点是格式化的正确性会在编译时检查。
## 例子：
fn main() {
    // 通常情况下，`{}` 会被任意变量内容所替换。
    // 变量内容会转化成字符串。
    println!("{} days", 31);

    // 不加后缀的话，31 就自动成为 i32 类型。
    // 你可以添加后缀来改变 31 的类型。

    // 用变量替换字符串有多种写法。
    // 比如可以使用位置参数。
    println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob");

    // 可以使用命名参数。
    println!("{subject} {verb} {object}",
             object="the lazy dog",
             subject="the quick brown fox",
             verb="jumps over");

    // 可以在 `:` 后面指定特殊的格式。
    println!("{} of {:b} people know binary, the other half don't", 1, 2);

    // 你可以按指定宽度来右对齐文本。
    // 下面语句输出 "     1"，5 个空格后面连着 1。
    println!("{number:>width$}", number=1, width=6);

    // 你可以在数字左边补 0。下面语句输出 "000001"。
    println!("{number:>0width$}", number=1, width=6);

    // println! 会检查使用到的参数数量是否正确。
    println!("My name is {0}, {1} {0}", "Bond"，"James");
    // 改正 ^ 补上漏掉的参数："James"

    // 创建一个包含单个 `i32` 的结构体（structure）。命名为 `Structure`。
    #[allow(dead_code)]
    struct Structure(i32);

    // 但是像结构体这样的自定义类型需要更复杂的方式来处理。
    // 下面语句无法运行。
    println!("This struct `{}` won't print...", Structure(3));
    // 改正 ^ 注释掉此行。
}

# Rust 字符串
Rust 语言提供了两种字符串

字符串字面量 &str。它是 Rust 核心内置的数据类型。

字符串对象 String。它不是 Rust 核心的一部分，只是 Rust 标准库中的一个 公开 pub 结构体。

## 字符串字面量 &str
字符串字面量 &str 就是在 编译时 就知道其值的字符串类型，是 Rust 语言核心的一部分。

字符串字面量 &str 是字符的集合，被硬编码赋值给一个变量。

let name1 = "你好，简单教程 简单编程";
字符串字面量的核心代码可以在模块 std::str 中找到，如果你有兴趣，可以阅读一二。

Rust 中的字符串字面量被称之为 字符串切片。因为它的底层实现是 切片。

下面的代码，我们定义了两个字符串字面量 company 和 location

fn main() {
   let company:&str="简单教程";
   let location:&str = "中国";
   println!("公司名 : {} 位于 :{}",company,location);
}
## 字符串对象
字符串对象是 Rust 标准库提供的内建类型。

与字符串字面量不同的是：字符串对象并不是 Rust 核心内置的数据类型，它只是标准库中的一个 公开 pub 的结构体。

字符串对象在标准库中的定义语法如下

pub struct String
字符串对象是是一个 长度可变的集合，它是 可变 的而且使用 UTF-8 作为底层数据编码格式。

字符串对象在 堆 heap 中分配，可以在运行时提供字符串值以及相应的操作方法。

##创建字符串对象的语法
要创建一个字符串对象，有两种方法：

一种是创建一个新的空字符串，使用 String::new() 静态方法

String::new()
另一种是根据指定的字符串字面量来创建字符串对象，使用 String::from() 方法

String::from()

 范例
下面，我们分别使用 String::new() 方法和 String::from() 方法创建字符串对象，并输出字符串对象的长度

fn main(){
   let empty_string = String::new();
   println!("长度是 {}",empty_string.len());

   let content_string = String::from("简单教程");
   println!("长度是 {}",content_string.len());
}
编译运行以上 Rust 代码，输出结果如下

长度是 0
长度是 12
 
## 字符串对象常用的方法
方法	原型	说明
new()	pub const fn new() -> String	创建一个新的字符串对象
to_string()	fn to_string(&self) -> String	将字符串字面量转换为字符串对象
replace()	pub fn replace<'a, P>(&'a self, from: P, to: &str) -> String	搜索指定模式并替换
as_str()	pub fn as_str(&self) -> &str	将字符串对象转换为字符串字面量
push()	pub fn push(&mut self, ch: char)	再字符串末尾追加字符
push_str()	pub fn push_str(&mut self, string: &str)	再字符串末尾追加字符串
len()	pub fn len(&self) -> usize	返回字符串的字节长度
trim()	pub fn trim(&self) -> &str	去除字符串首尾的空白符
split_whitespace()	pub fn split_whitespace(&self) -> SplitWhitespace	根据空白符分割字符串并返回分割后的迭代器
split()	pub fn split<'a, P>(&'a self, pat: P) -> Split<'a, P>	根据指定模式分割字符串并返回分割后的迭代器。模式 P 可以是字符串字面量或字符或一个返回分割符的闭包
chars()	pub fn chars(&self) -> Chars	返回字符串所有字符组成的迭代器 
### 原字符串后追加字符 push()
如果要在一个字符串后面追加字符则首先需要将该字符串声明为 可变 的，也就是使用 mut 关键字。然后再调用 push() 方法。

push() 是在原字符上追加，而不是返回一个新的字符串

fn main(){
   let mut company = "简单教程".to_string();
   company.push('t');
   println!("{}",company);
}
编译运行以上 Rust 代码，输出结果如下

简单教程t
原字符串后追加字符串 push_str()
如果要在一个字符串后面追加字符串则首先需要将该字符串声明为 可变 的，也就是使用 mut 关键字。然后再调用 push_str() 方法。

push_str() 是在原字符上追加，而不是返回一个新的字符串

fn main(){
   let mut company = "简单教程".to_string();
   company.push_str(" 简单编程");
   println!("{}",company);
}
编译运行以上 Rust 代码，输出结果如下

简单教程 简单编程
 
## trim() 方法实例
fn main() {
   let mut mystr=String::from("   i like juicy pussy    ");
  
   println!("length of string is :{}",mystr.len());
     mystr.trim();
     println!("the new length of string is :{}",mystr.trim().len());
}

length of string is :25
the new length of string is :18
## split_whitespace()实例
fn main() {
   let mut mystr=String::from("i like juicy patty");
   let mut i=1;
   
    for part in mystr.split_whitespace(){
        println!("part {} is :{}",i,part);
    }
   
     
}
## split实例
fn main() {
   let mut mystr=String::from("i like juicy patty");
   let mut i=1;
   
    for part in mystr.split(" "){
        println!("part {} is :{}",i,part);
    }
   
     
}
## split() 方法最大的缺点是不可重入迭代，也就是迭代器一旦使用，则需要重新调用才可以再用。

但我们可以先在迭代器上调用 collect() 方法将迭代器转换为 向量 Vector ，这样就可以重复使用了。

fn main() {
   let fullname = "李白，诗仙，唐朝";

   for token in fullname.split("，"){
      println!("token is {}",token);
   }

   // 存储在一个向量中
   println!("\n");
   let tokens:Vec<&str>= fullname.split("，").collect();
   println!("姓名 is {}",tokens[0]);
   println!("称号 {}",tokens[1]);
   println!("朝代 {}",tokens[2]);
}
编译运行以上 Rust 代码，输出结果如下

token is 李白
token is 诗仙
token is 唐朝


姓名 is 李白
称号 诗仙
朝代 唐朝

## 将字符串打散为字符数组 chars()
如果要将一个字符串打散为所有字符组成的数组，可以使用 chars() 方法。

从某些方面说，如果我们要迭代字符串中的每一个字符，则必须首先将它打散为字符数组，然后才能遍历。

fn main(){
   let n1 = "简单教程 www.twle.cn".to_string();

   for n in n1.chars(){
      println!("{}",n);
   }
}

字符串连接符 + 的内部实现
字符串连接符 + 的内部实现，其实是重写了 add() 方法。该方法接受两个参数，第一个参数是当前的字符串对象 self ，也就是 + 左边的字符串，第二个参数是一个 引用，它指向了 + 右边的字符串。
范例
下面的代码，我们使用 字符串拼接符 + 将连个字符串变量拼接成一个新的字符串

fn main(){
   let n1 = "简单教程".to_string();
   let n2 = "简单编程".to_string();

   let n3 = n1 + &n2; // 需要传递 n2 的引用，注意：这里n1已经是不可用的了，因为方式了所有权转移
   println!("{}",n3);
}
编译运行以上 Rust 代码，输出结果如下

简单教程 简单编程
## 如果需要将其它类型转换为字符串类型，可以直接调用 to_string() 方法。

例如可以调用一个数字类型的变量的 to_string() 方法将当前变量转换为字符串类型。
   let number = 2020;
   let number_as_string = number.to_string(); 

   // 转换数字为字符串类型
   println!("{}",number_as_string);
   println!("{}",number_as_string=="2020");
}
编译运行以上 Rust 代码，输出结果如下

2020
true

## 格式化宏 format!
如果要把不同的变量或对象拼接成一个字符串，我们可以使用 格式化宏 ( format! )

格式化宏 format! 的使用方法如下

fn main(){
   let n1 = "简单教程".to_string();
   let n2 = "简单编程".to_string();
   let n3 = format!("{} {}",n1,n2);
   println!("{}",n3);
}
编译运行以上 Rust 代码，输出结果如下

简单教程 简单编程
 
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
## if条件实例3
fn main() {
    let a = 3;
    let number = if a > 0 { 1 } else { -1 };
    println!("number 为 {}", number);
}


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
loop 语句代表着一种死循环。它没有循环条件，也没有循环次数，它就是一个永动机，只能按ctrl+c强制终止循环或和break结合使用，
### loop循环实例1
fn main() {
     let mut countr=0;
    let result = loop {
        countr+=1;
        if countr==20{
            break countr*2 //终止循环并且将countr的值乘于2返回
        }
    };
    println!("result={}",result);
}
结果：result=40

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
## 实例1
fn main() {
    let s="Hello, World!";
    //let s1 = &s[0..5]; //获取切片s1，注意：是包头不包尾
   // let s1 = &s[0..=4]; //获取切片s1，这样子就可以包尾
    let s1 = &s[..=4]; //获取切片s1，这样子就可以包尾，这样子写表示从0开始
    //let s2 = &s[6..12];//
    let s2 = &s[6..];//这样子也行
    let s3 = &s[..];//这个表示将整个字符串作为切片
    println!("s1={}",s1);
    println!("s2={}",s2);
    println!("s3={}",s3);
    let mut str1 = s1.to_string();
    str1.push_str(s2);
    println!("str1={}",str1);
}
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

# Rust结构体
## 范例
下面的代码，我们定义了一个结构体 Employee ，它有着三个元素/字段，分别是姓名、年龄、公司。

struct Employee {
   name:String,
   company:String,
   age:u32
}

## 结构体初始化语法
let instance_name = Name_of_structure {
   field1:value1,
   field2:value2,
   field3:value3
}; 
从语法中可以看出，初始化结构体时的等号右边，就是把定义语法中的元素类型换成了具体的值。

结构体初始化，其实就是对 结构体中的各个元素进行赋值。

注意
千万不要忘记结尾的分号 ;
范例
下面的代码，我们定义了一个有三个元素的结构体 Employee，然后初始化一个实例 emp1，最后通过 元素访问符 来访问 emp1 的三个元素。

struct Employee {
   name:String,
   company:String,
   age:u32
}

fn main() {
   let emp1 = Employee {
      company:String::from("TutorialsPoint"),
      name:String::from("Mohtashim"),
      age:50
   };
   println!("Name is :{} company is {} age is {}",emp1.name,emp1.company,emp1.age);
}
编译运行以上 Rust 代码，输出结果如下

Name is :Mohtashim company is TutorialsPoint age is 50
## 修改结构体实例
修改结构体实例就是对结构体的个别元素 重新赋值。

结构体实例默认是 不可修改的，因为结构体实例也是一个使用 let 定义的变量。

如果要修改结构体实例，就必须在创建时添加 mut 关键字，让它变成可修改的。
范例
下面的范例给 Employee 的实例 emp1 添加了 mut 关键字，因此我们可以修改 emp1 的内部元素。

struct Employee {
   name:String,
   company:String,
   age:u32
}

let mut emp1 = Employee {
   company:String::from("TutorialsPoint"),
   name:String::from("Mohtashim"),
   age:50
};
emp1.age = 40;
println!("Name is :{} company is {} age is 
{}",emp1.name,emp1.company,emp1.age);
编译运行以上 Rust 代码，输出结果如下

Name is :Mohtashim company is TutorialsPoint age is 40
## 结构体作为函数的参数
结构体的用途之一就是可以作为参数传递给函数。

定一个结构体参数和定义其它类型的参数的语法是一样的。我们这里就不多介绍了，直接看范例

下面的代码定义了一个函数 display ，它接受一个 Employee 结构体实例作为参数并输出结构体的所有元素

fn display( emp:Employee) {
   println!("Name is :{} company is {} age is 
   {}",emp.name,emp.company,emp.age);
}
完整的可运行的实例代码如下

//定义一个结构体
struct Employee {
   name:String,
   company:String,
   age:u32
}
fn main() {
   //初始化结构体
   let emp1 = Employee {
      company:String::from("TutorialsPoint"),
      name:String::from("Mohtashim"),
      age:50
   };
   let emp2 = Employee{
      company:String::from("TutorialsPoint"),
      name:String::from("Kannan"),
      age:32
   };
   //将结构体作为参数传递给 display
   display(emp1);
   display(emp2);
}

// 使用点号(.) 访问符访问结构体的元素并输出它么的值
fn display( emp:Employee){
   println!("Name is :{} company is {} age is 
   {}",emp.name,emp.company,emp.age);
}
编译运行以上 Rust 代码，输出结果如下

Name is :Mohtashim company is TutorialsPoint age is 50
Name is :Kannan company is TutorialsPoint age is 32
## 结构体实例作为函数的返回值
Rust 中的结构体不仅仅可以作为函数的参数，还可以作为 函数的返回值。

函数返回结构体实例需要实现两个地方：

在 箭头 -> 后面指定结构体作为一个返回参数。
在函数的内部返回 结构体的实例
结构体实例作为函数的返回值的语法格式
struct My_struct {}

fn function_name([parameters]) -> My_struct {
   // 其它的函数逻辑
   return My_struct_instance;
}
范例
下面的代码，我们首先定义一个结构体 Employee ，接着定义一个方法 who_is_elder ，传入两个结构体 Employee 作为参数并返回年龄个大的那个。

fn main() {

   let emp1 = Employee{
      company:String::from("TutorialsPoint"),
      name:String::from("Mohtashim"),
      age:50
   };
   let emp2 = Employee {
      company:String::from("TutorialsPoint"),
      name:String::from("Kannan"),
      age:32
   };
   let elder = who_is_elder(emp1,emp2);
   println!("elder is:");

   display(elder);
}

//接受两个 Employee 的实例作为参数并返回年长的那个
fn who_is_elder (emp1:Employee,emp2:Employee)->Employee {
   if emp1.age>emp2.age {
      return emp1;
   } else {
      return emp2;
   }
}

// 显示结构体的所有元素
fn display( emp:Employee) {
   println!("Name is :{} company is {} age is {}",emp.name,emp.company,emp.age);
}

// 定义一个结构体
struct Employee {
   name:String,
   company:String,
   age:u32
}
编译运行以上 Rust 代码，输出结果如下

elder is:
Name is :Mohtashim company is TutorialsPoint age is 50

## 结构体中的方法
Rust 中的结构体可以定义 方法 ( method )。

方法 ( method ) 是一段代码的 逻辑组合，用于完成某项特定的任务或实现某项特定的功能。

方法（ method ） 和 函数（ function） 有什么不同之处呢？

简单的说：

函数（ function） 没有属主，也就是归属于谁，因此可以直接调用。
方法（ method ） 是有属主的，调用的时候必须指定 属主。
函数（ function） 没有属主，同一个程序不可以出现两个相同签名的函数。
方法（ method ） 有属主，不同的属主可以有着相同签名的方法。
定义方法时需要使用 fn 关键字。

fn 关键字是 function 取头尾两个字母的缩写。

结构体方法的 作用域 仅限于 结构体内部。

与 C++ 语言 中的结构体的方法不同的是，Rust 中的结构体方法只能定义在结构体的外面。

在定义结构体方法时需要使用 impl 关键字，语法格式如下

struct My_struct {}

impl My_struct { 
   // 属于结构体的所有其它代码
}
impl 关键字最重要的作用，就是定义上面我们所说的 方法的属主。所有被 impl My_struct 块包含的代码，都只属于 My_struct 这个结构。

impl 关键字是 implement 的前 4 个字母的缩写。意思是 实现。

结构体的普通方法（后面我们还会学到其它方法）时，第一个参数永远是 &self 关键字。self 是 自我 的意思，&self 永远表示着当前的结构体的一个实例。

这是不是可以带来其它的结构体方法的解释：结构体的方法就是用来操作当前结构体的一个实例的。

## 结构体方法的定义语法
定义结构体方法的语法格式如下

struct My_struct {}
impl My_struct { 

   // 定义一个结构体的普通方法
   fn method_name(&self[,other_parameters]) { 
      //方法的具体逻辑代码
   }

}
&self 是结构体普通方法固定的第一个参数，其它参数则是可选的。

即使结构体方法不需要传递任何参数，&self 也是固定的，必须存在的。

##结构体方法内部访问结构体元素
因为我们在定义方法时固定传递了 &self 关键字。而 &self 关键字又代表了当前方法的属主。

因此我们可以在方法内部使用 self. 来访问结构体的元素。
## 范例
下面的代码，我们首先定义了一个结构体 Rectangle 用于表示一个 长方形，它有宽高 两个元素 width 和 height。

然后我们又为 结构体 Rectangle 定义了一个方法 area 用于计算当前 长方形实例 的面积。

// 定义一个长方形结构体
struct Rectangle {
   width:u32, height:u32
}

// 为长方形结构体定义一个方法，用于计算当前长方形的面积
impl Rectangle {
   fn area(&self)->u32 {
      // 在方法内部，可以使用点号 `self.` 来访问当前结构体的元素。use the . operator to fetch the value of a field via the self keyword
      self.width * self.height
   }
}

fn main() {
   // 创建 Rectangle 结构体的一个实例
   let small = Rectangle {
      width:10,
      height:20
   };

   //计算并输出结构体的面积
   println!("width is {} height is {} area of Rectangle 
   is {}",small.width,small.height,small.area());
}
编译运行以上 Rust 代码，输出结果如下

width is 10 height is 20 area of Rectangle is 200

## 结构体的静态方法
Rust 中的结构体还可以有静态方法。

静态方法可以直接通过结构体名调用而无需先实例化。

结构体的静态方法定义方式和普通方法类似，唯一的不同点是 不需要使用 &self 作为参数。
### 定义静态方法的语法
结构体静态方法的定义语法格式如下

impl Structure_Name {

   // Structure_Name 结构体的静态方法
   fn method_name(param1: datatype, param2: datatype) -> return_type {
      // 方法内部逻辑
   }

}
静态方法和其它普通方法一样，参数是可选的。也就是可以没有参数

调用静态方法的语法
静态方法可以直接通过结构体名调用，而无需先实例化。

结构体的静态方法需要使用 structure_name:: 语法来访问，详细的语法格式如下

structure_name::method_name(v1,v2)
范例
下面的范例，我们为结构体 Point 定义了一个静态方法 getInstance()。

getInstance() 是一个 工厂方法，它初始化并返回结构体 Point 的实例。

//声明结构体 Point
struct Point {
   x: i32,
   y: i32,
}

impl Point {
   // 用于创建 Point 实例的静态方法
   fn getInstance(x: i32, y: i32) -> Point {
      Point { x: x, y: y }
   }
   // 用于显示结构体元素的普通方法
   fn display(&self){
      println!("x ={} y={}",self.x,self.y );
   }
}
fn main(){

   // 调用静态方法
   let p1 = Point::getInstance(10,20);
   p1.display();

}
编译运行以上 Rust 代码，输出结果如下

x =10 y=20


调试（Debug）,利用println！宏输出结构体变量
所有的类型，若想用 std::fmt 的格式化 trait 打印出来，都要求实现这个 trait。自动的实现只为一些类型提供，比如 std 库中的类型。所有其他类型 都必须手动实现。

fmt::Debug 这个 trait 使这项工作变得相当简单。所有类型都能推导（derive，即自 动创建）fmt::Debug 的实现。但是 fmt::Display 需要手动实现。



// 这个结构体不能使用 `fmt::Display` 或 `fmt::Debug` 来进行打印。
struct UnPrintable(i32);

// `derive` 属性会自动创建所需的实现，使这个 `struct` 能使用 `fmt::Debug` 打印。
#[derive(Debug)]
struct DebugPrintable(i32);

## 实例：
#[derive(Debug)] //如果想利用println！来输出结构体变量，必须在声明结构体前面加这个，否则报错
struct Person{
    name:String,
    age: u32,
    gender:String,
}
fn main() {
   
    let name = "Joe".to_string();
    let age= 20;
    let gender = "female".to_string();
    let mut p2 = Person{ //注意，默认是不能遍历结构体的属性的
        name,
        age,
        gender,
    };
    println!("{:?}",p2);
}

### 元组结构体
 //元组结构体,使用的是（）
 fn main(){
 
    #[derive(Debug)]
    struct User(String,String,i32);
    let u=User("Luis".to_string(),"male".to_string(),26);
    println!("{:?}",u);
    println!("name={}",u.0);
    println!("gender={}",u.1);
    println!("age={}",u.2);
}
结果：
User("Luis", "male", 26)
name=Luis
gender=male
age=26

# 没有任何字段的结构体(但是可以有方法)
## 实例
  //没有任何字段的结构体
  fn main{
    struct myStruct{} //这个结构体没有字段但是可以添加方法
     impl myStruct{
         fn add(&self,x:i32,y:i32)->i32{ //如果不是静态方法，需要&self，而且在第一位
          x+y
      }  //方法之间不需要分隔符
        fn sub(x:i32,y:i32)->i32{ //静态方法，不需要&self
            x-y
        }

     }
    let x = myStruct{};
    let res = x.add(10,20);
    let rs=myStruct::sub(30,10);//调用静态方法
    println!("result add={}，result sub={}",res,rs);
    
    }
# rust语言枚举
实例1
/*#[derive(Debug)]
enum Week{
    Mon,Tues,Wed,Thur,Fri,Sat,Sun
}*/
//c语言风格
#[derive(Debug)]
enum IpAddKind{
    v4,
    v6,
}

#[derive(Debug)]
struct IpAddr{
    kind:IpAddKind,
    address:String,
}
enum Message{
    Quit,
    Move{x: i32,y: i32},
    Write(String),
    Change(i32,i32,i32),
}
/*
等同于：
struct QuitMessage
struct MoveMessage{x: i32,y: i32,}
struct WriteMessage(String)
struct Change(i32,i32,i32)

*/
//枚举类型定义方法和结构体类似，也是用impl
//match的语法
impl Message{
    fn Print(&self){
        match *self {
            Message::Quit => println!("Quit Invoked..."),
            Message::Move{x, y} => println!("Move x={},y={}", x, y),
            Message::Change(x, y, z) => println!("Change x={},y={},z={}", x, y, z),
            _ => println!("Write"),
        };
    }
}

fn main() {
     /*let ip1 = IpAddr{
         kind:IpAddKind::v4,
         address:"192.168.1.100".to_string()
     };
    println!("ip1={:?}",ip1);
    */
    let q = Message::Quit;
    q.Print();
    let m = Message::Move { x: 10, y: 20};
    m.Print();
    let c =Message::Change(5,6,7);
    c.Print();
}
