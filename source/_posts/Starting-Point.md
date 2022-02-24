title: Starting Point
date: 2015-11-21 21:09:27
tags: swift
---

The tutorial recently published by Apple is called Start Developing iOS Apps (Swift).  [Link](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/DevelopiOSAppsSwift/RevisionHistory.html)

![](/img/startSwift.png)

Just a tip about this tutorial, I found the UI odd on iPhone 5s.  Maybe Apple presumes you should have iPhone 6 at least by now.

To give you a glance of what this project looks like, I show you MealTableViewController.swift as follows.

```
import UIKit

class MealTableViewController: UITableViewController {
    // MARK: Properties
    
    var meals = [Meal]()

    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Use the edit button item provided by the table view controller.
        navigationItem.leftBarButtonItem = editButtonItem()
        
        // Load any saved meals, otherwise load sample data.
        if let savedMeals = loadMeals() {
            meals += savedMeals
        } else {
            // Load the sample data.
            loadSampleMeals()
        }
    }
    
    func loadSampleMeals() {
        let photo1 = UIImage(named: "meal1")!
        let meal1 = Meal(name: "Caprese Salad", photo: photo1, rating: 4)!
        
        let photo2 = UIImage(named: "meal2")!
        let meal2 = Meal(name: "Chicken and Potatoes", photo: photo2, rating: 5)!
        
        let photo3 = UIImage(named: "meal3")!
        let meal3 = Meal(name: "Pasta with Meatballs", photo: photo3, rating: 3)!
        
        meals += [meal1, meal2, meal3]
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }

    // MARK: - Table view data source

    override func numberOfSectionsInTableView(tableView: UITableView) -> Int {
        return 1
    }

    override func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return meals.count
    }

    override func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
        // Table view cells are reused and should be dequeued using a cell identifier.
        let cellIdentifier = "MealTableViewCell"
        let cell = tableView.dequeueReusableCellWithIdentifier(cellIdentifier, forIndexPath: indexPath) as! MealTableViewCell
        
        // Fetches the appropriate meal for the data source layout.
        let meal = meals[indexPath.row]
        
        cell.nameLabel.text = meal.name
        cell.photoImageView.image = meal.photo
        cell.ratingControl.rating = meal.rating
        
        return cell
    }

    // Override to support conditional editing of the table view.
    override func tableView(tableView: UITableView, canEditRowAtIndexPath indexPath: NSIndexPath) -> Bool {
        // Return false if you do not want the specified item to be editable.
        return true
    }
    

    // Override to support editing the table view.
    override func tableView(tableView: UITableView, commitEditingStyle editingStyle: UITableViewCellEditingStyle, forRowAtIndexPath indexPath: NSIndexPath) {
        if editingStyle == .Delete {
            // Delete the row from the data source
            meals.removeAtIndex(indexPath.row)
            saveMeals()
            tableView.deleteRowsAtIndexPaths([indexPath], withRowAnimation: .Fade)
        } else if editingStyle == .Insert {
            // Create a new instance of the appropriate class, insert it into the array, and add a new row to the table view
        }    
    }


    /*
    // Override to support rearranging the table view.
    override func tableView(tableView: UITableView, moveRowAtIndexPath fromIndexPath: NSIndexPath, toIndexPath: NSIndexPath) {

    }
    */

    /*
    // Override to support conditional rearranging of the table view.
    override func tableView(tableView: UITableView, canMoveRowAtIndexPath indexPath: NSIndexPath) -> Bool {
        // Return false if you do not want the item to be re-orderable.
        return true
    }
    */

    
    // MARK: - Navigation

    // In a storyboard-based application, you will often want to do a little preparation before navigation
    override func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject?) {
        if segue.identifier == "ShowDetail" {
            let mealDetailViewController = segue.destinationViewController as! MealViewController
            
            // Get the cell that generated this segue.
            if let selectedMealCell = sender as? MealTableViewCell {
                let indexPath = tableView.indexPathForCell(selectedMealCell)!
                let selectedMeal = meals[indexPath.row]
                mealDetailViewController.meal = selectedMeal
            }
        }
        else if segue.identifier == "AddItem" {
            print("Adding new meal.")
        }
    }
    

    @IBAction func unwindToMealList(sender: UIStoryboardSegue) {
        if let sourceViewController = sender.sourceViewController as? MealViewController, meal = sourceViewController.meal {
            if let selectedIndexPath = tableView.indexPathForSelectedRow {
                // Update an existing meal.
                meals[selectedIndexPath.row] = meal
                tableView.reloadRowsAtIndexPaths([selectedIndexPath], withRowAnimation: .None)
            } else {
                // Add a new meal.
                let newIndexPath = NSIndexPath(forRow: meals.count, inSection: 0)
                meals.append(meal)
                tableView.insertRowsAtIndexPaths([newIndexPath], withRowAnimation: .Bottom)
            }
            // Save the meals.
            saveMeals()
        }
    }
    
    // MARK: NSCoding
    
    func saveMeals() {
        let isSuccessfulSave = NSKeyedArchiver.archiveRootObject(meals, toFile: Meal.ArchiveURL.path!)
        if !isSuccessfulSave {
            print("Failed to save meals...")
        }
    }
    
    func loadMeals() -> [Meal]? {
        return NSKeyedUnarchiver.unarchiveObjectWithFile(Meal.ArchiveURL.path!) as? [Meal]
    }
}
```

