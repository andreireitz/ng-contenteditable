ng-contenteditable
==================

#Native contenteditable directive for AngularJS#

An easy to use, somewhat experimental, directive to enable rich text editing for users, within the browser window. This directive has no dependency other frameworks. It does require a browser that supports both HTML5 contenteditable and HTML5 drag/drop events.

[Live Demo](http://inchsurf.com/ng-contenteditable/)

The available demo is requires jQuery and Bootstrap 3 (because I just wanted to put something together quick).

[Documentation](https://github.com/cathalsurfs/ng-contenteditable/wiki) (TODO)

##Requirements##

#####Firefox#####

Due to the experimental nature, it is strongly advised to use the __Foxy__ browser:

[Firefox](https://getfirefox.com)

Results with other browsers may vary, due to incomplete range selection support for browsers than don't do things in a sensible manner (Chrome, quite often). If you want to lose your sanity, go ahead and implement support for IE - although things should be good in IE 10 (not tested).

#Directives#

##editable##

Directive declaration style is by class, by adding the "editable" class name to any elements you wish to enable with this extension. Provides two-way binding on contenteditable elements. 

Example:

	<div class="editable" data-ng-model="your.data.model">Some default static content...</div>

If your model data is not available, ngContentEditable will default to whatever static content you have contained within your element.

##editable-control##

Directive declaration style is by class, by adding the "editable-control" class name to any elements you wish to function as a command / button within your web page or application.

#Services#

##editable.dragHelperService##

Main thing here is the following method:

###registerDropHandler(options)###

Method provides mechanism to register (withing your own directives) drop handler for editable elements.

Takes the following options object as only argument:

	{
		tag: string, 			// Name of tag (e.g. 'img')
		types: [], 				// Array of strings, for each mime type you want to accept (e.g. ['image/jpeg', 'image/png', 'image/gif'])
		node: angular.element 	// Wrapped element which is inserted into editable region (DOM) during uploading phase, if any are associated with this type, for positive user feedback.
		format: function 		// Callback function which passes single argument (data) to allow manipulation of inserted element on uploading phase completion (e.g. uploaded image final display).
	}

##Other##

Other services which are available, but primarily for internal use (required) are:

editable.utilityService (required by all)
editable.configService (required by editable directive)
editable.rangeHelperService (required by editable directive)
editable.commandHelperService (required by editable-control directive)
