# Debugging

## Learning objectives​
- Students are familiar and understand the following devtools:
  - Elements tab
    - Manipulate elements on the screen directly.
  - Console tab
    - Execute javascript directly in the console.
    - Read errors provided by javascript.
      - Find file/line number of error.
  - Sources tab
    - See files and use the debugger.
  - Network tab
    - Read and understand the status of network requests.
    - See status code and response of network request.
  - Components tab
    - Locate specific components and see state/prop values.
  - Redux devtools
    - Observe changes in redux state.
- Students are able to `console.log()` to check values

# Lecture Notes 

This lecture will cover debugging and how to use the Google Chrome Developer Tools. 

`Debugging` is the process of identifying and removing errors from software.

This term originated in 1940 from Admiral Grace Hopper who was working on the Mark II computer at Harvard and found a Moth inside of the machine. When they removed the moth they declared they were "debugging" the system.

![Debugging](images/debugging.jpg)

Debugging is a very important skill to have because you will never write any code that is 100% "bug free".

We are always adding new bugs to our code when we start adding new features or change around the architecture or design. Without the ability to find and remove the bugs inside of our code, we will never write good software.

The better you are at reasoning about code and figuring out why it is broken, the more valuable & efficient you will be as a programmer.

## Debugging Basics

```js
function addNumbers(num1, num2) {
  return num1 + num2;
}

addNumbers(4, "5");
```

Above is an example problem:

1. What is the result from this function execution?

2. Where is the bug inside the code?

3. How did you come to that conclusion?

Now here is a problem that is a bit more complex:

```js
var mySingleton = function() {
  function init() {
    function privateMethod() {
      console.log("I am private");
    }
    var privateVariable = "Im also private";
    var privateRandomNumber = Math.random();
    return {
      publicMethod: function() {
        console.log("The public can see me!");
      },
      publicProperty: "I am also public",
      getRandomNumber: function() {
        return privateRandomNumber;
      }
    };
  }
  return {
    getInstance: function() {
      if (instance) {
        instance = init();
      }
      return instance;
    }
  };
};

var mySingleton = singletonCreator();

var singleA = mySingleton.getInstance();
var singleB = mySingleton.getInstance();
console.log(singleA.getRandomNumber() === singleB.getRandomNumber());
```

Can you find the bug?

Just trying to take a look at this can take forever to figure out what's going on. Simply scanning for bugs is often an exercise in futility.

This is especially inefficient when we start dealing with very complex data and algorithms. This exercise was to show you that some problems can be quick to look at while others can take a very long time.

There are several things that can tell us our code has a bug: 
  - We receive an error. Often bugs will completely break our code and prevent us from using our app or coding further until we resolve them.
  - Our code doesn't behave as we expect. Even if a bug doesn't break our code it can prevent it from functioning as expected. We may receive a non-breaking error or warning in our console, or we may have to use developer tools to track down the bug.

Often our code will break and everything will look fine. Restarting processes like Node often can ensure that we're dealing with our most current code and not bugs we have already resolved. However, if we're running our latest code and it is breaking or not behaving properly, rest assured that the computer is right and it is time to use our developer tools to debug.

Thankfully, we have an array of quality tools at our disposal to use when it comes to debugging.

## Tools

Chrome has some amazing tools that we can use to help us in development. Coding without using these tools would be foolish. It is absolutely essential that you become familiar with them.

The following video is an excellent beginner/intermediate tutorial on how to use the Chrome developer tools: https://www.youtube.com/watch?v=x4q86IjJFag. The notes below are an overview of this content. 

## Elements

The Elements tab allows us to inspect our HTML elements and their CSS properties. This is extremely useful to help us determine where our elements are at and what properties are affecting them. 

We can select an HTML element by clicking it in our console. This will cause it to be highlighted on the web page, and will also display its CSS properties in the bottom or side of the console. We can also use the inspector (the mouse in the square in the top-left corner of the Elements tab) to select an element on the page and view it in the console. 

We can add, remove and adjust a given element just as we can in our code editor. The changes will be reflected on the web page, but DO NOT affect our actual code and will be lost upon page reload. This is a useful tool for determining what adjustments need to be made to our HTML and CSS. To make the actual changes you will have to go to your code editor or Sources tab.

### Console Tab

If there is an error that is being thrown on the client side (front end), the error will appear in the dev tools `Console`. Sometimes these errors will point us to the exact line and column of the error and sometimes they can be rather vague. If you do not understand an error after reading through it, copying and pasting it into a Google search can help you determine what might be causing it. 

We can also use the console to determine what is happening in our code. This video provides an excellent overview of common use cases for the console: https://www.youtube.com/watch?v=L8CDt1J3DAw&feature=youtu.be. Though you will predominantly use `console.log`, the other console methods are useful and should be learned.

In addition to logging information, we can write javascript expressions in the console and run them. To do so simply begin typing in the console. Hit enter to run. We can use `$_` to see the last expression that we ran. We can also use `$0, $1, $2` etc. to see the last HTML elements we inspected.

We can use JavaScript selectors (such as `document.getElementById()` and `document.querySelector()`) to select elements or CSS identifiers. A shortcut to do the same thing for elements is to use the `$` like so: `$('h1')`. We can adjust the properties affecting the selected elements using these selectors. 

We can open the console inside of any of the following tabs by pushing the `esc` key while in another tab. 

### Network Tab

The Network tab allows us to inspect what resources are being downloaded or uploaded and if they are performing as expected. Resources include all the files connected to our page (such as CSS stylesheets and JavaScript files) as well as any HTTP requests made to other files or external APIs.

Anytime we are checking up on http requests (whether successful or unsuccessful), we should be using the `network` tab.

The Headers, Preview and Response sections give us valuable information about our resources. Headers tells us what type of method a request was, if it was successful or not, and holds information that accompanies the request.

