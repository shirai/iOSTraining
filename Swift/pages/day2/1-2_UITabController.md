> 参考 [mixi-inc/iOSTraining 2.2 UITabController](https://github.com/mixi-inc/iOSTraining/wiki/2.2-UITabController)

[UITabBarController Class Reference](http://developer.apple.com/library/ios/#documentation/uikit/reference/UITabBarController_Class/Reference/Reference.html)

[iOS View Controllerプログラミングガイド](https://www.google.co.jp/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&ved=0CDMQFjAA&url=http%3A%2F%2Fdeveloper.apple.com%2Fjp%2Fdevcenter%2Fios%2Flibrary%2Fdocumentation%2FViewControllerPGforiPhoneOS.pdf&ei=UGlnUYi7K87ykAXXiYCQAQ&usg=AFQjCNGdaDn2IS1bJpHD08rsGEroiXr9RQ&sig2=qKCoJdJvpNipFuAD2NXfQw&bvm=bv.45107431,d.dGI)

# 概要

> ![tabController1](https://docs-assets.developer.apple.com/published/fb77ce00ad/tabbar_compare_db3ec478-a345-483f-9227-94ca1b78f604.jpg)
> [UITabBarController Class Reference](https://developer.apple.com/reference/uikit/uitabbarcontroller) から引用

UITabBarController は TabBar インタフェースを用いて ViewController を管理するコンテナです。

> ![tabController2](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/2.2/tabController2.png)

UITabBarController における重要な property と method は以下の通りです。

- viewControllers - viewController が含まれている NSArray
- selectedViewController - 現在表示されている ViewController を取得、別のViewControllerに変更可能なプロパティ
- delegate - 表示変更などのイベントを取得できる delegate
[UITabBarControllerDelegate Protocol](https://developer.apple.com/reference/uikit/uitabbarcontrollerdelegate)

tab の表示は ViewController の UITabBarItem を設定することで変更可能

# 実装
## プロジェクト作成
![createTabProject](./images/1_2/image1.png)

## moreViewControllers と tabBarItem
viewControllers に 5 つ以上の ViewController を管理させる場合、Tab では 4 つを管理し、それ以外の ViewController は more として管理されます。

> ![tabBarItem](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/2.2/tabBarItem.png)


FirstViewController.swift
```swift
init(imageName: String) {
    super.init(nibName: "FirstViewController", bundle: nil)
    title = imageName
    tabBarItem?.image = UIImage(named: imageName)
}
```

`init(nibName:bundle:)`を呼ぶためには、`FirstViewController.xib`が必要になります。

AppDelegate.swift
```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    // Override point for customization after application launch.
    if let tabBarContorller = window?.rootViewController as? UITabBarController {
        let viewControllers: [UIViewController] = [
            FirstViewController(imageName: "first"),
            FirstViewController(imageName: "second"),
            FirstViewController(imageName: "third"),
            FirstViewController(imageName: "fourth"),
            FirstViewController(imageName: "fifth"),
            FirstViewController(imageName: "sixth")
        ]
        tabBarContorller.viewControllers = viewControllers
    }
    return true
}
```

画像ファイルは[こちら](./images/day2/1_2/icons)

## tab のバッジ
> ![tabBadge](https://raw.github.com/mixi-inc/iOSTraining/master/Doc/Images/2.2/tabBadge.png)

tabBar の上にバッジを表示することが可能です。

```swift
tabBarItem.badgeValue = "5"
```

# Storyboardを用いた方法
Storyboardを用いることで、視覚的にTabBarControllerとその中に入るViewControllerをデザインすることができます。
iOS→Appを選択してNextをクリックし、開発画面のMain.storyboardからtabBarController作成します。

![img](./images/1_2/image1.png)

Main.storyboardに移動したら、iPhone画面をクリックして、Xcodeと書かれている上記メニュー欄の『Editor』をクリックします。『Editor』を選択後は、『Embed In』➡︎『Tab Bar Controller』をクリックしてください。

![img](./images/1_2/image2.png)

これで『Tab Bar Controller』画面が表示されました。
![img](./images/1_2/image3.png)

新しくViewControllerを追加する際は、ViewControllerをstoryboard上に追加し、Tab Bar Controller から controlを押しながらViewControllerへドラッグします

![img](./images/1_2/image4.png)

その後、segueは "view controllers" を選択します。

![img](./images/1_2/image5.png)

このように追加したViewControllerにSegueが追加されていれば完了です。

![img](./images/1_2/image6.png)


# 演習
* storyboard上のTabBarControllerに対して、新しくViewController（ThirdViewController）を追加してください。
* xibからロードしたViewContorller（FourthViewController）を更に追加してください。

解答は [after/day2/1.2/TabSample](../../after/day2/1.2/TabSample) をごらんください
