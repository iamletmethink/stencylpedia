> **Extending Stencyl**

> Engine ([Basics](http://www.stencyl.com/help/view/how-to-create-engine-extension/) - [iOS & Android](http://www.stencyl.com/help/view/how-to-create-native-engine-extension/) - [Flash](http://www.stencyl.com/help/view/flash-extensions/) - [Blocks](http://www.stencyl.com/help/view/adding-blocks/) - [API](http://static.stencyl.com/api/33/))

> Toolset ([Extensions](http://www.stencyl.com/help/view/creating-extensions/) - [API](http://api.stencyl.com/extensions/))


## Contents

* Introduction
* Concepts - Hooks and Callbacks
* Getting Started
* Publishing an Extension
* Reference
  * Javadocs (API)
  * Callback Reference
  * GUI API Reference
  * Data API Reference
 

## Introduction

Extensions are small applications or controls that add new functionality to Stencyl. They serve the same purpose as extensions for web browsers, such as Firefox and Chrome. Extensions allow the community to extend the utility of Stencyl itself to fit its unique needs. 

#### Our Best Extension - Dialog System

The most notable extension created with Stencyl at the moment is the [Dialog Extension](http://dialogextension.com/), a powerful, easy to use dialog system that supports pretty much every feature you'd need.

![dialog-extension](http://static.stencyl.com/pedia2/ch4/text/dialog.png)
 
#### What do you need to know?

* Java
* Swing and/or some experience creating GUIs

Although we provide an API that makes it simple to build a GUI with no Swing knowledge, knowing it will give you the ability to create more powerful extensions.

#### Can ___ be an extension?

As long as the extension has something to do with Stencyl, it's generally doable. If you're looking to extend the engine, [look here](http://www.stencyl.com/help/view/how-to-create-engine-extension) instead.

Today, since Extensions can only be accessed from the Extensions menu, this constraint means that extensions that deal with productivity or general use will work the best. Keep that in mind when developing your extension.

 
## Concepts - Hooks and Callbacks

Developing an extension is simple once you master two key concepts: hooks and callbacks.

#### Hooks

Hooks determine **where your extension is displayed** in Stencyl's GUI. At this time, the available places where an extension an hook into include:

* Extensions menu
* ???

#### Callbacks

Callbacks are functions that you implement inside your extension. These callback functions are called at specific times in Stencyl's lifecycle. 

For example, there are callbacks for these activities:

* User opens Stencyl
* User opens a game
* User saves a game

Every callback is documented at the end of this manual and inside our API docs.

 
## Getting Started - How to Create an Extension

#### Requirements

You will need the following before you begin.

* Java Development Kit (JDK) 1.8. Do not use anything older.
* The latest version of Stencyl. Avoid targeting old versions of Stencyl.
* Eclipse, Netbeans or any setup that can run an ANT Build. 

> ANT is a task running system for Java. We'll go through it when we reach the point where it's needed.
 
#### Download the Toolset SDK

[Download](http://static.stencyl.com/extensions/Stencyl-SDK-1.0.0.zip)

The SDK consists of a sample project and our API docs for extensions.

#### First Steps

1. Go to [WORKSPACE]/extensions/ - This folder contains all of your toolset extensions.
2. Open up the Sample Project in your IDE by creating a new, existing project. 
  * Peek at the README, which contains specific instructions for the nitty gritty project setup. 
  * Add sw.jar to the project's classpath and edit build.xml as directed.
3. After that is done, run the "dist" ANT task. This builds a JAR file that Stencyl recognizes as an extension.
4. Launch your copy of Stencyl, and you will see the Sample Extension appear in the Extensions menu and also inside the Extensions Manager. Play around with it.
 
#### Developing

1. Now that the sample extension runs, flip to SampleExtension.java, the source that defines the extension itself.
2. Do you see how it impplements a bunch of callback functions that all start with "on"?
3. Make a simple edit to it.
4. Rebuild and rerun in Stencyl. Does your change show up?


## Publishing an Extension

Extensions are distributed through our [Developer Center](http://www.stencyl.com/developers/market/). Extensions must be manually approved to show up on that site. To do this, you must do two things.

1. Post your extension on the [Forums](http://community.stencyl.com/index.php/board,11.0.html) for a community review.
2. If the community response is positive, we may post up your extension without any action on your part. If not, [contact us](http://www.stencyl.com/about/contact/) and point out your forum topic.

Include the following details in the forum topic.

* A **description** of your extension
* Your extension in JAR form
* A **48x48 PNG** icon for your extension
* At least **1 screenshot** of your extension

It's preferable that you either build documentation into the forum topic or provide a link to a site that does.


## API Documentation

View the [Java-based API](http://api.stencyl.com/extensions/).

We cover the main parts of this API in the following sections.


## Callback Reference

Callbacks are functions that you implement inside your extension. These callback functions are called at specific times in Stencyl's lifecycle. Consult the [API](http://api.stencyl.com/extensions/) for the full list of callbacks.

***

**onStartup()**<br/>
Called when Stencyl is launching. Try not to do anything intense, or it will slow down launch.

***

**onActivate()**<br/>
Called when the extension is told to display or "do work"

***

**onDestroy()**<br/>
Called when Stencyl is being quit out of. Usually, you'd use this to save stuff out.

***

**onGameSave(Game game)**<br/>
Happens whenever a game is saved.

***

**onGameOpened(Game game)**<br/>
Happens whenever a game is opened.

***

**onGameClosed(Game game)**<br/>
Happens whenever a game is closed.

***

**OptionsPanel onOptions()**<br/>
Returns a configuration panel for this extension that's shown when the Options button is clicked in the extensions manager. View the [API for the Options Panel](http://api.stencyl.com/extensions/stencyl/sw/ext/OptionsPanel.html) as well as the source to the Sample Extension for usage samples.

***

**onInstall()**<br/>
Happens when the extension is first installed.

***

**onUninstall()**<br/>
Happens when the extension is uninstalled. Do cleanup.

***


## GUI API Reference

We provide a set of functions to help you build a GUI or perform common tasks.

***

**showMessageDialog(String title, String text)**
<br/>
Pops up a modal dialog with the given title and text.

***

**doLongTask(final Runnable mainTask, final Runnable onFinish)**
<br/>
Perform a long task that would have hung/frozen the GUI. Pass in 2 Runnables. Runnables look like this:

```
Runnable r = new Runnable() {
    public void run() {
        //Do Stuff
    }
};
```

***

**setProgressMessage(final String msg)**
<br/>
Sets the message shown inside the progress spinner. Keep it brief!

***

**showProgressSpinner()**
<br/>
Shows the progress spinner. Use it in conjunction with doLongTask.

***

**hideProgressSpinner()**
<br/>
Hides the progress spinner.

*** 

## Data API Reference

If you need to store data, use our data API to save out this data to disk. Do not attempt to write out to other locations using the plain Java API's. We may reject your extension if you do so.

> TODO JUSTIN: There's a better place to store data - directly in a game's extras subfolder. This is now the preferred place to store data and is being used by all our top extensions.
 
***

**String readData()**
<br/>
Reads the extension's data into a String. No file path is provided because it all comes from a pre-determined location on disk.

***

**byte[] readDataAsBytes()**
<br/>
Reads the exension's data into a byte array.

***

**boolean saveData(String data)**
<br/>
Saves data, provided as text, to the data store.

***

**boolean saveDataAsBytes(byte[] b)**
<br/>
Saves data, provided as a byte array, to the data store.

*** 