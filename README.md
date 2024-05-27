## WonderMod (PaperMod fork - theme for Hugo)

<p align="center">
  <img src="https://raw.githubusercontent.com/wonderfall/hugo-WonderMod/master/.github/assets/web-capture.jpeg" title="WonderMod" alt="WonderMod image">
</p>

### What is this?
WonderMod is a fork of an original theme for [Hugo](https://gohugo.io/) called [PaperMod](https://github.com/adityatelange/hugo-PaperMod) (made by adityatelange). Since PaperMod isn't interested in a few changes such as **removing inline JavaScript**, which I personally require to harden my websites, I decided to maintain my own fork (I didn't want to keep overwriting a bunch of files as a fork workflow is much cleaner). Don't expect a ton of changes, and unless you know me, you probably don't want to use WonderMod.

When implementing new features, I try to do as much as I can with pure CSS code instead of adding new JavaScript code. I'd like to keep the JavaScript part minimal and that's why WonderMod should be totally usable when disabling JavaScript. WonderMod is also designed with strong CSP headers in mind: no inline JavaScript or style, no calls to third-parties.

**This fork is regularly synced with upstream changes from [PaperMod](https://github.com/adityatelange/hugo-PaperMod).** A merging workflow was chosen since rebasing WonderMod's changes every time could be less efficient. As such, commit history is a bit messy, but upstream changes will be merged on a best effort basis.

### Main changes
Current "main" changes are as follows:
- Remove inline JavaScript
- Improved YouTube shortcode
- Built-in Chroma instead of client-side syntax highlighting with HLJS
- Responsive Table of Contents with side display support
- Responsive "hamburger" menu for mobile
- Image optimization with next-gen image formats
- Simple reading progress bar
- Refactored RSS template (proper Atom feed)
- Bunch of CSS and other changes

### Image Optimization

Images are optimized by default without requiring
[shortcodes](https://gohugo.io/content-management/shortcodes/), by using a [custom](./layouts/_default/_markup/render-image.html) image [render hook](https://gohugo.io/getting-started/configuration-markup#markdown-render-hooks), which in turn uses the [image partial](./layouts/partial/image.html) that does all the heavy lifting.

By default, the theme creates resized versions of images ranging from 300 to 700 pixels wide in increments of 100 pixels.

If the image format is not [WebP](https://en.wikipedia.org/wiki/WebP), the image is converted. The original file format will serve as a fallback for browsers that don't support the WebP format.

Note that only images that are part of the [page bundle](https://gohugo.io/content-management/page-bundles/) are processed.
If served from the `static/` directory or external sources, the image will be displayed but not be processed.

Additionally, all images are lazily loaded to save the bandwidth of your users.

### Credits
Additional credits:
- [PaperModX](https://github.com/reorx/hugo-PaperModX/) by reorx
- [Hugo Gruvbox](https://github.com/schnerring/hugo-theme-gruvbox) theme (Image Optimization code)

### Configure
Most of the installation process and settings are shared with the original PaperMod, so check out [their documentation](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation). The noticeable differences though are the additional `config.yml` options:
- in order to enable syntax highlighting, add:

  ```
  markup:
      highlight:
          style: dracula
          noClasses: false
          guessSyntax: true
  ```

  See [Hugo documentation](https://gohugo.io/getting-started/configuration-markup#highlight) for more options.
  *Note: for some reason, the `guessSyntax` doesn't actually work but is required. Please make your code fences explicit for the time being.*

- to change the image compression quality from the default 75%, per the [official Image Processing Config Hugo docs](https://gohugo.io/content-management/image-processing/#image-processing-config):

  ```yaml
  imaging:
    quality: 75
  ```

- to change the default resize behavior:

  ```yaml
  params:
    imageResize:
      min: 300
      max: 700
      increment: 100
  ```
