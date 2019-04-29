---
description: the solution and the problem
---

# Cache

It's super easy to use [cache on rails](https://guides.rubyonrails.org/caching_with_rails.html) \(aka, `Rails.cache`\) but we need to keep this in mind:

* cache should **never** be a requirement for your app
* your app should load **good** without cache and **really good** with cache
* no cache is better than any type of cache, only use it as the **last resort**



