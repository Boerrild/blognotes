AngularJS
=========


# Angular UI Bootstrap directives

When using an angular ui directives for bootstrap, like popover, be aware that 
the directive usually adds a new context, which implies that the model of your 
target controller now needs to be referenced using '$parent', eg. :

    <select ng-model="$parent.myModel" popover="Filter by operational service" ... ></select>


# Loading-indicator and interpolation of a promise

Here's a neat little trick I use when showing a value that is being resolved as a promise:

JS:  
    $scope.myDefferedValue = somePromise(...);    

HTML:

    <p>{{!myDefferedValue.$resolved ? 'loading...' : myDefferedValue.somePropertyToShow}}</p>


