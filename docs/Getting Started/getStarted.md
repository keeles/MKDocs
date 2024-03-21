# What is EJS?

Embedded JavaScript, or EJS, is a simple and direct templating language that enables JavaScript to generate HTML. It's frequently used in Express.js, a Node.js framework for creating web applications, but it can also be used in other JavaScript environments.

EJS is designed to generate HTML content with embedded JavaScript, primarily on the server. It is used in server-side rendering to produce web pages dynamically, allowing for the creation of web pages with content that can change depending on user actions, server state, or other variables.

We aims to provide clear context and prerequisites for new users approaching EJS, laying out the groundwork necessary for successful application and further exploration of the templating engine's capabilities.

## Prerequisite

1. Node.JS  
    Make sure you installed Node JS on your local machine in order to write JavaScript
   The link is provided here:
   https://nodejs.org/en

   - After you download the latest version of Node, you can test the JavaScript that you wrote is correctly running in the terminal by typing

2. Text Editor  
   Use any text editor or (integrated development environment) IDE of your choice for writing code. Popular options include VSCode, Sublime Text, Atom, etc.

## Installation of EJS

To install EJS, use npm (node package manager) with the following command in your project directory:

`npm install ejs
`

## Basic Syntax

EJS tags include:

`<%`: 'Scriptlet' tag, for control-flow, no output  
`<%_`: ‘Whitespace Slurping’ Scriptlet tag, strips all whitespace before it  
`<%=`: Outputs the value into the template (HTML escaped)  
`<%-`: Outputs the unescaped value into the template (make sure to only use this with content that is coming from the dev, instead of the user)  
`<%#`: Comment tag, no execution, no output  
`<%%`: Outputs a literal `<%`  
`%>`: Plain ending tag  
`-%>`: Trim-mode ('newline slurp') tag, trims following newline  
`_%>`: ‘Whitespace Slurping’ ending tag, removes all whitespace after it

!!! info

    > for more in-depth information, please read [here](../Tags/tags.md/)

## Writing EJS Templates

Since EJS templates are HTML files with embedded JavaScript code, creating a `.ejs` files is very similar to creating a HTML file.

For example,  
views/index.ejs:

```html hl_lines="8"
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <h1>Welcome to EJS, <%= user.name %></h1>
  </body>
</html>
```

!!! info

    > JavaScript: (assuming you have your express.js set up, we have also set up a more in-depth instruction [here](../Express/express.md/)

```js hl_lines="2"
app.get("/", (req, res) => {
  res.render("index", { user: { name: "John Doe" } });
});
```

The HTML snippet shows the usage of EJS syntax that inputs the variable which you passed from JavaScript. Notice on line 2 of the JavaScript snippet, we passed in the user object with the name object in the second parameter, so when we put in to ejs file,
`Welcome to EJS, John Doe` will be rendered on the page.
