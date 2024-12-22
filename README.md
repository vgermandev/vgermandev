I am φίλος γνώσης working on a new computer language with the name __LKN__.

Please check the few notes below about it.

## LKN in one line


LKN is a computer language. “LKN” stands for “Language of Knowledge” or “Love for Knowledge.”
It can be used as a calculator, programming language, or inference/rule engine.
The programming language part is inspired by Smalltalk-80. C++20 is used to implement LKN interpreter.

Here is an example of arithmetic calculations:
````
LKN>2+5*4-6/2
19
````

Multiplication and division have a higher preference compared to addition and subtraction.
Calculation steps:
* 5*4=20
* 2+20=22
* 6/2=3
* 22-3=19

Parentheses can be used:
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

LKN strings are sequences of characters enclosed in backticks:
````
LKN>`Hello World`
Hello World
````
Strings can be added:
````
LKN>`Hello` + ` ` + `World`
Hello World
````

Numbers can be converted to strings:
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
Note: the above line consists of 4 sentences, each ending with a dot.
Last dot can be omitted.

### LKN collections.


#### Arrays.

Here is an array of 3 integers and how to extract element number 3 using “at:”:
````
LKN>Array(1 2 3) at:3
3
````

Adding arrays:
````
LKN>(Array(`e1`  `e2`  `e3`) + Array(`i1`  `i2`  `i3`)) at:2
e2i2
````

An array can be expanded by adding an element to it:
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


LKN has blocks. A block may have one or many statements. Block enclosed in brackets, block may have parameters:

[:l :r | l+r]

where ```:l :r ``` are two parameters.

To value block with parameters, the keyword “value:” can be used.
````
LKN>[:l :r | l+r] value:2 value:4
6
LKN>[:l :r | l+r] value:`abc` value:`XYZ`
abcXYZ
````
parameter names can be used to evaluate block:

````
[:l :r | l+r] l:`abc` r:`XYZ`
abcXYZ
[:l :r | l+r] r:`XYZ` l:`abc`
abcXYZ
````
Note that changing the parameter order is not affecting result

Internal variables can be used in a block:
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
Block can be assigned to variables:
````
LKN>b1:=[:l :r | v1:=10. l+r+v1+e]. e:=1000. b1 value:20 value:30
1060
````


### LKN Comparison operators


Numbers can be compared:
````
LKN>2>5
False

LKN>5>2
True

LKN>10 >= 5*2
True

LKN>9 >= 5*2
False

Strings can be compared:
LKN>`12`<`23`
True
LKN>`12`>`23`
False
LKN>`12`==`12`
True
LKN>`123`>`12`
True


````

Logic expressions can be constructed with the operators & and |, where “&” represents logical “AND” and “|” represents logical “OR”:
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

Here is the equivalent of “if then else”:
````
LKN>(2>=3)ifTrue:[`it is True` println]ifFalse:[`it is false` println].
it is false
````

### LKN supports loops:
````
LKN>sum:=0. i:=0. [i <= 5]whileTrue:[sum:=sum+i. i:= i+1]. sum println.
15

LKN>sum:=0. i:=0. [i > 5]whileFalse:[sum:=sum+i. i:= i+1]. sum println.
15 
````


### Collection can be iterated, and lambda/block can be applied to each element.
````
LKN>prod:=1.Array(1 2 3)do:[:i| (i+1) println].
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

LKN>Dlist(1 2 4 6 8 10) select:[:e|e>7]
DList(8 10)

LKN>Dlist(`a` `b` `c` `d`) select:[:e|e == `c` || e == `a`]
DList(a c)

````

### Recursion with blocks

Here is a recursive implementation of Factorial:
````
LKN>factorial:=[:n|| (n < 2)ifTrue:[1] ifFalse:[n*factorial n:(n-1)]].
Nil
LKN>factorial n:1
1
LKN>factorial n:2
2
LKN>factorial n:3
6
LKN>factorial n:4
24
````


## LKN Classes and Instances


To declare symbol to be class:
````
LKN>Person is a Class
Class Person
````

To add 3 attributes such as name, height, and weight:
````
LKN>Person instance has: name; has: height; has: weight.
Instance definition of Class Person
````

To instantiate a new Person and assign the new instance to a variable, one can do:
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

### LKN Class methods

Let's add a  method to class Person to calculate BMI (Body Mass Index):
````
LKN>Person implements:[getBmi|| weight/(height*height)].
````
Let call it
````
LKN>mia getBmi
19.03114186851211
````

### LKN Rules.

Examples of LKN shown so far are examples of LKN as a programming language.
Here is an example of LKN as a rule engine.

Let’s add a new field to Person's "bmi" with a rule attached to it:

````
Person has: bmi per [:height :weight| bmi:(weight/(height*height))].
````

To test it we need to start LKN fresh and enter/copy-paste the following sequence into the LKN shell:

````
Person is a Class.
Person instance has: name; has:height; has: weight.
Person implements:[getBmi|| weight/(height*height)].
Person has: bmi per [:height :weight| bmi:(weight/(height*height))].
mia refers to new Person with name:`Mia`;weight:55.0; height:1.7.
(`Mia's bmi: ` + (mia getBmi) asString) println.
(`Mia's bmi from rule: ` + (mia bmi) asString) println.
mia weight:85.
mia bmi println.
````

Below is what we can see on the screen:

