# 第6章 分支语句和逻辑运算符
## 6.1 if语句
当C++程序必须决定是否执行某个操作时，通常使用if语句来实现选择。if有两种格式：if和if else。如果测试条件为true，则if语句将引导程序执行语句或语句块；如果条件是false，程序将跳过这条语句或语句块。
```
if (test-condition)
    statement
```
如果test-condition（测试条件）为true，则程序将执行statement（语句），后者既可以是一条语句，也可以是语句块。如果测试条件为false，则程序将跳过语句。
通常情况下，测试条件都是关系表达式，如那些用来控制循环的表达式。
### 6.1.1 if else语句
if语句让程序决定是否执行特定的语句或语句块，而if else语句则让程序决定执行两条语句或语句块中的哪一条。
```
if (test-condition)
    statement1
else
    statement2
```
如果测试条件为true或非零，则程序将执行statement1，跳过statement2；如果测试条件为false或0，则程序将跳过statement1，执行statement2。
### 6.1.2 格式化if else语句
if else中的两种操作都必须是一条语句。如果需要多条语句，需要用大括号将它们括起来，组成一个块语句。
### 6.1.3 if else if else结构
可以将C++的if else语句进行扩展来满足这种需求。正如读者知道的，else之后应是一条语句，也可以是语句块。由于if else语句本身是一条语句，所以可以放在else的后面：
## 6.2 逻辑表达式
逻辑OR（||）、逻辑AND（&&）和逻辑NOT（!）。
### 6.2.1 逻辑OR运算符：||
C++可以采用逻辑OR运算符（||），将两个表达式组合在一起。如果原来表达式中的任何一个或全部都为true（或非零），则得到的表达式的值为true；否则，表达式的值为false。

由于||的优先级比关系运算符低，因此不需要在这些表达式中使用括号。

C++规定，||运算符是个顺序点（sequence point）。也是说，先修改左侧的值，再对右侧的值进行判定（C++11的说法是，运算符左边的子表达式先于右边的子表达式）。如果左侧的表达式为true，则C++将不会去判定右侧的表达式，因为只要一个表达式为true，则整个逻辑表达式为true。
### 6.2.2 逻辑AND运算符：&&
仅当原来的两个表达式都为true时，得到的表达式的值才为true。
由于&&的优先级低于关系运算符，因此不必在这些表达式中使用括号。和||运算符一样，&&运算符也是顺序点，因此将首先判定左侧，并且在右侧被判定之前产生所有的副作用。如果左侧为false，则整个逻辑表达式必定为false，在这种情况下，C++将不会再对右侧进行判定。
### 6.2.3 用&&来设置取值范围
与char指针变量可以通过指向一个字符串的开始位置来标识该字符串一样，char指针数组也可以标识一系列字符串，只要将每一个字符串的地址赋给各个数组元素即可。例如，qualify [1]存储字符串“mud tug-of-war\n”的地址。然后，程序便能够将cout、strlen( )或strcmp( )用于qualify [1]，就像用于其他字符串指针一样。使用const限定符可以避免无意间修改这些字符串。

在使用取值范围测试时，应确保取值范围之间既没有缝隙，又没有重叠。另外，应确保正确设置每个取值范围。

### 6.2.4 逻辑NOT运算符：!
!运算符将它后面的表达式的真值取反。
### 6.2.5 逻辑运算符细节
C++逻辑OR和逻辑AND运算符的优先级都低于关系运算符。

!运算符的优先级高于所有的关系运算符和算术运算符。

逻辑AND运算符的优先级高于逻辑OR运算符。

C++确保程序从左向右进行计算逻辑表达式，并在知道答案后立刻停止。
### 6.2.6 其他表示方式
标识符and、or和not都是C++保留字，这意味着不能将它们用作变量名等。它们并不是C语言中的保留字，但C语言程序可以将它们用作运算符，只要在程序中包含了头文件iso646.h。C++不要求使用头文件。
## 6.3 字符函数库cctype
C++从C语言继承了一个与字符相关的、非常方便的函数软件包，它可以简化诸如确定字符是否为大写字母、数字、标点符号等工作，这些函数的原型是在头文件cctype（老式的风格中为ctype.h）中定义的。
- isalpha()字符是否为字母字符。
- isdigits()字符是否为数字字符。
- isspace()字符是否为空白，如换行符、空格和制表符。
- ispunct()字符是否为标点符号。
- isalnum()字符是否为字母数字。
- iscntrl()字符是否为控制字符。
- isgraph()字符是否为空格之外的打印字符。
- isprint()字符是否为打印字符（包括空格）。
- islower()字符是否为小写字母。
- isupper()字符是否为大写字母。
- isxdigit()字符是否为十六进制数字。
- tolower()大写字符返回小写。
- toupper()小写字符返回大写。
## 6.4 ?:运算符
它是C++中唯一一个需要3个操作数的运算符。
```
expression1 ? expression2 : expression3
```
如果expression1为true，则整个条件表达式的值为expression2的值；否则，整个表达式的值为expression3的值。
```
5 > 3 ? 10 : 12
```
条件运算符生成一个表达式，因此是一个值，可以将其赋给变量或将其放到一个更大的表达式中。
## 6.5 switch语句
```
switch (integer-expression)
{
    case label1 : statement(s)
    case label2 : statement(s)
    ...
    default :statement(s)
}
```
执行到switch语句时，程序将跳到使用integer-expression的值标记的那一行。integer-expression必须是一个结果为整数值的表达式。另外，每个标签都必须是整数常量表达式。最常见的标签是int或char常量（如1或'q'），也可以是枚举量。如果integer-expression不与任何标签匹配，则程序将跳到标签为default的那一行。Default标签是可选的，如果被省略，而又没有匹配的标签，则程序将跳到switch后面的语句处执行。

