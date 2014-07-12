# Link Posts for Jekyll Sites

## Introduction

The code in this repository enables you to make *linked list*-style posts with Jekyll. This type of post uses its headline as a link to the external source you comment on. In most cases these linked headlines are marked by a symbol, e.g. an arrow, to distinguish them from regular headlines which lead to the post page instead (cf. example files). One well known example of a linked list is [daring fireball](http://daringfireball.net).

Although link posts are a clean and reader-friendly format for short comments on external resources, there's a downside: if the headline of the article leads to an external URL, you can only reach the actual article page on your blog through your archive (if you have one). To provide your reader with a link to the post page, you can add its permalink to the post's metadata. Both example files contain a line that generates a permalink in the post's meta data.

## How to use it

To create link posts, you need to add a variable called `link` followed by the external URL to your post's front matter. You also need to replace the liquid code generating post headlines in both `/index.html` and `/_layouts/post.html`. The new liquid code will check if a link is defined. If yes, it will insert an external link and the symbol. If no, it will insert the permalink to the post page.

The same needs to be done for any other layout file in which you want to use external links for the headlines. For example, if you want to use them with pages, you also have to add it to `/layouts/page.html`.

### YAML frontmatter

This is simple. Your YAML frontmatter should look like this for Youtube videos:

    ---
    title: Congratulations, Pinboard - The User-Friendly Bookmarking Site Turns Five
    layout: post
    link: https://blog.pinboard.in/2014/07/pinboard_turns_five/
    ---

### .html files

In `/index.html`, you need to replace the line generating post headlines in the loop with one of the following code blocks. The simple conditional statement checks whether an external link is present in a post's front matter and, if yes, creates an external link instead of a permalink.

In the first example, the conditional statement is embedded within the link. This version is also used in this repository's `index.html` example file:

    <h1 class="post-title"><a href="{% if post.link %}{{post.link}}{% else %}{{ post.url }}{% endif %}">{{ post.title }}</a>{% if post.link %}<span class="link-arrow"> &rarr;</span>{% endif %}</h1>

The second example is easier to read. Here, it's the other way around: the html code is embedded in the conditional statement. This code can be found in the `post.html` example file. In layout files, don't forget to prefix the variables with `post.` instead of `page.`:

    {% if page.link %}
    	<h1 class="post-title"><a href="{{ page.link }}">{{ page.title }} <span class="link-arrow">&rarr;</span></a></h1>
    {% else %}
    	<h1 class="post-title">{{ page.title }}</h1>
    {% endif %}
