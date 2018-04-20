---
layout: post
title: "Making a Static Website with Jekyll and S3"
description: S3 + Jekyll = Cheap Hosting
date: 14/2/2018
categories: ["AWS", "Web Development", "Jekyll"]
---

If you need to make a marketing website for your business, aside from the branding and design aspect, your main concerns are probably:

> Will the site be fast and responsive for my potential clients/customers?

> How much will the site cost to make and maintain?

Site speed and reliability is huge for marketing. People need to be able to access your site from a variety of devices and internet speeds. You don't want users to have to wait seconds for your page to respond. That's lost business right there.

But you also don't want to go bankrupt making the website. So you have to be cost conscious about building your marketing website and hosting it for potentially decades.

Rest assured, there's a solution that will put all these worries to rest.

That solution leverages the [most popular Amazon Web Services product](http://2ndwatch.com/blog/the-most-popular-aws-products-of-2016/): S3.

Aside from storing images or files for an application, S3 can also host static websites. Static websites are made up of HTML, CSS, and Javascript. Not only are they fast to load, they are one the easiest types of websites to put together.

It is even easier when using something like [Jekyll](https://jekyllrb.com/). Jekyll gives you the flexibility to use Markdown, raw HTML, partials for, say, a header or footer, and use SASS for styling. Not only that, it's very simple to set up.

But wait, there's more! In the form of a gem called [`s3_website`](https://github.com/laurilehmijoki/s3_website). What does S3 Website do? Well...it helps you make a website using S3. It pushes your static site content output from something like Jekyll and into the bucket of your choosing.

It can even create a bucket and set it up for static hosting, but I prefer to do it manually. It's not hard at all. [AWS has a guide for setting up a bucket for website hosting](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html), which goes through all the options and configuration needed for it to work. It also gives you more familiarity with what's going on in case you have to configure Cloudfront later. There are only a few steps to do, and once it's done you're ready to go.

You can get to the exciting part now: making your website actually a website.

After installing Jekyll, run the command to generate a new website:

```
jekyll new SITE_NAME
```

You can run `jekyll serve` to see the basic site it gives you. Which is more than sufficient for tutorial purposes.

The only edit to any of the files Jekyll generated that needs to be done for `s3_website` is the Gemfile. Add `gem 's3_website'` and run `bundle install`.

As the gem documentation suggests, running `s3_website cfg create` will create an `s3_website.yml` file containing the configuration for `s3_website`.

The two you really need are the following:

```
profile: <%= ENV['AWS_PROFILE'] %>
s3_bucket: <%= ENV['S3_BUCKET'] %>
```

In the above example, two critical values are set:

- `profile`: As in the AWS credential profile to be used.
- `s3_bucket`: The bucket that you want your Jekyll site to be pushed to.

Both are environment variables in the above example so it's flexible for any user/bucket.

So to deploy, you'd run the following:

```
AWS_PROFILE=profile S3_BUCKET=bucket s3_website push
```

And...if you did everything properly, your website should be live on the S3 URL for your bucket.

Congratulations! You have a static website that'll cost pennies a month to host!
