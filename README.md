# Steps to create a new post:

## Git clone the repo

```bash
git clone https://github.com/YiweiShen/yiweishen.github.io.git
```

## Install dependencies

```bash
cd yiweishen.github.io
npm install
```

## Create a new post

```bash
npx hexo new post "Post Title"
```

## Edit the post

By default, the post is created in `source/_posts/Post-Title.md`. Edit the post in your favorite editor.

## Create a new git branch and push the changes

```bash
git checkout -b new-post
git add .
git commit -m "Add a new post"
git push origin new-post
```

## Create a pull request

Create a pull request on GitHub and merge it to the main branch. GitHub Actions will automatically build and deploy the site.
