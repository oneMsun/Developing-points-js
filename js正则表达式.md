#####  1、声明正则：

```
var reg = new RegExp(‘a’,'gim')  = /a/gim;
//其中 g是全局匹配，i忽略大小写，m多行模式匹配
```




##### 2、test用法：用来测试匹配的字符串是否符合规则，如果成功返回true，否则返回一个false

```
var reg1 = /a/;
var reg2 = /a45/;
var reg3 = /B/;
var reg4 = /B/i;
var str = '123a45a6Abc';
console.log(reg1.test(str)); //true
console.log(reg2.test(str));//true
console.log(reg3.test(str));//false
console.log(reg4.test(str));//true
```



##### 3、str.replace(reg, newStr); 用来替换字符串中的某些符合规则的字符，返回值：是新的字符串

```
var str = 'asda'
var str1 = str.replace('a', 'ff')
var str2 = str.replace('a', 'b')
var str3 = str.replace(/a/g, 'b')
console.log(str1);
console.log(str2);
console.log(str3);
```



##### 4、str.match(reg) 用来匹配符合规则的字符，返回一个数组。分为两种情况，全局和非全局，返回值是一个数组。
当不是全局匹配的时候，数组里面有一个index代表匹配成功的位置，还有一个input代表匹配的原字符串。<br/>
如果是全局匹配的时候，那么就直接返回所有匹配到的字符串组成的数组。如果匹配不成功，返回一个null

```
var str = 'a1a2a3a4a5';  
str.match(/a/); // ["a", index: 0, input: "a1a2a3a4a5"]
str.match(/a/g) // ["a", "a", "a", "a", “a"]
```



##### 5、str.search(reg) 匹配字符串，如果成功返回相应匹配字符的的索引位置，如果失败返回-1

```
var str = "abcdef";
var reg = /a/;
console.log(str.search(reg)); //0
```



##### 6、正则表达式的元字符都有那些？

```
.  *  +  ?  ^  $  |  \  ()   []   {}   \n  \r \t
```


##### 7、元字符 [] 构建一个简单的类 ，例如：[abc] 指的是匹配 a或b或c，[^abc]除了 abc以外的字符

```
var str = 'a1b2c3d4e5';
str.replace(/[abcde]/g, 'Q');  // “Q1Q2Q3Q4Q5"
var str = 'a1b2c3^*()d4e5';
str.replace(/[^abcde]/g, 'Q');  // “aQbQcQQQQQdQeQ"
```



##### 8、范围类：

```
var str1 = 'a1ds23mds45msaghjm6789m2347mgffgdg';
str1.replace(/[a-z]/g, '-');  
// “-1--23---45-------6789-2347-------"
var str2 = 'asd673%AD-F34L-J977_sdsa-d_&%113';
str2.replace(/[a-zA-Z0-9_-]/g, ‘=')
```



##### 9、预定义类：

```
. 匹配除了新行符或者换行符的任意字符
console.log('abcdef '.match(/a.../g));   // [‘abcd’]

 \n 换行符  \r 回车符  \t 横向制表符

\s 匹配的是空白字符，包括上面的换行符、制表符等
console.log('r\n da’.match(/\s/g)); //["↵", " "]

\S 匹配除了空白字符的所有内容相当于： [^\s]
console.log('r\n d a’.match(/\S/g)); // ["r", "d", "a"]

\w 匹配所有的数字字母下划线，相当于 [A-Za-z0-9_]
\W 正好与 \w 相反
\d 匹配所有的数字
\D 匹配所有的非数字 相当于 [^0-9] 或者 [^\d]
```



##### 10、边界类：
^ 以…作为开头<br/>
$ 以…作为结尾<br/>
\b 单词边界<br/>
\B 非单词边界

```
var str = ‘@111\n@222\n@333';
str.replace(/^@\d/gm, 'Q') 
//“Q11
Q22
Q33”
```


##### 11、量词：
表示匹配出现0次或者多次的内容  => n>=0次<br/>
? 匹配0次或者1次  => 0或者1<br/>
匹配至少出现1次的内容 =>  n>=1次<br/>
{n} 匹配中间出现过 n次的内容<br/>
{min,} 匹配至少 min 次的内容<br/>
{min, max} 匹配 min 到 max 次的内容


```
验证QQ号码：
var text = document.querySelector('.text');
var btn = document.querySelector('.btn');
btn.onclick = function (){
      var val = text.value;
      var reg = /^[1-9]\d{4,11}$/;
      if(reg.test(val)){
        alert('验证成功')
      }else{
        alert('验证失败')
      }
}
```



##### 12、贪婪模式和非贪婪模式：
贪婪模式：就是尽可能多的去匹配，默认是贪婪模式<br/>
非贪婪模式：尽可能少的去匹配<br/>

```
var str = 'a12345678b';
str.replace(/\d{2,4}/g, 'Q');  // "aQQb"
str.replace(/\d{2,4}?/g, 'Q');  // “aQQQQb”
```



##### 13、匹配中文：

```
/[\u4e00-\u9fa5]/
```



##### 14、分组：用小括号包起来就是一组

```
'abcabcabc123abc'.match(/(abc){3}/g);  // ["abcabcabc"]
```



##### 15、或 |

```
'brinarybrincry'.match(/brin(a|c)ry/g)  // ["brinary", “brincry"]
```




##### 16、子项：用小括号包起来的部分称为子项：

```
'2017-06-02'.replace(/(\d{4})-(\d{2})-(\d{2})/, ‘$2/$3/$1')
//"06/02/2017"
```


##### 17、重复子项：

```
/(\w)(\w)\2\1/.test('abba');  // true
'aaaaacccc11%%%%111ssssffffffff'.match(/(.)\1+/g) 
// ["aaaaa", "cccc", "11", "%%%%", "111", "ssss", "ffffffff"]
```


##### 18、replace的高级用法：

```
var str = ‘aaaaacvvvvv22323sddfgggsssssssfdfgfff';
str.replace(/(.)\1+/g, function ($0, $1, index, input){
    console.log($0, $1, index, input)
})
```


##### 19、转义：

```
\. => .
```


##### 20、正则的一些面试问题：
1)去掉字符串两边的的空格

```
function trim(str) { 
    return str.replace(/(^\s*)|(\s*$)/g, ""); 
}
```


2)验证QQ号码：

```
function QQ(val){
    var reg = /^[1-9]\d{4,11}$/;
    if(reg.test(val)){
         alert('验证成功')
     }else{
         alert('验证失败')
     }
}
```


3)验证邮箱：

```
function mail(str){
    var regex = /^\w+@([0-9a-z]+\.[a-z]{2,3}(\.[a-z]{2})?)$/g;
    if(regex.test(str)){
          console.log('ok');
     }else{
          console.log('erro');
     }
}
var str = '122@qq.com'
mail(str);
```


4)手机号验证：

```
function mobile(val){
    var reg = /^1[3|4|5|7|8][0-9]\d{8}$/g;
    if(reg.test(val)){
      console.log('ok');
    }else {
      console.log('erro');
    }
}
```


