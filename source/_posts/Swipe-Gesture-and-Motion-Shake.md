title: Swipe Gesture and Motion Shake
date: 2015-12-12 21:08:11
tags: swift
---

Define an UISwipeGestureRecognizer:

```
override func viewDidLoad() {
    super.viewDidLoad()
    var swipeRight = UISwipeGestureRecognizer(target: self, action: "swiped:")
    swipeRight.direction = UISwipeGestureRecognizerDirection.Right
    self.view.addGestureRecognizer(swipeRight)
}
```

Detailed actions are in the func:
```
func swiped(gesture: UISwipeGestureRecognizer) {  
    if let swipeGesture = gesture as? UISwipeGestureRecognizer {
        switch swipeGesture.direction {   
             case UISwipeGestureRecognizerDirection.Right: 
                 print("right")
             default:
                 break
        }    
    }
}
```

To deal with the motion shake of iPhone:
```
override func motionEnded(motion: UIEventSubtype, withEvent event: UIEvent?) {
    if event?.subtype == UIEventSubtype.MotionShake {
        print("The phone has been shaken.”)
    }
}
```