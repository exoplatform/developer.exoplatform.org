---
title: SXY-000
tagline: THIS IS THE EXCERPT OF THE RULE (have to be short)
permalink: /rules/SXY-000/
author: exoplatform
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

HERE YOU DESCRIBE THE RULE

### <i class="fa fa-lightbulb-o"></i> The solution

HERE YOU CAN DESCRIBE A SOLUTION TO RESPECT THE RULE

<a name="why"></a>
## Why?

HERE YOU HAVE TO EXPLAIN WHY THE RULE IS DEFINED

<a name="examples"></a>
## Examples

### An example

<div class="panel panel-danger">
  <div class="panel-heading">
    <h3 class="panel-title"><i class="fa fa-thumbs-down pull-right"></i> Wrong Java example</h3>
  </div>
  <div class="panel-body">

{% highlight java %}
...
{% endhighlight %}

  </div>
</div>


<div class="panel panel-success">
  <div class="panel-heading">
    <h3 class="panel-title"><i class="fa fa-thumbs-up pull-right"></i> Good Java example</h3>
  </div>
  <div class="panel-body">

{% highlight java %}
...
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
      <td>PMD</td>
      <td><a href="http://pmd.sourceforge.net/rules/logging-java.html#AvoidPrintStackTrace">AvoidPrintStackTrace</a></td>
       <td>
{% highlight text %}
...
{% endhighlight %}
       </td>
       <td>BLOCKER or CRITICAL or ... (Sonar level)</td>
     </tr>
     <tr>
       <td>Checkstyle</td>
       <td><a href="http://checkstyle.sourceforge.net/config_coding.html#IllegalCatch" >IllegalCatch</a></td>
       <td>
{% highlight text %}
...
{% endhighlight %}
       </td>
       <td>BLOCKER or CRITICAL or ... (Sonar level)</td>
     </tr>
   </tbody>
  </table>
</div>
