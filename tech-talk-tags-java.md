## [Testing class compatibility with isAssignableFrom](/tech-talk/2024/05/10/is-assignable-from.md)

May 10, 2024 ·

<!-- -->

4 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

info

This post is from JsPlumb, which is now in maintenance mode. We still use this code in VisuallyJs though.

Classes are a controversial topic in the Javascript/Typescript world. Are they a terrible idea? Are they really useful, when used sensibly? This post will make no attempt at answering either of these questions. This post is about a niche method that I first encountered many years ago in the world of Java - `isAssignableFrom` - and how you can go about writing it for use in Typescript/Javascript.

### What does it do?[​](#what-does-it-do "Direct link to What does it do?")

This is what the Javadocs have to say about it:

So, given some class, you can use `isAssignableFrom` to figure out whether that class is a subclass of some other class.

### Why would I need this?[​](#why-would-i-need-this "Direct link to Why would I need this?")

If you're thinking it's a bit niche, yes, I agree. `isAssignableFrom` is one of those methods you don't use much. But when you need it, you need it.

**Tags:**

* [typescript](/tech-talk/tags/typescript.md)
* [java](/tech-talk/tags/java.md)
* [class](/tech-talk/tags/class.md)
* [interface](/tech-talk/tags/interface.md)
* [inheritance](/tech-talk/tags/inheritance.md)

[**Read more**](/tech-talk/2024/05/10/is-assignable-from.md)
