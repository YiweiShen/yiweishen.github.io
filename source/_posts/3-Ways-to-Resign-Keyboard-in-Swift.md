title: 3 Ways to Resign Keyboard in Swift
date: 2015-12-03 19:07:11
tags: swift
---

For the apps that enable users to input something in a textfield, you should always keep an eye on the keyboard resign.  Here are 3 of the most common ways to accomplish this goal.

No.1 To resign the first responder position of the keyboard in the buttom action so that press this bottom would also cause keyboard dismiss:

```
self.someTextField.resignFirstResponder()
```

No.2 To override the touchesBegan function so that if users touch outside the keyboard, the keyboard closes down:
```
override func touchesBegan(touches: Set<UITouch>, withEvent event: UIEvent?) {
        self.view.endEditing(true)
}
```

No.3 To inherit UITextFieldDelegate for the current ViewController, then use textFieldShouldReturn function so that when users press return key of the keyboard, the keyboard resigns:
```
func textFieldShouldReturn(textField: UITextField) -> Bool {
        someTextField.resignFirstResponder()
        return true
}
```

Just a simple note for myself.