# learnRust

# rust 基本语法
# rust 函数实例
fn main() {
       let x=10;
       let y=20;
       
      println!("{}+{}={}",x,y,add(x,y));
    }
fn add(x:i32,y:i32) -> i32{ //rust中用->i32表示函数返回值，函数可以在调用语句后面声明
    return x+y;
}  
