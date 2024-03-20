# Advanced Templating Features
EJS (Embedded JavaScript Templates) is a powerful templating engine that can revolutionize how you build dynamic websites. In this guide, we're going to explore a variety of options and features that EJS offers, enabling you to tailor it perfectly to your project's needs. From speeding up your rendering process with template caching to customizing your templating syntax with unique delimiters, this journey will unveil the full potential of EJS for your web development projects.

Whether you're diving into EJS for the first time or you're a seasoned developer looking to enhance your existing projects, understanding the breadth of options available can open up new possibilities. We'll cover how to optimize performance, manage modular templates through includes, control the execution context, and even set up EJS for efficient client-side rendering. Let's embark on this explorative path together, unlocking advanced techniques to make your web development workflow more efficient and your templates more powerful.

## Options
Options in EJS act as customizable settings that dictate how your templates behave and render. These options range from performance optimizations like template caching to syntax adjustments for template delimiters. They can also influence the output's whitespace, ensuring your site's source code is clean and maintainable. Understanding and utilizing these options allows you to fine-tune your templating environment, whether you're aiming to enhance performance, ensure your templates are more readable, or need EJS to better fit within your existing development setup.

### Caching Compiled Functions
Caching is a critical performance feature in EJS, designed to eliminate redundant template compilation on every render. By enabling caching (`cache: true`) and assigning a unique `filename` for each template, EJS caches the compiled version, dramatically speeding up subsequent renders. This optimization is invaluable in production, where performance is paramount. Here's how you can enable caching:

``` javascript
ejs.renderFile('path/to/template.ejs', { title: 'EJS Caching Example' }, { cache: true, filename: 'template' }, function(err, html) {
  if (err) {
    console.error(err);
  } else {
    console.log(html);
  }
});
```
###  Including Subtemplates
To promote DRY principles and enhance template manageability, EJS facilitates the inclusion of subtemplates. This feature allows you to reuse template parts (like headers and footers) across different pages. Including a subtemplate is straightforward, using the `<%- include('path/to/subtemplate', { someData: 'data' }) %> syntax. For example, integrating a common header and footer could look like this:

``` javascript
<%- include('partials/header', { title: 'My Website' }) %>
<h1>Welcome to My Website</h1>
<p>This is an example of including subtemplates.</p>
<%- include('partials/footer') %>
```

### Custom Delimiters
EJS uses `<%` and `%>` as its default scriptlet tags, but you can customize these delimiters if they conflict with other template languages or if you prefer a different style. This is done by setting the `delimiter`, `openDelimiter`, and `closeDelimiter` options. Customizing delimiters can be particularly useful when integrating EJS with other systems where the default syntax might cause issues. For instance, if you wanted to use square brackets instead of angle brackets, you could configure EJS as follows:

```javascript
ejs.render('[%= user.name %]', { user: { name: 'Alice' } }, { delimiter: '%' });
```

### Debugging
EJS templates compile down to JavaScript functions, and sometimes it can be challenging to understand how your template translates into JavaScript, especially when errors occur. By setting the `debug` option to `true`, EJS will log the generated function body, giving you insight into the compilation process. This can be invaluable for debugging complex templates. However, it's best to use this feature during development only, as it can impact performance.

```javascript
ejs.compile('template', { compileDebug: true });
```

### Control Flow, Output Escaping, and Comments
EJS supports direct control flow statements (like `if`, `else`, `for`) within templates, enabling dynamic content rendering based on conditions. It also provides mechanisms for safely escaping output to prevent XSS attacks, using `<%= %>` for escaped output and `<%- %>` for raw output. Additionally, EJS supports comments via `<%# %>` tags, which can be useful for leaving notes or temporarily disabling parts of the template. Here's a combined example demonstrating these features:
```html
<!--Inside your ejs file-->
<%# This is a comment %>
<% if (user) { %>
  <h1>Hello, <%= user.name %></h1>
<% } else { %>
  <h1>Hello, Guest</h1>
<% } %>
```

## Include
In EJS, the `include` function streamlines web development by allowing for the insertion of reusable templates, such as user details, into a main template, thus adhering to the DRY principle. This modular approach facilitates easier maintenance and scalability of web applications. For instance, to display a list of users, you can loop through a users array and include a sub-template for each user, as shown below:
``` html
<ul>
  <% users.forEach(user => <%- include('user/show', { user }); %>); %>
</ul>
```

By leveraging these features, you can create powerful, flexible, and secure templates with EJS. Whether you're building a small project or a large web application, EJS offers the tools needed to efficiently generate dynamic HTML content.

## Conclusion

By the end of this section, you will have successfully learned the following:

- :octicons-heart-fill-24:{ .heart } 
- :octicons-heart-fill-24:{ .heart } 
- :octicons-heart-fill-24:{ .heart } 


Great job 🤗.