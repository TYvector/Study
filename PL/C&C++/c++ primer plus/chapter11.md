# 第11章 使用类
## 11.1 运算符重载
运算符重载是一种形式的C++多态。运算符重载将重载的概念扩展到运算符上，允许赋予C++运算符多种含义。实际上，很多C++（也包括C语言）运算符已经被重载。例如，将*运算符用于地址，将得到存储在这个地址中的值；但将它用于两个数字时，得到的将是它们的乘积。C++根据操作数的数目和类型来决定采用哪种操作。

C++允许将运算符重载扩展到用户定义的类型，重载运算符可使代码看起来更自然。

但在C++中，可以定义一个表示数组的类，并重载+运算符。

要重载运算符，需使用被称为运算符函数的特殊函数形式。运算符函数的格式如下：
```
operatorop(argument-list)
```
operator +( )重载+运算符，operator * ( )重载*运算符。op必须是有效的C++运算符，不能虚构一个新的符号。operator 函数将重载[ ]运算符，因为[ ]是数组索引运算符。假设有一个
Salesperson类，并为它定义了一个operator +( )成员函数，以重载+运算符，以便能够将两个Saleperson对象的销售额相加，则如果district2、sid和sara都是Salesperson类对象，便可以编写这样的等式：
```
district2 = sid + sara;
```
编译器发现，操作数是Salesperson类对象，因此使用相应的运算符函数替换上述运算符：
```
district2 = sid.operator+(sara);
```
然后该函数将隐式地使用sid（因为它调用了方法），而显式地使用sara对象（因为它被作为参数传递），来计算总和，并返回这个值。当然最重要的是，可以使用简便的+运算符表示法，而不必使用笨拙的函数表示法。
## 11.2 计算时间：一个运算符重载示例
将参数声明为引用的目的是为了提高效率。

不要返回指向局部变量或临时对象的引用。函数执行完毕后，局部变量和临时对象将消失，引用将指向不存在的数据。
### 11.2.1 添加加法运算符
```
total = coding + fixing;
```
注意，在运算符表示法中，运算符左侧的对象（这里为coding）是调用对象，运算符右边的对象（这里为fixing）是作为参数被传递的对象。

operator +( )函数的名称使得可以使用函数表示法或运算符表示法来调用它。编译器将根据操作数的类型来确定如何做：

可以将两个以上的对象相加吗？

### 11.2.2 重载限制
多数C++运算符（参见表11.1）都可以用这样的方式重载。重载的运算符（有些例外情况）不必是成员函数，但必须至少有一个操作数是用户定义的类型。下面详细介绍C++对用户定义的运算符重载的限制。

1. 重载后的运算符必须至少有一个操作数是用户定义的类型，这将防止用户为标准类型重载运算符。因此，不能将减法运算符（−）重载为计算两个double值的和，而不是它们的差。虽然这种限制将对创造性有所影响，但可以确保程序正常运行。
2. 使用运算符时不能违反运算符原来的句法规则。例如，不能将求模运算符（%）重载成使用一个操作数：同样，不能修改运算符的优先级。因此，如果将加号运算符重载成将两个类相加，则新的运算符与原来的加号具有相同的优先级。
3. 不能创建新运算符。例如，不能定义operator **( )函数来表示求幂。
4. 不能重载下面的运算符。
- sizeof：sizeof运算符。
- .：成员运算符。
- . *：成员指针运算符。
- ::：作用域解析运算符。
- ?:：条件运算符。
- typeid：一个RTTI运算符。
- const_cast：强制类型转换运算符。
- dynamic_cast：强制类型转换运算符。
- reinterpret_cast：强制类型转换运算符。
- static_cast：强制类型转换运算符。

5. 表中的大多数运算符都可以通过成员或非成员函数进行重载，但下面的运算符只能通过成员函数进行重载。
- =：赋值运算符。
- ( )：函数调用运算符。
- [ ]：下标运算符。
- ->：通过指针访问类成员的运算符。

