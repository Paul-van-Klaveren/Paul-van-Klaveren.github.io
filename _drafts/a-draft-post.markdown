---
title:  "A Draft Post"
description: Work in progress
## date: add a date when publishing
---

Drafts are posts without a date. They’re posts you’re still working on and don’t want to publish yet. To get up and running with drafts, check the `_drafts` folder in the site’s root.

To preview your site with drafts, simply run **`jekyll serve`** or **`jekyll build`** with the **`--drafts`** switch. Each will be assigned the value modification time of the draft file for its date, and thus you will see currently edited drafts as the latest posts.
`oO 0`

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

This is some text with a foot note.[^1]. Other text with a footnote.[^footnote].

Or [^other-note] …and [^codeblock-note]

### Code block
```
func explain(topic: String) {
	let x = 123
	if x ~= 0.bunchOfNumbers.count {
		print("Glory!")
	}
}
```
NB. `bunchOfNumbers` can be any type of Collection.
Also, consider 
ruby: `x = Class.new`{:.language-ruby}
bash: `for i in {1..4}; do echo KAAS; done`{:.language-bash}

Using { % language } :
{% highlight swift %}
func explain(topic: String) {
   let x = 123
   if x ~= 0.bunchOfNumbers.count {
      print("Glory!")
   }
}
{% endhighlight %}

text text text text text text text 
text text text text text 
text text text text text text 
text text text text text 
text text text text text text text text 

* list one
^ 
* list two
text text text text 
text text text text 


---

#### Sources

[^1]: Some *crazy* footnote definition.

[^footnote]:
    > Blockquotes can be in a footnote.

        as well as code blocks

    or, naturally, simple paragraphs.

[^other-note]:       no code block here (spaces are stripped away)

[^codeblock-note]:
        this is now a code block (8 spaces indentation)



[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com
