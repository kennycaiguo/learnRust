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
  
