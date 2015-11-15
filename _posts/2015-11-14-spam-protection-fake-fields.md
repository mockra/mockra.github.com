---
layout: post
title: Spam Protection - Fake Form Fields
---
There are a variety of ways to prevent spam from passing through your forms,
but one method I like is using a fake form field. While it's not going to be
the best method for stopping spam, it doesn't hinder the user experience, which
is a big plus.

This approach relies on the fact that most scripts don't render CSS, so they'll
fill in an invisible form field, whereas your users that can't see the field
will not. Here's an example of how you can setup the fake field.

```
  <input type="text" name="business" id="business" class="fake-field" tabindex="-1">
```

```
  .fake-field {
    display: none !important;
  }
```

You can then use javascript to prevent your form from being submitted if that
input contains a value. There's also the option of preventing the input server
side as well. It's a simple approach towards stopping bots, but it's a decent
solution that doesn't affect user experience. It's even better when combined
with a spam detection service.
