# developer.exoplatform.org

This site groups together all documentations useful to develop or contribute to eXo Platform projects.
It is built using [Jekyll](https://github.com/mojombo/jekyll) and its extension [Jekyll Bootstrap](http://jekyllbootstrap.com/)

## How to contribute ?

Feel free to fork the repository and to propose pull requests.

## How to preview the site ?

1.   [Install Jekyll](https://github.com/mojombo/jekyll/wiki/install). It is a ruby gem and often it is just :

    sudo gem update --system

    sudo gem install jekyll rdiscount RedCloth
    
    sudo easy_install Pygments

2.   In order to get a server up and running with your Jekyll site, run:

    jekyll serve --watch

and then browse to <http://localhost:4000>.

## How to create a new post ?

    rake post title="A Title" [date="2012-02-09"]

## How to create a new page ?

    rake page name="about.md"

You can also specify a sub-directory path.
If you don't specify a file extention we create an index.html at the path specified

## License

[Creative Commons BY-NC-SA](http://creativecommons.org/licenses/by-nc-sa/3.0/)

