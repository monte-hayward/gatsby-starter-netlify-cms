---
templateKey: blog-post
title: 'Quick Add : Blog'
date: 2019-07-02T20:01:01.292Z
description: >-
  Content Manager offers quick add for blog posts and not site pages, as
  configured.
featuredpost: true
featuredimage: /img/chemex.jpg
tags:
  - quickadd
---
Body: Derpderp types stuff sometimes.

Content Manager offers quick add for blog posts and not site pages, as configured. Blog posts all have the same set of fields. They are a NetlifyCMS `folder collection`. They can have attribute `create: true`, allowing content admins to create new blog pages.

The Pages collection is a `files` collection. These contain "one or more uniquely configured files", according to [docs on Collection Types](https://www.netlifycms.org/docs/collection-types). The example configuration is shown below.

Other pages in this example site are contructed without NetlifyCMS. E.g., the Contact directory has 3 gatsby pages in `.js` format. Page text (copy) is embedded in the JavaScript in these files.

```yaml
backend:
  name: git-gateway
  branch: master

media_folder: static/img
public_folder: /img

collections:
  - name: "blog"
    label: "Blog"
    folder: "src/pages/blog"
    create: true
    slug: "{{year}}-{{month}}-{{day}}-{{slug}}"
    fields:
      - {label: "Template Key", name: "templateKey", widget: "hidden", default: "blog-post"}
      - {label: "Title", name: "title", widget: "string"}
      - {label: "Publish Date", name: "date", widget: "datetime"}
      - {label: "Description", name: "description", widget: "text"}
      - {label: "Featured Post", name: "featuredpost", widget: "boolean"}
      - {label: "Featured Image", name: "featuredimage", widget: image}
      - {label: "Body", name: "body", widget: "markdown"}
      - {label: "Tags", name: "tags", widget: "list"}

  - name: "pages"
    label: "Pages"
    files:
      - file: "src/pages/index.md"
        label: "Landing Page"
        name: "index"
        fields:
          - {label: "Template Key", name: "templateKey", widget: "hidden", default: "index-page"}
          - {label: Title, name: title, widget: string}
          - {label: Image, name: image, widget: image}
          - {label: Heading, name: heading, widget: string}
          - {label: Subheading, name: subheading, widget: string}
          - {label: Mainpitch, name: mainpitch, widget: object, fields: [{label: Title, name: title, widget: string}, {label: Description, name: description, widget: text}]}
          - {label: Description, name: description, widget: string}
          - {label: Intro, name: intro, widget: object, fields: [{label: Heading, name: heading, widget: string}, {label: Description, name: description, widget: text}, {label: Blurbs, name: blurbs, widget: list, fields: [{label: Image, name: image, widget: image}, {label: Text, name: text, widget: text}]}]}
          - {label: Main, name: main, widget: object, fields: [{label: Heading, name: heading, widget: string}, {label: Description, name: description, widget: text}, {label: Image1, name: image1, widget: object, fields: [{label: Image, name: image, widget: image}, {label: Alt, name: alt, widget: string}]}, {label: Image2, name: image2, widget: object, fields: [{label: Image, name: image, widget: image}, {label: Alt, name: alt, widget: string}]}, {label: Image3, name: image3, widget: object, fields: [{label: Image, name: image, widget: image}, {label: Alt, name: alt, widget: string}]}]}
      - file: "src/pages/about/index.md"
        label: "About"
        name: "about"
        fields:
          - {label: "Template Key", name: "templateKey", widget: "hidden", default: "about-page"}
          - {label: "Title", name: "title", widget: "string"}
          - {label: "Body", name: "body", widget: "markdown"}
      - file: "src/pages/products/index.md"
        label: "Products Page"
        name: "products"
        fields:
          - {label: "Template Key", name: "templateKey", widget: "hidden", default: "product-page"}
          - {label: Title, name: title, widget: string}
          - {label: Image, name: image, widget: image}
          - {label: Heading, name: heading, widget: string}
          - {label: Description, name: description, widget: string}
          - {label: Intro, name: intro, widget: object, fields: [{label: Heading, name: heading, widget: string}, {label: Description, name: description, widget: text}, {label: Blurbs, name: blurbs, widget: list, fields: [{label: Image, name: image, widget: image}, {label: Text, name: text, widget: text}]}]}
          - {label: Main, name: main, widget: object, fields: [{label: Heading, name: heading, widget: string}, {label: Description, name: description, widget: text}, {label: Image1, name: image1, widget: object, fields: [{label: Image, name: image, widget: image}, {label: Alt, name: alt, widget: string}]}, {label: Image2, name: image2, widget: object, fields: [{label: Image, name: image, widget: image}, {label: Alt, name: alt, widget: string}]}, {label: Image3, name: image3, widget: object, fields: [{label: Image, name: image, widget: image}, {label: Alt, name: alt, widget: string}]}]}
          - {label: Testimonials, name: testimonials, widget: list, fields: [{label: Quote, name: quote, widget: string}, {label: Author, name: author, widget: string}]}
          - {label: Full_image, name: full_image, widget: image}
          - {label: Pricing, name: pricing, widget: object, fields: [{label: Heading, name: heading, widget: string}, {label: Description, name: description, widget: string}, {label: Plans, name: plans, widget: list, fields: [{label: Plan, name: plan, widget: string}, {label: Price, name: price, widget: string}, {label: Description, name: description, widget: string}, {label: Items, name: items, widget: list}]}]}
```

