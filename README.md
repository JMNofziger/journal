# Journal

Here is the flow for publishing in case you forget:
https://gohugo.io/tutorials/github-pages-blog/

Here's the flow because you do forget:
```shell
echo "Deleting old publication"
rm -rf public
mkdir public
git worktree prune
rm -rf .git/worktrees/public/

echo "Checking out gh-pages branch into public"
git worktree add -B gh-pages public origin/gh-pages

echo "Removing existing files"
rm -rf public/\*

echo "Generating site"
hugo

echo "Updating gh-pages branch"
cd public && git add --all && git commit -m "Publishing to gh-pages"
git status
echo "If things look good, then git push"
```
