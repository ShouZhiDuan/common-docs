### 阅读目录

- [一、工具准备](https://blog.csdn.net/u013490280/article/details/107853908#_4)
- [二、开始解读](https://blog.csdn.net/u013490280/article/details/107853908#_14)
- - [2.1、代码](https://blog.csdn.net/u013490280/article/details/107853908#21_15)
  - - [2.1.1、Java 源码](https://blog.csdn.net/u013490280/article/details/107853908#211Java__16)
    - [2.1.2、class 文件源码](https://blog.csdn.net/u013490280/article/details/107853908#212class__36)
  - [2.2、开始解读](https://blog.csdn.net/u013490280/article/details/107853908#22_39)
  - - [2.2.1 magic](https://blog.csdn.net/u013490280/article/details/107853908#221_magic_68)
    - [2.2.2 minor_version](https://blog.csdn.net/u013490280/article/details/107853908#222_minor_version_81)
    - [2.2.3 major_version](https://blog.csdn.net/u013490280/article/details/107853908#223_major_version_91)
    - [2.2.4 constant_pool_count](https://blog.csdn.net/u013490280/article/details/107853908#224_constant_pool_count_107)
    - [2.2.5 constant_pool[constant_pool_count-1\]](https://blog.csdn.net/u013490280/article/details/107853908#225_constant_poolconstant_pool_count1_121)
    - - [2.2.5.1 #1](https://blog.csdn.net/u013490280/article/details/107853908#2251_1_154)
      - [2.2.5.2 #2](https://blog.csdn.net/u013490280/article/details/107853908#2252_2_174)
      - [2.2.5.3 #3](https://blog.csdn.net/u013490280/article/details/107853908#2253_3_195)
      - [2.2.5.4 #4](https://blog.csdn.net/u013490280/article/details/107853908#2254_4_213)
      - [2.2.5.5 #5](https://blog.csdn.net/u013490280/article/details/107853908#2255_5_231)
      - [2.2.5.6 #6](https://blog.csdn.net/u013490280/article/details/107853908#2256_6_252)
      - [2.2.5.7 #7](https://blog.csdn.net/u013490280/article/details/107853908#2257_7_272)
      - [2.2.5.8 #8](https://blog.csdn.net/u013490280/article/details/107853908#2258_8_292)
      - [2.2.5.9 #9](https://blog.csdn.net/u013490280/article/details/107853908#2259_9_312)
      - [2.2.5.10 #10](https://blog.csdn.net/u013490280/article/details/107853908#22510_10_331)
      - [2.2.5.11 #11](https://blog.csdn.net/u013490280/article/details/107853908#22511_11_352)
      - [2.2.5.12 #12](https://blog.csdn.net/u013490280/article/details/107853908#22512_12_373)
      - [2.2.5.13 #13](https://blog.csdn.net/u013490280/article/details/107853908#22513_13_394)
      - [2.2.5.14 #14](https://blog.csdn.net/u013490280/article/details/107853908#22514_14_416)
      - [2.2.5.15 #15](https://blog.csdn.net/u013490280/article/details/107853908#22515_15_435)
      - [2.2.5.16 #16](https://blog.csdn.net/u013490280/article/details/107853908#22516_16_455)
      - [2.2.5.17 #17](https://blog.csdn.net/u013490280/article/details/107853908#22517_17_475)
      - [2.2.5.18 #18](https://blog.csdn.net/u013490280/article/details/107853908#22518_18_496)
      - [2.2.5.19 #19](https://blog.csdn.net/u013490280/article/details/107853908#22519_19_518)
      - [2.2.5.20 #20](https://blog.csdn.net/u013490280/article/details/107853908#22520_20_537)
      - [2.2.5.21 #21](https://blog.csdn.net/u013490280/article/details/107853908#22521_21_559)
    - [2.2.6 access_flags](https://blog.csdn.net/u013490280/article/details/107853908#226_access_flags_579)
    - [2.2.7 this_class](https://blog.csdn.net/u013490280/article/details/107853908#227_this_class_612)
    - [2.2.8 super_class](https://blog.csdn.net/u013490280/article/details/107853908#228_super_class_630)
    - [2.2.9 interfaces_count](https://blog.csdn.net/u013490280/article/details/107853908#229_interfaces_count_650)
    - [2.2.10 interfaces[interfaces_count\]](https://blog.csdn.net/u013490280/article/details/107853908#2210_interfacesinterfaces_count_667)
    - [2.2.11 fields_count](https://blog.csdn.net/u013490280/article/details/107853908#2211_fields_count_681)
    - [2.2.12 fields[fields_count\]](https://blog.csdn.net/u013490280/article/details/107853908#2212_fieldsfields_count_698)
    - - [2.2.12.1 #1](https://blog.csdn.net/u013490280/article/details/107853908#22121_1_749)
    - [2.2.13 methods_count](https://blog.csdn.net/u013490280/article/details/107853908#2213_methods_count_772)
    - [2.2.14 methods[methods_count\]](https://blog.csdn.net/u013490280/article/details/107853908#2214_methodsmethods_count_789)
    - - [2.2.14.1 #1](https://blog.csdn.net/u013490280/article/details/107853908#22141_1_840)
      - [2.2.14.2 #2](https://blog.csdn.net/u013490280/article/details/107853908#22142_2_985)
    - [2.2.15 attributes_count](https://blog.csdn.net/u013490280/article/details/107853908#2215__attributes_count_1130)
    - [2.2.16 attributes[attributes_count\]](https://blog.csdn.net/u013490280/article/details/107853908#2216_attributesattributes_count_1146)
    - - [2.2.16.1 #1](https://blog.csdn.net/u013490280/article/details/107853908#22161_1_1174)
  - [2.3 javap 工具结果](https://blog.csdn.net/u013490280/article/details/107853908#23_javap__1202)
- [参考](https://blog.csdn.net/u013490280/article/details/107853908#_1278)



# 一、工具准备

> 介绍编译环境和工具。

- JDK 8
- IDEA
- WinHex (查看class文件内容，下载地址：http://www.x-ways.net/winhex/)
- javap（查看和验证最后结果，JDK自带工具）
- Java 虚拟机规范 （https://docs.oracle.com/javase/specs/jvms/se8/html/index.html）

# 二、开始解读

## 2.1、代码

### 2.1.1、Java 源码

```java
package com.hyl.learnerJVM.classtest;

/**
 * class测试类
 *
 * @author hyl
 * @version v1.0: ClassTest.java, v 0.1 2020/8/7 8:03 $
 */
public class ClassTest {

    private long n;

    public long inLong() {
        return n + 1;
    }
}123456789101112131415
```

### 2.1.2、class 文件源码

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200807082511767.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTM0OTAyODA=,size_16,color_FFFFFF,t_70)

## 2.2、开始解读

> 首先需要了解 class 文件的整体结构。

根据《Java 虚拟机规范》结构如下

```
ClassFile {
    u4             magic;
    u2             minor_version;
    u2             major_version;
    u2             constant_pool_count;
    cp_info        constant_pool[constant_pool_count-1];
    u2             access_flags;
    u2             this_class;
    u2             super_class;
    u2             interfaces_count;
    u2             interfaces[interfaces_count];
    u2             fields_count;
    field_info     fields[fields_count];
    u2             methods_count;
    method_info    methods[methods_count];
    u2             attributes_count;
    attribute_info attributes[attributes_count];
}
123456789101112131415161718
```

来自 https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html#jvms-4.1

接下来按照这个结构顺序解读。

### 2.2.1 magic

u4：4 个字节

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000000   CA FE BA BE
12
```

**魔数**（Magic Number），唯一作用是确定这个文件是否为一个能被虚拟机接受的 Class 文件。（“cafe babe” 和 “Java” 也算是个彩蛋）

官方说明：

> The magic item supplies the magic number identifying the class file format; it has the value 0xCAFEBABE.

### 2.2.2 minor_version

u2：2 个字节

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000000               00 00
12
```

**次版本号**，曾经在 Java 2 中出现过，以后，就再也没有被使用过了，基本上固定为零了。

### 2.2.3 major_version

u2：2 个字节

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000000                     00 34
12
```

**主版本号**，Java 版本从 45 开始，JDK 1.1 以后每个大版本加 1 ，这里 52（0x34）就是 JDK1.8 的意思。

官方说明：

> The values of the minor_version and major_version items are the minor and major version numbers of this class file. Together, a major and a minor version number determine the version of the class file format. If a class file has major version number M and minor version number m, we denote the version of its class file format as M.m. Thus, class file format versions may be ordered lexicographically, for example, 1.5 < 2.0 < 2.1.
> A Java Virtual Machine implementation can support a class file format of version v if and only if v lies in some contiguous range Mi.0 ≤ v ≤ Mj.m. The release level of the Java SE platform to which a Java Virtual Machine implementation conforms is responsible for determining the range.
> *Oracle’s Java Virtual Machine implementation in JDK release 1.0.2 supports class file format versions 45.0 through 45.3 inclusive. JDK releases 1.1.* support class file format versions in the range 45.0 through 45.65535 inclusive. For k ≥ 2, JDK release 1.k supports class file format versions in the range 45.0 through 44+k.0 inclusive.*

### 2.2.4 constant_pool_count

u2：2 个字节

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000000                            00 16
12
```

**常量池容量计数值**，就是接下来有几个常量。这里是显示有 22（0x16）个，但是实际上只有 21 个，因为 第 0 个预留了，用于 “ 不引用任何一个常量池项目 ”，所以常量池的引用是从 1 开始。对于其他集合类型，一般都是从 0 下标开始的。

官方说明：

> The value of the constant_pool_count item is equal to the number of entries in the constant_pool table plus one. A constant_pool index is considered valid if it is greater than zero and less than constant_pool_count, with the exception for constants of type long and double noted in [§4.4.5](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html#jvms-4.4.5).

### 2.2.5 constant_pool[constant_pool_count-1]

cp_info：常量表结构，长度是 `constant_pool_count-1`。（从上文可知是 21 个）

结构如下：

```
cp_info {
    u1 tag;
    u1 info[];
}
1234
```

tag 的类型如下：

| 类型 Constant Type            | 标志 Value | 描述                     |
| ----------------------------- | ---------- | ------------------------ |
| `CONSTANT_Class`              | 7          | 类和接口的符号引用       |
| `CONSTANT_Fieldref`           | 9          | 字段的符号引用           |
| `CONSTANT_Methodref`          | 10         | 类中方法的符号引用       |
| `CONSTANT_InterfaceMethodref` | 11         | 接口中方法的符号引用     |
| `CONSTANT_String`             | 8          | 字符串类型字面量         |
| `CONSTANT_Integer`            | 3          | 整型字面量               |
| `CONSTANT_Float`              | 4          | 浮点型字面量             |
| `CONSTANT_Long`               | 5          | 长整型字面量             |
| `CONSTANT_Double`             | 6          | 双精度浮点型字面量       |
| `CONSTANT_NameAndType`        | 12         | 字段或方法的部分符号引用 |
| `CONSTANT_Utf8`               | 1          | UTF-8 编码的字符串       |
| `CONSTANT_MethodHandle`       | 15         | 表示方法句柄             |
| `CONSTANT_MethodType`         | 16         | 表示方法类型             |
| `CONSTANT_InvokeDynamic`      | 18         | 表示一个动态方法调用     |

接下逐个常量做解读

#### 2.2.5.1 #1

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000000                                  0A 00 04 00 12
12
```

`CONSTANT_Methodref` 结构：

```
CONSTANT_Methodref_info {
    u1 tag;
    u2 class_index;
    u2 name_and_type_index;
}
12345
```

解读：

```
#1 = Methodref          #4.#18
1
```

#### 2.2.5.2 #2

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000000                                                 09
00000016   00 03 00 13 
123
```

`CONSTANT_Fieldref` 结构：

```
CONSTANT_Fieldref_info {
    u1 tag;
    u2 class_index;
    u2 name_and_type_index;
}
12345
```

解读：

```
#2 = Fieldref           #3.#19
1
```

#### 2.2.5.3 #3

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000016               07 00 14 
12
```

`CONSTANT_Class` 结构：

```
CONSTANT_Class_info {
    u1 tag;
    u2 name_index;
}
1234
```

解读：

```
#3 = Class              #20
1
```

#### 2.2.5.4 #4

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000016                        07  00 15
12
```

`CONSTANT_Class` 结构：

```
CONSTANT_Class_info {
    u1 tag;
    u2 name_index;
}
1234
```

解读：

```
#4 = Class              #21
1
```

#### 2.2.5.5 #5

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000016                                  01 00 01 6E
12
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#5 = Utf8               n
1
```

> 这里 utf-8 使用的是缩写编码。从 `\u0001` 到 `\u007f` 之间的字符，使用一个字节（相当于1~127的ASCII码）。从`\u0080` 到 `\u07ff` 之间采用两个字节。从 `\u0800` 到 `\uffff` 按照普通的 UTF-8 使用三个字节。

#### 2.2.5.6 #6

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000016                                              01 00
00000032   01 4A 
123
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#6 = Utf8               J
1
```

#### 2.2.5.7 #7

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000032         01 00 06 3C 69 6E  69 74 3E 

123
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#7 = Utf8               <init>
1
```

#### 2.2.5.8 #8

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000032                                     01 00 03 28 29
00000048   56
123
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#8 = Utf8               ()V
1
```

#### 2.2.5.9 #9

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000048      01 00 04 43 6F 64 65
12
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#9 = Utf8               Code
1
```

#### 2.2.5.10 #10

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000048                            01 00 0F 4C 69 6E 65 4E
00000064   75 6D 62 65 72 54 61 62  6C 65
123
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#10 = Utf8               LineNumberTable
1
```

#### 2.2.5.11 #11

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000064                                  01 00 12 4C 6F 63
00000080   61 6C 56 61 72 69 61 62  6C 65 54 61 62 6C 65
123
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#11 = Utf8               LocalVariableTable
1
```

#### 2.2.5.12 #12

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000080                                                 01
00000096   00 04 74 68 69 73
123
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#12 = Utf8               this
1
```

#### 2.2.5.13 #13

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000096                     01 00  28 4C 63 6F 6D 2F 68 79
00000112   6C 2F 6C 65 61 72 6E 65  72 4A 56 4D 2F 63 6C 61
00000128   73 73 74 65 73 74 2F 43  6C 61 73 73 54 65 73 74
00000144   3B
12345
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#13 = Utf8               Lcom/hyl/learnerJVM/classtest/ClassTest;
1
```

#### 2.2.5.14 #14

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000144      01 00 06 69 6E 4C 6F  6E 67
12
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#14 = Utf8               inLong
1
```

#### 2.2.5.15 #15

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000144                                  01 00 03 28 29 4A
12
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#15 = Utf8               ()J
1
```

#### 2.2.5.16 #16

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000160   01 00 0A 53 6F 75 72 63  65 46 69 6C 65
12
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#16 = Utf8               SourceFile
1
```

#### 2.2.5.17 #17

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000160                                           01 00 0E
00000176   43 6C 61 73 73 54 65 73  74 2E 6A 61 76 61
123
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#17 = Utf8               ClassTest.java
1
```

#### 2.2.5.18 #18

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000176                                              0C 00
00000192   07 00 08
123
```

`CONSTANT_NameAndType` 结构：

```
CONSTANT_NameAndType_info {
    u1 tag;
    u2 name_index;
    u2 descriptor_index;
}
12345
```

解读：

```
#18 = NameAndType        #7:#8
1
```

#### 2.2.5.19 #19

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000192            0C 00 05 00 06
12
```

`CONSTANT_NameAndType` 结构：

```
CONSTANT_NameAndType_info {
    u1 tag;
    u2 name_index;
    u2 descriptor_index;
}
12345
```

解读：

```
#19 = NameAndType        #5:#6
1
```

#### 2.2.5.20 #20

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000192                            01 00 26 63 6F 6D 2F 68
00000208   79 6C 2F 6C 65 61 72 6E  65 72 4A 56 4D 2F 63 6C
00000224   61 73 73 74 65 73 74 2F  43 6C 61 73 73 54 65 73
00000240   74
12345
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#20 = Utf8               com/hyl/learnerJVM/classtest/ClassTest
1
```

#### 2.2.5.21 #21

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000240      01 00 10 6A 61 76 61  2F 6C 61 6E 67 2F 4F 62
00000256   6A 65 63 74
123
```

`CONSTANT_Utf8` 结构：

```
CONSTANT_Utf8_info {
    u1 tag;
    u2 length;
    u1 bytes[length];
}
12345
```

解读：

```
#21 = Utf8               java/lang/Object
1
```

### 2.2.6 access_flags

u2：两个字节

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000256               00 21
12
```

**访问标志**，识别一些类或接口的访问信息，包括，是类还是接口；是否是 `public` ；是否是 `abstract` 类型；是否声明 `final` ；等等。

访问标识如下：

| Flag Name        | Value  | 含义                                           | Interpretation                                               |
| ---------------- | ------ | ---------------------------------------------- | ------------------------------------------------------------ |
| `ACC_PUBLIC`     | 0x0001 | 是否为public 类型                              | Declared `public`; may be accessed from outside its package. |
| `ACC_FINAL`      | 0x0010 | 是否被声明 final，只有类可设置                 | Declared `final`; no subclasses allowed.                     |
| `ACC_SUPER`      | 0x0020 | 是否允许使用*invokespecial* 字节码指令的新语义 | Treat superclass methods specially when invoked by the *invokespecial* instruction. |
| `ACC_INTERFACE`  | 0x0200 | 标识这是个接口                                 | Is an interface, not a class.                                |
| `ACC_ABSTRACT`   | 0x0400 | 是否为 `abstract` 类型                         | Declared `abstract`; must not be instantiated.               |
| `ACC_SYNTHETIC`  | 0x1000 | 标识这个类并非由用户代码产生的                 | Declared synthetic; not present in the source code.          |
| `ACC_ANNOTATION` | 0x2000 | 标识这是个注解                                 | Declared as an annotation type.                              |
| `ACC_ENUM`       | 0x4000 | 标识这是个枚举                                 | Declared as an `enum` type.                                  |

原文 https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html#jvms-4.1-200-E.1

解读：

access_flags 的值为：0x0001 | 0x0020 = 0x0021

```
flags: ACC_PUBLIC, ACC_SUPER
1
```

### 2.2.7 this_class

u2：两个字节

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000256                     00 03
12
```

**类索引**，确定这个类的全限名。指向一个 class 类型的常量。

官方说明：

> The value of the this_class item must be a valid index into the constant_pool table. The constant_pool entry at that index must be a CONSTANT_Class_info structure ([§4.4.1](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html#jvms-4.4.1)) representing the class or interface defined by this class file.

解读：

```
#3  = Class              #20            // com/hyl/learnerJVM/classtest/ClassTest
1
```

### 2.2.8 super_class

u2：两个字节

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000256                            00 04
12
```

**父类索引**，确定这个父类的全限名。指向一个 class 类型常量。

官方说明：

> For a class, the value of the super_class item either must be zero or must be a valid index into the constant_pool table. If the value of the super_class item is nonzero, the constant_pool entry at that index must be a CONSTANT_Class_info structure representing the direct superclass of the class defined by this class file. Neither the direct superclass nor any of its superclasses may have the ACC_FINAL flag set in the access_flags item of its ClassFile structure.
> If the value of the super_class item is zero, then this class file must represent the class Object, the only class or interface without a direct superclass.
> For an interface, the value of the super_class item must always be a valid index into the constant_pool table. The constant_pool entry at that index must be a CONSTANT_Class_info structure representing the class Object.

解读：

```
#4 = Class              #21            // java/lang/Object
1
```

### 2.2.9 interfaces_count

u2：两个字节

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000256                                  00 00
12
```

**接口计数器**，表示接口索引表的容量。

官方说明：

> The value of the interfaces_count item gives the number of direct superinterfaces of this class or interface type.

解读：

这里接口数量为零，所以接下来的接口索引表不存在了。

### 2.2.10 interfaces[interfaces_count]

u2：两个字节一组。

因为没有接口，所以这里在 class 文件中不存在。

**接口索引表**，包含实现的接口。

官方说明：

> Each value in the interfaces array must be a valid index into the constant_pool table. The constant_pool entry at each value of interfaces[i], where 0 ≤ i < interfaces_count, must be a CONSTANT_Class_info structure representing an interface that is a direct superinterface of this class or interface type, in the left-to-right order given in the source for the type.

解读：
这里不存在。

### 2.2.11 fields_count

u2：两个字节。

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000256                                        00 01
12
```

**字段表计数器**，表示接下来有几个字段表。

官方说明：

> The value of the fields_count item gives the number of field_info structures in the fields table. The field_info structures represent all fields, both class variables and instance variables, declared by this class or interface type.

解读：

接下来有一个字段表。

### 2.2.12 fields[fields_count]

field_info： 字段表结构，长度是`fields_count`，这里是一个。

结构如下:

```
field_info {
    u2             access_flags;
    u2             name_index;
    u2             descriptor_index;
    u2             attributes_count;
    attribute_info attributes[attributes_count];
}
1234567
```

**access_flags**，字段修饰符，它与类的修饰符很像都是一个 u2 的数据类型。

字段访问标识含义：

| Flag Name       | Value  | 含义                     | Interpretation                                               |
| --------------- | ------ | ------------------------ | ------------------------------------------------------------ |
| `ACC_PUBLIC`    | 0x0001 | 字段是否`public`         | Declared `public`; may be accessed from outside its package. |
| `ACC_PRIVATE`   | 0x0002 | 字段是否`private`        | Declared `private`; usable only within the defining class.   |
| `ACC_PROTECTED` | 0x0004 | 字段是否`protected`      | Declared `protected`; may be accessed within subclasses.     |
| `ACC_STATIC`    | 0x0008 | 字段是否`static`         | Declared `static`.                                           |
| `ACC_FINAL`     | 0x0010 | 字段是否`final`          | Declared `final`; never directly assigned to after object construction (JLS §17.5). |
| `ACC_VOLATILE`  | 0x0040 | 字段是否`volatile`       | Declared `volatile`; cannot be cached.                       |
| `ACC_TRANSIENT` | 0x0080 | 字段是否`transient`      | Declared `transient`; not written or read by a persistent object manager. |
| `ACC_SYNTHETIC` | 0x1000 | 字段是否由编译器自动产生 | Declared synthetic; not present in the source code.          |
| `ACC_ENUM`      | 0x4000 | 字段是否`enum`           | Declared as an element of an `enum`.                         |

**descriptor_index**，描述符，描述数据类型、方法的参数列表（包括数量、类型以及顺序）和放回值。

描述符标识字符含义：

| *FieldType* term    | Type        | 含义              | Interpretation                                               |
| ------------------- | ----------- | ----------------- | ------------------------------------------------------------ |
| `B`                 | `byte`      | 基本类型`byte`    | signed byte                                                  |
| `C`                 | `char`      | 基本类型`char`    | Unicode character code point in the Basic Multilingual Plane, encoded with UTF-16 |
| `D`                 | `double`    | 基本类型`double`  | double-precision floating-point value                        |
| `F`                 | `float`     | 基本类型`float`   | single-precision floating-point value                        |
| `I`                 | `int`       | 基本类型`int`     | integer                                                      |
| `J`                 | `long`      | 基本类型`long`    | long integer                                                 |
| `L` *ClassName* `;` | `reference` | 对象类型          | an instance of class *ClassName*                             |
| `S`                 | `short`     | 基本类型`short`   | signed short                                                 |
| `Z`                 | `boolean`   | 基本类型`boolean` | `true` or `false`                                            |
| `[`                 | `reference` | 一个数组维度      | one array dimension                                          |

#### 2.2.12.1 #1

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000256                                              00 02
00000272   00 05 00 06 00 00
123
```

| 字段                         | 源码  | 说明                            |
| ---------------------------- | ----- | ------------------------------- |
| access_flags                 | 00 02 | 字段是`private`                 |
| name_index                   | 00 05 | `#5 = Utf8 n`字段名为 `n`       |
| descriptor_index             | 00 06 | `#6 = Utf8 J` 字段类型为 `long` |
| attributes_count             | 00 00 | 其他属性描述为空                |
| attributes[attributes_count] | -     | -                               |

解读：

```
  private long n;
    descriptor: J
    flags: ACC_PRIVATE
123
```

### 2.2.13 methods_count

u2：两个字节。

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000272                     00 02
12
```

**方法表集合计数**，记录接下里将会有几个方法表集合。

官方说明：

> The value of the methods_count item gives the number of method_info structures in the methods table.

解读：

接下来会有两个方法表集合。

### 2.2.14 methods[methods_count]

method_info：方法表结构，长度`methods_count`，从上文可知，两个。

结构如下：

```
method_info {
    u2             access_flags;
    u2             name_index;
    u2             descriptor_index;
    u2             attributes_count;
    attribute_info attributes[attributes_count];
}
1234567
```

access_flags，方法访问标志。
如下：

| Flag Name          | Value  | 含义                             | Interpretation                                               |
| ------------------ | ------ | -------------------------------- | ------------------------------------------------------------ |
| `ACC_PUBLIC`       | 0x0001 | 方法是否为`public`               | Declared `public`; may be accessed from outside its package. |
| `ACC_PRIVATE`      | 0x0002 | 方法是否为`private`              | Declared `private`; accessible only within the defining class. |
| `ACC_PROTECTED`    | 0x0004 | 方法是否为`protected`            | Declared `protected`; may be accessed within subclasses.     |
| `ACC_STATIC`       | 0x0008 | 方法是否为`static`               | Declared `static`.                                           |
| `ACC_FINAL`        | 0x0010 | 方法是否为`final`                | Declared `final`; must not be overridden ([§5.4.5](https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-5.html#jvms-5.4.5)). |
| `ACC_SYNCHRONIZED` | 0x0020 | 方法是否为`synchronized`         | Declared `synchronized`; invocation is wrapped by a monitor use. |
| `ACC_BRIDGE`       | 0x0040 | 方法是不是由编译器产生的桥接方法 | A bridge method, generated by the compiler.                  |
| `ACC_VARARGS`      | 0x0080 | 方法是否接受不定参数             | Declared with variable number of arguments.                  |
| `ACC_NATIVE`       | 0x0100 | 方法是否为`native`               | Declared `native`; implemented in a language other than Java. |
| `ACC_ABSTRACT`     | 0x0400 | 方法是否为`abstract`             | Declared `abstract`; no implementation is provided.          |
| `ACC_STRICT`       | 0x0800 | 方法是否为`strictfp`             | Declared `strictfp`; floating-point mode is FP-strict.       |
| `ACC_SYNTHETIC`    | 0x1000 | 方法是由编译器自动产生           | Declared synthetic; not present in the source code.          |

attributes，方法属性，以下是属性

| Attribute                                                    | Location                                 | `class` file |
| ------------------------------------------------------------ | ---------------------------------------- | ------------ |
| `Code`                                                       | `method_info`                            | 45.3         |
| `Exceptions`                                                 | `method_info`                            | 45.3         |
| `RuntimeVisibleParameterAnnotations`, `RuntimeInvisibleParameterAnnotations` | `method_info`                            | 49.0         |
| `AnnotationDefault`                                          | `method_info`                            | 49.0         |
| `MethodParameters`                                           | `method_info`                            | 52.0         |
| `Synthetic`                                                  | `ClassFile`, `field_info`, `method_info` | 45.3         |
| `Deprecated`                                                 | `ClassFile`, `field_info`, `method_info` | 45.3         |
| `Signature`                                                  | `ClassFile`, `field_info`, `method_info` | 49.0         |
| `RuntimeVisibleAnnotations`, `RuntimeInvisibleAnnotations`   | `ClassFile`, `field_info`, `method_info` | 49.0         |

完整属性列表：https://docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html#jvms-4.7

#### 2.2.14.1 #1

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000272                            00 01 00 07 00 08 00 01
00000288   00 09 00 00 00 2F 00 01  00 01 00 00 00 05 2A B7
00000304   00 01 B1 00 00 00 02 00  0A 00 00 00 06 00 01 00
00000320   00 00 09 00 0B 00 00 00  0C 00 01 00 00 00 05 00
00000336   0C 00 0D 00 00
123456
```

字段对应：

| access_flags | name_index         | descriptor_index              | attributes_count |
| ------------ | ------------------ | ----------------------------- | ---------------- |
| 00 01        | 00 07              | 00 08                         | 00 01            |
| `ACC_PUBLIC` | `#7 = Utf8 `方法名 | `#8 = Utf8 ()V`返回类型`viod` | 有一个属性表集合 |

方法属性：
`0x00 09`, `#9 = Utf8 Code`，是一个`Code`属性。

`Code` 属性结构如下：

```
Code_attribute {
    u2 attribute_name_index;
    u4 attribute_length;
    u2 max_stack;
    u2 max_locals;
    u4 code_length;
    u1 code[code_length];
    u2 exception_table_length;
    {   u2 start_pc;
        u2 end_pc;
        u2 handler_pc;
        u2 catch_type;
    } exception_table[exception_table_length];
    u2 attributes_count;
    attribute_info attributes[attributes_count];
}
12345678910111213141516
```

对应解读：

| 类型                   | 长度 | 源码        | 含义                                        |
| ---------------------- | ---- | ----------- | ------------------------------------------- |
| `attribute_name_index` | u2   | 00 09       | `#9 = Utf8 Code` 表明是 `Code` 属性         |
| `attribute_length`     | u4   | 00 00 00 2F | `0x2F`，47个长度                            |
| `max_stack`            | u2   | 00 01       | 操作数栈（Operand Stack）深度的最大值，1    |
| `max_locals`           | u2   | 00 01       | 局部变量表所需的储存空间，1个变量槽（Slot） |
| `code_length`          | u4   | 00 00 00 05 | 方法指令长度，5 个字节                      |

`code[5]`指令解读：

| 源码     | 字节码                                              | 含义                                       |
| -------- | --------------------------------------------------- | ------------------------------------------ |
| 2A       | aload_0                                             | 将第一引用类型本地变量推送至栈顶           |
| B7 00 01 | invokespecial #1 `//Method java/lang/Object."":()V` | 调用超类构造方法，实例初始化方法，私有方法 |
| B1       | return                                              | 从当前方法返回 viod                        |

`exception_table_length`,**00 00**，异常表为零。

`exception_table[exception_table_length]`，就不存在啦。

`attributes_count`，方法属性表集合数，**00 02**，两个，如下。

**00 0A**：
`#10 = Utf8 LineNumberTable`，可知是`LineNumberTable`属性。

> `LineNumberTable`属性，用于描述 Java 源码行号与字节码（字节码的偏移量）之间的对应关系。

结构如下：

```
LineNumberTable_attribute {
    u2 attribute_name_index;
    u4 attribute_length;
    u2 line_number_table_length;
    {   u2 start_pc;
        u2 line_number;	
    } line_number_table[line_number_table_length];
}
12345678
```

| attribute_name_index | attribute_length | line_number_table_length |
| -------------------- | ---------------- | ------------------------ |
| 00 0A                | 00 00 00 06      | 00 01                    |
| `LineNumberTable`    | 6个字节长度      | 一个                     |

```
line_number_table[1]
```

| start_pc | start_pc |
| -------- | -------- |
| 00 00    | 00 09    |

**00 0B**：
`#11 = Utf8 LocalVariableTable`，可知是`LocalVariableTable` 属性。

> `LocalVariableTable` 属性,用于描述栈帧中局部变量表的变量与 Java 源码中定义的变量之间的关系。

结构如下:

```
LocalVariableTable_attribute {
    u2 attribute_name_index;
    u4 attribute_length;
    u2 local_variable_table_length;
    {   u2 start_pc;
        u2 length;
        u2 name_index;
        u2 descriptor_index;
        u2 index;
    } local_variable_table[local_variable_table_length];
}
1234567891011
```

| attribute_name_index      | attribute_length | local_variable_table_length |
| ------------------------- | ---------------- | --------------------------- |
| 00 0B                     | 00 00 00 0C      | 00 01                       |
| `LocalVariableTable` 属性 | 12个长度         | 1个值                       |

```
local_variable_table[1]
```

| start_pc | length | name_index        | descriptor_index                                      | index |
| -------- | ------ | ----------------- | ----------------------------------------------------- | ----- |
| 00 00    | 00 05  | 00 0C             | 00 0D                                                 | 00 00 |
| 0        | 5      | `#12 = Utf8 this` | `#13 = Utf8 Lcom/hyl/learnerJVM/classtest/ClassTest;` | 0     |

> `start_pc`和`length`属性分别代表了整个局部变量的生命周期开始的字节码偏移量及其作用范围覆盖长度，结合起来就是局部变量在字节码之中的作用范围。

> `this` 变量是系统默认添加进去的。

> `Signature` 储存一个方法在字节码层面的特征签名，保存参数类型，但并不是原生类型，而是包含了参数化类型的信息。

最终整个方法解读为：

```
  public com.hyl.learnerJVM.classtest.ClassTest();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 9: 0
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       5     0  this   Lcom/hyl/learnerJVM/classtest/ClassTest;
12345678910111213
```

#### 2.2.14.2 #2

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000336                  00 01 00  0E 00 0F 00 01 00 09 00
00000352   00 00 31 00 04 00 01 00  00 00 07 2A B4 00 02 0A
00000368   61 AD 00 00 00 02 00 0A  00 00 00 06 00 01 00 00
00000384   00 0E 00 0B 00 00 00 0C  00 01 00 00 00 07 00 0C
00000400   00 0D 00 00
123456
```

字段对应：

| access_flags | name_index                | descriptor_index                | attributes_count |
| ------------ | ------------------------- | ------------------------------- | ---------------- |
| 00 01        | 00 0E                     | 00 0F                           | 00 01            |
| `ACC_PUBLIC` | `#14 = Utf8 inLong`方法名 | `#15 = Utf8 ()J`返回类型 `long` | 有一个属性表集合 |

方法属性：

`0x00 09`, `#9 = Utf8 Code`，是一个`Code`属性。

`Code` 属性结构如下：

```
Code_attribute {
    u2 attribute_name_index;
    u4 attribute_length;
    u2 max_stack;
    u2 max_locals;
    u4 code_length;
    u1 code[code_length];
    u2 exception_table_length;
    {   u2 start_pc;
        u2 end_pc;
        u2 handler_pc;
        u2 catch_type;
    } exception_table[exception_table_length];
    u2 attributes_count;
    attribute_info attributes[attributes_count];
}
12345678910111213141516
```

对应解读：

| 类型                   | 长度 | 源码        | 含义                                        |
| ---------------------- | ---- | ----------- | ------------------------------------------- |
| `attribute_name_index` | u2   | 00 09       | `#9 = Utf8 Code` 表明是 `Code` 属性         |
| `attribute_length`     | u4   | 00 00 00 31 | `0x31`，49个长度                            |
| `max_stack`            | u2   | 00 04       | 操作数栈（Operand Stack）深度的最大值，4    |
| `max_locals`           | u2   | 00 01       | 局部变量表所需的储存空间，1个变量槽（Slot） |
| `code_length`          | u4   | 00 00 00 07 | 方法指令长度，7 个字节                      |

`code[7]`指令解读：

| 源码     | 字节码                     | 含义                                       |
| -------- | -------------------------- | ------------------------------------------ |
| 2A       | aload_0                    | 将第一引用类型本地变量推送至栈顶           |
| B4 00 02 | getfield #2 `// Field n:J` | 获得指定类的实例域，并将其值压入栈顶       |
| 0A       | lconst_1                   | 将 long 类型 1 推送至栈顶                  |
| 61       | ladd                       | 将栈顶两个 long 类型值相加并将结果压入栈顶 |
| AD       | lreturn                    | 从当前方法返回 long                        |

`exception_table_length`,**00 00**，异常表为零。

`exception_table[exception_table_length]`，就不存在啦。

`attributes_count`，方法属性表集合数，**00 02**，两个，如下。

**00 0A**：
`#10 = Utf8 LineNumberTable`，可知是`LineNumberTable`属性。

> `LineNumberTable`属性，用于描述 Java 源码行号与字节码（字节码的偏移量）之间的对应关系。

结构如下：

```
LineNumberTable_attribute {
    u2 attribute_name_index;
    u4 attribute_length;
    u2 line_number_table_length;
    {   u2 start_pc;
        u2 line_number; 
    } line_number_table[line_number_table_length];
}
12345678
```

| attribute_name_index | attribute_length | line_number_table_length |
| -------------------- | ---------------- | ------------------------ |
| 00 0A                | 00 00 00 06      | 00 01                    |
| `LineNumberTable`    | 6个字节长度      | 一个                     |

```
line_number_table[1]
```

| start_pc | start_pc |
| -------- | -------- |
| 00 00    | 00 0E    |

**00 0B**：
`#11 = Utf8 LocalVariableTable`，可知是`LocalVariableTable` 属性。

> `LocalVariableTable` 属性,用于描述栈帧中局部变量表的变量与 Java 源码中定义的变量之间的关系。

结构如下：

```
LocalVariableTable_attribute {
    u2 attribute_name_index;
    u4 attribute_length;
    u2 local_variable_table_length;
    {   u2 start_pc;
        u2 length;
        u2 name_index;
        u2 descriptor_index;
        u2 index;
    } local_variable_table[local_variable_table_length];
}
1234567891011
```

| attribute_name_index      | attribute_length | local_variable_table_length |
| ------------------------- | ---------------- | --------------------------- |
| 00 0B                     | 00 00 00 0C      | 00 01                       |
| `LocalVariableTable` 属性 | 12个长度         | 1个值                       |

```
local_variable_table[1]
```

| start_pc | length | name_index        | descriptor_index                                      | index |
| -------- | ------ | ----------------- | ----------------------------------------------------- | ----- |
| 00 00    | 00 07  | 00 0C             | 00 0D                                                 | 00 00 |
| 0        | 7      | `#12 = Utf8 this` | `#13 = Utf8 Lcom/hyl/learnerJVM/classtest/ClassTest;` | 0     |

> `start_pc`和`length`属性分别代表了整个局部变量的生命周期开始的字节码偏移量及其作用范围覆盖长度，结合起来就是局部变量在字节码之中的作用范围。

> `this` 变量是系统默认添加进去的。

> `Signature` 储存一个方法在字节码层面的特征签名，保存参数类型，但并不是原生类型，而是包含了参数化类型的信息。

最终整个方法解读为：

```
  public long inLong();
    descriptor: ()J
    flags: ACC_PUBLIC
    Code:
      stack=4, locals=1, args_size=1
         0: aload_0
         1: getfield      #2                  // Field n:J
         4: lconst_1
         5: ladd
         6: lreturn
      LineNumberTable:
        line 14: 0
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       7     0  this   Lcom/hyl/learnerJVM/classtest/ClassTest;
123456789101112131415
```

### 2.2.15 attributes_count

u2：两个字节。

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000400               00 01
12
```

class属性表集合的计数，这里有一个。

官方说明：

> The value of the attributes_count item gives the number of attributes in the attributes table of this class.

解读：
接下里有一个文件的属性表集合

### 2.2.16 attributes[attributes_count]

attribute_info：属性表结构，长度`attributes_count`，从上文可知，一个。

结构如下：

```
attribute_info {
    u2 attribute_name_index;
    u4 attribute_length;
    u1 info[attribute_length];
}
12345
```

属性类型列表：

| Attribute                                                  | Location                                 | `class` file |
| ---------------------------------------------------------- | ---------------------------------------- | ------------ |
| `SourceFile`                                               | `ClassFile`                              | 45.3         |
| `InnerClasses`                                             | `ClassFile`                              | 45.3         |
| `EnclosingMethod`                                          | `ClassFile`                              | 49.0         |
| `SourceDebugExtension`                                     | `ClassFile`                              | 49.0         |
| `BootstrapMethods`                                         | `ClassFile`                              | 51.0         |
| `Synthetic`                                                | `ClassFile`, `field_info`, `method_info` | 45.3         |
| `Deprecated`                                               | `ClassFile`, `field_info`, `method_info` | 45.3         |
| `Signature`                                                | `ClassFile`, `field_info`, `method_info` | 49.0         |
| `RuntimeVisibleAnnotations`, `RuntimeInvisibleAnnotations` | `ClassFile`, `field_info`, `method_info` | 49.0         |

#### 2.2.16.1 #1

```log
Offset      0  1  2  3  4  5  6  7   8  9 10 11 12 13 14 15
00000400                     00 10  00 00 00 02 00 11
12
```

| 结构                   | 源码        | 解释                                             |
| ---------------------- | ----------- | ------------------------------------------------ |
| attribute_name_index   | 00 10       | `0x10,#16 = Utf8 SourceFile`                     |
| attribute_length       | 00 00 00 02 | 两个字节                                         |
| info[attribute_length] | 00 11       | 由下图结构可知，`0x11,#17 = Utf8 ClassTest.java` |

根据解读是`SourceFile`，结构如下：

```
SourceFile_attribute {
    u2 attribute_name_index;
    u4 attribute_length;
    u2 sourcefile_index;
}
12345
```

`SourceFile`属性用于记录生成这个 Class 文件的源码文件名称。

解读：

```
SourceFile: "ClassTest.java"
1
```

## 2.3 javap 工具结果

指令

```shell
javap -verbose -p ClassTest.class
```

结果

```tex
Classfile /D:/git/mybase/projects/github/learner-JVM/target/classes/com/hyl/le                                                                                                                                                                                                  arnerJVM/classtest/ClassTest.class
  Last modified 2020-8-7; size 414 bytes
  MD5 checksum cdd61b9867778e815b9d0b93b1412a9d
  Compiled from "ClassTest.java"
public class com.hyl.learnerJVM.classtest.ClassTest
  minor version: 0
  major version: 52
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #4.#18         // java/lang/Object."<init>":()V
   #2 = Fieldref           #3.#19         // com/hyl/learnerJVM/classtest/Clas                                                                                                                                                                                                  sTest.n:J
   #3 = Class              #20            // com/hyl/learnerJVM/classtest/Clas                                                                                                                                                                                                  sTest
   #4 = Class              #21            // java/lang/Object
   #5 = Utf8               n
   #6 = Utf8               J
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               LocalVariableTable
  #12 = Utf8               this
  #13 = Utf8               Lcom/hyl/learnerJVM/classtest/ClassTest;
  #14 = Utf8               inLong
  #15 = Utf8               ()J
  #16 = Utf8               SourceFile
  #17 = Utf8               ClassTest.java
  #18 = NameAndType        #7:#8          // "<init>":()V
  #19 = NameAndType        #5:#6          // n:J
  #20 = Utf8               com/hyl/learnerJVM/classtest/ClassTest
  #21 = Utf8               java/lang/Object
{
  private long n;
    descriptor: J
    flags: ACC_PRIVATE

  public com.hyl.learnerJVM.classtest.ClassTest();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 9: 0
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       5     0  this   Lcom/hyl/learnerJVM/classtest/ClassTest;

  public long inLong();
    descriptor: ()J
    flags: ACC_PUBLIC
    Code: 
      stack=4, locals=1, args_size=1
         0: aload_0
         1: getfield      #2                  // Field n:J
         4: lconst_1
         5: ladd
         6: lreturn       
      LineNumberTable:
        line 14: 0
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       7     0  this   Lcom/hyl/learnerJVM/classtest/ClassTest;
}
SourceFile: "ClassTest.java"
```

