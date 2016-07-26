# XTAnimations
About the collection of various forms of animation

#### YY直播点赞效果
![](http://ww4.sinaimg.cn/large/e6a4355cgw1f5ttdqlqrvg208w0h2x6s.gif)
```objectivec
XTLoveHeartView *heart = [[XTLoveHeartView alloc]initWithFrame:CGRectMake(0, 0, 40, 40)];
[self.view addSubview:heart];
CGPoint fountainSource = CGPointMake(self.view.frame.size.width - 80, self.view.bounds.size.height - 30 / 2.0 - 10);
heart.center = fountainSource;
[heart animateInView:self.view];
```
#### 烟花演示效果
![](http://ww3.sinaimg.cn/large/e6a4355cgw1f5tll5lp8qg208w0gk7wk.gif)

#### SNOW
![](http://ww4.sinaimg.cn/large/e6a4355cgw1f61moqud49g208w0gp4qq.gif)

#### 跑马灯
![](http://ww4.sinaimg.cn/large/e6a4355cgw1f61mq3x60gg208w0gnkjl.gif)
```objectivec
- (void)viewDidLoad {
[super viewDidLoad];
// Do any additional setup after loading the view.
self.view.backgroundColor = [UIColor blackColor];

XTScrollLabelView *drawMarqueeView  = [[XTScrollLabelView alloc] initWithFrame:CGRectMake(0, 0, 250.f, 20)];
drawMarqueeView.delegate          = self;
drawMarqueeView.marqueeDirection  = FromLeftType;
drawMarqueeView.center            = self.view.center;
[self.view addSubview:drawMarqueeView];
[drawMarqueeView addContentView:[self createLabelWithText:@"夏天是个很好的季节, 而夏天然后是简书的推荐作者, 喜欢分享!"
textColor:[self randomColor]]];
[drawMarqueeView startAnimation];

}

- (UILabel *)createLabelWithText:(NSString *)text textColor:(UIColor *)textColor {

NSString *string = [NSString stringWithFormat:@" %@ ", text];
CGFloat width = [string widthWithStringAttribute:@{NSFontAttributeName : [UIFont systemFontOfSize:14.f]}];
UILabel  *label  = [[UILabel alloc] initWithFrame:CGRectMake(0, 0, width, 20)];
label.font       = [UIFont systemFontOfSize:14.f];
label.text       = string;
label.textColor  = textColor;

return label;
}
- (UIColor *)randomColor {

return [UIColor colorWithRed:[self randomValue] green:[self randomValue] blue:[self randomValue] alpha:1];
}
- (CGFloat)randomValue {

return arc4random() % 256 / 255.f;
}
- (void)drawMarqueeView:(XTScrollLabelView *)drawMarqueeView animationDidStopFinished:(BOOL)finished
{
[drawMarqueeView stopAnimation];
dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(1.0 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
[drawMarqueeView addContentView:[self createLabelWithText:[self randomString]
textColor:[self randomColor]]];
[drawMarqueeView startAnimation];
});
}
- (NSString *)randomString {

NSArray *array = @[@"人帅",
@"勤劳",
@"年轻",
@"刻苦",
@"开玩笑",
@"都是我编的, 前面的别跑"];
return array[arc4random() % array.count];
}

```

