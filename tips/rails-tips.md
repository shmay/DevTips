* You can pass multiple arguments to `Model.pluck`:
``` ruby 
  Product.pluck :id,:name  #[1, "Cool shoes"], [2, "a shirt"]
```

`pluck` is a highly useful method in general, since you're only instantiating an array of integer, not a bunch of AR objects, which is more efficient / fast in general.  Also, you can easily grab distinct IDs via (EG) `pluck('distinct(questions.id)')`.

* ActiveRecord makes it really easy to use DB transactions, which basically groups your database commands so that either they all succeed, or none of them do (get rolled back if failed); good article [here](http://vaidehijoshi.github.io/blog/2015/08/18/safer-sql-using-activerecord-transactions/) ... quick example:

``` ruby
Product.transaction do
  @product.buy!
  @user.charge!
  @merchant.add_sale!
end #either all commands succeed or none do
```

Note that only an exception will force a rollback, hence the need for the `!`s.  More examples [here](http://api.rubyonrails.org/classes/ActiveRecord/Transactions/ClassMethods.html).

* helps to [alias](https://en.wikipedia.org/wiki/Alias_(command)) `bundle exec` to `b`; [article](https://coderwall.com/p/my5veg/shell-alias-to-stop-writing-bundle-exec)
