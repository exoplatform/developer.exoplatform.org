# developer.exoplatform.org

This site groups together all documentations useful to develop or contribute to eXo Platform projects.
It is built using [Jekyll](https://github.com/mojombo/jekyll) and its extension [Jekyll Bootstrap](http://jekyllbootstrap.com/)
 and deployed on [Github Pages](https://pages.github.com).

## How to contribute ?

Feel free to fork the repository and to propose pull requests.

## How to preview the site ?

1.    Install RVM and ruby

    curl -sSL https://get.rvm.io | bash -s stable

    rvm install 2.1.1

    rvm use 2.1.1

2.   [Install Github Pages](https://help.github.com/articles/using-jekyll-with-pages) which will [Install Jekyll](https://github.com/mojombo/jekyll/wiki/install) too. In your developer.exoplatform.org local clone directory just call :

    gem install bundler

    bundle install 

3.   In order to get a server up and running with your Jekyll site, run:

    jekyll serve --watch --drafts

and then browse to <http://localhost:4000>.

4.   In order to update jekyll and related :

    bundle update

## How to create a new post ?

    rake post title="A Title" [date="2012-02-09"]

## How to create a new page ?

    rake page name="about.md"

You can also specify a sub-directory path.
If you don't specify a file extension we create an index.html at the path specified

## License

[Creative Commons BY-NC-SA](http://creativecommons.org/licenses/by-nc-sa/3.0/)

