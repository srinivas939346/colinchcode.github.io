---
layout: post
title: "[python] Dynamic typing in dynamically typed languages other than Python"
description: " "
date: 2023-10-26
tags: [python]
comments: true
share: true
---

# Ruby:
Ruby is another popular dynamically typed language that follows the "duck typing" principle. In Ruby, variables can hold different types of objects, and their behavior is determined by the methods they respond to, rather than their specific type. This allows for greater flexibility and ease of programming.

```ruby
def greet(name)
  puts "Hello, #{name}!"
end

greet("John")     # Output: Hello, John!
greet(123)        # Output: Hello, 123!
greet([1, 2, 3])  # Output: Hello, [1, 2, 3]!
```

# JavaScript:
JavaScript is a dynamically typed scripting language commonly used for web development. Similar to Python, JavaScript variables can hold any type of data, and their type can change during execution.

```javascript
let greeting = "Hello";
console.log(greeting);  // Output: Hello

greeting = 123;
console.log(greeting);  // Output: 123

greeting = [1, 2, 3];
console.log(greeting);  // Output: [1, 2, 3]
```

# PHP:
PHP, a widely used web development language, also supports dynamic typing. PHP variables are loosely typed and can hold any type of data. The type of a variable is determined by the value assigned to it.

```php
$greeting = "Hello";
echo $greeting;  // Output: Hello

$greeting = 123;
echo $greeting;  // Output: 123

$greeting = [1, 2, 3];
echo $greeting;  // Output: Array
```

Dynamic typing allows for increased flexibility and faster development as programmers can easily change the type of a variable without having to declare it explicitly. However, it also introduces the possibility of runtime errors if not used carefully. It's important to handle type conversions and ensure that variables are used appropriately in dynamically typed languages.