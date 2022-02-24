title: Embrace Cocoapods
date: 2016-01-10 15:35:02
tags: swift
---

Yes there are desperate times, maybe because things get worse before they get better.  Anyway, please use Cocoapods in your projects.

Install CocoaPods:
```
sudo gem install cocoapods
```
It would not work if you are in China, try:
```
gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
gem sources -l
```
Try install CocoaPods again:
```
sudo gem install cocoapods
```
Up and running, next setup the Pod:
```
pod setup
```
Navigate to the directory containing your project:
```
cd someDirectory
pod init
```
Open the Podfile using command (or edit it using any text editor):
```
open -a Xcode Podfile
```
Modify Podfile (just for example):
```
platform :ios, ‘8.0’
use_frameworks!
 
target 'AlamofireSwiftyJSONSample' do
    pod 'Alamofire'
    pod 'SwiftyJSON'
end
```
Save it and Go back to terminal (still at your project directory):
```
pod install
```
From now on you have to use the .xcworkspace of your project.  And before starting your work, remember to include these framework in the General, Linked Frameworks and Libraries.

You could find a better tutorial by googling.