C++中的case标签只是行标签，而不是选项之间的界线。程序跳到switch中特定代码行后，将依次执行之后的所有语句，除非有明确的其他指示。程序不会在执行到下一个case处自动停止，要让程序执行完一组特定语句后停止，必须使用break语句。这将导致程序跳到switch后面的语句处执行。
### 6.5.1 将枚举量用作标签
当switch语句将int值和枚举量标签进行比较时，将枚举量提升为int。另外，在while循环测试条件中，也会将枚举量提升为int类型。
### 6.5.2 switch和if else
if else可以处理取值范围。

switch语句中的每一个case标签都必须是一个单独的值。这个值必须是整数。
## 6.6 break和continue语句
可以在switch语句或任何循环中使用break语句，使程序跳到switch或循环后面的语句处执行。continue语句用于循环中，让程序跳过循环体中余下的代码，并开始新一轮循环。

虽然continue语句导致该程序跳过循环体的剩余部分，但不会跳过循环的更新表达式。在for循环中，continue语句使程序直接跳到更新表达式处，然后跳到测试表达式处。然而，对于while循环来说，continue将使程序直接跳到测试表达式处，因此while循环体中位于continue之后的更新表达式都将被跳过。

C++也有goto语句。
## 6.7 读取数字的循环
clear( )方法重置错误输入标记，同时也重置文件尾。输入错误和EOF都将导致cin返回false。
```
while (!(cin >> golf[i])){
    cin.clear();
    while (cin.get() != '\n')
        continue;
    cout << "Please enter a number: ";
}
```
如果用户输入88，则cin表达式将为true，因此将一个值放到数组中；而表达式!(cin >> golf [i])为false，因此结束内部循环。然而，如果用户输入must i?，则cin表达式将为false，因此不会将任何值放到数组中；而表达式!(cin >> golf [i])将为true，因此进入内部的while循环。该循环的第一条语句使用clear( )方法重置输入，如果省略这条语句，程序将拒绝继续读取输入。接下来，程序在while循环中使用cin.get( )来读取行尾之前的所有输入，从而删除这一行中的错误输入。另一种方法是读取到下一个空白字符，这样将每次删除一个单词，而不是一次删除整行。最后，程序告诉用户，应输入一个数字。
## 6.8 简单文件输入/输出
### 6.8.1 文本I/O和文本文件
使用cin进行输入时，程序将输入视为一系列的字节，其中每个字节都被解释为字符编码。不管目标数据类型是什么，输入一开始都是字符数据——文本数据。然后，cin对象负责将文本转换为其他类型。

控制台输入的文件版本是文本文件，即每个字节都存储了一个字符编码的文件。并非所有的文件都是文本文件，例如，数据库和电子表格以数值格式（即二进制整数或浮点格式）来存储数值数据。另外，字处理文件中可能包含文本信息，但也可能包含用于描述格式、字体、打印机等的非文本数据。

### 6.8.2 写入到文本文件中
对于文件输入，C++使用类似于cout的东西。
cout的一些事实：
- 必须包含头文件iostream。
- 头文件iostream定义了一个用处理输出的ostream类。
- 头文件iostream声明了一个名为cout的ostream变量（对象）。
- 必须指明名称空间std；例如，为引用元素cout和endl，必须使用编译指令using或前缀std::。
- 可以结合使用cout和运算符<<来显示各种类型的数据。

