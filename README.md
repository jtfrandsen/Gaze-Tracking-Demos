# Gaze Tracking Demos

**Purpose:** To inspire creativity in others to find meaningful applications for gaze tracking.

**Summary:** A conglomeration of AR experiences that showcase the power of gaze tracking. The experiences herein can be classified into two primary groups, object manipulation or analytical applications. Each experience highlights a separate use case and is intended to inspire AR authors think about how gaze tracking could enhance their own AR experiences.

### **Table of Contents**

- [What is Gaze Tracking?](#what-is-gaze-tracking)
- [ThingMark for Viewing AR Experiences](#thingmark-for-viewing-ar-experiences)
- [Object Manipulation](#object-manipulation)
  - [Understanding Gaze Tracking Demo](#understanding-gaze-tracking-demo)
  - [Put That, There Demo](#put-that-there-demo)
  - [User Gaze Redirection Demo](#user-gaze-redirection-demo)
  - [Simon Game Demo](#simon-game-demo)
  - [UR Robot Point Programming](#ur-robot-point-programming)
- [Analytical Applications](#analytical-applications)
  - [Quantifying Gaze Duration Demo](#quantifying-gaze-duration-demo)
  - [Board of Colorful Labels Demo](#board-of-colorful-labels-demo)
  - [Ring of Colorful Labels Demo](#ring-of-colorful-labels-demo)
  - [Logging User 3D Coordinates Demo](#logging-user-3d-coordinates-demo)
  - [Logging User Gaze Coordinates Demo](#logging-user-gaze-coordinates-demo)
 

## What is Gaze Tracking?

### Background Explanation

Before we jump right into an explanation of gaze tracking, it is important that you understand a little bit about how the position and orientation of objects are defined in a virtual 3D space. To start off, virtually positioning an object in a 3D environment isn't something that was invented for augmented reality. It has actually been around much longer and is widely used in almost every video game you have ever played. It is what allows the computer to keep track of your character and the other objects in the environment and is crucial as your character moves throughout the virtual area.

In order to define an object's position, the computer must know the object's location and which way it is facing. The location data typically come in the form of three-dimensional coordinates *(X,Y,Z)*, while the orientation data are commonly a set of angles or orthogonal vectors. These data fully-define any object in 3D space and are essential for a realistic rendering of the virtual environment.

### Position & Orientation in Vuforia 

Vuforia defines objects within the augmented reality realm using these same principles. Every object that is placed into an AR experience must have both its position and orientation defined. With this definition, the AR exprience is rendered consistently, no matter where the user is viewing from. Every widget (e.g., model, model item, 3D label) can be given X,Y,Z-coordinates, as well as X,Y,Z-rotations.

The user's position and orientation are also defined out of necessity and are constantly changing as they move through the AR space. These definitions are always made to track the user's device, whether it be a mobile device, or an AR headset. In contrast to the angles used for the other objects in the experience, the user's orientation is defined by a pair of orthogonal vectors. In the image below, the user's 3D coordinates relative to the experience origin are represented by the iPad model. The blue vector is normal to the user's device screen and represents the direction in which they are looking. The green vector is orthogonal to the blue and points vertically out of the device. It tells how the user's device is rotated about the blue vector and defines the remaining critical information.

<img width="450" alt="3D Position   Orientation" src="https://user-images.githubusercontent.com/86619231/125130156-c1374e00-e0bd-11eb-84a8-00e8cefb6635.png">

By figuring out how to access this complete set of data, we can know exactly where the user is and where they are looking in realtion to the objects in the AR experience. This knowledge allows us to take our AR experiences to the next level by using the user's position and gaze to find out more about what they are actually seeing. We can use these data to manipulate the objects in the experience or perform analysis and learn more about the users.

## ThingMark for Viewing AR Experiences

The AR experiences described below can all be viewed by scanning this ThingMark with the Vuforia View app:

<img width="300" alt="ThingMark" src="https://user-images.githubusercontent.com/86619231/125703339-dea6da9a-ef52-420b-8ef5-9cd0fcf38b19.png">

## Object Manipulation

One of the potential use cases for gaze tracking is to employ data about the user's gaze to manipulate objects within the AR space. There are endless applications in which the ability to change an AR experience based on what the user is seeing would be beneficial. Listed below are some simple demos to show potential use cases and inspire your creativity in implementing gaze tracking for yourself.

- [Understanding Gaze Tracking Demo](#understanding-gaze-tracking-demo)
- [Put That, There Demo](#put-that-there-demo)
- [User Gaze Redirection Demo](#user-gaze-redirection-demo)
- [Simon Game Demo](#simon-game-demo)
- [UR Robot Point Programming](#ur-robot-point-programming)

### Understanding Gaze Tracking Demo

This first example is fundamentally a proof of concept that helped me better understand the nature of gaze data within Vuforia Studio. Beacause it was the first AR experience created that incorperates gaze tracking, it is primarily focused on making gaze tracking data visible. There are six on-screen labels that constantly update with the user's X, Y, & Z-coordinates (the yellow point in the above explanation), as well as the X, Y, & Z components of the gaze vector (the blue vector in the above explanation). This data display allows the user to see the gaze data that are being processed in real time and gives them a better idea of what the data actually look like.

In addition to the data display, there is a basic example of moving a model within a 3D space based on the user's position. There is a small model of the Death Star that mirrors the user's position across the X-Y plane that moves left, right, up, or down with the user's device just like an object in a real mirror would. A brief screen recording of this AR experience is included below:

*As the user moves left and right, up and down, or forward and backward, watch the X, Y, and Z labels change, respectively.*

[![Understanding Gaze Tracking Demo Video](https://img.youtube.com/vi/XZiJFjOexxo/0.jpg)](https://www.youtube.com/watch?v=XZiJFjOexxo)

The "Understanding Gaze Tracking Demo" experience can be downloaded [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Understanding_Gaze_Tracking_Demo.zip) or viewed with the [ThingMark](#thingmark-for-viewing-ar-experiences) above.

### Put That, There Demo

The next example shows how gaze tracking can be used to move entire models within an AR experience. Currently, Vuforia Studio lacks the ability to reposition individual models without moving the tracking for the entire experience. This means that it is presently impossible to move AR objects relative to each other, which would necessary for tasks like laying out a space (e.g., a shop floor) using augmented reality. This AR experience serves as a remedy to this inability and is a powerful demonstration of how gaze tracking could be used to manipulate objects within an AR experience. It is based on a retro MIT Architecture Machine Group demo [Put That There](https://youtu.be/CbIn8p4_4CQ).

The mechanism for this experience is as follows: A voice command (HoloLens) or a on-screen button (mobile devices) is used to trigger the model relocation. The model displaying on the user's screen is selected and the relocation process begins. (If there is more than one model on screen, the model closest to the user is selected.) The selected model's position is determined by the point at which the user's gaze vector (the blue vector in the above explanation) intersects the ground plane (Y=0). This intersection provides an X-Z coordinate for the model to follow and once the desired position is found, the model can be locked in place with another voice command or button-press. A brief screen recording of this AR experience is included below:

*Models within the AR experience are moved relative to each other throughout the 3D environment using a Microsoft HoloLens 2.*

[![Put That, There on HoloLens 2](https://img.youtube.com/vi/h0_2xMTR_lk/0.jpg)](https://www.youtube.com/watch?v=h0_2xMTR_lk)

*Additionally, an updated twin of the AR experience can be rendered in Onshape.*

[![Put That, There with Onshape Twin](https://img.youtube.com/vi/_Gu3hrTNyVs/0.jpg)](https://www.youtube.com/watch?v=_Gu3hrTNyVs)

The "Put That, There Demo" experiences can be downloaded [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Put_That__There_Demo.zip) for mobile devices or [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Put_That__There_Demo_-_HoloLens.zip) for 3D Eyeware, or viewed with the [ThingMark](#thingmark-for-viewing-ar-experiences) above.

### User Gaze Redirection Demo

This example demonstrates how gaze tracking can be used to monitor where users are looking within an experience and redirect their gaze if necessary. This capability is useful for first-time users of an AR experience who are not familiar with where they need to point their device. It is easy to get lost in a new, virtual space which is when this AR experience becomes useful.

This AR experience operates by monitoring how focused the users gaze is on a certain object (in this case, a pneumatic valve assembly). If their focus ever falls below some defined threshold, an arrow appears on-screen and points them back to the object of interest. This arrow moves with the user's device to stay in the center of the screen and can rapidly roll, pitch, or yaw as a means of directing the user to look where they need to. A brief screen recording of this AR experience is included below:

*A snippet from the experience showing how the arrow helps the user easily redirect their gaze.*

<img width="450" alt="User Gaze Redirection Demo GIF" src="https://user-images.githubusercontent.com/86619231/142079431-a6436dd7-e8ae-40f8-a985-d14c00df6889.gif">

The "User Gaze Redirection Demo" experience can be downloaded [here](https://github.com/jtfrandsen/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/User_Gaze_Redirection_Demo.zip).

### Simon Game Demo

Next, this experience is a demonstration of how gaze tracking can enable users to interact with specific components on a model. In contrast to the "Put That, There" Demo that focuses on moving an entire model, this AR experience is lets users select specific part of a model using their gaze. This is done by tracking the user's gaze in relation to a specified portion of the model, rather than the model in its entirety. The ability to identify certain parts of a model greatly enhances the capabilities of gaze tracking and creates many additional applications in which gaze tracking could be used.

This AR experience is an augmented reality recreation of the classic game ["Simon"](https://en.wikipedia.org/wiki/Simon_(game)) and can be played either by gaze or by touch. When playing by gaze, the user selects the game's buttons using their gaze vector (the blue vector in the above explanation). The vector's position is represented by an on-screen reticle to make selecting easier. When selected, the button in question is highlighted, then pressed after a brief delay. When playing by touch, the user selects the game's button simply by pressing on their device screen, much like what happens in the physical game. A brief screen recording of this AR experience is included below:

*The classic game "Simon" is now in augmented reality and can be played either by gaze or by touch.*

[![Simon Game Demo Video](https://img.youtube.com/vi/56xJi2435xo/0.jpg)](https://www.youtube.com/watch?v=56xJi2435xo)

The "Simon Game Demo" experience can be downloaded [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Simon_Game.zip) or viewed with the [ThingMark](#thingmark-for-viewing-ar-experiences) above.

### UR Robot Point Programming

The last example in the object manipulation category demonstrates how gaze tracking can be used to interact with the physical world. This AR experience allows users to create 3D waypoints and paths for a UR3e robot to follow, in a way that is much more intuitive than using the supplied teach pendant. Once the user has defined a path in AR, this digital path is used to govern how the physical robot actually moves. It is a great example of how spatially-relevant, data-rich augmented reality can enhance and transform an industrial workspace.

One unique aspect of this AR exprience is that it incorperates a bidirectional flow of data. Data from the physical UR3e's joints are harvested by KEPServerEX and passed to a ThingWorx server for processing. A seamless integration between ThingWorx and Vuforia Studio/View allows the joint angle values to update the digital robot in AR, which renders a digital twin that overlays directly on top of the physical robot. With the digital overlaying the physical, users can use this AR experience to define waypoints in three-dimensional space and create paths for the physical robot to follow. Data flows back to the robot as 3D coordinates are sent to ThingWorx, where they are translated into [UR Script](https://www.zacobria.com/universal-robots-knowledge-base-tech-support-forum-hints-tips-cb2-cb3/index.php/ur-script-send-commands-from-host-pc-to-robot-via-socket-connection/) commands and forwared back to the physical UR3e. The robot interprets the commands and can then move accordingly. A data flow diagram and brief screen recording for this AR experience are included below:

*A simplified flow diagram showing how data flow bidirectionally between the physical and digital UR robots.*

<img width="600" alt="UR Robot Data Flow Map" src="https://user-images.githubusercontent.com/86619231/140633177-a38aace1-0374-4332-99ad-51b09cd6c4a5.jpg">

*A snippet from the experience showing how 3D waypoints are defined for the robot, using gaze tracking.*

<img width="450" alt="UR Robot Point Programming GIF" src="https://user-images.githubusercontent.com/86619231/141862239-2ea990d1-c826-40b6-b47f-bfa755c365af.gif">

The "UR Robot Point Programming" experience can be downloaded [here](). The associated ThingWorx and Kepware components can be downloaded [here](https://github.com/jtfrandsen/Gaze-Tracking-Demos/raw/main/IIoT%20Files/Entities.twx) and [here](https://github.com/jtfrandsen/Gaze-Tracking-Demos/raw/main/IIoT%20Files/UR.Robot.GitHub.opf), respectively.

## Analytical Applications

The other potential use case for gaze tracking detailed here is harvesting and logging data about the user's gaze in order to perform analysis and learn more about the users themselves. This analysis could be very useful to AR authors seeking quantitative feedback because they could see exactly how users move through their AR experiences and/or what they were looking at. It could also help those managing AR experiences (e.g., educators or line managers in a factory) to monitor how their users are interacting with the AR experiences. Listed below are some simple demos to show potential use cases and inspire your creativity in implementing gaze tracking for yourself.

- [Quantifying Gaze Duration Demo](#quantifying-gaze-duration-demo)
- [Board of Colorful Labels Demo](#board-of-colorful-labels-demo)
- [Ring of Colorful Labels Demo](#ring-of-colorful-labels-demo)
- [Logging User 3D Coordinates Demo](#logging-user-3d-coordinates-demo)
- [Logging User Gaze Coordinates Demo](#logging-user-gaze-coordinates-demo)

Download all ThingWorx entities required for these experiences [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Entities.twx).

### Quantifying Gaze Duration Demo

The first example in the analytics category was created as a testing grounds to figure out how to quantify the time spent looking at each object in the AR experience. It is similar to the "Understanding Gaze Tracking Demo" above, in that it is primarily focused on making gaze tracking data visible. There are seven on-screen labels that constantly update with the total time spent in the AR experience, the user's focus on both objects, their distance from both objects, as well as the time they have spent looking at each object. This data display allows the user to see the gaze data that are being processed in real time and gives them a better idea of what the data actually look like.

This experience is able to determine if a user is looking at an object by taking the dot product between the gaze vector (the blue vector in the above explanation) and the vector from the user to the object in question. When used with unit vectors, the dot product yields a value between \[-1, 1\] and the closer the result is to 1, the closer the two vectors are aligned. Testing was performed to determine that a dot product was greater than or equal to 0.85 meant the object was currently displayed on the screen. It could then be concluded that when the dot product of the gaze vector and any object exceeded the threshold of 0.85, the gaze timer for that object should increment. A brief screen recording of this AR experience is included below:

*As the user focuses their gaze on each object, the corresponding timer increments to compute the total gaze duration for that object.*

[![Quantifying Gaze Duration Demo Video](https://img.youtube.com/vi/N58wQ4ZVTQk/0.jpg)](https://www.youtube.com/watch?v=N58wQ4ZVTQk)

The "Quantifying Gaze Duration Demo" experience can be downloaded [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Quantifying_Gaze_Duration_Demo.zip) or viewed with the [ThingMark](#thingmark-for-viewing-ar-experiences) above.

### Board of Colorful Labels Demo

The next example shows how gaze tracking can be used to conduct experiments to quantify how captivated users are by different elements within the AR space. This AR experience contains 10 3D labels that all different colors and strives to quantify how different colored labels engage the user's attention. The color of the each label is randomly assigned each time the experience is opened in order to minimize any bias created by the label's position. The labels have been arranged like a flat billboard for easy viewing.

As the user moves throughout the AR experience, their gaze data is continuously passed into ThingWorx and logged in a DataTable every 0.5 seconds. This data table contains three fields pertaining to the experience as a whole, as well as four separate fields for each of the 10 labels. Explanations for each data field are listed below:

<details>
<summary>Data Field Explanations</summary>
<br>
  extraTime: The total time spent not looking at any of the objects. <br>
  objectBeingViewed: The object closest to the center of the device screen. <br>
  totalTime: The total time spent inside the AR experience. <br>
  obj#Class: The label's randomly assigned CSS class, which controls the label's color. <br>
  obj#Dist: The distance from the user to the label. <br>
  obj#Dot: The dot product of the user's gaze vector and the vector from the user to the label (this quantifies the user's focus on the label). <br>
  obj#Timer: The total time spent viewing the label.
</details>
<br>

<img height="350" alt="Sample Data Table" src="https://user-images.githubusercontent.com/86619231/126009238-069bcd1e-8f6e-460e-ba2b-7a640f2e3de3.png">

Once the data have been harvested, many forms of analysis can be performed to quantify what kinds of interactions user's are having with the elements of an AR experience. A brief screen recording showing a sample interaction and the accompanying analysis is included below:

*Charts like the one shown in this video can be used to analyze how users interact with an AR experience.*

[![Board of Colorful Labels Demo Video](https://img.youtube.com/vi/QF1vHx24uEY/0.jpg)](https://www.youtube.com/watch?v=QF1vHx24uEY)

The "Board of Colorful Labels Demo" experience can be downloaded [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Board_of_Colorful_Labels.zip) or viewed with the [ThingMark](#thingmark-for-viewing-ar-experiences) above.

### Ring of Colorful Labels Demo

This example is fundamentally a twin of the "Board of Colorful Labels Demo", but with a different layout for the labels. Instead of being arranged as a flat billboard, the 10 3D labels form a ring around the experience's origin. This new layout serves as another demonstration for how experiements could be set up for quantification with gaze tracking. A brief screen recording of this AR experience is included below:

*Many data point about the user's gaze are logged into a ThingWorx data table. This AR experience serves as a sample environment for harvesting gaze data.*

[![Ring of Colorful Labels Demo Video](https://img.youtube.com/vi/eX7HjJLnazs/0.jpg)](https://www.youtube.com/watch?v=eX7HjJLnazs)

The "Ring of Colorful Labels Demo" experience can be downloaded [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Ring_of_Colorful_Labels.zip) or viewed with the [ThingMark](#thingmark-for-viewing-ar-experiences) above.

### Logging User 3D Coordinates Demo

Here is another example in the analytics category that demonstrates how gaze tracking can be used to record a user's motion through an AR experience. This experience is similar to the "Understanding Gaze Tracking Demo", in that the user's 3D coordinates (the yellow point in the above explanation) are the primary data being used. This experience goes one step further than the "Understanding Gaze Tracking Demo" by logging the X, Y, & Z-coordinates to a ThingWorx data table so analysis can be performed. One intuitive method for visualizing how users move through AR experiences is by creating a heat map of their coordinates to show the areas in which they spent the most time. A sample heat map and a screen recording of when the data was collected are included below:

*The darkest red regions indicate where the most time was spent, while each dot represents a point where data was collected.*

<img width="600" alt="Sample User Coordinate Heat Map" src="https://user-images.githubusercontent.com/86619231/126197497-531ef5de-7d02-4646-b712-9f44200e392a.png">

*A condensed version of the experience in which the data for the above heat map was collected.*

<img width="450" alt="Logging User 3D Coordinates Demo GIF" src="https://user-images.githubusercontent.com/86619231/126430000-ad923916-0b36-4f87-985e-3dc8c765c26f.gif">

The "Logging User 3D Coordinates Demo" experience can be downloaded [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Logging_User_3D_Coordinates_Demo.zip) or viewed with the [ThingMark](#thingmark-for-viewing-ar-experiences) above.

### Logging User Gaze Coordinates Demo

The final example in the analytics category demonstrates another method for recording user's gaze using gaze tracking. This experience is similar to the "Put That, There Demo", in that the intersection of the user's gaze vector (the blue vector in the above explanation) with a defined plane is the primary data being used. However, instead of using this intersection point to move a model, this experience takes that point and logs it to a ThingWorx data table so analysis can be performed. One intuitive method for visualizing where users are pointing their devices is by creating a heat map the gaze intersetion points to show the areas the viewed the longest. A sample heat map and a screen recording of when the data was collected are included below:

*The darkest red regions indicate where the most time was spent, while each dot represents a point where data was collected.*

<img width="600" alt="Sample Gaze Coordinate Heat Map" src="https://user-images.githubusercontent.com/86619231/126362705-6d8be665-d437-4106-ac1d-789b969f31fb.png">

*A condensed version of the experience in which the data for the above heat map was collected.*

<img width="450" alt="Logging User Gaze Coordinates Demo GIF" src="https://user-images.githubusercontent.com/86619231/126428817-27ad55f7-63a1-49c9-8db1-0d739417489d.gif">

The "Logging User Gaze Coordinates Demo" experience can be downloaded [here](https://github.com/PTC-Education/Gaze-Tracking-Demos/raw/main/AR%20Experience%20Files/Logging_User_Gaze_Coordinates_Demo.zip) or viewed with the [ThingMark](#thingmark-for-viewing-ar-experiences) above.