+|-|*|/|%|^
:-:|:-:|:-:|:--:|:--:|:-:
&|\||~=|!|=|<
\>|+=|-=|*=|/=|%=
^=|&=|\|=|<<|>>|>>=
<<=|==|!=|<=|>=|&&
\|\||++|--|,|->*|->
()|[]|new|delete|new[]|delete[]

除了这些正式限制之外，还应在重载运算符时遵循一些明智的限制。例如，不要将*运算符重载成交换两个Time对象的数据成员。表示法中没有任何内容可以表明运算符完成的工作，因此最好定义一个其名称具有说明性的类方法，如Swap( )。
### 11.2.3 其他重载运算符

## 11.3 友元
C++提供了另外一种形式的访问权限：友元。友元有3种：
- 友元函数；
- 友元类；
- 友元成员函数。
  
通过让函数成为类的友元，可以赋予该函数与类的成员函数相同的访问权限。

在前面的Time类示例中，重载的乘法运算符与其他两种重载运算符的差别在于，它使用了两种不同的类型。也就是说，加法和减法运算符都结合两个Time值，而乘法运算符将一个Time值与一个double值结合在一起。这限制了该运算符的使用方式。记住，左侧的操作数是调用对象。也就是说，下面的语句：
```
A = B * 2.75;
/*将被转换为下面的成员函数调用：*/
A = B.operator*(2.75);
```
但下面的语句又如何呢？
```
A = 2.75 * B;
```
从概念上说，2.75 * B应与B *2.75相同，但第一个表达式不对应于成员函数，因为2.75不是Time类型的对象。记住，左侧的操作数应是调用对象，但2.75不是对象。因此，编译器不能使用成员函数调用来替换该表达式。

解决这个难题的一种方式是，告知每个人（包括程序员自己），只能按B * 2.75这种格式编写，不能写成2.75 * B。这是一种对服务器友好-客户警惕的（server-friendly, client-beware）解决方案，与OOP无关。

然而，还有另一种解决方式——非成员函数（记住，大多数运算符都可以通过成员或非成员函数来重载）。非成员函数不是由对象调用的，它使用的所有值（包括对象）都是显式参数。这样，编译器能够将下面的表达式：
```
A = 2.75 * B;
/*与下面的非成员函数调用匹配：*/
A = operator*(2.75, B);
/*该函数的原型如下：*/
Time operator*(double m, const Time & t);
```
对于非成员重载运算符函数来说，运算符表达式左边的操作数对应于运算符函数的第一个参数，运算符表达式右边的操作数对应于运算符函数的第二个参数。而原来的成员函数则按相反的顺序处理操作数，也就是说，double值乘以Time值。

使用非成员函数可以按所需的顺序获得操作数（先是double，然后是Time），但引发了一个新问题：非成员函数不能直接访问类的私有数据，至少常规非成员函数不能访问。然而，有一类特殊的非成员函数可以访问类的私有成员，它们被称为友元函数
### 11.3.1 创建友元
创建友元函数的第一步是将其原型放在类声明中，并在原型声明前加上关键字friend：
```
friend Time operator*(double m, const Time & t);
```
该原型意味着下面两点：
- 虽然operator *( )函数是在类声明中声明的，但它不是成员函数，因此不能使用成员运算符来调用；
- 虽然operator *( )函数不是成员函数，但它与成员函数的访问权限相同。

第二步是编写函数定义。因为它不是成员函数，所以不要使用Time::限定符。另外，不要在定义中使用关键字friend，定义应该如下：
```
Time operator*(double m, const Time & t)
{
    .....
}
```
总之，类的友元函数是非成员函数，其访问权限与成员函数相同。

应将友元函数看作类的扩展接口的组成部分。只有类声明可以决定哪一个函数是友元，因此类声明仍然控制了哪些函数可以访问私有数据。总之，类方法和友元只是表达类接口的两种不同机制。

如果要为类重载运算符，并将非类的项作为其第一个操作数，则可以用友元函数来反转操作数的顺序。
### 11.3.2 常用的友元：重载<<运算符
一个很有用的类特性是，可以对<<运算符进行重载，使之能与cout一起来显示对象的内容。
#### <<的第一种重载版本
要使Time类知道使用cout，必须使用友元函数。
```
void operator<<(ostream & os, const Time & t)
{
    os << t.hours << " hours, " << t.minutes << " minutes";
}
```
这样可以使用下面的语句：
```
cout << trip;
```
新的Time类声明使operatro<<( )函数成为Time类的一个友元函数。但该函数不是ostream类的友元。

