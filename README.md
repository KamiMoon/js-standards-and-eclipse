# js-standards-and-eclipse

Recommended way to import a JS project into Eclipse
* Temporarily turn off build automatically, because node_modules folder is too big.
* File->New>JavaScript Project pick the option to create project from existing source.
* Under Project facets convert to JavaScript.
* In include paths add node_modules as excluded.

Install and use JSHint with Eclipse
* Website:  http://jshint.com/about/
* Configuration Options:  http://jshint.com/docs/options/
* Eclipse plugin:  http://github.eclipsesource.com/jshint-eclipse/
* JSHint File:  https://github.com/KamiMoon/js-standards-and-eclipse/blob/master/jshint/.jshintrc
* Under project properties make sure JavaScript is selected as a project facet. This will enable JavaScript tooling for Eclipse. Eclipse comes with some minimal tooling for JavaScript. JSHint will enhance the tooling further.
* Follow the instructions to install the plugin: http://github.eclipsesource.com/jshint-eclipse/install.html
* A .jshintrc file will need to be placed in the root of your project.
* Once the plugin is installed and Eclipse is restarted you will have a JSHint option on your project properties where you can configure JSHint. Configure the includes, excludes, and tell the plugin to use the .jshintrc file.

JavaScript Code Formatter
* Windows->Preferences->JavaScript->Code Style->Formatter. Import https://github.com/KamiMoon/js-standards-and-eclipse/blob/master/formatter/javascript-formatter.xml and apply these settings.
* Windows->Preferences->JavaScript->Code Style->Clean Up. Import https://github.com/KamiMoon/js-standards-and-eclipse/blob/master/formatter/javascript-cleanup.xml and apply these settings.
* Under Windows->Preferences->JavaScript->Editor->Save Actions perform the selectied actions on save:  Format Source code.  Additonal actions:  Convert control statement bodies to block, remove uncessary parentheses, remove trailing whitespaces on all lines

AngularJS Plugin
* Follow instructions here and install:  https://github.com/angelozerr/angularjs-eclipse


