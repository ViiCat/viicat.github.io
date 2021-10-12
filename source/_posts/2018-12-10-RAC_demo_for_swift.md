---
layout: post
title: "RAC demo for Swift"
date: 2018-12-10 08:00:00 +0800
categories: [iOS, Swift, ReactiveCocoa]
---

此Demo用RAC展示简单的登录界面:

1、界面实现允许输入最多11位字符的用户名

2、当输入6位以上密码且11位字符达成条件后，登录按钮背景变成红色


<a href = "https://github.com/ViiCat/SSSwiftRAC">Demo 传送门</a>

### 效果
<img src="/images/racswift.gif" width="300">

### 上代码
LoginViewModel.swift

```
class LoginViewModel: NSObject {
    
    func binding(account: UITextField, password: UITextField, loginButton: UIButton) {
        
        // 信号
        let accountSignal  = account.reactive.continuousTextValues
        let passwordSignal = password.reactive.continuousTextValues
        
        
        // 用户名输入信号
        let accountMapSignal = accountSignal.map({ (value) -> Bool in
            
            // 字符串大于11位数 截取前11位
            if ((value!.characters.count) > 11) {
                
                let startIdx = value?.index((value!.startIndex), offsetBy: 0)
                let endIdx = value?.index(startIdx!, offsetBy:11)
                let result = value!.substring(with: startIdx!..<endIdx!)
                
                account.text = result
            }
            
            // 返回信号的值
            return  account.text!.characters.count == 11 ? true : false
        })
        
        
        // 密码输入信号
        let passwordMapSignal = passwordSignal.map({ (value) -> Bool in
            // 返回信号的值
            return value!.characters.count > 5 ? true : false
        })
        
        
        // 合并信号
        let bgColorSignl = Signal.combineLatest(accountMapSignal, passwordMapSignal).map { (arg) -> UIColor in
            
            let (value1, value2) = arg
            return value1 && value2 ? .red : .lightGray
        }
        
        let bgColor = Property(initial: .lightGray, then: bgColorSignl)
        
        // 绑定
        loginButton.reactive.backgroundColor <~ bgColor
        
    }
}
```

LoginViewController.swift

```
import UIKit

class LoginViewController: UIViewController {

    @IBOutlet weak var txtAccount: UITextField!
    
    @IBOutlet weak var txtPwd: UITextField!
    
    @IBOutlet weak var btnLogin: UIButton!
    
    override func viewDidLoad() {
        super.viewDidLoad()

        // Do any additional setup after loading the view.
        let viewModel = LoginViewModel()
        viewModel.binding(account: txtAccount, password: txtPwd, loginButton: btnLogin)

    }
}
```
