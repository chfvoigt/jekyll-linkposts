# Link Posts for Jekyll Sites

## Introduction

The code in this repository enables you to create *linked-list* style posts with Jekyll. This type of post uses its headline as a link an external source. In many cases these headlines are marked by a symbol, e.g. an arrow, to distinguish them from regular headlines go to the post's permalink (cf. example files). One well known example of a linked list is [Daring Fireball](http://daringfireball.net).

Although link posts are clean and reader-friendly for short comments on external resources, there's a downside: if the headline of the article leads to an external URL, you can only reach the actual article page on your blog through your archive (if you have one). To provide your reader with a link to the post page, you can add its permalink to the post's meta data. Both example files contain a line that generates a permalink in the post's meta data line.

## Getting started

To create a link post, you need to add a variable called `link` followed by the external URL to its front matter. You also need to replace the liquid code generating post headlines in both `/index.html` and `/_layouts/post.html`. The new liquid code will check if a link is defined. If it is, it will insert the external url in the link and a right arrow at the end of the headline. If no link is defined, it will behave as in a standard installation.

The same change needs to be applied in any other layout file in which external links should be used for the headlines. If for example you want to use them with pages, you also have to modify `/layouts/page.html`.

### YAML frontmatter

Your YAML front matter of a link post should contain the ´link´ variable:

    ---
    title: Congratulations, Pinboard - The User-Friendly Bookmarking Site Turns Five
    layout: post
    link: https://blog.pinboard.in/2014/07/pinboard_turns_five/
    ---

### Template and layout files

In `/index.html`, you need to replace the line in the loop generating post headlines with one of the following code blocks. The simple conditional statement checks whether an external link is present in the post's front matter and, if yes, creates an external link instead of a permalink.

In the first example, the conditional statement is embedded within the link. This version is also used in this repository's `index.html` example file:

    <h1 class="post-title"><a href="{% if post.link %}{{ post.link }}{% else %}{{ post.url }}{% endif %}">{{ post.title }}</a>{% if post.link %}<span class="link-arrow"> &rarr;</span>{% endif %}</h1>

In the second example the html code is embedded in the conditional statement. This code can be found in the `post.html` example file. In layout files, don't forget to prefix the variables with `post.` instead of `page.`:

    {% if page.link %}
    	<h1 class="post-title"><a href="{{ page.link }}">{{ page.title }} <span class="link-arrow">&rarr;</span></a></h1>
    {% else %}
    	<h1 class="post-title">{{ page.title }}</h1>
    {% endif %}