文件输出与此极其相似。
- 必须包含头文件fstream。
- 头文件fstream定义了一个用于处理输出的ofstream类。
- 需要声明一个或多个ofstream变量（对象），并以自己喜欢的方式对其进行命名，条件是遵守常用的命名规则。
- 必须指明名称空间std；例如，为引用元素ofstream，必须使用编译指令using或前缀std::。
- 需要将ofstream对象与文件关联起来。为此，方法之一是使用open()方法。
- 使用完文件后，应使用方法close( )将其关闭。
- 可结合使用ofstream对象和运算符<<来输出各种类型的数据。
虽然头文件iostream提供了一个预先定义好的名为cout的ostream对象，但您必须声明自己的ofstream对象，为其命名，并将其同文件关联起来。
```
ofstream outFile;
ofstrean fout;
```
下面演示了如何将这种对象与特定的文件关联起来：
```
outFile.open("fish.txt");
char filename[50];
cin >> filename;
fout.open(filename);
```
下面演示了如何使用这种对象：
```
double wt = 125.8;
outFile << wt;
char line[81] = "Objects are closer than they appear.";
fout << line << endl;
```
声明一个ofstream对象并将其同文件关联起来后，便可以像使用cout那样使用它。所有可用于cout的操作和方法（如<<、endl和setf( )）都可用于ofstream对象。
使用文件输出的主要步骤如下。
1. 包含头文件fstream。
2. 创建一个ofstream对象。
3. 将该ofstream对象同一个文件关联起来。
4. 就像使用cout那样使用该ofstream对象。

该程序运行之前，文件carinfo.txt并不存在。在这种情况下，方法open( )将新建一个名为carinfo.txt的文件。如果在此运行该程序，文件carinfo.txt将存在，此时情况将如何呢？默认情况下，open( )将首先截断该文件，即将其长度截短到零——丢其原有的内容，然后将新的输出加入到该文件中。
### 6.8.3 读取文本文件
控制台输入涉及多个方面，下面首先总结这些方面。
- 必须包含头文件iostream。
- 头文件iostream定义了一个用处理输入的istream类。
- 头文件iostream声明了一个名为cin的istream变量（对象）。
- 必须指明名称空间std；例如，为引用元素cin，必须使用编译指令using或前缀std::。
- 可以结合使用cin和运算符>>来读取各种类型的数据。
- 可以使用cin和get( )方法来读取一个字符，使用cin和getline( )来读取一行字符。
- 可以结合使用cin和eof( )、fail( )方法来判断输入是否成功。
- 对象cin本身被用作测试条件时，如果最后一个读取操作成功，它将被转换为布尔值true，否则被转换为false。

文件输出与此极其相似：
- 必须包含头文件fstream。
- 头文件fstream定义了一个用于处理输入的ifstream类。
- 需要声明一个或多个ifstream变量（对象），并以自己喜欢的方式对其进行命名，条件是遵守常用的命名规则。
- 必须指明名称空间std；例如，为引用元素ifstream，必须使用编译指令using或前缀std::。
- 需要将ifstream对象与文件关联起来。为此，方法之一是使用open( )方法。
- 使用完文件后，应使用close( )方法将其关闭。
- 可结合使用ifstream对象和运算符>>来读取各种类型的数据。
- 可以使用ifstream对象和get( )方法来读取一个字符，使用ifstream对象和getline( )来读取一行字符。
- 可以结合使用ifstream和eof( )、fail( )等方法来判断输入是否成功。
- ifstream对象本身被用作测试条件时，如果最后一个读取操作成功，它将被转换为布尔值true，否则被转换为false。
```
ifstream inFile;
ifstream fin;

inFile.open("bowling.txt");
char filename[50];
cin >> filename;
fin.open(filename);

double wt;
inFile >> wt;
char line[81];
fin.getline(line, 81);
```
声明一个ifstream对象并将其同文件关联起来后，便可以像使用cin那样使用它。所有可用于cin的操作和方法都可用于ifstream对象（如前述示例中的inFile和fin）。

如果试图打开一个不存在的文件用于输入，情况将如何呢？这种错误将导致后面使用ifstream对象进行输入时失败。检查文件是否被成功打开的首先方法是使用方法is_open( )
```
inFile.open("bowling.txt");
if (!inFile.is_open())
{
    exit(EXIT_FAILURE);
}
```
如果文件被成功地打开，方法is_open( )将返回true；因此如果文件没有被打开，表达式!inFile.isopen( )将为true。函数exit( )的原型是在头文件cstdlib中定义的，在该头文件中，还定义了一个用于同操作系统通信的参数值EXIT_FAILURE。函数exit( )终止程序。

需要特别注意的是文件读取循环的正确设计。读取文件时，有几点需要检查。首先，程序读取文件时不应超过EOF。如果最后一次读取数据时遇到EOF，方法eof( )将返回true。其次，程序可能遇到类型不匹配的情况。

一种更简单的方法是使用good( )方法，该方法在没有发生任何错误时返回true
## 6.9 总结
