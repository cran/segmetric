
<!-- README.md is generated from README.Rmd. Please edit that file -->

# segmetric <img src="inst/extdata/img/logo.png" align="right" width="120"/>

Segmentation Assessment Metrics (`segmetric`)

<!-- badges: start -->

[![Software
License](https://img.shields.io/badge/license-MIT-green)](https://github.com/brazil-data-cube/rstac/blob/master/LICENSE)
[![Software Life
Cycle](https://img.shields.io/badge/lifecycle-stable-brightgreen.svg)](https://lifecycle.r-lib.org/articles/stages.html)
<!-- badges: end -->

The `segmetric` is an open source package that provides a set of metrics
for analysis and evaluation of geospatial segmentation. It includes more
than 20 metrics used in literature for spatial segmentation assessment
(Van Rijsbergen, 1979; Levine and Nazif, 1982; Janssen and Molenaar,
1995; Lucieer and Stein, 2002; Carleer et al., 2005; Moller et al.,
2007; van Coillie et al., 2008; Costa et al., 2008; Weidner, 2008;
Feitosa et al., 2010; Clinton et al. 2010; Persello and Bruzzone, 2010;
Yang et al., 2014; and Zhang et al., 2015).

## Installation

``` r
# install via CRAN 
install.packages("segmetric")
```

### Development version

To install the development version of `segmetric`, run the following
commands

``` r
# load necessary libraries
library(devtools)

install_github("michellepicoli/segmetric")
```

## Usage

Spatial datasets can be loaded using `sf` objects. To create a
`segmetric` object, use function `sm_read()`:

``` r
library(segmetric)

# load example datasets
data("sample_ref_sf", package = "segmetric")
data("sample_seg_sf", package = "segmetric")

# create segmetric object
m <- sm_read(ref_sf = sample_ref_sf, seg_sf = sample_seg_sf)
```

Plot your data using `plot()` command:

``` r
plot(m)
```

<img src="inst/extdata/img/plot-1.png" width="50%" />

Segmentation metrics can be computed by function `sm_compute()`. Use
`summary()` to obtain an overall metric (mean or weighted mean).

``` r
# compute AFI metric and summarize it
sm_compute(m, "AFI") %>% summary()
#> [1] -0.007097452
```

Make multiple calls to compute more other metrics:

``` r
# compute OS1, F_measure, and US2 metrics
m <- 
  sm_compute(m, "OS1") %>%
  sm_compute("F_measure") %>%
  sm_compute("US2")

# summarize them
summary(m)
#>        OS1  F_measure        US2 
#> 0.17341468 0.84728616 0.08617454
```

To see all supported metrics, type `?metric_functions` or run:

``` r
# list all supported metrics
sm_list_metrics()
#>  [1] "AFI"       "D_index"   "E"         "ED3"       "F_measure" "Fitness"  
#>  [7] "M"         "OMerging"  "OS1"       "OS2"       "OS3"       "PI"       
#> [13] "precision" "QR"        "RAsub"     "RAsuper"   "recall"    "UMerging" 
#> [19] "US1"       "US2"       "US3"
```

## Getting Help

A detailed documentation with examples on how to use each function
inside `segmetric` package can be obtained by typing `?segmetric` in R
console.

## How to contribute?

The `segmetric` package was implemented based on an extensible
architecture. Feel free to contribute by implementing new metrics
functions.

1.  Make a project
    [fork](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo).
2.  Edit file `R/metric-funs.R` implementing the new metric.
3.  Register your metric in `.db_registry()` function at `R/db.R` file
    using `sm_reg_metric()`.
4.  Make a [Pull
    Request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request)
    on the branch
    [dev](https://github.com/michellepicoli/segmetric/tree/dev).

## Acknowledgements

This research was supported by the European Research Council (ERC) under
the European Union’s Horizon 2020 research and innovation program (Grant
agreement No 677140 MIDLAND).

## References

-   Carleer, A.P., Debeir, O., Wolff, E., 2005. Assessment of very high
    spatial resolution satellite image segmentations. Photogramm. Eng.
    Remote. Sens. 71, 1285-1294.
    <http://dx.doi.org/10.14358/PERS.71.11.1285>.
-   Clinton, N., Holt, A., Scarborough, J., Yan, L., Gong, P., 2010.
    Accuracy assessment measures for object-based image segmentation
    goodness. Photogramm. Eng. Remote. Sens. 76, pp. 289-299.
-   Costa, G.A.O.P., Feitosa, R.Q., Cazes, T.B., Feijo, B., 2008.
    Genetic adaptation of segmentation parameters. In: Blaschke, T.,
    Lang, S., Hay, G.J. (Eds.), Object-based Image Analysis. Springer
    Berlin Heidelberg, Berlin, Heidelberg, pp. 679-695.
    <http://dx.doi.org/10.1007/978-3-540-77058-9_37>.
-   Feitosa, R.Q., Ferreira, R.S., Almeida, C.M., Camargo, F.F., Costa,
    G.A.O.P., 2010. Similarity metrics for genetic adaptation of
    segmentation parameters. In: 3rd International Conference on
    Geographic Object-Based Image Analysis (GEOBIA 2010). The
    International Archives of the Photogrammetry, Remote Sensing and
    Spatial Information Sciences, Ghent.
-   Janssen, L.L.F., Molenaar, M., 1995. Terrain objects, their dynamics
    and their monitoring by the integration of GIS and remote sensing.
    IEEE Trans. Geosci. Remote Sens. 33, pp. 749-758.
    <http://dx.doi.org/10.1109/36.387590>.
-   Levine, M.D., Nazif, A.M., 1982. An experimental rule based system
    for testing low level segmentation strategies. In: Preston, K.,
    Uhr, L. (Eds.), Multicomputers and Image Processing: Algorithms and
    Programs. Academic Press, New York, pp. 149-160.
-   Lucieer, A., Stein, A., 2002. Existential uncertainty of spatial
    objects segmented from satellite sensor imagery. Geosci. Remote.
    Sens. IEEE Trans. 40, pp. 2518-2521.
    <http://dx.doi.org/10.1109/TGRS.2002.805072>.
-   Moller, M., Lymburner, L., Volk, M., 2007. The comparison index: a
    tool for assessing the accuracy of image segmentation. Int. J. Appl.
    Earth Obs. Geoinf. 9, pp. 311-321.
    <http://dx.doi.org/10.1016/j.jag.2006.10.002>.
-   Persello, C., Bruzzone, L., 2010. A novel protocol for accuracy
    assessment in classification of very high resolution images. IEEE
    Trans. Geosci. Remote Sens. 48, pp. 1232-1244.
    <http://dx.doi.org/10.1109/TGRS.2009.2029570>.
-   Van Coillie, F.M.B., Verbeke, L.P.C., De Wulf, R.R., 2008.
    Semi-automated forest stand delineation using wavelet based
    segmentation of very high resolution optical imagery. In:
    Object-Based Image Analysis: Spatial Concepts for Knowledge-Driven
    Remote Sensing Applications, pp. 237-256.
    <http://dx.doi.org/10.1007/978-3-540-77058-9_13>.
-   Van Rijsbergen, C.J., 1979. Information Retrieval.
    Butterworth-Heinemann, London.
-   Weidner, U., 2008. Contribution to the assessment of segmentation
    quality for remote sensing applications. Int. Arch. Photogramm.
    Remote Sens. Spat. Inf. Sci. 37, pp. 479-484.
-   Yang Yang, J., Li, P., He, Y., 2014. A multi-band approach to
    unsupervised scale parameter selection for multi-scale image
    segmentation. ISPRS J. Photogramm. Remote Sens. 94, pp. 13-24.
    <http://dx.doi.org/10.1016/j.isprsjprs.2014.04.008>.
-   Zhang, X., Feng, X., Xiao, P., He, G., Zhu, L., 2015a. Segmentation
    quality evaluation using region-based precision and recall measures
    for remote sensing images. ISPRS J. Photogramm. Remote Sens. 102,
    pp. 73-84. <http://dx.doi.org/10.1016/j.isprsjprs.2015.01.009>.
