# JSErrata

Documentation of JavaScript Compiler/SPEC inconsistencies and other things worth mentioning.

## Improper Boolean Conversions

### Arrays

The following statements are true.  Test them in the Javascript console of your choice:

      [] == false
      ![] == false
      [] == ![]
      !![] == true

Furthermore, so long as an array contains a single element which will evaluate to false, it will continue to evaluate to false in a way similar to the above.

      [null] == false
      [false] == false
      [""] == false
      [[[[null]]]] == false

Additional Information: This appears to be due to loose type conversions.  When evaluating on an array, the contents are cast to string.  Without multiple elements in an array, there are no commas to make the result truthy.  And so, the inner most value is evaluated for truthiness.

### The Null Case

The following statements are true. Test them in the Javascript console of your choice:

      null != false
      null != true
      !null == true
      !!null == false

While null is "falsy", in it's standalone form, it will evaluate to neither true nor false.

Additional Information: ~~TODO~~

### Special Strings

The following statement are true. Test them in the Javascript console of your choice:

      "longstring" != false
      "longstring" != true
      !!"longstring" == true
    
      "true" != true
      "true" != false
      "false" != true
      "false" != false
    
      "1" == true
      "0" == false
    
      "" == false

While emptry strings will evaluate to false, any non-empty string that is not "1" or "0" will evaluate to neither true nor false, though they are techinically truthy.

More Info: Don't use loose inequalities when comparing with true or false.

## Exciting Short-Hand

### Bang-Tilde

Bit-wise and boolean not operators can be combined to quickly compare values to -1.

      !~-1 === true
      !~0 === false
      !~1 === false

This is due to the nature of bitwise not operators.

      ~1 === 0
      ~(any other int) !== 0
   
      !0 === true

### Bitwise Division

~~TODO~~

## Unexpected Results

### Non-Atomic Evaluation

      var x = 0;
      
      function f() {
            x = x + 10;
            return 1;
      }
      
      x += f(); // x === 1

The preceding code, if executed will result in `x = 1`. This is a combination of shorthand and typical left-to-right evaluation. `x += f()` is just shorthand for `x = x + f()`. Because the expression `x + f()` is evaluated left-to-right, the interpreter will first obtain the value of the first operand, `x`, which is zero, and then obtain the value of the second operand, `f()`, which is one. Changes to `x` that happen inside `f()` don't affect the collected operand values.

Based on an [article about non-atomic operations in C#](http://blogs.msdn.com/b/oldnewthing/archive/2014/08/14/10549885.aspx)
