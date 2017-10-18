---
title: Android代码规范
date: 2017-10-16 16:30:05
tags: [Android]
categories: 代码规范
---

### 一：文件命名规范：

#### 1、Class文件命名：

① 类文件名采用`驼峰`命名法，以`大写字母`开头；

② 继承组件的类应该以组件名结尾，例如：`XxxActivity`，`XxxService`，`XxxReceiver`，`XxxProvider`， `XxxFragment`，`XxxDialog`...

② 自定义控件以继承的控件名结尾，例如：`xxxImage`， `xxxButton`， `xxxView`，`xxxLayout`...

③ 工具类以`Utils`结尾，例如：`HttpUtils`，`ImageLoadUtils`，`SPUtils`...

#### 2、Resources 文件命名：

① drawable文件命名：

| Asset Type |     前缀     |                  示例                  |
| :--------: | :--------: | :----------------------------------: |
| Action bar |   `ab_`    |             `ab_setting`             |
|   Button   |   `btn_`   | `btn_home_normal`，`btn_home_pressed` |
|  Divider   | `divider_` |          `divider_vertical`          |
|    Icon    |   `ic_`    |              `ic_start`              |
|    Menu    |  `menu_`   |             `menu_share`             |
|    Tabs    |   `tab_`   |              `tab_news`              |
| background |   `_bg`    |              `login_bg`              |

② 选择器状态的文件命名：

|  State   |  Suffix 尾缀  |         示例          |
| :------: | :---------: | :-----------------: |
|  Normal  |  `_normal`  |  `ic_order_normal`  |
| Pressed  | `_pressed`  | `ic_order_pressed`  |
| Focused  | `_focused`  | `ic_order_focused`  |
| Disabled | `_disabled` | `ic_order_disabled` |
| Selected | `_selected` | `ic_order_selected` |

③ layout文件命名：`layout_main`, `fragment_home`, `item_photo`，`dialog_change_password`，`popup_date`...

④ 控件id命名：

|       控件       |   缩写   |      示例       |
| :------------: | :----: | :-----------: |
|  LinearLayout  |  `ll`  |  `ll_friend`  |
| RelativeLayout |  `rl`  | `rl_message`  |
|  FrameLayout   |  `fl`  |   `fl_cart`   |
|  TableLayout   | `tab`  |   `tl_news`   |
|  RecyclerView  |  `rv`  |   `rv_list`   |
|     Button     | `btn`  | `btn_publish` |
|  ImageButton   | `ibtn` | `ibtn_avatar` |
|    TextView    |  `tv`  |   `tv_name`   |
|   ImageView    |  `iv`  |   `iv_head`   |
|    EditText    |  `et`  | `et_password` |



### 代码内部命名：

① 类变量命名：

- 公有变量按`小驼峰`命名；


- 静态常量以`大写字母+下划线`命名；
- 非公有&非静态变量以`m`开头；
- 私有&静态变量以`s`开头；
- 使用`功能/描述`+`类型`命名；
- 变量较多，`分类摆放`并`注释`；
- 接口类在`最后`；
- `get`，`set`方法去掉`m`
- 方法形参用`_`开头
- 方法名见名知意
- 尽量使用三目运算符
- 接口尽量不要使用内部类，多个接口方法加上开始-结束注释
- `if` 判断加上 `{}`

示例：

```java
public class CodeStandard implements LoginType {
  
  	// 公有变量按小驼峰命名；
    public String userName = "zhangSan";
  
  	// 静态常量以大写字母+下划线命名；
  	public final static LOGIN_TYPE = "weixnLogin";
  
  	// 非公有&非静态变量以m开头；
  	private String mPassword = "123456";
  
  	// 私有&静态变量以s开头；
  	private static String sAddress = "上海"
      
    private Login mLogin;
      
    public void init() {
        mLogin.setLogin(this)
    }
    
    // 方法形参用 _ 开头
    public void setPassword(String _password) {
        this.mPassword = _password;
    }
  
  	public String getPassword() {
        this.mPassword;
    }
  
  	// 方法名见名知意，尽量使用三目运算符。
  	public int max(int _value1, int _value2){
        return _value1 > _value ? _value1 : _value2
    }
  
  
  	<!-- 登录类型的接口方法 start-->
    public void qqLogin() {
        ...
    }
  
    public void weixinLogin() {
        ...
    }
  	<!-- 登录类型的接口方法 end-->
}
```



 



