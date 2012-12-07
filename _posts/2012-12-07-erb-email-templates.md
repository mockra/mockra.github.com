---
layout: post
title: ERB Email Templates
---
I was playing around with ERB the other day and ended up designing a really
simple e-mail system with templates. Here's the system I created.

    class Email
      def deliver
        EmailApi.new(email_options).deliver
      end

      def template
        File.open "templates/#{handle}.erb"
      end

      def message
        ERB.new(template.read).result(binding)
      end

      def handle
        self.class.to_s.downcase
      end
    end

    class SignupEmail < Email
      attr_accessor :user
      def initialize user
        @user = user
      end

      def email_options
        { :body => message,
          :to => user.email,
          :subject => subject
        }
      end

      def subject
        "Welcome #{user.name}"
      end
    end

In order to send a sign up email to a new user, you would call:

    SignupEmail.new(user).deliver

EmailApi would represent the service you're using to deliver e-mails in your
application. The body of the e-mail would be created from the signupemail.erb
file in the templates directory.

By passing binding to ERB, you're able to access the @user variable in your
template.
