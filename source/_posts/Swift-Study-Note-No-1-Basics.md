title: Swift Study Note No.1 - Basics
date: 2015-10-07 12:08:03
tags: swift
---

Just like [Cheng Zhao](http://cheng.guru/blog/2015/09/14/autoit.html) said, quote:

"其实网上的大部分的教程都非高手写成，而是新手在学习过程中的总结。有大量原创入门教程的知名博客，并不意味着博主是一个绝世高手，而是说明他是一个孜孜不倦的学习者。"

I am writing this as a study note for myself and if it could help you in any way, I am glad.

This note will be structured similar to the Lynda online course Swift Programming Language First Look with Simon Allardice.

### Introduction
Swift is a new language. I am not going to say more about its history or differences between Swift and other languages. Please Google. Or hey Siri.
### Using Xcode
As a swiftly (ha...) updating language, Swift changes a lot (I guess) since its publication. You should always use the updated Xcode for programming. (Please ignore my naive advice if you are coding for production.)
### Core Syntax
#### The structure of Swift
Go and find out yourself.
#### Writing Swift in playgrounds
Try it, please.
#### Declaring variables
```
var myVariable = 1
```
#### Creating constants
```
let myVariable = "this lable"
```
#### Printing values
```
print myVarialbe
```
#### Writing if statements
```
if score > 50 {
	some codes
} else {
	some other codes
}
```
#### Using the switch statement
```
let vegetable = "apple"

switch vegetable {
case "apple":
	let comment = "Good."
case "pine":
	let comment = "OK."
default:
	let comment = "whats that?"
}
```
#### Creating loops in Swift
```
for score in scores {
	some codes
}
```
#### Defining functions
```
func funcName (name : String) {
	some codes
}
```
#### Creating and using arrays
```
var list = ["a","b"]
```
#### Using dictionaries
```
var member : [String : String] = ["Wang":"Shanghai", "Xia":"Guangzhou"]
```
#### Understanding tuples
```
(Int, Int)
```
#### Creating optional variables
```
(Int, Int)?
(Int?,Int?)
# Please note that they are different.
```
#### Defining and using enumerations
```
enum CompassPoint {
	case North
	case South
	case East
	case West
}
```
#### Writing closures
```
{
some lines of code
}
```
#### Creating classes and instantiating objects
```
class videoMode {
	var resolution = Resolution()
	var interlaced = false
	var frameRate = 0.0
	var name: String?
}

struct Resolution {
	var width = 0
	var height = 0
}
```
### Conclusion
Thats it. Please correct me if any.