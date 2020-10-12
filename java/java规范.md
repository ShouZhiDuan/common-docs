# Java规范

## 1、JavaBean属性规范

```
规范中另一个特别的地方就是：
1.第二个字母为大写的属性名要区别对待。如果属性名的第二个字母是大写的，那么该属性名直接用作 getter/setter 方法中 get/set 的后部分，就是说大小写不变。
2.属性是首字母大写，次字母小写是，你永远都找不到它的 getter/setter 方法的。
3.对于 boolean 类型属性的 getter 方法是 isXxx() 还是 getXxx() 就自己决定了，isXxx() 应该更接近于自然语言，更顺溜些。
一般JavaBean属性以小写字母开头，驼峰命名格式，相应的 getter/setter 方法是 get/set 接上首字母大写的属性名。例如：属性名为userName，其对应的getter/setter 方法是 getUserName/setUserName。
但是，还有一些特殊情况：
1、如果属性名的第二个字母大写，那么该属性名直接用作 getter/setter 方法中 get/set 的后部分，就是说大小写不变。例如属性名为uName，方法是getuName/setuName。
2、如果属性名的前两个字母是大写（一般的专有名词和缩略词都会大写），也是属性名直接用作 getter/setter 方法中 get/set 的后部分。例如属性名为URL，方法是getURL/setURL。
3、如果属性名的首字母大写，也是属性名直接用作 getter/setter 方法中 get/set 的后部分。例如属性名为Name，方法是getName/setName，这种是最糟糕的情况，会找不到属性出错，因为默认的属性名是name。
4、如果属性名以"is"开头，则getter方法会省掉get，set方法会去掉is。例如属性名为isOK，方法是isOK/setOK。
需要注意的是有些开发工具自动生成的getter/setter方法，并没有考虑到上面所说的特例情况，会导致bug的产生。
我们在定义JavaBean的属性名时，应该尽量避免属性名的头两个字母中任意一个为大写以及属性名以"is"开头。
5、to see https://blog.csdn.net/Com_ma/article/details/82696156
```

