# String Format

## Learning Goals

- Learn about the various ways to format a `String`

## Introduction

Sometimes we want to format a `String` a certain way. For example, we might want
to insert so many spaces between words when printing a `String` value, or we
might want to print a `boolean` value with all uppercase characters instead of
lowercase characters. Let's look at ways we can format a `String` to ensure it
will print out on the console a certain way!

## The `format()` method

The `String` class has a method to help format a `String` value called
`format()`! To help explain how to use the `format()` method, let's look at an
example:

```java
public class StringExample {
    public static void main(String[] args) {
        String bootcamp = "Flatiron School";
        
        // Concatenate two strings using the format() method
        String string1 = String.format("%s is the best!", bootcamp);
        
        System.out.println(string1);
    }
}
```

The code above will have the following output:

```plaintext
Flatiron School is the best!
```

As we can see in the example above, the `format()` method is a static method.
Remember this means it does not need a `String` instance to be called. In this
case we see the `format()` method takes in two parameters, a `String` form and
an object. In the example, the object just happens to be another `String` but
it could be an `Integer`. We may also see it has a symbol that looks like this:
`%s`. The `%` symbol flags Java to let it know that some format specifiers will
follow, like a conversion character such as `s`. **Conversion characters** are
only valid for certain data types and signal that a certain object will be
placed within the `String` at the spot where the conversion character appears.
The `%s` signals that another `String` will be placed where the `%s` appears. In
the example above, we see that the `%s` is in the beginning, and will be
replaced with the `bootcamp` value. Hence, the output "Flatiron School is the
best!" is printed to the console. It should be noted that when conversion
characters are used, the second parameter must be the correlating data type.

Here are some of the conversion characters we may see:

| Conversion Character | Data Type              |
|----------------------|------------------------|
| s                    | String                 |
| d                    | Integer                |
| f                    | Floating-Point Numbers |
| n                    | New line               |

Let's keep exploring the `format()` method with some more examples:

```java
public class StringExample {
    public static void main(String[] args) {
        String bootcamp = "Flatiron School";
        String show = "Parks and Recreation";
        
        // Concatenate two strings using the format() method
        String string1 = String.format("%s is the best!", bootcamp);
        
        // Use multiple conversion characters
        String string2 = String.format("%s has %d seasons.", show, 7);
        
        // Use a floating-point number
        String string3 = String.format("An ice cream cone costs $%f", 2.99);
        
        System.out.println(string1);
        System.out.println(string2);
        System.out.println(string3);
    }
}
```

The above will print the following output:

```plaintext
Flatiron School is the best!
Parks and Recreation has 7 seasons.
An ice cream cone costs $2.990000
```

As we can see with `string2`, we can actually have multiple conversion
characters within a `String`! When we do, we need to make sure we specify the
appropriate number of object parameters afterwards. In this example, since we
had a string conversion character and an integer conversion character, we need
to provide both a `String` and an `Integer` as parameters in the `format()`
method! Order is important, so we should always make sure that the following
object parameters are in the same order as their correlating conversion
character appears.

With `string3`, we see that we are going to print out a floating-point number,
so we use the `%f` character. Except, when we print `string3` to the console,
we get an output with more decimal values than we originally expected. We might
have only expected to see "An ice cream cone costs $2.99", but instead we see
"An ice cream cone costs $2.990000". This is because when we use the `format()`
method to print a `float`, we are printing a default of 6 decimal digits. In
order to specify how many decimal places we want, we need to adjust its
precision. To do so, we can do this:

```java
public class StringExample {
    public static void main(String[] args) {
        // Use a floating-point number with 2 decimal places
        String string3 = String.format("An ice cream cone costs $%.2f", 2.99);

        System.out.println(string3);
    }
}
```

By stating .2 prior to the conversion character, `f`, we are specifying a
**precision**. The precision will always be specified right before the
conversion character and should always be in the format `.[precision]`. In this
case, we specify a 2, therefore we should only print out to 2 decimal places
when printing the `float`:

```plaintext
An ice cream cone costs $2.99
```

Now what if we want to print some whitespace in front of a given format
specifier? We can do so by specifying the width like this:

```java
public class StringExample {
    public static void main(String[] args) {
        // Use a floating-point number with 2 decimal places and a width of 14
        String string3 = String.format("An ice cream cone costs $%14.2f", 2.99);

        System.out.println(string3);
    }
}
```

By specifying a **width**, we are saying we want the format specifier to take up
a certain amount of space. In this example, we are saying we want the "2.99" to
take up 14 spaces inclusive. Since there are 4 characters within "2.99", it will
prepend 10 spaces prior to printing the "2.99".

```plaintext
An ice cream cone costs $          2.99
```

Say, for example, we want to actually prepend "2.99" with leading zeroes instead
of spaces? We could then provide a **flag** that will fill the width:

```java
public class StringExample {
    public static void main(String[] args) {
        // Use a floating-point number with 2 decimal places and a width of 14
        // and leading zeroes
        String string3 = String.format("An ice cream cone costs $%014.2f", 2.99);

        System.out.println(string3);
    }
}
```

When we specify a flag, the flag will always come directly after the `%` and
before the width. This will now output the following:

```plaintext
An ice cream cone costs $00000000002.99
```

In conclusion, when we are using the `String` class' `format()` method, we can
use the following syntax:

```plaintext
%[flag][width][.precision]conversion-character
```

It should also be noted that the specifiers in brackets are optional. The `%`
and character conversion are required when formatting a `String`.

## The `printf()` method

We might not always want to initialize a new `String` to just format it.
Sometimes we just want to print a formatted `String` if we do not care about
holding onto how it is formatted.

This is where the `printf()` comes into play!

The `printf()` method can be used instead of a `System.out.print()` or a
`System.out.println()` to print a formatted `String` using the same formatting
rules as above!

Consider the following:

```java
public class StringExample {
    public static void main(String[] args) {
        String bootcamp = "Flatiron School";
        String show = "Parks and Recreation";
        
        // Use printf() instead of String.format()
        System.out.printf("%s is the best!%n", bootcamp);
        System.out.printf("%s has %d seasons.%n", show, 7);
        System.out.printf("An ice cream cone costs $%014.2f%n", 2.99);
    }
}
```

Notice that the same formatting rules defined above are being used here as well!
We can still make use of the conversion characters, width, precision, and flags
as we do with the `format()` method. This is an easy way to simply print to
the console a formatted `String` without initializing a separate variable. Also
note the use of `%n` to write a new line out after each of the `printf()`
statements.

This will output the following:

```plaintext
Flatiron School is the best!
Parks and Recreation has 7 seasons.
An ice cream cone costs $00000000002.99
```
