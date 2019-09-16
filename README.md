<a alt = "TravisCI Build Status" href="https://travis-ci.org/rstudio-education/stat545"><img src="https://travis-ci.org/rstudio-education/stat545.svg?branch=master" height = 20 /></a>
<a alt = "Netlify Deployments" href="https://app.netlify.com/sites/stat545-book/deploys"><img src="https://api.netlify.com/api/v1/badges/22cbd49d-9d4d-462f-9d28-a797fa14a11d/deploy-status" height = 20 /></a>
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" height = 20 /></a>
<a alt = "Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public." href="http://www.repostatus.org/#wip"><img src="http://www.repostatus.org/badges/latest/wip.svg" height = 20 /></a>

This bookdown book is a *work in progress*. We'll update this `README` and the repo status when ready! :rocket:

# Requirements to preview the site locally 

Install the required packages.
    
## Option 1: Use pak 

Here's one way to install the needed packages (only the ones that you don't already have) using the [pak package](https://pak.r-lib.org/index.html).

<!--TODO: Change pkg_list to not be static, maybe use renv::dependencies(path = "DESCRIPTION")?-->

```r
pkg_list <- c("bookdown", "devtools", "dichromat", "DT", "fs", "gapminder",
              "gender", "geonames", "git2r", "glue", "gridExtra",  "htmltools",
              "httr", "knitr", "RColorBrewer", "rebird", "rmarkdown", "rplos", 
              "rvest", "testthat", "tidyverse", "usethis", "viridis", "xfun", 
              "xml2", "ropensci/genderdata", "rstudio/gt", "rstudio/renv")

# install.packages("pak")
pak::pkg_install(pkg_list)
```

## Option 2: Use renv for a project-specific library

Another option is to use the [renv package](https://rstudio.github.io/renv/index.html) to replicate our exact project library. renv is a package that uses a [snapshot and restore](https://environments.rstudio.com/snapshot.html) strategy to create **r**eproducible **env**nvironments for R projects. renv will create a private, project-specific library that is separate from your personal library of packages. This would be a good option if, for example, you have another project that relies on a specific version of a package and you don't want to mess with it by upgrading, downgrading, etc.

If you want to learn more about what renv is doing behind the scenes checkout [renv's main site](https://rstudio.github.io/renv/index.html).

*Note: The renv package is still in under active development, so please open an issue here if these instructions seem out of date.*

Once you have a local copy of this project (either via [fork and clone](https://happygitwithr.com/fork-and-clone.html) or by downloading this repository as a ZIP file), follow these steps:

1. Install the renv package (not on CRAN yet).
   
    ```r
    # install.packages("devtools")
    devtools::install_github("rstudio/renv")
    ```
    
1. Run `renv::init(bare = TRUE)` in the Console.
    + This will create a private, project-specific library. The `bare = TRUE` argument tells renv that it should *not* try to add anything to this new library yet. If you take a took at the Packages tab in RStudio there will be two headers: "Packrat Library" and "System Library". The only package listed under "Packrat Library" (i.e. the private, project-specific library) will be renv.
1. Run `renv::restore()` in the Console.
    + This will print out "The following package(s) will be installed" followed by a long list of packages. Respond yes. renv will install the packages by copying them over from the cache in the `renv/` folder.
1. Restart R (*Session* > *Restart R*)
    + If you take a look at the Packages tab, there should be a lot more packages listed under "Packrat Library" now.
1. You should now be able to render the bookdown locally via either `bookdown::serve_book()` or *Addins* > *Preview Book*.

## OMDb API key

One file, 37_diy-web-data.Rmd, accesses the Open Movie Database API, which requires a key. The site will render without this, without rendering this file. Set up an OMDb key to render this file.

1. Request an API key [here](https://www.omdbapi.com/apikey.aspx).
1. Check your email and follow the instructions to activate your key
1. Add the API key to your `.Renviron` file. First, open your .`Renviron` file with the usethis package:
  
    ```r
    library(usethis)
    edit_r_environ()
    ```
    
    Next, add `OMDB_API_KEY=<your-key>` on a new line, replacing `<your-key>` with your OMDb key. (Make sure to have your `.Renviron` file end on a new line!)