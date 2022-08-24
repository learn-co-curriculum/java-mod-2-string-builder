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
case we see the `format()` method takes in two parameters, a `String` that we
want to format and the objects we want to inject into the `String`. In the
example, the object just happens to be another `String` but it could be an
`Integer` or a `Float`. We also see in the `String` that we want to format a
character that looks like this: `%s`. The `%` tells Java that some format
specifiers will follow and be placed here. The `s` that follows the `%` is a
conversion character. **Conversion characters** are only valid for certain data
types and signal that a certain object will be placed within the `String` at the
spot where the conversion character appears. Therefore, the `%s` says that
another `String` will be placed where the `%s` appears. In the example above, we
see that the `%s` is in the beginning, and will be replaced with the `bootcamp`
value. Hence, the output "Flatiron School is the best!" is printed to the
console. It should be noted that when conversion characters are used, the second
parameter must be the correlating data type.

Here are some of the conversion characters we may see:

| Conversion Character | Data Type              |
|----------------------|------------------------|
| s                    | String                 |
| d                    | Integer                |
| f                    | Floating-Point Numbers |
| n                    | New line               |

### Formatting Rules

When we want to format a `String`, we can use the following syntax:

```plaintext
%[flag][width][.precision]conversion-character
```

To break down the syntax some more:

- The **flag** format specifier contains a set of characters to specify the
  format of the output. The character set very much depends on the data type
  that is to be formatted.
- The **width** specifier specifies the amount of characters we want to output
  when formatting the value.
- The **precision** specifier is usually used when the data type we are
  formatting is a `Float` and specifies how many decimal values should be
  printed.
- Notice that the flat, width, and precision format specifiers are in brackets.
  These specifiers are optional whereas the `%` and the conversion character are
  required when formatting a `String`.

Let's explore these other optional specifiers some more with some examples:

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

Here, we are using the precision format specifier to specify we want to display
only a specific amount of decimal places. The precision format specifier always
starts with a dot `.` and can then be followed by the number of decimal places.
In this case, we specify a 2, therefore we should only print out to 2 decimal
places when printing the `float`:

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

By specifying a width, we are saying we want the output to take up a certain
amount of space. In this example, we are saying we want the "2.99" to take up 14
characters worth of space. Since there are 4 characters within "2.99", it will
prepend 10 spaces prior to printing the "2.99".

```plaintext
An ice cream cone costs $          2.99
```

Cool! So we have seen the precision and width format specifiers, but what about
the flag specifier? Let's say we want to actually prepend "2.99" with leading
zeroes now instead of spaces. This is where we can specify a flag with `0` to
pad the output with zeroes:

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

This will now output the following:

```plaintext
An ice cream cone costs $00000000002.99
```

Some other flags include the following:

| Flags | Description                                      |
|-------|--------------------------------------------------|
| -     | Print the value left-justified                   |
| +     | Print the sign of the number (positive/negative) |
| 0     | Print the number with leading zeroes             |

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
