---
title: iOS开发记录
date: 2017-09-15 09:42:18
tags:
cover: https://i.loli.net/2019/11/28/3rvwfU9nB1ldzVo.jpg
---

# iOS开发快捷方式

## Xcode7.0以上打开HTTP权限
以Open as ->Source Code 的方法打开info.plist文件，然后加入以下代码
这段代码放的位置不用固定
```
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```

## 关于Cocopods
```
pod update --no-repo-update
pod install --verbose --no-repo-update

```
## Podfile 默认初始化文本
```
platform :ios , '8.0'
use_frameworks!
inhibit_all_warnings!  ##屏蔽pod一切警告
target 'ProjectName’ do
  pod 'AFNetworking', '~> 2.6'
  pod 'FMDB'
  pod 'MJRefresh'
  pod 'MJExtension'
  pod 'ShareSDK3'
  
end

```

<!--more-->


### CocoaPods中的头文件import导入时不能自动补齐的解决方法
选择工程的 Target -> Build Settings 菜单，找到”User Header Search Paths”设置项
新增一个值"$(PODS_ROOT)"，并且选择”recursive”，这样xcode就会在项目目录中递归搜索文件

### CocoaPods安装教程(需要把淘宝网址改为 https ，其他不变)

### [http://www.bubuko.com/infodetail-425274.html ](http://www.bubuko.com/infodetail-425274.html)


## 系统默认的字体为：
```
font-family: ".SFUIText-Regular";
font-weight: normal;
font-style: normal;
font-size: 17.00pt
```

## 屏蔽的方法如下:
Xcode8里边 Edit Scheme-> Run -> Arguments, 在Environment Variables里边添加
```OS_ACTIVITY_MODE ＝ Disable```

