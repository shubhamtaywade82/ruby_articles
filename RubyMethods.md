# Methods in Ruby (types and naming conventions)

Hi!

# Methods

Methods are the collection of executable statements enclosed in block with a name

```ruby
  def method_name
    ..... some code
    ..... some more code
  end
```

We use them remove the redundant code we might write at different parts of our code. Without methods we would have to copy and paste the same code in the places we need them repeatedly.

It is obvious that the method **name** gives hints about what they are going to perform. Unclear, hazy or non-relatable method name can confuse any naive or even a developer who will be using that method for their code. Confusions may lead to headaches for other developers and also bugs in our code

Lets see some techniques to avoid these thing from happening in your code.

Before diving into the methods naming conventions and guidelines lets see some aspects of the methods

* Well indented method contents
* Follow the programming language guidelines then override these with the organizations guidelines
* functions or methods are short and to the point
* one method performs one task or action
* maintain consistency or the convention used to the scope of the entire codebase(eg. using single quote vs double quotes)



## Naming Convention

At First Ruby has its default method naming conventions i.e. the names should be combination of `lowercase letters` and `snake_case` to join two or more words in the method name eg. `downcase`, `get_median`, `confirm_account`, etc.

```ruby
def account_information
  # code to display account information
end
```

Ruby do not restrict the length of the method name but we must always keep the name between 3 characters to maximum 30 or 60 characters so that they are easy for the developer or the user to understand the purpose of the method in one glance.

## Use verbs

- Methods are the doers your application, a method `authenticate` in any application will perform an action of authenticating the user by sending an confirmation to the user's email to verify that the action is performed by the valid user or not
- Since methods are performing some actions in the application we should name them as verbs (verbs are the words that show actions like sing, ran, eat, write, delete etc)
- Method names should be a verb or verb phrase ,like - `pay_bill`, `remove_product`, `delete_item` or `save`
- Our Application is a Book and the code is the lines and content of the book.Code we write should look like a phrase or an sentence that we read in a book.

- accessor for attributes should be named as per their `title` for eg attributes of the bike are engine_size, stroke, fuel_type, mileage, etc
- To define their accessor ruby has the method like `attr_accessor, attr_writer, and attr_reader` but in some exceptional cases if we want to define some accessors manually
- Suppose for the mileage, we should use the name itself for defing there getters and setters.

```ruby
# bad name (donot use the set prefix for setter method name)
def set_milage(value)
  @mileage = value
end

# bad name (donot user the get prefix for getter method name)
def get_mileage
  @mileage
end

# good example
# append = sign in front of the method name to recognize this method as setter
# ruby gives sugar coating for this method name we can use it as
def milage=(value)
  @milage = value
end
# the above method can be invoked as
# mileage=(value)
# this can be simply written as
# mileage= value
# and ruby allows us to write this also as
# milege = value
# the space between the method name and the = sign is consided void and the argument  is placed after the = space

# good example for getter method
def mileage
  @mileage
end
# by default a ruby method returns the last statement so here the @mileage is returned and then can be invoked and assigned to any variable or used for comparison (or any thing just like an variable)

variable = mileage
or
if mileage > 70
  puts "Efficient for on city roads"
else
  puts "not efficient for city roads"
end
```

Verbs

- If we are conveying this information to any one we wont be saying "I am **money** the customers account" it is confusing an not correct as well.
- Here we are using the noun instead of verb
- If we say "i am going to **deposit** money in the bank" will make sense
- deposit is or verb in this context

```ruby
class Account
  def initialize(customer)
    @customer = customer
  end

  # Bad method
  def money(amount)
    @customer.balance += amount
  end
end
```

- Now change this method name to depsite

```ruby
class Account
  def initialize(customer)
    @customer = customer
  end

  # Good method
  def deposit(amount)
    @customer.balance += amount
  end
end
```

- the word deposit tells the reader that the action it will perform is to deposit amount in the bank account and it will add into the balance.

## Return values

- This is another way to choose the method name by the data type returned by it, If the method is returning a boolean value (true or false) then we should append the method name with a question mark (?).

```ruby
def equal?(number_one, number_two)
  number_one == number_two
end

# calling this method equal?(5, 6) => false
# calling this method equal?(5, 5) => true
```

This will suggest that the value returned by the method is a boolean value an nothing else

```ruby
def confirmed?
  !!self.confirmed_at
end
```

We can also use a linking verb instead of a question mark

```
def is_confirmed
  !!self.confirmed_at
end
```
This is also readable. but Ruby conventions asks to use the ? instead of the linking verbs

This method checks whether the current user confirmed_at attribute is nil or has any value in it, if there is a value this method will return `true` else if the attribute is `nil` then the method will return `false`
This gives the the person who is reading your method a hint that the method is returning a true or false value here(confirmed or not)

- If a method is returning a new value without changing the state of the object or editing the original object then this type of method should be named as the values title eg:  'email', 'name', 'address' etc.

## Methods that are Dangerous

Methods that change the state of the object they are invoked on.

- These methods are unique methods that change the data of the object (the state of the object itself)
- Appending these methods hint the reader of your code that this method is **dangerous** , and the effects of, or actions performed but these methods are **irreversible**
- If we define method that changes the data or state of the object upon calling this method on the object then mark them with an exclamation point to avoid confusion.
- They are also available in the ruby built in library eg: sort!, delete! etc

```ruby
def User
  attr_accessor :followers

  def un_follow!(follower)
    @followers.delete(follower)
  end
end

```


Here the class has a single method, method un_follow! deletes the follower from the followers collection of the user
The ! tells the reader that the change done by this method is permanent or dangerous
Like the sort! method in the Ruby libray for Array Class


```ruby
elements = [4, 56, 2, 1, 67]
elements.sort # => returns new_numbers will contain
              # the sorted copy of numbers
#=> [1, 2, 4, 56, 67]
elements      # original array is not changed
#=> [4, 56, 2, 1, 67]
elements.sort! # Change the original array object here(elements)
#=> [1, 2, 4, 56, 67]
elements      # original array is changed
#=> [1, 2, 4, 56, 67]
```


