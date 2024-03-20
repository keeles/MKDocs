# Tags
EJS tags are special markers within EJS (Embedded JavaScript Templates) that signal to the EJS engine where JavaScript code is embedded within an HTML file. 

These tags allow you to inject data, execute JavaScript code, control flow within your templates (such as loops and conditionals), and manage whitespace. 

Understanding EJS tags is crucial for creating dynamic web pages that can display content based on user interaction, server data, or any logic defined in your JavaScript code. Here's a quick overview of the primary types of EJS tags and what they do:

## Scriptlet Tag
The Scriptlet tag `<% %>` is used for embedding any JavaScript code in the template that doesn't produce output in the final HTML. This can include control flow statements, variable declarations, or any logic necessary to prepare the data for display.
``` html
<%
  let greeting = 'Hello';   
  let name = 'World';
%>
```

## Whitespace Slurping Scriptlet Tag
The Whitespace Slurping Scriptlet tag `<%_ _%>` allows you to include JavaScript logic in your template while also removing the whitespace before it. It's useful for controlling the amount of whitespace in the rendered output for a cleaner look.
```html
<%_ let greeting = 'Hello'; _%>
<%_ let name = 'World'; _%>
```

## Outputs the Value (HTML Escaped)
The `<%=` tag outputs the value of a JavaScript expression within the template, escaping any HTML to prevent XSS attacks. This is used to safely render user-generated content or any data that may include characters interpreted as HTML.

```html
<p><%= greeting %> <%= name %>!</p>
```

## Outputs the Unescaped Value
The `<%-` tag outputs the unescaped value into the template. It should be used when you're confident that the content does not pose a risk of XSS attacks, such as when displaying content that includes HTML tags which are part of the design.
```html
<p><%- someHtmlContent %></p>
```

## Comment Tag
The Comment tag `<%# %>` lets you add comments within your EJS templates. These comments do not execute and are not included in the final HTML output. It's useful for leaving notes or commenting out parts of the template during development.

```html
<%# This is a comment and won't be rendered in the output %>
```

## Outputs a Literal '<%'
The `<%%` tag outputs a literal `<%` in the template. This can be useful when you need to display the tag itself as part of the webpage, such as in documentation or examples.
```html
<%% This will output <% in the HTML %>
```

## Plain Ending Tag
The `%>` tag is used to close any of the opening EJS tags. It signifies the end of JavaScript code or control flow statements within the template.
```html
<%
  let greeting = "Hello, World!";
%>
```

## Trim-mode ('newline slurp') Tag
The `-%>` tag trims the newline character following it in the template, which helps control the whitespace in the rendered output. It's used at the end of a scriptlet t o remove the line break that follows it.
```html
<%
  let greeting = 'Hello';
-%>
```

## Whitespace Slurping Ending Tag
The `_%>` tag removes all trailing whitespace after it, similar to the opening tag but used at the end. It's useful for minimizing the amount of unnecessary whitespace in the final output.
```html 
<%_ let greeting = 'Hello'; _%>
```

## Conclusion
By combining these tags in various ways, you can create templates that are both dynamic and secure, rendering content based on data and logic while keeping your HTML clean and organized. 

Congratulations! 🎉 You have learnt all the tags required for you to use ejs effectively.