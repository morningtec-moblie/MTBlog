---
title: iOS代码规范
date: 2017-10-17
tags: [iOS,代码规范,OC]
categories: [iOS,by范献超]
author: by范献超
---


# 参考：
[Objective-C编码规范[译]](http://www.jianshu.com/p/8b76814b3663)

[IOS 编码规范整理](http://www.jianshu.com/p/f13119c179a4)

[iOS团队代码规范（OC版）](http://hawkingouyang.com/2016/09/10/7_ObjC-code-style-as-team/)



# 语言

应该使用US英语.

**应该:**
```
UIColor *myColor = [UIColor whiteColor];
```

**不应该：**
```
UIColor *myColour = [UIColor whiteColor];
```

<!-- more -->

# 代码组织

在函数分组和protocol/delegate实现中使用#pragma mark -来分类方法，要遵循以下一般结构：

```
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}
```

# 空格

缩进使用4个空格，确保在Xcode偏好设置来设置。(raywenderlich.com使用2个空格)
方法大括号和其他大括号(if/else/switch/while 等.)总是在同一行语句打开但在新行中关闭。

**应该:**

```
if (user.isHappy) {
    //Do something
} else {
    //Do something else
}
```

**不应该：**

```
if (user.isHappy)
{
  //Do something
}
else {
  //Do something else
}
```

- 在方法之间应该有且只有一行，这样有利于在视觉上更清晰和更易于组织。在方法内的空白应该分离功能，但通常都抽离出来成为一个新方法。

- 优先使用`auto-synthesis`。但如果有必要，`@synthesize` 和 `@dynamic`应该在实现中每个都声明新的一行。

- 应该避免以冒号对齐的方式来调用方法。因为有时方法签名可能有3个以上的冒号和冒号对齐会使代码更加易读。请不要这样做，尽管冒号对齐的方法包含代码块，因为Xcode的对齐方式令它难以辨认。

**应该:**

```
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];
```

**不应该：**

```
// colon-aligning makes the block indentation hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```

- 推荐使用容器符号（[]以及{}）来表示数组和字典。容器符号与内容之间应使用空格分开

```
NSArray* array = @[ [foo description], @"Another String", [bar description] ];
NSDictionary* dict = @{ NSForegroundColorAttributeName : [NSColor redColor] };
```

# 注释

- 语句注释 <br>
当需要注释时，注释应该用来解释这段特殊代码为什么要这样做。任何被使用的注释都必须保持最新或被删除。<br>
一般都避免使用块注释，因为代码尽可能做到自解释，只有当断断续续或几行代码时才需要注释。例外：这不应用在生成文档的注释

- 声明注释<br>
每个类、category和protocol都需在注释中说明它的用途以及在整个框架中的作用

- 变量注释<br>
尽可能详细地对关键变量进行注释，说明其作用


# 命名

- Apple命名规则尽可能坚持，特别是与这些相关的memory management rules (NARC)。<br><br>长的，描述性的方法和变量命名是好的。

**应该:**

```
UIButton *settingsButton;
```

**不应该：**

```
UIButton *setBut;
```

- 三个字符前缀应该经常用在类和常量命名，但在Core Data的实体名中应被忽略。对于官方的raywenderlich.com书、初学者工具包或教程，前缀'RWT'应该被使用。<br><br>常量应该使用驼峰式命名规则，所有的单词首字母大写和加上与类名有关的前缀。

**应该:**

```
static NSTimeInterval const RWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;
```

**不应该：**

```
static NSTimeInterval const fadetime = 1.7;
```

- 属性也是使用驼峰式，但首单词的首字母小写。<br>对属性使用auto-synthesis，而不是手动编写@ synthesize语句，除非你有一个好的理由。

**应该:**

```
@property (strong, nonatomic) NSString *descriptiveVariableName;
```

**不应该：**

```
id varnm;

```

## 总体命名规范（遵循苹果官方规范）

`小驼峰命名法(CamelCase):第一个单词小写字母开头，其他单词首字母大写；`

`大驼峰命名法(PascalCase):所有首字母大写。`

```

1、类名、协议名：遵循大驼峰命名法；

2、常量：这里的常量指的是宏(#define)、枚举(enum)、常量(const)等，名称遵循大驼峰命名法；

3、方法

方法名和方法参数遵循相同的规则，使用小写开头的小驼峰法；

避免使用下划线作为前缀，苹果公司保留这种使用，由第三方使用可能会导致命名冲突;

4、变量：

类成员变量，属性，局部变量，使用小写开头的小驼峰法，其中类成员变量在名称最前面加一个下划线，比如:myLovalVariable, _myInstanceVariable；变量名的名称尽量可以推测其用途，具有描述性。

5、方法的参数命名：

不要再方法名中使用类似 pointer,ptr这样的字眼去表示指针，参数本身的类型足以说明；

不要使用简写，拼出完整的单词；

6、前缀

前缀是编程接口命名的重要部分，它们区分了软件的不同功能区域：

前缀可以防止第三方开发者与Apple的命名冲突；

同样可以防止Apple内部的命名冲突；

前缀有指定格式：

它由二到三个大写字母组成，不使用下划线和子前缀，

命名类、协议、常量和typedef结构体时使用前缀。

方法名不使用前缀（因为它存在于特定类的命名空间中），私有方法可以加前缀，比如private_XXX。

结构体字段不使用前缀。
```



更多命名规则见 [IOS 编码规范整理](http://www.jianshu.com/p/f13119c179a4)

# 下划线

当使用属性时，实例变量应该使用self.来访问和改变。这就意味着所有属性将会视觉效果不同，因为它们前面都有self.。

但有一个特例：在初始化方法里，实例变量(例如，_variableName)应该直接被使用来避免getters/setters潜在的副作用。

局部变量不应该包含下划线。


# 方法

在方法签名中，应该在方法类型(-/+ 符号)之后有一个空格。在方法各个段之间应该也有一个空格(符合Apple的风格)。在参数之前应该包含一个具有描述性的关键字来描述参数。

"and"这个词的用法应该保留。它不应该用于多个参数来说明，就像initWithWidth:height以下这个例子：

**应该:**

```
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```

**不应该：**

```
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  // Never do this.
```

# 变量

变量尽量以描述性的方式来命名。单个字符的变量命名应该尽量避免，除了在for()循环。

星号表示变量是指针。例如， `NSString *text` 既不是 `NSString* text` 也不是 `NSString * text`，除了一些特殊情况下常量。

私有变量 应该尽可能代替实例变量的使用。尽管使用实例变量是一种有效的方式，但更偏向于使用属性来保持代码一致性。

通过使用'back'属性(_variable，变量名前面有下划线)直接访问实例变量应该尽量避免，除了在初始化方法(`init, initWithCoder:`, 等…)，dealloc 方法和自定义的setters和getters。想了解关于如何在初始化方法和dealloc直接使用Accessor方法的更多信息，查看这里

**应该:**

```
@interface RWTTutorial : NSObject

@property (strong, nonatomic) NSString *tutorialName;

@end
```

**不应该：**

```
@interface RWTTutorial : NSObject {
  NSString *tutorialName;
}
```

# 属性特性

所有属性特性应该显式地列出来，有助于新手阅读代码。属性特性的顺序应该是storage、atomicity，与在Interface Builder连接UI元素时自动生成代码一致。

**应该:**

```
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (strong, nonatomic) NSString *tutorialName;
```

**不应该：**

```
@property (nonatomic, weak) IBOutlet UIView *containerView;
@property (nonatomic) NSString *tutorialName;
```

NSString应该使用copy 而不是 strong的属性特性。

为什么？即使你声明一个NSString的属性，有人可能传入一个NSMutableString的实例，然后在你没有注意的情况下修改它。

**应该:**

```
@property (copy, nonatomic) NSString *tutorialName;
```

**不应该：**

```
@property (strong, nonatomic) NSString *tutorialName;
```

# 点符号语法

点语法是一种很方便封装访问方法调用的方式。当你使用点语法时，通过使用getter或setter方法，属性仍然被访问或修改。想了解更多，阅读这里

点语法应该总是被用来访问和修改属性，因为它使代码更加简洁。[]符号更偏向于用在其他例子。

**应该:**

```
NSInteger arrayCount = self.array.count;
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**不应该：**

```
NSInteger arrayCount = [self.array count];
[view setBackgroundColor:[UIColor orangeColor]];
[[UIApplication sharedApplication] delegate];
```

# 字面值

NSString, NSDictionary, NSArray, 和 NSNumber的字面值应该在创建这些类的不可变实例时被使用。请特别注意nil值不能传入NSArray和NSDictionary字面值，因为这样会导致crash。

**应该:**

```
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```

**不应该：**

```
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```

# 常量

常量是容易重复被使用和无需通过查找和代替就能快速修改值。常量应该使用static来声明而不是使用#define，除非显式地使用宏。

**应该:**

```
static NSString * const RWTAboutViewControllerCompanyName = @"RayWenderlich.com";

static CGFloat const RWTImageThumbnailHeight = 50.0;
```

**不应该：**

```
#define CompanyName @"RayWenderlich.com"
#define thumbnailHeight 2
```

# 枚举类型

当使用enum时，推荐使用新的固定基本类型规格，因为它有更强的类型检查和代码补全。现在SDK有一个宏NS_ENUM()来帮助和鼓励你使用固定的基本类型。

例如:

```
typedef NS_ENUM(NSInteger, RWTLeftMenuTopItemType) {
  RWTLeftMenuTopItemMain,
  RWTLeftMenuTopItemShows,
  RWTLeftMenuTopItemSchedule
};
```

你也可以显式地赋值(展示旧的k-style常量定义)：

```
typedef NS_ENUM(NSInteger, RWTGlobalConstants) {
  RWTPinSizeMin = 1,
  RWTPinSizeMax = 5,
  RWTPinCountMin = 100,
  RWTPinCountMax = 500,
};
```
旧的k-style常量定义应该避免除非编写Core Foundation C的代码。

**不应该：**

```
enum GlobalConstants {
  kMaxPinSize = 5,
  kMaxPinCount = 500,
};
```

# Case语句

大括号在case语句中并不是必须的，除非编译器强制要求。当一个case语句包含多行代码时，大括号应该加上。

```
switch (condition) {
  case 1:
    // ...
    break;
  case 2: {
    // ...
    // Multi-line example using braces
    break;
  }
  case 3:
    // ...
    break;
  default: 
    // ...
    break;
}
```

有很多次，当相同代码被多个cases使用时，一个fall-through应该被使用。一个fall-through就是在case最后移除'break'语句，这样就能够允许执行流程跳转到下一个case值。为了代码更加清晰，一个fall-through需要注释一下。

```
switch (condition) {
  case 1:
    // ** fall-through! **
  case 2:
    // code executed for values 1 and 2
    break;
  default: 
    // ...
    break;
}
```

当在switch使用枚举类型时，'default'是不需要的。例如：

```
RWTLeftMenuTopItemType menuType = RWTLeftMenuTopItemMain;

switch (menuType) {
  case RWTLeftMenuTopItemMain:
    // ...
    break;
  case RWTLeftMenuTopItemShows:
    // ...
    break;
  case RWTLeftMenuTopItemSchedule:
    // ...
    break;
}
```

# 私有属性

私有属性应该在类的实现文件中的类扩展(匿名分类)中声明，命名分类(比如RWTPrivate或private)应该从不使用除非是扩展其他类。匿名分类应该通过使用<headerfile>+Private.h文件的命名规则暴露给测试。

例如:

```
@interface RWTDetailViewController ()

@property (strong, nonatomic) GADBannerView *googleAdView;
@property (strong, nonatomic) ADBannerView *iAdView;
@property (strong, nonatomic) UIWebView *adXWebView;

@end
```

# 布尔值

Objective-C使用YES和NO。因为true和false应该只在CoreFoundation，C或C++代码使用。既然nil解析成NO，所以没有必要在条件语句比较。不要拿某样东西直接与YES比较，因为YES被定义为1和一个BOOL能被设置为8位。

这是为了在不同文件保持一致性和在视觉上更加简洁而考虑。

**应该:**

```
if (someObject) {}
if (![anotherObject boolValue]) {}
```

**不应该：**

```
if (someObject == nil) {}
if ([anotherObject boolValue] == NO) {}
if (isAwesome == YES) {} // Never do this.
if (isAwesome == true) {} // Never do this.
如果BOOL属性的名字是一个形容词，属性就能忽略"is"前缀，但要指定get访问器的惯用名称。例如：

@property (assign, getter=isEditable) BOOL editable;
文字和例子从这里引用Cocoa Naming Guidelines
```

# 条件语句

条件语句主体为了防止出错应该使用大括号包围，即使条件语句主体能够不用大括号编写(如，只用一行代码)。这些错误包括添加第二行代码和期望它成为if语句；还有，even more dangerous defect可能发生在if语句里面一行代码被注释了，然后下一行代码不知不觉地成为if语句的一部分。除此之外，这种风格与其他条件语句的风格保持一致，所以更加容易阅读。

**应该:**

```
if (!error) {
  return success;
}
```

**不应该：**

```
if (!error)
  return success;
```

或

```
if (!error) return success;
```

# 三元操作符

当需要提高代码的清晰性和简洁性时，三元操作符?:才会使用。单个条件求值常常需要它。多个条件求值时，如果使用if语句或重构成实例变量时，代码会更加易读。一般来说，最好使用三元操作符是在根据条件来赋值的情况下。

Non-boolean的变量与某东西比较，加上括号()会提高可读性。如果被比较的变量是boolean类型，那么就不需要括号。

**应该:**

```
NSInteger value = 5;
result = (value != 0) ? x : y;

BOOL isHorizontal = YES;
result = isHorizontal ? x : y;
```

**不应该：**

```
result = a > b ? x = c > d ? c : d : y;
```

# Init方法

Init方法应该遵循Apple生成代码模板的命名规则。返回类型应该使用instancetype而不是id

```
- (instancetype)init {
  self = [super init];
  if (self) {
    // ...
  }
  return self;
}
```

查看关于instancetype的文章Class Constructor Methods


# 类构造方法

当类构造方法被使用时，它应该返回类型是instancetype而不是id。这样确保编译器正确地推断结果类型。

```
@interface Airplane
+ (instancetype)airplaneWithType:(RWTAirplaneType)type;
@end
```

关于更多instancetype信息，请查看NSHipster.com


# CGRect函数

当访问CGRect里的x, y, width, 或 height时，应该使用CGGeometry函数而不是直接通过结构体来访问。引用Apple的CGGeometry:

在这个参考文档中所有的函数，接受CGRect结构体作为输入，在计算它们结果时隐式地标准化这些rectangles。因此，你的应用程序应该避免直接访问和修改保存在CGRect数据结构中的数据。相反，使用这些函数来操纵rectangles和获取它们的特性。
**应该:**

```
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
CGRect frame = CGRectMake(0.0, 0.0, width, height);
```

**不应该：**

```
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };
```

#
# 黄金路径

当使用条件语句编码时，左手边的代码应该是"golden" 或 "happy"路径。也就是不要嵌套if语句，多个返回语句也是OK。

**应该:**

```
- (void)someMethod {
  if (![someOther boolValue]) {
    return;
  }

  //Do something important
}
```

**不应该：**

```
- (void)someMethod {
  if ([someOther boolValue]) {
    //Do something important
  }
}
```

# 错误处理

当方法通过引用来返回一个错误参数，判断返回值而不是错误变量。

**应该:**

```
NSError *error;
if (![self trySomethingWithError:&error]) {
  // Handle Error
}
```

**不应该：**

```
NSError *error;
[self trySomethingWithError:&error];
if (error) {
  // Handle Error
}
```

在成功的情况下，有些Apple的APIs记录垃圾值(garbage values)到错误参数(如果non-NULL)，那么判断错误值会导致false负值和crash。


# 单例模式

单例对象应该使用线程安全模式来创建共享实例。

```
+ (instancetype)sharedInstance {
  static id sharedInstance = nil;

  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    sharedInstance = [[self alloc] init];
  });

  return sharedInstance;
}
```

这会防止possible and sometimes prolific crashes.

# 换行符

换行符是一个很重要的主题，因为它的风格指南主要为了打印和网上的可读性。

例如:

```
self.productsRequest = [[SKProductsRequest alloc] initWithProductIdentifiers:productIdentifiers];
一行很长的代码应该分成两行代码，下一行用两个空格隔开。

self.productsRequest = [[SKProductsRequest alloc] 
  initWithProductIdentifiers:productIdentifiers];
```

# Xcode工程

物理文件应该与Xcode工程文件保持同步来避免文件扩张。任何Xcode分组的创建应该在文件系统的文件体现。代码不仅是根据类型来分组，而且还可以根据功能来分组，这样代码更加清晰。

尽可能在target的Build Settings打开"Treat Warnings as Errors，和启用以下additional warnings。如果你需要忽略特殊的警告，使用 Clang's pragma feature。

# 语法糖

代码中使用语法糖，提高写代码效率

- NSArray

```
   //NSArray的定义
    NSArray *array = @[@"lu", @"da", @"shi", @YES, @123];
    //NSArray的访问
    array[index];
```
    
- NSDictionary

```
   //NSDictionary的定义简化
   NSDictionary *dictionary = @{
                                @"key0" : @"value0",
                                @"key1" : @"value1",
                                @"key2" : @"value2"
                                };
    //NSDictionary访问数据简化
    dictionary[@"key2"];
```
   
- NSNumber

```
    NSNumber *a = @123;
    NSNumber *b = @11.2;
    NSNumber *c = @('a');
```

# 项目工程目录

## 当前SDK项目目录（面向对象）
- ApplicationLayer（应用层）
  - Base（基类）
  - View （UI类）
- DataAccessLayer（数据层）
  - Network（网络层）
  	 - Common（公共数据处理方法）
  	 - Model（数据模型）
  - DataSDKNeed（SDK需要数据收集）
  - Persistence（数据缓存）
- ServiceLayer(服务层)
  - Services（服务）
  	 - Common（全局pch等头文件）
  	 - Libs（第三方）
  	 - Category (分类)
  	 - Tools (工具类)
  	 - Other (其他)
  - Other(扩展)

## 其他案例：

- Modules：存放功能模块。将程序划分为多个功能模块，每个模块基于MVC/MVVM组织代码

- Library：存放三方库

- Util：存放自己封装的工具类

- Catergory：存放扩展类

- Custom：存放自定义的其他类

- MacroAndConstant：存放宏定义和常量的文件

- BaseViewController：基类，单独提出来

- SupportingFile：存放项目配置文件

- Resource：存放资源，按照图片，音频，视频不同分类存放

- Request：封装的网络请求类
