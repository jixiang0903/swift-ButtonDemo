# swift-ButtonDemo

//        UIButtonType.system：前面不带图标，默认文字颜色为蓝色，有触摸时的高亮效果
//        UIButtonType.custom：定制按钮，前面不带图标，默认文字颜色为白色，无触摸时的高亮效果
//        UIButtonType.contactAdd：前面带“+”图标按钮，默认文字颜色为蓝色，有触摸时的高亮效果
//        UIButtonType.detailDisclosure：前面带“!”图标按钮，默认文字颜色为蓝色，有触摸时的高亮效果
//        UIButtonType.infoDark：为感叹号“!”圆形按钮
//        UIButtonType.infoLight：为感叹号“!”圆形按钮
        
        //创建一个ContactAdd类型的按钮
        let addBtn:UIButton = UIButton(type:.custom)
        //设置按钮位置和大小
        addBtn.frame = CGRect(x:10, y:50, width:150, height:50)
        //设置按钮文字
        addBtn.setTitle("按钮", for: .normal)
        self.view .addSubview(addBtn)
        
        //圆角
        addBtn.layer.cornerRadius = 10
        addBtn.layer.masksToBounds = true
        
        //对于Custom定制类型按钮，代码可简化为：
        //let addBtn = UIButton(frame:CGRect(x:10, y:50, width:100, height:30))
        
        //按钮的文字设置
        addBtn.setTitle("普通状态", for: .normal)//普通状态下文字
        addBtn.setTitle("点击状态", for: .highlighted)//触摸状态下
        addBtn.setTitle("禁用状态", for: .disabled)//禁用状态
//        addBtn.isEnabled = false
        
        //按钮文字颜色的设置
        addBtn.setTitleColor(UIColor.black, for: .normal)//普通状态下文字颜色
        addBtn.setTitleColor(UIColor.green, for: .highlighted)//触摸状态下文字的颜色
        addBtn.setTitleColor(UIColor.red, for: .disabled)////禁用状态下文字的颜色
        
        //按钮文字阴影颜色的设置
        addBtn.setTitleShadowColor(UIColor.green, for: .normal)//普通状态下文字阴影的颜色
        addBtn.setTitleShadowColor(UIColor.red, for: .highlighted)//触摸状态下文字阴影的颜色
        addBtn.setTitleShadowColor(UIColor.gray, for:.disabled) //禁用状态下文字阴影的颜色
        addBtn.titleLabel?.shadowOffset = CGSize(width: -1, height: 1)
        
        //按钮文字的字体和大小设置
        addBtn.titleLabel?.font = UIFont.systemFont(ofSize: 17)
        
        //按钮背景颜色设置
        //addBtn.backgroundColor = UIColor.cyan
        
        //按钮文字图标的设置
        //（1）默认情况下按钮会被渲染成单一颜色
        //addBtn.setImage(UIImage(named:"返回"), for: .normal)
        addBtn.adjustsImageWhenHighlighted = false//使触摸模式下按钮也不会变暗（半透明）
        addBtn.adjustsImageWhenDisabled = false//使禁用模式下按钮也不会变暗（半透明）
        
        //（2）也可以设置成保留图标原来的颜色
        //let iconimg = UIImage(named:"group@2x")?.withRenderingMode(.alwaysOriginal)
        //addBtn.setImage(iconimg, for: .normal)
        addBtn.adjustsImageWhenHighlighted = false //使触摸模式下按钮也不会变暗（半透明）
        addBtn.adjustsImageWhenDisabled = false //使禁用模式下按钮也不会变暗（半透明）
        
        //设置按钮背景图片
        addBtn.setBackgroundImage(UIImage(named:"group2@3x"), for: .normal)
        
        //按钮触摸点击事件响应
//        常用的触摸事件类型：
//        touchDown：单点触摸按下事件，点触屏幕
//        touchDownRepeat：多点触摸按下事件，点触计数大于1，按下第2、3或第4根手指的时候
//        touchDragInside：触摸在控件内拖动时
//        touchDragOutside：触摸在控件外拖动时
//        touchDragEnter：触摸从控件之外拖动到内部时
//        touchDragExit：触摸从控件内部拖动到外部时
//        touchUpInside：在控件之内触摸并抬起事件
//        touchUpOutside：在控件之外触摸抬起事件
//        touchCancel：触摸取消事件，即一次触摸因为放上太多手指而被取消，或者电话打断
        //不传递触摸对象（即点击的按钮）
        addBtn.addTarget(self, action:#selector(tapped), for:.touchUpInside)

        //传递触摸对象（即点击的按钮），需要在定义action参数时，方法名称后面带上冒号
        //addBtn.addTarget(self, action:#selector(tapped(_:)), for:.touchUpInside)
        
        //按钮文字太长时的处理方法
        //默认情况下，如果按钮文字太长超过按钮尺寸，则会省略中间的文字,比如下面代码：
        let button1 = UIButton(frame:CGRect(x:20, y:150, width:130, height:50))
        button1.setTitle("这个是一段 very 长的文字", for: .normal)
        button1.setTitleColor(UIColor.white, for: .normal)
        button1.backgroundColor = UIColor.orange
        self.view.addSubview(button1)
        //我们通过修改 button 按钮中 titleLabel 的 lineBreakMode 属性，便可以调整按钮在文字超长的情况下如何显示，以及是否换行。
        //省略尾部文字
        button1.titleLabel?.lineBreakMode = .byWordWrapping
        //.byTruncatingHead：省略头部文字，省略部分用...代替
        //.byTruncatingMiddle：省略中间部分文字，省略部分用...代替（默认）
        //.byTruncatingTail：省略尾部文字，省略部分用...代替
        //.byClipping：直接将多余的部分截断
        //.byWordWrapping：自动换行（按词拆分）
        //.byCharWrapping：自动换行（按字符拆分）
        
        //注意：当设置自动换行后（byWordWrapping 或 byCharWrapping），我们可以在设置 title 时通过 \n 进行手动换行。
        
        button1.setTitle("欢迎访问\nhangge.com", for: .normal)  
    }
    func tapped(){
        print("tapped")
    }
    
//    func tapped(_ button:UIButton){
//        print("133424254")
//    }
    
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
}





![](https://github.com/jixiang0903/swift-ButtonDemo/blob/master/WechatIMG60.jpeg)
