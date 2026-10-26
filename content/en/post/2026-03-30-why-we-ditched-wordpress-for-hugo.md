---
title: "Hugo vs WordPress: How We Run a Bilingual Blog on GitHub Pages"
date: 2026-03-30
lastmod: 2026-10-05T13:46:25+09:00
draft: false
authors: ["tikklabs-editor"]
categories: ["Blog Operations"]
tags: ["Hugo", "GitHub Pages", "SEO"]
slug: "2026-03-30-why-we-ditched-wordpress-for-hugo"
translationKey: "hugo-operations"
featureimage: "img/editorial/hugo.webp"
images: ["img/editorial/hugo.webp"]
description: "A factual look at the Tikklabs Hugo setup, its deployment checks, multilingual settings and maintenance trade-offs versus WordPress."
showToc: true
---

Tikklabs runs a bilingual blog using **Hugo, the Blowfish theme and GitHub Pages**. This is a description of the current setup, not a claim that we operated a WordPress site and migrated it.

Hugo is not the best choice for every publisher. Publishing can be automated, but theme changes, build failures and search settings still need an operator. Here is what this setup actually does and how its maintenance differs from WordPress.

## How a post reaches this website

1. Update the source article and images in the repository.
2. GitHub Actions runs Hugo to generate HTML.
3. After a successful build, GitHub Pages publishes the generated files.
4. Check the live article, images and links at their real URLs.

Changing a repository file is different from publishing a page. If deployment fails, visitors may still see the previous version. **Checking the live page** is the final step.

![From editing an article to checking the published page](img/editorial/hugo-publish-en.svg "The current Tikklabs publishing flow.")

## Hugo and WordPress maintain different things

| Area | Hugo + GitHub Pages | WordPress |
|---|---|---|
| Editing | Files, with an editor or automation | Primarily the admin editor |
| Serving pages | Prebuilt static files | Server-generated or cached pages |
| Server maintenance | Static deployment pipeline | Hosting, PHP and database environment |
| Additional features | Templates, external services or development | Plugins and other integrations |
| Cost comparison | Domain, external features and maintenance | Hosting, domain, paid features and maintenance |

A well-configured WordPress site can be fast. A Hugo site can still be slowed by large images, advertising and scripts. Compare actual pages with comparable features rather than treating the generator as a performance guarantee.

## Search settings we actually manage

### Production URLs and sitemaps

The production `baseURL` is `https://tikklabs.com/`. We check that local-development URLs do not appear in deployed sitemaps.

The Korean and English sitemaps include published articles and core pages such as the topic guide. Automatic tag, category, series and author listings are excluded and carry `noindex, follow`. This is a choice for the current content structure, not a universal requirement.

### Corresponding language pages

Related translations share a `translationKey`. Hugo uses that relationship to supply language links and alternate-page information. We verify the resulting English and Korean pages rather than checking only the source field.

`hreflang` identifies corresponding language versions; it is not a ranking score or forced redirect. The optional `x-default` value identifies a fallback for unmatched languages or regions. We do not claim an implementation that the site does not contain.

### Internal links and publishing state

Keep existing URLs when updating titles. Links need the actual published path, including `/post/` where applicable. A link to an unpublished draft cannot supply the explanation a reader expects.

## What this architecture cannot guarantee

Prebuilt pages reduce the need to assemble article content from a database on each visit. They do not eliminate risks in repository accounts, deployment permissions, third-party scripts or integrated services.

Hugo does not guarantee a perfect Lighthouse score or high search rankings. Check performance after adding images or advertising, including on mobile. Useful content and reliable navigation remain publishing responsibilities.

## Who may prefer this setup

File-based publishing can suit an informational blog with automated production and relatively few interactive features. WordPress may be more convenient for teams that want an admin editor and extensive plugin workflows.

For Tikklabs, updating content, generating the site, deploying and checking the live page belong to one publishing task. The useful comparison is whether the maintenance process supports consistent, helpful articles.

### References

- [Hugo deployment on GitHub Pages](https://gohugo.io/host-and-deploy/host-on-github-pages/)
- [Hugo multilingual content](https://gohugo.io/content-management/multilingual/)
- [Google language-version guidance](https://developers.google.com/search/docs/specialty/international/localized-versions)
- [Tikklabs source repository](https://github.com/Tikklabs-editor/rohbomb.github.io)

[Start with the topic guides](/guides/)
