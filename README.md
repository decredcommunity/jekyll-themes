# The Primer Light theme patch

Files in this directory configure [Jekyll](https://jekyllrb.com/) and [GitHub Pages](https://pages.github.com/) to build a Markdown-based website.

The files are based on the [Primer theme](https://github.com/pages-themes/primer) for GitHub Pages (which is the default as of 2020). Notable differences:

- removed Cloudflare and Google tracking from `_layouts/default.html`
- removed unwanted `h1` title block from `_layouts/default.html`
- removed import of `rouge` syntax highlighting from `_sass/jekyll-theme-primer.scss`
- import of `primer-utilities/index.scss` reduced to importing only padding and margin bits in `_sass/jekyll-theme-primer.scss`
- the final CSS size is reduced from 72 to 44 KiB
- link style is set to have no `.html` extension via the `permalink: :title` [directive](https://jekyllrb.com/docs/permalinks/) in `_config.yml`

All changes above are done as patches on top of the Primer theme code. You can inspect each patch by reading Git history of this directory.

Jekyll stuff is deliberately extracted into its own mini-repo to keep Markdown content repositories independent from site building code. As a bonus, it makes this Jekyll config reusable.

## Usage

The naive way is to copy `_layouts`, `_sass` and `_config.yml` from this directory to the repository from which you build your Pages site, and set your title in `_config.yml`.

A slighly more advanced way is to use Git.

Keeping these files in a standalone ([orphan](https://git-scm.com/docs/git-checkout#Documentation/git-checkout.txt---orphanltnewbranchgt)) Git branch allows to easily copy it to any Markdown repository where you need it.

These commands will add a remote named `jekyllthemes` that only tracks one branch `primerlight` with Jekyll files:

    $ git remote add -t primerlight jekyllthemes https://github.com/decredcommunity/jekyll-themes.git
    $ git fetch jekyllthemes

Then whenever you need to build your Pages site you can checkout the Jekyll files among other build steps:

    $ git checkout jekyllthemes/primerlight _layouts _sass _config.yml

And finally edit `_config.yml` to set your own `title`.
