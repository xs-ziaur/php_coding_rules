### Best practices for php programming

We are all good programmers and we know how to write good programs, but there are some hidden things we might have missed in the programming world. Knowing it could help us to improve our code in speed and readability. I would like to point out few tips and practices in PHP that I found useful.
    
As you know, PHP (Hypertext Preprocessor) is a widely-used, free, efficient, and versatile programming language that allows developers to create dynamic content, basically used for developing web based applications. Let’s dig a little bit deep into it to see how we can improve the way we write it. This article is meant to help PHP beginners and above, If you haven’t learned the fundamentals of PHP programming yet, take your time to learn and come back.

### 1. Avoid short PHP tags 

Short tags `(<? ?>, <?=?>)` are easy to use, but it is not always reliable, because short tags can be disabled using the `short_open_tag` ini setting and not all servers are enabled it by default. So the code written in short tags is not portable across servers unless you have access to the ini settings. Another reason to avoid short tag is it may confuse with `<?xml ?>` notation. The recommended use of the PHP tag is `<?php`
```
    <?php
    // My super portable code goes here
    ?>
```

Plus, if you are sure that your PHP version is `5.4.0` and above, you are allowed to use `<?= ?>` tag too. It is a shortcut syntax of echo and it is pretty handy to print a variable in the inline code. Since PHP `5.4.0`, this tag is made free from the `short_open_tag` ini configuration setting.

```
    <?=$myVariableToPrint?>
```

Now, push yourself hard to avoid using this tag
```
    <?
        // My code that may not work on all servers
    ?>
```

Well, in the history there are other tags are also used that are abandoned in the latest versions(PHP7+). Just listing them to add it your DONT’S list.
```
    <% %> <%=%> // ASP style tag support in PHP
    <script language="php"> </script>
```

#### 2. Avoid closing tag in PHP only files 
If your file contains only PHP code, the closing tag (?>) is optional. It is recommended to avoid closing tag because it prevents unwanted white-space or new lines being added at the end of files. That is handy to use output buffering and we will be able to add headers to the response later.

