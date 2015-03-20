![ngContentEditable](https://raw.githubusercontent.com/cathalsurfs/ng-contenteditable/master/demo/img/logo.png)

=====================
##ngContentEditable##

###Native contenteditable directive for AngularJS###

An easy to use, somewhat experimental, directive to enable rich text editing for users, within the browser window. This directive has no dependency on other frameworks. It does require a browser that supports both HTML5 contenteditable and HTML5 drag/drop events.

[Live Demo](http://inchsurf.com/ng-contenteditable/)

The available demo requires jQuery and Bootstrap 3 (because I just wanted to put something together quick).

[Documentation](https://github.com/cathalsurfs/ng-contenteditable/wiki) (TODO)

[Reference](https://github.com/cathalsurfs/ng-contenteditable/blob/master/demo/js/app.js) (see code comments)

[Tests](https://github.com/cathalsurfs/ng-contenteditable/tree/master/test) (see notes below)

##Requirements##

###Firefox###

Due to the experimental nature of this extension, it is __strongly__ advised to use the [Foxy](https://getfirefox.com) browser, at this time.

Results with other browsers may vary, due to funky implementations for range selection in browsers than don't do things sensibly or as expected (Chrome, quite often). If you want to lose your sanity, go ahead and implement support for IE - although things should be good to go in IE 10 (not tested). Wider support is planned.

#Directives#

##editable##

Directive declaration style is by class, by adding the "editable" class name to any elements you wish to enable with this extension. Provides native drag and drop functionality to editable regions (including reads from local file system). Provides two-way binding on contenteditable elements. 

Example:

	<div class="editable" data-ng-model="your.data.model">Some default static content...</div>

If your model data is not available, ngContentEditable will default to whatever static content you have contained within your element. This is handy, when for example you are mocking up a web page, or you want to publish with initial static content the user can later modify. Subsequent changes can update to your model.

####Scope####

Any directives which are placed within an editable region (either implicitly or by user drag drop interaction), will be compiled dynamically. These directives will have access to the following property (as long as they are not defined with isolate scope):

__$isNgContentEditable__ (Boolean)

You can access this property to determine if your directive is effectively in "editable mode". In this case, you can define logic for specific behaviors.

##editable-component##

Directive declaration style is by class, by adding the "editable-component" class name to any elements / directives for which you want to __preserve__ scope. Note - preservation of scope may not be completely reliable. For example, where the user selects a range which encompasses any editable-component directives, any subsequent drag event is cancelled for safety.

##editable-control##

Directive declaration style is by class, by adding the "editable-control" class name to any elements you wish to function as a command / button within your web page or application.

#Services#

##editable.dragHelperService##

Main thing here is the following method:

###registerDropHandler(options)###

Method provides mechanism to register (from within your own associated directives) a drop handler for editable elements.

Takes the following options object as its only argument:

	{
		tag: String, 			// Name of tag (e.g. 'img')
		types: [], 				// Array of strings, for each mime type you want to accept (e.g. ['image/jpeg', 'image/png', 'image/gif'])
		node: angular.element 	// Wrapped element which is inserted into editable region (DOM) during uploading phase, if any are associated with this type, for positive user feedback.
		format: Function 		// Callback function which passes single argument (data) to allow manipulation of inserted element on uploading phase completion (e.g. uploaded image final display).
	}

##Other##

Other services which are available, but primarily for internal use (required) are:

__editable.utilityService__ (required by all)

__editable.configService__ (required by editable directive)

__editable.rangeHelperService__ (required by editable directive)

__editable.commandHelperService__ (required by editable-control directive)

##Tests##

Sorry, tests are a bit sparse at the moment. For now, I've made available some basic sanity testing and testing around validation of two-way data binding on editable regions. Also, a little bit of range / selection interaction with editable regions, for good measure (for now).

[Tests](https://github.com/cathalsurfs/ng-contenteditable/tree/master/test)

I will decide if implementing more robust cross-browser support is of greater initial value, than launching into simulation of user interactions for HTML5 drag and drop, range selection etc.
