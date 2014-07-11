# Link Posts for Jekyll Sites

## What it is

The code in this repository enables you to make *linked list*-style posts with Jekyll. This type of link post turns the title of the article into a link to the external source you comment on. In most cases these links are marked by a symbol, e.g. an arrow, to distinguish them from regular posts (cf. example files).

Although link posts are a clean format for short comments on external resources, there's a downside: if the headline of the article leads to an external URL, you can only reach the actual article page on your blog through your archive (if you have one). To provide your reader with a link to the post page, you can add its permalink to the post's metadata (cf. example files).

## How to use it

To create link posts, you need to add a variable called `link` followed by the external URL to your post's front matter. You also need to replace the liquid code generating post headlines in both `/index.html` and `/_layouts/post.html`. The new code will read the variable and insert the corresponding code if it is present.

The same needs to be done for any other layout file in which you want to use external links for the headlines. For example, if you want to use them with pages, you also have to add it to `/layouts/page.html`.

### YAML frontmatter

This is simple. Your YAML frontmatter should look like this for Youtube videos:

    ---
    title: Pinboard - A User-Friendly Bookmarking Site
    layout: post
    link: http://pinboard.in
    ---

### .html files

For the loop in `/index.html`, you need to replace the line generating the headline of a post with one of the following code blocks which check whether an external link is present in a post's front matter and, if so, inserts it into the headline instead of the article's permalink. 

In the first example, I embedded the conditional statement within the link. You can find this code block in the `index.html` example file:

    <h1 class="post-title"><a href="{% if post.link %}{{post.link}}{% else %}{{ post.url }}{% endif %}">{{ post.title }}</a>{% if post.link %}<span class="link-arrow"> &rarr;</span>{% endif %}</h1>

The second example is easier to read. Here, the html code is embedded in the conditional statement. This code can be found in the other example file (the `post.html` example file), for which (like for any other layout file) you also need to use `post.` instead of `page.`:

    {% if page.link %}
    	<h1 class="post-title"><a href="{{ page.link }}">{{ page.title }} <span class="link-arrow">&rarr;</span></a></h1>
    {% else %}
    	<h1 class="post-title">{{ page.title }}</h1>
    {% endif %}

The two example files will also generate permalinks in the post's metadata line in case you'd like to have a look at it.
