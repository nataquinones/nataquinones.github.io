# HOWTO
## 1. Create `Gemfile` in directory
`bundle init`

## 2. Add `jekyll` as a dependency in the `Gemfile`
`gem "jekyll"`

## 3. Build the site: outputs a static site to a directory called `_site`.
`jekyll build`

## 4. Does the same thing except it rebuilds any time you make a change and runs a local web server at.
`jekyll serve`