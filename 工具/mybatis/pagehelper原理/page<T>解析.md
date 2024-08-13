在page<T>中有很多的this，如下直接返回一个集合this，是因为他整个类本身就继承自ArrayList<T>

```
public List<E> getResult() {
    return this;
}
```



`total` 通常表示满足查询条件的总记录数,用来计算总页数

`result`表示所有的内容
