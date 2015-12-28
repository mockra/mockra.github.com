---
layout: post
title: Ember Truth Helpers
---
While it's typically cleaner to keep complicated logic out of your templates,
there can be times where you want or need to stick it in your templates. Due to
the limitations of the default handlebars `if` statement, that's not possible
out of the box. I'll admit this might be for good reason, but I've found the
`ember-truth-helpers` addon valuable in some projects.

You can install the addon with:

```
  ember install ember-truth-helpers
```

The addon itself provides some straightforward functionality that allows you to
add logic to your `if` statements. For example:

```
{% raw %}
  {{#if (and a b)}}
    {{show-some-component}}
  {{else}}
    {{show-alternate-component}}
  {{/if}}
{% endraw %}
```

```
{% raw %}
  {{#each options as |option|}}
    {{#if (eq value option)}}
      {{option}}
    {{else}}
      <div class="button" {{action 'toggleOption' option}}>
        {{option}}
      </div>
    {{/if}}
  {{/each}}
{% endraw %}
```

It's important to keep in mind that a lot of this functionality will be better
off in a computed property. If you find you can't use a computed property in a
certain context, then you might want to render each object in a component.

For cases where a component doesn't make sense, or it's simpler to keep the
logic in the template, then this addon is a great tool.
