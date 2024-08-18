stream是把collections对象给转换成对象流，然后可以通过一些函数来对他们进行处理

#### map和collectors

```java
 Set<Long> itemIds= vos.stream().map(CartVO::getItemId).collect(Collectors.toSet());
```

`map`是把集合内的东西转换成指定的对象流 ，文档里方法使用是 `map(Function<? super T, ? extends R> mapper)`,意思是**传一个方法**，通过这方法来得到想要的类型,比如这里传的就是CartVO里面的getItemId方法【注意⚠️：这里传的是方法名】，在下面我再举一个更普遍的例子

```java
List<String> words = new ArrayList<>();
words.add("apple");
words.add("banana");
words.add("watermelon");
//现在要求把每一个单词的长度存到一个List里面
List<String> lengthofwords = words.stream().map(String::length).collect(Collectors.toList());
sout(lengthofwords)
//输出[5, 6, 10]
```

然后我们可以在collect方法之前，使用peek方法，可以用来让我们查看流内的情况

```java
map(String::length).peek(System.out::printf)
```

因为Map不属于collection类，所以collector里面没有转换成map的方法，只有 `toList`和 `toSet`

