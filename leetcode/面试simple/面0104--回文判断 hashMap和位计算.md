##### Map的一些方法

HashMap类常用方法
（1）put(K key, V value)
（2）get(Object key) 
（3）size() 
（4）clear() 
（5）isEmpty ()
（6）remove(Object key)
（7）values()  得到只含value的集合
（8）keySet()   得到只含key的集合

（9）entrySet() 
（10）iterator 迭代器
a、与get()方法结合：
b、与entry对象结合

```java
//entrySet作用是把hashMap转化成一个Map.Entry<这里面的类型由你的map决定>类型的集合，可以更简便得遍历Map
HashMap<String,Integer> hashmap = new HashMap<>(256);
for(Map.Entry<String,Integer> entry:hashmap.entrySet()){
  sout("key="+entry.getKey()+"value="+entry.getValue())
}
```

```java
//iterator迭代器遍历
HashMap<String,Integer> hashmap = new HashMap<>(256);
//得先弄一个set
Set<String> set1 = hashmap.keyset();
Iterator<String> iterator = set1.iterator();
for(iterator.hasNext()){
  String key = iterator.next();  //这里是重点
  sout(key+":"+hashmap.get(key));
}
```



第一个方法

```java
  HashMap<Character, Integer> map = new HashMap<>(128);
        for(char c:s.toCharArray()){
            if(map.containsKey(c)){
                map.put(c, map.get(c)+1);
            }else {
            map.put(c, 1);
        }}
        int count = 0;
        for(int i:map.values()){
            if(i%2!=0){
                count++;
            }
            }
        if (count==1||count==0){
            return true;

        }else {return false;}


```



##### Long类型只有64位，当要包含所有的ASCII码时得要两个Long

##### Long和Integer里面的bitCount方法，可以计算二进制中1的个数





第二个方法

```java
class Solution {
    public boolean canPermutePalindrome(String s) {
        long front = 0, end = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) >= 64) {
                end ^= 1L << s.charAt(i) - 64;//这里是把所有ASCII码分成两部分，这里是大的那一部分
            } else {
                front ^= 1L << s.charAt(i);
            }
        }//异或操作，偶数是0，奇数是1，回文只允许一个奇数
        return Long.bitCount(front) + Long.bitCount(end) <= 1;
    }
}

```

