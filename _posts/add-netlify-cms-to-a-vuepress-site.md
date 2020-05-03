---
title: Add Netlify CMS to your VuePress site
date: 2020-05-03T14:46:47.996Z
thumbnail: /media/workflow.png
tags:
  - VuePress
  - Netlify
  - Netlify CMS
---
If you're using VuePress, but you want to add a bit of content management to your markdown files, Netlify CMS is the perfect choice. 

It's a light-weight CMS hosted on your site that hooks directly into your Git repo, creating branches for drafts and merging your content into master when you click to publish. What I love about this CMS is that I still have complete control of my content. No vendor lock-in. No databases. Just some helpful tools to manage your markdown files, including:

* Rich text editing and preview for your markdown files
* Publishing workflow to manage content (draft, review, ready, publish and unpublish)
* Configurable inputs and defaults for your [frontmatter](https://v1.vuepress.vuejs.org/guide/frontmatter.html)
* Multiple author access controls ([with Netlify Identity](https://docs.netlify.com/visitor-access/identity/))

![Rich text editor screen](/media/cmseditor.png)

If you don't already have a VuePress site, or if you just want to play with Netlify CMS, I've made a [GitHub template](https://github.com/petedavisdev/VuePress-with-Netlify-CMS) for you which you can deploy using this magic button:

<a href="https://app.netlify.com/start/deploy?repository=https://github.com/petedavisdev/VuePress-with-Netlify-CMS&amp;stack=cms"><img src="https://www.netlify.com/img/deploy/button.svg" alt="Deploy to Netlify"></a>

If you do already have a VuePress site and you want to add Netlify CMS, this tutorial is for you.

## Setup OAuth on GitHub

To keep it simple for now, we are going to set up access to the CMS with GitHub

1. Go to your [developer settings on GitHub](https://github.com/settings/developers) and add a new OAuth app.
2. Enter the name and full URL of your website and set the authorization callback URL:

```
https://api.netlify.com/auth/done
```

3. Click Register application to get your Client ID and Client Secret. You will need these in a moment.
4. In your site Settings, open 'Access control'. Under OAuth, click 'Install provider' and copy in the Client ID and Secret from [GitHub](https://github.com/settings/developers).

## Add Netlify CMS admin files to your project

In your `.vuepress` folder, add a `public` folder and within that, add an `admin` folder where you will add two files:

1. `index.html`

<<< @/.vuepress/public/snippets/admin.index.html

2. `config.yml`

<<< @/.vuepress/public/snippets/admin.config.yml

This config will enable you to edit your homepage, but not delete it. It will also give you the ability to create, edit and delete pages. It will manage pages in a `_pages` folder, so edit this if you have a different folder for your pages.

## Login to your CMS and create pages

With these files deployed, you can now access your CMS. Simply add \`/admin\` to the end of your website url in the browser and you will be invited to login with GitHub. Once logged in you will see a collection called Home, which contains your homepage and a collection called Pages, which will be empty or contain your existing pages.

![CMS Contents screen](/media/collections.png)

Now you can start using the CMS to edit and add pages.

Be aware that new pages do not appear in the pages list or on your website until they have been published, and they cannot be published until they have been marked as "Ready", so go to the workflow tab to edit your drafts.

![Workflow screen](/media/workflow.png)

Try creating some new pages (e.g. About and Contact) and see the new branches that appear automatically in your Git repo. Netlify will publish these branches as previews, so that you can see exactly how your website will look once they have been published.

![View Preview link](/media/viewpreview.png)

Set these pages as ready and then publish them. This merges the branch to master, so Netlify will build and deploy your site with your new pages, but you'll need some navigation to get to them.

Open up your `.vuepress/congif.js` file and add the following theme config:

<<< @/.vuepress/public/snippets/vuepress.config.js{4-10}

Now you can get to the pages you created with your CMS.

## Next...

[Netlify CMS docs](https://www.netlifycms.org/docs/intro/)

[Netlify Identity docs](https://docs.netlify.com/visitor-access/identity/)

<TinyLetter />