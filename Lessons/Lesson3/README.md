<!-- Run this slideshow via the following command: -->
<!-- reveal-md README.md -w -->


<!-- .slide: class="header" -->

# Protocols and Delegates

## [Slides](https://make-school-courses.github.io/MOB-1.3-Dynamic-iOS-Apps/Slides/Lesson3/README.html ':ignore')

<!-- > -->

# Why you should know this

The delegate pattern is widely used in iOS development to communicate between objects. We've seen it before in `UITableViews` and `UICollectionViews`. If we understand how the delegate pattern works, we can implement our own to have more control over how our classes communicate.

<!-- > -->

## Learning Objectives

1. Construct and use protocols to define 'contracts' in code
1. Identify delegation in UIKit
1. Implement delegates in code

<!-- > -->

## Delegates

Meaning in the real world.

*To delegate* as a verb means to give control.<br>
*A delegate* as a noun means a person acting on behalf of another.

<!-- > -->

In software.

Delegation is a **design pattern** that enables a class or structure to hand off (or delegate) some of its responsibilities to an instance of another type.

In iOS development, delegation is used as a way for one class to **communicate** to another class. It'a a communication pattern.

The example that looks the most familiar to us is when using a tableview. The tableview by itself doesn’t know what information to show or the number of rows it needs to display. But they can find out by asking its dataSource.

A tableview’s dataSource must conform to the `UITableViewDatasouce` protocol, which has the right information needed to know what and how to display information.

<!-- > -->

# The Boss and the Intern 👩🏻‍💻

We'll represent the communication pattern using the following analogy.

Boss- Knows the bugs that need to be fixed, and knows how to do it.
Intern - Doesn't know anything and is just waiting for instructions from the senior dev.

The Boss will choose ticket to fix a bug and assign it to the Intern. Once they receive instructions, the Intern can act according to the task.

Download the [supporting files](https://github.com/amelinagzz/delegate-starter) for the example.

<!-- > -->

## BossVC

- Set up a protocol, the commands it gives to the Intern.

```swift
protocol TaskSelectionProtocol{
    func didSelectTask(task:String)
}
```

Here he have a list for command for the Intern, it could be one or more.

<!-- > -->

- Create a variable to hold the delegate.

```swift
var selectionDelegate: TaskSelectionProtocol!
```

<!-- > -->

- Tell the delegate(intern) what we want to do.

```swift
selectionDelegate.didSelectTask(task: "New Feature")
selectionDelegate.didSelectTask(task: "Bug Fix")
```

```swift
dismiss(animated: true, completion: nil)
```

<!-- > -->

## InternVC

- Assign the delegate

```swift
bossVC.selectionDelegate = self
```

Here the InternVC is telling the BossVC instance that it wants to be its intern, by assigning itself as the selectionDelegate.

<!-- > -->

- What to do after the Boss gives instructions

```swift
extension InternVC: TaskSelectionProtocol{
    func didSelectTask(task: String) {
        self.selectionLabel.text = "Working on \(task)"
    }
}
```

The Intern can proceed to work on the assigned task.

<!-- > -->

## Can we say it in a diagram?

Part 1 - individual<br>
Using the example of boss/intern or other if it's easier for you, create a diagram to remember how delegates work.<br>
Try to include the following key words: **delegate**, **delegator** and **delegate protocol**.

Add your own entry to [this Jamboard](https://jamboard.google.com/d/1F6mVerVYxf7AEYv8KReZKCgGMTBwmRc96qQkEz5lbXg/viewer).

Part 2 - Pairs<br>
Share and explain your diagram to a peer and compare both diagrams to see any similarities or differences<br>
**Discuss the table view scenario, who is the delegate and delegator? What is the protocol being used?**

<!-- > -->

## Creating our own delegate

Download the [starter files](https://github.com/amelinagzz/delegates-starter) to try after the explanation.

Scenario: We have an app with two view controllers. `FirstViewController` has a button that takes us to `SecondViewController`. There we have 3 views of different colors. The goal is that by selecting one of the views, the app will take us back to the first view controller and change the background color to the one selected previously.

We need a way of communication between both view controllers and pass information back from one to the other. Here's where delegates are useful.

Go ahead and implement the solution for the scenario using delegates.

<!--
The first part will take place in `SecondViewController`.

### Step 1: Adding the protocol
```Swift
protocol BackgroundColorDelegate{
    func colorSelected(color:UIColor)
}
```
### Step 2: Creating a delegate property
```Swift
var delegate: BackgroundColorDelegate?
```
### Step 3: Adding the delegate method call
```Swift
//Dismiss view controller and call method
self.delegate?.colorSelected(color: someColor)
```

Now we move to `FirstViewController`

### Step 4: Adopting the protocol
Include `BackgroundColorDelegate` in the class declaration.

### Step 5: Creating a reference of SecondViewController specifying the delegate
```Swift
let secondVC = segue.destination as! SecondViewController
            secondVC.delegate = self
```
### Step 6: Use the method of the protocol
```Swift
func colorSelected(color: UIColor) {
  // set background color
}
```

Running the program should work as expected now -->

<!-- > -->

## Completion Handlers

Remember closures and completion handlers? These can be used instead of delegates.

Download [this working example](https://github.com/dmlebron/tutorial_closures) and look at the code to find out how delegates are being replaced by closures and see how it leads to a similar result.<br>

In groups of 3 answer the following:

**Q:** What does the app do?<br>
**Q:** Where are closures being used?<br>
**Q:** How would the approach be with delegates? Change it.<br>

<!-- > -->

## Class Assignment

**Individually**

Change the implementation of the boss/intern to use a completion handler.<br>
If you are done early, practice doing the same for the 3 colors app.

<!-- > -->

## Lab recommendation

Start [Giphy Tutorial](https://www.makeschool.com/academy/track/giphy-search-for-ios-hrs).

<!-- > -->

## Additional Resources

1. [Example for delegates](https://medium.com/@jamesrochabrun/implementing-delegates-in-swift-step-by-step-d3211cbac3ef)
1. [Closures as delegates - article](https://medium.com/@dmlebron/using-swift-closures-as-an-alternative-to-delegates-5c3c1a7f45d6)
1. [Understanding delegates - article](https://www.appcoda.com/swift-delegate/)
1. [Delegates simple analogy - article](https://blog.bobthedeveloper.io/the-meaning-of-delegate-in-swift-347eaa9674d)
1. [More on Delegates](https://www.andrewcbancroft.com/2015/04/08/how-delegation-works-a-swift-developer-guide/)
1. [Intern/Boss analogy](https://www.youtube.com/watch?v=DBWu6TnhLeY)
