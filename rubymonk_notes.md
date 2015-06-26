# RubyMonk Notes

## Objects

* Everything is an object.
* If you don't specify an object, `self` refers to `main`.
* The response to invoking a method on an object is *always* another object.
* Calling `methods` on an object lists the methods that object responds to.


## Strings

* Any valid block of Ruby code placed inside `#{}` will be evaluated and inserted at that location.
* A String literal created with single quotes does not support interpolation.
* Double quotes allow for escape sequences while single quotes do not.
* Convention to use '?' at the end of a method if that method returns only boolean values.
* You can use '<<' just like '+', but in this case the String object 'Monk' will be appended to the object represented by 'Ruby' itself. In the first case of using '+', the original string is not modified, as a third string 'RubyMonk' is created. This can make a huge difference in your memory utilization, if you are doing really large scale string manipulations.
* `sub` replaces the first occurence of the search term, `gsub` replaces all occurences.
* In Ruby you specify a RegEx by putting it between a pair of forward slashes (/).


## Conditions and Loops

    if #condition
      #do something
    elsif #condition
      #do something
    else
      #do something
    end

* `unless x` is equivalent to `if !x`.
* The objects `false` and `nil` equates to false. Every other object like say `1`, `0`, `""` are all evaluated to be `true`.


## Arrays

* Arrays in Ruby allow you to store any kind of objects in any combination with no restrictions on type.
* The n<sup>th</sup> value in an array has an index of n-1.
* Array indexes using negative numbers is called reverse index lookup. The values of the index start at -1.
* `<<` is the append function.
* The `map` method is used to transform the contents of an array according to a specified set of rules defined inside the code block. `[1, 2, 3, 4, 5].map { |i| i + 1 }`
* Ruby aliases the method `Array#map` to `Array#collect`; they can be used interchangeably.
* The `select` method filters elements in a collection according to a boolean expression.
* The `delete_if` method deletes elements in a collection according to a boolean expression.
* `for` loops are hardly used in Ruby, `Array#each` and its siblings are the de facto standard.


## Hashes

* A blank hash can be declared using two curly braces `{}`.
* You can use `each` to iterate over the elements in a Hash. However, there are 2 values passed to the block: the key and value of each element.


## Classes

* You can look up the class of any object by calling the `class` method.
* Using `is_a?` asks whether an object is a particular class.
* Classes are objects that belong to the class `Class`.
* Classes act as the factories that build objects.
* An object built by a class is called 'an instance of that class'. Calling `new` on a class results in an instance being created.
* For a class to justify its existence, it needs to have two distinct features: state and behavior.
* `@` symbol designates variables as instance variables of a class.


## Methods

* A method is simply something one object can do for another.
* The data an object contains is what it *is* and its methods are what it can *do*.
* The `method` method will return an object's method as an object. (whoa...) That object can then be called as a method using the `call` method.
* Ruby doesn't allow spaces in method names.
* As a convention, method names are in lowercase.
* If no `return` keyword is specified, the object created by the last line in the method is automatically treated as the return value.
* A method must *always* return exactly one object.
* Calling `return` exits the method at that point.
* Calling `return` without specifying an object to return results in a `nil`.
* As someone using a method, you don't usually care about how it works, just that it does. 
* As the author of the method, you're free to change its internal implementation so long as it continues producing the same result.
* Method params can have default values: `def add(a_number, another_number = 0)`
* The splat operator `*` is used to handle methods which have a variable parameter list.
* The splat operator works both ways - you can use it to convert arrays to parameter lists as easily as we just converted a parameter list to an array.


## Lambdas and Blocks

* A lambda is just a function without a name.
* Lambdas are objects, just like everything else.
* Lambdas take parameters by surrounding them with pipes.
* Use `{}` for single line lambdas and `do..end` for lambdas that are longer than a single line.
* A block is a piece of code that *can't* be stored in a variable and isn't an object. One of the rare instances where Ruby's "everything is an object" rule is broken.
* The `yield` keyword can call a *single* lambda that has been *implicitly* passed to a method without using the parameter list.


## Modules

* Modules only hold behavior, unlike classes, which hold both behavior *and* state.
* Since a module cannot be instantiated, there is no way for its methods to be called directly.
* To include a module in a class, use the method `include` which takes one parameter - the name of a `Module`.
* All modules are instances of `Module`.
* `Module` is the superclass of `Class`, so this means that all classes are also modules, and can be used as such.
* Namespacing is a way of bundling logically related objects together.
* `::` is a constant lookup operator that looks up the `Array` constant only in the `Perimeter` module.
* When creating libraries with Ruby, it is good practice to namespace your code under the name of your library or project.
* If you prepend a constant with `::` without a parent, the scoping happens on the topmost level.


## Streams

* An input/output stream is a sequence of data bytes that are accessed sequentially or randomly.
* Ruby defines constants `STDOUT`, `STDIN` and `STDERR` that are `IO` objects pointing to your program's input, output and error streams that you can use through your terminal, without opening any new files.
* Whenever you call `puts`, the output is sent to the `IO` object that `STDOUT` points to. It is the same for `gets`, where the input is captured by the `IO` object for `STDIN` and the `warn` method which directs to `STDERR`.
* The `Kernel` module provides us with global variables `$stdout`, `$stdin` and `$stderr` as well, which point to the same `IO` objects that the constants `STDOUT`, `STDIN` and `STDERR` point to.
* Whenever you call `puts`, you're actually calling `Kernel.puts` (methods in `Kernel` are accessible everywhere in Ruby), which in turn calls `$stdout.puts`.
* The purpose of these global variables is temporary redirection: you can assign these global variables to another `IO` object and pick up an IO stream other than the one that it is linked to by default.
* `w` is write mode. `r+` is read-write mode.
* `File#rewind` is necessary because Ruby keeps track of your position when reading from a `File` object.
* `File#seek` lets you seek to a particular byte in the file to start reading from.
* `File#readlines` returns an array of all the lines of the opened IO stream.
* Use `File#write` to write a string to a file.
