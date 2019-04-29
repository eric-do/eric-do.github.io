---
layout: post
title: "React Gotchas"
comments: true
---
## Setup: file structure
1. Create folders: src/components, src/data, src/styles
2. Create index files: src/index.js ./index.html
3. Create package.json: make sure to include react, react-dom, jquery, babel, etc
4. Index.html: dependencies like jquery and styles go in the header, component js files go at the end of body

## Setup: run
```
babel . --out-dir compiled --presets=react --ignore=node_modules,compiled --source-maps inline --watch
```
```
live-server
```


## Gotcha moments during coding
### Class names
React requires 'className' rather than 'class' for HTML tags.
```
 <div className="navbar">MovieList</div>
```

### HTML tags
Tags should be closed off JSX style if they do not have a corresponding separate closing tag.
```javascript
 <input type="submit" value="Go!" className="submit" />
```

### Event handlers
Event handlers require function definitions, not function invokations.
```javascript
<input type="submit" value="Go!" className="submit" onClick={(e) => props.submitHandler(e)}/>
```

Also, what's the difference between the line above and this one? Both produce the same event in submitHandler:
```javascript
<input type="submit" value="Go!" className="submit" onClick={props.submitHandler}/>
```

Event handlers must be passed down as props, referencing **this**.
```javascript
 <Search submitHandler={this.submitHandler.bind(this)}/>
```
### Inline styles
Inline styles are not done in HTML style. Differences:
* Style is an object rather than a string of key/value pairs
* Attributes should be camelCase rather than snake-case
* Values are strings

```javascript
<div id="no-results" style={props.found === true ? {display: "none"} : {}}>
```

### Exports
* Make sure component files are being exported
* Make sure component files are being imported **and** using the intended import name

### Using brackets in one liners

```javascript
{
  props.movies.map(movie => {
    <MovieEntry movie={movie} />
  }) 
}
```

instead of

```javascript
{
  props.movies.map(movie => (
    <MovieEntry movie={movie} />
  )) 
}
```