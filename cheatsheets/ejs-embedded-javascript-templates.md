---
title: Java Primitive Data Types
description:
created: 2018-09-15
---

EJS - Embedded JavaScript templates is a simple templating language using which you can generate HTML. EJS does not enforce any new syntax instead you write in plain JavaScript. You can use EJS either at client side or at Server side.


#### Sample Syntax

```javascript
<% if (post.title) { %>
  <h1><%= post.title %></h1>
<% } %>
```

#### Usage - 1

```javascript
templateString = '<h1> <%= title %> </h1>';
options = {};

var template = ejs.compile(templateString, options);

var data = {
    title : 'This is the post title'
}

var outputString = template(data); // outputString -> <h1> This is the post title </h1>
```

#### Usage - 2

```javascript
var outputString = ejs.render(templateString, data, options);
```

#### Usage - 3 (Template is in a file)

```javascript
ejs.renderFile(templateFilePath, data, options, function(err, outputString){
    console.log(outputString);
});
```

## Tags

#### <% 

This is Scriptlet tag, you can write control flows under scriptlet tag, this outputs nothing

#### <%_ _%>

This is 'Whitespace Slurping' tag, this removes all whitespaces before it.


#### <%= %>

This gives HTML escaped output into template.

#### <%- %>

This gives HTML un-escaped output into template.

#### <%# %>
Comment tag


## Includes

#### include

```javascript
<%- include('path/to/another/ejs/file', data) %>
```