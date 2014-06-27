JSErrata
========

Documentation of JavaScript Compiler/SPEC inconsistencies and other things worth mentioning.

# Improper Boolean Conversions

## Arrays

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

Additional Information: ~~TODO~~

## The Null Case

The following statements are true. Test them in the Javascript console of your choice:

  null != false
  null != true
  !null == true
  !!null == false

While null is "falsy", in it's standalone form, it will evaluate to neither true nor false.

Additional Information: ~~TODO~~

## Special Strings

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

More Info: ~~TODO~~

# Exciting Short-Hand

## Bang-Tilda

~~TODO~~

## Bitwise Division

~~TODO~~
