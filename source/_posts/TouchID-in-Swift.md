title: TouchID in Swift
date: 2015-12-25 21:34:11
tags: swift
---

To use the TouchID in your app, first include LocalAuthentication.framework and then add some code. The reason for implementing dispatch_async is that it somehow speeds up the UI updating process.

```Swift
import UIKit
import LocalAuthentication

class ViewController: UIViewController {

    @IBOutlet weak var statusLabel: UILabel!
    
    @IBAction func authAction(sender: AnyObject) {
        authAction()
    }

    override func viewDidLoad() {
        super.viewDidLoad()
    }

    func authAction() {
        
        let laContext = LAContext()
        var authError : NSError?
        let authReason = "Unlock the app"
        
        if laContext.canEvaluatePolicy(LAPolicy.DeviceOwnerAuthenticationWithBiometrics, error: &authError) {
            laContext.evaluatePolicy(LAPolicy.DeviceOwnerAuthenticationWithBiometrics, localizedReason: authReason, reply: { (success, error) -> Void in
                if success {
                    dispatch_async(dispatch_get_main_queue(), { () -> Void in
                        self.successForLogin()
                    })
                } else {
                    dispatch_async(dispatch_get_main_queue(), { () -> Void in
                        self.failedForLogin()
                    })
                }
            })
        }
    }
    
    func successForLogin() {
        statusLabel.text = "Succeeded"
    }
    
    func failedForLogin() {
        statusLabel.text = "Failed"
    }

}
```
