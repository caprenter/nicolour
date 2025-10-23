# Nicolour Website

## About
This is a static site that displays at https://nicolour.me.uk/

## Deployment
It is deployed via the docs directory of the main branch of this repo using Github Pages.

### Cron update
We rebuild the site once a day using the GitHub API and [gh-cli](https://cli.github.com/) tool, using a cron job on another server (David's). 

Use the script under 

    /scripts/update_jekyll_sites.sh.example

to set up a cron job. The job is logged in a jekyll_update.log file locally.

This requires a GitHub authentication token which expires every now and again. If you need to replace that token you do it on the server that is running the cron job in the above file.

## Local Development

If you set up your local development environment with Docker, then you also have access to a suite of Behat tests for testing both the live and your local development site.

Alternatively you can just work on the site as you would with a general Jekyll project

Clone the repository

	cd nicolour

### With Docker

    docker-compose up
    # NB running it without the -d flag allows to watch jekyll rebuild and see any errors as you work
    # The site will be up on 0.0.0.0:4000

#### Bring down the testing stack 

      docker-compose down

### Without Docker
	
    cd docs/
    # First run only
    bundle install 
    # Bring the site up
    bundle exec jekyll serve
    # The site should be up on 127.0.0.0:4000


# General Site Building

## Images

### Banner/Splash images

Main banner images are 16:9 aspect ratio .jpg files (if you need dimensions try 1280x800px)

Handy resize code

     find . -name '*.jpg' -size +100k  -print0 | while read -d $'\0' file ; do smartresize "$file" 1280 . ; done


### Gallery

Gallery Images should be no wider than 1080px

Rename them all 'Nicolour1_' e.g Nicoulour1_billybilly5p

Thumbnails should be 400px square - see below.

Place images in '/assets/images/gallery'

File names of the images are used to generate captions etc.

Underscores in filenames will be replaced by spaces in captions, titles and alt text. 

Run this script in that directory to generate Thumbnails
    
    find . \( -name '*.jpg' -or -name '*.JPG' \) -print0 |  while read -d $'\0' file ; do convert -define jpeg:size=400x400  "$file" -thumbnail 300x300^ -gravity center -extent 300x300  ../thumbnails/"$file" ; done

#### How the gallery works
The gallery is made with [Lightbox for Bootstrap](https://ashleydw.github.io/lightbox/)

There is jekyll config in `config.yml`.

These scripts need to be on the page:

    ## In the header
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">

    ## Before the </body> tag
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
    <!-- Lightbox -->
    <script src="https://cdn.jsdelivr.net/npm/bs5-lightbox@1.8.3/dist/index.bundle.min.js"></script>


### Band Images

Band images are 4:3 aspect ratio.

## Previous events listings
These are generated from public google spreadsheets:
https://docs.google.com/spreadsheets/d/1-Eugy7Wfl0O2dSach2D2dOoE8JEW2tI3sqChuCvLUYg/edit

Fetch the data with the script:

    #Fetch the data from those sheets.
    cd scripts
    ./fetch_events_data.sh 
    
    #Fetch and commit changes
    ./fetch_events_data.sh update
    
    #Fetch and commit and push changes to origin main
    ./fetch_events_data.sh update push

# Testing

If you have set up your development environment with Docker then you can run the tests against your local site or the live site using Behat.

We have created a network for the 3 containers (behat, selenium, jekyll), and assigned IP Addresses to each so that the local testing can find the Jekyll site.

The `behat.yml` file contains configuration for the live URL, the local network,and other stuff.

##  Run the tests 

By default the tests will run against a site live on the web as configured in `behat.yml`.

To run against a local development site use the `profile` flag:
 
    --profile=local 

### Optional: Set up a bash alias

Add line to your terminal profile file on your local machine: 
  
     alias behat='docker exec -it behat behat --colors "$@"'

Either reload terminal session or refresh session to make the alias permanent across sessions

### Examples: 
**NB** the examples assume you have set up an alias (see above)
    
    # Get version information
    behat --version 

    # Run all available tests against a LIVE site
    behat 

    # Run all available tests against a local development site
    behat --profile=local 


#### Partial tests

    # Run all tests tagged 'subsection'
    behat --tags @subsection  

    # Run all tests tagged 'javascript' with a javascript enabled browser against a LIVE site.
    behat --tags @javascript  

    # Run all tests tagged 'javascript' with a javascript enabled browser against a LOCAL site.
    behat --profile=local --tags @javascript


## Watch the tests 

You can launch a vnc browser instance in Chrome/Chromium to watch Selenium tests at

     http://localhost:7900 - the password is "secret"

## Writing and contributing tests

Everything is in the `testing` directory. See the Behat docs for more help.


# Contributing
Please fork the repo,and make pull requests from your clone to this one.

## Branches
- `main` holds the most recently deployed code
- `(number)-(name)` branches are working branches where (number) is an issue number and (name) is made up, but has some relation to the issue

## Workflow
* Pick (or create an issue)
* Create a branch (from main if practical) - name the branch (issue number)-(suitable name) e.g. 23-fix-the-footer
* Work on the branch.
* Push to your own fork
* Make a pull request in this repo.