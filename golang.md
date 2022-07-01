# Golang Advance
#### 1.golang判断结构体是否实现了某个接口
```go
type Lstater interface {
	LstatIfPossible(name string) (os.FileInfo, bool, error)
}

type OsFs struct{}

// 判断OsFs是否实现了Lstater接口
var _ Lstater = (*OsFs)(nil)
// var _ Lstater = OsFs{}
// var _ Lstater = &OsFs{}
// 其实就是变量的定义，_ 就是舍去变量不要，go中规定定义的变量都必须有使用的地方，但我们目的是判断类型是否实现了接口，不必使用变量。没有实现该接口类型则编译不通过.

func (OsFs) LstatIfPossible(name string) (os.FileInfo, bool, error) {
	fi, err := os.Lstat(name)
	return fi, true, err
}

// var _ Lstater = new(OsFs) 或 var _ Lstater = (*OsFs)(nil)
// 第一种需要分配内存，第二种不需要分配内存就能达到目的

```
