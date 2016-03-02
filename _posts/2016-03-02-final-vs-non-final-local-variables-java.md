---
layout:     post
title:      My Opinion on Final vs. Non-Final Local Variables in Java
date:       2016-03-02
summary:    In my company we had a discussion about whether we should enforce the use of the final keyword for local variables in Java or not. In this blog post I would like to present my personal opinion on the subject.
tags: java checkstyle
---

In my company we had a discussion about whether we should enforce the use of the `final` keyword for local variables in Java or not. In this blog post I would like to present my personal opinion on the subject.

These days this task could easily be achieved with tools such as [FindBugs](http://findbugs.sourceforge.net/) and  [Checkstyle](http://checkstyle.sourceforge.net/). Here is an example Checkstyle XML configuration snippet:

{% gist 39ac59ebf2acdcce6490 %}

Both major build systems for Java [Maven](https://maven.apache.org/) and [Gradle](http://gradle.org/) have plug-in support for Checkstyle and FindBugs, thus one could easily enforce this rule as part of the build system. As I mentioned in a [previous post](http://blog.devng.com/2015/10/01/code-format-validation-nodejs-jsfmt/), I am in favour of such tools and their integration into the whole build and continuous integration process. However, my personal opinion is that it is a waste of time to declare every local variable as final, sure it can optimize the compilation and code execution a bit, but I believe that the visual clutter and added verbosity is not worth it. To quote the [Zen of Python](https://www.python.org/dev/peps/pep-0020/): "Readability counts.", and I personally read a lot more code than I write. On the other side, some Java developers would argue that they prefer to have the `final` keyword whenever possible in order to have clean and strict code and thus preventing logical errors. In my experience, however, I have never encountered a logic error just because of a lack of final variables. Usually the root cause for logical errors is the lack of code reviews and good tests.

I am curious to know what other developers think on the matter.