[PHP: PHP tags - Manual](https://www.php.net/manual/en/language.basic-syntax.phptags.php?source=post_page-----e43234446fd3--------------------------------)

If a file is pure PHP code, it is preferable to omit the PHP closing tag at the end of the file. This prevents…
php.net

#### 3. Code Formatting and Layout
It doesn’t matter in-terms of code execution if we didn’t format the code well. But it does matter, when another person came to read it or another team try to update it or even worst when we come back to review our own code after a long time.

Well formatted code is easier to understand and it look consistent, clean and readable. It didn’t take too much effort, you can use the automatic code formatting feature of your IDE — most of the good IDE have that option, or you take a little time to format it yourself. Read more about PSR-2: Coding Style Guide which is a coding style standard for code formatting.

[PSR-2: Coding Style Guide - PHP-FIG](http://www.php-fig.org/psr/psr-2/?source=post_page-----e43234446fd3--------------------------------)
We're a group of established PHP projects whose goal is to talk about commonalities between our projects and find ways…
www.php-fig.org

See an example of well indented code:
```
    function calculate($a, $b, $c) {
        $result = 0;
        $x = $a + $b;
        if($x >= $c){
            $result = ($a + $b) * $c;
        }else{
            $result = $a * ($b + $c);
        }
        
        return $result;
    }
```

And this is NOT, don’t do like this
```
    function calculate($a, $b, $c) { $result = 0;
    $x = $a + $b;
    if($x >= $c){
            $result = ($a + $b) * $c;  }else{
    $result = $a * ($b + $c); }
    return $result;
    }
```

4. Write Comment Code
Comments are the part of code that helps to describe what is a piece of code or a function or a class is doing. Writing comments is a good practice to let others know what you’re doing or to remind yourself what you did. You don’t want to comment every line in your code but do when you think it is necessary to understand your code later. 

These are the examples of commenting styles on PHP
```
    <?php
        echo 'Hello World 1'; // A single line comment
        echo 'Hello World 2'; # Another way to do a single line comment

        /*
        This is a multi-line comment
        Its cool when I want to write an essay about my code
        */
        echo 'Hello World 3';
```
[PHP: Comments - Manual](http://php.net/manual/en/language.basic-syntax.comments.php?source=post_page-----e43234446fd3--------------------------------)
The "one-line" comment styles only comment to the end of the line or the current block of PHP code, whichever comes… php.net

5. Choosing Names

Naming your variables, functions, or classes are important. While naming, you should consider these factors
- The name you chose should be meaningful
- The name should be in a language everybody will understand (preferably in English)
- Follow consistent naming convention
There are many naming standards with slight variations, like PSR-1: Basic Coding Standard or Zend Framework Naming Conventions. You can choose any style based on your convenience, just make sure it is consistent throughout the project. 
Mostly I use the following naming convention style
```
    ClassName
    function_name
    $variable_name
    CONSTANT_NAME
```
### Here are the list of best read about naming conventions

[PSR-1: Basic Coding Standard - PHP-FIG](http://www.php-fig.org/psr/psr-1?source=post_page-----e43234446fd3--------------------------------)
    We're a group of established PHP projects whose goal is to talk about commonalities between our projects and find ways… `www.php-fig.org`

    [Manual - Documentation - Zend Framework](http://framework.zend.com/manual/1.12/en/coding-standard.naming-conventions.html?source=post_page-----e43234446fd3--------------------------------) 
    
    Zend Framework standardizes on a class naming convention whereby the names of the classes directly map to the… `framework.zend.com`

[Naming classes, methods, functions and variables](http://programmers.stackexchange.com/questions/149303/naming-classes-methods-functions-and-variables?source=post_page-----e43234446fd3--------------------------------)
There are 3 important naming conventions: with_underscores PascalCased camelCased Other variants are not important… `programmers.stackexchange.com`

#### 6. Understanding ‘echo’

The PHP echo statement is a language construct (not exactly a function) used to output data to the screen. echo and print both do the same thing, but echo is a little faster. echo can take multiple parameters, and it is faster than concatenating strings.

For example...

`echo "Hello ", $name, "!";` is faster and neater than… `echo 'Hello ' . $name . '!';`

Also you can use expressions `echo "Sum: ", 1 + 2;` which is better than `echo 'Sum: ' . (1 + 2);`

But echo has no return value, so it cannot be used in expressions. So the following code is invalid!
```
    ($some_var) ? echo 'true' : echo 'false';
```
instead you can use like this
```
echo $some_var ? 'true' : 'false';
```

7. Using variables

It is not necessary to initialize variables in PHP however it is a good practice. Uninitialized variables will have a default value, relying on the default value may end up in unexpected results of your program. So it is recommended to initialize your variables before using them, and that will make your code much cleaner.
```
    $my_array = array();
    $my_integer = 0;
    $my_boolean = false;
    Also avoid using unwanted variable declarations. Variables cost memory, so removing unwanted variable declaration can reduce memory load. For example…
    $my_name = $data['name'];
    echo $my_name;
```
In the above code we can definitely avoid the variable $my_name, like...
echo $data['name'];

8. Use of Ternary Operators

A simple if/else statement can be changed to make use of ternary operators. It makes your code shorter, readable and saves few lines too. The usage is simple…
```
    // Usage of Ternary Operators
    $variable = (CONDITION) ? IFTRUE : IFFALSE;

    // Similar if/else condition usage in one line
    if(CONDITION) { $variable = IFTRUE; } else { $variable = IFFALSE; }
```
An example usage of ternary operators
```
    $action = (empty($_POST['action'])) ? 'default' : $_POST['action'];
    Is identical to this if/else statement
    if (empty($_POST['action'])) {
        $action = 'default';
    } else {
        $action = $_POST['action'];
    }
```
[PHP: Comparison Operatores - Manual](http://php.net/manual/en/language.operators.comparison.php?source=post_page-----e43234446fd3--------------------------------#language.operators.comparison.ternary)

9. Use of Comparison Operators

PHP have strict and loose comparison operators, the difference is strict comparison validates value and type while loose comparison only validates value. You can use any of the comparison, but to avoid unexpected program behavior, you should be very clear what you are doing.
It is not a big deal to choose, if you want to compare the value and the type go for strict comparison otherwise use loose ones.

For example, you are validating a POST value and you don’t know in which type it will come always and you only care about the value. Then go for loose comparison
```
    // Pass if $_POST['user_id'] is an integer 1234 or a string '1234'
    if($_POST['user_id'] == '1234'){ 
    echo 'Hello Special user';
    }
```

But, for example, you are validating a return value from a function and you really care the type of the return value. In the below example if you don’t use strict comparison the condition will pass if the function return ‘1’, which will be a serious flaw.
```
    // Pass only if the function IsThisAdmin() return a boolean true
    if(IsThisAdmin($_POST['user_id']) === true){
        echo 'Hello Admin';
    }
```

Another very common example for this is while using `strpos` to compare strings. Here in the below example, if you `use != for comparison`, it print output as 'string not found', which is wrong.

The reason is `strpos` return 0, which is the position of the string and the loose comparison consider 0 as false, hence the unexpected result. So the correct check is as follows...
```
    if (strpos('abcdef', 'a') !== false) {
        echo 'string found'; // Found, thanks to operator !==
    } else {
        echo 'string not found'; // Not found, thanks to operator !==
    }
```

[PHP: strpos - Manual](http://php.net/manual/en/function.strpos.php?source=post_page-----e43234446fd3--------------------------------)

10. About Strings
Let us take a look at common ways of specifying strings and its use in PHP.
Single quoted Enclosed in single quotes (') is a simple way to specify a string. It doesn't parse any special characters, but it allow escape character with a backslash (\), generally for escaping a single quotes and backslash itself in the string. So this way is ideal if you want to output a special character literally, such as \r or \n, and this method is good if you have a simple string to specify.
echo 'Hello, \n this is a newline';
// Outputs: Hello, \n this is a newline

Double quoted
Enclosed in double-quotes (") is a another way to specify a string, and PHP will interpret more escape sequences for special characters. So \n in the string really output a newline instead of literally printing it. And variables specified in the string will be parsed and replaced with its value, if available. This method is ideal if you have to specify variables or special characters in your string.
```
$name = "Dipu Raj";

echo "Hello, My name is $name";
// Outputs: Hello, My name is Dipu Raj

echo "See the first character of my name '{$name[0]}'"; 
```
// Outputs: See the first character of my name 'D'
There are many talk about performance of both string specifications. Some point out that single quoted is faster because it doesn’t include much parsing. But in my opinion both give same performance on normal use, a few parsing doesn’t make noticeable performance lack. So use any method you want as the situation demands, unless you want to do micro-optimization.
Heredoc and Nowdoc are the other complex way of specifying strings, they are not used very common. You can read more about them on PHP strings manual.

[PHP:Strings - Manual](http://php.net/manual/en/language.types.string.php?source=post_page-----e43234446fd3--------------------------------)

11. About Arrays

Array in PHP is optimized for several different uses, it can be used as an array, list, hash table, dictionary, collection, stack, queue, etc. Let’s look into some cool features of PHP Array probably don’t use commonly.

Since PHP 5.4, we get the short array syntax, which allow to use [] instead of array(). Checkout the short and regular syntax example...
```
    // Short array declaration syntax, as of PHP 5.4
    $my_array = [1, 2, 3, 4];
    $my_array_2 = ['one' => 1, 'two' => 2, 'three' => 3, 'four' => 4];

    // Regular array declaration syntax, all PHP versions
    $my_array = array(1, 2, 3, 4);
    $my_array_2 = array('one' => 1, 'two' => 2, 'three' => 3, 'four' => 4);
```

Square brackets and curly braces can be used for accessing array elements. Both line of code have same effect in the below example…
```
    echo $my_array[2];
    echo $my_array{2};
    Since PHP 5.4, we can directly access the result of a function or method as array (array dereferencing).
    <?php
    function getColors() {
        return array('red', 'blue', 'green', 'yellow');
    }

    // As of PHP 5.4
    $second_color = getColors()[1];

    // Previously it was only possible using a temporary variable
    $tmp = getColors();
    $second_color = $tmp[1];
```

The foreach loop provides an easy way to traverse an array
```
    foreach ($my_array as $key => $value)
    {
        echo 'Key: ', $key, ' Value: ', $value;
    }
```

Since PHP 5, we can manipulate array value directly by passing them by reference.
```
    // PHP 5
    foreach ($colors as &$color) {   // &$color pass by reference
        $color = strtoupper($color);
    }

    /* Make sure to unset the reference variable,
    it may affect the array value if the variable $color is modified elsewhere in the code */
    unset($color); // Unset the reference variable

    // Older versions workaround
    foreach ($colors as $key => $color) {
        $colors[$key] = strtoupper($color);
    }
```
Use quotes if you have array key as a string. It still works if you don’t, but that is not recommended. The reason is that PHP assume it as a constant if you don’t enclose in quotes, and PHP automatically converts it into a string if there is no defined constant in that name, that’s why it still works, but we are giving the compiler an extra load. Also if you already have a constant with the same name, you get weird results.
```
    echo $my_array_2['three']; // Correct
    echo $my_array_2[three]; // Wrong code
```

An in PHP is actually an ordered map. A map is a type that associates values to keys. This type is optimized for…
php.net
[PHP: array - Manual](http://php.net/manual/en/language.types.array.php?source=post_page-----e43234446fd3--------------------------------)

Happy Coding!






Resource: 
    - https://medium.com/techlaboratory/php-programming-best-practices-and-coding-styles-e43234446fd3 