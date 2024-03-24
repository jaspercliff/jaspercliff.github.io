# HashMap

## 遍历
在Java中，遍历`HashMap`可以通过几种不同的方式完成，每种方式适用于不同的场景和需求。以下是一些常见的遍历方法：

### 1. 使用`entrySet()`遍历键值对
这是遍历`HashMap`中所有键值对最常见也是最高效的方法，因为它直接访问了映射中的每个`Map.Entry`对象。

``` java
Map<String, Integer> map = new HashMap<>();
// 添加一些数据到map中
map.put("Apple", 1);
map.put("Banana", 2);
map.put("Cherry", 3);

for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " = " + entry.getValue());
}
```

### 2. 使用`keySet()`遍历所有键，然后获取每个键的值
如果你只对键感兴趣，或者需要在遍历时对每个键单独处理，可以使用这种方法。但如果需要同时访问键和值，这种方法比使用`entrySet()`效率低，因为每次获取值时都需要进行一次查找。

``` java
for (String key : map.keySet()) {
    Integer value = map.get(key);
    System.out.println(key + " = " + value);
}
```

### 3. 使用`values()`遍历所有值
如果你只需要处理值，而不关心每个值对应的键是什么，可以使用这种方法。

``` java
for (Integer value : map.values()) {
    System.out.println(value);
}
```

### 4. 使用Java 8的`forEach`方法
Java 8引入了一个新的`forEach`方法，它可以更简洁地遍历`HashMap`。

``` java
map.forEach((key, value) -> System.out.println(key + " = " + value));
```

这种方法使用了Lambda表达式，使代码更加简洁。`forEach`方法接收一个`BiConsumer`函数接口，这个接口对每个键值对执行给定的操作。

### 总结
选择哪种遍历方法取决于你的具体需求：
- 如果需要同时访问键和值，推荐使用`entrySet()`。
- 如果只需要访问键或只需要访问值，可以使用`keySet()`或`values()`。
- 如果喜欢更现代、更简洁的代码风格，可以使用Java 8的`forEach`方法。

