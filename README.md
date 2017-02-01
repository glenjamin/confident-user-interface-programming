# Confident User Interface Programming

A talk at CodeMesh 2016 by [Glen Mailer](https://twitter.com/glenathan).

### Watch the recording

[![a Recording of the Talk](https://img.youtube.com/vi/62Y9JCOtzGY/0.jpg)](https://www.youtube.com/watch?v=62Y9JCOtzGY) 

https://www.youtube.com/watch?v=

## Introduction

The few iterations of this talk I've done to reach this point have had
very different names, as I've struggled to distill the idea down to
something pithy.

With this title I did specifically want to note that the title refers to
Confidence, and not correctness. Correctness is much harder, and pretty
hard to quantify in any meaningful way for a complicated user interface.

My personal belief is that confidence is best achieved through effective
feedback, and recently someone [wrote a medium thinkpiece][1hz] on the subject
which I thought was rather apt.

## The Talk

Here's a rough list of the things I talked about during my talk. There should
be a recording available soon, which I'll post here too.

 * Ways to acheive 1hz feedback, specifically for browser JavaScript.
   * Linting via [eslint][eslint].
     * Ideally with [tight editor integration][sublimelinter] for
       lint-as-you-type.
   * Fast unit tests -- averaging 1ms per test.
     * I like to use [mocha][mocha]
     * I like to use `--watch` and `--growl` to run the tests whenever files
       change, and see the feedback while keeping my editor in focus.
     * Some systems can go further, and use knowledge of the module dependency
      graph to only run tests relevant to your changes.

 * These approaches are fairly mainstream, although adoption for frontend
   JavaScript probably still lags behind popular backend development platforms.

 * Another related approach is [Hot Module Reloading][hmr], in this case
   provided by [Webpack][webpack] for my demo app [Emojifight][emojifight].
   * Changing CSS via web inspector is <1hz.
   * But making this change in our source code and reloading often isn't.
   * Good luck getting under 1hz for a change to JavaScript on page 4.
     * Make the change
     * Wait for the bundle to rebuild
     * Reload the page
     * Interact with the UI until you get back to the right state
     * Repeat
   * Hot Module reloading allows us to replace CSS and JS of a small portion of
     a running application while preserving the existing state - bringing us
     back under the magic 1Hz line we arbitrarily picked earlier.
   * Iteratively building our application becomes almost conversational, we can
     try things out and see how they look very quickly.

 * There's still some drawbacks here, our application is only ever in one state
   at once, if we want to see others we have to interact with it.

 * About a year ago I saw a [talk at Strangeloop][devcards-strangeloop] by a
   guy called Bruce Hauman about his tool [Devcards][devcards]. This presented
   an approach which gave us a way to see many states at once, building on the
   benefits of hot reloading. Unfortunately for me it was quite tied to
   ClojureScript, and my day job was not.

 * This led me to port the approach to JavaScript into a project called
   Devboard.
   * This portion of the talk consisted of a live demonstration of building up
     a component iteratively using the devboard as a development aid.
   * It's difficult to convey this experience via text, but please do take a
     look at
     * [The devboard project on github][devboard]
     * [The devboard example pages][devboard-example]
     * [The final thermometer widget][thermo] that was built.

[1hz]: https://medium.com/@MartinCracauer/software-development-at-1-hz-5530bb58fc0e
[eslint]: http://eslint.org/
[sublimelinter]: https://github.com/roadhump/SublimeLinter-eslint
[mocha]: http://mochajs.org/
[hmr]: http://webpack.github.io/docs/hot-module-replacement-with-webpack.html
[webpack]: http://webpack.github.io/
[emojifight]: https://github.com/glenjamin/emojifight
[devcards-strangeloop]: https://www.youtube.com/watch?v=G7Z_g2fnEDg
[devcards]: http://rigsomelight.com/devcards/#!/devdemos.core
[devboard]: https://github.com/glenjamin/devboard
[devboard-example]: http://glenjamin.github.io/devboard/
[thermo]: http://glenjamin.github.io/devboard/#/4.%20Thermometer%20demo
