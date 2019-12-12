# How it works

## Python side

```python
import google.colab.output

def some_function(*args, **kwargs):
    #your code
    
google.colab.output.register_callback('js_callback', some_function)
```

## JS side

```javascript
var kernel = google.colab.kernel;
var resultPromise = kernel.invokeFunction("js_callback",
                                          [arg1,arg2],
                                          {kwarg1: 1, kwarg2: 2}); //returns a Promise
resultPromise.then(
    function(value) {
      console.log(value); //go figure what it returns in console
    }, function(value) {
      console.log(value); //no idea what's gonna happen here
    });
```

Python errors returned to the JS will show up in console.
