# Method Scope Lab

## Learning Goals

- Define a local variable with the expected value
- Recognize the restrictions of local variable scope
- Define a method that outputs a popular catch phrase
- Define a method that takes in an argument

## Introduction

We're going to build a catch phrase generator. Using knowledge of methods,
scope, and variables, we're going to create a few methods that print a catch
phrase from some popular video games.

## Define a Local Variable With the Expected Value

Open up `lib/catch_phrases.rb`. You should see the following method:

```ruby
def mario
  status = 'Thank You Mario! But Our Princess Is In Another Castle!'
  puts phrase
end
```

Note that the method is trying to `puts` out a variable called `phrase`.

If we run the test for this method only by typing `rspec spec/catch_phrases_spec.rb`
into your terminal in the directory of this lab. You should see the following
error:

```ruby
NameError:
  undefined local variable or method `phrase' for #<RSpec::ExampleGroups::CatchPhrasesRb:0x007fa5eb399b88>
```

This error is occurring because the code inside the `#mario` method is trying to
use the `phrase` variable **but** it's not present inside the _scope_ of the
`#mario` method. **It is out of scope.**

If we look at the test for this method in `spec/catch_phrase_spec.rb` we can see
that it expects "It's-a me, Mario!" to be printed out.

```ruby
describe "#mario" do
  it "puts out 'It's-a me, Mario!'" do
    phrase = "It's-a me, Mario!"
    expect{mario}.to output("It's-a me, Mario!\n").to_stdout
  end
end
```

We need to define the variable `phrase` in our `#mario` method. When `phrase` is
called, the output should be "It's-a me, Mario!"

Once `phrase` is defined in the method, the first test should pass. Let's move
on to the next method!

## Recognize the Restrictions of Local Variable Scope

In `lib/catch_phrases.rb`, take a look at the following method:

```ruby
def toadstool
  puts status
end
```

Notice that the body of this method is setting a calling a variable that is set
in the `#mario` method. When we run the tests, we are getting a `NameError`
because `status` is `undefined`.

Wait a minute, you might be wondering. Didn't we define `status` inside the
`#mario` method? We did, but variables defined inside a method are only
accessible to that method. They are not available outside of that method in any
other context.

Make sure that the `status` variable is in the correct context to be used by the
`#toadstool` method.

Now that we've walked through a couple of methods, let's define two new methods
from scratch!

## Define a Method That Outputs a Popular Catch Phrase

Now that our first two tests should be passing, let's try writing a method from
scratch on our own. In `lib/catch_phrases.rb`, define the method `link` that
will output the phrase "It's Dangerous To Go Alone! Take This."

## Define a Method That Takes in an Argument

For our final method, we'll want to define the method `any_phrase`. After this
method is defined, we can see that our next failing test looks like this:

```ruby
expected block to output "Hey! Listen!\n" to stdout, but output nothing
```

Take a look at our test `rspec spec/catch_phrases_spec.rb`:

```ruby
describe "#any_phrase" do
  it "takes in an argument and puts out the catch phrase" do
    phrase = "Do A Barrel Roll!"
    expect{any_phrase(phrase)}.to output("Do A Barrel Roll!\n").to_stdout
  end
end
```

This test expects `any_phrase` pass in an argument called `phrase` that outputs
"Hey! Listen!" Define a method that takes this passed in variable and can output
the phrase that is assigned to that variable.

Now run your tests again. If all methods have been written correctly, you should
see four tests passing!

## Conclusion

We've discussed building methods and recognizing how scope works within the
context of each method. With these concepts put together we can see how it
functions in practice. As we discuss scope further, we'll understand more about
how to access variables in different scopes.