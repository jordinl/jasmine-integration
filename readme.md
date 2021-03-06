jasmine-integration
===================

Integration tests with jasmine. Visit [node-todo](https://github.com/jordinl/node-todo) for an example. Benefits of using this tool in a browser:

- Ability to run tests in isolation.
- Set breakpoints.
- Ability to see actual contents of the page loaded.
- Faster performance than phantomjs.


## Usage

First you need to visit a url and probably wait until the page is loaded:

````
  beforeEach(function(done) {
    page = visit("/");
    page.ready(done);
  });
````

The page object supports clicking on elements:

````
  page.click("#selector")
````

And filling in input fields:

````
  page.fill_in("#selector", "Some text");
````

Async behavior with waitFor:

````
  beforeEach(function(done) {
	page.click("button");
	page.waitFor(function() {
	  return someCondition() == true;
    }, done);
  });
````

Waiting for page changes:
````
  beforeEach(function(done) {
	page.click("button");
	page.onBodyChange(done);
  });
````

To show the contents of the page:

````
  page.show();
````

## Installation

- Install grunt cli: `npm install grunt-cli -g`

- In package.json append to your devDependencies:

	````
	"jasmine-integration": "0.0.2"
	````
- Install node modules: `npm install`
 
- Add the following to your Gruntfile:

	````
	grunt.loadNpmTasks('jasmine-integration');
	````

## Basic setup for jasmine

Assuming test files are called *Spec.js and the app is a node app. Add the following to config/jasmine.yml

````
spec_files:
  - "**/*[Ss]pec.{js,coffee}"

application_port: 8080

server_command: "node server.js"
````

## Running tests

- To run tests in the browser `grunt jasmine:server`

- To run tests in headless mode `grunt jasmine:server:ci`