Generally speaking, this tutorial by Apple of 21 Oct 2015 is the best learning material so far in the market for beginners of iOS development.  You have to check it out and learn all that piece by piece.  At current moment it is most up-to-date and of course compatible with Swift 2.1.  I spent last whole week on this and finally pull it off at this Saturday.  Not because it is difficult, but simply I just dont have that amount of time to walk all the way through.  It is sad when you have to focus your daily job on something you just dont enjoy.  Hopefully the experience I gain would be useful eventually at some point of time, if you ask for comfort.

Another thing quite helpful is iOS and Swift Terminology.  For the terms you will encounter, I paste the Glossary as below for easy reference.

```
action
A piece of code that’s linked to an event that can occur in your app.

activity viewer
Part of the Xcode toolbar that displays messages about the build process and other information.

adaptive interface
A UI that automatically adjusts so that it looks good in the context of the available screen space.

adopt
To indicate that a class, structure, or enumeration conforms to a protocol.

application programming interface (API)
A set of functions, classes, protocols, and other components that define how pieces of software should interact with each other.

app delegate
An object in your app (specifically, an instance of the AppDelegate class) that creates the window where your app’s content is drawn and that provides a place to respond to state transitions within the app.

application object
An object in your app that’s responsible for managing the life cycle of the app, communicating with its delegate, the app delegate, during state transitions within the app.

argument
A value you pass in to a function, method, or initializer to satisfy one of its parameters.

array
A data type that stores multiple values of the same type in an ordered list.

Attributes inspector
An inspector that you use to customize visual attributes of a UI element in a storyboard.

asset catalog
A tool to manage assets like images that are used by your app as part of its UI.

assistant editor
In Xcode, a secondary editor window that appears side-by-side with your primary editor.

Auto Layout
A layout engine that helps lay out your UI based on the constraints you specify.

base class
A class that’s at the root of its class hierarchy, meaning that it has no superclass.

canvas
The background of a storyboard where you add and arrange UI elements.

class
A piece of code that describes the behavior and properties common to any particular type of object, essentially providing a blueprint for the object.

class hierarchy
A hierarchical representation of a class’s relationships to its superclass and subclasses.

closed range operator
An operator (...) that lets you create a range of numbers that includes both the lower and upper values.

Cocoa Touch
The set of Apple frameworks and technologies used to develop iOS apps.

code completion
A feature of Xcode that infers what you’re trying to type from context and provides suggestions that you can select.

completion handler
A closure that’s passed as a parameter to a method that calls the closure when it finishes executing.

comment
A piece of text in a source code file that doesn’t get compiled as part of the program but provides context or other useful information about individual pieces of code.

conditional statement
A control flow statement that checks whether a condition is true before executing a piece of code.

conform to
For a class, structure, or enumeration to satisfy the requirements of a protocol.

console
A tool for debugging and for logging information for debugging purposes.

constant
A value that’s initialized once and cannot change, indicated in Swift by the let keyword.

constraint
In Auto Layout, a rule that explains where one element should be located relative to another, what size it should be, or which of two elements should shrink first when something reduces the space available for each of them.

content view
A view object that’s located at the top of a view hierarchy, serving as a container for the subviews in its hierarchy.

control
A specialized type of view (specifically, an instance of the UIControl class or one of its subclasses) that responds to user input.

convenience initializer
A secondary initializer, which adds additional behavior or customization, but must eventually call through to a designated initializer.

data model
The representation or structure of data within an app.

data source
An object that manages the app’s data model, providing a view object with the information it needs to display that data.

delegate
An object that acts on behalf of, or in coordination with, another object.

designated initializer
One of the primary initializers for a class; a convenience initializer within a class must ultimately call through to a designated initializer.

destination view controller
The view controller whose contents are displayed at the end of a segue.

downcast
To attempt to cast an object to one of its subclass types.

entry point
Where control enters a program or piece of code.

enumeration
A data type that defines a group of related values and enables you to work with those values in a type-safe way within your code.

event-driven programming
A category of programming in which the flow of the app is determined by events: system events and user actions.

extension
A capability to add functionality to an existing type.

failable initializer
An initializer that could return nil after initialization.

first responder
An object that is first to receive many kinds of app events, including key events, motion events, and action messages, among others.

fix-it
A suggested fix for a compiler error in Xcode.

forced type cast operator
An operator (as!) that attempts a downcast and force-unwraps the result.

force-unwrap operator
An operator (!) placed after an optional value to access its underlying value.

function
A reusable, named piece of code that can be referred to from many places in a program.

functions menu
In Xcode, a jump menu that lets you navigate directly to a specific declaration or section in a source code file.

gesture recognizer
An object that you attach to a view that allows the view to respond to actions the way a control does.

global
A constant, variable, or function defined at the top-level scope of a program.

half-open range operator
An operator (..<) that lets you create a range of numbers that includes the lower but not the upper value.

Identity inspector
An inspector that you use to edit properties of an object in a storyboard related to that object’s identity, such as what class the object belongs to.

identity operator
An operator (===) that tests whether two object references both refer to the same object instance.

immutable
A value that cannot be changed (or mutated) after it’s initialized, like a constant.

implement
To define the behavior of something in code.

implicitly unwrapped optional
An optional that can also be used like a nonoptional value, without the need to unwrap the optional value each time it is accessed, because it’s assumed to always have a value after that value is initially set.

inheritance
When a class is a subclass of another class, it gets all of its behavior (methods, properties, and other characteristics) from its superclass.

initializer
A method that handles the process of preparing an instance of a class, structure, or enumeration for use, which involves setting an initial value for its properties and performing any other required setup.

inspector pane
An area in Xcode that displays inspectors, such as the Attributes inspector, Identity inspector, and Size inspector.

instance
A specific occurrence of a class (that is, an object), structure, or enumeration.

integrated development environment (IDE)
A software application that provides a set of tools for software development.

Interface Builder
The graphical environment for building a UI in Xcode.

intrinsic content size
The minimum size needed to display all the content in a view without clipping or distorting that content.

iterate
To perform repeatedly.

library pane
An area in Xcode that displays one of the ready-to-use libraries of resources for your project, like the Object library.

local
A constant or variable defined only within a particular, limited scope, like a loop, conditional statement, or function.

loop
A control flow statement that executes the same piece of code multiple times.

method
A reusable, named piece of code that’s associated with a particular class, structure, or enumeration.

modal segue
A segue in which one view controller presents another view controller as its child, requiring a user to perform an operation on the presented controller before returning to the main flow of the app.

Model-View-Controller (MVC)
A pattern of app design in which view controllers serve as the communication pipeline between views and the data model.

mutable
A value that is able to be changed (or mutated) after it’s initialized, like a variable.

navigation controller
A specialized view controller subclass that manages transitions backward and forward through a series of view controllers.

navigation stack
The set of view controllers managed by a particular navigation controller.

nil
The absence of a value or no value.

nil coalescing operator
An operator (??) placed between two values, a ?? b, that unwraps an optional a if it contains a value, or returns a default value b if a is nil.

object
An instance of a class.

Object library
Part of the Xcode workspace window that shows a list of objects that can be added to a storyboard, including each object’s name, description, and visual representation.

optional
A value that contains either an underlying value or nil to indicate that the value is missing.

optional binding
The process of attempting to assign an optional value to a constant in a conditional statement to see if the optional contains an underlying value.

optional type cast operator
An operator (as?) that attempts a downcast and returns the result as an optional value.

outlet
A reference to an object in a storyboard from a source code file.

outline view
A pane in a storyboard that lets you see a hierarchical representation of the objects in your storyboard.

override
To replace an implementation of a method defined on a superclass.

parameter
An additional piece of information that must be passed into a function, method, or initializer when it’s called.

playground
A type of file in which you can change and play around with Swift code directly in Xcode and see the immediate results.

project navigator
Part of the Xcode workspace window that displays all the files in your project.

property
A piece of data encapsulated within a class, structure, or enumeration.

property observer
A piece of code that’s called every time a property’s value is set that’s used to observe and respond to changes in the property’s value.

protocol
A blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality.

read-only
A value that can only be viewed (read) but never changed (written).

read-write
A value that can be both viewed (read) and changed (written).

resize handles
Small white squares that appear on a UI element’s borders when it’s selected so you can change its size on the canvas.

root view controller
The first item added to a navigation controller’s navigation stack, which is never popped off (removed from) the stack.

run loop
An event processing loop that you use to schedule work and coordinate the receipt of incoming events in your app.

runtime
The period during which a program is executing.

scene
A storyboard representation of a screen of content in your app.

scene dock
A bar that contains information related to a scene in a storyboard.

segue
A transition between two view controllers in a storyboard.

show segue
A segue that pushes new content on top of the current view controller stack.

Simulator
An app in Xcode that simulates the behavior and appearance of running an app on a device.

Size inspector
An inspector that you use to edit the size and position of a UI element in a storyboard.

source view controller
The view controller whose contents are displayed at the beginning of a segue.

storyboard
A file that contains a visual representation of the app’s UI (user interface), showing screens of content and the transitions between them, that you work on in Interface Builder.

storyboard entry point
The first scene that’s shown from a storyboard when an app starts.

string interpolation
The process of inserting string representations of constants, variables, literals, and expressions into longer strings.

structure
A data type that’s similar to a class, but doesn’t support inheritance and is passed by value instead of by reference.

subclass
A class that’s a child of another class (known as its superclass).

subview
A view that is enclosed by another view (known as its superview).

superclass
A class that’s a parent of another class (known as its subclass).

superview
A view that encloses another view (known as its subview).

Swift standard library
A set of data types and capabilities designed for Swift and baked into the language.

target
The object that receives the action message in the target-action pattern.

target-action
A design pattern in which one object sends a message to another object when a specific event occurs.

tuple
A grouping of values.

type casting
A way to check the type of an object, and to treat that object as if it’s a different superclass or subclass from somewhere else in its own class hierarchy.

type inference
The ability of the Swift compiler to determine the type of a value from context, without an explicit type declaration.

UIKit
A Cocoa Touch framework for working with the UI layer of an iOS app.

underscore
A representation of a wildcard in Swift (_).

unit test
A piece of code written specifically to test a small, self-contained piece of behavior in your app to make sure it behaves correctly.

unwrap
To extract an underlying value from an optional.

user interface (UI)
The layer of visual elements that lets a user interact with a piece of software.

utility area
An area in Xcode that displays the inspector pane and library pane.

unwind segue
A type of segue used to implement backward navigation.

variable
A value that can change after it’s been initialized, indicated in Swift by the var keyword.

view
An object that’s used to construct your UI and display content to the user.

view controller
An object that manages a set of views and coordinates the flow of information between the app’s data model and the views that display that data.

view hierarchy
A hierarchical representation of views relative to other views.

workspace window
The Xcode window, which you use to manage and navigate through the files and resources in your project.
```