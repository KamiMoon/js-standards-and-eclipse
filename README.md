# js-standards-and-eclipse

Just having a W3Schools understanding of JavaScript is not enough.

"JavaScript is the only language people feel like they don't need to learn to use."- Douglas Crockford

I would recommend anything written by Douglas Crockford (http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742), but to get people up to speed here is a quick list of the most important and hardest things for most developers to grasp when dealing with JavaScript. JSHint will automatically detect most of these issues as well.

Also a good link: http://jstherightway.org/

Falsey Values
JavaScript is dynamically typed and these will evaluate as false while everything else is true:
false (boolean)
0 (zero)
"" (empty string)
null (assigned by programmer)
undefined (automatically assigned by JavaScript)
NaN (Not a Number, a result of some bad math or operation)
All variables are assigned to undefined by default. If a variable is declared like this:




# Recommended way to import a JS project into Eclipse
* Temporarily turn off build automatically, because node_modules folder is too big.
* File->New>JavaScript Project pick the option to create project from existing source.
* Under Project facets convert to JavaScript.
* In include paths add node_modules as excluded.

# Install and use JSHint with Eclipse
* Website:  http://jshint.com/about/
* Configuration Options:  http://jshint.com/docs/options/
* Eclipse plugin:  http://github.eclipsesource.com/jshint-eclipse/
* JSHint File:  https://github.com/KamiMoon/js-standards-and-eclipse/blob/master/jshint/.jshintrc
* Under project properties make sure JavaScript is selected as a project facet. This will enable JavaScript tooling for Eclipse. Eclipse comes with some minimal tooling for JavaScript. JSHint will enhance the tooling further.
* Follow the instructions to install the plugin: http://github.eclipsesource.com/jshint-eclipse/install.html
* A .jshintrc file will need to be placed in the root of your project.
* Once the plugin is installed and Eclipse is restarted you will have a JSHint option on your project properties where you can configure JSHint. Configure the includes, excludes, and tell the plugin to use the .jshintrc file.

# JavaScript Code Formatter
* Windows->Preferences->JavaScript->Code Style->Formatter. Import https://github.com/KamiMoon/js-standards-and-eclipse/blob/master/formatter/javascript-formatter.xml and apply these settings.
* Windows->Preferences->JavaScript->Code Style->Clean Up. Import https://github.com/KamiMoon/js-standards-and-eclipse/blob/master/formatter/javascript-cleanup.xml and apply these settings.
* Under Windows->Preferences->JavaScript->Editor->Save Actions perform the selectied actions on save:  Format Source code.  Additonal actions:  Convert control statement bodies to block, remove uncessary parentheses, remove trailing whitespaces on all lines

# AngularJS Plugin
* Follow instructions here and install:  https://github.com/angelozerr/angularjs-eclipse


