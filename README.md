Practice 3: Navigation and Testing

Welcome to project three! In this project, we will be learning the navigation tools used in Purdue HCR as well as how to make some automated tests for the app. We will make a simple app with a bottom tab bar that will let you add an event, show a list of events, and show list of restaurants that you input.
![Figure1.1.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.1.png)

Figure 1.1: Let’s start by creating a new Single View App project in Xcode. After you make it, go to the Main.storyboard file and add a tab bar controller.

![Figure1.2.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.2.png)

Figure 1.2: This shows what the storyboard looks like after you add the tab bar controller. Now go ahead and delete the old view controller and set the tab bar controller as the initial view.

![Figure1.3.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.3.png)

Figure 1.3: Next, add 3 storyboard references to the Main storyboard and connect them with a Control-drag to the tab bar controller and give them the relationship segue of ‘view controllers’. This should result in a bottom bar appearing on the view with arrows pointing to the storyboard references. What this does is tells the app that each of those tab buttons is going to point to a View controller that is located in a different file.

![Figure1.4.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.4.png)

Figure 1.4: Next, for organizations sake, add three new groups(folders) to the file view on the left. Notice that these are named Restaurants, List Events, and Add New Events. In each of these folders, right click, add a new storyboard file. Then give the new storyboard files a name. In the example, they are named <FolderName>Storyboard.storyboard. All of our UI elements for the page will go into the respective Storyboard.

![Figure1.5.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.5.png)

Figure 1.5: Next, go back to Main.storyboard and click on the Storyboard references, open the right menu, and choose the correct storyboard from the drop down that matches the names. Make sure you do that for all three of them. This tells XCode which Storybaord these references actually point to. A quick note about how we do this in PurdueHCR: instead of building these connections with a storyboard, we actually do that in the code. If you look at this file, you can see how we do it programatically.
https://github.com/Decoder22/PurdueHCR-iOS/blob/master/PurdueHCR/ViewControllers/FlowControllers/TabBarController.swift

![Figure1.6.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.6.png)

Figure 1.6: Now, in each of your new storyboard files, add a View Controller, set it as the initial View Controller, add a label to it, then add a tab bar item. Make sure you give that tab bar a label and an image. If you want to be lazy, like I was here, you can change the 'System Item' option to one of Apple's presets.

![Figure1.7.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.7.png)

Figure 1.7: Now when you click run, this is what you should see. Each tab button relates to a different view. Some possible pitfalls at this step are:
1. Did you set an initial View Controllers in each storyboard? You can tell by looking to see if there is an arrow pointing into one of the view controllers.
2. Did you name your storyboard references in Main.storyboard properly? Is there a segue (arrow) pointing from the tab bar controller to each of the storyboard references? Do they have the relationship as 'view controllers'?

![Figure1.8.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.8.png) 

Figure 1.8 shows some simple views on the tab bar that were created for this project. For my example, the leftmost View controller will list your events with an image. You should have covered how to make Tableviews and Tableview cells in a previous tutorial, so go back and look there for the instructions. The middle tab is an add event tab. It contains a picture view and a text field. The example uses Apple's UIImagePickerController. You do not need to implement that if you do not want to. The Third tab options combines the display and creation of restaurants to one Storyboard. Feel free to make whatever you want on these three tabs.


One question that may arise from this example is: “How do I take the data from the add event page and put it onto the list events page?” That is a good question. On the page to the right, it is easy, because you can just pass the information back to the Tableview after you add a restaurant. But how do you move information across two tabs? Well, the way that PurdueHCR handles it is with the design pattern called a Singleton.

We can always go into the discussion about whether or not this is the best design pattern for this project, but for now lets just show you how it works.

 
![Figure1.9.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.9.png)

Figure 1.9 shows what the code for the shared instance looks like. We make a new file named DataManager.swift and create a class called DataManager. If you look at line 13, you will see some keywords that you may not know like static. Static is the keyword that makes all this work. What static means is that the variable known as sharedInstance may be accessed from anywhere in our program and is the EXACT SAME THING no matter where you call it. 
'DataManager.sharedInstance.events'
Will return you the exact same thing everywhere. So in your ViewController for adding an event, when they hit the add event button, you have this code:

![Figure1.10.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.10.png)

Figure 1.10 will take the text from the field as well as the image from the picture, bundle it into an Event object, and add it to the list of events in the sharedInstance. Now in your list events tableview, put this code:
 
![Figure1.11.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.11.png)

Line 13 creates a variable called events that contains the list of events from the DataManager. Then the method at line 25 says that everytime that the view is going to appear, go back and refresh the list of events from the database and reload the tableview to refresh the information.

You may wonder why we need to make a SharedInstance for something so trivial as sharing information between two tabs, and in this instance, your curiosity would be correct. But once you start diving into the networking code in the next project, you will see why having a shared data class will make it much easier to talk to the database.

Now hopefully you understand a little more about how to do the navigation options in iOS as well as getting a peak into how we will handle data in our apps. Now however, comes the fun part of programming. Testing your implementation.

Part 2 Testing

How do you know when a project works? Is it when you try to do something and the project does what you expect? What happens, though, if you put in something that the code is not prepared to handle? How do you make sure that your code is protected from misuse? The best way to do that is with testing.

As a part of Agile, Scrum, and SAFE, testing your system is critical to knowing when you have completed your User Stories. As you develop for PurdueHCR, we are going to require that you have tested your code and that it works to the specification you have. 

In the old days, the simplest way to do testing was by hand. Each time you made a change, you would have a document with test cases that you would manually check by actually putting that information into the app and doing a visual check. Luckily, Apple has made testing our code really easy, and even allows us to automate the testing! Watch this video to see how quick and painless it is to write UI tests for iOS!

https://www.youtube.com/watch?v=TsAxeBARuMU

For this tab bar project, we would like you to make 3 UI tests. Some examples include:
•	Does the test work with normal input
•	What happens if they leave the input fields empty.
•	They put too many characters into an input field

