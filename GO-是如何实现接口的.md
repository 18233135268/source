 Q ：GO 是如何实现接口的

A:
    从语法上看，Interface定义了一个或一组method(s)，这些method(s)只有函数签名，没有具体的实现代码（有没有联想起C++中的虚函数？）。若某个数据类型实现了Interface中定义的那些被称为"methods"的函数，则称这些数据类型实现（implement）了interface。

例如：

type Abser interface {
    Abs() float64
}

type MyFloat float64

func (f MyFloat) Abs() float64 {
    if f < 0 {
        return float64(-f)
    }
    return float64(f)
}

上面的代码中，通过type语法声明了一个名为Abser的interface类型（Go中约定的interface类型名通常取其内部声明的method名的er形式）而第通过type语法声明了MyFloat类型且为该类型定义了名为Abs()的method。
根据上面的解释，Abs()是interface类型Abser定义的方法，而MyFloat实现了该方法，所以，MyFloat实现了Abser接口。