---
layout: post
title: Steve Yegge endorses Kotlin so maybe I should try it?
---

## Pontifications

* Followup to yesterday's [How difficult is it to make Kotlin CLI or UI-less apps for Android?](http://rolandtanglao.com/2017/05/22/p1-kotlin-for-android-cli-apps/), maybe I should try it since Steve Yegge endorses it?!?
* From [Why Kotlin Is Better Than Whatever Dumb Language You're Using](https://steve-yegge.blogspot.ca/2017/05/why-kotlin-is-better-than-whatever-dumb.html)

**QUOTE**

<blockquote>

"**It works like Java**.  It's not "weird" like Clojure or Scala (and let's face it, they're both pretty weird.)  You can learn it quickly.  It was obviously designed to be accessible to Java developers.<br /><br />
    
**It's safer than Java**.  It provides built-in support for many things that are handled in Java these days with annotation processors -- override checking, nullability analysis, etc.  It also has safer numeric conversion rules, and although I'm not sure I like them, I have to appreciate how they force me to think about all my number representations.<br /><br />
    
**It's interoperable with Java**.  And I mean their interop is flawless.  I've seen too many JVM languages go down in flames because you couldn't subclass, I dunno, a static inner class of a nonstatic inner class, or whatever weird-ass edge case you needed at the time.  Kotlin has made Java interop a top priority, which means migration to Kotlin can be done incrementally, one file at a time.<br /><br />
    
**It's succinct**.  I'm a bit of a golfer, I'll be honest.  All else being equal, I like shorter programs that do the same thing, if they're clear enough.  Kotlin makes for a great round of golf.  On average I find it to be about 5-10% shorter than the equivalent Jython code (which is sort of my gold standard), while remaining more readable and far more typesafe.<br /></br />

**It's practical**.  Kotlin allows multiple classes per file, top-level functions, operator overloading, extension methods, type aliasing, string templating, and a whole bunch of other bog-standard language features that for whatever reason Java just never adopted even though everyone wanted them.<br /><br />
    
**It's evolving fast**.  For instance they just launched coroutine support, which is going to provide the foundation for async/await, generators and all your other favorite non-threaded concurrency features.<br /><br />
    
**It's unashamed**.  Kotlin often borrows great ideas from other languages, and doesn't try to hide it.  They'll say, "We liked C#'s generics, so we did it that way."  I like that.<br /><br />
    
**It's got DSLs**.  No DSL should ever be created without serious consideration of the alternatives -- but a DSL done well can be a powerful tool.  Look at Gradle's DSL, for instance, in comparison to the thousands of lines of XML in a typical Maven project.  Kotlin makes that kind of thing easy.<br /><br />
    
**It's got one hell of an IDE**.  Lately I've taken to writing new files in Emacs, which lets me bust out a ton of code very quickly, code which just happens to be full of horrible errors.  And then I open it in IntelliJ and hit Alt-Enter like 50 times while the IDE fixes everything for me.  It's a great symbiosis.<br /><br />
    
**It's fun**.  Kotlin is just plain fun.  Maybe it's subliminal advertising, since their keyword for declaring methods is fun.  But it's somehow turned me from a surly professional programmer into a hobbyist again."

</blockquote>

**END QUOTE**