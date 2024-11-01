---
layout: syllabus_page
course: ruby
title: File Handling in Ruby language
date: 7th Sept, 2020 22:00:00
parent: /ruby/section-two/
tags:
 - file
description: File Handling in Ruby language
permalink: /ruby/section-three/file-handling/
prev_link: /ruby/section-three/module/
comments: true
---

# File Handling in Ruby

Working with files is an essential part of software development, as sometimes one needs to write some important information to a file and read it later.

Ruby provides many different ways to work with files.

Let's first check the number of supported file modes.

| Mode | Description |
| -- | -- |
| `r` | Read only mode. File pointer is positioned at start of file. |
| `r+` | Read and write mode. File pointer is positioned at start of file. |
| `w` | Write only mode. File pointer is positioned at start of file. |
| `w+` | Read and write mode. File pointer is positioned at start of file. |
| `a` | Append mode. File pointer is at end of file. Append the data if file exists else create a new file. |
| `a+` | Read and append mode. File pointer is at end of file. Append the data if file exists else create a new file. |

## Opening a file

If you want to open an existing file for reading, then it can be done in following way:

```ruby
file_object = File.open("some_file.txt")  # read mode('r') is default
# use file_object for processing

file_object = File.open("some_file.txt", "w+")  # read mode('r') is default
```

## Creating a file

We can create a new file using `File.new()` method for reading, writing, or, for both, as per the `r+`, or `a+` mode mentioned above.
Also, we need to use `file_object.close()` method to close that file so that system resources can be released.

```ruby
file_object = File.new("new_file.txt", "w")
# use file_object for processing
```

## Write to a file

To write content to the file, we can use `file_object.syswrite()` method. The file should be opened in write mode for this method.

```ruby
file_object.syswrite("content");

# or
file_object.write("content");

# or
file_object.puts("content");
```

__NOTE:__ The methods `write` and `puts` will write the content to the buffer, while `syswrite` will directly write to the disk.
The method `puts` will add a newline, unless there is already a newline character at the end of the content, after the content while `write` and `syswrite` just write the specified content only.
The addition of a newline character acts the same as when we use it for an instance of `String`.

## Closing the file

It is important to close the file handle after the required operations are done.
It will help to release the resources like memory to be released for other purposes.

```ruby
file_object.close()
```

## Example

```ruby
file = File.new("foo.txt", "w")
file.syswrite "this is first line\n"
file.close

file = File.open("foo.txt", "w")
file.syswrite "this is second line\n"
file.close

file = File.open("foo.txt", "w+")
file.syswrite "this is third line\n"
file.close

file = File.open("foo.txt", "a")
file.puts "this is fourth line"
file.close

file = File.open("foo.txt", "a+")
file.puts "this is fifth line"
file.close

# output
this is third line
this is fourth line
this is fifth line
```

__NOTE:__ Notice above that the file has been overwritten on mode `w` and `w+`.

## Using a block

It is recommended to use block style while reading and writing files as it handles closing the file for you when the block is finished executing.

```ruby
File.open("some_file.txt", "w") do |file|
  file.puts "some content"
end
```

## File reading variants

A file can be read in many different ways.
We will see few reading options we have in Ruby.

In the following examples, we will consider a file named `foo.txt` with following content:

```text
this is first line
this is second line
this is third line
```

### Read at once

We can read the whole file at once.

```ruby
# let's say some_file.txt has "some content as file content"
File.open("foo.txt", "r") do |file|
  puts file.read
end

# output
this is first line
this is second line
this is third line
```

### Read line by line using File#readlines

We can read the file content line by line through `FILE#readlines` method too.
In such case, each line of the file will be treated like an element in the array.

```ruby
FILE.readlines('foo.txt').each do |line|
  puts line
end

# output
this is first line
this is second line
this is third line
```

### Read line by line using IO#readlines

We can read the file content line by line through `IO#readlines` method too.
In such case, each line of the file will be treated like an element in the array.

```ruby
IO.readlines('foo.txt').each do |line|
  puts line
end

# output
this is first line
this is second line
this is third line
```

### Read line by line using IO#foreach

We can read the file content line by line through `IO#foreach` method, too.
The difference between the method `foreach` and the method `readlines` is that the method `foreach` is yielding each line from the block.

```ruby
IO.foreach('foo.txt') do |line|
  puts line
end

# output
this is first line
this is second line
this is third line
```

## Getting Information about File

Sometimes it is necessary to find information about a file before performing any operations.
Ruby provides many different methods for this very purpose.

We will see few common methods below:

- To see if a file already exists or not

  ```ruby
  File.exists?("foo.txt") # return true of false
  ```

- Check whether a file is a file or directory

  ```ruby
  File.file?("foo.txt") # true
  File.directory?("some_directory") # true
  ```

- Check whether a file is readable, writable or executable?

  ```ruby
  File.readable?("foo.txt") # true

  File.writable?("foo.txt") # true

  File.executable?("foo.txt") # false
  ```

- Check size of a file

  ```ruby
  File.size("foo.txt") # 58
  ```

- Check if a file is empty or not

  ```ruby
  File.zero?("foo.txt") # false
  ```

- Find the extension of a file

  ```ruby
  File.extname("foo.txt") # .txt
  ```

You can find all of the file related methods in [File official documentation](https://ruby-doc.org/core-3.2.2/File.html){:target="_blank"}.
