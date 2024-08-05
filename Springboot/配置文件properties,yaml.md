驼峰

只有双引号有转译字符

![image-20240802100312765](/Users/elfish/Library/Application Support/typora-user-images/image-20240802100312765.png)

```yaml
people:
  age: 18
  name: 李四
  birth-day: 2022/10/10 12:00
  #birthDay 可以 写成 birth-day
  alive: false
  cat:
    id: 1
    name: cat01
  dogs:
    -
      name: dog01
      id: 01
    -
      name: dog02
      id: 02
    -
      name: dog03
      id: 03
  pig-map:
    pig01:
      name: pig01
      id: 1
    pig02:
      name: pig02
      id: 2
      #这里的map也可以这样
    pig-map: {pig01:{name:pig01,id:1}}
```

`｜` 保留文本格式

```properties
literal: |
  This is a multi-line string.
  Line breaks and spaces
  are preserved.
```

`>`压缩换行符成空格

```properties
folded: >
  This is a multi-line string.
  Line breaks are replaced
  with spaces.
```

`---`可以分割文档，尤其是在配置很多的时候，可以把同一个配置项放一起折叠起来，不容易眼花缭乱