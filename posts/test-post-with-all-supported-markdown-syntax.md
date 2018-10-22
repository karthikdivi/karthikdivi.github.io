---
title: Test post with all supported markdown syntax
description: Sample post with all supported markdown syntax in the blog
tag: sample-tag
created: 2017-12-04
---

Markdown:
```
## Some example title, with h2 size
### Some example title, with h3 size
#### Smaller title, with h4 size
```
Result:

## Some example title, with h2 size
### Some example title, with h3 size
#### Smaller title, with h4 size
---
Markdown:
``````
Following is some sample javascript code.
```javascript
var i = 10
if(i>0){
    console.log('Positive');
}
```
``````
Result:
Following is some sample java code.
```javascript
var i = 10
if(i>0){
    console.log('Positive');
}
```
---
Markdown:

```
Following are some bullet points
* first point
* second point
```
Result:
Following are some bullet points
* first point
* second point
---
Markdown:

```
Following are some numbered points
1. first point
2. second point
```
Result:

Following are some numbered points
1. first point
2. second point

---
Markdown:

```
**Sample Bold data**
~~Strikethrough~~
```

Result:

**Sample Bold data**
~~Strikethrough~~

---
Markdown:
```
[This is how you put links](http://karthikdivi.com/blog)
![This is how you put images](https://static.karthikdivi.com/images/blogs/1512365970828/aa0a9c62-1938-42fe-8f78-6b05c6206e60_1.46d4a484f4d2036eab79a61f2ac75d9c.jpeg)
```
Result:

[This is how you put links](http://karthikdivi.com/blog)
![This is how you put images](https://static.karthikdivi.com/images/blogs/1512365970828/aa0a9c62-1938-42fe-8f78-6b05c6206e60_1.46d4a484f4d2036eab79a61f2ac75d9c.jpeg)

---
Markdown:
```
| column1 | column2 |
|--------|--------|
|data1|data2|
|data3|data4|
```
Result:

| column1 | column2 |
|--------|--------|
|data1|data2|
|data3|data4|

---


Markdown:
```
---
This code is between page breaks

---
```

Result: 

---
This code is between page breaks

---