---
title: SXY-000
tagline: about something
permalink: /standards/SXY-000/
tags: [foo,bar]
controlsSeverity: [blocker,critical,major,minor,info]
status: draft
validationDate:
sinceLevel:
published: false
---

<a name="what"></a>
## What?

### <i class="fa fa-info-circle"></i> The rule

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed dictum pretium purus, in lobortis odio blandit et. Nulla facilisi. Donec sit amet consectetur nunc. Vestibulum dictum accumsan quam, non iaculis lectus viverra quis. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Praesent iaculis purus nisl, sed faucibus nibh ultricies id. Curabitur ut ipsum sed nulla eleifend viverra eget vitae arcu. Morbi finibus placerat congue.

### <i class="fa fa-lightbulb-o"></i> The solution

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed dictum pretium purus, in lobortis odio blandit et. Nulla facilisi. Donec sit amet consectetur nunc. Vestibulum dictum accumsan quam, non iaculis lectus viverra quis. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Praesent iaculis purus nisl, sed faucibus nibh ultricies id. Curabitur ut ipsum sed nulla eleifend viverra eget vitae arcu. Morbi finibus placerat congue.

<a name="why"></a>
## Why?

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed dictum pretium purus, in lobortis odio blandit et. Nulla facilisi. Donec sit amet consectetur nunc. Vestibulum dictum accumsan quam, non iaculis lectus viverra quis. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Praesent iaculis purus nisl, sed faucibus nibh ultricies id. Curabitur ut ipsum sed nulla eleifend viverra eget vitae arcu. Morbi finibus placerat congue.

<a name="examples"></a>
## Examples

### An example

<div class="panel panel-danger">
  <div class="panel-heading">
    <h3 class="panel-title"><i class="fa fa-thumbs-down pull-right"></i> Wrong example</h3>
  </div>
  <div class="panel-body">

{% highlight java %}
    if ((attribute == null)
       || (This.attribute == null)
       || (This.attribute == anotherAttribute)) {
      this.attribute = attribute;
    }
    else {
      this.attribute += "" + attribute;
    }
{% endhighlight %}

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed dictum pretium purus, in lobortis odio blandit et. Nulla facilisi. Donec sit amet consectetur nunc. Vestibulum dictum accumsan quam, non iaculis lectus viverra quis. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Praesent iaculis purus nisl, sed faucibus nibh ultricies id. Curabitur ut ipsum sed nulla eleifend viverra eget vitae arcu. Morbi finibus placerat congue.

  </div>
</div>


<div class="panel panel-success">
  <div class="panel-heading">
    <h3 class="panel-title"><i class="fa fa-thumbs-up pull-right"></i> Good example</h3>
  </div>
  <div class="panel-body">

{% highlight java %}
    if ((attribute == null) ||
         (This.attribute == null) ||
         (This.attribute == anotherAttribute)) {
      this.attribute = attribute;
    }
    else {
      this.attribute += "" + attribute;
    }
{% endhighlight %}

  </div>
</div>


<a name="controls"></a>
## <i class="fa fa-shield"></i> Controls

### for Java

<div class="table-responsive">
  <table class="table">
    <thead>
      <tr>
        <th>Rule Type</th>
        <th>Rule</th>
        <th>Rule Settings</th>
        <th>Severity</th>
      </tr>
    </thead>
    <tbody>
    <tr>
      <td>Checkstyle</td>
      <td><a href="http://checkstyle.sourceforge.net/config_sizes.html#LineLength">Sizes - LineLength</a></td>
       <td>
{% highlight text %}
module name="LineLength"
property name="max"
value="130"
property name="tabWidth"
value="2"
{% endhighlight %}
       </td>
       <td>MINOR</td>
     </tr>
     <tr>
       <td>Checkstyle</td>
       <td><a href="http://checkstyle.sourceforge.net/config_whitespace.html#FileTabCharacter" >Whitespace -
       FileTabCharacter</a></td>
       <td>
{% highlight text %}
module name="FileTabCharacter"
property name="eachLine" value="true"
property name="fileExtensions" value="java,xml"
{% endhighlight %}
       </td>
       <td>MAJOR</td>
     </tr>
   </tbody>
  </table>
</div>
