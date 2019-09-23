# Quantifying and understanding reproductive allocation schedules in plants

Contact: [Daniel Falster](http://danielfalster.com/)

This repository contains all the code used to produce figures in the manuscript:

Wenk EH, Falster DS (2015) **Quantifying and understanding reproductive allocation schedules in plants**. *Ecology and Evolution* 5: 5521-5538. [10.1002/ece3.1802](http://doi.org/10.1002/ece3.1802)

## Running the code

All analyses were done in `R`. All code needed to reproduce the results is included in this repository in the `analysis.R` file. Figures will be output to a directory called `output`.

If reproducing these results on your own machine, you much first install the package [smatr](cran.r-project.org/package=smatr), described in [Warton et al 2013](http://doi.org/10.1111/j.2041-210X.2011.00153.x) and `deSolve`:
  
```
install.packages(c('smatr', 'deSolve'))
```

You can access an interactive RStudio session with the required software pre-installed by opening a container hosted by [Binder](http://mybinder.org): 

[![Launch Rstudio Binder](http://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/dfalster/Wenk_RA_review/master?urlpath=rstudio)

To ensure long-term [computational reproducibility](https://www.britishecologicalsociety.org/wp-content/uploads/2017/12/guide-to-reproducible-code.pdf) of this work, we have created a [Docker](http://dockerhub.com) image to enable others to reproduce these results on their local machines using the same software and versions we used to conduct the original analysis. Instructions for reproducing this work using the docker image are available at the bottom of the page. 

## Material included in the repository include:

- `data/`: Raw data
- `R/`: directory containing functions used in analysis
- `DESCRIPTION`: A machine-readable [compendium]() file containing key metadata and dependencies 
- `LICENSE.md`: License for the materials
- `Dockerfile` & `.binder/Dockerfile`: files used to generate docker containers for long-term reproducibility

## License

### Data

The data included in the data directory was made available by Martin Henery. With Martin's permission, it is being made available here under the [CC0 license](https://creativecommons.org/choose/zero/). If you use the data, we encourage you would to cite the original publication from where it was collected:

Henery, M. & Westoby, M. (2001) Seed mass and seed nutrient content as predictors of seed output variation between species. *Oikos* **92**: 479–490. doi: [10.1034/j.1600-0706.2001.920309.x](http://doi.org/10.1034/j.1600-0706.2001.920309.x)

### Code

All code (all R files, script files but not data) is under the [MIT licence](http://opensource.org/licenses/MIT):

> Copyright (c) 2014 Daniel S. Falster

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Running via Docker

If you have Docker installed, you can recreate the computing environment as follows. 

First clone this repository:

```
git clone https://github.com/dfalster/Wenk_RA_review.git
```

Then fetch the container:

```
docker pull traitecoevo/wenk_ra_review
```

From within your downloaded repo, launch the container using the following code (it will map your current working directory inside the docker container): 

```
docker run --user root -v $(pwd):/home/rstudio/ -p 8787:8787 -e DISABLE_AUTH=true traitecoevo/wenk_ra_review
```

The code above initialises a docker container, which runs an rstudio session, which is accessed by pointing your browser to [localhost:8787](http://localhost:8787). For more instructions on running docker, see the info from [rocker](https://hub.docker.com/r/rocker/rstudio).

### NOTE: Building the docker image

For posterity, the docker image was built off [`rocker/verse:3.6.1` container](https://hub.docker.com/r/rocker/verse) via the following command, in a terminal contained within the downloaded repo:

```
docker build -t traitecoevo/wenk_ra_review .
```

and was then pushed to [dockerhub](https://cloud.docker.com/u/traitecoevo/repository/docker/traitecoevo/wenk_ra_review). The image used by binder builds off this container, adding extra features needed by binder, as described in [rocker/binder](https://hub.docker.com/r/rocker/binder/dockerfile).
