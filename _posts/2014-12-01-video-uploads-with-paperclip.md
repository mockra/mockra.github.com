---
layout: post
title: Video Uploads with Paperclip
---
Uploading videos to a Rails application using Paperclip is almost identical to
image uploads. Here's a quick example of how to get started using Paperclip in
your project.

The first thing you'll need to do is add the library to your `Gemfile`.

`gem "paperclip"`

You'll then want to run `bundle install` before continuing.  The next step in
our example is adding migrations for the record you want to store a video for.
In our case, we're going to have a `Video` record that stores our `file`.

Our migrations will look like:

~~~
  class CreateVideos < ActiveRecord::Migration
    def change
      create_table :videos do |t|
        t.string :title
        t.attachment :file

        t.timestamps
      end
    end
  end
~~~

We'll then want to add the appropriate logic to our model. In this case, we're
going to use the `file` column for storing our attachment. We're also going to
skip validating the content type.

~~~
  class Video < ActiveRecord::Base
     has_attached_file :file
     do_not_validate_attachment_file_type :file
  end
~~~

You'll also want to add a `file_field` to the form you're using to create a
`Video` record. Here's an example of what that looks like using `simple_form`
and `slim`.

~~~
  = simple_form_for @video do |f|
    = f.input :title
    = f.file_field :file
    = f.submit
~~~

When we want to display the video on a page, we can use the following code:

~~~
  video width="100%" controls=""
    source src="#{@video.file.url}"
~~~

We'll most likely want to store our videos on S3, which is easy to do using
Paperclip. The first thing we'll need to do is add the `aws-sdk` library to our
Gemfile.

`gem 'aws-sdk'`

You may want to only include this gem in your production environment. We'll
then want to include some configuration in `config/environments/production.rb`.

~~~
  config.paperclip_defaults = {
    storage: :s3,
    s3_credentials: {
      bucket: 'your-bucket-name'
    }
  }
~~~

You'll also need to add the `config/aws.yml` file. This is where you'll put
your amazon keys.

~~~
  production:
    access_key_id: your-access-key
    secret_access_key: your-secret-key
~~~

Once you've finished setting up AWS for your project, your video uploads will
be ready to go!
