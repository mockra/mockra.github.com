---
layout: post
title: Credit Card Form Styling
---
Adding styling and formatting to a credit card form is a great way to improve
your conversion rate. One of the best tools for improving your payment form is
[jQuery.payment](https://github.com/stripe/jquery.payment), which provides
formatting, validation, and css markup for your credit card fields.

The first step is including the library, here's a link to a
[CDN](http://cdnjs.com/libraries/jquery.payment). You can then add payment
formatting to your form:

{% gist mockra/ad138b4622925812b641 %}

This will format the credit card input and cvc fields. It will also add a
credit card class to your input once a card number is entered. You can use this
class to style your form based on the type of card.

An example would be adding a background-image to your input based on the type of card. Here's an example of the css you could use to add card provider images.

{% gist mockra/663d09b6ba58f84a7a32 %}
