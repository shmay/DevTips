## Sidekiq

[Sidekiq](https://github.com/mperham/sidekiq) will **NOT** use multiple cores by default (at least with CRuby).  Its [concurrency](https://github.com/mperham/sidekiq/wiki/Advanced-Options#concurrency) option merely sets the number of threads per core.  For CRuby, it's ["One core per process"](https://github.com/mperham/sidekiq/issues/1244#issuecomment-26136518).

Luckily, Sidekiq deploy helper gems, like 
mina-sidekiq, often let easily you specify the number of Sidekiq processes you'd like to spin up: https://github.com/Mic92/mina-sidekiq#available-options

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

## misc

* have a lot of routes?  use grep/ack to help filter them, eg: `bin/rails routes | grep questions`

## good gems

* [annotate](https://github.com/ctran/annotate_models) (annotate your models)
* **deploying:** capistrano / [mina](https://github.com/mina-deploy/mina) (i much prefer mina)
* **auth:** [devise](https://github.com/plataformatec/devise) / [Sorcery](https://github.com/Sorcery/sorcery) (I prefer Sorcery for its simplicity and flexibility)
* **debugging:** byebug, pry, pry-byebug
* **cron jobs:** [whenever](https://github.com/javan/whenever) - amazing DSL for cron jobs
* **authorization:** [pundit](https://github.com/elabs/pundit) - havent used, but heard good things.
* [Bullet](https://github.com/flyerhzm/bullet) to help kill N+1 queries and unused eager loading

Also see thoughtbot's [suspenders](https://github.com/thoughtbot/suspenders) Rails template app for a bunch of sane Rails gems / defaults.

Aaaaand this big ol list of good Ruby gems: https://github.com/markets/awesome-ruby (via https://github.com/sindresorhus/awesome)

## aliasing

helps to [alias](https://en.wikipedia.org/wiki/Alias_(command)) `bundle exec` to `b`; [article](https://coderwall.com/p/my5veg/shell-alias-to-stop-writing-bundle-exec).  just put `alias b="bundle exec"` in your `~/.bash_profile` (Mac) or `~/.bashrc` (Linux).  it also helps to alias commonly used commands, eg `alias rdm="bin/rails db:migrate"`

though for the most part you can avoid using `bundle exec` with Rails thanks to [binstubs](https://github.com/rbenv/rbenv/wiki/Understanding-binstubs) and [spring](https://github.com/rails/spring) (eg `bin/rails s`)
