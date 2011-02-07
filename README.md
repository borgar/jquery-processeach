# jQuery.processEach

This is a small jQuery plugin that allows you to run long running processor intensive loops without the browser interrupting the process with a "long running script" dialog.

The function's API is like jQuery's built in [`jQuery.each`](http://api.jquery.com/jQuery.each/), but with two exceptions:

1. It runs asynchronously (so you can consider the lines following it's invocation will be run "parallel" to the loop). This is similar to how `jQuery.ajax()` works.

2. It takes an additional callback that is run when the loop is exited:

        jQuery.processEach( someArray, function( index, value ){
          // return false will break the loop
        },
        function ( subject, result ) {
          // subject is the original collection being processed
          // result is the last return value from first callback
        });

    This second function passes two parameters:

    1. The original collection object (or array) being processed.
    2. The last return value from the former callback. This is mostly useful
       to check if the loop was broken out of (with `return false`).

The process is yielded every iteration if it [has passed 100ms of execution](http://www.nczonline.net/blog/2009/08/11/timed-array-processing-in-javascript/).
