---
title: "How to add tags to a Hugo site"
description: A simple tutorial explaining how to add tags to posts.
author: Tyler
date: 2022-06-20
draft: false
tags: ["tutorial", "hugo"]
---

In this tutorial, I'll be explaining how to add tags to a post in Hugo.

You can scroll all the way to the bottom of this post to see its tags.

> Note: This tutorial is geared towards those who are using Hugo themes with *header.html* and *footer.html* partials.
>If your theme does not have these, [here's a better tutorial](https://www.jakewiesler.com/blog/hugo-taxonomies).

{{< toc >}}

## Step 1A: What's a tag?

Simply put, a "tag" is a key word that dictates what your post is about.

For example, the tags for this post are "tutorial" and "hugo".

Tags allow a user to see a list of posts related to what they are currently reading.

So, if you click "tutorial" at the bottom of this post, you will see a list of posts that also have a "tutorial" tag.

Hugo provides support for tags in the form of **taxonomies**.

## Step 1B: What's a taxonomy?

A taxonomy is a user-defined grouping of content.

They include tags, as well as categories. In fact, these are two default taxonomies that Hugo supports right out of the gate. More info [here](https://gohugo.io/content-management/taxonomies/#configure-taxonomies).

You won't need to edit your config file!

##  Step 2: Adding tag layouts

The process is pretty straightforward. We'll be working with 2 files.

First, go onto your layouts folder, and add a new subfolder titled: **taxonomy**.

In this folder, create 2 files: one named **terms.html** and one named **list.html**

Open **terms.html** in your text editor, and copy this code into it: 
```
{{ partial "header.html" . }}

<section>
  <h1>Tags</h1>
  <ul>
    {{ range .Data.Terms.Alphabetical }}
      <li>
        <h2>
          <a href="{{ .Page.Permalink }}">({{ .Count }}) {{ .Page.Title }}</a>
        </h2>
      </li>
    {{ end }}
  </ul>
</section>

{{ partial "footer.html" . }}
```

Save the file, then open **list.html** in your text editor, and copy this code into it:
```
{{ partial "header.html" . }}

<section>
  <h1>Tag: {{ .Title }}</h1>
  <ul>
    {{ range .Pages }}
      <li>
        <h2>
          <a href="{{ .Permalink }}">{{ .Title }}</a>
        </h2>
        <time>{{ .Date.Format (.Site.Params.dateform | default "January 2006") }}</time>
      </li>
    {{ end }}
  </ul>
</section>

{{ partial "footer.html" . }}
```

Save this file too.

Now we're pretty much done the hard part.

## Step 4: Adding tags to posts

Now, to add tags to a post, simply open the post in your text editor, and add tags to the front matter.

For this post, I added: `tags: ["tutorial", "hugo:]` to the front matter.

You can add as many tags as you want, just make sure they're in brackets.

## Step 4A: A separate tags page.

Everyone's Hugo theme is different, so there's a chance that this step may not work.

If you have the archie theme like I do, then it *will* work!

This step adds a list of posts that have the same tag.

We'll make a new post to showcase it

In your **posts** folder, create a new folder titled: **test_post**

In this folder, create a index.md file, and open it in your text editor.

Add this front matter to it:

```
---
title: "Testing tags"
description: just testing a tags page
date: 2022-06-20
draft: false
tags: ["testing"]
---
```

Add whatever else you want to the post, then save it.

This is a process Hugo calls "page bundling". You can find out more [here](https://gohugo.io/content-management/page-bundles/).

When you run your site locally, you should be able to find your tag at the bottom of the post, and clicking it will bring you to a page with other posts that also have the tag.

## Conclusion

I hope this tutorial helped you add tags to your posts!!

You can view this site's [GitHub repo](https://github.com/autonot/aspii.xyz) if you want to see what I did (in case your tags don't work).

:)



