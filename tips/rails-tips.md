## pluck

You can pass multiple arguments to `Model.pluck`:

``` ruby 
  Product.pluck :id,:name  #[1, "Cool shoes"], [2, "a shirt"]
```

`pluck` is a highly useful method in general, since you're only instantiating a simple array, not a bunch of AR objects, which is more efficient / fast.  FYI, you can easily grab distinct IDs via (EG) `pluck('distinct(questions.id)')`.

## DB Transactions with AR

ActiveRecord makes it really easy to use DB transactions, which basically groups your database commands so that either they all succeed, or none of them do (get rolled back if failed); good article [here](http://vaidehijoshi.github.io/blog/2015/08/18/safer-sql-using-activerecord-transactions/) ... quick example:

``` ruby
Product.transaction do
  @product.buy!
  @user.charge!
  @merchant.add_sale!
end #either all commands succeed or none do
```

Note that only an exception will force a rollback, hence the need for the `!`s.  More examples [here](http://api.rubyonrails.org/classes/ActiveRecord/Transactions/ClassMethods.html).

## aliasing

helps to [alias](https://en.wikipedia.org/wiki/Alias_(command)) `bundle exec` to `b`; [article](https://coderwall.com/p/my5veg/shell-alias-to-stop-writing-bundle-exec).  just put `alias b="bundle exec"` in your `~/.bash_profile` (Mac) or `~/.bashrc` (Linux).  it also helps to alias commonly used commands, eg `alias rdm="bin/rails db:migrate"`

though for the most part you can avoid using `bundle exec` with Rails thanks to [binstubs](https://github.com/rbenv/rbenv/wiki/Understanding-binstubs) and [spring](https://github.com/rails/spring) (eg `bin/rails s`)
