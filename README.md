# README

This repo is a minimal reproduction of a funky bug.

Steps to Reproduce:
- Clone this repo
- Run the rails server locally
- Visit the root url

```bash
git clone git@github.com:wenley/ViewComponent-3.5.0-bug.git
cd ViewComponent-3.5.0-bug
bundle
rails s -3000
open http://localhost:3000/
```

## Bug Description

When a component defines a `render_one` with a slot name starting with `call`, the app will crash when attempting to render.

This started as of v3.5.0 and does not occur with v3.4.0.

[This is the specific line](https://github.com/ViewComponent/view_component/commit/425338ffc99d59c335ccd82f95ba17135ab18be9#diff-fa28fa6e2d5f267384e7793b855281451a46b8437431867871a298fc52fe4940R99) where the app crashes, but the root cause appears to be the slot name being caught by [the logic to find "inline calls"](https://github.com/ViewComponent/view_component/blob/425338ffc99d59c335ccd82f95ba17135ab18be9/lib/view_component/compiler.rb#L222).
