# CMU15545 Project0



实验的出现的bug
=====

首先异常必须要使用throw 这个关键，否则会继续执行下一行代码，这样异常的检测就没有用了，而且如果不使用throw有些不会报错，但是测试用例过不去


第二在构造函数的时候，new二级指针要使用一下的形式，同时析构函数要以相反的顺序进行析构

``` c++
    this->data_ = new T *[rows];
    for(int i=0;i<rows;i++){
      data_[i] = new T[cols];
    }
```

第三再对长度进行比较时要使用static_cast<int>转换，不然会报错，如：
``` C++
void FillFrom(const std::vector<T> &source) override {
    if(static_cast<int>(source.size()) != this->rows_ * this->cols_)
      throw bustub::Exception(bustub::ExceptionType::OUT_OF_RANGE,"out of range");
    
    for(int i=0;i<static_cast<int>(source.size());++i){
      int rows = i / this->cols_;
      int cols = i % this->cols_;
      SetElement(rows, cols, source[i]);
    }
  }
```