Preview and Response are very useful for API calls especially, as they show us what came back from the request and what type of data it is. 

### Sources

In the Sources tab under File System we can add folders to our workspace. This allows us to permanently edit our code right from the browser. To add a folder to the workspace, click 'Add to workspace'. Follow the file path to the folder you want to add and select it. You will then see a pop-up in Chrome asking for permission to edit the folder. Once you grant permission you can select a file from the folder, edit it, and use `Ctrl + S` (Windows) or `Cmd + S` (Mac) to save the changes. 

We can also add breakpoints in our code by clicking the line number. These breakpoints will stop the code on the selected line as it runs through the file. We can then inspect the values of our code at that point in time. This can provide useful information about what is happening as our code runs. As an alternative to creating breakpoints in the console, we can place the keyword `debugger` in our code to achieve the same effect. 

We can also make code Snippets in the Sources tab. Snippets are reusable pieces of code that run in the scope of the page we are inspecting. 

### Components

The Components tab is part of the React Developer Tools Chrome extension. It allows us to quickly and easily view our component tree and see what each component contains. 

This is especially useful for checking what our props and state values are without having to clutter our code with console logs.  

The Components tab is very simple. There is a file tree that you can navigate through, allowing you to see which folder contains a give file. When you select a file its state and props values will be displayed on the left, along with it's parent components. 

### Redux Devtools. 

Redux Devtools is a Chrome extension that allows us to inspect what is happening on our redux state from the console. To install these tools go to this link: https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en.

To implement these tools we need to bring a few things into our redux store. First we need to install `redux-devtools-extension` in our app using npm. Then in our store we will destructure `composeWithDevTools` off of it. We will then pass `composeWithDevTools` as an argument in our `createStore`, and invoke it passing in middleware:

  - Without Redux Devtools:
```javascript
  import {createStore, applyMiddleware} from 'redux';
  import promiseMiddleware from 'redux-promise-middleware';
  import userReducer from './userReducer'

  export default createStore(userReducer,
      applyMiddleware(promiseMiddleware)
  )
```

  - With Redux Devtools:

```javascript
  import {createStore, applyMiddleware} from 'redux';
  import promiseMiddleware from 'redux-promise-middleware';
  import userReducer from './userReducer'
  import {composeWithDevTools} from 'redux-devtools-extension'

  export default createStore(userReducer, composeWithDevTools(
      applyMiddleware(promiseMiddleware)
  ))
```

Once we have implemented it in our code as above we can open the Redux tab in our Chrome Developer Tools. In this tab we can open the Inspector, which will show us which action creator functions have been called. We can select any of these actions to view what the value of redux state was at that time, allowing us to 'time travel' throughout our app. The Log monitor is a log of every redux action that has taken place and what the result was. Chart is an interactive data chart of the data held on redux and where and how it is being passed. 

We can use these tools to track what is happening in our Redux and debug when something unexpected happens (or when something expected doesn't happen). 

## Debugging Project
We can practice use our Console, Network and Source tools with this repo: https://github.com/joeblank/debug-lecture-helper

Fork and clone the above repo. Checkout to branch 'one' on the project to practice using the Console tab. Once you have debugged that file, checkout to branch 'two'.

On branch 'three' there is an app with four buttons. Some may not be working correctly. Use your Network tab to resolve any bugs. You may need to refer to these docs for the API we are attempting to use: https://app.swaggerhub.com/apis/DevMountain/Joes-Auto/1.0.0

Branch 'four' will require you to use breakpoints in the Source tab to debug. 

# Additional Resources

General Resources: 
  - These are the official docs for Chrome Developer Tools. They should be your first resource for learning how to use them: https://developers.google.com/web/tools/chrome-devtools
  - Great overview of Elements, Console, Sources and Network tabs: https://www.youtube.com/watch?v=x4q86IjJFag

Elements tab: 
  - A guide to editing HTML elements in the DOM https://developers.google.com/web/tools/chrome-devtools/dom
  - A guide to changing CSS properties: https://developers.google.com/web/tools/chrome-devtools/css

Console Tab: 
  - Beyond console.log in 100 seconds - a brief overview to other useful console features: https://www.youtube.com/watch?v=L8CDt1J3DAw&feature=youtu.be
  - A guide to using JavaScript in the Console tab from the official Chrome Developer Tools docs: https://developers.google.com/web/tools/chrome-devtools/console/javascript
  - A general guide to using the Console tab from the official Chrome Developer Tools docs: https://developers.google.com/web/tools/chrome-devtools/console

Network Tab:
  - A simple guide to using the Network tab: https://www.youtube.com/watch?v=nl8iKlo2NeM
  - A guide to using the Network tab from the official Chrome Developer Tools docs: https://developers.google.com/web/tools/chrome-devtools/network

Sources Tab: 
  - Basic debugging using the Source tab: https://developers.google.com/web/tools/chrome-devtools/javascript
  - How to make and use Snippets: https://developers.google.com/web/tools/chrome-devtools/javascript/snippets

Components:
  - A guide to using the Components tab in React DevTools: https://flaviocopes.com/react-developer-tools/
  - This guide walks through the using the most recent version of React DevTools: https://blog.logrocket.com/debug-react-applications-with-the-new-react-devtools/

Redux Dev Tools:
  - This video tutorial walks through setting up and using Redux Dev Tools: https://www.youtube.com/watch?v=KZYyQEi7Fzc
  - Read-along tutorial of using Redux Dev Tools: https://www.tutorialspoint.com/redux/redux_devtools.htm
  - This article will walk you through the process of setting up and using Redux Dev Tools: https://medium.com/@samueldinesh/setting-up-redux-devtools-a-simple-guide-3b386a6254fa