````
LKN>Person is a Class.
Definition of Class Person
LKN>Person instance has: name; has:height; has: weight.
Instance definition of Class Person
LKN>Person implements:[getBmi|| weight/(height*height)].
Class Person
LKN>Person has: bmi per [:height :weight| bmi:(weight/(height*height))].
Class Person
LKN>mia refers to new Person with name:`Mia`;weight:55.0; height:1.7.
Nil
LKN>(`Mia's bmi: ` + (mia getBmi) asString) println.
Mia's bmi: 19.031142

LKN>(`Mia's bmi from rule: ` + (mia bmi) asString) println.
Mia's bmi from rule: 19.031142

LKN>mia weight:85.
Instance of Person
LKN>mia bmi println.
29.41176470588235
````
Please note that Mia had a weight of 55 and a BMI of 19.031142—somewhat on the lower side.
Then we change the weight to 85. As a result, Mias's bmi becomes 29.41176470588235, which is bmi of an overweight person.
Ah, we just contradict the title of this article: "LKN in one line," since we break the one-line rule.
Let's get back to one line.
If one stores the below text in a file with the name Person.lkn:
````
Person is a Class.
Person instance has: name; has:height; has: weight.
Person implements:[getBmi|| weight/(height*height)].
Person has: bmi per [:height :weight| bmi:(weight/(height*height))].


mia refers to new Person with name:`Mia`;weight:55.0; height:1.7.
(`Mia's bmi: ` + (mia getBmi) asString) println.
(`Mia's bmi from rule: ` + (mia bmi) asString) println.
mia weight:85.
(`Mia's bmi after gaining 30kg : ` + (mia bmi) asString) println.
````
Then just one line can be used to evaluate all lines from this file:

````
LKN>evaluateFile:`Person.lkn`
Mia's bmi: 19.031142
Mia's bmi from rule: 19.031142
Mia's bmi after gaining 30kg : 29.411765
````

Now we have 2 ways to calculate bmi.
First on demand with method "getbmi":```[getBmi|| weight/(height*height)].```
And the second way is to use an attribute with a rule: ```bmi per [:height :weight| bmi:(weight/(height*height))].```
In the second case any changes in height or weight will trigger rule execution of bmi.

Rules can trigger each other. Please take a look at the below rule definition:

````
Person has: weight_category being one of (Obese Overweight NormalWeight UnderWeight)
		determined by 
		[:bmi |
			(bmi > 30) ifTrue:[	weight_category:Obese]ifFalse:
			[
				(bmi >=25) ifTrue:[weight_category:Overweight]ifFalse:
				[
					(bmi >=18.5 ) ifTrue:[weight_category:NormalWeight]ifFalse:
					[
						weight_category:UnderWeight
					]
				]
			]
		].
````

Once bmi of a person is known, it is possible to say if the person is Underweight,  Normal Weight, Overweight or Obese:


| BMI | Weight Category|
|-----|---------------------|
| greater then 30	 | Obese         |
| between 30 and 25	 | Overweight    |
| between 18.5 and 25| Normal Weight |
| less than 18.5     | Underweight   |

The rule is triggered by: ```[:bmi```
followed by ranges of bmi and corresponding weight_category.

Adding this rule into the Person.lkn file:

````
Person is a Class.
Person instance has: name; has:height; has: weight.
Person implements:[getBmi|| weight/(height*height)].
Person has: bmi per [:height :weight| bmi:(weight/(height*height))].
Person has: weight_category being one of (Obese Overweight NormalWeight UnderWeight)
		determined by 
		[:bmi |
			(bmi > 30) ifTrue:[	weight_category:Obese]ifFalse:
			[
				(bmi >=25) ifTrue:[weight_category:Overweight]ifFalse:
				[
					(bmi >=18.5 ) ifTrue:[weight_category:NormalWeight]ifFalse:
					[
						weight_category:UnderWeight
					]
				]
			]
		].

mia refers to new Person with name:`Mia`;weight:55.0; height:1.7.
(`Mia's bmi: ` + (mia getBmi) asString) println.
(`Mia's bmi from ruleg: ` + (mia bmi) asString) println.
mia weight:85.
(`Mia's bmi after gainin 30kg : ` + (mia bmi) asString) println.
mia weight_category println.
(`Mia's weight category: ` + mia weight_category) println.
````

Produces the following output:
````
LKN>evaluateFile:`Person.lkn`
Mia's bmi: 19.031142
Mia's bmi from rule: 19.031142
Mia's bmi after gaining 30kg : 29.411765
Overweight
Mia's weight category: Overweight
````

If mia loses 20 kg, she will get to Normal Weight:

````
LKN>mia weight:65
Instance of Person
LKN>mia bmi
22.49134948096885
LKN>mia weight_category
NormalWeight
````

2 rules triggered here sequentially:
changed weight triggered first rule, and the new value of bmi is calculated to be ````22.49134948096885 ````
The change of bmi value triggered the second rule, and mia became a normal weight with bmi ````22.49134948096885.````
 





<!--
Person is a Class.
Person instance has: name; has:height; has: weight.
mia refers to new Person with name:`Mia`;weight:55.0; height:1.7.
Person implements:[getBmi|| weight/(height*height)].
(`Mia's bmi: ` + (mia getBmi) asString) println.
-->

<!--
## To be continued ##

-->
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
