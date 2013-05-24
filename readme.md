# Node-JSRender
An actively maintained wrapper for the jsrender project by @borismoore (https://github.com/BorisMoore/jsrender). Uses latest source from the jsrender project and extends functionality for easy use in Node.js.

## Install
	npm install node-jsrender

## Usage

### Loading a Template From a String
```
// Require the node module
var jsrender = require('node-jsrender');

// Load a template from string
jsrender.loadString('#myTemplate', '{{:data}}');

// Render the template with data
jsrender.render['#myTemplate']({data: 'hello'});

// Output is: "hello"
```

### Loading a Template From a File (Synchronously)
```
// Require the node module
var jsrender = require('node-jsrender');

// Load a template from ./templates/myTemplate.html
//     Contents of ./templates/myTemplate.html is: "{{:data}}"
jsrender.loadFileSync('#myTemplate', './templates/myTemplate.html');

// Render the template with data
jsrender.render['#myTemplate']({data: 'hello'});

// Output is: "hello"
```

### Loading a Template From a File (Asynchronously)
```
// Require the node module
var jsrender = require('node-jsrender');

// Load a template from ./templates/myTemplate.html
//     Contents of ./templates/myTemplate.html is: "{{:data}}"
jsrender.loadFile('#myTemplate', './templates/myTemplate.html', function (err, template) {
	if (!err) {
		// Template was loaded
		// Render the template with data
		jsrender.render['#myTemplate']({data: 'hello'});
		
		// Output is: "hello"
	} else {
		throw(err);
	}
});
```

### Referencing Other Templates From Inside Templates
In jsrender when you want to reference another template on the client-side you can use something like:

```
{{for myData tmpl="#myTemplate" /}}
```

On the server the usage is exactly the same but you just need to make sure you name your template correctly
when you load it. For instance if you use the line above with the template name "#myTemplate" then you also
need to load your template with the same name (including the hash) like so:

```
jsrender.loadString('#myTemplate', '{{:data}}');
```
or
```
jsrender.loadFileSync('#myTemplate', './templates/myTemplate.html');
```