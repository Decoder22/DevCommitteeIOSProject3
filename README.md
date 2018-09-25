Practice 3: Navigation and Testing

Welcome to project three! In this project, we will be learning the navigation tools used in Purdue HCR as well as how to make some automated tests for the app. We will make a simple app with a bottom tab bar that will let you add an event, show a list of events, and show list of restaurants that you input.
![Figure1.1.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.1.png)
Figure 1.1: Let’s start by creating a new Single View App project in Xcode. After you make it, go to the Main.storyboard file and add a tab bar controller.

![Figure1.2.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.2.png)
Figure 1.2: This shows what the storyboard looks like after you add the tab bar controller. 

![Figure1.3.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.3.png)

Figure 1.3: Next, add 3 storyboard references to the Main storyboard and connect them with a Control-drag to the tab bar controller and give them the relationship segue of ‘view controllers’. This should result in a bottom bar appearing on the view with arrows pointing to the storyboard references.

![Figure1.4.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.4.png)

Figure 1.4: Next, for organizations sake, add three new groups to the file view on the left. Notice that these are names Restaurants, List Events, and Add New Events. In each of these folders, right click, add a new file, and select storyboard. Then give the new storyboard files a name. In the example, they are named <FolderName>Storyboard.storyboard. 

![Figure1.5.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.5.png)

Figure 1.5: Next, go back to Main.storyboard and click on the Storyboard references, open the right menu, and choose the storyboard from the drop down that matches the names.

![Figure1.6.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.6.png)
Figure 1.6: Now, in each of your new storyboard files, add a View Controller, set it as the initial View Controller, add a label to it, then add a tab bar item. That tab bar item will be what is shown on the bottom bar of the app. 

![Figure1.7.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.7.png)
Figure 1.7: Now when you click run, this is what you should see. Your tab bar may not have images, but that is ok. Click on the tab buttons and they should take you between the different View Controllers. You can do a quick change of the tab bar images by clicking on the tab bar item in its storyboard file and changing its ‘System Item’ property on the right bar.

![Figure1.8.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.8.png) 

Figure 1.8 shows some simple views on the tab bar that were created for this project. The left is an event list, the middle is a way to add an event, and the right is a list of restaurants with and add button. This is just an example, so you can do whatever you would like to do. 


One question that may arise from this example is: “How do I take the data from the add event page and put it onto the list events page?” That is a good question. On the page to the right, it is easy, because you can just pass the information back to the Tableview after you add a restaurant, but how do you move information across two tabs? Well, the way that PurdueHCR handles it is with a Shared Instance.

 
![Figure1.9.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.9.png)

Figure 1.9 shows what the code for the shared instance looks like. We make a new file named DataManager.swift and create a class called DataManager. If you look at line 13, you will see some keywords that you may not know like static. Static is the keyword that makes all this work. What static means is that the variable known as sharedInstance may be accessed from anywhere in our program and is the EXACT SAME THING no matter where you call it. 
DataManager.sharedInstance.events
Will return you the exact same thing everywhere. So in your ViewController for adding an event, when they hit the add event button, you have this code:
![Figure1.10.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.10.png)

This code will take the text from the field as well as the image from the picture, bundle it into an Event object, and add it to the list of events in the sharedInstance. Now in your list events tableview, put this code:
 
![Figure1.11.png](https://github.com/Decoder22/DevCommitteeIOSProject3/blob/master/readmePictures/Figure1.11.png)

Line 13 creates a variable called events that contains the list of events from the DataManager. Then the method at line 25 says that everytime that the view is going to appear, go back and refresh the list of events from the database and reload the tableview to refresh the information.


Now hopefully you understand a little more about how to do the navigation options in iOS.




Part 2 Testing

How do you know when a project works? Is it when you try to do something and the project does what you expect? What happens, though, if you put in something that the code is not prepared to handle? How do you make sure that your code is protected from misuse? The best way to do that is with testing.

As a part of Agile, Scrum, and SAFE, testing your system is critical to knowing when you have completed your User Stories. As you develop for PurdueHCR, we are going to require that you have tested your code and that it works to the specification you have. 

Luckily, Apple has made testing our code really easy! Watch this video to see how quick and painless it is to write tests for iOS!

https://www.youtube.com/watch?v=TsAxeBARuMU

Write 3 tests for your project. Some examples include:
•	Does the test work with normal input
•	What happens if they leave the input fields empty.
•	They put too many characters into an input field

