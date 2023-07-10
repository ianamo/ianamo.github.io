---
title: My Road to the Full Stack, Part Two -- Feel the MERN
layout: post
---

In my last post about my journey to full stack development, I gave a brief analogy for what we mean by a "full stack": our frontend is like our front lawn, where we can do a lot of cool stuff, but always in full view of the neighborhood and with little opportunity for security or secrets. The backend is our house, where we have more control about access and display, and includes our database, where we store stuff. The MERN stack, which you'll recall was my goal stack to learn, is just a set of software that implements this structure. We have ReactJS, our "front lawn" framework, ExpresssJS and NodeJS, which will be our house connected to MongoDB, our database. 

You can find a lot of documentation about these, and I won't try to reproduce that information. My goal is just to explain what these are and give a few pointers that I would have liked to know when I was learning these things. 

If you're coming to this stack without prior experience, I would start by learning React. It can do some very fun things right out of the box, and finding hosting for React apps is relatively cheap and easy, usually free. The advice generally given is not to tackle React until you are very familiar with vanilla JavaScript, and this is true. You should mess around making things in pure JS before moving on to React &mdash; the best way is probably to make something in regular JS and then try to reproduce and extend its functionality in React. Kind of like translating between two languages, both React and regular JS have their own idioms and their own ways of accomplishing their goals. Let's take a super simple example: suppose you wanted to implement a website with two elements, a piece of text that holds a number, and a button that will make that number increase by one every time it is pressed. That should be shockingly useful, right? Maybe someone doing inventory can use it for counting...

Here's how you might implement it with regular JS. First you would have your HTML:

``` html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>Counter App</title>
</head>
<body>
	<p id="counter">0</p>
	<button onclick=handleClick()>ADD ONE</button>
</body>
</html>
```

This sets up the HTML for the browser, giving it the required text (with the initial value of 0) and telling it to call a function called "handleClick" every time the button is pressed. Now we just need our JS to tell the browser what should happen in the handleClick function. We could, if we wished, create a separate `index.js` and then import it into our HTML, but since this is a pretty simple operation, we can also just make use of the `script` tag to define it right there in the HTML document. The final product ends up looking like this:

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>Counter App</title>
</head>
<body>
	<script>
	function handleClick() {
		let num = Number(document.getElementById('counter').innerHTML);
		num += 1;
		document.getElementById('counter').innerHTML = num;
	}	
	</script>
	<p id="counter">0</p>
	<button onclick=handleClick()>ADD ONE</button>
</body>
</html>
```

Betweeen the `script` tags, we have defined `handleClick`: it will access the inner HTML of the `<p>` tag with the ID "counter," convert it into a number with the handy `Number()` function, and then increment it by one, finally accessing the `<p>` tag again to set it to the new incremented value. This is just one way to implement this functionality: we also could have added an event listener on the button to execute a similar function. As you can see, writing regular JS demands familiarity with the Document-Object Model (DOM) so that we can get access to different elements of our website and alter them. 

We can implement the same kind of thing in React, but it requires a different idiom. For one thing, even initializing a React project is considerably more complex than just writing an HTML file. Insteal of having a single file to worry about, we now have a whole project folder with subfolders and so on. To simplify this, let's make use of a great online IDE for react, Codesandbox. You can see my implementation [here)](https://codesandbox.io/s/counter-ctjqj8). The key bit of code looks like this:

```javascript
import { useState } from "react";
import "./styles.css";

export default function App() {
  const [counter, setCounter] = useState(0);
  function handleClick() {
    setCounter(counter + 1);
  }

  return (
    <div className="App">
      <p>{counter}</p>
      <button onClick={handleClick}>ADD ONE</button>
    </div>
  );
}
```

In some ways, the React way of doing this is simpler, and in some ways it's more complicated. Instead of just manipulating text in an HTML document, our code now mixes HTML and JavaScript in ways that can look a bit untidy at first (though this does make the creation of reusable bits of HTML and JS called _components_ considerably easier to implement). Basically, instead of inserting a script into HTML, our document is now a JavaScript function that returns an HTML element (in this case, a `div`, though it can be anything). We are permitted to mix JS variables right into the HTML, as long as we put them in the curly braces, as you can see was done with `{counter}`. We can make this variable into something that can be easily changed and updated in real time by using the `useState` function, which is an example of a React hook. `useState` lets us set default values (in this case, initializing the counter to 0) and also define a function we'll use to modify its value &mdash; namely, `setCounter`. 

There's a lot more that could be said about the process of writing React code, but the point here is just to say that regular JS and ReactJS have their own idiomatic ways of accomplishing the same goals, and it's important to be able to understand the differences and translate between them. The complexity of React starts to pay off as you get into more and more complicated kinds of apps. 

Anyway, that's the R in our MERN, and if you're like me, you're probably starting to wonder about the other letters &mdash; Mongo, Express, and Node. The quick-and-dirty explanation is that Node is a project for extending where JavaScript can be used. JS was originally designed to run in a browser, like Chrome or Firefox. The basic purpose of Node is to turn it into a language that can be used in the manner of more typical scripting languages like Python or Ruby &mdash; something that can run as a computer program and not just within the browser. Expresss is one instance of a Node app, that uses JS to run a web server on your computer, something that allows you to use JS not just on your front lawn but to build your house as well. Recall that developing on the backend requires you to define how and under what conditions things in your house can be accessed, a set of rules that's called an API in the lingo, and Express is a great framework for writing APIs. Mongo is our database, of a variety known as no-SQL or non-relational. There's a lot more to be said about that as well, obviously, beyond the scope of a single blog post!

The thing to know is that while setting up your local environment for Express, Node, and Mongo development is relatively easy, deploying such projects is more complicated than with frontend apps like React, and sometimes the best option for hosting your backend is just to pony up for some fees. There is also less margin for error, because a good backend requires security and secrets that you can accicentally reveal to the whole internet if you're not careful. In my next post in this series, I'll talk about the MERN stack a bit more and in the context of developing my app [Alexandria](https://superb-sable-476bca.netlify.app/) for tracking books lended between users.