调用cout << trip应使用cout对象本身，而不是它的拷贝，因此该函数按引用（而不是按值）来传递该对象。这样，表达式cout << trip将导致os成为cout的一个别名；而表达式cerr << trip将导致os成为cerr的一个别名。Time对象可以按值或按引用来传递，因为这两种形式都使函数能够使用对象的值。按引用传递使用的内存和时间都比按值传递少。

#### <<的第二种重载版本
ostream类将operator<<( )函数实现为返回一个指向ostream对象的引用。具体地说，它返回一个指向调用对象（这里是cout）的引用。因此，表达式(cout << x)本身就是ostream对象cout，从而可以位于<<运算符的左侧。

可以对友元函数采用相同的方法。只要修改operator<<( )函数，让它返回ostream对象的引用即可：
```
ostream & operator << (ostream & os, const Time & t)
{
    ...
    return os;
}
```

注意，返回类型是ostream &。这意味着该函数返回ostream对象的引用。因为函数开始执行时，程序传递了一个对象引用给它，这样做的最终结果是，函数的返回值就是传递给它的对象。

只有在类声明中的原型中才能使用friend关键字。除非函数定义也是原型，否则不能在函数定义中使用该关键字。
## 11.4 重载运算符：作为成员函数还是非成员函数
对于很多运算符来说，可以选择使用成员函数或非成员函数来实现运算符重载。一般来说，非成员函数应是友元函数，这样它才能直接访问类的私有数据。

加法运算符需要两个操作数。对于成员函数版本来说，一个操作数通过this指针隐式地传递，另一个操作数作为函数参数显式地传递；对于友元版本来说，两个操作数都作为参数来传递。

非成员版本的重载运算符函数所需的形参数目与运算符使用的操作数数目相同；而成员版本所需的参数数目少一个，因为其中的一个操作数是被隐式地传递的调用对象。

这两个原型都与表达式T2 + T3匹配，其中T2和T3都是Time类型对象。也就是说，编译器将下面的语句：
```
T1 = T2 + T3;
/*转换为下面两个的任何一个：*/
T1 = T2.operator+(T3);
T1 = operator+(T2, T3);
```
记住，在定义运算符时，必须选择其中的一种格式，而不能同时选择这两种格式。因为这两种格式都与同一个表达式匹配，同时定义这两种格式将被视为二义性错误，导致编译错误。

那么哪种格式最好呢？对于某些运算符来说（如前所述），成员函数是唯一合法的选择。在其他情况下，这两种格式没有太大的区别。有时，根据类设计，使用非成员函数版本可能更好（尤其是为类定义类型转换时）。
## 11.5 再谈重载：一个矢量类
这样的成员被称为状态成员（state member），因为这种成员描述的是对象所处的状态。

## 11.6 类的自动转换和强制类型转换
C++语言不自动转换不兼容的类型。在无法自动转换时，可以使用强制类型转换：
可以将类定义成与基本类型或另一个类相关，使得从一种类型转换为另一种类型是有意义的。在这种情况下，程序员可以指示C++如何自动进行转换，或通过强制类型转换来完成。

下面的构造函数用于将double类型的值转换为Stonewt类型：
```
Stonewt(double lbs);
/*也就是说，可以编写这样的代码：*/
Stonewt myCat;
myCat = 19.6;
```
程序将使用构造函数Stonewt(double)来创建一个临时的Stonewt对象，并将19.6作为初始化值。随后，采用逐成员赋值方式将该临时对象的内容复制到myCat中。这一过程称为隐式转换，因为它是自动进行的，而不需要显式强制类型转换。

