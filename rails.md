---
description: >-
  Ruby on Rails is the framework I like the most. I will try to keep here some
  nice things about it that people usually are unfamiliar with.
---

# Rails

## runner

[Rails runner](https://guides.rubyonrails.org/command_line.html#rails-runner) is useful to **run scripts within rails**.

So you can run a script like the one bellow like this: `bundle exec rails r my_script.rb`

```ruby
User.find_each do |user|
  puts user.name
  puts user.email
end
```

## 

