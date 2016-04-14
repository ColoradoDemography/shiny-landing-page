# Shiny Landing Page

This repo contains the html and assets to generate a landing page for shiny that replaces the default shiny server page.  This should help provide more information and options if someone finds the root URL.

## How to Use

### Set-up

To start you'll need to open up a bash into your container with the follwoing command:

```
docker exec -it shiny-server bash

```

Then you'll need to change the directory to where the shiny-server looks for it's page and clone the page into that dir.  THe code below will do this.

``` 
cd /srv/shiny-server/

git clone https://github.com/ColoradoDemography/shiny-landing-page/
```

So far we have the files in the container, but we don't have them were SHiny looks for them.  We need to move them into that main directory.

To copy the index.html file and overwrite the default shiny file run this:

```
cp /srv/shiny-server/shiny-landing-page/index.html /srv/shiny-server/
```

You're almost there, but the html file needs to be able to find its links.  So we need to move over the 'assets' folder from the github repo.

Note:  you'll notice that we had to ass a `-R` to the `cp` command.  This tells Linux to run through all the files and folders in the directory and copy them all.

```
cp -R /srv/shiny-server/shiny-landing-page/assets/ /srv/shiny-server/

```

### Updating the file

So we have a system that uses git, but indirectly to update the site.  If we want to update it we need a different approach.

To start you need to change the directory to the repo and use git to update the original repo by calling:

```
cd /srv/shiny-server/shiny-landing-page/

git pull
```

After this, use whichever `cp` call you need to use to update.  If you changed both, then run both commands, otherwise just run the one for the file(s) you changed.
