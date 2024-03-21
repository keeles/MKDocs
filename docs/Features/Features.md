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

## CLI
EJS's command-line interface (CLI) brings the power of EJS templating to the terminal, providing a suite of options for rendering files directly from the command line. This feature is especially useful for batch processing, testing, or integrating EJS into scripts and other development workflows. The CLI supports a range of options that mirror those available in the JavaScript API, making it a versatile tool for developers familiar with EJS.

### cache
The cache option enables the caching of compiled functions, significantly speeding up the rendering process for templates that are used frequently. This option requires the use of the filename parameter to uniquely identify each template in the cache, ensuring that templates are correctly retrieved from cache when needed.

#### -o / --output-file FILE 
The `-o` or `--output-file` argument specifies a file to which the rendered output should be written. By default, EJS renders to stdout, which is suitable for viewing output directly in the terminal or piping to other commands. However, when rendering files as part of a build process or for static site generation, directing output to a specific file is often necessary.


#### -f / --data-file FILE
The `-f` or `--data-file` option allows you to specify a JSON-formatted file as the source of data for rendering the template. This feature is particularly useful when you have predefined data structures or are utilizing data from an external source, enabling dynamic content generation based on the contents of the file.

#### -i / --data-input STRING
Similar to the `-f` option, `-i` or `--data-input` accepts a JSON-formatted and URI-encoded string as input data for rendering. This option is ideal for passing small amounts of data directly through the command line without the need for an external file.

#### -m / --delimiter CHARACTER
The `-m` or `--delimiter` argument allows you to customize the character used for opening and closing tags within your EJS templates. By default, EJS uses % as the delimiter, but this can be changed to any character that suits your project's needs, providing flexibility in template syntax.

#### -p / --open-delimiter CHARACTER
With `-p` or `--open-delimiter`, you can define a custom character to replace the standard left angle bracket (<) for opening EJS tags. This option is useful when integrating EJS templates with other languages or systems where the default syntax may cause conflicts.

#### -c / --close-delimiter CHARACTER
The `-c` or `--close-delimiter` option serves a similar purpose to -p, but for the closing tag, allowing you to specify a custom character to replace the right angle bracket (>) for closing EJS tags. This customization ensures compatibility across different environments and syntax requirements.

#### -s / --strict
Enabling the `-s` or `--strict` mode forces the generated functions to run in JavaScript's strict mode. This mode imposes stricter parsing and error handling on your code, helping to prevent common coding bloopers and making it easier to write "secure" JavaScript.

#### -n / --no-with
The `-n` or `--no-with` option disables the use of JavaScript's with statement in the template's scope. This leads to better performance and more predictable scope resolution, with variables explicitly taken from the locals object. This option implicitly enables strict mode (--strict).

#### -l / --locals-name
With `-l` or `--locals-name`, you can specify the name of the object that stores local variables in templates when not using the with statement. This option provides clarity and control over how data is accessed within your templates, improving readability and maintainability.

#### -w / --rm-whitespace
The `-w` or `--rm-whitespace` argument instructs EJS to remove all safe-to-remove whitespace from the rendered output, including leading and trailing whitespace around template tags. This can lead to smaller file sizes and cleaner output, especially for production environments.

#### -d / --debug
Using `-d` or `--debug` outputs the generated function body to the console. This feature is invaluable for debugging complex templates, as it allows developers to inspect the compiled JavaScript produced by EJS from their templates.

#### -h / --help
The `-h` or `--help` option displays a help message summarizing the available commands and options in the EJS CLI. This is a quick way to get an overview of the CLI's capabilities or to remind yourself of the syntax for less frequently used options.

#### -V/v / --version
Finally, `-V` or `--version` displays the currently installed version of EJS. This can be useful for troubleshooting, ensuring compatibility, or simply checking if an update is available.


!!! success
    :octicons-heart-fill-24:{ .heart } By leveraging these features, you can create powerful, flexible, and secure templates with EJS. Whether you're building a small project or a large web application, EJS offers the tools needed to efficiently generate dynamic HTML content.

    Great job 🤗.