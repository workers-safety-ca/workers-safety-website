# Workers' Health and Safety Legal Clinic website

## Website Automation
This repository is used to manage a static website hosted on Github pages. It is deployed using Github Actions to run `hugo`.

## Hugo
The site is built using the static site generator [Hugo](https://gohugo.io/). The main site config is in `config.toml`.

## This repository builds and deploys automatically using Github Actions.
The `.github/workflows/hugo.yaml` defines the Github Actions to build and publish the website. Check the configuration for the version of Hugo for building. The site configuration must use variables that are supported by the version of Hugo in that config. The config can be updated to support a [newer version of Hugo](https://github.com/gohugoio/hugo/releases).

## Website: development and publishing

### Pages
To work with the site content, get to the repository root directory. Edit a page within the `content/` directory or copy an existing one and save it to a directory within it.

### Data/snippets
The `data/` directory holds "snippets" that are placed into "lists" within other pages, such as the carousel and features section on the homepage.

### Static files
Images and files are placed in the `static/` directory. When the site is build these get copied to the site root as-is. So `static/img/` gets copied to `img/`. Images which are necessary for the look and feel of the website should be placed in the repo here.

### Newsletters and archives
Newsletter and archive files (mostly pdfs, some images) are stored in AWS S3. After they are uploaded to AWS S3 in the newsletter.workers-safety.ca bucket, the URL is copied (like `https://s3.amazonaws.com/newsletter.workers-safety.ca/*`) and put into a page in this repo.

The repo contains a copy of a small script which is hosted on the AWS S3 bucket to create a GUI for navigating the archive list. It's clunky but it works. There's no easy way to get https on a whole S3 bucket, just the individual objects.

### Publishing
Whenever any file is saved in this repo, the site will get regenerated and published. There is an "Actions" tab on the repo where you can view the progress of the rebuild. It should typically take less than two minutes.

## Staging website
If there are any changes which you'd like to view before publishing, you can make them on the [fork](https://github.com/workers-safety-ca/workers-safety-test). After making the change there it can be viewed on [the staging site](https://staging.workers-safety.ca/). The staging site is public (it costs money to get the option to publish them privately). But after the changes have been reviewed, you can unpublish the staging site by going to the [settings](https://github.com/workers-safety-ca/workers-safety-test/settings/pages), clicking the three dots next to the "Your site is live at ..." and click Unpublish site. It will be rebuild the next time a change is made.

### Getting changes from staging to live
This workflow involves going to the [staging repo](https://github.com/workers-safety-ca/workers-safety-test/settings/pages).

1. Click "Sync fork" to make sure the fork has all the changes from the main repo. Click "Update branch" if there are, otherwise you're golden.
2. Click "Contribute".
3. This brings you to a "Comparing changes" form. If you've got a green "Able to merge" it's ready. Click on option to "Create pull request".
4. Add a title if there is none - a short description of the change. Description can be blank unless you want to add more detail.
5. Click "Create pull request" at the bottom of the form.
6. Once the pull request is created it will show the differences between the staging repo and the main one. You can review it (or have a developer review it if needed).
7. If it all looks good you can select "Squash and merge" option under the green button "Merge pull request". Make it so!
8. Once it's merged it will automatically start rebuilding and publishing the changes.

## Theme

The theme is hugo-universal which is linked via a git submodule. It is currently not customized, but in order to do so the whole theme should be copied into a separate directory, renamed and update `config.toml` to point to the customized theme.

## Build site locally

The [Quick Start](https://gohugo.io/getting-started/quick-start/) steps help with this. Install Hugo. Clone the repo (use test if you want to deploy to staging first).
Run `git submodule init` and then `git submodule update` to fetch the theme linked via git submodule.

Run `hugo server`. It should provide a link for viewing. Any changes will be reflected automatically on the local build.
