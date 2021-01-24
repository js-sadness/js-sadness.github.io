# JS Sadness

This is [js-sadness.com](https://js-sadness.com/), inspired by [phpsadness.com](http://phpsadness.com/).

## Status
This project was started only a few days ago, it is still work in progress. 
It's going to take a few weeks until this is ready for real content.

## Contributing
As this project is was created only a few days ago, 
we currently want to limit contributions to the three founding members.
We hope that plenty of sadnesses will be contributed 
once the basic structure of the website has shaped.

## Pushing changes
This repository uses [`jekyll`](https://jekyllrb.com/) which comes with github pages.
Before merging to master, build the site locally and test it:

### Setup
With ruby and jekyll installed, run `bundle install` 
inside this project directory in order to install all dependencies. 

### Running
With jekyll installed, run `bundle exec jekyll serve` inside this project directory, 
and then visit [localhost on port 4000](http://localhost:4000/).  

All pull requests will additionally be checked automatically.

## Project Structure

### _sadnesses
This folder contains all sadnesses. Add a file to this folder
in order to contribute sadness.

Each sadness should contain the following points, if feasible:
1. The Facts
1. Why is this a Problem
1. Our Suggestion to improving the language
1. Workarounds that work today
1. Further Reading

### _layouts
This folder contains the html files 
which are reused across the pages of this website.

### _categories
This folder contains all categories. 
They should be referenced from individual sadnesses.
For each category, an overview page is generated.

