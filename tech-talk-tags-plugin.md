## [Docusaurus JSON environment loader](/tech-talk/2022/07/26/docusaurus-env-loader-json-plugin.md)

July 22, 2022 ·

<!-- -->

2 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

info

This post is from JsPlumb, which is now in maintenance mode. We still use this plugin in the VisuallyJs site though.

JsPlumb uses [Docusaurus](https://docusaurus.io/), a super handy static site generator, for various parts of our ecosystem, including our [Documentation](https://docs.jsplumbtoolkit.com) and also our recently released [stand alone components](https://components.jsplumbtoolkit.com) product.

While developing the site for JsPlumb Components, we wanted to include a couple of pieces of information that would vary depending on whether we were running in development mode locally (ie `docusaurus start`) or building for production. We looked into the various options available, all based on the `dotenv` plugin for Webpack, but couldn't find what we were looking for: a solution that worked, with minimal manual intervention, in both development mode and when building for production.

So we ended up building our own plugin. This plugin reads values from a JSON file and makes them available to your site via the `customFields` map in the Docusaurus `siteConfig`.

note

When I say "Docusaurus" in this post I am talking about v2/v3. I've not used v1.

**Tags:**

* [community](/tech-talk/tags/community.md)
* [toolkit](/tech-talk/tags/toolkit.md)
* [plugin](/tech-talk/tags/plugin.md)
* [docusaurus](/tech-talk/tags/docusaurus.md)

[**Read more**](/tech-talk/2022/07/26/docusaurus-env-loader-json-plugin.md)
