---
layout:     post
title:      Continuous Integration with Source Code Format Validation for Node.js Using jsfmt
date:       2015-10-01
summary:    Recently I started exploring Go and Node.js on different projects. Soon I found out that there are some things which I really like about Go, but are missing on Node.js, such as the gofmt tool. Gofmt is a tool that automatically formats Go source code. The nice thing about it is that endless discussions among your team members on how the source code should be formatted are more or less a thing of the past. So I started looking for similar tools for Node.js and I found jsfmt, which is beautifier/formatter for JS, but it can also validate JS code formatting. Great, exactly what I was looking for.
tags: javascript nodejs bash ci
---

Recently I started exploring Go and Node.js on different projects. Soon I found out that there are some things which I really like about Go, but are missing on Node.js, such as the `gofmt` tool.
[Gofmt](https://golang.org/cmd/gofmt/) is a tool that automatically formats Go source code. The nice thing about it is that endless discussions among your team members on how the source code should be formatted are more or less a thing of the past. However, such discussions among JavaScript (JS) developers are not uncommon and can take hours, which is very counterproductive. This is especially painful when people start reformatting other people’s source code, because then they are messing up the git history and git blame becomes useless. IMHO people in one team should agree on some code styling rules and follow them. I as a Java developer am used to this, because in almost every big Java project on which I have worked uses [checkstyle](https://github.com/checkstyle/checkstyle) and incorporates this into the
Continuous Integration (CI) build, thus if you are not following the checkstyle rules your build will not pass the CI. Problem solved.

So I started looking for similar tools for Node.js and I found [jsfmt](https://github.com/rdio/jsfmt), which is beautifier/formatter for JS, but it can also validate JS code formatting. Great, exactly what I was looking for. The problem is that `jsfmt` works on individual files, so I wrote a simple bash script called `checkfmt-js.sh` which will check the format of all `*.js` and `*.json` files in your Node.js project:

{% gist e081028122f574187a50 %}

This shell script only validates your JS source code, it does not change it. It also skips all automatically downloaded packages in the _node_modules_ sub-folder.

Note that if you are not happy with the presets of `jsfmt` you can overwrite them via a `.jsfmtrc` file.

## CI Integration

With the help of the `checkfmt-js.sh` script we can integrate source code format validations as part of our CI build, so that the build will fail if the developer submits a malformated JS/JSON file. Here is a sample configuration for [Travis CI](https://travis-ci.org/) or [Vexor CI](https://vexor.io/) for accomplishing this task:

{% gist d85752dfb4577bb6fb20 %}

## Auto Format

Of course you also want to format your files with `jsfmt`, so that your CI build does not fail all the time. To do this  with `jsfmt`  on a single JS file use:

```
jsfmt -w my-source-file.js
```

For a JSON file make sure to add the `-j` flag too.

If you are using the [Atom](https://atom.io) editor you can install the _atom-jsfmt_ plugin, which will auto-format your JS code every time you save, so you don't have to think about it.

```
apm install atom-jsfmt
```

Alternatively, you can use the following `fmt-js.sh` script to format of all `*.js` and `*.json` files in your Node.js project:

{% gist 46e20596c7c7cadb02b9 %}

## Alternatives

As an alternative to _jsfmt_ one can also use [JSCS — JavaScript Code Style](http://jscs.info), which is a code style linter for programmatically enforcing your style guide. It can also auto-format your JS files.  _Jscs_ has more features and configuration options than _jsfmt_. However, I like the simplicity of _jsfmt_ and the fact that it is very similar to _gofmt_, which makes the tool switching between Go and Node.js a bit easier.

## Conclusion
In conclusion, I believe that imposing the same code format for all developers is a good idea. It makes the source version control history more meaningful. In addition, it stops the pointless source code style wars, and good programmers can focus more on what really matters - programming. Therefore source code formatting validation should be part of your CI build.
