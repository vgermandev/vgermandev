I am working on new computer language with name __LKN__.

Please check below few notes about it.

## LKN in one line


LKN is a computer language. “LKN” stands for “Language of Knowledge” or “Love for Knowledge”. It can be used as Calculator, Programming Language, Inference/rule engine. Programming language part is inspirited by Smalltalk 

Here is an example of arithmetic calculations:
````
LKN>2+5*4-6/2
19
````

Multiplication and division have higher preference compare to addition and subtraction.
Calculation steps:
* 5*4=20
* 2+20=22
* 6/2=3
* 22-3=19

parentheses can be used:
````
LKN>(2+5)*4-6/2
25
````

Calculation steps:
* 2+5=7
* 7*4=28
* 6/2=3
* 28-3=25

Real Numbers:
````
LKN>2.2 * 4.0
8.8
````

Scientific notation:
````
LKN>2e3
2000

LKN>2e-3
0.002

LKN>2e10/1000000
20000

LKN>2e-6+7
7.000002
````

steps for 2e-6+7:
* 2e-6 = 0.000002
* 0.000002+7=7.000002

LKN strings are sequence of characters enclosed in  back ticks:
````
LKN>`Hello World`
Hello World
````
Strings can be added:
````
LKN>`Hello` + ` ` + `World`
Hello World
````

Numbers can be converted to strings
````
LKN>5555 asString + 6666 asString
55556666
````

compare to
````
LKN>5555+6666
12221
````

Numbers and strings can be assigned to variables:
````
LKN>var1:=4444.  var2:=7777. var3:=var1+var2. var3*2.
24442
````
Note above line consist of 4 sentences each ended with dot
Last dot can be omitted.

### LKN collections.

#### Arrays.


Here is array of 3 integers and how to extract element number 3 using “at:”
````
LKN>Array(1 2 3) at:3
3
Adding arrays:
LKN>(Array(`e1`  `e2`  `e3`) + Array(`i1`  `i2`  `i3`)) at:2
e2i2
````

Array can be expanded by adding element to it
````
LKN>((Array(`e1` `e2` `e3`)+Array(`i1` `i2` `i3`)) add:`last element`)at:4
last element
````



#### Double Linked Lists


````
LKN>Dlist(1 2 3) first
1
LKN>Dlist(1 2 3) last
3
LKN>Dlist(1 2 3) before:3
2
````


#### Sets

````
LKN>Set(1 2) add:3 println
Set(1 2 3)

LKN>Set(1 2) add:3 includes:2
True
LKN>Set(1 2) add:3 includes:22
False
````


#### Maps(collection of key value pairs):


````
LKN>Map((`k1` 1.1) (`k2` 2.2) (`k3` 3.3)) at:`k2`
2.2

LKN>Map((`k1` 1.1) (`k2` 2.2)) at:`k3` put:3.3
Map((k1 1.1) (k2 2.2) (k3 3.3))
````


### Functions/Lambdas/Closures.


LKN has blocks. Block can consist of one or many statements. Block enclosed in brackets, block may have parameters:

[:l :r | l+r]

where ```:l :r ``` are two parameters.

To value block with parameters, the keyword “value:” can be used.
````
LKN>[:l :r | l+r] value:2 value:4
6
LKN>[:l :r | l+r] value:`abc` value:`XYZ`
abcXYZ
````

Block can have internal variables:
````
LKN>[:l :r | var1:= ` it is var1 `.l+r+var1] value:`abc` value:`XYZ`
abcXYZ it is var1
````
Notice: block returns value of last statement.

Block can see variables declared outside of it’s own scope:
````
LKN>e:=`e`.[:l :r | v1:= ` v1 `.l+r+v1+e] value:`a` value:`X`
aX v1 e
````
block can be assigned to variables
````
LKN>b1:=[:l :r | v1:=10. l+r+v1+e]. e:=1000. b1 value:20 value:30
1060
````


#### LKN Comparison operators


numbers can be compared:
````
LKN>2>5
False

LKN>5>2
True

LKN>10 >= 5*2
True

LKN>9 >= 5*2
False

Strings can be compared
LKN>`12`<`23`
True
LKN>`12`>`23`
False
LKN>`12`==`12`
True
LKN>`123`>`12`
True


````

Logic expression can be constructed with operator & and |. where “&” represend logical “AND” and “|” represent logical “OR”:
````
LKN>10 >= 5*2 & 7 > 6
True

LKN>10 >= 5 | 6 > 8
True
````

### Conditional evaluation:

````
LKN>(3>=3)ifTrue:[`it is True` println]
it is True

LKN>(2>=3)ifFalse:[`it is False` println]
it is False
````

Here is equivalent of “if then else”
````
LKN>(2>=3)ifTrue:[`it is True` println]ifFalse:[`it is false` println].
it is false
````
### LKN support loops:
````
LKN>sum:=0. i:=0. [i <= 5]whileTrue:[sum:=sum+i. i:= i+1]. sum println.
15

LKN>sum:=0. i:=0. [i > 5]whileFalse:[sum:=sum+i. i:= i+1]. sum println.
15 
````


### Collection can be iterated and lambda/block can be applied to each element
````
LKN>prod:=1.Array(1 2 3)do:[:i| (i+1) println. prod:=prod*i. prod println].
2
3
4

LKN>prod:=1.Array(1 2 3)do:[:i| (i+1) println. prod:=prod*i. prod println].
2
1
3
2
4
6
````


### Blocks can be passed as parameters:

````
LKN>Dlist(1 2 4 6 8 10) detect:[:e|e>7]
8

LKN>Dlist(`a` `b` `c` `d`) select:[:e|e == `c` || e == `a`]
DList(a c)

````


### LKN Classes and Instances


To declare symbol to be class:
````
LKN>Person is a Class
Class Person
````

To add 3 attributes name, height and weight:
````
LKN>Person instance has: name; has:height; has: weight.
Instance definition of Class Person
````

To instantiate new Person and assign new instance to variable one can do:
````
mia refers to new Person with name:`Mia`;weight:55.0; height:1.7.
````

To check mia’s weight and height:
````
LKN>mia weight
55.00000000000000
LKN>mia height
1.70000000000000
````

## To be continued ##


<!--
**vgermandev/vgermandev** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
