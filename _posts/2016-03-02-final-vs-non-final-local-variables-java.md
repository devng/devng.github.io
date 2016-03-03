---
layout:     post
title:      My Opinion on Final vs. Non-Final Local Variables in Java
date:       2016-03-02
summary:    In my company we had a discussion about whether we should enforce the use of the final keyword for local variables in Java or not. In this blog post I would like to present my personal opinion on the subject.
tags: java checkstyle code reviews
---

In my company we had a discussion about whether we should enforce the use of the `final` keyword for __local__ variables in Java or not. In this blog post I would like to present my personal opinion on the subject.

These days this task could easily be achieved with tools such as [FindBugs](http://findbugs.sourceforge.net/) and  [Checkstyle](http://checkstyle.sourceforge.net/). Here is an example Checkstyle XML configuration snippet:

{% gist 39ac59ebf2acdcce6490 %}

Both major build systems for Java, i.e. [Maven](https://maven.apache.org/) and [Gradle](http://gradle.org/), have plug-in support for Checkstyle and FindBugs, thus one could easily apply this rule as part of the build system. As I mentioned in a [previous post](http://blog.devng.com/2015/10/01/code-format-validation-nodejs-jsfmt/), I am in favour of such tools and their integration into the whole build and continuous integration process. However, my personal opinion is that it is a waste of time to declare __every local__ variable as final, sure it can optimize the compilation
a bit, but I believe that the visual clutter and added verbosity is not worth it. To quote the [Zen of Python](https://www.python.org/dev/peps/pep-0020/): _"Readability counts."_, and I personally read a lot more code than I write. Don't get me wrong, I would not mind an occasional use of `final` inside methods when it makes sense, but it is up to the developer and his reviewers to decide when this is necessary. Blindly enforcing this rule is not the way to go here. On the other side, some Java developers would argue that they prefer to have the `final` keyword whenever possible in order to have strict code and thus preventing logical errors. In my Java experience thus far I have never encountered a logical error just because of a lack of final variables. Usually the root cause for logical errors and bugs is the lack of code reviews and good automated tests.

I am curious to know what other developers think on the matter.
