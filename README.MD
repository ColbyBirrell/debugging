# Debugging

In this lecture we talk about debugging practices.

`Debugging` is the process of identifying and removing errors from software.

This term originated in 1940 from Admiral Grace Hopper who was working on the Mark II computer at Harvard and found a Moth inside of the machine. When they removed the moth they delcared they were "debugging" the system.

![Debugging](images/debugging.jpg)

Debugging is a very important skill to have because you will never write any code that is 100% "bug free".

We are always adding new bugs to our code when we start adding new features or change around the architecture or design. Without the ability to find and remove the bugs inside of our code, we will never writew good software.

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

This problem was just trying to take a look at this can take forever to figure out what's going on.

This can be very inneffectiant especially when we start dealing with very complex data and algortihims. This was just to show you that some problems can be quick to look at and others can take a very long time.

Thankfully we have a ton of tools at our disposle to use when it comes to debugging.

## Tools

Chrome has some amazing tools that we can use to help us development. It would be rrally dumb to try to create something without using these tools.

You NEED to learn how to use them.

We can practice use the following tools with Joe's awesome repo: https://github.com/joeblank/debug-lecture-helper

### Console Tab

If there is an error that is being thrown on the client side (front end), the error will appear in the dev tools `console`.

This can sometimes be very descriptive and tell you exactly where the error is or can sometimes be very vague.

Go ahead and checkout to branch 1 on Joe's project to practice.

### Network Tab

Anytime we are checking up on successful or unsuccessful http requests, we should be using the `network` tab.

### Sources

The three main parts of the `sources tab include the `file navigator`, the `code editor`, and the `debugging pane`.

The file navigator will show us the files being used for the site.

The code editor will show you the actual code for the files.

The debugging pane allows us to put break points into our code rather than always just console logging.