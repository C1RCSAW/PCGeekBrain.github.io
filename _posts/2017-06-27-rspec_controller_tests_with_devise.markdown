---
layout: post
title:  "RSPEC Controller tests with Devise"
date:   2017-06-27 15:58:22 +0000
---


## Setup

(**Note:** it would seem that the `warden` gem is required as well for the devise test helpers)

To generate your rspec shell in rails run `rails generate rspec:install`

To add Devise (assuming the gem is required) you simply need to add the following after `Rspec.configure do |config|`:

```
config.include Devise::TestHelpers, type: :controller
```

then simply use `type: :controller` after your tests `RSpec.describe ...` for RSpec to auto load all the functions you need.

## Details

Devise test helpers give you two usefull functions. `sign_in` and `sign_out`. They are actually rather self explanatory (`sign_in` just takes a user model) regardless here is the source code: https://github.com/plataformatec/devise/blob/master/lib/devise/test/controller_helpers.rb

## Issues: Devise sign_in helper not working in nested context/describe
When nesting contexts or descriptions for simple organization and simple docs generation. This seems to be since response is not reset on a new call to `get` or `post`. The solution to this is simply to remove the nesting and just add more text to the describe to try and help with this. 

See this commit for a code example: https://github.com/PCGeekBrain/libshare-rails/commit/48daa86557d28d8a147c96fdff54a7f2e1ea7771



