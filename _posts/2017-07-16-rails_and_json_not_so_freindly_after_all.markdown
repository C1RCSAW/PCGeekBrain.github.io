---
layout: post
title:  "Rails and JSON: Not so freindly after all."
date:   2017-07-16 18:41:08 -0400
---


I woke up this morning thinking that fufiliing some relatively trivial SPA featrues on top of my old rails project would not be so complicated. After all, rails big claim to fame is that it supported dynamic SPA style development from day one. Well, that is not really the case.

## Are you html_safe?
when it comes to json, like xml every single character makes a difference. However rails built in tag generators mark their output as `html_safe` (or no need to escape when rendering) this works just fine for HTML pages, but the inability to turn it off without corrupting the data beyond repair (`.to_json.to_s` is the only way I found, and it adds all these symbols that json does not like one bit) forces you to inplament helper functions twice. Once in js and once in ruby. In my opinion this can lead to a bad user experiance too fast and needs to be addressed.

## Nill is truely missing this evening.
Rails 101, `nill` is the only falsy value that is not false. As such, one grows accostomed to relying on `nill` to kinda behave the same as false. Beware, `nill` means `nill` and if it renders in your json you will be left with some nice syntax errors.

## ActiveModel serilization, there is no shortcut for that?
Ok, this is a pet peve but why does the serializer work with `render json: @object` (which calls `@object.to_json` under the hood) but when you call `@object.to_json` directly it pretends it does not exists. For anyone wondering *this* is how you use a serializer in your json

```
ActiveModel::SerializableResource.new(@object).serializable_hash.to_json.html_safe
```

Insane I know.