![apple-phone-head.jpg](https://i.loli.net/2019/11/28/1B8LlwjkaIP6fvs.jpg)

# 关于代码：

## 代码延时调用

```
[self performSelector:@selector(aaa) withObject:nil afterDelay:2];

// 或者

dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(second * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
        [self dismiss];
});

```


## 根据格式化标签获取时间
### [unix 时间戳转换网站 ](https://tool.lu/timestamp/)
 
```
// Unix 时间戳1574870400000 = 北京时间：2019-11-28 00:00:00
NSString * unixTime = @"1574870400000";//模拟获得Unix时间戳,注意iOS只可处理10位的时间戳,而Android往往是13位。
NSTimeInterval interval = [[unixTime substringToIndex:10] doubleValue];//iOS只能取前10位

NSDate * date = [NSDate dateWithTimeIntervalSince1970:interval];
NSDateFormatter *format = [[NSDateFormatter alloc] init];
[format setDateFormat:@"yyyy年MM月dd日 HH:mm:ss"];
NSString *timeBeijing = [format stringFromDate:date];
```

## 输出沙盒路径
```
NSLog(@"***%@",NSHomeDirectory());

```

## 设置电量栏格式（白色字体）
```
application.statusBarStyle = UIStatusBarStyleLightContent;

<key>UIViewControllerBasedStatusBarAppearance</key>
    <false/>

```

## TextField 注册监听事件
```
[[UITextField alloc init] addTarget:self action:@selector(textChange:) forControlEvents:UIControlEventEditingChanged];
```

## 生成某个字符串的大小（自动调节）
```
CGSize textSize = [text sizeWithAttributes:@{ NSFontAttributeName : [UIFont systemFontOfSize: textFont ] }]; //此方法只是粗略计算

```
## UIView中的坐标转换
```
- (CGPoint)convertPoint:(CGPoint)point toView:(UIView *)view;
- (CGPoint)convertPoint:(CGPoint)point fromView:(UIView *)view;
- (CGRect) convertRect:(CGRect)  rect toView:(UIView *)  view;
- (CGRect) convertRect:(CGRect)  rect fromView:(UIView *)  view;
```
### Spring 动画
```
+ (void)animateWithDuration:(NSTimeInterval)duration delay:(NSTimeInterval)delay usingSpringWithDamping:(CGFloat)dampingRatio initialSpringVelocity:(CGFloat)velocity options:(UIViewAnimationOptions)options animations:(void (^)(void))animations completion:(void (^)(BOOL finished))completion

```
## 获取字符串前N位的字符（用于替代StringReplacing方法）
```
NSString * beforeStr = [_textView.text substringWithRange:NSMakeRange(0, 20)];
_textView.text = beforeStr;

```

## 用CAlayer代替 UIImageView
```
CALayer * imageLayer = [CALayer layer];
imageLayer.frame = CGRectMake(0, 64, 100, 100);
UIImage * image = [UIImage imageNamed:@""];
imageLayer.contents = (id)image;
imageLayer.backgroundColor = [UIColor magentaColor].CGColor;
[self.view.layer addSublayer:imageLayer];

```

## MJ Refresh 出现Too much   的解决方法：
### 选中项目 - Project - Build Settings-Apple LLVM 6.0-Preprocessing中的Enable Strict Checking of objc_msgsend calls 设置为 NO 即可


## TableView或CollectionView获取刷新完成状态
```
[tableView performBatchUpdates:^{ } ];

```

## TableViewCell 的样式和颜色
```
cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator; //右箭头图标

TableViewCell选中状态颜色设置
cell.selectionStyle = UITableViewCellSelectionStyleNone;  

自定义UITableViewCell选中时背景色：
cell.selectedBackgroundView = [[UIView alloc] initWithFrame:cell.frame];  
cell.selectedBackgroundView.backgroundColor = CustomColor;  

自定义UITableViewCell选中时背景
cell.selectedBackgroundView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@“image”]] ;  

Cell上字体颜色  
cell.textLabel.highlightedTextColor = HighLightedTextColor;
[cell.textLabel setTextColor: NomalColor] ;

设置tableViewCell间的分割线的颜色
[tableView setSeparatorColor:[UIColor xxxx ]]; 

```

## 自定义 Log 带错误所在函数
```
#ifdef DEBUG #define DDLOG(...) printf(" %s\n",[[NSString stringWithFormat:__VA_ARGS__]UTF8String]);
#define DDLOG_CURRENT_METHOD NSLog(@"%@-%@", NSStringFromClass([self class]), NSStringFromSelector(_cmd)) #else #define DDLOG(...) ; 
#define DDLOG_CURRENT_METHOD ; 
#endif
```

## 判断用户权限是否打开
```
//从相册选取
ALAuthorizationStatus author = [ALAssetsLibrary authorizationStatus];
if (author == ALAuthorizationStatusRestricted || author ==ALAuthorizationStatusDenied){
            NSLog(@"相册 未授权");
            MyAlertViewWenXin(@"请在iPhone的“设置-隐私-照片”中允许好实在访问您的照片");
        }else{
            NSLog(@"相册 已授权");
}

//使用相机拍摄        
NSString *mediaType = AVMediaTypeVideo;
AVAuthorizationStatus authStatus = [AVCaptureDevice authorizationStatusForMediaType:mediaType];
if(authStatus == AVAuthorizationStatusRestricted || authStatus == AVAuthorizationStatusDenied){
            NSLog(@"will 相机权限受限");
            MyAlertViewWenXin(@"请在iPhone的“设置-隐私-相机”中允许好实在访问您的相机");
        }else{
            NSLog(@"will 相机功能打开");
        }

//您的定位服务
if([CLLocationManager locationServicesEnabled] && [CLLocationManager authorizationStatus] != kCLAuthorizationStatusDenied) {
        NSLog(@"will 已开启");
    }else{
        NSLog(@"will 未开启");
        MyAlertViewWenXin(@"请在iPhone的“设置-隐私-定位服务”中允许好实在访问您的定位服务");
}
```














