# [This website](http://zyang.ca) is powered by hugo,github pages and github action.

## Writing a post
Just add the post to the github repo, when github receive any commit, the github action will run automatively.
All the generated contents will be added to the gh-pages branch.

## Add a domain name
- In the gh-pages branch, add a file named `CNAME` with the doamin name.
- From your domain provider(Godaddy), config the A record to github's IP.


The github action code.
```yaml
# Workflow to build and deploy site to Github Pages using Hugo

name: github pages

on:
  push:
    branches: [ master ]

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v2
      with:
          submodules: true  # Fetch Hugo themes
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

    # Step 2 - Sets up the latest version of Hugo
    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
          hugo-version: 'latest'

    # Step 3 - Clean and don't fail
    - name: Clean public directory
      run: rm -rf public

    # Step 4 - Builds the site using the latest version of Hugo
    # Also specifies the theme we want to use
    - name: Build
      run: hugo --theme=PaperMod

    # Step 5 - Create name file
    - name: Create cname file
      run: echo 'zyang.ca' > public/CNAME

    # Step 6 - Push our generated site to our gh-pages branch
    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
  ```
