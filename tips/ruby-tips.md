### Ruby Tips

* learn [Pry](https://github.com/pry/pry); love Pry
  * [pry-byebug](https://github.com/deivid-rodriguez/pry-byebug) gives Pry some step-by-step debugging capabilities
  * [pry-rails](https://github.com/rweng/pry-rails) adds Pry to the Rails console
* only `false` and `nil` are falsy
* class methods are stored in eigenclasses; see: https://gist.github.com/jfarmer/2625060
```ruby
class << self # lets you access the eigenclass
  def blah # im a class method (instance method on the eigenclass)
  end
end

# equivalent to:
def self.blah
end
```
* the `source_location` method lets you know where a Ruby method is defined.  http://stackoverflow.com/a/3393706/548170
* it's easy to create your own logger with Ruby's [Logger](https://ruby-doc.org/stdlib-2.1.0/libdoc/logger/rdoc/Logger.html) class:
```ruby
    logger = Logger.new('logfile.log')
    logger.info 'what up'
```

