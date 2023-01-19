# Documentation

I love documentation. But also, documentation is the worst. Making documentation is hard. [Making great documentation](diataxis-divio-quickstart.md) even harder. But it is instrumental to helping your code be useful to people that aren't you, and that's a worthwhile pursuit! Even if you're making things just for yourself, the `people that aren't you` descriptor also includes you in a few years/months/weeks, who has no idea what you were even thinking.

These are the notes that I'm making while reworking the documentation for [semantic.works](https://semantic.works).

## Design principles
1. *Don't Repeat Yourself.* If we're copying documentation across places, we're doing something wrong.
2. *Good.* The Divio documentation principles should apply.
3. *Ease of use: writers.* Minimising maintenance for the people who make the code is essential. Having them sign in to a whole different platform to write the documentation for their code would be way too much friction.
4. *Ease of use: readers.* We have a bunch of projects going on, written in Ruby, Lisp, Elixer, JavaScript, Python... The documentations should resemble eachother and be consistent.
5. *Micro-first.* Semantic.works is about microservices, so that means there'll be a bunch of documentation which is **small**. And that's okay! But it is important to not build the base structure to accommodate big projects. A documentation folder for something that can be explained in one README is a no-go. Start from a single file, and expand only if necessary.


## Attempt A: automated generation
There are a doc generators! JSDoc is my favourite just for its syntax alone.
But ruh roh, did you read the first two letters of that name? A lock-in to a programming language. Yes, we could find a documentation generator for every language we use, but then we will semi-break `3.`, but mostly full break `4.`. Unless we morph every of those generators to the same output. Also breaking `4.`.

How about the general purpose ones?
Yes! There are two really cool options. First was Doxygen: a seemingly cool tool with a bunch of supported languages! But a few of our common ones are missing, so I feel like a fool.

Then Dexy. You can see the remains of my tests with it (including Dockerising it) in [Other/dexy/](Other/dexy/). But to give you the gist: it is a super extendible and really cool amalgemation of text processing, bundled into a pretty easily configurable yaml. Jinja, pandoc and markdown are but a few of the [impressive list of built-in tools](https://dexy.github.io/dexy-user-guide/#_filter_documentation). Sadly, while it can run a bunch of languages and grab the output, it seems to lack the ability to dissect the code you give it in any meaningful ways. This bundled with a website that is split across domains and a lack of updates in the last few years, make it sub-ideal for what I'm trying to do.