只有接受一个参数的构造函数才能作为转换函数。下面的构造函数有两个参数，因此不能用来转换类型：然而，如果给第二个参数提供默认值，它便可用于转换int：
```
Stonewt(int stn, double lbs);
Stonewt(int stn, double lbs = 0);
```
将构造函数用作自动类型转换函数似乎是一项不错的特性。然而，当程序员拥有更丰富的C++经验时，将发现这种自动特性并非总是合乎需要的，因为这会导致意外的类型转换。因此，C++新增了关键字explicit，用于关闭这种自动特性。也就是说，可以这样声明构造函数：
```
explicit Stonewt(double lbs);
```
这将关闭上述示例中介绍的隐式转换，但仍然允许显式转换，即显式强制类型转换：
```
Stonewt myCat;
myCat = 19.6;
myCat = Stonewt(19.6);
myCat = (Stonewt)19.6;
```
只接受一个参数的构造函数定义了从参数类型到类类型的转换。如果使用关键字explicit限定了这种构造函数，则它只能用于显示转换，否则也可以用于隐式转换。

编译器在什么时候将使用Stonewt(double)函数呢？如果在声明中使用了关键字explicit，则Stonewt(double)将只用于显式强制类型转换，否则还可以用于下面的隐式转换。
- 将Stonewt对象初始化为double值时。
- 将double值赋给Stonewt对象时。
- 将double值传递给接受Stonewt参数的函数时。
- 返回值被声明为Stonewt的函数试图返回double值时。
- 在上述任意一种情况下，使用可转换为double类型的内置类型时。

函数原型化提供的参数匹配过程，允许使用Stonewt（double）构造函数来转换其他数值类型。也就是说，下面两条语句都首先将int转换为double，然后使用Stonewt（double）构造函数。
```
Stonewt Jumbo(7000);
Jumbo = 7300;
```
然而，当且仅当转换不存在二义性时，才会进行这种二步转换。也就是说，如果这个类还定义了构造函数Stonewt（long），则编译器将拒绝这些语句，可能指出：int可被转换为long或double，因此调用存在二义性。
### 11.6.1 转换函数
是否可以将Stonewt对象转换为double值,可以这样做，但不是使用构造函数。构造函数只用于从某种类型到类类型的转换。要进行相反的转换，必须使用特殊的C++运算符函数——转换函数。

转换函数是用户定义的强制类型转换，可以像使用强制类型转换那样使用它们。如果定义了从Stonewt到double的转换函数，就可以使用下面的转换
```
Stone wolfe(285.7);
double host = double (wolfe);
double thinker = (double) wolfe;
```
也可以让编译器来决定如何做：
```
Stonewt wells(20, 3);
double star = wells;
```
要转换为typeName类型，需要使用这种形式的转换函数：
```
operator typeName();
```

请注意以下几点：
- 转换函数必须是类方法；
- 转换函数不能指定返回类型；
- 转换函数不能有参数。

转换为double类型的函数的原型如下：
```
operator double();
```

typeName（这里为double）指出了要转换成的类型，因此不需要指定返回类型。转换函数是类方法意味着：它需要通过类对象来调用，从而告知函数要转换的值。因此，函数不需要参数。

在C++中，int和double值都可以被赋给long变量，当类定义了两种或更多的转换时，仍可以用显式强制类型转换来指出要使用哪个转换函数。

在用户不希望进行转换时，转换函数也可能进行转换。

