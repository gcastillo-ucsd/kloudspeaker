Running development version of Kloudspeaker requires installing node.js.

1. Clone Kloudspeaker git repo https://github.com/sjarvela/kloudspeaker.git.

2. Install project dependencies by running "npm install" and "bower install" in kloudspeaker root.

3. Set up local web server

* Create folder where app is published

* Copy development index.html into app web folder

* Create symbolic links from source folders to app web folder: backend, bower_components, css, fonts, localization and templates

* Create configuration.php just like in production version, and run installer


Kloudspeaker uses grunt, and following are most common tasks:

* To compile css from sass, run "grunt sass"

* To build production version, run "grunt"

See gruntfile.js for other tasks.