总之，C++为类提供了下面的类型转换。
- 只有一个参数的类构造函数用于将类型与该参数相同的值转换为类类型。例如，将int值赋给Stonewt对象时，接受int参数的Stonewt类构造函数将自动被调用。然而，在构造函数声明中使用explicit可防止隐式转换，而只允许显式转换。
- 被称为转换函数的特殊类成员运算符函数，用于将类对象转换为其他类型。转换函数是类成员，没有返回类型、没有参数、名为operator typeName( )，其中，typeName是对象将被转换成的类型。将类对象赋给typeName变量或将其强制转换为typeName类型时，该转换函数将自动被调用。
### 11.6.2 转换函数和友元函数
要将double量和Stonewt量相加，有两种选择。第一种方法是（刚介绍过）将下面的函数定义为友元函数，让Stonewt(double)构造函数将double类型的参数转换为Stonewt类型的参数：
```
operator+(const Stonewt &, const Stonewt &)
```
第二种方法是，将加法运算符重载为一个显式使用double类型参数
```
Stonewt operator+(double x);
friend Stonewt operator+(double x, Stonewt &s);
```
每一种方法都有其优点。第一种方法（依赖于隐式转换）使程序更简短，因为定义的函数较少。这也意味程序员需要完成的工作较少，出错的机会较小。这种方法的缺点是，每次需要转换时，都将调用转换构造函数，这增加时间和内存开销。第二种方法（增加一个显式地匹配类型的函数）则正好相反。它使程序较长，程序员需要完成的工作更多，但运行速度较快。
如果程序经常需要将double值与Stonewt对象相加，则重载加法更合适；如果程序只是偶尔使用这种加法，则依赖于自动转换更简单，但为了更保险，可以使用显式转换。
## 11.7 总结
- 本章介绍了定义和使用类的许多重要方面，其中的一些内容可能较难理解，但随着实践经验的不断增加，您将逐渐掌握它们。
- 一般来说，访问私有类成员的唯一方法是使用类方法。C++使用友元函数来避开这种限制。要让函数成为友元，需要在类声明中声明该函数，并在声明前加上关键字friend。
- C++扩展了对运算符的重载，允许自定义特殊的运算符函数，这种函数描述了特定的运算符与类之间的关系。运算符函数可以是类成员函数，也可以是友元函数（有一些运算符函数只能是类成员函数）。要调用运算符函数，可以直接调用该函数，也可以以通常的句法使用被重载的运算符。对于运算符op，其运算符函数的格式如下：
```
operatorop(argument-list)
```
- argument-list表示该运算符的操作数。如果运算符函数是类成员函数，则第一个操作数是调用对象，它不在argument-list中。例如，本章通过为Vector类定义operator +( )成员函数重载了加法。如果up、right和result都是Vector对象，则可以使用下面的任何一条语句来调用矢量加法：
```
result = up.operator+(right);
result = up + right;
```
- 在第二条语句中，由于操作数up和right的类型都是Vector，因此C++将使用Vector的加法定义。
- 当运算符函数是成员函数时，则第一个操作数将是调用该函数的对象。例如，在前面的语句中，up对象是调用函数的对象。定义运算符函数时，如果要使其第一个操作数不是类对象，则必须使用友元函数。这样就可以将操作数按所需的顺序传递给函数了。
- 最常见的运算符重载任务之一是定义<<运算符，使之可与cout一起使用，来显示对象的内容。要让ostream对象成为第一个操作数，需要将运算符函数定义为友元；要使重新定义的运算符能与其自身拼接，需要将返回类型声明为ostream &。下面的通用格式能够满足这种要求：
```
ostream & operator<<(ostream & os, const c_name & obj)
{
    os << ...;
    return os;
}
```
- 然而，如果类包含这样的方法，它返回需要显示的数据成员的值，则可以使用这些方法，无需在operator<<( )中直接访问这些成员。在这种情况下，函数不必（也不应当）是友元。
- C++允许指定在类和基本类型之间进行转换的方式。首先，任何接受唯一一个参数的构造函数都可被用作转换函数，将类型与该参数相同的值转换为类。如果将类型与该参数相同的值赋给对象，则C++将自动调用该构造函数。例如，假设有一个String类，它包含一个将char *值作为其唯一参数的构造函数，那么如果bean是String对象，则可以使用下面的语句：
```
bean = "pinto";
```
- 然而，如果在该构造函数的声明前加上了关键字explicit，则该构造函数将只能用于显式转换：
```
bean = String("pinto");
```
- 要将类对象转换为其他类型，必须定义转换函数，指出如何进行这种转换。转换函数必须是成员函数。将类对象转换为typeName类型的转换函数的原型如下：
```
operator typeName();
```
注意，转换函数没有返回类型、没有参数，但必须返回转换后的值（虽然没有声明返回类型）。例如，下面是将Vector转换为double类型的函数：
```
Vector::operator double()
{
    ...
    return a_double_value;
}
```


