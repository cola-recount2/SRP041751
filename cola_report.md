cola Report for recount2:SRP041751
==================

**Date**: 2019-12-26 00:12:13 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 16571    54
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[SD:kmeans](#SD-kmeans)     |          2| 1.000|           0.995|       0.998|** |           |
|[SD:pam](#SD-pam)           |          6| 1.000|           0.974|       0.989|** |3,5        |
|[MAD:kmeans](#MAD-kmeans)   |          2| 1.000|           0.983|       0.990|** |           |
|[MAD:skmeans](#MAD-skmeans) |          2| 1.000|           0.967|       0.986|** |           |
|[ATC:hclust](#ATC-hclust)   |          2| 1.000|           0.961|       0.983|** |           |
|[ATC:kmeans](#ATC-kmeans)   |          2| 1.000|           0.975|       0.989|** |           |
|[ATC:NMF](#ATC-NMF)         |          2| 1.000|           0.982|       0.992|** |           |
|[SD:NMF](#SD-NMF)           |          2| 0.999|           0.962|       0.984|** |           |
|[MAD:pam](#MAD-pam)         |          6| 0.970|           0.896|       0.961|** |           |
|[ATC:skmeans](#ATC-skmeans) |          4| 0.929|           0.903|       0.959|*  |2,3        |
|[SD:skmeans](#SD-skmeans)   |          2| 0.923|           0.937|       0.973|*  |           |
|[ATC:pam](#ATC-pam)         |          6| 0.908|           0.829|       0.937|*  |3,4        |
|[CV:pam](#CV-pam)           |          6| 0.905|           0.913|       0.958|*  |2,3,5      |
|[MAD:hclust](#MAD-hclust)   |          2| 0.902|           0.958|       0.975|*  |           |
|[MAD:NMF](#MAD-NMF)         |          2| 0.885|           0.932|       0.971|   |           |
|[CV:skmeans](#CV-skmeans)   |          3| 0.882|           0.894|       0.954|   |           |
|[CV:NMF](#CV-NMF)           |          3| 0.875|           0.876|       0.950|   |           |
|[SD:mclust](#SD-mclust)     |          2| 0.759|           0.950|       0.965|   |           |
|[ATC:mclust](#ATC-mclust)   |          2| 0.752|           0.916|       0.962|   |           |
|[CV:mclust](#CV-mclust)     |          2| 0.747|           0.858|       0.939|   |           |
|[CV:hclust](#CV-hclust)     |          3| 0.656|           0.773|       0.910|   |           |
|[CV:kmeans](#CV-kmeans)     |          2| 0.549|           0.882|       0.927|   |           |
|[MAD:mclust](#MAD-mclust)   |          3| 0.504|           0.743|       0.862|   |           |
|[SD:hclust](#SD-hclust)     |         NA|    NA|              NA|          NA|   |           |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2 0.999           0.962       0.984          0.485 0.516   0.516
#&gt; CV:NMF      2 0.641           0.847       0.926          0.480 0.508   0.508
#&gt; MAD:NMF     2 0.885           0.932       0.971          0.491 0.508   0.508
#&gt; ATC:NMF     2 1.000           0.982       0.992          0.463 0.535   0.535
#&gt; SD:skmeans  2 0.923           0.937       0.973          0.502 0.502   0.502
#&gt; CV:skmeans  2 0.849           0.881       0.955          0.503 0.497   0.497
#&gt; MAD:skmeans 2 1.000           0.967       0.986          0.509 0.491   0.491
#&gt; ATC:skmeans 2 1.000           0.957       0.984          0.507 0.497   0.497
#&gt; SD:mclust   2 0.759           0.950       0.965          0.450 0.525   0.525
#&gt; CV:mclust   2 0.747           0.858       0.939          0.440 0.575   0.575
#&gt; MAD:mclust  2 0.520           0.814       0.909          0.356 0.693   0.693
#&gt; ATC:mclust  2 0.752           0.916       0.962          0.470 0.535   0.535
#&gt; SD:kmeans   2 1.000           0.995       0.998          0.474 0.525   0.525
#&gt; CV:kmeans   2 0.549           0.882       0.927          0.434 0.535   0.535
#&gt; MAD:kmeans  2 1.000           0.983       0.990          0.478 0.525   0.525
#&gt; ATC:kmeans  2 1.000           0.975       0.989          0.474 0.525   0.525
#&gt; SD:pam      2 0.820           0.892       0.953          0.415 0.609   0.609
#&gt; CV:pam      2 1.000           0.958       0.982          0.352 0.628   0.628
#&gt; MAD:pam     2 0.887           0.939       0.974          0.502 0.497   0.497
#&gt; ATC:pam     2 0.823           0.888       0.957          0.480 0.525   0.525
#&gt; SD:hclust   2 0.454           0.924       0.899          0.346 0.560   0.560
#&gt; CV:hclust   2 0.398           0.743       0.859          0.292 0.669   0.669
#&gt; MAD:hclust  2 0.902           0.958       0.975          0.437 0.560   0.560
#&gt; ATC:hclust  2 1.000           0.961       0.983          0.438 0.575   0.575
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 0.893           0.901       0.960         0.2981 0.790   0.619
#&gt; CV:NMF      3 0.875           0.876       0.950         0.3501 0.735   0.527
#&gt; MAD:NMF     3 0.662           0.684       0.833         0.2903 0.778   0.596
#&gt; ATC:NMF     3 0.638           0.702       0.849         0.1773 0.913   0.844
#&gt; SD:skmeans  3 0.894           0.924       0.965         0.3182 0.718   0.496
#&gt; CV:skmeans  3 0.882           0.894       0.954         0.3124 0.734   0.515
#&gt; MAD:skmeans 3 0.673           0.659       0.827         0.2770 0.837   0.678
#&gt; ATC:skmeans 3 0.976           0.951       0.975         0.2101 0.875   0.752
#&gt; SD:mclust   3 0.430           0.467       0.719         0.3199 0.709   0.490
#&gt; CV:mclust   3 0.346           0.248       0.678         0.3211 0.640   0.476
#&gt; MAD:mclust  3 0.504           0.743       0.862         0.4658 0.756   0.655
#&gt; ATC:mclust  3 0.517           0.712       0.858         0.2427 0.755   0.603
#&gt; SD:kmeans   3 0.626           0.775       0.886         0.2425 0.901   0.814
#&gt; CV:kmeans   3 0.658           0.828       0.905         0.3443 0.855   0.737
#&gt; MAD:kmeans  3 0.517           0.249       0.660         0.3028 0.900   0.817
#&gt; ATC:kmeans  3 0.829           0.889       0.926         0.3837 0.737   0.529
#&gt; SD:pam      3 0.911           0.876       0.936         0.2619 0.844   0.748
#&gt; CV:pam      3 0.968           0.928       0.978         0.3136 0.876   0.804
#&gt; MAD:pam     3 0.719           0.697       0.867         0.2247 0.860   0.732
#&gt; ATC:pam     3 0.929           0.913       0.966         0.4073 0.739   0.530
#&gt; SD:hclust   3 0.832           0.887       0.921         0.4217 0.951   0.913
#&gt; CV:hclust   3 0.656           0.773       0.910         0.5074 0.915   0.874
#&gt; MAD:hclust  3 0.923           0.932       0.980         0.0447 0.989   0.980
#&gt; ATC:hclust  3 0.678           0.831       0.840         0.2002 0.980   0.966
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.737           0.682       0.816         0.1612 0.771   0.472
#&gt; CV:NMF      4 0.632           0.455       0.716         0.1236 0.881   0.682
#&gt; MAD:NMF     4 0.813           0.891       0.934         0.1585 0.783   0.493
#&gt; ATC:NMF     4 0.599           0.790       0.837         0.2642 0.732   0.493
#&gt; SD:skmeans  4 0.853           0.868       0.936         0.1223 0.866   0.627
#&gt; CV:skmeans  4 0.721           0.652       0.851         0.1098 0.881   0.670
#&gt; MAD:skmeans 4 0.824           0.861       0.939         0.1388 0.820   0.544
#&gt; ATC:skmeans 4 0.929           0.903       0.959         0.1219 0.906   0.762
#&gt; SD:mclust   4 0.473           0.706       0.767         0.1476 0.778   0.504
#&gt; CV:mclust   4 0.465           0.533       0.715         0.1654 0.748   0.531
#&gt; MAD:mclust  4 0.471           0.597       0.805         0.2518 0.903   0.805
#&gt; ATC:mclust  4 0.533           0.492       0.739         0.1802 0.813   0.597
#&gt; SD:kmeans   4 0.580           0.716       0.808         0.1788 0.809   0.573
#&gt; CV:kmeans   4 0.619           0.640       0.821         0.1648 0.886   0.743
#&gt; MAD:kmeans  4 0.612           0.657       0.791         0.1507 0.708   0.434
#&gt; ATC:kmeans  4 0.722           0.699       0.822         0.1019 0.960   0.883
#&gt; SD:pam      4 0.831           0.846       0.921         0.1367 0.957   0.910
#&gt; CV:pam      4 0.966           0.927       0.977         0.0714 0.983   0.967
#&gt; MAD:pam     4 0.891           0.784       0.895         0.1724 0.809   0.563
#&gt; ATC:pam     4 0.985           0.921       0.968         0.0842 0.916   0.750
#&gt; SD:hclust   4 0.871           0.899       0.965         0.0397 0.974   0.950
#&gt; CV:hclust   4 0.595           0.654       0.851         0.1852 0.876   0.796
#&gt; MAD:hclust  4 0.812           0.898       0.929         0.1296 0.956   0.920
#&gt; ATC:hclust  4 0.704           0.670       0.846         0.2523 0.754   0.557
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.707           0.701       0.811         0.0531 0.934   0.766
#&gt; CV:NMF      5 0.760           0.725       0.826         0.0718 0.796   0.412
#&gt; MAD:NMF     5 0.835           0.807       0.887         0.0476 0.963   0.864
#&gt; ATC:NMF     5 0.653           0.700       0.841         0.0641 0.993   0.976
#&gt; SD:skmeans  5 0.835           0.832       0.913         0.0627 0.920   0.705
#&gt; CV:skmeans  5 0.733           0.713       0.834         0.0584 0.890   0.625
#&gt; MAD:skmeans 5 0.882           0.846       0.925         0.0659 0.911   0.676
#&gt; ATC:skmeans 5 0.832           0.828       0.860         0.0702 0.916   0.737
#&gt; SD:mclust   5 0.608           0.402       0.667         0.1466 0.845   0.574
#&gt; CV:mclust   5 0.529           0.541       0.689         0.1093 0.646   0.258
#&gt; MAD:mclust  5 0.674           0.674       0.818         0.2036 0.724   0.382
#&gt; ATC:mclust  5 0.539           0.474       0.702         0.0914 0.742   0.380
#&gt; SD:kmeans   5 0.668           0.672       0.788         0.0841 0.932   0.761
#&gt; CV:kmeans   5 0.663           0.572       0.775         0.0763 0.893   0.707
#&gt; MAD:kmeans  5 0.767           0.748       0.837         0.0761 0.867   0.563
#&gt; ATC:kmeans  5 0.724           0.676       0.793         0.0640 0.904   0.703
#&gt; SD:pam      5 1.000           0.948       0.980         0.1743 0.822   0.612
#&gt; CV:pam      5 0.942           0.902       0.969         0.2972 0.845   0.691
#&gt; MAD:pam     5 0.848           0.792       0.916         0.0250 0.785   0.425
#&gt; ATC:pam     5 0.857           0.792       0.919         0.0692 0.915   0.697
#&gt; SD:hclust   5 0.868           0.837       0.938         0.0311 0.994   0.989
#&gt; CV:hclust   5 0.604           0.667       0.874         0.0894 0.904   0.811
#&gt; MAD:hclust  5 0.661           0.771       0.909         0.0968 0.922   0.847
#&gt; ATC:hclust  5 0.663           0.705       0.846         0.0175 0.904   0.730
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.835           0.776       0.892         0.0475 0.908   0.633
#&gt; CV:NMF      6 0.880           0.828       0.916         0.0468 0.952   0.780
#&gt; MAD:NMF     6 0.816           0.733       0.869         0.0396 0.954   0.812
#&gt; ATC:NMF     6 0.647           0.626       0.815         0.0411 0.844   0.549
#&gt; SD:skmeans  6 0.814           0.808       0.888         0.0308 0.962   0.824
#&gt; CV:skmeans  6 0.792           0.741       0.853         0.0376 0.969   0.852
#&gt; MAD:skmeans 6 0.862           0.783       0.890         0.0315 0.945   0.759
#&gt; ATC:skmeans 6 0.817           0.776       0.861         0.0339 0.980   0.923
#&gt; SD:mclust   6 0.712           0.607       0.745         0.0255 0.847   0.454
#&gt; CV:mclust   6 0.627           0.538       0.708         0.0601 0.843   0.416
#&gt; MAD:mclust  6 0.701           0.788       0.831         0.0373 0.913   0.607
#&gt; ATC:mclust  6 0.778           0.806       0.837         0.0753 0.840   0.475
#&gt; SD:kmeans   6 0.789           0.634       0.810         0.0512 0.959   0.835
#&gt; CV:kmeans   6 0.707           0.508       0.767         0.0567 0.920   0.732
#&gt; MAD:kmeans  6 0.809           0.687       0.806         0.0443 0.957   0.801
#&gt; ATC:kmeans  6 0.738           0.683       0.783         0.0524 0.891   0.574
#&gt; SD:pam      6 1.000           0.974       0.989         0.0487 0.957   0.859
#&gt; CV:pam      6 0.905           0.913       0.958         0.0688 0.957   0.877
#&gt; MAD:pam     6 0.970           0.896       0.961         0.0716 0.888   0.608
#&gt; ATC:pam     6 0.908           0.829       0.937         0.0202 0.963   0.831
#&gt; SD:hclust   6 0.811           0.842       0.933         0.0486 0.990   0.979
#&gt; CV:hclust   6 0.685           0.668       0.845         0.0525 0.933   0.860
#&gt; MAD:hclust  6 0.721           0.819       0.915         0.1253 0.949   0.883
#&gt; ATC:hclust  6 0.693           0.568       0.825         0.0614 0.881   0.652
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   There is no best k.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.454           0.924       0.899         0.3464 0.560   0.560
#> 3 3 0.832           0.887       0.921         0.4217 0.951   0.913
#> 4 4 0.871           0.899       0.965         0.0397 0.974   0.950
#> 5 5 0.868           0.837       0.938         0.0311 0.994   0.989
#> 6 6 0.811           0.842       0.933         0.0486 0.990   0.979
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] NA
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.965 0.000 1.000
#&gt; SRR1274529     2   0.000      0.965 0.000 1.000
#&gt; SRR1274530     2   0.000      0.965 0.000 1.000
#&gt; SRR1274531     2   0.327      0.909 0.060 0.940
#&gt; SRR1274532     2   0.000      0.965 0.000 1.000
#&gt; SRR1274533     2   0.000      0.965 0.000 1.000
#&gt; SRR1274534     2   0.000      0.965 0.000 1.000
#&gt; SRR1274535     2   0.000      0.965 0.000 1.000
#&gt; SRR1274536     2   0.402      0.883 0.080 0.920
#&gt; SRR1274537     2   0.000      0.965 0.000 1.000
#&gt; SRR1274538     2   0.000      0.965 0.000 1.000
#&gt; SRR1274539     2   0.000      0.965 0.000 1.000
#&gt; SRR1274540     2   0.000      0.965 0.000 1.000
#&gt; SRR1274541     2   0.000      0.965 0.000 1.000
#&gt; SRR1274542     2   0.000      0.965 0.000 1.000
#&gt; SRR1274543     2   0.000      0.965 0.000 1.000
#&gt; SRR1274544     2   0.000      0.965 0.000 1.000
#&gt; SRR1274545     2   0.000      0.965 0.000 1.000
#&gt; SRR1274546     2   0.000      0.965 0.000 1.000
#&gt; SRR1274547     2   0.000      0.965 0.000 1.000
#&gt; SRR1274548     2   0.000      0.965 0.000 1.000
#&gt; SRR1274549     2   0.855      0.457 0.280 0.720
#&gt; SRR1274550     1   0.833      0.926 0.736 0.264
#&gt; SRR1274551     2   0.000      0.965 0.000 1.000
#&gt; SRR1274552     1   0.833      0.926 0.736 0.264
#&gt; SRR1274553     1   0.833      0.926 0.736 0.264
#&gt; SRR1274554     2   0.000      0.965 0.000 1.000
#&gt; SRR1274555     1   0.833      0.926 0.736 0.264
#&gt; SRR1274556     1   0.833      0.926 0.736 0.264
#&gt; SRR1274557     1   0.833      0.926 0.736 0.264
#&gt; SRR1274558     2   0.506      0.834 0.112 0.888
#&gt; SRR1274559     2   0.506      0.834 0.112 0.888
#&gt; SRR1274560     2   0.506      0.834 0.112 0.888
#&gt; SRR1274561     1   0.881      0.907 0.700 0.300
#&gt; SRR1274562     1   0.814      0.928 0.748 0.252
#&gt; SRR1274563     1   0.833      0.926 0.736 0.264
#&gt; SRR1274564     2   0.402      0.883 0.080 0.920
#&gt; SRR1274565     2   0.000      0.965 0.000 1.000
#&gt; SRR1274566     2   0.141      0.949 0.020 0.980
#&gt; SRR1274567     2   0.141      0.949 0.020 0.980
#&gt; SRR1274568     2   0.278      0.921 0.048 0.952
#&gt; SRR1274569     1   0.833      0.927 0.736 0.264
#&gt; SRR1274570     1   0.833      0.927 0.736 0.264
#&gt; SRR1274571     1   0.833      0.927 0.736 0.264
#&gt; SRR1274572     1   0.833      0.927 0.736 0.264
#&gt; SRR1274573     2   0.000      0.965 0.000 1.000
#&gt; SRR1274574     2   0.000      0.965 0.000 1.000
#&gt; SRR1274575     2   0.000      0.965 0.000 1.000
#&gt; SRR1274576     2   0.000      0.965 0.000 1.000
#&gt; SRR1274577     2   0.000      0.965 0.000 1.000
#&gt; SRR1274578     1   0.833      0.927 0.736 0.264
#&gt; SRR1274579     1   0.833      0.927 0.736 0.264
#&gt; SRR1274580     1   0.833      0.927 0.736 0.264
#&gt; SRR1274581     1   0.833      0.601 0.736 0.264
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274530     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274531     2  0.2947     0.9069 0.020 0.920 0.060
#&gt; SRR1274532     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274533     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274534     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274535     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274536     2  0.2537     0.9115 0.000 0.920 0.080
#&gt; SRR1274537     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274539     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274540     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274546     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274549     2  0.7798     0.4398 0.080 0.624 0.296
#&gt; SRR1274550     3  0.5397     1.0000 0.280 0.000 0.720
#&gt; SRR1274551     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274552     3  0.5397     1.0000 0.280 0.000 0.720
#&gt; SRR1274553     3  0.5397     1.0000 0.280 0.000 0.720
#&gt; SRR1274554     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274555     3  0.5397     1.0000 0.280 0.000 0.720
#&gt; SRR1274556     3  0.5397     1.0000 0.280 0.000 0.720
#&gt; SRR1274557     3  0.5397     1.0000 0.280 0.000 0.720
#&gt; SRR1274558     2  0.3192     0.8756 0.112 0.888 0.000
#&gt; SRR1274559     2  0.3192     0.8756 0.112 0.888 0.000
#&gt; SRR1274560     2  0.3192     0.8756 0.112 0.888 0.000
#&gt; SRR1274561     1  0.8013     0.0478 0.588 0.080 0.332
#&gt; SRR1274562     1  0.5905     0.0354 0.648 0.000 0.352
#&gt; SRR1274563     3  0.5397     1.0000 0.280 0.000 0.720
#&gt; SRR1274564     2  0.2537     0.9115 0.000 0.920 0.080
#&gt; SRR1274565     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274566     2  0.0892     0.9587 0.000 0.980 0.020
#&gt; SRR1274567     2  0.0892     0.9587 0.000 0.980 0.020
#&gt; SRR1274568     2  0.1753     0.9364 0.048 0.952 0.000
#&gt; SRR1274569     1  0.0000     0.8038 1.000 0.000 0.000
#&gt; SRR1274570     1  0.0000     0.8038 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000     0.8038 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0000     0.8038 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274576     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274577     2  0.0000     0.9703 0.000 1.000 0.000
#&gt; SRR1274578     1  0.0000     0.8038 1.000 0.000 0.000
#&gt; SRR1274579     1  0.0000     0.8038 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000     0.8038 1.000 0.000 0.000
#&gt; SRR1274581     1  0.9050     0.3671 0.536 0.168 0.296
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1274528     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274529     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274530     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274531     2  0.2011      0.902 0.000 0.920 0.080  0
#&gt; SRR1274532     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274533     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274534     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274535     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274536     2  0.2011      0.907 0.000 0.920 0.080  0
#&gt; SRR1274537     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274538     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274539     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274540     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274541     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274542     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274543     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274544     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274545     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274546     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274547     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274548     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274549     2  0.4776      0.430 0.000 0.624 0.376  0
#&gt; SRR1274550     3  0.0000      0.860 0.000 0.000 1.000  0
#&gt; SRR1274551     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274552     3  0.0000      0.860 0.000 0.000 1.000  0
#&gt; SRR1274553     3  0.0000      0.860 0.000 0.000 1.000  0
#&gt; SRR1274554     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274555     3  0.0000      0.860 0.000 0.000 1.000  0
#&gt; SRR1274556     3  0.0000      0.860 0.000 0.000 1.000  0
#&gt; SRR1274557     3  0.0000      0.860 0.000 0.000 1.000  0
#&gt; SRR1274558     2  0.2530      0.871 0.112 0.888 0.000  0
#&gt; SRR1274559     2  0.2530      0.871 0.112 0.888 0.000  0
#&gt; SRR1274560     2  0.2530      0.871 0.112 0.888 0.000  0
#&gt; SRR1274561     3  0.6453      0.364 0.360 0.080 0.560  0
#&gt; SRR1274562     3  0.4855      0.382 0.400 0.000 0.600  0
#&gt; SRR1274563     3  0.0000      0.860 0.000 0.000 1.000  0
#&gt; SRR1274564     2  0.2011      0.907 0.000 0.920 0.080  0
#&gt; SRR1274565     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274566     2  0.0707      0.957 0.000 0.980 0.020  0
#&gt; SRR1274567     2  0.0707      0.957 0.000 0.980 0.020  0
#&gt; SRR1274568     2  0.1389      0.934 0.048 0.952 0.000  0
#&gt; SRR1274569     1  0.0000      1.000 1.000 0.000 0.000  0
#&gt; SRR1274570     1  0.0000      1.000 1.000 0.000 0.000  0
#&gt; SRR1274571     1  0.0000      1.000 1.000 0.000 0.000  0
#&gt; SRR1274572     1  0.0000      1.000 1.000 0.000 0.000  0
#&gt; SRR1274573     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274574     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274575     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274576     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274577     2  0.0000      0.969 0.000 1.000 0.000  0
#&gt; SRR1274578     1  0.0000      1.000 1.000 0.000 0.000  0
#&gt; SRR1274579     1  0.0000      1.000 1.000 0.000 0.000  0
#&gt; SRR1274580     1  0.0000      1.000 1.000 0.000 0.000  0
#&gt; SRR1274581     4  0.0000      0.000 0.000 0.000 0.000  1
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274530     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274531     2  0.1831      0.905 0.000 0.920 0.000 0.004 0.076
#&gt; SRR1274532     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274534     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274535     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274536     2  0.2074      0.909 0.000 0.920 0.000 0.044 0.036
#&gt; SRR1274537     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274540     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     2  0.6343      0.441 0.000 0.624 0.200 0.044 0.132
#&gt; SRR1274550     3  0.4959      0.561 0.000 0.000 0.684 0.240 0.076
#&gt; SRR1274551     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.4959      0.561 0.000 0.000 0.684 0.240 0.076
#&gt; SRR1274553     3  0.4959      0.561 0.000 0.000 0.684 0.240 0.076
#&gt; SRR1274554     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274555     3  0.0000      0.536 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     5  0.4171      0.000 0.000 0.000 0.396 0.000 0.604
#&gt; SRR1274557     3  0.0000      0.536 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274558     2  0.3454      0.801 0.028 0.816 0.000 0.156 0.000
#&gt; SRR1274559     2  0.3454      0.801 0.028 0.816 0.000 0.156 0.000
#&gt; SRR1274560     2  0.3454      0.801 0.028 0.816 0.000 0.156 0.000
#&gt; SRR1274561     3  0.5558      0.330 0.360 0.080 0.560 0.000 0.000
#&gt; SRR1274562     3  0.4182      0.362 0.400 0.000 0.600 0.000 0.000
#&gt; SRR1274563     3  0.0000      0.536 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274564     2  0.2074      0.909 0.000 0.920 0.000 0.044 0.036
#&gt; SRR1274565     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274566     2  0.0693      0.954 0.000 0.980 0.000 0.012 0.008
#&gt; SRR1274567     2  0.0693      0.954 0.000 0.980 0.000 0.012 0.008
#&gt; SRR1274568     2  0.1701      0.921 0.016 0.936 0.000 0.048 0.000
#&gt; SRR1274569     1  0.1792      0.891 0.916 0.000 0.000 0.084 0.000
#&gt; SRR1274570     1  0.0000      0.983 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.983 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.983 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274576     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274577     2  0.0000      0.965 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274578     1  0.0000      0.983 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.983 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.983 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     4  0.4171      0.000 0.000 0.000 0.000 0.604 0.396
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.0858      0.932 0.000 0.968 0.000 0.028 0.004 0.000
#&gt; SRR1274530     2  0.0858      0.932 0.000 0.968 0.000 0.028 0.004 0.000
#&gt; SRR1274531     2  0.1967      0.886 0.000 0.904 0.000 0.084 0.012 0.000
#&gt; SRR1274532     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274534     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274535     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274536     2  0.3215      0.834 0.000 0.828 0.000 0.072 0.100 0.000
#&gt; SRR1274537     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274540     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.0858      0.932 0.000 0.968 0.000 0.028 0.004 0.000
#&gt; SRR1274546     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274549     2  0.6430      0.358 0.000 0.560 0.200 0.140 0.100 0.000
#&gt; SRR1274550     5  0.1327      1.000 0.000 0.000 0.064 0.000 0.936 0.000
#&gt; SRR1274551     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.1327      1.000 0.000 0.000 0.064 0.000 0.936 0.000
#&gt; SRR1274553     5  0.1327      1.000 0.000 0.000 0.064 0.000 0.936 0.000
#&gt; SRR1274554     2  0.0972      0.930 0.000 0.964 0.000 0.008 0.028 0.000
#&gt; SRR1274555     3  0.0000      0.576 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274556     4  0.3684      0.000 0.000 0.000 0.332 0.664 0.004 0.000
#&gt; SRR1274557     3  0.0000      0.576 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274558     2  0.3323      0.725 0.000 0.752 0.000 0.000 0.008 0.240
#&gt; SRR1274559     2  0.3756      0.704 0.000 0.736 0.000 0.016 0.008 0.240
#&gt; SRR1274560     2  0.3756      0.704 0.000 0.736 0.000 0.016 0.008 0.240
#&gt; SRR1274561     3  0.5768      0.430 0.316 0.064 0.560 0.060 0.000 0.000
#&gt; SRR1274562     3  0.4530      0.449 0.356 0.000 0.600 0.044 0.000 0.000
#&gt; SRR1274563     3  0.0000      0.576 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274564     2  0.3215      0.834 0.000 0.828 0.000 0.072 0.100 0.000
#&gt; SRR1274565     2  0.1049      0.928 0.000 0.960 0.000 0.008 0.032 0.000
#&gt; SRR1274566     2  0.2258      0.892 0.000 0.896 0.000 0.044 0.060 0.000
#&gt; SRR1274567     2  0.2258      0.892 0.000 0.896 0.000 0.044 0.060 0.000
#&gt; SRR1274568     2  0.1327      0.908 0.000 0.936 0.000 0.000 0.000 0.064
#&gt; SRR1274569     1  0.1957      0.851 0.888 0.000 0.000 0.000 0.000 0.112
#&gt; SRR1274570     1  0.0000      0.977 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.977 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.977 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.0858      0.932 0.000 0.968 0.000 0.028 0.004 0.000
#&gt; SRR1274576     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274577     2  0.0000      0.943 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274578     1  0.0000      0.977 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.977 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.977 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     6  0.3076      0.000 0.000 0.000 0.000 0.240 0.000 0.760
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.995       0.998         0.4744 0.525   0.525
#> 3 3 0.626           0.775       0.886         0.2425 0.901   0.814
#> 4 4 0.580           0.716       0.808         0.1788 0.809   0.573
#> 5 5 0.668           0.672       0.788         0.0841 0.932   0.761
#> 6 6 0.789           0.634       0.810         0.0512 0.959   0.835
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      1.000 0.000 1.000
#&gt; SRR1274529     2   0.000      1.000 0.000 1.000
#&gt; SRR1274530     2   0.000      1.000 0.000 1.000
#&gt; SRR1274531     2   0.000      1.000 0.000 1.000
#&gt; SRR1274532     2   0.000      1.000 0.000 1.000
#&gt; SRR1274533     2   0.000      1.000 0.000 1.000
#&gt; SRR1274534     2   0.000      1.000 0.000 1.000
#&gt; SRR1274535     2   0.000      1.000 0.000 1.000
#&gt; SRR1274536     2   0.000      1.000 0.000 1.000
#&gt; SRR1274537     2   0.000      1.000 0.000 1.000
#&gt; SRR1274538     2   0.000      1.000 0.000 1.000
#&gt; SRR1274539     2   0.000      1.000 0.000 1.000
#&gt; SRR1274540     2   0.000      1.000 0.000 1.000
#&gt; SRR1274541     2   0.000      1.000 0.000 1.000
#&gt; SRR1274542     2   0.000      1.000 0.000 1.000
#&gt; SRR1274543     2   0.000      1.000 0.000 1.000
#&gt; SRR1274544     2   0.000      1.000 0.000 1.000
#&gt; SRR1274545     2   0.000      1.000 0.000 1.000
#&gt; SRR1274546     2   0.000      1.000 0.000 1.000
#&gt; SRR1274547     2   0.000      1.000 0.000 1.000
#&gt; SRR1274548     2   0.000      1.000 0.000 1.000
#&gt; SRR1274549     1   0.311      0.943 0.944 0.056
#&gt; SRR1274550     1   0.000      0.993 1.000 0.000
#&gt; SRR1274551     2   0.000      1.000 0.000 1.000
#&gt; SRR1274552     1   0.358      0.931 0.932 0.068
#&gt; SRR1274553     1   0.000      0.993 1.000 0.000
#&gt; SRR1274554     2   0.000      1.000 0.000 1.000
#&gt; SRR1274555     1   0.000      0.993 1.000 0.000
#&gt; SRR1274556     1   0.000      0.993 1.000 0.000
#&gt; SRR1274557     1   0.000      0.993 1.000 0.000
#&gt; SRR1274558     2   0.000      1.000 0.000 1.000
#&gt; SRR1274559     1   0.000      0.993 1.000 0.000
#&gt; SRR1274560     1   0.000      0.993 1.000 0.000
#&gt; SRR1274561     1   0.000      0.993 1.000 0.000
#&gt; SRR1274562     1   0.000      0.993 1.000 0.000
#&gt; SRR1274563     1   0.000      0.993 1.000 0.000
#&gt; SRR1274564     2   0.000      1.000 0.000 1.000
#&gt; SRR1274565     2   0.000      1.000 0.000 1.000
#&gt; SRR1274566     2   0.000      1.000 0.000 1.000
#&gt; SRR1274567     2   0.000      1.000 0.000 1.000
#&gt; SRR1274568     2   0.000      1.000 0.000 1.000
#&gt; SRR1274569     1   0.000      0.993 1.000 0.000
#&gt; SRR1274570     1   0.000      0.993 1.000 0.000
#&gt; SRR1274571     1   0.000      0.993 1.000 0.000
#&gt; SRR1274572     1   0.000      0.993 1.000 0.000
#&gt; SRR1274573     2   0.000      1.000 0.000 1.000
#&gt; SRR1274574     2   0.000      1.000 0.000 1.000
#&gt; SRR1274575     2   0.000      1.000 0.000 1.000
#&gt; SRR1274576     2   0.000      1.000 0.000 1.000
#&gt; SRR1274577     2   0.000      1.000 0.000 1.000
#&gt; SRR1274578     1   0.000      0.993 1.000 0.000
#&gt; SRR1274579     1   0.000      0.993 1.000 0.000
#&gt; SRR1274580     1   0.000      0.993 1.000 0.000
#&gt; SRR1274581     1   0.000      0.993 1.000 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274529     2  0.3551     0.8260 0.000 0.868 0.132
#&gt; SRR1274530     2  0.3551     0.8260 0.000 0.868 0.132
#&gt; SRR1274531     3  0.6309    -0.4177 0.000 0.496 0.504
#&gt; SRR1274532     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274533     2  0.5706     0.5907 0.000 0.680 0.320
#&gt; SRR1274534     2  0.4842     0.7217 0.000 0.776 0.224
#&gt; SRR1274535     2  0.5905     0.5333 0.000 0.648 0.352
#&gt; SRR1274536     2  0.6154     0.5366 0.000 0.592 0.408
#&gt; SRR1274537     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274539     2  0.4842     0.7217 0.000 0.776 0.224
#&gt; SRR1274540     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274545     2  0.1860     0.8649 0.000 0.948 0.052
#&gt; SRR1274546     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274549     3  0.0000     0.6897 0.000 0.000 1.000
#&gt; SRR1274550     3  0.3551     0.8035 0.132 0.000 0.868
#&gt; SRR1274551     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274552     3  0.3551     0.8035 0.132 0.000 0.868
#&gt; SRR1274553     3  0.3551     0.8035 0.132 0.000 0.868
#&gt; SRR1274554     2  0.5835     0.5560 0.000 0.660 0.340
#&gt; SRR1274555     3  0.3551     0.8035 0.132 0.000 0.868
#&gt; SRR1274556     3  0.3551     0.8035 0.132 0.000 0.868
#&gt; SRR1274557     3  0.3551     0.8035 0.132 0.000 0.868
#&gt; SRR1274558     2  0.0592     0.8774 0.012 0.988 0.000
#&gt; SRR1274559     1  0.3764     0.8296 0.892 0.040 0.068
#&gt; SRR1274560     1  0.2845     0.8597 0.920 0.012 0.068
#&gt; SRR1274561     1  0.5621     0.5555 0.692 0.000 0.308
#&gt; SRR1274562     1  0.4654     0.7223 0.792 0.000 0.208
#&gt; SRR1274563     3  0.3879     0.7799 0.152 0.000 0.848
#&gt; SRR1274564     2  0.3879     0.8203 0.000 0.848 0.152
#&gt; SRR1274565     2  0.3619     0.8252 0.000 0.864 0.136
#&gt; SRR1274566     2  0.3879     0.8203 0.000 0.848 0.152
#&gt; SRR1274567     2  0.6154     0.5366 0.000 0.592 0.408
#&gt; SRR1274568     2  0.3207     0.8374 0.012 0.904 0.084
#&gt; SRR1274569     1  0.0000     0.9145 1.000 0.000 0.000
#&gt; SRR1274570     1  0.0000     0.9145 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000     0.9145 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0000     0.9145 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274575     2  0.3551     0.8260 0.000 0.868 0.132
#&gt; SRR1274576     2  0.0000     0.8823 0.000 1.000 0.000
#&gt; SRR1274577     2  0.5098     0.6955 0.000 0.752 0.248
#&gt; SRR1274578     1  0.0000     0.9145 1.000 0.000 0.000
#&gt; SRR1274579     1  0.0000     0.9145 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000     0.9145 1.000 0.000 0.000
#&gt; SRR1274581     3  0.6309     0.0678 0.496 0.000 0.504
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.4222     0.5276 0.000 0.728 0.000 0.272
#&gt; SRR1274530     2  0.4222     0.5276 0.000 0.728 0.000 0.272
#&gt; SRR1274531     4  0.5678     0.5878 0.000 0.172 0.112 0.716
#&gt; SRR1274532     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274533     4  0.7013     0.6943 0.000 0.356 0.128 0.516
#&gt; SRR1274534     4  0.6735     0.6830 0.000 0.388 0.096 0.516
#&gt; SRR1274535     4  0.7013     0.6943 0.000 0.356 0.128 0.516
#&gt; SRR1274536     4  0.5742     0.5865 0.000 0.276 0.060 0.664
#&gt; SRR1274537     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274539     4  0.6735     0.6830 0.000 0.388 0.096 0.516
#&gt; SRR1274540     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.2973     0.7167 0.000 0.856 0.000 0.144
#&gt; SRR1274546     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274549     3  0.4134     0.6593 0.000 0.000 0.740 0.260
#&gt; SRR1274550     3  0.2704     0.7851 0.000 0.000 0.876 0.124
#&gt; SRR1274551     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.4304     0.6771 0.000 0.000 0.716 0.284
#&gt; SRR1274553     3  0.4193     0.6964 0.000 0.000 0.732 0.268
#&gt; SRR1274554     4  0.6972     0.6954 0.000 0.356 0.124 0.520
#&gt; SRR1274555     3  0.0188     0.8077 0.000 0.000 0.996 0.004
#&gt; SRR1274556     3  0.0336     0.8063 0.000 0.000 0.992 0.008
#&gt; SRR1274557     3  0.0188     0.8077 0.000 0.000 0.996 0.004
#&gt; SRR1274558     2  0.5442    -0.0719 0.028 0.636 0.000 0.336
#&gt; SRR1274559     1  0.5374     0.6384 0.688 0.020 0.012 0.280
#&gt; SRR1274560     1  0.4485     0.6891 0.740 0.000 0.012 0.248
#&gt; SRR1274561     1  0.7191     0.4166 0.516 0.000 0.328 0.156
#&gt; SRR1274562     1  0.4761     0.4404 0.628 0.000 0.372 0.000
#&gt; SRR1274563     3  0.0336     0.8028 0.008 0.000 0.992 0.000
#&gt; SRR1274564     4  0.4643     0.5307 0.000 0.344 0.000 0.656
#&gt; SRR1274565     4  0.4713     0.5128 0.000 0.360 0.000 0.640
#&gt; SRR1274566     4  0.4643     0.5307 0.000 0.344 0.000 0.656
#&gt; SRR1274567     4  0.5890     0.5861 0.000 0.268 0.072 0.660
#&gt; SRR1274568     4  0.6118     0.5873 0.028 0.412 0.012 0.548
#&gt; SRR1274569     1  0.1474     0.8191 0.948 0.000 0.000 0.052
#&gt; SRR1274570     1  0.1302     0.8206 0.956 0.000 0.000 0.044
#&gt; SRR1274571     1  0.1302     0.8206 0.956 0.000 0.000 0.044
#&gt; SRR1274572     1  0.1004     0.8176 0.972 0.000 0.004 0.024
#&gt; SRR1274573     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.8895 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.4222     0.5276 0.000 0.728 0.000 0.272
#&gt; SRR1274576     2  0.0592     0.8677 0.000 0.984 0.000 0.016
#&gt; SRR1274577     4  0.6766     0.6889 0.000 0.380 0.100 0.520
#&gt; SRR1274578     1  0.1661     0.8128 0.944 0.000 0.004 0.052
#&gt; SRR1274579     1  0.1661     0.8128 0.944 0.000 0.004 0.052
#&gt; SRR1274580     1  0.1661     0.8128 0.944 0.000 0.004 0.052
#&gt; SRR1274581     3  0.7449     0.2171 0.332 0.000 0.480 0.188
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.4532     0.5317 0.000 0.672 0.004 0.304 0.020
#&gt; SRR1274530     2  0.4532     0.5317 0.000 0.672 0.004 0.304 0.020
#&gt; SRR1274531     4  0.6005    -0.3638 0.000 0.036 0.044 0.508 0.412
#&gt; SRR1274532     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.6874     0.7546 0.000 0.136 0.052 0.264 0.548
#&gt; SRR1274534     5  0.6853     0.7530 0.000 0.148 0.044 0.264 0.544
#&gt; SRR1274535     5  0.6839     0.7525 0.000 0.132 0.052 0.264 0.552
#&gt; SRR1274536     4  0.2756     0.7627 0.000 0.096 0.012 0.880 0.012
#&gt; SRR1274537     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.6853     0.7530 0.000 0.148 0.044 0.264 0.544
#&gt; SRR1274540     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.2144     0.8312 0.000 0.912 0.000 0.068 0.020
#&gt; SRR1274546     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0404     0.8933 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1274548     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     4  0.4354     0.2917 0.000 0.000 0.368 0.624 0.008
#&gt; SRR1274550     3  0.3884     0.5613 0.000 0.000 0.708 0.004 0.288
#&gt; SRR1274551     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.5883     0.2378 0.000 0.000 0.388 0.104 0.508
#&gt; SRR1274553     5  0.5815     0.2160 0.000 0.000 0.396 0.096 0.508
#&gt; SRR1274554     5  0.7020     0.7379 0.000 0.140 0.052 0.292 0.516
#&gt; SRR1274555     3  0.0290     0.9078 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1274556     3  0.0566     0.9044 0.000 0.000 0.984 0.004 0.012
#&gt; SRR1274557     3  0.0404     0.9075 0.000 0.000 0.988 0.000 0.012
#&gt; SRR1274558     2  0.6538    -0.2097 0.008 0.444 0.000 0.152 0.396
#&gt; SRR1274559     1  0.6505     0.4807 0.440 0.000 0.004 0.164 0.392
#&gt; SRR1274560     1  0.6451     0.4941 0.452 0.000 0.004 0.156 0.388
#&gt; SRR1274561     1  0.8233     0.3686 0.332 0.000 0.296 0.116 0.256
#&gt; SRR1274562     1  0.6029     0.2311 0.456 0.000 0.448 0.008 0.088
#&gt; SRR1274563     3  0.0324     0.9040 0.000 0.000 0.992 0.004 0.004
#&gt; SRR1274564     4  0.2329     0.7647 0.000 0.124 0.000 0.876 0.000
#&gt; SRR1274565     4  0.2864     0.7479 0.000 0.136 0.000 0.852 0.012
#&gt; SRR1274566     4  0.2329     0.7647 0.000 0.124 0.000 0.876 0.000
#&gt; SRR1274567     4  0.2756     0.7627 0.000 0.096 0.012 0.880 0.012
#&gt; SRR1274568     5  0.5895     0.5321 0.008 0.148 0.000 0.220 0.624
#&gt; SRR1274569     1  0.4178     0.6775 0.748 0.000 0.004 0.028 0.220
#&gt; SRR1274570     1  0.3951     0.6826 0.776 0.000 0.004 0.028 0.192
#&gt; SRR1274571     1  0.3951     0.6826 0.776 0.000 0.004 0.028 0.192
#&gt; SRR1274572     1  0.0000     0.6694 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.9011 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.4532     0.5317 0.000 0.672 0.004 0.304 0.020
#&gt; SRR1274576     2  0.1608     0.8384 0.000 0.928 0.000 0.000 0.072
#&gt; SRR1274577     5  0.6871     0.7285 0.000 0.144 0.040 0.292 0.524
#&gt; SRR1274578     1  0.2142     0.6547 0.920 0.000 0.004 0.028 0.048
#&gt; SRR1274579     1  0.2142     0.6547 0.920 0.000 0.004 0.028 0.048
#&gt; SRR1274580     1  0.2142     0.6547 0.920 0.000 0.004 0.028 0.048
#&gt; SRR1274581     1  0.8412     0.0807 0.352 0.000 0.188 0.260 0.200
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.5798     0.0363 0.000 0.456 0.008 0.436 0.020 0.080
#&gt; SRR1274530     2  0.5798     0.0363 0.000 0.456 0.008 0.436 0.020 0.080
#&gt; SRR1274531     5  0.3198     0.5271 0.000 0.000 0.000 0.260 0.740 0.000
#&gt; SRR1274532     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.1007     0.8090 0.000 0.044 0.000 0.000 0.956 0.000
#&gt; SRR1274534     5  0.1141     0.8091 0.000 0.052 0.000 0.000 0.948 0.000
#&gt; SRR1274535     5  0.1007     0.8090 0.000 0.044 0.000 0.000 0.956 0.000
#&gt; SRR1274536     4  0.3235     0.9220 0.000 0.052 0.000 0.820 0.128 0.000
#&gt; SRR1274537     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.1141     0.8091 0.000 0.052 0.000 0.000 0.948 0.000
#&gt; SRR1274540     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.3137     0.7627 0.000 0.860 0.008 0.036 0.020 0.076
#&gt; SRR1274546     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0603     0.8496 0.000 0.980 0.000 0.000 0.016 0.004
#&gt; SRR1274548     2  0.0146     0.8601 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1274549     4  0.5247     0.5635 0.000 0.000 0.260 0.620 0.108 0.012
#&gt; SRR1274550     3  0.6256     0.1070 0.000 0.000 0.480 0.064 0.360 0.096
#&gt; SRR1274551     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.5937     0.4870 0.000 0.000 0.136 0.096 0.628 0.140
#&gt; SRR1274553     5  0.5937     0.4870 0.000 0.000 0.136 0.096 0.628 0.140
#&gt; SRR1274554     5  0.1700     0.8056 0.000 0.048 0.000 0.024 0.928 0.000
#&gt; SRR1274555     3  0.0632     0.7626 0.000 0.000 0.976 0.000 0.024 0.000
#&gt; SRR1274556     3  0.1149     0.7568 0.000 0.000 0.960 0.008 0.024 0.008
#&gt; SRR1274557     3  0.0632     0.7626 0.000 0.000 0.976 0.000 0.024 0.000
#&gt; SRR1274558     2  0.7098    -0.1851 0.332 0.376 0.004 0.068 0.220 0.000
#&gt; SRR1274559     1  0.5042     0.5409 0.700 0.000 0.008 0.108 0.164 0.020
#&gt; SRR1274560     1  0.5000     0.5435 0.704 0.000 0.008 0.104 0.164 0.020
#&gt; SRR1274561     1  0.5374     0.4742 0.656 0.000 0.188 0.132 0.008 0.016
#&gt; SRR1274562     3  0.5462    -0.0514 0.404 0.000 0.492 0.008 0.000 0.096
#&gt; SRR1274563     3  0.0891     0.7604 0.000 0.000 0.968 0.008 0.024 0.000
#&gt; SRR1274564     4  0.3254     0.9214 0.000 0.056 0.000 0.820 0.124 0.000
#&gt; SRR1274565     4  0.3627     0.9144 0.000 0.056 0.000 0.800 0.136 0.008
#&gt; SRR1274566     4  0.3463     0.9222 0.000 0.056 0.000 0.816 0.120 0.008
#&gt; SRR1274567     4  0.3444     0.9226 0.000 0.052 0.000 0.816 0.124 0.008
#&gt; SRR1274568     5  0.5715     0.2830 0.328 0.040 0.004 0.068 0.560 0.000
#&gt; SRR1274569     1  0.0000     0.5551 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.1556     0.5094 0.920 0.000 0.000 0.000 0.000 0.080
#&gt; SRR1274571     1  0.1556     0.5094 0.920 0.000 0.000 0.000 0.000 0.080
#&gt; SRR1274572     1  0.3804    -0.4961 0.576 0.000 0.000 0.000 0.000 0.424
#&gt; SRR1274573     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.8628 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.5798     0.0363 0.000 0.456 0.008 0.436 0.020 0.080
#&gt; SRR1274576     2  0.2340     0.7350 0.000 0.852 0.000 0.000 0.148 0.000
#&gt; SRR1274577     5  0.1765     0.8047 0.000 0.052 0.000 0.024 0.924 0.000
#&gt; SRR1274578     6  0.3804     0.6906 0.424 0.000 0.000 0.000 0.000 0.576
#&gt; SRR1274579     6  0.3804     0.6906 0.424 0.000 0.000 0.000 0.000 0.576
#&gt; SRR1274580     6  0.3804     0.6906 0.424 0.000 0.000 0.000 0.000 0.576
#&gt; SRR1274581     6  0.4658     0.2658 0.012 0.000 0.084 0.140 0.020 0.744
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.923           0.937       0.973         0.5016 0.502   0.502
#> 3 3 0.894           0.924       0.965         0.3182 0.718   0.496
#> 4 4 0.853           0.868       0.936         0.1223 0.866   0.627
#> 5 5 0.835           0.832       0.913         0.0627 0.920   0.705
#> 6 6 0.814           0.808       0.888         0.0308 0.962   0.824
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.964 0.000 1.000
#&gt; SRR1274529     2   0.000      0.964 0.000 1.000
#&gt; SRR1274530     2   0.000      0.964 0.000 1.000
#&gt; SRR1274531     2   0.706      0.766 0.192 0.808
#&gt; SRR1274532     2   0.000      0.964 0.000 1.000
#&gt; SRR1274533     2   0.000      0.964 0.000 1.000
#&gt; SRR1274534     2   0.000      0.964 0.000 1.000
#&gt; SRR1274535     2   0.996      0.168 0.464 0.536
#&gt; SRR1274536     2   0.615      0.816 0.152 0.848
#&gt; SRR1274537     2   0.000      0.964 0.000 1.000
#&gt; SRR1274538     2   0.000      0.964 0.000 1.000
#&gt; SRR1274539     2   0.000      0.964 0.000 1.000
#&gt; SRR1274540     2   0.000      0.964 0.000 1.000
#&gt; SRR1274541     2   0.000      0.964 0.000 1.000
#&gt; SRR1274542     2   0.000      0.964 0.000 1.000
#&gt; SRR1274543     2   0.000      0.964 0.000 1.000
#&gt; SRR1274544     2   0.000      0.964 0.000 1.000
#&gt; SRR1274545     2   0.000      0.964 0.000 1.000
#&gt; SRR1274546     2   0.000      0.964 0.000 1.000
#&gt; SRR1274547     2   0.000      0.964 0.000 1.000
#&gt; SRR1274548     2   0.000      0.964 0.000 1.000
#&gt; SRR1274549     1   0.000      0.981 1.000 0.000
#&gt; SRR1274550     1   0.000      0.981 1.000 0.000
#&gt; SRR1274551     2   0.000      0.964 0.000 1.000
#&gt; SRR1274552     1   0.000      0.981 1.000 0.000
#&gt; SRR1274553     1   0.000      0.981 1.000 0.000
#&gt; SRR1274554     2   0.224      0.935 0.036 0.964
#&gt; SRR1274555     1   0.000      0.981 1.000 0.000
#&gt; SRR1274556     1   0.000      0.981 1.000 0.000
#&gt; SRR1274557     1   0.000      0.981 1.000 0.000
#&gt; SRR1274558     2   0.730      0.736 0.204 0.796
#&gt; SRR1274559     1   0.000      0.981 1.000 0.000
#&gt; SRR1274560     1   0.000      0.981 1.000 0.000
#&gt; SRR1274561     1   0.000      0.981 1.000 0.000
#&gt; SRR1274562     1   0.000      0.981 1.000 0.000
#&gt; SRR1274563     1   0.000      0.981 1.000 0.000
#&gt; SRR1274564     2   0.000      0.964 0.000 1.000
#&gt; SRR1274565     2   0.000      0.964 0.000 1.000
#&gt; SRR1274566     2   0.000      0.964 0.000 1.000
#&gt; SRR1274567     1   0.788      0.674 0.764 0.236
#&gt; SRR1274568     1   0.388      0.911 0.924 0.076
#&gt; SRR1274569     1   0.000      0.981 1.000 0.000
#&gt; SRR1274570     1   0.000      0.981 1.000 0.000
#&gt; SRR1274571     1   0.000      0.981 1.000 0.000
#&gt; SRR1274572     1   0.000      0.981 1.000 0.000
#&gt; SRR1274573     2   0.000      0.964 0.000 1.000
#&gt; SRR1274574     2   0.000      0.964 0.000 1.000
#&gt; SRR1274575     2   0.000      0.964 0.000 1.000
#&gt; SRR1274576     2   0.000      0.964 0.000 1.000
#&gt; SRR1274577     1   0.388      0.911 0.924 0.076
#&gt; SRR1274578     1   0.000      0.981 1.000 0.000
#&gt; SRR1274579     1   0.000      0.981 1.000 0.000
#&gt; SRR1274580     1   0.000      0.981 1.000 0.000
#&gt; SRR1274581     1   0.000      0.981 1.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0747      0.979 0.000 0.984 0.016
#&gt; SRR1274530     2  0.0747      0.979 0.000 0.984 0.016
#&gt; SRR1274531     3  0.0000      0.932 0.000 0.000 1.000
#&gt; SRR1274532     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274533     3  0.0747      0.931 0.000 0.016 0.984
#&gt; SRR1274534     3  0.4887      0.731 0.000 0.228 0.772
#&gt; SRR1274535     3  0.0747      0.931 0.000 0.016 0.984
#&gt; SRR1274536     3  0.0000      0.932 0.000 0.000 1.000
#&gt; SRR1274537     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274539     3  0.4887      0.731 0.000 0.228 0.772
#&gt; SRR1274540     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0747      0.979 0.000 0.984 0.016
#&gt; SRR1274546     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274549     3  0.0000      0.932 0.000 0.000 1.000
#&gt; SRR1274550     3  0.0747      0.934 0.016 0.000 0.984
#&gt; SRR1274551     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274552     3  0.0892      0.933 0.020 0.000 0.980
#&gt; SRR1274553     3  0.0892      0.933 0.020 0.000 0.980
#&gt; SRR1274554     3  0.0747      0.931 0.000 0.016 0.984
#&gt; SRR1274555     3  0.0747      0.934 0.016 0.000 0.984
#&gt; SRR1274556     3  0.0747      0.934 0.016 0.000 0.984
#&gt; SRR1274557     3  0.0747      0.934 0.016 0.000 0.984
#&gt; SRR1274558     1  0.6045      0.386 0.620 0.380 0.000
#&gt; SRR1274559     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274561     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274562     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274563     3  0.1163      0.928 0.028 0.000 0.972
#&gt; SRR1274564     2  0.3192      0.887 0.000 0.888 0.112
#&gt; SRR1274565     2  0.0747      0.979 0.000 0.984 0.016
#&gt; SRR1274566     2  0.3038      0.896 0.000 0.896 0.104
#&gt; SRR1274567     3  0.0237      0.932 0.004 0.000 0.996
#&gt; SRR1274568     1  0.0747      0.934 0.984 0.016 0.000
#&gt; SRR1274569     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0747      0.979 0.000 0.984 0.016
#&gt; SRR1274576     2  0.0000      0.986 0.000 1.000 0.000
#&gt; SRR1274577     3  0.6629      0.436 0.360 0.016 0.624
#&gt; SRR1274578     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.949 1.000 0.000 0.000
#&gt; SRR1274581     1  0.4291      0.750 0.820 0.000 0.180
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274529     4  0.4898      0.476 0.000 0.416 0.000 0.584
#&gt; SRR1274530     4  0.4898      0.476 0.000 0.416 0.000 0.584
#&gt; SRR1274531     3  0.3688      0.812 0.000 0.000 0.792 0.208
#&gt; SRR1274532     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274533     3  0.0000      0.917 0.000 0.000 1.000 0.000
#&gt; SRR1274534     3  0.2149      0.855 0.000 0.088 0.912 0.000
#&gt; SRR1274535     3  0.0000      0.917 0.000 0.000 1.000 0.000
#&gt; SRR1274536     4  0.0000      0.747 0.000 0.000 0.000 1.000
#&gt; SRR1274537     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274539     3  0.2149      0.855 0.000 0.088 0.912 0.000
#&gt; SRR1274540     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.1302      0.911 0.000 0.956 0.000 0.044
#&gt; SRR1274546     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274549     4  0.3726      0.502 0.000 0.000 0.212 0.788
#&gt; SRR1274550     3  0.0336      0.918 0.000 0.000 0.992 0.008
#&gt; SRR1274551     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.0336      0.918 0.000 0.000 0.992 0.008
#&gt; SRR1274553     3  0.0336      0.918 0.000 0.000 0.992 0.008
#&gt; SRR1274554     3  0.0469      0.915 0.000 0.000 0.988 0.012
#&gt; SRR1274555     3  0.3160      0.880 0.020 0.000 0.872 0.108
#&gt; SRR1274556     3  0.3658      0.858 0.020 0.000 0.836 0.144
#&gt; SRR1274557     3  0.2469      0.887 0.000 0.000 0.892 0.108
#&gt; SRR1274558     2  0.4907      0.255 0.420 0.580 0.000 0.000
#&gt; SRR1274559     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.0592      0.960 0.984 0.000 0.000 0.016
#&gt; SRR1274562     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274563     3  0.4608      0.826 0.096 0.000 0.800 0.104
#&gt; SRR1274564     4  0.0336      0.751 0.000 0.008 0.000 0.992
#&gt; SRR1274565     4  0.2654      0.743 0.000 0.108 0.004 0.888
#&gt; SRR1274566     4  0.0376      0.750 0.000 0.004 0.004 0.992
#&gt; SRR1274567     4  0.0000      0.747 0.000 0.000 0.000 1.000
#&gt; SRR1274568     1  0.1767      0.927 0.944 0.012 0.044 0.000
#&gt; SRR1274569     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.962 0.000 1.000 0.000 0.000
#&gt; SRR1274575     4  0.4898      0.476 0.000 0.416 0.000 0.584
#&gt; SRR1274576     2  0.0188      0.958 0.000 0.996 0.004 0.000
#&gt; SRR1274577     3  0.1610      0.901 0.032 0.000 0.952 0.016
#&gt; SRR1274578     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.972 1.000 0.000 0.000 0.000
#&gt; SRR1274581     1  0.5109      0.674 0.736 0.000 0.052 0.212
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.3177      0.792 0.000 0.208 0.000 0.792 0.000
#&gt; SRR1274530     4  0.3177      0.792 0.000 0.208 0.000 0.792 0.000
#&gt; SRR1274531     3  0.5382      0.556 0.000 0.000 0.656 0.120 0.224
#&gt; SRR1274532     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.1732      0.962 0.000 0.000 0.080 0.000 0.920
#&gt; SRR1274534     5  0.1670      0.969 0.000 0.012 0.052 0.000 0.936
#&gt; SRR1274535     5  0.1671      0.966 0.000 0.000 0.076 0.000 0.924
#&gt; SRR1274536     4  0.0290      0.872 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1274537     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.1670      0.969 0.000 0.012 0.052 0.000 0.936
#&gt; SRR1274540     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.2561      0.800 0.000 0.856 0.000 0.144 0.000
#&gt; SRR1274546     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     3  0.3424      0.678 0.000 0.000 0.760 0.240 0.000
#&gt; SRR1274550     3  0.2127      0.796 0.000 0.000 0.892 0.000 0.108
#&gt; SRR1274551     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.2732      0.764 0.000 0.000 0.840 0.000 0.160
#&gt; SRR1274553     3  0.2732      0.764 0.000 0.000 0.840 0.000 0.160
#&gt; SRR1274554     5  0.1478      0.970 0.000 0.000 0.064 0.000 0.936
#&gt; SRR1274555     3  0.0000      0.821 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     3  0.0000      0.821 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274557     3  0.0880      0.818 0.000 0.000 0.968 0.000 0.032
#&gt; SRR1274558     1  0.4708      0.211 0.548 0.436 0.000 0.000 0.016
#&gt; SRR1274559     1  0.0510      0.838 0.984 0.000 0.000 0.000 0.016
#&gt; SRR1274560     1  0.0510      0.838 0.984 0.000 0.000 0.000 0.016
#&gt; SRR1274561     1  0.3039      0.745 0.836 0.000 0.152 0.000 0.012
#&gt; SRR1274562     1  0.5151      0.539 0.644 0.000 0.300 0.008 0.048
#&gt; SRR1274563     3  0.0000      0.821 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274564     4  0.0290      0.872 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1274565     4  0.0290      0.871 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1274566     4  0.0290      0.872 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1274567     4  0.0290      0.872 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1274568     1  0.4192      0.294 0.596 0.000 0.000 0.000 0.404
#&gt; SRR1274569     1  0.0162      0.840 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1274570     1  0.0162      0.841 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274571     1  0.0162      0.841 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274572     1  0.2352      0.834 0.912 0.000 0.032 0.008 0.048
#&gt; SRR1274573     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.970 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.3177      0.792 0.000 0.208 0.000 0.792 0.000
#&gt; SRR1274576     2  0.3684      0.605 0.000 0.720 0.000 0.000 0.280
#&gt; SRR1274577     5  0.0566      0.928 0.004 0.000 0.012 0.000 0.984
#&gt; SRR1274578     1  0.2352      0.834 0.912 0.000 0.032 0.008 0.048
#&gt; SRR1274579     1  0.2352      0.834 0.912 0.000 0.032 0.008 0.048
#&gt; SRR1274580     1  0.2352      0.834 0.912 0.000 0.032 0.008 0.048
#&gt; SRR1274581     3  0.5302      0.298 0.336 0.000 0.608 0.008 0.048
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.4563      0.658 0.056 0.284 0.000 0.656 0.004 0.000
#&gt; SRR1274530     4  0.4581      0.653 0.056 0.288 0.000 0.652 0.004 0.000
#&gt; SRR1274531     3  0.4556      0.666 0.000 0.000 0.696 0.188 0.116 0.000
#&gt; SRR1274532     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.1552      0.919 0.036 0.000 0.020 0.000 0.940 0.004
#&gt; SRR1274534     5  0.0363      0.936 0.000 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1274535     5  0.1498      0.916 0.028 0.000 0.032 0.000 0.940 0.000
#&gt; SRR1274536     4  0.0146      0.782 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1274537     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.0363      0.936 0.000 0.012 0.000 0.000 0.988 0.000
#&gt; SRR1274540     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.3079      0.804 0.056 0.844 0.000 0.096 0.004 0.000
#&gt; SRR1274546     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.1429      0.921 0.052 0.940 0.000 0.004 0.004 0.000
#&gt; SRR1274548     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274549     3  0.3482      0.595 0.000 0.000 0.684 0.316 0.000 0.000
#&gt; SRR1274550     3  0.2917      0.772 0.016 0.000 0.840 0.000 0.136 0.008
#&gt; SRR1274551     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.4154      0.674 0.036 0.000 0.712 0.000 0.244 0.008
#&gt; SRR1274553     3  0.4130      0.678 0.036 0.000 0.716 0.000 0.240 0.008
#&gt; SRR1274554     5  0.1555      0.918 0.040 0.000 0.012 0.008 0.940 0.000
#&gt; SRR1274555     3  0.0146      0.818 0.004 0.000 0.996 0.000 0.000 0.000
#&gt; SRR1274556     3  0.0000      0.818 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274557     3  0.0146      0.818 0.004 0.000 0.996 0.000 0.000 0.000
#&gt; SRR1274558     1  0.2775      0.648 0.856 0.104 0.000 0.000 0.000 0.040
#&gt; SRR1274559     1  0.2378      0.728 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1274560     1  0.2378      0.728 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1274561     1  0.5336      0.592 0.592 0.000 0.180 0.000 0.000 0.228
#&gt; SRR1274562     6  0.3954      0.481 0.012 0.000 0.352 0.000 0.000 0.636
#&gt; SRR1274563     3  0.0146      0.818 0.004 0.000 0.996 0.000 0.000 0.000
#&gt; SRR1274564     4  0.0146      0.782 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR1274565     4  0.1049      0.775 0.032 0.000 0.000 0.960 0.008 0.000
#&gt; SRR1274566     4  0.0717      0.781 0.016 0.000 0.000 0.976 0.008 0.000
#&gt; SRR1274567     4  0.0717      0.781 0.016 0.000 0.000 0.976 0.008 0.000
#&gt; SRR1274568     1  0.2560      0.657 0.872 0.000 0.000 0.000 0.092 0.036
#&gt; SRR1274569     1  0.3804      0.610 0.576 0.000 0.000 0.000 0.000 0.424
#&gt; SRR1274570     1  0.3851      0.564 0.540 0.000 0.000 0.000 0.000 0.460
#&gt; SRR1274571     1  0.3847      0.571 0.544 0.000 0.000 0.000 0.000 0.456
#&gt; SRR1274572     6  0.0713      0.815 0.028 0.000 0.000 0.000 0.000 0.972
#&gt; SRR1274573     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.4581      0.653 0.056 0.288 0.000 0.652 0.004 0.000
#&gt; SRR1274576     2  0.3352      0.738 0.032 0.792 0.000 0.000 0.176 0.000
#&gt; SRR1274577     5  0.2928      0.856 0.056 0.000 0.000 0.004 0.856 0.084
#&gt; SRR1274578     6  0.0260      0.832 0.008 0.000 0.000 0.000 0.000 0.992
#&gt; SRR1274579     6  0.0260      0.832 0.008 0.000 0.000 0.000 0.000 0.992
#&gt; SRR1274580     6  0.0260      0.832 0.008 0.000 0.000 0.000 0.000 0.992
#&gt; SRR1274581     6  0.2809      0.701 0.004 0.000 0.168 0.004 0.000 0.824
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.820           0.892       0.953         0.4152 0.609   0.609
#> 3 3 0.911           0.876       0.936         0.2619 0.844   0.748
#> 4 4 0.831           0.846       0.921         0.1367 0.957   0.910
#> 5 5 1.000           0.948       0.980         0.1743 0.822   0.612
#> 6 6 1.000           0.974       0.989         0.0487 0.957   0.859
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 3 5
```

There is also optional best $k$ = 3 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.938 0.000 1.000
#&gt; SRR1274529     2   0.000      0.938 0.000 1.000
#&gt; SRR1274530     2   0.000      0.938 0.000 1.000
#&gt; SRR1274531     2   0.416      0.871 0.084 0.916
#&gt; SRR1274532     2   0.000      0.938 0.000 1.000
#&gt; SRR1274533     2   0.000      0.938 0.000 1.000
#&gt; SRR1274534     2   0.000      0.938 0.000 1.000
#&gt; SRR1274535     2   0.000      0.938 0.000 1.000
#&gt; SRR1274536     2   0.861      0.647 0.284 0.716
#&gt; SRR1274537     2   0.000      0.938 0.000 1.000
#&gt; SRR1274538     2   0.000      0.938 0.000 1.000
#&gt; SRR1274539     2   0.000      0.938 0.000 1.000
#&gt; SRR1274540     2   0.000      0.938 0.000 1.000
#&gt; SRR1274541     2   0.000      0.938 0.000 1.000
#&gt; SRR1274542     2   0.000      0.938 0.000 1.000
#&gt; SRR1274543     2   0.000      0.938 0.000 1.000
#&gt; SRR1274544     2   0.000      0.938 0.000 1.000
#&gt; SRR1274545     2   0.000      0.938 0.000 1.000
#&gt; SRR1274546     2   0.000      0.938 0.000 1.000
#&gt; SRR1274547     2   0.000      0.938 0.000 1.000
#&gt; SRR1274548     2   0.000      0.938 0.000 1.000
#&gt; SRR1274549     2   0.866      0.641 0.288 0.712
#&gt; SRR1274550     2   0.866      0.641 0.288 0.712
#&gt; SRR1274551     2   0.000      0.938 0.000 1.000
#&gt; SRR1274552     2   0.861      0.647 0.284 0.716
#&gt; SRR1274553     2   0.876      0.628 0.296 0.704
#&gt; SRR1274554     2   0.000      0.938 0.000 1.000
#&gt; SRR1274555     1   0.000      0.971 1.000 0.000
#&gt; SRR1274556     2   0.980      0.369 0.416 0.584
#&gt; SRR1274557     1   0.921      0.410 0.664 0.336
#&gt; SRR1274558     2   0.000      0.938 0.000 1.000
#&gt; SRR1274559     1   0.000      0.971 1.000 0.000
#&gt; SRR1274560     1   0.000      0.971 1.000 0.000
#&gt; SRR1274561     1   0.000      0.971 1.000 0.000
#&gt; SRR1274562     1   0.000      0.971 1.000 0.000
#&gt; SRR1274563     1   0.000      0.971 1.000 0.000
#&gt; SRR1274564     2   0.000      0.938 0.000 1.000
#&gt; SRR1274565     2   0.000      0.938 0.000 1.000
#&gt; SRR1274566     2   0.000      0.938 0.000 1.000
#&gt; SRR1274567     2   0.866      0.641 0.288 0.712
#&gt; SRR1274568     2   0.000      0.938 0.000 1.000
#&gt; SRR1274569     1   0.000      0.971 1.000 0.000
#&gt; SRR1274570     1   0.000      0.971 1.000 0.000
#&gt; SRR1274571     1   0.000      0.971 1.000 0.000
#&gt; SRR1274572     1   0.000      0.971 1.000 0.000
#&gt; SRR1274573     2   0.000      0.938 0.000 1.000
#&gt; SRR1274574     2   0.000      0.938 0.000 1.000
#&gt; SRR1274575     2   0.000      0.938 0.000 1.000
#&gt; SRR1274576     2   0.000      0.938 0.000 1.000
#&gt; SRR1274577     2   0.000      0.938 0.000 1.000
#&gt; SRR1274578     1   0.000      0.971 1.000 0.000
#&gt; SRR1274579     1   0.000      0.971 1.000 0.000
#&gt; SRR1274580     1   0.000      0.971 1.000 0.000
#&gt; SRR1274581     2   0.000      0.938 0.000 1.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274529     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274530     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274531     2   0.280      0.871 0.000 0.908 0.092
#&gt; SRR1274532     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274533     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274534     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274535     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274536     2   0.536      0.570 0.000 0.724 0.276
#&gt; SRR1274537     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274538     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274539     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274540     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274541     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274542     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274543     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274544     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274545     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274546     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274547     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274548     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274549     3   0.000      0.840 0.000 0.000 1.000
#&gt; SRR1274550     3   0.000      0.840 0.000 0.000 1.000
#&gt; SRR1274551     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274552     3   0.629      0.110 0.000 0.464 0.536
#&gt; SRR1274553     3   0.271      0.732 0.000 0.088 0.912
#&gt; SRR1274554     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274555     3   0.000      0.840 0.000 0.000 1.000
#&gt; SRR1274556     3   0.000      0.840 0.000 0.000 1.000
#&gt; SRR1274557     3   0.000      0.840 0.000 0.000 1.000
#&gt; SRR1274558     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274559     1   0.536      0.824 0.724 0.000 0.276
#&gt; SRR1274560     1   0.536      0.824 0.724 0.000 0.276
#&gt; SRR1274561     1   0.536      0.824 0.724 0.000 0.276
#&gt; SRR1274562     1   0.581      0.756 0.664 0.000 0.336
#&gt; SRR1274563     3   0.000      0.840 0.000 0.000 1.000
#&gt; SRR1274564     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274565     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274566     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274567     2   0.536      0.570 0.000 0.724 0.276
#&gt; SRR1274568     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274569     1   0.536      0.824 0.724 0.000 0.276
#&gt; SRR1274570     1   0.518      0.823 0.744 0.000 0.256
#&gt; SRR1274571     1   0.536      0.824 0.724 0.000 0.276
#&gt; SRR1274572     1   0.000      0.750 1.000 0.000 0.000
#&gt; SRR1274573     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274574     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274575     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274576     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274577     2   0.000      0.969 0.000 1.000 0.000
#&gt; SRR1274578     1   0.000      0.750 1.000 0.000 0.000
#&gt; SRR1274579     1   0.000      0.750 1.000 0.000 0.000
#&gt; SRR1274580     1   0.000      0.750 1.000 0.000 0.000
#&gt; SRR1274581     2   0.536      0.649 0.276 0.724 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274530     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274531     2  0.7336      0.360 0.284 0.520 0.196 0.000
#&gt; SRR1274532     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274533     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274534     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274535     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274536     2  0.4304      0.709 0.284 0.716 0.000 0.000
#&gt; SRR1274537     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274539     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274540     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274549     3  0.4304      0.547 0.284 0.000 0.716 0.000
#&gt; SRR1274550     3  0.0000      0.814 0.000 0.000 1.000 0.000
#&gt; SRR1274551     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.5821      0.272 0.032 0.432 0.536 0.000
#&gt; SRR1274553     3  0.2149      0.741 0.000 0.088 0.912 0.000
#&gt; SRR1274554     2  0.4304      0.709 0.284 0.716 0.000 0.000
#&gt; SRR1274555     3  0.0000      0.814 0.000 0.000 1.000 0.000
#&gt; SRR1274556     3  0.0000      0.814 0.000 0.000 1.000 0.000
#&gt; SRR1274557     3  0.0000      0.814 0.000 0.000 1.000 0.000
#&gt; SRR1274558     2  0.0336      0.914 0.008 0.992 0.000 0.000
#&gt; SRR1274559     1  0.4304      0.985 0.716 0.000 0.000 0.284
#&gt; SRR1274560     1  0.4304      0.985 0.716 0.000 0.000 0.284
#&gt; SRR1274561     1  0.4304      0.985 0.716 0.000 0.000 0.284
#&gt; SRR1274562     1  0.5496      0.903 0.704 0.000 0.064 0.232
#&gt; SRR1274563     3  0.0000      0.814 0.000 0.000 1.000 0.000
#&gt; SRR1274564     2  0.4304      0.709 0.284 0.716 0.000 0.000
#&gt; SRR1274565     2  0.4304      0.709 0.284 0.716 0.000 0.000
#&gt; SRR1274566     2  0.4304      0.709 0.284 0.716 0.000 0.000
#&gt; SRR1274567     2  0.4304      0.709 0.284 0.716 0.000 0.000
#&gt; SRR1274568     2  0.0336      0.914 0.008 0.992 0.000 0.000
#&gt; SRR1274569     1  0.4304      0.985 0.716 0.000 0.000 0.284
#&gt; SRR1274570     1  0.4304      0.985 0.716 0.000 0.000 0.284
#&gt; SRR1274571     1  0.4304      0.985 0.716 0.000 0.000 0.284
#&gt; SRR1274572     1  0.4356      0.977 0.708 0.000 0.000 0.292
#&gt; SRR1274573     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274576     2  0.0000      0.920 0.000 1.000 0.000 0.000
#&gt; SRR1274577     2  0.4304      0.709 0.284 0.716 0.000 0.000
#&gt; SRR1274578     4  0.0000      0.825 0.000 0.000 0.000 1.000
#&gt; SRR1274579     4  0.0000      0.825 0.000 0.000 0.000 1.000
#&gt; SRR1274580     4  0.0000      0.825 0.000 0.000 0.000 1.000
#&gt; SRR1274581     4  0.4304      0.568 0.284 0.000 0.000 0.716
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274530     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274531     4   0.000      0.973 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274532     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274534     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274535     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274536     4   0.000      0.973 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274537     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274540     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274546     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274548     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     4   0.000      0.973 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274550     3   0.000      0.968 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274551     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     2   0.499      0.335 0.000 0.600 0.360 0.040 0.000
#&gt; SRR1274553     3   0.185      0.835 0.000 0.088 0.912 0.000 0.000
#&gt; SRR1274554     4   0.179      0.855 0.000 0.084 0.000 0.916 0.000
#&gt; SRR1274555     3   0.000      0.968 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     3   0.000      0.968 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274557     3   0.000      0.968 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274558     2   0.148      0.919 0.064 0.936 0.000 0.000 0.000
#&gt; SRR1274559     1   0.000      0.975 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274560     1   0.000      0.975 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274561     1   0.000      0.975 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274562     1   0.196      0.892 0.904 0.000 0.096 0.000 0.000
#&gt; SRR1274563     3   0.000      0.968 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274564     4   0.000      0.973 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274565     4   0.000      0.973 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274566     4   0.000      0.973 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274567     4   0.000      0.973 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274568     2   0.148      0.919 0.064 0.936 0.000 0.000 0.000
#&gt; SRR1274569     1   0.000      0.975 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1   0.000      0.975 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1   0.000      0.975 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1   0.148      0.927 0.936 0.000 0.000 0.000 0.064
#&gt; SRR1274573     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274576     2   0.000      0.979 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274577     4   0.104      0.927 0.000 0.040 0.000 0.960 0.000
#&gt; SRR1274578     5   0.000      0.930 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274579     5   0.000      0.930 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274580     5   0.000      0.930 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274581     5   0.293      0.776 0.000 0.000 0.000 0.180 0.820
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274530     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274531     4  0.0000      0.974 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274532     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     2  0.0713      0.969 0.000 0.972 0.000 0.000 0.028 0.000
#&gt; SRR1274534     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274535     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274536     4  0.0000      0.974 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274537     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274540     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274549     4  0.0000      0.974 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274550     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274551     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274553     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274554     4  0.1610      0.859 0.000 0.084 0.000 0.916 0.000 0.000
#&gt; SRR1274555     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274556     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274557     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274558     2  0.1327      0.934 0.064 0.936 0.000 0.000 0.000 0.000
#&gt; SRR1274559     1  0.0000      0.976 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.976 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.0000      0.976 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274562     1  0.1765      0.897 0.904 0.000 0.096 0.000 0.000 0.000
#&gt; SRR1274563     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274564     4  0.0000      0.974 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274565     4  0.0000      0.974 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274566     4  0.0000      0.974 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274567     4  0.0000      0.974 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274568     2  0.1327      0.934 0.064 0.936 0.000 0.000 0.000 0.000
#&gt; SRR1274569     1  0.0000      0.976 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.976 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.976 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.1327      0.928 0.936 0.000 0.000 0.000 0.000 0.064
#&gt; SRR1274573     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274576     2  0.0000      0.993 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274577     4  0.0937      0.929 0.000 0.040 0.000 0.960 0.000 0.000
#&gt; SRR1274578     6  0.0000      0.935 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274579     6  0.0000      0.935 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274580     6  0.0000      0.935 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274581     6  0.3235      0.791 0.000 0.000 0.000 0.128 0.052 0.820
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.759           0.950       0.965         0.4504 0.525   0.525
#> 3 3 0.430           0.467       0.719         0.3199 0.709   0.490
#> 4 4 0.473           0.706       0.767         0.1476 0.778   0.504
#> 5 5 0.608           0.402       0.667         0.1466 0.845   0.574
#> 6 6 0.712           0.607       0.745         0.0255 0.847   0.454
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000      0.910 0.000 1.000
#&gt; SRR1274529     2  0.5629      0.891 0.132 0.868
#&gt; SRR1274530     2  0.5629      0.891 0.132 0.868
#&gt; SRR1274531     1  0.0938      0.992 0.988 0.012
#&gt; SRR1274532     2  0.0000      0.910 0.000 1.000
#&gt; SRR1274533     1  0.0938      0.992 0.988 0.012
#&gt; SRR1274534     1  0.0672      0.994 0.992 0.008
#&gt; SRR1274535     1  0.0938      0.992 0.988 0.012
#&gt; SRR1274536     1  0.0938      0.992 0.988 0.012
#&gt; SRR1274537     2  0.7745      0.793 0.228 0.772
#&gt; SRR1274538     2  0.6438      0.864 0.164 0.836
#&gt; SRR1274539     1  0.0672      0.994 0.992 0.008
#&gt; SRR1274540     2  0.0000      0.910 0.000 1.000
#&gt; SRR1274541     2  0.0000      0.910 0.000 1.000
#&gt; SRR1274542     2  0.0000      0.910 0.000 1.000
#&gt; SRR1274543     2  0.9323      0.576 0.348 0.652
#&gt; SRR1274544     2  0.0000      0.910 0.000 1.000
#&gt; SRR1274545     2  0.5629      0.891 0.132 0.868
#&gt; SRR1274546     2  0.0000      0.910 0.000 1.000
#&gt; SRR1274547     2  0.4690      0.898 0.100 0.900
#&gt; SRR1274548     2  0.6973      0.841 0.188 0.812
#&gt; SRR1274549     1  0.0376      0.996 0.996 0.004
#&gt; SRR1274550     1  0.0376      0.996 0.996 0.004
#&gt; SRR1274551     2  0.0000      0.910 0.000 1.000
#&gt; SRR1274552     1  0.0376      0.996 0.996 0.004
#&gt; SRR1274553     1  0.0376      0.996 0.996 0.004
#&gt; SRR1274554     1  0.0672      0.994 0.992 0.008
#&gt; SRR1274555     1  0.0376      0.996 0.996 0.004
#&gt; SRR1274556     1  0.0376      0.996 0.996 0.004
#&gt; SRR1274557     1  0.0376      0.996 0.996 0.004
#&gt; SRR1274558     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274559     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274560     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274561     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274562     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274563     1  0.0376      0.996 0.996 0.004
#&gt; SRR1274564     1  0.0938      0.992 0.988 0.012
#&gt; SRR1274565     1  0.1184      0.988 0.984 0.016
#&gt; SRR1274566     1  0.0938      0.992 0.988 0.012
#&gt; SRR1274567     1  0.0672      0.994 0.992 0.008
#&gt; SRR1274568     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274569     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274570     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274571     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274572     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274573     2  0.0000      0.910 0.000 1.000
#&gt; SRR1274574     2  0.0672      0.910 0.008 0.992
#&gt; SRR1274575     2  0.5629      0.891 0.132 0.868
#&gt; SRR1274576     2  0.5946      0.883 0.144 0.856
#&gt; SRR1274577     1  0.0376      0.996 0.996 0.004
#&gt; SRR1274578     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274579     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274580     1  0.0000      0.995 1.000 0.000
#&gt; SRR1274581     1  0.0000      0.995 1.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.1411     0.8498 0.000 0.964 0.036
#&gt; SRR1274529     3  0.5467     0.4535 0.032 0.176 0.792
#&gt; SRR1274530     3  0.5521     0.4521 0.032 0.180 0.788
#&gt; SRR1274531     3  0.7346     0.3174 0.368 0.040 0.592
#&gt; SRR1274532     2  0.0000     0.8563 0.000 1.000 0.000
#&gt; SRR1274533     3  0.7291     0.3261 0.356 0.040 0.604
#&gt; SRR1274534     3  0.6228     0.2626 0.372 0.004 0.624
#&gt; SRR1274535     3  0.7190     0.3216 0.356 0.036 0.608
#&gt; SRR1274536     3  0.3530     0.5019 0.068 0.032 0.900
#&gt; SRR1274537     2  0.5956     0.6396 0.004 0.672 0.324
#&gt; SRR1274538     2  0.5760     0.6351 0.000 0.672 0.328
#&gt; SRR1274539     3  0.6379     0.2726 0.368 0.008 0.624
#&gt; SRR1274540     2  0.0000     0.8563 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000     0.8563 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000     0.8563 0.000 1.000 0.000
#&gt; SRR1274543     2  0.6600     0.4898 0.012 0.604 0.384
#&gt; SRR1274544     2  0.0000     0.8563 0.000 1.000 0.000
#&gt; SRR1274545     3  0.6099     0.3856 0.032 0.228 0.740
#&gt; SRR1274546     2  0.0237     0.8561 0.000 0.996 0.004
#&gt; SRR1274547     2  0.5803     0.6956 0.016 0.736 0.248
#&gt; SRR1274548     2  0.4887     0.7570 0.000 0.772 0.228
#&gt; SRR1274549     1  0.7072     0.0839 0.504 0.020 0.476
#&gt; SRR1274550     3  0.7186    -0.0919 0.476 0.024 0.500
#&gt; SRR1274551     2  0.0000     0.8563 0.000 1.000 0.000
#&gt; SRR1274552     3  0.6442     0.0521 0.432 0.004 0.564
#&gt; SRR1274553     3  0.6520    -0.1501 0.488 0.004 0.508
#&gt; SRR1274554     3  0.7291     0.3261 0.356 0.040 0.604
#&gt; SRR1274555     1  0.6308     0.1441 0.508 0.000 0.492
#&gt; SRR1274556     1  0.7069     0.0970 0.508 0.020 0.472
#&gt; SRR1274557     3  0.7074    -0.1101 0.480 0.020 0.500
#&gt; SRR1274558     1  0.6235     0.2965 0.564 0.000 0.436
#&gt; SRR1274559     1  0.5882     0.4267 0.652 0.000 0.348
#&gt; SRR1274560     1  0.5397     0.4764 0.720 0.000 0.280
#&gt; SRR1274561     1  0.6235     0.3310 0.564 0.000 0.436
#&gt; SRR1274562     1  0.6235     0.3310 0.564 0.000 0.436
#&gt; SRR1274563     1  0.6235     0.3310 0.564 0.000 0.436
#&gt; SRR1274564     3  0.3649     0.5035 0.068 0.036 0.896
#&gt; SRR1274565     3  0.3967     0.5042 0.072 0.044 0.884
#&gt; SRR1274566     3  0.3856     0.5046 0.072 0.040 0.888
#&gt; SRR1274567     3  0.4418     0.4742 0.132 0.020 0.848
#&gt; SRR1274568     1  0.5882     0.4344 0.652 0.000 0.348
#&gt; SRR1274569     1  0.0237     0.5399 0.996 0.000 0.004
#&gt; SRR1274570     1  0.0000     0.5379 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000     0.5379 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0424     0.5417 0.992 0.000 0.008
#&gt; SRR1274573     2  0.0000     0.8563 0.000 1.000 0.000
#&gt; SRR1274574     2  0.2796     0.8345 0.000 0.908 0.092
#&gt; SRR1274575     3  0.5521     0.4521 0.032 0.180 0.788
#&gt; SRR1274576     2  0.5291     0.7115 0.000 0.732 0.268
#&gt; SRR1274577     3  0.6280     0.0265 0.460 0.000 0.540
#&gt; SRR1274578     1  0.0424     0.5417 0.992 0.000 0.008
#&gt; SRR1274579     1  0.0424     0.5417 0.992 0.000 0.008
#&gt; SRR1274580     1  0.0424     0.5417 0.992 0.000 0.008
#&gt; SRR1274581     1  0.6244     0.2499 0.560 0.000 0.440
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.2256      0.744 0.000 0.924 0.056 0.020
#&gt; SRR1274529     4  0.6289      0.949 0.000 0.236 0.116 0.648
#&gt; SRR1274530     4  0.6267      0.953 0.000 0.240 0.112 0.648
#&gt; SRR1274531     3  0.4625      0.653 0.008 0.092 0.812 0.088
#&gt; SRR1274532     2  0.0000      0.758 0.000 1.000 0.000 0.000
#&gt; SRR1274533     3  0.2565      0.657 0.000 0.032 0.912 0.056
#&gt; SRR1274534     3  0.2313      0.667 0.000 0.032 0.924 0.044
#&gt; SRR1274535     3  0.2443      0.658 0.000 0.024 0.916 0.060
#&gt; SRR1274536     3  0.6705      0.494 0.012 0.080 0.592 0.316
#&gt; SRR1274537     2  0.6041      0.490 0.000 0.608 0.332 0.060
#&gt; SRR1274538     2  0.5759      0.546 0.000 0.668 0.268 0.064
#&gt; SRR1274539     3  0.2111      0.667 0.000 0.024 0.932 0.044
#&gt; SRR1274540     2  0.0000      0.758 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0469      0.757 0.000 0.988 0.012 0.000
#&gt; SRR1274542     2  0.0188      0.759 0.000 0.996 0.004 0.000
#&gt; SRR1274543     2  0.5973      0.480 0.000 0.612 0.332 0.056
#&gt; SRR1274544     2  0.0188      0.759 0.000 0.996 0.004 0.000
#&gt; SRR1274545     4  0.6801      0.856 0.000 0.308 0.124 0.568
#&gt; SRR1274546     2  0.0817      0.759 0.000 0.976 0.024 0.000
#&gt; SRR1274547     2  0.5440      0.522 0.000 0.736 0.104 0.160
#&gt; SRR1274548     2  0.5905      0.527 0.000 0.636 0.304 0.060
#&gt; SRR1274549     3  0.8105      0.650 0.172 0.064 0.564 0.200
#&gt; SRR1274550     3  0.5172      0.715 0.160 0.020 0.772 0.048
#&gt; SRR1274551     2  0.0000      0.758 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.2686      0.708 0.032 0.012 0.916 0.040
#&gt; SRR1274553     3  0.4033      0.716 0.116 0.004 0.836 0.044
#&gt; SRR1274554     3  0.2546      0.657 0.000 0.028 0.912 0.060
#&gt; SRR1274555     3  0.6511      0.693 0.172 0.000 0.640 0.188
#&gt; SRR1274556     3  0.6750      0.692 0.168 0.004 0.628 0.200
#&gt; SRR1274557     3  0.6827      0.707 0.160 0.048 0.680 0.112
#&gt; SRR1274558     3  0.5794      0.653 0.104 0.012 0.732 0.152
#&gt; SRR1274559     3  0.6910      0.578 0.252 0.000 0.584 0.164
#&gt; SRR1274560     3  0.7049      0.532 0.300 0.000 0.548 0.152
#&gt; SRR1274561     3  0.6860      0.657 0.244 0.000 0.592 0.164
#&gt; SRR1274562     3  0.7128      0.636 0.260 0.000 0.556 0.184
#&gt; SRR1274563     3  0.6110      0.700 0.176 0.000 0.680 0.144
#&gt; SRR1274564     3  0.6607      0.480 0.008 0.084 0.600 0.308
#&gt; SRR1274565     3  0.6636      0.483 0.008 0.108 0.628 0.256
#&gt; SRR1274566     3  0.6732      0.466 0.008 0.096 0.596 0.300
#&gt; SRR1274567     3  0.6300      0.625 0.032 0.044 0.660 0.264
#&gt; SRR1274568     3  0.5904      0.651 0.112 0.012 0.724 0.152
#&gt; SRR1274569     1  0.2830      0.918 0.900 0.000 0.040 0.060
#&gt; SRR1274570     1  0.1557      0.954 0.944 0.000 0.000 0.056
#&gt; SRR1274571     1  0.1557      0.954 0.944 0.000 0.000 0.056
#&gt; SRR1274572     1  0.0000      0.968 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0188      0.758 0.000 0.996 0.000 0.004
#&gt; SRR1274574     2  0.3216      0.694 0.000 0.880 0.044 0.076
#&gt; SRR1274575     4  0.6267      0.953 0.000 0.240 0.112 0.648
#&gt; SRR1274576     2  0.5883      0.494 0.000 0.640 0.300 0.060
#&gt; SRR1274577     3  0.2982      0.699 0.068 0.004 0.896 0.032
#&gt; SRR1274578     1  0.0000      0.968 1.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.968 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.968 1.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.7210      0.634 0.276 0.000 0.540 0.184
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.4509    0.62625 0.000 0.728 0.224 0.044 0.004
#&gt; SRR1274529     4  0.2230    0.79283 0.000 0.116 0.000 0.884 0.000
#&gt; SRR1274530     4  0.2230    0.79283 0.000 0.116 0.000 0.884 0.000
#&gt; SRR1274531     5  0.7254   -0.02223 0.000 0.024 0.328 0.248 0.400
#&gt; SRR1274532     2  0.0000    0.71273 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     3  0.6532   -0.04979 0.000 0.020 0.520 0.132 0.328
#&gt; SRR1274534     3  0.6440   -0.05171 0.000 0.024 0.532 0.112 0.332
#&gt; SRR1274535     3  0.6287   -0.05019 0.000 0.012 0.536 0.124 0.328
#&gt; SRR1274536     4  0.5451    0.55471 0.000 0.024 0.104 0.700 0.172
#&gt; SRR1274537     2  0.6692    0.46196 0.000 0.504 0.308 0.172 0.016
#&gt; SRR1274538     2  0.5860    0.39740 0.000 0.556 0.068 0.360 0.016
#&gt; SRR1274539     3  0.6440   -0.05171 0.000 0.024 0.532 0.112 0.332
#&gt; SRR1274540     2  0.0162    0.71160 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1274541     2  0.0162    0.71160 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1274542     2  0.0000    0.71273 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.6112    0.46701 0.000 0.532 0.364 0.088 0.016
#&gt; SRR1274544     2  0.0000    0.71273 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     4  0.3864    0.70617 0.000 0.188 0.020 0.784 0.008
#&gt; SRR1274546     2  0.2278    0.69971 0.000 0.908 0.060 0.032 0.000
#&gt; SRR1274547     2  0.5235    0.24719 0.000 0.524 0.024 0.440 0.012
#&gt; SRR1274548     2  0.6544    0.48787 0.000 0.548 0.180 0.256 0.016
#&gt; SRR1274549     3  0.6893    0.08910 0.028 0.000 0.468 0.152 0.352
#&gt; SRR1274550     3  0.2481    0.07611 0.032 0.012 0.916 0.016 0.024
#&gt; SRR1274551     2  0.0000    0.71273 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.2927    0.00456 0.000 0.000 0.868 0.092 0.040
#&gt; SRR1274553     3  0.2026    0.06116 0.012 0.000 0.924 0.056 0.008
#&gt; SRR1274554     3  0.6708   -0.07489 0.000 0.012 0.480 0.180 0.328
#&gt; SRR1274555     3  0.5705    0.16750 0.036 0.000 0.488 0.024 0.452
#&gt; SRR1274556     3  0.5977    0.15243 0.036 0.000 0.464 0.040 0.460
#&gt; SRR1274557     3  0.6793    0.12585 0.032 0.012 0.524 0.096 0.336
#&gt; SRR1274558     5  0.5716    0.10822 0.036 0.012 0.464 0.008 0.480
#&gt; SRR1274559     5  0.6638    0.04019 0.256 0.000 0.252 0.004 0.488
#&gt; SRR1274560     1  0.6771   -0.10844 0.368 0.000 0.272 0.000 0.360
#&gt; SRR1274561     3  0.6666    0.11789 0.224 0.000 0.472 0.004 0.300
#&gt; SRR1274562     3  0.6931    0.12126 0.236 0.000 0.448 0.012 0.304
#&gt; SRR1274563     3  0.5690    0.16904 0.036 0.000 0.508 0.024 0.432
#&gt; SRR1274564     4  0.4067    0.72364 0.000 0.024 0.060 0.816 0.100
#&gt; SRR1274565     4  0.3587    0.74956 0.000 0.036 0.096 0.844 0.024
#&gt; SRR1274566     4  0.3736    0.74260 0.000 0.024 0.064 0.840 0.072
#&gt; SRR1274567     5  0.6904   -0.03736 0.000 0.012 0.204 0.380 0.404
#&gt; SRR1274568     5  0.5716    0.10822 0.036 0.012 0.464 0.008 0.480
#&gt; SRR1274569     1  0.1965    0.85086 0.904 0.000 0.000 0.000 0.096
#&gt; SRR1274570     1  0.1792    0.85803 0.916 0.000 0.000 0.000 0.084
#&gt; SRR1274571     1  0.1792    0.85803 0.916 0.000 0.000 0.000 0.084
#&gt; SRR1274572     1  0.0324    0.86805 0.992 0.000 0.004 0.000 0.004
#&gt; SRR1274573     2  0.0000    0.71273 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.4814    0.33506 0.000 0.568 0.016 0.412 0.004
#&gt; SRR1274575     4  0.2230    0.79283 0.000 0.116 0.000 0.884 0.000
#&gt; SRR1274576     2  0.7915    0.16513 0.000 0.364 0.360 0.104 0.172
#&gt; SRR1274577     3  0.6175   -0.07857 0.008 0.004 0.568 0.116 0.304
#&gt; SRR1274578     1  0.0290    0.86737 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1274579     1  0.0324    0.86805 0.992 0.000 0.004 0.000 0.004
#&gt; SRR1274580     1  0.0324    0.86805 0.992 0.000 0.004 0.000 0.004
#&gt; SRR1274581     3  0.7176    0.10746 0.252 0.000 0.412 0.020 0.316
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     6  0.5434     0.2319 0.000 0.456 0.000 0.060 0.024 0.460
#&gt; SRR1274529     4  0.1387     0.6733 0.000 0.068 0.000 0.932 0.000 0.000
#&gt; SRR1274530     4  0.1387     0.6733 0.000 0.068 0.000 0.932 0.000 0.000
#&gt; SRR1274531     3  0.4520     0.6381 0.000 0.020 0.676 0.024 0.276 0.004
#&gt; SRR1274532     2  0.0000     0.7450 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.0692     0.9789 0.000 0.020 0.000 0.000 0.976 0.004
#&gt; SRR1274534     5  0.0653     0.9746 0.000 0.004 0.004 0.012 0.980 0.000
#&gt; SRR1274535     5  0.0458     0.9798 0.000 0.016 0.000 0.000 0.984 0.000
#&gt; SRR1274536     3  0.5141     0.4788 0.000 0.004 0.608 0.304 0.076 0.008
#&gt; SRR1274537     6  0.6106     0.3637 0.000 0.392 0.000 0.096 0.048 0.464
#&gt; SRR1274538     6  0.6079     0.3443 0.000 0.392 0.000 0.112 0.036 0.460
#&gt; SRR1274539     5  0.0653     0.9746 0.000 0.004 0.004 0.012 0.980 0.000
#&gt; SRR1274540     2  0.0000     0.7450 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.7450 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.7450 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     6  0.6517     0.3752 0.000 0.360 0.004 0.092 0.080 0.464
#&gt; SRR1274544     2  0.0000     0.7450 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     4  0.3640     0.4928 0.000 0.204 0.000 0.764 0.004 0.028
#&gt; SRR1274546     2  0.4076    -0.1778 0.000 0.540 0.000 0.000 0.008 0.452
#&gt; SRR1274547     2  0.6408    -0.0655 0.000 0.400 0.000 0.372 0.024 0.204
#&gt; SRR1274548     6  0.6178     0.3685 0.000 0.392 0.000 0.088 0.060 0.460
#&gt; SRR1274549     3  0.1340     0.7631 0.000 0.000 0.948 0.040 0.004 0.008
#&gt; SRR1274550     3  0.2177     0.7591 0.000 0.008 0.908 0.000 0.052 0.032
#&gt; SRR1274551     2  0.0000     0.7450 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.3602     0.7304 0.000 0.000 0.784 0.056 0.160 0.000
#&gt; SRR1274553     3  0.2560     0.7623 0.000 0.000 0.872 0.036 0.092 0.000
#&gt; SRR1274554     5  0.0692     0.9789 0.000 0.020 0.000 0.000 0.976 0.004
#&gt; SRR1274555     3  0.1297     0.7586 0.000 0.000 0.948 0.012 0.000 0.040
#&gt; SRR1274556     3  0.1708     0.7610 0.000 0.000 0.932 0.040 0.004 0.024
#&gt; SRR1274557     3  0.1679     0.7588 0.000 0.012 0.936 0.000 0.016 0.036
#&gt; SRR1274558     6  0.6011    -0.3629 0.000 0.000 0.336 0.000 0.248 0.416
#&gt; SRR1274559     3  0.4951     0.5168 0.012 0.000 0.516 0.020 0.012 0.440
#&gt; SRR1274560     3  0.5028     0.5174 0.016 0.000 0.516 0.020 0.012 0.436
#&gt; SRR1274561     3  0.3717     0.7483 0.076 0.000 0.832 0.032 0.020 0.040
#&gt; SRR1274562     3  0.3287     0.7500 0.076 0.000 0.852 0.016 0.012 0.044
#&gt; SRR1274563     3  0.1297     0.7600 0.000 0.000 0.948 0.000 0.012 0.040
#&gt; SRR1274564     4  0.5199     0.3811 0.000 0.004 0.320 0.592 0.076 0.008
#&gt; SRR1274565     4  0.5310     0.5238 0.000 0.024 0.240 0.644 0.088 0.004
#&gt; SRR1274566     4  0.5075     0.4600 0.000 0.004 0.288 0.624 0.076 0.008
#&gt; SRR1274567     3  0.4873     0.5644 0.000 0.004 0.660 0.256 0.072 0.008
#&gt; SRR1274568     6  0.6044    -0.3250 0.000 0.000 0.308 0.000 0.276 0.416
#&gt; SRR1274569     1  0.2631     0.9003 0.840 0.000 0.008 0.000 0.000 0.152
#&gt; SRR1274570     1  0.1957     0.9229 0.888 0.000 0.000 0.000 0.000 0.112
#&gt; SRR1274571     1  0.1957     0.9229 0.888 0.000 0.000 0.000 0.000 0.112
#&gt; SRR1274572     1  0.0000     0.9344 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0547     0.7280 0.000 0.980 0.000 0.020 0.000 0.000
#&gt; SRR1274574     2  0.5927    -0.0220 0.000 0.448 0.000 0.324 0.000 0.228
#&gt; SRR1274575     4  0.1387     0.6733 0.000 0.068 0.000 0.932 0.000 0.000
#&gt; SRR1274576     6  0.6530     0.3586 0.000 0.336 0.000 0.072 0.124 0.468
#&gt; SRR1274577     3  0.7278     0.2599 0.000 0.012 0.384 0.084 0.340 0.180
#&gt; SRR1274578     1  0.1204     0.9289 0.944 0.000 0.000 0.000 0.000 0.056
#&gt; SRR1274579     1  0.0000     0.9344 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000     0.9344 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.4706     0.7121 0.080 0.000 0.744 0.064 0.000 0.112
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.999           0.962       0.984         0.4849 0.516   0.516
#> 3 3 0.893           0.901       0.960         0.2981 0.790   0.619
#> 4 4 0.737           0.682       0.816         0.1612 0.771   0.472
#> 5 5 0.707           0.701       0.811         0.0531 0.934   0.766
#> 6 6 0.835           0.776       0.892         0.0475 0.908   0.633
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274529     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274530     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274531     2  0.1843      0.962 0.028 0.972
#&gt; SRR1274532     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274533     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274534     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274535     2  0.0376      0.981 0.004 0.996
#&gt; SRR1274536     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274537     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274538     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274539     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274540     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274541     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274542     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274543     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274544     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274545     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274546     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274547     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274548     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274549     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274550     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274551     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274552     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274553     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274554     2  0.1184      0.971 0.016 0.984
#&gt; SRR1274555     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274556     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274557     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274558     2  0.4298      0.902 0.088 0.912
#&gt; SRR1274559     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274560     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274561     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274562     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274563     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274564     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274565     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274566     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274567     1  0.9427      0.411 0.640 0.360
#&gt; SRR1274568     2  0.8207      0.663 0.256 0.744
#&gt; SRR1274569     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274570     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274571     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274572     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274573     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274574     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274575     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274576     2  0.0000      0.984 0.000 1.000
#&gt; SRR1274577     2  0.5408      0.861 0.124 0.876
#&gt; SRR1274578     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274579     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274580     1  0.0000      0.981 1.000 0.000
#&gt; SRR1274581     1  0.0000      0.981 1.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0237      0.950 0.000 0.996 0.004
#&gt; SRR1274530     2  0.0237      0.950 0.000 0.996 0.004
#&gt; SRR1274531     3  0.0000      0.936 0.000 0.000 1.000
#&gt; SRR1274532     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274533     3  0.6252      0.176 0.000 0.444 0.556
#&gt; SRR1274534     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274535     3  0.0237      0.935 0.000 0.004 0.996
#&gt; SRR1274536     3  0.0000      0.936 0.000 0.000 1.000
#&gt; SRR1274537     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274539     2  0.0892      0.936 0.000 0.980 0.020
#&gt; SRR1274540     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0237      0.950 0.000 0.996 0.004
#&gt; SRR1274546     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0237      0.950 0.000 0.996 0.004
#&gt; SRR1274548     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274549     3  0.0000      0.936 0.000 0.000 1.000
#&gt; SRR1274550     3  0.0237      0.937 0.004 0.000 0.996
#&gt; SRR1274551     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274552     3  0.0237      0.937 0.004 0.000 0.996
#&gt; SRR1274553     3  0.0237      0.937 0.004 0.000 0.996
#&gt; SRR1274554     3  0.4062      0.760 0.000 0.164 0.836
#&gt; SRR1274555     3  0.0237      0.937 0.004 0.000 0.996
#&gt; SRR1274556     3  0.0237      0.937 0.004 0.000 0.996
#&gt; SRR1274557     3  0.0237      0.937 0.004 0.000 0.996
#&gt; SRR1274558     2  0.6180      0.333 0.416 0.584 0.000
#&gt; SRR1274559     1  0.0000      0.984 1.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.984 1.000 0.000 0.000
#&gt; SRR1274561     1  0.3879      0.819 0.848 0.000 0.152
#&gt; SRR1274562     1  0.0424      0.977 0.992 0.000 0.008
#&gt; SRR1274563     3  0.0237      0.937 0.004 0.000 0.996
#&gt; SRR1274564     2  0.5098      0.660 0.000 0.752 0.248
#&gt; SRR1274565     2  0.0237      0.950 0.000 0.996 0.004
#&gt; SRR1274566     2  0.4002      0.789 0.000 0.840 0.160
#&gt; SRR1274567     3  0.0000      0.936 0.000 0.000 1.000
#&gt; SRR1274568     2  0.6154      0.353 0.408 0.592 0.000
#&gt; SRR1274569     1  0.0000      0.984 1.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.984 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.984 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.984 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0237      0.950 0.000 0.996 0.004
#&gt; SRR1274576     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274577     2  0.0000      0.951 0.000 1.000 0.000
#&gt; SRR1274578     1  0.0000      0.984 1.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.984 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.984 1.000 0.000 0.000
#&gt; SRR1274581     3  0.2066      0.891 0.060 0.000 0.940
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.4761     0.7575 0.000 0.628 0.000 0.372
#&gt; SRR1274529     4  0.0000     0.6953 0.000 0.000 0.000 1.000
#&gt; SRR1274530     4  0.0000     0.6953 0.000 0.000 0.000 1.000
#&gt; SRR1274531     3  0.1356     0.8521 0.000 0.032 0.960 0.008
#&gt; SRR1274532     2  0.4804     0.7544 0.000 0.616 0.000 0.384
#&gt; SRR1274533     2  0.3161     0.4810 0.000 0.864 0.124 0.012
#&gt; SRR1274534     2  0.1302     0.5984 0.000 0.956 0.000 0.044
#&gt; SRR1274535     2  0.3751     0.3495 0.000 0.800 0.196 0.004
#&gt; SRR1274536     4  0.4790     0.3938 0.000 0.000 0.380 0.620
#&gt; SRR1274537     2  0.4713     0.7568 0.000 0.640 0.000 0.360
#&gt; SRR1274538     2  0.4898     0.7277 0.000 0.584 0.000 0.416
#&gt; SRR1274539     2  0.1452     0.5931 0.000 0.956 0.008 0.036
#&gt; SRR1274540     2  0.4916     0.7181 0.000 0.576 0.000 0.424
#&gt; SRR1274541     2  0.4804     0.7544 0.000 0.616 0.000 0.384
#&gt; SRR1274542     2  0.4804     0.7544 0.000 0.616 0.000 0.384
#&gt; SRR1274543     2  0.4761     0.7575 0.000 0.628 0.000 0.372
#&gt; SRR1274544     2  0.4830     0.7492 0.000 0.608 0.000 0.392
#&gt; SRR1274545     4  0.0188     0.6919 0.000 0.004 0.000 0.996
#&gt; SRR1274546     2  0.4776     0.7567 0.000 0.624 0.000 0.376
#&gt; SRR1274547     4  0.1474     0.6302 0.000 0.052 0.000 0.948
#&gt; SRR1274548     2  0.4713     0.7569 0.000 0.640 0.000 0.360
#&gt; SRR1274549     3  0.0188     0.8548 0.000 0.000 0.996 0.004
#&gt; SRR1274550     3  0.4406     0.7306 0.000 0.300 0.700 0.000
#&gt; SRR1274551     2  0.4933     0.7076 0.000 0.568 0.000 0.432
#&gt; SRR1274552     3  0.4624     0.7039 0.000 0.340 0.660 0.000
#&gt; SRR1274553     3  0.4585     0.7107 0.000 0.332 0.668 0.000
#&gt; SRR1274554     2  0.4283     0.2383 0.000 0.740 0.256 0.004
#&gt; SRR1274555     3  0.0188     0.8591 0.000 0.004 0.996 0.000
#&gt; SRR1274556     3  0.0000     0.8572 0.000 0.000 1.000 0.000
#&gt; SRR1274557     3  0.0188     0.8591 0.000 0.004 0.996 0.000
#&gt; SRR1274558     1  0.6155     0.0163 0.536 0.412 0.000 0.052
#&gt; SRR1274559     1  0.0000     0.9046 1.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000     0.9046 1.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.3649     0.7049 0.796 0.000 0.204 0.000
#&gt; SRR1274562     1  0.2216     0.8431 0.908 0.000 0.092 0.000
#&gt; SRR1274563     3  0.0188     0.8591 0.000 0.004 0.996 0.000
#&gt; SRR1274564     4  0.4477     0.5071 0.000 0.000 0.312 0.688
#&gt; SRR1274565     4  0.0376     0.6945 0.000 0.004 0.004 0.992
#&gt; SRR1274566     4  0.4331     0.5369 0.000 0.000 0.288 0.712
#&gt; SRR1274567     4  0.4790     0.3938 0.000 0.000 0.380 0.620
#&gt; SRR1274568     2  0.5666     0.3938 0.348 0.616 0.000 0.036
#&gt; SRR1274569     1  0.0000     0.9046 1.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000     0.9046 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000     0.9046 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0707     0.9027 0.980 0.020 0.000 0.000
#&gt; SRR1274573     2  0.4877     0.7359 0.000 0.592 0.000 0.408
#&gt; SRR1274574     4  0.4977    -0.5597 0.000 0.460 0.000 0.540
#&gt; SRR1274575     4  0.0000     0.6953 0.000 0.000 0.000 1.000
#&gt; SRR1274576     2  0.4431     0.7360 0.000 0.696 0.000 0.304
#&gt; SRR1274577     2  0.0336     0.5767 0.000 0.992 0.000 0.008
#&gt; SRR1274578     1  0.1302     0.8976 0.956 0.044 0.000 0.000
#&gt; SRR1274579     1  0.1302     0.8976 0.956 0.044 0.000 0.000
#&gt; SRR1274580     1  0.1302     0.8976 0.956 0.044 0.000 0.000
#&gt; SRR1274581     3  0.3110     0.8049 0.056 0.048 0.892 0.004
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0290     0.8417 0.000 0.992 0.000 0.000 0.008
#&gt; SRR1274529     4  0.2605     0.8383 0.000 0.148 0.000 0.852 0.000
#&gt; SRR1274530     4  0.2605     0.8383 0.000 0.148 0.000 0.852 0.000
#&gt; SRR1274531     3  0.1341     0.8151 0.000 0.000 0.944 0.000 0.056
#&gt; SRR1274532     2  0.0609     0.8472 0.000 0.980 0.000 0.020 0.000
#&gt; SRR1274533     5  0.5459     0.5226 0.000 0.316 0.084 0.000 0.600
#&gt; SRR1274534     2  0.4291     0.0312 0.000 0.536 0.000 0.000 0.464
#&gt; SRR1274535     5  0.5791     0.6028 0.000 0.260 0.140 0.000 0.600
#&gt; SRR1274536     4  0.2773     0.7432 0.000 0.000 0.164 0.836 0.000
#&gt; SRR1274537     2  0.0703     0.8330 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1274538     2  0.0794     0.8451 0.000 0.972 0.000 0.028 0.000
#&gt; SRR1274539     2  0.4268     0.1026 0.000 0.556 0.000 0.000 0.444
#&gt; SRR1274540     2  0.0794     0.8451 0.000 0.972 0.000 0.028 0.000
#&gt; SRR1274541     2  0.0609     0.8472 0.000 0.980 0.000 0.020 0.000
#&gt; SRR1274542     2  0.0609     0.8472 0.000 0.980 0.000 0.020 0.000
#&gt; SRR1274543     2  0.0162     0.8455 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1274544     2  0.0609     0.8472 0.000 0.980 0.000 0.020 0.000
#&gt; SRR1274545     4  0.2929     0.8224 0.000 0.180 0.000 0.820 0.000
#&gt; SRR1274546     2  0.0000     0.8445 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     4  0.4030     0.6217 0.000 0.352 0.000 0.648 0.000
#&gt; SRR1274548     2  0.0404     0.8400 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1274549     3  0.1907     0.8100 0.000 0.000 0.928 0.044 0.028
#&gt; SRR1274550     5  0.4249     0.5707 0.000 0.000 0.432 0.000 0.568
#&gt; SRR1274551     2  0.0794     0.8451 0.000 0.972 0.000 0.028 0.000
#&gt; SRR1274552     5  0.4436     0.6235 0.000 0.008 0.396 0.000 0.596
#&gt; SRR1274553     5  0.4192     0.6172 0.000 0.000 0.404 0.000 0.596
#&gt; SRR1274554     2  0.6163     0.1446 0.000 0.536 0.300 0.000 0.164
#&gt; SRR1274555     3  0.0000     0.8616 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     3  0.0290     0.8578 0.000 0.000 0.992 0.000 0.008
#&gt; SRR1274557     3  0.0000     0.8616 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274558     1  0.4225     0.2970 0.632 0.364 0.000 0.004 0.000
#&gt; SRR1274559     1  0.0162     0.7851 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1274560     1  0.0162     0.7851 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1274561     1  0.2286     0.7213 0.888 0.000 0.108 0.004 0.000
#&gt; SRR1274562     1  0.4828     0.4754 0.648 0.000 0.320 0.012 0.020
#&gt; SRR1274563     3  0.0000     0.8616 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274564     4  0.3115     0.7966 0.000 0.036 0.112 0.852 0.000
#&gt; SRR1274565     4  0.6062     0.6014 0.000 0.308 0.108 0.572 0.012
#&gt; SRR1274566     4  0.3371     0.7995 0.000 0.040 0.104 0.848 0.008
#&gt; SRR1274567     4  0.3093     0.7384 0.000 0.000 0.168 0.824 0.008
#&gt; SRR1274568     2  0.4479     0.5533 0.264 0.700 0.000 0.000 0.036
#&gt; SRR1274569     1  0.0162     0.7851 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1274570     1  0.0000     0.7853 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000     0.7853 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.4049     0.7400 0.792 0.000 0.000 0.084 0.124
#&gt; SRR1274573     2  0.0794     0.8451 0.000 0.972 0.000 0.028 0.000
#&gt; SRR1274574     2  0.2127     0.7654 0.000 0.892 0.000 0.108 0.000
#&gt; SRR1274575     4  0.2605     0.8383 0.000 0.148 0.000 0.852 0.000
#&gt; SRR1274576     2  0.1043     0.8215 0.000 0.960 0.000 0.000 0.040
#&gt; SRR1274577     2  0.5739     0.3602 0.000 0.556 0.000 0.100 0.344
#&gt; SRR1274578     1  0.5820     0.6377 0.572 0.000 0.000 0.120 0.308
#&gt; SRR1274579     1  0.5788     0.6434 0.580 0.000 0.000 0.120 0.300
#&gt; SRR1274580     1  0.5772     0.6459 0.584 0.000 0.000 0.120 0.296
#&gt; SRR1274581     3  0.6376     0.3458 0.040 0.000 0.496 0.068 0.396
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000     0.9796 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.0632     0.8582 0.000 0.024 0.000 0.976 0.000 0.000
#&gt; SRR1274530     4  0.0632     0.8582 0.000 0.024 0.000 0.976 0.000 0.000
#&gt; SRR1274531     3  0.0935     0.7527 0.000 0.000 0.964 0.000 0.032 0.004
#&gt; SRR1274532     2  0.0000     0.9796 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.2250     0.8629 0.000 0.040 0.064 0.000 0.896 0.000
#&gt; SRR1274534     5  0.2912     0.7199 0.000 0.216 0.000 0.000 0.784 0.000
#&gt; SRR1274535     5  0.2147     0.8686 0.000 0.020 0.084 0.000 0.896 0.000
#&gt; SRR1274536     4  0.0508     0.8500 0.000 0.000 0.012 0.984 0.000 0.004
#&gt; SRR1274537     2  0.0146     0.9777 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1274538     2  0.0146     0.9768 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274539     5  0.3189     0.6951 0.000 0.236 0.004 0.000 0.760 0.000
#&gt; SRR1274540     2  0.0000     0.9796 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9796 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9796 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0146     0.9777 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1274544     2  0.0000     0.9796 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     4  0.1327     0.8347 0.000 0.064 0.000 0.936 0.000 0.000
#&gt; SRR1274546     2  0.0000     0.9796 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     4  0.3409     0.5676 0.000 0.300 0.000 0.700 0.000 0.000
#&gt; SRR1274548     2  0.0146     0.9777 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1274549     3  0.1888     0.7198 0.000 0.000 0.916 0.068 0.012 0.004
#&gt; SRR1274550     5  0.2100     0.8574 0.000 0.000 0.112 0.004 0.884 0.000
#&gt; SRR1274551     2  0.0000     0.9796 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.2006     0.8629 0.000 0.000 0.104 0.004 0.892 0.000
#&gt; SRR1274553     5  0.2006     0.8629 0.000 0.000 0.104 0.004 0.892 0.000
#&gt; SRR1274554     3  0.5543     0.0701 0.000 0.452 0.464 0.004 0.048 0.032
#&gt; SRR1274555     3  0.0363     0.7599 0.000 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1274556     3  0.0291     0.7587 0.000 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1274557     3  0.0260     0.7598 0.000 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1274558     1  0.2996     0.5367 0.772 0.228 0.000 0.000 0.000 0.000
#&gt; SRR1274559     1  0.0000     0.8346 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000     0.8346 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.1556     0.7696 0.920 0.000 0.080 0.000 0.000 0.000
#&gt; SRR1274562     3  0.4591     0.0755 0.452 0.000 0.516 0.000 0.004 0.028
#&gt; SRR1274563     3  0.0363     0.7596 0.000 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1274564     4  0.0551     0.8516 0.000 0.004 0.008 0.984 0.000 0.004
#&gt; SRR1274565     4  0.7122     0.1300 0.000 0.284 0.264 0.396 0.028 0.028
#&gt; SRR1274566     4  0.1508     0.8453 0.000 0.004 0.016 0.948 0.020 0.012
#&gt; SRR1274567     4  0.2063     0.8209 0.000 0.000 0.060 0.912 0.020 0.008
#&gt; SRR1274568     2  0.3865     0.6728 0.208 0.756 0.004 0.000 0.016 0.016
#&gt; SRR1274569     1  0.0363     0.8355 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1274570     1  0.0363     0.8355 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1274571     1  0.0363     0.8355 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1274572     1  0.3860    -0.1716 0.528 0.000 0.000 0.000 0.000 0.472
#&gt; SRR1274573     2  0.0000     0.9796 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0260     0.9730 0.000 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1274575     4  0.0632     0.8582 0.000 0.024 0.000 0.976 0.000 0.000
#&gt; SRR1274576     2  0.0260     0.9746 0.000 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1274577     6  0.4113     0.6118 0.000 0.188 0.004 0.004 0.056 0.748
#&gt; SRR1274578     6  0.2527     0.8430 0.168 0.000 0.000 0.000 0.000 0.832
#&gt; SRR1274579     6  0.2631     0.8436 0.180 0.000 0.000 0.000 0.000 0.820
#&gt; SRR1274580     6  0.2730     0.8342 0.192 0.000 0.000 0.000 0.000 0.808
#&gt; SRR1274581     3  0.7174     0.2307 0.068 0.000 0.428 0.020 0.164 0.320
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.398           0.743       0.859         0.2917 0.669   0.669
#> 3 3 0.656           0.773       0.910         0.5074 0.915   0.874
#> 4 4 0.595           0.654       0.851         0.1852 0.876   0.796
#> 5 5 0.604           0.667       0.874         0.0894 0.904   0.811
#> 6 6 0.685           0.668       0.845         0.0525 0.933   0.860
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274529     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274530     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274531     2  0.2603     0.8556 0.044 0.956
#&gt; SRR1274532     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274533     2  0.6048     0.7243 0.148 0.852
#&gt; SRR1274534     2  0.1414     0.8758 0.020 0.980
#&gt; SRR1274535     2  0.1414     0.8758 0.020 0.980
#&gt; SRR1274536     2  0.3114     0.8445 0.056 0.944
#&gt; SRR1274537     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274538     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274539     2  0.1414     0.8758 0.020 0.980
#&gt; SRR1274540     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274541     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274542     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274543     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274544     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274545     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274546     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274547     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274548     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274549     2  0.3114     0.8445 0.056 0.944
#&gt; SRR1274550     2  0.7674     0.5905 0.224 0.776
#&gt; SRR1274551     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274552     2  0.7674     0.5905 0.224 0.776
#&gt; SRR1274553     2  0.7674     0.5905 0.224 0.776
#&gt; SRR1274554     2  0.1414     0.8758 0.020 0.980
#&gt; SRR1274555     1  0.9358     0.5707 0.648 0.352
#&gt; SRR1274556     2  0.9732    -0.0533 0.404 0.596
#&gt; SRR1274557     1  0.9358     0.5707 0.648 0.352
#&gt; SRR1274558     2  0.6623     0.6335 0.172 0.828
#&gt; SRR1274559     2  0.7883     0.4752 0.236 0.764
#&gt; SRR1274560     2  0.7883     0.4752 0.236 0.764
#&gt; SRR1274561     1  0.8909     0.6528 0.692 0.308
#&gt; SRR1274562     1  0.9170     0.6314 0.668 0.332
#&gt; SRR1274563     1  0.9358     0.5707 0.648 0.352
#&gt; SRR1274564     2  0.3114     0.8445 0.056 0.944
#&gt; SRR1274565     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274566     2  0.0376     0.8837 0.004 0.996
#&gt; SRR1274567     2  0.0376     0.8837 0.004 0.996
#&gt; SRR1274568     2  0.5059     0.7533 0.112 0.888
#&gt; SRR1274569     1  0.9754     0.6734 0.592 0.408
#&gt; SRR1274570     1  0.9661     0.6936 0.608 0.392
#&gt; SRR1274571     1  0.9661     0.6936 0.608 0.392
#&gt; SRR1274572     1  0.9661     0.6936 0.608 0.392
#&gt; SRR1274573     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274574     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274575     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274576     2  0.0000     0.8854 0.000 1.000
#&gt; SRR1274577     2  0.2043     0.8704 0.032 0.968
#&gt; SRR1274578     2  0.9963    -0.4455 0.464 0.536
#&gt; SRR1274579     1  0.9661     0.6936 0.608 0.392
#&gt; SRR1274580     1  0.9661     0.6936 0.608 0.392
#&gt; SRR1274581     2  0.8016     0.5094 0.244 0.756
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274530     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274531     2  0.1860     0.8921 0.000 0.948 0.052
#&gt; SRR1274532     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274533     2  0.4326     0.7912 0.012 0.844 0.144
#&gt; SRR1274534     2  0.0892     0.9105 0.000 0.980 0.020
#&gt; SRR1274535     2  0.0892     0.9105 0.000 0.980 0.020
#&gt; SRR1274536     2  0.1964     0.8880 0.000 0.944 0.056
#&gt; SRR1274537     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274539     2  0.0892     0.9105 0.000 0.980 0.020
#&gt; SRR1274540     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274546     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274549     2  0.1964     0.8880 0.000 0.944 0.056
#&gt; SRR1274550     2  0.6852     0.5173 0.036 0.664 0.300
#&gt; SRR1274551     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274552     2  0.6852     0.5173 0.036 0.664 0.300
#&gt; SRR1274553     2  0.6852     0.5173 0.036 0.664 0.300
#&gt; SRR1274554     2  0.0892     0.9105 0.000 0.980 0.020
#&gt; SRR1274555     3  0.1529     0.6139 0.040 0.000 0.960
#&gt; SRR1274556     3  0.7174    -0.0731 0.024 0.460 0.516
#&gt; SRR1274557     3  0.1529     0.6139 0.040 0.000 0.960
#&gt; SRR1274558     2  0.4796     0.6925 0.220 0.780 0.000
#&gt; SRR1274559     2  0.5678     0.5502 0.316 0.684 0.000
#&gt; SRR1274560     2  0.5678     0.5502 0.316 0.684 0.000
#&gt; SRR1274561     1  0.7671     0.0297 0.492 0.044 0.464
#&gt; SRR1274562     3  0.6204    -0.0153 0.424 0.000 0.576
#&gt; SRR1274563     3  0.1860     0.6090 0.052 0.000 0.948
#&gt; SRR1274564     2  0.1964     0.8880 0.000 0.944 0.056
#&gt; SRR1274565     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274566     2  0.0237     0.9166 0.000 0.996 0.004
#&gt; SRR1274567     2  0.0237     0.9166 0.000 0.996 0.004
#&gt; SRR1274568     2  0.4110     0.7807 0.152 0.844 0.004
#&gt; SRR1274569     1  0.3267     0.7160 0.884 0.116 0.000
#&gt; SRR1274570     1  0.0592     0.8332 0.988 0.012 0.000
#&gt; SRR1274571     1  0.0592     0.8332 0.988 0.012 0.000
#&gt; SRR1274572     1  0.0592     0.8332 0.988 0.012 0.000
#&gt; SRR1274573     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274576     2  0.0000     0.9178 0.000 1.000 0.000
#&gt; SRR1274577     2  0.1482     0.9069 0.012 0.968 0.020
#&gt; SRR1274578     1  0.4399     0.5708 0.812 0.188 0.000
#&gt; SRR1274579     1  0.0592     0.8332 0.988 0.012 0.000
#&gt; SRR1274580     1  0.0592     0.8332 0.988 0.012 0.000
#&gt; SRR1274581     2  0.8380     0.3737 0.276 0.600 0.124
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274530     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274531     2  0.4761    0.46281 0.000 0.664 0.332 0.004
#&gt; SRR1274532     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274533     2  0.4972   -0.01659 0.000 0.544 0.456 0.000
#&gt; SRR1274534     2  0.0817    0.87398 0.000 0.976 0.024 0.000
#&gt; SRR1274535     2  0.0921    0.87228 0.000 0.972 0.028 0.000
#&gt; SRR1274536     2  0.4730    0.40237 0.000 0.636 0.364 0.000
#&gt; SRR1274537     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274539     2  0.0817    0.87398 0.000 0.976 0.024 0.000
#&gt; SRR1274540     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274546     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274549     2  0.4730    0.40237 0.000 0.636 0.364 0.000
#&gt; SRR1274550     3  0.4730    0.46209 0.000 0.364 0.636 0.000
#&gt; SRR1274551     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.4730    0.46209 0.000 0.364 0.636 0.000
#&gt; SRR1274553     3  0.4730    0.46209 0.000 0.364 0.636 0.000
#&gt; SRR1274554     2  0.1211    0.86566 0.000 0.960 0.040 0.000
#&gt; SRR1274555     3  0.4955   -0.18963 0.000 0.000 0.556 0.444
#&gt; SRR1274556     3  0.3471    0.21313 0.000 0.072 0.868 0.060
#&gt; SRR1274557     3  0.4955   -0.18963 0.000 0.000 0.556 0.444
#&gt; SRR1274558     2  0.3873    0.63200 0.228 0.772 0.000 0.000
#&gt; SRR1274559     2  0.4543    0.46842 0.324 0.676 0.000 0.000
#&gt; SRR1274560     2  0.4543    0.46842 0.324 0.676 0.000 0.000
#&gt; SRR1274561     4  0.6854   -0.00644 0.460 0.044 0.028 0.468
#&gt; SRR1274562     4  0.7207    0.18921 0.376 0.000 0.144 0.480
#&gt; SRR1274563     4  0.5168   -0.14940 0.004 0.000 0.492 0.504
#&gt; SRR1274564     2  0.4730    0.40237 0.000 0.636 0.364 0.000
#&gt; SRR1274565     2  0.0817    0.87351 0.000 0.976 0.024 0.000
#&gt; SRR1274566     2  0.1867    0.83409 0.000 0.928 0.072 0.000
#&gt; SRR1274567     2  0.1867    0.83409 0.000 0.928 0.072 0.000
#&gt; SRR1274568     2  0.3355    0.72443 0.160 0.836 0.004 0.000
#&gt; SRR1274569     1  0.2408    0.72580 0.896 0.104 0.000 0.000
#&gt; SRR1274570     1  0.0000    0.88288 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000    0.88288 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000    0.88288 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274576     2  0.0000    0.88476 0.000 1.000 0.000 0.000
#&gt; SRR1274577     2  0.1284    0.87009 0.012 0.964 0.024 0.000
#&gt; SRR1274578     1  0.3486    0.51832 0.812 0.188 0.000 0.000
#&gt; SRR1274579     1  0.0000    0.88288 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000    0.88288 1.000 0.000 0.000 0.000
#&gt; SRR1274581     4  0.7953   -0.15882 0.148 0.412 0.024 0.416
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274530     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274531     2   0.497     -0.184 0.000 0.540 0.008 0.436 0.016
#&gt; SRR1274532     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     4   0.389      0.389 0.000 0.320 0.000 0.680 0.000
#&gt; SRR1274534     2   0.120      0.866 0.000 0.952 0.000 0.048 0.000
#&gt; SRR1274535     2   0.141      0.858 0.000 0.940 0.000 0.060 0.000
#&gt; SRR1274536     4   0.475      0.232 0.000 0.492 0.000 0.492 0.016
#&gt; SRR1274537     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     2   0.120      0.866 0.000 0.952 0.000 0.048 0.000
#&gt; SRR1274540     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274546     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274548     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     2   0.475     -0.361 0.000 0.492 0.000 0.492 0.016
#&gt; SRR1274550     4   0.444      0.466 0.000 0.136 0.104 0.760 0.000
#&gt; SRR1274551     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     4   0.444      0.466 0.000 0.136 0.104 0.760 0.000
#&gt; SRR1274553     4   0.444      0.466 0.000 0.136 0.104 0.760 0.000
#&gt; SRR1274554     2   0.161      0.850 0.000 0.928 0.000 0.072 0.000
#&gt; SRR1274555     3   0.000      0.785 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     4   0.488     -0.197 0.000 0.008 0.392 0.584 0.016
#&gt; SRR1274557     3   0.000      0.785 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274558     2   0.334      0.608 0.228 0.772 0.000 0.000 0.000
#&gt; SRR1274559     2   0.391      0.398 0.324 0.676 0.000 0.000 0.000
#&gt; SRR1274560     2   0.391      0.398 0.324 0.676 0.000 0.000 0.000
#&gt; SRR1274561     1   0.828     -0.239 0.368 0.044 0.308 0.036 0.244
#&gt; SRR1274562     3   0.740      0.287 0.280 0.000 0.436 0.040 0.244
#&gt; SRR1274563     3   0.172      0.775 0.004 0.000 0.936 0.008 0.052
#&gt; SRR1274564     4   0.475      0.232 0.000 0.492 0.000 0.492 0.016
#&gt; SRR1274565     2   0.112      0.864 0.000 0.956 0.000 0.044 0.000
#&gt; SRR1274566     2   0.191      0.810 0.000 0.908 0.000 0.092 0.000
#&gt; SRR1274567     2   0.191      0.810 0.000 0.908 0.000 0.092 0.000
#&gt; SRR1274568     2   0.301      0.714 0.160 0.832 0.000 0.008 0.000
#&gt; SRR1274569     1   0.207      0.699 0.896 0.104 0.000 0.000 0.000
#&gt; SRR1274570     1   0.000      0.821 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1   0.000      0.821 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1   0.000      0.821 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274576     2   0.000      0.894 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274577     2   0.181      0.858 0.012 0.936 0.000 0.044 0.008
#&gt; SRR1274578     1   0.321      0.518 0.812 0.180 0.000 0.000 0.008
#&gt; SRR1274579     1   0.000      0.821 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1   0.000      0.821 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     5   0.356      0.000 0.000 0.260 0.000 0.000 0.740
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274530     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274531     2  0.7117    -0.0388 0.000 0.456 0.100 0.112 0.312 0.020
#&gt; SRR1274532     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.3221     0.4972 0.000 0.264 0.000 0.000 0.736 0.000
#&gt; SRR1274534     2  0.1075     0.8168 0.000 0.952 0.000 0.000 0.048 0.000
#&gt; SRR1274535     2  0.1327     0.8086 0.000 0.936 0.000 0.000 0.064 0.000
#&gt; SRR1274536     2  0.7568    -0.2266 0.000 0.380 0.108 0.176 0.316 0.020
#&gt; SRR1274537     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     2  0.1075     0.8168 0.000 0.952 0.000 0.000 0.048 0.000
#&gt; SRR1274540     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274546     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274549     2  0.7568    -0.2266 0.000 0.380 0.108 0.176 0.316 0.020
#&gt; SRR1274550     5  0.1556     0.8380 0.000 0.080 0.000 0.000 0.920 0.000
#&gt; SRR1274551     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.1556     0.8380 0.000 0.080 0.000 0.000 0.920 0.000
#&gt; SRR1274553     5  0.1556     0.8380 0.000 0.080 0.000 0.000 0.920 0.000
#&gt; SRR1274554     2  0.1531     0.8061 0.000 0.928 0.004 0.000 0.068 0.000
#&gt; SRR1274555     3  0.3620     0.6654 0.000 0.000 0.648 0.352 0.000 0.000
#&gt; SRR1274556     3  0.3761     0.2128 0.000 0.008 0.744 0.000 0.228 0.020
#&gt; SRR1274557     3  0.3620     0.6654 0.000 0.000 0.648 0.352 0.000 0.000
#&gt; SRR1274558     2  0.4586     0.5262 0.104 0.712 0.000 0.000 0.008 0.176
#&gt; SRR1274559     2  0.5384     0.3263 0.200 0.616 0.000 0.000 0.008 0.176
#&gt; SRR1274560     2  0.5384     0.3263 0.200 0.616 0.000 0.000 0.008 0.176
#&gt; SRR1274561     4  0.4173     0.7218 0.268 0.044 0.000 0.688 0.000 0.000
#&gt; SRR1274562     4  0.2597     0.6809 0.176 0.000 0.000 0.824 0.000 0.000
#&gt; SRR1274563     3  0.3789     0.6051 0.000 0.000 0.584 0.416 0.000 0.000
#&gt; SRR1274564     2  0.7568    -0.2266 0.000 0.380 0.108 0.176 0.316 0.020
#&gt; SRR1274565     2  0.1511     0.8103 0.000 0.944 0.012 0.012 0.032 0.000
#&gt; SRR1274566     2  0.3159     0.7237 0.000 0.856 0.056 0.056 0.032 0.000
#&gt; SRR1274567     2  0.3159     0.7237 0.000 0.856 0.056 0.056 0.032 0.000
#&gt; SRR1274568     2  0.4044     0.6233 0.064 0.772 0.000 0.000 0.016 0.148
#&gt; SRR1274569     1  0.3566     0.6435 0.800 0.104 0.000 0.000 0.000 0.096
#&gt; SRR1274570     1  0.1714     0.7819 0.908 0.000 0.000 0.000 0.000 0.092
#&gt; SRR1274571     1  0.0000     0.8339 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000     0.8339 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274576     2  0.0000     0.8424 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274577     2  0.1549     0.8090 0.000 0.936 0.000 0.000 0.044 0.020
#&gt; SRR1274578     1  0.3156     0.5316 0.800 0.180 0.000 0.000 0.000 0.020
#&gt; SRR1274579     1  0.0363     0.8310 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1274580     1  0.0363     0.8310 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR1274581     6  0.2883     0.0000 0.000 0.212 0.000 0.000 0.000 0.788
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.549           0.882       0.927         0.4335 0.535   0.535
#> 3 3 0.658           0.828       0.905         0.3443 0.855   0.737
#> 4 4 0.619           0.640       0.821         0.1648 0.886   0.743
#> 5 5 0.663           0.572       0.775         0.0763 0.893   0.707
#> 6 6 0.707           0.508       0.767         0.0567 0.920   0.732
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.961 0.000 1.000
#&gt; SRR1274529     2   0.000      0.961 0.000 1.000
#&gt; SRR1274530     2   0.000      0.961 0.000 1.000
#&gt; SRR1274531     2   0.680      0.766 0.180 0.820
#&gt; SRR1274532     2   0.000      0.961 0.000 1.000
#&gt; SRR1274533     2   0.295      0.914 0.052 0.948
#&gt; SRR1274534     2   0.000      0.961 0.000 1.000
#&gt; SRR1274535     2   0.000      0.961 0.000 1.000
#&gt; SRR1274536     2   0.552      0.826 0.128 0.872
#&gt; SRR1274537     2   0.000      0.961 0.000 1.000
#&gt; SRR1274538     2   0.000      0.961 0.000 1.000
#&gt; SRR1274539     2   0.000      0.961 0.000 1.000
#&gt; SRR1274540     2   0.000      0.961 0.000 1.000
#&gt; SRR1274541     2   0.000      0.961 0.000 1.000
#&gt; SRR1274542     2   0.000      0.961 0.000 1.000
#&gt; SRR1274543     2   0.000      0.961 0.000 1.000
#&gt; SRR1274544     2   0.000      0.961 0.000 1.000
#&gt; SRR1274545     2   0.000      0.961 0.000 1.000
#&gt; SRR1274546     2   0.000      0.961 0.000 1.000
#&gt; SRR1274547     2   0.000      0.961 0.000 1.000
#&gt; SRR1274548     2   0.000      0.961 0.000 1.000
#&gt; SRR1274549     1   0.706      0.776 0.808 0.192
#&gt; SRR1274550     1   0.795      0.761 0.760 0.240
#&gt; SRR1274551     2   0.000      0.961 0.000 1.000
#&gt; SRR1274552     1   0.802      0.759 0.756 0.244
#&gt; SRR1274553     1   0.802      0.759 0.756 0.244
#&gt; SRR1274554     2   0.000      0.961 0.000 1.000
#&gt; SRR1274555     1   0.000      0.826 1.000 0.000
#&gt; SRR1274556     1   0.541      0.819 0.876 0.124
#&gt; SRR1274557     1   0.430      0.829 0.912 0.088
#&gt; SRR1274558     2   0.260      0.915 0.044 0.956
#&gt; SRR1274559     1   0.706      0.864 0.808 0.192
#&gt; SRR1274560     1   0.706      0.864 0.808 0.192
#&gt; SRR1274561     1   0.000      0.826 1.000 0.000
#&gt; SRR1274562     1   0.000      0.826 1.000 0.000
#&gt; SRR1274563     1   0.000      0.826 1.000 0.000
#&gt; SRR1274564     2   0.311      0.910 0.056 0.944
#&gt; SRR1274565     2   0.000      0.961 0.000 1.000
#&gt; SRR1274566     2   0.000      0.961 0.000 1.000
#&gt; SRR1274567     2   0.584      0.815 0.140 0.860
#&gt; SRR1274568     2   0.204      0.931 0.032 0.968
#&gt; SRR1274569     1   0.706      0.864 0.808 0.192
#&gt; SRR1274570     1   0.706      0.864 0.808 0.192
#&gt; SRR1274571     1   0.706      0.864 0.808 0.192
#&gt; SRR1274572     1   0.706      0.864 0.808 0.192
#&gt; SRR1274573     2   0.000      0.961 0.000 1.000
#&gt; SRR1274574     2   0.000      0.961 0.000 1.000
#&gt; SRR1274575     2   0.000      0.961 0.000 1.000
#&gt; SRR1274576     2   0.000      0.961 0.000 1.000
#&gt; SRR1274577     2   0.000      0.961 0.000 1.000
#&gt; SRR1274578     1   0.706      0.864 0.808 0.192
#&gt; SRR1274579     1   0.706      0.864 0.808 0.192
#&gt; SRR1274580     1   0.706      0.864 0.808 0.192
#&gt; SRR1274581     2   0.990     -0.163 0.440 0.560
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274529     2  0.3528      0.864 0.016 0.892 0.092
#&gt; SRR1274530     2  0.3528      0.864 0.016 0.892 0.092
#&gt; SRR1274531     3  0.2165      0.796 0.000 0.064 0.936
#&gt; SRR1274532     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274533     2  0.6062      0.364 0.000 0.616 0.384
#&gt; SRR1274534     2  0.3038      0.859 0.000 0.896 0.104
#&gt; SRR1274535     2  0.3752      0.820 0.000 0.856 0.144
#&gt; SRR1274536     3  0.6096      0.570 0.016 0.280 0.704
#&gt; SRR1274537     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274539     2  0.3038      0.859 0.000 0.896 0.104
#&gt; SRR1274540     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0747      0.912 0.016 0.984 0.000
#&gt; SRR1274546     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0747      0.912 0.016 0.984 0.000
#&gt; SRR1274548     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274549     3  0.0000      0.797 0.000 0.000 1.000
#&gt; SRR1274550     3  0.4902      0.825 0.092 0.064 0.844
#&gt; SRR1274551     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274552     3  0.5085      0.822 0.092 0.072 0.836
#&gt; SRR1274553     3  0.4995      0.824 0.092 0.068 0.840
#&gt; SRR1274554     2  0.3267      0.848 0.000 0.884 0.116
#&gt; SRR1274555     3  0.3482      0.801 0.128 0.000 0.872
#&gt; SRR1274556     3  0.2878      0.810 0.096 0.000 0.904
#&gt; SRR1274557     3  0.3482      0.801 0.128 0.000 0.872
#&gt; SRR1274558     2  0.3192      0.834 0.112 0.888 0.000
#&gt; SRR1274559     1  0.2261      0.893 0.932 0.068 0.000
#&gt; SRR1274560     1  0.1860      0.912 0.948 0.052 0.000
#&gt; SRR1274561     1  0.5905      0.427 0.648 0.000 0.352
#&gt; SRR1274562     1  0.5905      0.427 0.648 0.000 0.352
#&gt; SRR1274563     3  0.3482      0.801 0.128 0.000 0.872
#&gt; SRR1274564     2  0.6608      0.488 0.016 0.628 0.356
#&gt; SRR1274565     2  0.2269      0.896 0.016 0.944 0.040
#&gt; SRR1274566     2  0.3769      0.858 0.016 0.880 0.104
#&gt; SRR1274567     3  0.6096      0.572 0.016 0.280 0.704
#&gt; SRR1274568     2  0.2066      0.880 0.060 0.940 0.000
#&gt; SRR1274569     1  0.1860      0.912 0.948 0.052 0.000
#&gt; SRR1274570     1  0.1860      0.912 0.948 0.052 0.000
#&gt; SRR1274571     1  0.1860      0.912 0.948 0.052 0.000
#&gt; SRR1274572     1  0.1860      0.912 0.948 0.052 0.000
#&gt; SRR1274573     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274575     2  0.3528      0.864 0.016 0.892 0.092
#&gt; SRR1274576     2  0.0000      0.918 0.000 1.000 0.000
#&gt; SRR1274577     2  0.1753      0.896 0.000 0.952 0.048
#&gt; SRR1274578     1  0.1860      0.912 0.948 0.052 0.000
#&gt; SRR1274579     1  0.1860      0.912 0.948 0.052 0.000
#&gt; SRR1274580     1  0.1860      0.912 0.948 0.052 0.000
#&gt; SRR1274581     2  0.7931      0.480 0.284 0.624 0.092
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.3710     0.6935 0.004 0.804 0.000 0.192
#&gt; SRR1274530     2  0.3710     0.6935 0.004 0.804 0.000 0.192
#&gt; SRR1274531     4  0.5243     0.3104 0.004 0.004 0.416 0.576
#&gt; SRR1274532     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274533     4  0.6730     0.4733 0.008 0.280 0.104 0.608
#&gt; SRR1274534     2  0.5368     0.4274 0.000 0.636 0.024 0.340
#&gt; SRR1274535     4  0.5933     0.2199 0.000 0.408 0.040 0.552
#&gt; SRR1274536     4  0.5935     0.4208 0.004 0.064 0.268 0.664
#&gt; SRR1274537     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274539     2  0.5403     0.4111 0.000 0.628 0.024 0.348
#&gt; SRR1274540     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.3105     0.7343 0.004 0.856 0.000 0.140
#&gt; SRR1274546     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0376     0.8176 0.004 0.992 0.000 0.004
#&gt; SRR1274548     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274549     3  0.4898    -0.0120 0.000 0.000 0.584 0.416
#&gt; SRR1274550     4  0.5515     0.3891 0.008 0.008 0.420 0.564
#&gt; SRR1274551     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274552     4  0.5702     0.4148 0.012 0.012 0.400 0.576
#&gt; SRR1274553     4  0.5702     0.4148 0.012 0.012 0.400 0.576
#&gt; SRR1274554     2  0.5663     0.1645 0.000 0.536 0.024 0.440
#&gt; SRR1274555     3  0.0188     0.6703 0.000 0.000 0.996 0.004
#&gt; SRR1274556     3  0.3219     0.4994 0.000 0.000 0.836 0.164
#&gt; SRR1274557     3  0.0188     0.6703 0.000 0.000 0.996 0.004
#&gt; SRR1274558     2  0.4395     0.6197 0.204 0.776 0.004 0.016
#&gt; SRR1274559     1  0.2075     0.8954 0.936 0.016 0.004 0.044
#&gt; SRR1274560     1  0.1247     0.9223 0.968 0.012 0.004 0.016
#&gt; SRR1274561     3  0.4679     0.4438 0.352 0.000 0.648 0.000
#&gt; SRR1274562     3  0.5291     0.4551 0.324 0.000 0.652 0.024
#&gt; SRR1274563     3  0.0000     0.6700 0.000 0.000 1.000 0.000
#&gt; SRR1274564     4  0.5873     0.4025 0.004 0.292 0.052 0.652
#&gt; SRR1274565     2  0.4761     0.5607 0.004 0.664 0.000 0.332
#&gt; SRR1274566     2  0.5119     0.3643 0.004 0.556 0.000 0.440
#&gt; SRR1274567     4  0.5722     0.3889 0.004 0.044 0.292 0.660
#&gt; SRR1274568     2  0.6429     0.4878 0.160 0.648 0.000 0.192
#&gt; SRR1274569     1  0.0469     0.9311 0.988 0.012 0.000 0.000
#&gt; SRR1274570     1  0.0469     0.9311 0.988 0.012 0.000 0.000
#&gt; SRR1274571     1  0.0469     0.9311 0.988 0.012 0.000 0.000
#&gt; SRR1274572     1  0.1767     0.9254 0.944 0.012 0.000 0.044
#&gt; SRR1274573     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.3710     0.6935 0.004 0.804 0.000 0.192
#&gt; SRR1274576     2  0.0000     0.8218 0.000 1.000 0.000 0.000
#&gt; SRR1274577     2  0.5110     0.4268 0.000 0.636 0.012 0.352
#&gt; SRR1274578     1  0.3529     0.8915 0.836 0.012 0.000 0.152
#&gt; SRR1274579     1  0.3428     0.8962 0.844 0.012 0.000 0.144
#&gt; SRR1274580     1  0.3428     0.8962 0.844 0.012 0.000 0.144
#&gt; SRR1274581     2  0.8334     0.0798 0.152 0.424 0.044 0.380
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.4243     0.5172 0.000 0.712 0.000 0.264 0.024
#&gt; SRR1274530     2  0.4243     0.5172 0.000 0.712 0.000 0.264 0.024
#&gt; SRR1274531     4  0.5269     0.1136 0.004 0.000 0.120 0.688 0.188
#&gt; SRR1274532     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.6473     0.4803 0.004 0.116 0.012 0.376 0.492
#&gt; SRR1274534     2  0.6554    -0.0961 0.000 0.484 0.004 0.192 0.320
#&gt; SRR1274535     5  0.6740     0.3317 0.000 0.212 0.004 0.380 0.404
#&gt; SRR1274536     4  0.2172     0.4430 0.000 0.020 0.060 0.916 0.004
#&gt; SRR1274537     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     2  0.6576    -0.1079 0.000 0.480 0.004 0.196 0.320
#&gt; SRR1274540     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.2505     0.7251 0.000 0.888 0.000 0.092 0.020
#&gt; SRR1274546     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0566     0.8075 0.000 0.984 0.000 0.004 0.012
#&gt; SRR1274548     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     4  0.4268     0.1870 0.000 0.000 0.344 0.648 0.008
#&gt; SRR1274550     5  0.6439     0.5384 0.000 0.000 0.192 0.332 0.476
#&gt; SRR1274551     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.6282     0.5561 0.000 0.000 0.164 0.340 0.496
#&gt; SRR1274553     5  0.6282     0.5561 0.000 0.000 0.164 0.340 0.496
#&gt; SRR1274554     4  0.6939    -0.2471 0.000 0.328 0.004 0.368 0.300
#&gt; SRR1274555     3  0.0798     0.8013 0.000 0.000 0.976 0.016 0.008
#&gt; SRR1274556     3  0.3810     0.6206 0.000 0.000 0.788 0.176 0.036
#&gt; SRR1274557     3  0.0798     0.8013 0.000 0.000 0.976 0.016 0.008
#&gt; SRR1274558     2  0.5881     0.4113 0.248 0.652 0.008 0.048 0.044
#&gt; SRR1274559     1  0.3631     0.7377 0.852 0.008 0.016 0.072 0.052
#&gt; SRR1274560     1  0.3108     0.7613 0.880 0.004 0.016 0.048 0.052
#&gt; SRR1274561     3  0.4818     0.6329 0.260 0.000 0.688 0.004 0.048
#&gt; SRR1274562     3  0.4477     0.6529 0.252 0.000 0.708 0.000 0.040
#&gt; SRR1274563     3  0.1082     0.8000 0.000 0.000 0.964 0.008 0.028
#&gt; SRR1274564     4  0.2408     0.4615 0.000 0.092 0.016 0.892 0.000
#&gt; SRR1274565     4  0.5238    -0.0111 0.000 0.472 0.000 0.484 0.044
#&gt; SRR1274566     4  0.4354     0.3746 0.000 0.256 0.000 0.712 0.032
#&gt; SRR1274567     4  0.3164     0.4561 0.000 0.020 0.084 0.868 0.028
#&gt; SRR1274568     2  0.7836     0.0907 0.224 0.484 0.004 0.172 0.116
#&gt; SRR1274569     1  0.0740     0.8102 0.980 0.004 0.000 0.008 0.008
#&gt; SRR1274570     1  0.0162     0.8135 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0162     0.8135 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1274572     1  0.2674     0.7908 0.856 0.004 0.000 0.000 0.140
#&gt; SRR1274573     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.8169 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.4243     0.5172 0.000 0.712 0.000 0.264 0.024
#&gt; SRR1274576     2  0.0798     0.8024 0.000 0.976 0.000 0.008 0.016
#&gt; SRR1274577     2  0.6690    -0.1939 0.000 0.432 0.000 0.268 0.300
#&gt; SRR1274578     1  0.4318     0.7322 0.644 0.004 0.000 0.004 0.348
#&gt; SRR1274579     1  0.4302     0.7348 0.648 0.004 0.000 0.004 0.344
#&gt; SRR1274580     1  0.4302     0.7348 0.648 0.004 0.000 0.004 0.344
#&gt; SRR1274581     5  0.7323    -0.0410 0.076 0.392 0.004 0.100 0.428
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.5500    0.01256 0.000 0.564 0.004 0.332 0.016 0.084
#&gt; SRR1274530     2  0.5500    0.01256 0.000 0.564 0.004 0.332 0.016 0.084
#&gt; SRR1274531     5  0.5116   -0.19038 0.000 0.000 0.020 0.464 0.476 0.040
#&gt; SRR1274532     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.2497    0.53748 0.000 0.032 0.000 0.032 0.896 0.040
#&gt; SRR1274534     5  0.6229   -0.00698 0.000 0.376 0.008 0.032 0.472 0.112
#&gt; SRR1274535     5  0.4831    0.48694 0.000 0.100 0.008 0.040 0.740 0.112
#&gt; SRR1274536     4  0.2726    0.69268 0.000 0.008 0.008 0.848 0.136 0.000
#&gt; SRR1274537     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.6229   -0.00698 0.000 0.376 0.008 0.032 0.472 0.112
#&gt; SRR1274540     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.3063    0.60421 0.000 0.860 0.004 0.040 0.016 0.080
#&gt; SRR1274546     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.1442    0.72205 0.000 0.944 0.004 0.000 0.012 0.040
#&gt; SRR1274548     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274549     4  0.5411    0.39921 0.000 0.000 0.256 0.588 0.152 0.004
#&gt; SRR1274550     5  0.1781    0.52761 0.000 0.000 0.060 0.008 0.924 0.008
#&gt; SRR1274551     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.1909    0.52260 0.000 0.000 0.052 0.004 0.920 0.024
#&gt; SRR1274553     5  0.1909    0.52260 0.000 0.000 0.052 0.004 0.920 0.024
#&gt; SRR1274554     5  0.7425    0.27378 0.000 0.172 0.012 0.168 0.456 0.192
#&gt; SRR1274555     3  0.0547    0.76738 0.000 0.000 0.980 0.000 0.020 0.000
#&gt; SRR1274556     3  0.3554    0.63246 0.000 0.000 0.808 0.108 0.080 0.004
#&gt; SRR1274557     3  0.0692    0.76652 0.000 0.000 0.976 0.004 0.020 0.000
#&gt; SRR1274558     2  0.6313   -0.26810 0.312 0.464 0.000 0.024 0.000 0.200
#&gt; SRR1274559     1  0.3790    0.56932 0.752 0.000 0.004 0.024 0.004 0.216
#&gt; SRR1274560     1  0.3534    0.58342 0.772 0.000 0.004 0.024 0.000 0.200
#&gt; SRR1274561     3  0.6172    0.46263 0.316 0.000 0.520 0.056 0.000 0.108
#&gt; SRR1274562     3  0.5646    0.58355 0.248 0.000 0.612 0.048 0.000 0.092
#&gt; SRR1274563     3  0.2772    0.76073 0.000 0.000 0.876 0.036 0.020 0.068
#&gt; SRR1274564     4  0.2664    0.69532 0.000 0.016 0.000 0.848 0.136 0.000
#&gt; SRR1274565     4  0.6752   -0.16016 0.000 0.296 0.008 0.472 0.052 0.172
#&gt; SRR1274566     4  0.4580    0.62196 0.000 0.072 0.008 0.768 0.064 0.088
#&gt; SRR1274567     4  0.3532    0.68987 0.000 0.004 0.016 0.828 0.092 0.060
#&gt; SRR1274568     2  0.8410   -0.42763 0.248 0.320 0.004 0.096 0.080 0.252
#&gt; SRR1274569     1  0.1524    0.67033 0.932 0.000 0.000 0.008 0.000 0.060
#&gt; SRR1274570     1  0.0146    0.68855 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0508    0.68702 0.984 0.000 0.004 0.012 0.000 0.000
#&gt; SRR1274572     1  0.3426    0.64897 0.764 0.000 0.004 0.012 0.000 0.220
#&gt; SRR1274573     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000    0.77725 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.5500    0.01256 0.000 0.564 0.004 0.332 0.016 0.084
#&gt; SRR1274576     2  0.1633    0.68932 0.000 0.932 0.000 0.000 0.024 0.044
#&gt; SRR1274577     5  0.7546    0.06027 0.000 0.264 0.008 0.140 0.392 0.196
#&gt; SRR1274578     1  0.4097    0.54805 0.500 0.000 0.000 0.008 0.000 0.492
#&gt; SRR1274579     1  0.3864    0.56652 0.520 0.000 0.000 0.000 0.000 0.480
#&gt; SRR1274580     1  0.3864    0.56652 0.520 0.000 0.000 0.000 0.000 0.480
#&gt; SRR1274581     6  0.7451    0.00000 0.040 0.340 0.012 0.060 0.120 0.428
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.849           0.881       0.955         0.5034 0.497   0.497
#> 3 3 0.882           0.894       0.954         0.3124 0.734   0.515
#> 4 4 0.721           0.652       0.851         0.1098 0.881   0.670
#> 5 5 0.733           0.713       0.834         0.0584 0.890   0.625
#> 6 6 0.792           0.741       0.853         0.0376 0.969   0.852
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274529     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274530     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274531     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274532     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274533     2  0.0938     0.9423 0.012 0.988
#&gt; SRR1274534     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274535     2  0.5059     0.8412 0.112 0.888
#&gt; SRR1274536     2  0.8608     0.5822 0.284 0.716
#&gt; SRR1274537     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274538     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274539     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274540     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274541     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274542     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274543     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274544     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274545     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274546     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274547     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274548     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274549     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274550     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274551     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274552     1  0.4161     0.8691 0.916 0.084
#&gt; SRR1274553     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274554     2  0.9996    -0.0343 0.488 0.512
#&gt; SRR1274555     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274556     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274557     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274558     2  0.9580     0.3586 0.380 0.620
#&gt; SRR1274559     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274560     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274561     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274562     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274563     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274564     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274565     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274566     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274567     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274568     1  0.8608     0.5916 0.716 0.284
#&gt; SRR1274569     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274570     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274571     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274572     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274573     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274574     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274575     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274576     2  0.0000     0.9521 0.000 1.000
#&gt; SRR1274577     1  0.9635     0.3756 0.612 0.388
#&gt; SRR1274578     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274579     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274580     1  0.0000     0.9460 1.000 0.000
#&gt; SRR1274581     1  0.9710     0.3197 0.600 0.400
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274529     2  0.1163      0.954 0.000 0.972 0.028
#&gt; SRR1274530     2  0.1163      0.954 0.000 0.972 0.028
#&gt; SRR1274531     3  0.0000      0.938 0.000 0.000 1.000
#&gt; SRR1274532     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274533     3  0.1163      0.931 0.000 0.028 0.972
#&gt; SRR1274534     2  0.4974      0.685 0.000 0.764 0.236
#&gt; SRR1274535     3  0.3038      0.859 0.000 0.104 0.896
#&gt; SRR1274536     3  0.0000      0.938 0.000 0.000 1.000
#&gt; SRR1274537     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274539     2  0.5016      0.678 0.000 0.760 0.240
#&gt; SRR1274540     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274545     2  0.1163      0.954 0.000 0.972 0.028
#&gt; SRR1274546     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274549     3  0.0000      0.938 0.000 0.000 1.000
#&gt; SRR1274550     3  0.1163      0.940 0.028 0.000 0.972
#&gt; SRR1274551     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274552     3  0.1163      0.940 0.028 0.000 0.972
#&gt; SRR1274553     3  0.1163      0.940 0.028 0.000 0.972
#&gt; SRR1274554     3  0.1163      0.931 0.000 0.028 0.972
#&gt; SRR1274555     3  0.1163      0.940 0.028 0.000 0.972
#&gt; SRR1274556     3  0.1163      0.940 0.028 0.000 0.972
#&gt; SRR1274557     3  0.1163      0.940 0.028 0.000 0.972
#&gt; SRR1274558     1  0.4931      0.698 0.768 0.232 0.000
#&gt; SRR1274559     1  0.0000      0.911 1.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.911 1.000 0.000 0.000
#&gt; SRR1274561     1  0.4504      0.730 0.804 0.000 0.196
#&gt; SRR1274562     1  0.4504      0.730 0.804 0.000 0.196
#&gt; SRR1274563     3  0.1163      0.940 0.028 0.000 0.972
#&gt; SRR1274564     3  0.0592      0.932 0.000 0.012 0.988
#&gt; SRR1274565     2  0.1163      0.954 0.000 0.972 0.028
#&gt; SRR1274566     3  0.6225      0.219 0.000 0.432 0.568
#&gt; SRR1274567     3  0.0000      0.938 0.000 0.000 1.000
#&gt; SRR1274568     1  0.1163      0.896 0.972 0.028 0.000
#&gt; SRR1274569     1  0.0000      0.911 1.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.911 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.911 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.911 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274575     2  0.1163      0.954 0.000 0.972 0.028
#&gt; SRR1274576     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR1274577     1  0.1163      0.896 0.972 0.028 0.000
#&gt; SRR1274578     1  0.0000      0.911 1.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.911 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.911 1.000 0.000 0.000
#&gt; SRR1274581     1  0.6513      0.304 0.592 0.400 0.008
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.4643     0.5262 0.000 0.656 0.000 0.344
#&gt; SRR1274530     2  0.4643     0.5262 0.000 0.656 0.000 0.344
#&gt; SRR1274531     3  0.4998     0.0916 0.000 0.000 0.512 0.488
#&gt; SRR1274532     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274533     3  0.0188     0.6071 0.000 0.004 0.996 0.000
#&gt; SRR1274534     3  0.4343     0.4123 0.000 0.264 0.732 0.004
#&gt; SRR1274535     3  0.1635     0.5893 0.000 0.044 0.948 0.008
#&gt; SRR1274536     4  0.3219     0.6046 0.000 0.000 0.164 0.836
#&gt; SRR1274537     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274539     3  0.4343     0.4123 0.000 0.264 0.732 0.004
#&gt; SRR1274540     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.2814     0.8145 0.000 0.868 0.000 0.132
#&gt; SRR1274546     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274549     4  0.4843     0.1141 0.000 0.000 0.396 0.604
#&gt; SRR1274550     3  0.0000     0.6076 0.000 0.000 1.000 0.000
#&gt; SRR1274551     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.0000     0.6076 0.000 0.000 1.000 0.000
#&gt; SRR1274553     3  0.0000     0.6076 0.000 0.000 1.000 0.000
#&gt; SRR1274554     3  0.3975     0.4962 0.000 0.000 0.760 0.240
#&gt; SRR1274555     3  0.4907     0.2823 0.000 0.000 0.580 0.420
#&gt; SRR1274556     3  0.4907     0.2823 0.000 0.000 0.580 0.420
#&gt; SRR1274557     3  0.4907     0.2823 0.000 0.000 0.580 0.420
#&gt; SRR1274558     1  0.4331     0.5620 0.712 0.288 0.000 0.000
#&gt; SRR1274559     1  0.0000     0.8419 1.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000     0.8419 1.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.5233     0.4324 0.648 0.000 0.020 0.332
#&gt; SRR1274562     1  0.5331     0.4258 0.644 0.000 0.024 0.332
#&gt; SRR1274563     3  0.4907     0.2823 0.000 0.000 0.580 0.420
#&gt; SRR1274564     4  0.3123     0.6103 0.000 0.000 0.156 0.844
#&gt; SRR1274565     4  0.4888    -0.0553 0.000 0.412 0.000 0.588
#&gt; SRR1274566     4  0.0376     0.6230 0.000 0.004 0.004 0.992
#&gt; SRR1274567     4  0.0336     0.6252 0.000 0.000 0.008 0.992
#&gt; SRR1274568     1  0.2760     0.7433 0.872 0.128 0.000 0.000
#&gt; SRR1274569     1  0.0000     0.8419 1.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000     0.8419 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000     0.8419 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000     0.8419 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.9309 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.4643     0.5262 0.000 0.656 0.000 0.344
#&gt; SRR1274576     2  0.0188     0.9276 0.000 0.996 0.000 0.004
#&gt; SRR1274577     3  0.7727     0.0122 0.388 0.004 0.416 0.192
#&gt; SRR1274578     1  0.0336     0.8395 0.992 0.000 0.000 0.008
#&gt; SRR1274579     1  0.0188     0.8411 0.996 0.000 0.000 0.004
#&gt; SRR1274580     1  0.0188     0.8411 0.996 0.000 0.000 0.004
#&gt; SRR1274581     1  0.8823     0.0931 0.404 0.368 0.140 0.088
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.4283      0.396 0.000 0.456 0.000 0.544 0.000
#&gt; SRR1274530     4  0.4283      0.396 0.000 0.456 0.000 0.544 0.000
#&gt; SRR1274531     3  0.1399      0.753 0.000 0.000 0.952 0.020 0.028
#&gt; SRR1274532     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.3612      0.671 0.000 0.000 0.268 0.000 0.732
#&gt; SRR1274534     5  0.4389      0.618 0.000 0.184 0.056 0.004 0.756
#&gt; SRR1274535     5  0.3630      0.680 0.000 0.016 0.204 0.000 0.780
#&gt; SRR1274536     4  0.4252      0.493 0.000 0.000 0.280 0.700 0.020
#&gt; SRR1274537     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.4389      0.618 0.000 0.184 0.056 0.004 0.756
#&gt; SRR1274540     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.3336      0.594 0.000 0.772 0.000 0.228 0.000
#&gt; SRR1274546     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0404      0.960 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1274548     2  0.0162      0.967 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1274549     3  0.2798      0.682 0.000 0.000 0.852 0.140 0.008
#&gt; SRR1274550     5  0.4235      0.567 0.000 0.000 0.424 0.000 0.576
#&gt; SRR1274551     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.4182      0.598 0.000 0.000 0.400 0.000 0.600
#&gt; SRR1274553     5  0.4182      0.598 0.000 0.000 0.400 0.000 0.600
#&gt; SRR1274554     5  0.6071      0.525 0.000 0.000 0.192 0.236 0.572
#&gt; SRR1274555     3  0.0000      0.782 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     3  0.0000      0.782 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274557     3  0.0000      0.782 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274558     1  0.4236      0.560 0.728 0.248 0.000 0.008 0.016
#&gt; SRR1274559     1  0.0798      0.781 0.976 0.000 0.000 0.008 0.016
#&gt; SRR1274560     1  0.0798      0.781 0.976 0.000 0.000 0.008 0.016
#&gt; SRR1274561     3  0.4359      0.393 0.412 0.000 0.584 0.000 0.004
#&gt; SRR1274562     3  0.4310      0.422 0.392 0.000 0.604 0.000 0.004
#&gt; SRR1274563     3  0.0000      0.782 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274564     4  0.4114      0.503 0.000 0.000 0.272 0.712 0.016
#&gt; SRR1274565     4  0.3053      0.605 0.000 0.128 0.008 0.852 0.012
#&gt; SRR1274566     4  0.3022      0.571 0.000 0.004 0.136 0.848 0.012
#&gt; SRR1274567     4  0.3203      0.558 0.000 0.000 0.168 0.820 0.012
#&gt; SRR1274568     1  0.4103      0.696 0.812 0.056 0.000 0.024 0.108
#&gt; SRR1274569     1  0.0000      0.786 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.786 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.786 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0566      0.784 0.984 0.000 0.000 0.012 0.004
#&gt; SRR1274573     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.971 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.4283      0.396 0.000 0.456 0.000 0.544 0.000
#&gt; SRR1274576     2  0.2286      0.836 0.000 0.888 0.000 0.004 0.108
#&gt; SRR1274577     5  0.5598      0.267 0.112 0.000 0.000 0.276 0.612
#&gt; SRR1274578     1  0.5682      0.666 0.668 0.000 0.016 0.132 0.184
#&gt; SRR1274579     1  0.5682      0.666 0.668 0.000 0.016 0.132 0.184
#&gt; SRR1274580     1  0.5682      0.666 0.668 0.000 0.016 0.132 0.184
#&gt; SRR1274581     1  0.8957      0.138 0.336 0.284 0.032 0.160 0.188
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.5390      0.340 0.000 0.424 0.012 0.504 0.016 0.044
#&gt; SRR1274530     4  0.5390      0.340 0.000 0.424 0.012 0.504 0.016 0.044
#&gt; SRR1274531     3  0.2333      0.814 0.000 0.000 0.896 0.060 0.040 0.004
#&gt; SRR1274532     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.2350      0.792 0.000 0.000 0.100 0.000 0.880 0.020
#&gt; SRR1274534     5  0.2492      0.746 0.000 0.068 0.000 0.008 0.888 0.036
#&gt; SRR1274535     5  0.1465      0.777 0.000 0.004 0.024 0.004 0.948 0.020
#&gt; SRR1274536     4  0.3176      0.511 0.000 0.000 0.156 0.812 0.032 0.000
#&gt; SRR1274537     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0508      0.950 0.000 0.984 0.000 0.000 0.004 0.012
#&gt; SRR1274539     5  0.2434      0.749 0.000 0.064 0.000 0.008 0.892 0.036
#&gt; SRR1274540     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.4515      0.552 0.000 0.720 0.012 0.212 0.012 0.044
#&gt; SRR1274546     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.2577      0.859 0.000 0.896 0.012 0.036 0.012 0.044
#&gt; SRR1274548     2  0.0405      0.953 0.000 0.988 0.000 0.000 0.004 0.008
#&gt; SRR1274549     3  0.3629      0.644 0.000 0.000 0.724 0.260 0.016 0.000
#&gt; SRR1274550     5  0.3101      0.720 0.000 0.000 0.244 0.000 0.756 0.000
#&gt; SRR1274551     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.3284      0.764 0.000 0.000 0.196 0.000 0.784 0.020
#&gt; SRR1274553     5  0.3284      0.764 0.000 0.000 0.196 0.000 0.784 0.020
#&gt; SRR1274554     5  0.6236      0.362 0.000 0.000 0.036 0.288 0.512 0.164
#&gt; SRR1274555     3  0.0508      0.849 0.000 0.000 0.984 0.004 0.012 0.000
#&gt; SRR1274556     3  0.0508      0.849 0.000 0.000 0.984 0.004 0.012 0.000
#&gt; SRR1274557     3  0.0508      0.849 0.000 0.000 0.984 0.004 0.012 0.000
#&gt; SRR1274558     1  0.1753      0.729 0.912 0.084 0.000 0.000 0.000 0.004
#&gt; SRR1274559     1  0.0000      0.815 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.815 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274561     3  0.4127      0.575 0.284 0.000 0.684 0.004 0.000 0.028
#&gt; SRR1274562     3  0.3857      0.709 0.160 0.000 0.772 0.004 0.000 0.064
#&gt; SRR1274563     3  0.0363      0.847 0.000 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1274564     4  0.2911      0.524 0.000 0.000 0.144 0.832 0.024 0.000
#&gt; SRR1274565     4  0.2752      0.533 0.000 0.012 0.000 0.864 0.020 0.104
#&gt; SRR1274566     4  0.2508      0.547 0.000 0.000 0.016 0.884 0.016 0.084
#&gt; SRR1274567     4  0.2831      0.544 0.000 0.000 0.032 0.868 0.016 0.084
#&gt; SRR1274568     1  0.2357      0.772 0.888 0.012 0.000 0.004 0.004 0.092
#&gt; SRR1274569     1  0.2558      0.811 0.840 0.000 0.000 0.004 0.000 0.156
#&gt; SRR1274570     1  0.2632      0.807 0.832 0.000 0.000 0.004 0.000 0.164
#&gt; SRR1274571     1  0.2773      0.805 0.828 0.000 0.004 0.004 0.000 0.164
#&gt; SRR1274572     1  0.3756      0.593 0.676 0.000 0.004 0.004 0.000 0.316
#&gt; SRR1274573     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.960 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.5390      0.340 0.000 0.424 0.012 0.504 0.016 0.044
#&gt; SRR1274576     2  0.2742      0.823 0.000 0.872 0.000 0.008 0.076 0.044
#&gt; SRR1274577     6  0.4559      0.406 0.008 0.000 0.004 0.092 0.172 0.724
#&gt; SRR1274578     6  0.2964      0.666 0.204 0.000 0.004 0.000 0.000 0.792
#&gt; SRR1274579     6  0.2964      0.666 0.204 0.000 0.004 0.000 0.000 0.792
#&gt; SRR1274580     6  0.2964      0.666 0.204 0.000 0.004 0.000 0.000 0.792
#&gt; SRR1274581     6  0.6972      0.333 0.084 0.280 0.008 0.076 0.032 0.520
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.958       0.982         0.3519 0.628   0.628
#> 3 3 0.968           0.928       0.978         0.3136 0.876   0.804
#> 4 4 0.966           0.927       0.977         0.0714 0.983   0.967
#> 5 5 0.942           0.902       0.969         0.2972 0.845   0.691
#> 6 6 0.905           0.913       0.958         0.0688 0.957   0.877
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 5
```

There is also optional best $k$ = 2 3 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      1.000 0.000 1.000
#&gt; SRR1274529     2   0.000      1.000 0.000 1.000
#&gt; SRR1274530     2   0.000      1.000 0.000 1.000
#&gt; SRR1274531     2   0.000      1.000 0.000 1.000
#&gt; SRR1274532     2   0.000      1.000 0.000 1.000
#&gt; SRR1274533     2   0.000      1.000 0.000 1.000
#&gt; SRR1274534     2   0.000      1.000 0.000 1.000
#&gt; SRR1274535     2   0.000      1.000 0.000 1.000
#&gt; SRR1274536     2   0.000      1.000 0.000 1.000
#&gt; SRR1274537     2   0.000      1.000 0.000 1.000
#&gt; SRR1274538     2   0.000      1.000 0.000 1.000
#&gt; SRR1274539     2   0.000      1.000 0.000 1.000
#&gt; SRR1274540     2   0.000      1.000 0.000 1.000
#&gt; SRR1274541     2   0.000      1.000 0.000 1.000
#&gt; SRR1274542     2   0.000      1.000 0.000 1.000
#&gt; SRR1274543     2   0.000      1.000 0.000 1.000
#&gt; SRR1274544     2   0.000      1.000 0.000 1.000
#&gt; SRR1274545     2   0.000      1.000 0.000 1.000
#&gt; SRR1274546     2   0.000      1.000 0.000 1.000
#&gt; SRR1274547     2   0.000      1.000 0.000 1.000
#&gt; SRR1274548     2   0.000      1.000 0.000 1.000
#&gt; SRR1274549     2   0.000      1.000 0.000 1.000
#&gt; SRR1274550     2   0.000      1.000 0.000 1.000
#&gt; SRR1274551     2   0.000      1.000 0.000 1.000
#&gt; SRR1274552     2   0.000      1.000 0.000 1.000
#&gt; SRR1274553     2   0.000      1.000 0.000 1.000
#&gt; SRR1274554     2   0.000      1.000 0.000 1.000
#&gt; SRR1274555     1   0.975      0.398 0.592 0.408
#&gt; SRR1274556     2   0.000      1.000 0.000 1.000
#&gt; SRR1274557     2   0.000      1.000 0.000 1.000
#&gt; SRR1274558     2   0.000      1.000 0.000 1.000
#&gt; SRR1274559     1   0.697      0.760 0.812 0.188
#&gt; SRR1274560     1   0.000      0.916 1.000 0.000
#&gt; SRR1274561     1   0.000      0.916 1.000 0.000
#&gt; SRR1274562     1   0.000      0.916 1.000 0.000
#&gt; SRR1274563     1   0.000      0.916 1.000 0.000
#&gt; SRR1274564     2   0.000      1.000 0.000 1.000
#&gt; SRR1274565     2   0.000      1.000 0.000 1.000
#&gt; SRR1274566     2   0.000      1.000 0.000 1.000
#&gt; SRR1274567     2   0.000      1.000 0.000 1.000
#&gt; SRR1274568     2   0.000      1.000 0.000 1.000
#&gt; SRR1274569     1   0.000      0.916 1.000 0.000
#&gt; SRR1274570     1   0.000      0.916 1.000 0.000
#&gt; SRR1274571     1   0.000      0.916 1.000 0.000
#&gt; SRR1274572     1   0.000      0.916 1.000 0.000
#&gt; SRR1274573     2   0.000      1.000 0.000 1.000
#&gt; SRR1274574     2   0.000      1.000 0.000 1.000
#&gt; SRR1274575     2   0.000      1.000 0.000 1.000
#&gt; SRR1274576     2   0.000      1.000 0.000 1.000
#&gt; SRR1274577     2   0.000      1.000 0.000 1.000
#&gt; SRR1274578     1   0.971      0.417 0.600 0.400
#&gt; SRR1274579     1   0.000      0.916 1.000 0.000
#&gt; SRR1274580     1   0.000      0.916 1.000 0.000
#&gt; SRR1274581     2   0.000      1.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274529     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274530     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274531     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274532     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274533     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274534     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274535     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274536     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274537     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274538     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274539     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274540     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274541     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274542     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274543     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274544     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274545     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274546     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274547     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274548     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274549     3   0.406      0.685 0.000 0.164 0.836
#&gt; SRR1274550     3   0.613      0.384 0.000 0.400 0.600
#&gt; SRR1274551     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274552     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274553     2   0.129      0.963 0.000 0.968 0.032
#&gt; SRR1274554     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274555     3   0.000      0.807 0.000 0.000 1.000
#&gt; SRR1274556     3   0.000      0.807 0.000 0.000 1.000
#&gt; SRR1274557     3   0.000      0.807 0.000 0.000 1.000
#&gt; SRR1274558     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274559     1   0.450      0.619 0.804 0.196 0.000
#&gt; SRR1274560     1   0.000      0.894 1.000 0.000 0.000
#&gt; SRR1274561     1   0.000      0.894 1.000 0.000 0.000
#&gt; SRR1274562     1   0.116      0.874 0.972 0.000 0.028
#&gt; SRR1274563     3   0.000      0.807 0.000 0.000 1.000
#&gt; SRR1274564     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274565     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274566     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274567     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274568     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274569     1   0.000      0.894 1.000 0.000 0.000
#&gt; SRR1274570     1   0.000      0.894 1.000 0.000 0.000
#&gt; SRR1274571     1   0.000      0.894 1.000 0.000 0.000
#&gt; SRR1274572     1   0.000      0.894 1.000 0.000 0.000
#&gt; SRR1274573     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274574     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274575     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274576     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274577     2   0.000      0.999 0.000 1.000 0.000
#&gt; SRR1274578     1   0.610      0.264 0.608 0.392 0.000
#&gt; SRR1274579     1   0.000      0.894 1.000 0.000 0.000
#&gt; SRR1274580     1   0.000      0.894 1.000 0.000 0.000
#&gt; SRR1274581     2   0.000      0.999 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274530     2  0.0336      0.983 0.000 0.992 0.000 0.008
#&gt; SRR1274531     2  0.0592      0.978 0.000 0.984 0.000 0.016
#&gt; SRR1274532     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274533     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274534     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274535     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274536     2  0.0592      0.978 0.000 0.984 0.000 0.016
#&gt; SRR1274537     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274539     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274540     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274549     3  0.3790      0.587 0.000 0.164 0.820 0.016
#&gt; SRR1274550     3  0.4855      0.306 0.000 0.400 0.600 0.000
#&gt; SRR1274551     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274552     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274553     2  0.1022      0.958 0.000 0.968 0.032 0.000
#&gt; SRR1274554     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274555     3  0.0000      0.740 0.000 0.000 1.000 0.000
#&gt; SRR1274556     3  0.0000      0.740 0.000 0.000 1.000 0.000
#&gt; SRR1274557     3  0.0000      0.740 0.000 0.000 1.000 0.000
#&gt; SRR1274558     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274559     1  0.3444      0.600 0.816 0.184 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.944 1.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.0000      0.944 1.000 0.000 0.000 0.000
#&gt; SRR1274562     1  0.0336      0.938 0.992 0.000 0.008 0.000
#&gt; SRR1274563     3  0.0000      0.740 0.000 0.000 1.000 0.000
#&gt; SRR1274564     2  0.0592      0.978 0.000 0.984 0.000 0.016
#&gt; SRR1274565     2  0.0592      0.978 0.000 0.984 0.000 0.016
#&gt; SRR1274566     2  0.0592      0.978 0.000 0.984 0.000 0.016
#&gt; SRR1274567     2  0.0592      0.978 0.000 0.984 0.000 0.016
#&gt; SRR1274568     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274569     1  0.0000      0.944 1.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.944 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.944 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.944 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.0336      0.983 0.000 0.992 0.000 0.008
#&gt; SRR1274576     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274577     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR1274578     4  0.0592      1.000 0.016 0.000 0.000 0.984
#&gt; SRR1274579     4  0.0592      1.000 0.016 0.000 0.000 0.984
#&gt; SRR1274580     4  0.0592      1.000 0.016 0.000 0.000 0.984
#&gt; SRR1274581     2  0.4331      0.582 0.000 0.712 0.000 0.288
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274530     2  0.0510      0.960 0.000 0.984 0.000 0.016 0.000
#&gt; SRR1274531     4  0.0703      0.859 0.000 0.024 0.000 0.976 0.000
#&gt; SRR1274532     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274534     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274535     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274536     4  0.0290      0.877 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1274537     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274540     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     4  0.0290      0.865 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1274550     3  0.4425      0.264 0.000 0.392 0.600 0.008 0.000
#&gt; SRR1274551     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     2  0.0290      0.967 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1274553     2  0.1168      0.939 0.000 0.960 0.032 0.008 0.000
#&gt; SRR1274554     4  0.4268      0.210 0.000 0.444 0.000 0.556 0.000
#&gt; SRR1274555     3  0.0000      0.788 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     3  0.0000      0.788 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274557     3  0.0000      0.788 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274558     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274559     1  0.2020      0.806 0.900 0.100 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274562     1  0.0290      0.966 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1274563     3  0.0000      0.788 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274564     4  0.0290      0.877 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1274565     4  0.0290      0.877 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1274566     4  0.0290      0.877 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1274567     4  0.0290      0.877 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1274568     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274569     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.972 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.1965      0.875 0.000 0.904 0.000 0.096 0.000
#&gt; SRR1274576     2  0.0000      0.974 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274577     2  0.3210      0.704 0.000 0.788 0.000 0.212 0.000
#&gt; SRR1274578     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274579     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274580     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274581     2  0.3816      0.567 0.000 0.696 0.000 0.000 0.304
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274530     2  0.0458      0.948 0.000 0.984 0.000 0.016 0.000 0.000
#&gt; SRR1274531     4  0.0458      0.864 0.000 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1274532     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     2  0.0790      0.934 0.000 0.968 0.000 0.000 0.032 0.000
#&gt; SRR1274534     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274535     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274536     4  0.0000      0.883 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274537     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274540     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274549     4  0.0000      0.883 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274550     5  0.2340      1.000 0.000 0.148 0.000 0.000 0.852 0.000
#&gt; SRR1274551     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.2340      1.000 0.000 0.148 0.000 0.000 0.852 0.000
#&gt; SRR1274553     5  0.2340      1.000 0.000 0.148 0.000 0.000 0.852 0.000
#&gt; SRR1274554     4  0.3823      0.140 0.000 0.436 0.000 0.564 0.000 0.000
#&gt; SRR1274555     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274556     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274557     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274558     2  0.2340      0.794 0.000 0.852 0.000 0.000 0.148 0.000
#&gt; SRR1274559     1  0.3967      0.754 0.760 0.092 0.000 0.000 0.148 0.000
#&gt; SRR1274560     1  0.2340      0.874 0.852 0.000 0.000 0.000 0.148 0.000
#&gt; SRR1274561     1  0.1814      0.900 0.900 0.000 0.000 0.000 0.100 0.000
#&gt; SRR1274562     1  0.1007      0.912 0.956 0.000 0.044 0.000 0.000 0.000
#&gt; SRR1274563     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274564     4  0.0000      0.883 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274565     4  0.0000      0.883 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274566     4  0.0000      0.883 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274567     4  0.0000      0.883 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274568     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274569     1  0.0000      0.927 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.927 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.927 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.927 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.1765      0.858 0.000 0.904 0.000 0.096 0.000 0.000
#&gt; SRR1274576     2  0.0000      0.962 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274577     2  0.2969      0.659 0.000 0.776 0.000 0.224 0.000 0.000
#&gt; SRR1274578     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274579     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274580     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274581     2  0.3565      0.497 0.000 0.692 0.000 0.004 0.000 0.304
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.747           0.858       0.939         0.4397 0.575   0.575
#> 3 3 0.346           0.248       0.678         0.3211 0.640   0.476
#> 4 4 0.465           0.533       0.715         0.1654 0.748   0.531
#> 5 5 0.529           0.541       0.689         0.1093 0.646   0.258
#> 6 6 0.627           0.538       0.708         0.0601 0.843   0.416
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000      0.933 0.000 1.000
#&gt; SRR1274529     1  0.9795      0.337 0.584 0.416
#&gt; SRR1274530     1  0.9833      0.315 0.576 0.424
#&gt; SRR1274531     1  0.0672      0.927 0.992 0.008
#&gt; SRR1274532     2  0.0000      0.933 0.000 1.000
#&gt; SRR1274533     1  0.0672      0.927 0.992 0.008
#&gt; SRR1274534     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274535     1  0.2778      0.896 0.952 0.048
#&gt; SRR1274536     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274537     2  0.8327      0.682 0.264 0.736
#&gt; SRR1274538     2  0.3733      0.898 0.072 0.928
#&gt; SRR1274539     1  0.4298      0.860 0.912 0.088
#&gt; SRR1274540     2  0.0000      0.933 0.000 1.000
#&gt; SRR1274541     2  0.0000      0.933 0.000 1.000
#&gt; SRR1274542     2  0.0000      0.933 0.000 1.000
#&gt; SRR1274543     2  0.2948      0.911 0.052 0.948
#&gt; SRR1274544     2  0.0000      0.933 0.000 1.000
#&gt; SRR1274545     1  0.9996      0.105 0.512 0.488
#&gt; SRR1274546     2  0.0000      0.933 0.000 1.000
#&gt; SRR1274547     2  0.7745      0.693 0.228 0.772
#&gt; SRR1274548     2  0.8144      0.701 0.252 0.748
#&gt; SRR1274549     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274550     1  0.0672      0.927 0.992 0.008
#&gt; SRR1274551     2  0.0376      0.933 0.004 0.996
#&gt; SRR1274552     1  0.0672      0.927 0.992 0.008
#&gt; SRR1274553     1  0.0376      0.929 0.996 0.004
#&gt; SRR1274554     1  0.1184      0.922 0.984 0.016
#&gt; SRR1274555     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274556     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274557     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274558     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274559     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274560     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274561     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274562     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274563     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274564     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274565     1  0.7950      0.680 0.760 0.240
#&gt; SRR1274566     1  0.6623      0.770 0.828 0.172
#&gt; SRR1274567     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274568     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274569     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274570     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274571     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274572     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274573     2  0.0000      0.933 0.000 1.000
#&gt; SRR1274574     2  0.0376      0.933 0.004 0.996
#&gt; SRR1274575     1  0.9795      0.337 0.584 0.416
#&gt; SRR1274576     2  0.2778      0.913 0.048 0.952
#&gt; SRR1274577     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274578     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274579     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274580     1  0.0000      0.931 1.000 0.000
#&gt; SRR1274581     1  0.0376      0.929 0.996 0.004
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2   0.362    0.67286 0.136 0.864 0.000
#&gt; SRR1274529     2   0.586    0.52690 0.020 0.740 0.240
#&gt; SRR1274530     2   0.536    0.55180 0.020 0.784 0.196
#&gt; SRR1274531     3   0.620   -0.02130 0.000 0.424 0.576
#&gt; SRR1274532     2   0.369    0.67297 0.140 0.860 0.000
#&gt; SRR1274533     2   0.966    0.37165 0.244 0.460 0.296
#&gt; SRR1274534     2   0.914    0.23456 0.144 0.448 0.408
#&gt; SRR1274535     2   0.966    0.37165 0.244 0.460 0.296
#&gt; SRR1274536     3   0.843   -0.04564 0.260 0.136 0.604
#&gt; SRR1274537     2   0.594    0.62506 0.064 0.784 0.152
#&gt; SRR1274538     2   0.511    0.61951 0.008 0.780 0.212
#&gt; SRR1274539     2   0.966    0.37165 0.244 0.460 0.296
#&gt; SRR1274540     2   0.369    0.67297 0.140 0.860 0.000
#&gt; SRR1274541     2   0.369    0.67297 0.140 0.860 0.000
#&gt; SRR1274542     2   0.369    0.67297 0.140 0.860 0.000
#&gt; SRR1274543     2   0.429    0.65393 0.008 0.840 0.152
#&gt; SRR1274544     2   0.369    0.67297 0.140 0.860 0.000
#&gt; SRR1274545     2   0.495    0.57925 0.016 0.808 0.176
#&gt; SRR1274546     2   0.369    0.67297 0.140 0.860 0.000
#&gt; SRR1274547     2   0.362    0.63051 0.000 0.864 0.136
#&gt; SRR1274548     2   0.506    0.61983 0.008 0.784 0.208
#&gt; SRR1274549     3   0.819   -0.11308 0.292 0.104 0.604
#&gt; SRR1274550     3   0.784   -0.14986 0.052 0.456 0.492
#&gt; SRR1274551     2   0.369    0.67297 0.140 0.860 0.000
#&gt; SRR1274552     3   0.792   -0.16459 0.056 0.460 0.484
#&gt; SRR1274553     3   0.792   -0.16459 0.056 0.460 0.484
#&gt; SRR1274554     2   0.966    0.37165 0.244 0.460 0.296
#&gt; SRR1274555     3   0.826   -0.30086 0.436 0.076 0.488
#&gt; SRR1274556     3   0.755   -0.01429 0.044 0.396 0.560
#&gt; SRR1274557     3   0.755   -0.01429 0.044 0.396 0.560
#&gt; SRR1274558     3   0.502   -0.24325 0.240 0.000 0.760
#&gt; SRR1274559     3   0.502   -0.24325 0.240 0.000 0.760
#&gt; SRR1274560     3   0.502   -0.24325 0.240 0.000 0.760
#&gt; SRR1274561     1   0.620    0.94302 0.576 0.000 0.424
#&gt; SRR1274562     1   0.620    0.94302 0.576 0.000 0.424
#&gt; SRR1274563     1   0.604    0.88508 0.620 0.000 0.380
#&gt; SRR1274564     3   0.613    0.01902 0.000 0.400 0.600
#&gt; SRR1274565     2   0.652    0.15363 0.004 0.504 0.492
#&gt; SRR1274566     3   0.621   -0.03045 0.000 0.428 0.572
#&gt; SRR1274567     3   0.815   -0.12159 0.296 0.100 0.604
#&gt; SRR1274568     3   0.502   -0.24325 0.240 0.000 0.760
#&gt; SRR1274569     3   0.522   -0.23620 0.260 0.000 0.740
#&gt; SRR1274570     3   0.525   -0.23969 0.264 0.000 0.736
#&gt; SRR1274571     3   0.525   -0.23969 0.264 0.000 0.736
#&gt; SRR1274572     3   0.525   -0.23969 0.264 0.000 0.736
#&gt; SRR1274573     2   0.369    0.67297 0.140 0.860 0.000
#&gt; SRR1274574     2   0.196    0.67880 0.056 0.944 0.000
#&gt; SRR1274575     2   0.536    0.55180 0.020 0.784 0.196
#&gt; SRR1274576     2   0.383    0.66282 0.008 0.868 0.124
#&gt; SRR1274577     3   0.528   -0.24347 0.180 0.024 0.796
#&gt; SRR1274578     3   0.514   -0.23790 0.252 0.000 0.748
#&gt; SRR1274579     3   0.522   -0.23620 0.260 0.000 0.740
#&gt; SRR1274580     3   0.522   -0.23620 0.260 0.000 0.740
#&gt; SRR1274581     3   0.494    0.00975 0.056 0.104 0.840
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.4916      0.630 0.000 0.576 0.000 0.424
#&gt; SRR1274529     2  0.5564      0.627 0.000 0.708 0.076 0.216
#&gt; SRR1274530     2  0.5953      0.633 0.000 0.656 0.076 0.268
#&gt; SRR1274531     2  0.5506      0.391 0.072 0.772 0.120 0.036
#&gt; SRR1274532     2  0.4925      0.630 0.000 0.572 0.000 0.428
#&gt; SRR1274533     2  0.6691     -0.522 0.016 0.560 0.060 0.364
#&gt; SRR1274534     2  0.6529      0.192 0.056 0.696 0.068 0.180
#&gt; SRR1274535     2  0.6495     -0.672 0.004 0.492 0.060 0.444
#&gt; SRR1274536     2  0.5288      0.377 0.060 0.740 0.196 0.004
#&gt; SRR1274537     2  0.3765      0.287 0.004 0.812 0.004 0.180
#&gt; SRR1274538     2  0.0188      0.529 0.000 0.996 0.000 0.004
#&gt; SRR1274539     2  0.6233      0.158 0.040 0.704 0.060 0.196
#&gt; SRR1274540     2  0.4898      0.631 0.000 0.584 0.000 0.416
#&gt; SRR1274541     2  0.4925      0.630 0.000 0.572 0.000 0.428
#&gt; SRR1274542     2  0.4925      0.630 0.000 0.572 0.000 0.428
#&gt; SRR1274543     2  0.1557      0.566 0.000 0.944 0.000 0.056
#&gt; SRR1274544     2  0.4925      0.630 0.000 0.572 0.000 0.428
#&gt; SRR1274545     2  0.5677      0.636 0.000 0.680 0.064 0.256
#&gt; SRR1274546     2  0.4925      0.630 0.000 0.572 0.000 0.428
#&gt; SRR1274547     2  0.4840      0.639 0.000 0.732 0.028 0.240
#&gt; SRR1274548     2  0.0188      0.535 0.000 0.996 0.000 0.004
#&gt; SRR1274549     2  0.6117      0.328 0.072 0.688 0.224 0.016
#&gt; SRR1274550     4  0.7869      0.770 0.060 0.380 0.080 0.480
#&gt; SRR1274551     2  0.4877      0.633 0.000 0.592 0.000 0.408
#&gt; SRR1274552     4  0.7761      0.810 0.060 0.336 0.080 0.524
#&gt; SRR1274553     4  0.7720      0.806 0.060 0.324 0.080 0.536
#&gt; SRR1274554     2  0.6497     -0.678 0.004 0.488 0.060 0.448
#&gt; SRR1274555     3  0.3668      0.670 0.072 0.024 0.872 0.032
#&gt; SRR1274556     3  0.7392      0.239 0.072 0.364 0.524 0.040
#&gt; SRR1274557     3  0.7172      0.385 0.072 0.304 0.584 0.040
#&gt; SRR1274558     1  0.7696      0.621 0.536 0.028 0.300 0.136
#&gt; SRR1274559     1  0.5254      0.746 0.672 0.028 0.300 0.000
#&gt; SRR1274560     1  0.5231      0.750 0.676 0.028 0.296 0.000
#&gt; SRR1274561     3  0.2760      0.625 0.128 0.000 0.872 0.000
#&gt; SRR1274562     3  0.2760      0.625 0.128 0.000 0.872 0.000
#&gt; SRR1274563     3  0.3497      0.630 0.124 0.000 0.852 0.024
#&gt; SRR1274564     2  0.4606      0.439 0.060 0.808 0.124 0.008
#&gt; SRR1274565     2  0.3304      0.476 0.048 0.888 0.052 0.012
#&gt; SRR1274566     2  0.4147      0.451 0.040 0.832 0.120 0.008
#&gt; SRR1274567     3  0.5325      0.515 0.068 0.204 0.728 0.000
#&gt; SRR1274568     1  0.7153      0.698 0.604 0.028 0.264 0.104
#&gt; SRR1274569     1  0.3266      0.833 0.832 0.000 0.168 0.000
#&gt; SRR1274570     1  0.3266      0.833 0.832 0.000 0.168 0.000
#&gt; SRR1274571     1  0.3266      0.833 0.832 0.000 0.168 0.000
#&gt; SRR1274572     1  0.3266      0.833 0.832 0.000 0.168 0.000
#&gt; SRR1274573     2  0.4925      0.630 0.000 0.572 0.000 0.428
#&gt; SRR1274574     2  0.4605      0.639 0.000 0.664 0.000 0.336
#&gt; SRR1274575     2  0.5873      0.632 0.000 0.668 0.076 0.256
#&gt; SRR1274576     2  0.1389      0.558 0.000 0.952 0.000 0.048
#&gt; SRR1274577     4  0.9028      0.632 0.292 0.256 0.064 0.388
#&gt; SRR1274578     1  0.0707      0.765 0.980 0.000 0.020 0.000
#&gt; SRR1274579     1  0.0000      0.762 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.762 1.000 0.000 0.000 0.000
#&gt; SRR1274581     4  0.8623      0.752 0.168 0.376 0.056 0.400
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     4  0.0609    0.89698 0.000 0.020 0.000 0.980 0.000
#&gt; SRR1274529     2  0.5120    0.32794 0.000 0.628 0.028 0.328 0.016
#&gt; SRR1274530     2  0.4910    0.30404 0.000 0.628 0.020 0.340 0.012
#&gt; SRR1274531     3  0.4596    0.55046 0.000 0.148 0.768 0.020 0.064
#&gt; SRR1274532     4  0.0000    0.90802 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274533     5  0.5615    0.88933 0.000 0.052 0.228 0.048 0.672
#&gt; SRR1274534     5  0.7247    0.85555 0.036 0.088 0.208 0.076 0.592
#&gt; SRR1274535     5  0.4665    0.87952 0.000 0.040 0.224 0.012 0.724
#&gt; SRR1274536     3  0.4312    0.56229 0.000 0.156 0.776 0.008 0.060
#&gt; SRR1274537     2  0.8014    0.43651 0.012 0.468 0.196 0.228 0.096
#&gt; SRR1274538     2  0.7975    0.44443 0.012 0.404 0.204 0.316 0.064
#&gt; SRR1274539     5  0.7097    0.86235 0.024 0.092 0.212 0.076 0.596
#&gt; SRR1274540     4  0.0963    0.89193 0.000 0.036 0.000 0.964 0.000
#&gt; SRR1274541     4  0.0000    0.90802 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274542     4  0.0000    0.90802 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274543     2  0.8174    0.42345 0.012 0.416 0.188 0.288 0.096
#&gt; SRR1274544     4  0.0000    0.90802 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274545     2  0.5136    0.21686 0.000 0.528 0.024 0.440 0.008
#&gt; SRR1274546     4  0.0000    0.90802 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274547     2  0.5774    0.24900 0.000 0.492 0.028 0.444 0.036
#&gt; SRR1274548     2  0.7813    0.46424 0.012 0.464 0.200 0.260 0.064
#&gt; SRR1274549     3  0.2625    0.60335 0.000 0.108 0.876 0.016 0.000
#&gt; SRR1274550     3  0.4625    0.36299 0.000 0.012 0.660 0.012 0.316
#&gt; SRR1274551     4  0.1341    0.87705 0.000 0.056 0.000 0.944 0.000
#&gt; SRR1274552     3  0.4661    0.35242 0.000 0.012 0.652 0.012 0.324
#&gt; SRR1274553     3  0.4643    0.35831 0.000 0.012 0.656 0.012 0.320
#&gt; SRR1274554     5  0.4665    0.87952 0.000 0.040 0.224 0.012 0.724
#&gt; SRR1274555     3  0.4210    0.53664 0.000 0.036 0.740 0.000 0.224
#&gt; SRR1274556     3  0.1988    0.60822 0.000 0.048 0.928 0.008 0.016
#&gt; SRR1274557     3  0.3071    0.60163 0.000 0.032 0.880 0.032 0.056
#&gt; SRR1274558     2  0.6992    0.00298 0.224 0.564 0.136 0.000 0.076
#&gt; SRR1274559     2  0.7057   -0.09343 0.256 0.532 0.156 0.000 0.056
#&gt; SRR1274560     1  0.7188    0.46426 0.444 0.360 0.148 0.000 0.048
#&gt; SRR1274561     3  0.5589    0.53595 0.036 0.076 0.684 0.000 0.204
#&gt; SRR1274562     3  0.5308    0.53784 0.032 0.068 0.708 0.000 0.192
#&gt; SRR1274563     3  0.4588    0.53819 0.004 0.056 0.732 0.000 0.208
#&gt; SRR1274564     3  0.4650    0.54425 0.000 0.140 0.772 0.036 0.052
#&gt; SRR1274565     2  0.8387    0.34182 0.052 0.408 0.328 0.140 0.072
#&gt; SRR1274566     3  0.7513   -0.32038 0.000 0.364 0.420 0.128 0.088
#&gt; SRR1274567     3  0.5300    0.57557 0.008 0.060 0.752 0.076 0.104
#&gt; SRR1274568     2  0.6871   -0.02253 0.256 0.552 0.140 0.000 0.052
#&gt; SRR1274569     1  0.3305    0.84686 0.776 0.224 0.000 0.000 0.000
#&gt; SRR1274570     1  0.3461    0.84554 0.772 0.224 0.000 0.000 0.004
#&gt; SRR1274571     1  0.3305    0.84686 0.776 0.224 0.000 0.000 0.000
#&gt; SRR1274572     1  0.3305    0.84686 0.776 0.224 0.000 0.000 0.000
#&gt; SRR1274573     4  0.0880    0.88091 0.000 0.032 0.000 0.968 0.000
#&gt; SRR1274574     4  0.4822   -0.08201 0.000 0.416 0.016 0.564 0.004
#&gt; SRR1274575     2  0.5042    0.32080 0.000 0.628 0.028 0.332 0.012
#&gt; SRR1274576     2  0.8044    0.46115 0.012 0.440 0.196 0.268 0.084
#&gt; SRR1274577     2  0.7968   -0.06788 0.076 0.328 0.312 0.000 0.284
#&gt; SRR1274578     1  0.2127    0.73302 0.892 0.000 0.108 0.000 0.000
#&gt; SRR1274579     1  0.0000    0.78515 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000    0.78515 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     2  0.7348   -0.05751 0.024 0.352 0.332 0.000 0.292
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.1007    0.71099 0.000 0.956 0.000 0.000 0.000 0.044
#&gt; SRR1274529     6  0.4178    0.43932 0.000 0.284 0.000 0.012 0.020 0.684
#&gt; SRR1274530     6  0.4044    0.41906 0.000 0.312 0.000 0.008 0.012 0.668
#&gt; SRR1274531     4  0.7439    0.61852 0.000 0.028 0.156 0.448 0.268 0.100
#&gt; SRR1274532     2  0.0000    0.73254 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.2405    0.82010 0.000 0.016 0.004 0.000 0.880 0.100
#&gt; SRR1274534     5  0.3351    0.78088 0.000 0.036 0.000 0.004 0.808 0.152
#&gt; SRR1274535     5  0.1411    0.83263 0.000 0.004 0.000 0.000 0.936 0.060
#&gt; SRR1274536     4  0.5968    0.66864 0.000 0.000 0.044 0.580 0.236 0.140
#&gt; SRR1274537     6  0.5137    0.12012 0.000 0.416 0.000 0.004 0.072 0.508
#&gt; SRR1274538     2  0.6108   -0.06095 0.000 0.424 0.000 0.004 0.240 0.332
#&gt; SRR1274539     5  0.3313    0.77990 0.000 0.036 0.000 0.004 0.812 0.148
#&gt; SRR1274540     2  0.0458    0.72528 0.000 0.984 0.000 0.000 0.000 0.016
#&gt; SRR1274541     2  0.0000    0.73254 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000    0.73254 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.6134   -0.06409 0.000 0.408 0.000 0.004 0.244 0.344
#&gt; SRR1274544     2  0.0000    0.73254 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     6  0.4877    0.30691 0.000 0.424 0.000 0.036 0.012 0.528
#&gt; SRR1274546     2  0.0146    0.73055 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1274547     6  0.4935    0.19745 0.000 0.460 0.000 0.004 0.052 0.484
#&gt; SRR1274548     6  0.5160    0.06354 0.000 0.448 0.000 0.004 0.072 0.476
#&gt; SRR1274549     4  0.5804    0.43505 0.004 0.000 0.332 0.532 0.116 0.016
#&gt; SRR1274550     5  0.1801    0.80648 0.000 0.004 0.040 0.012 0.932 0.012
#&gt; SRR1274551     2  0.1204    0.69346 0.000 0.944 0.000 0.000 0.000 0.056
#&gt; SRR1274552     5  0.1672    0.81174 0.000 0.004 0.028 0.012 0.940 0.016
#&gt; SRR1274553     5  0.1749    0.81006 0.000 0.004 0.032 0.012 0.936 0.016
#&gt; SRR1274554     5  0.1333    0.83370 0.000 0.008 0.000 0.000 0.944 0.048
#&gt; SRR1274555     3  0.0146    0.87922 0.000 0.004 0.996 0.000 0.000 0.000
#&gt; SRR1274556     3  0.2256    0.86877 0.000 0.008 0.892 0.004 0.092 0.004
#&gt; SRR1274557     3  0.2205    0.87353 0.000 0.008 0.896 0.004 0.088 0.004
#&gt; SRR1274558     6  0.7558   -0.23732 0.316 0.000 0.032 0.268 0.056 0.328
#&gt; SRR1274559     1  0.7209   -0.00272 0.412 0.000 0.040 0.288 0.028 0.232
#&gt; SRR1274560     1  0.6593    0.17151 0.524 0.000 0.040 0.268 0.020 0.148
#&gt; SRR1274561     4  0.5532    0.40407 0.096 0.000 0.304 0.580 0.004 0.016
#&gt; SRR1274562     4  0.5447    0.35666 0.104 0.000 0.340 0.548 0.004 0.004
#&gt; SRR1274563     3  0.0260    0.87412 0.008 0.000 0.992 0.000 0.000 0.000
#&gt; SRR1274564     4  0.6798    0.65172 0.000 0.032 0.040 0.524 0.236 0.168
#&gt; SRR1274565     4  0.7790    0.25952 0.016 0.136 0.000 0.332 0.216 0.300
#&gt; SRR1274566     4  0.7316    0.60989 0.000 0.116 0.036 0.492 0.240 0.116
#&gt; SRR1274567     4  0.6049    0.67589 0.008 0.008 0.072 0.612 0.236 0.064
#&gt; SRR1274568     6  0.7561   -0.24787 0.268 0.000 0.036 0.268 0.056 0.372
#&gt; SRR1274569     1  0.0146    0.70681 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1274570     1  0.0000    0.70719 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0146    0.70681 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1274572     1  0.0000    0.70719 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0146    0.73053 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1274574     2  0.3151    0.42814 0.000 0.748 0.000 0.000 0.000 0.252
#&gt; SRR1274575     6  0.4097    0.43987 0.000 0.284 0.000 0.012 0.016 0.688
#&gt; SRR1274576     2  0.6138   -0.06898 0.000 0.428 0.000 0.004 0.272 0.296
#&gt; SRR1274577     5  0.4797    0.58555 0.016 0.000 0.008 0.032 0.644 0.300
#&gt; SRR1274578     1  0.4264    0.61976 0.604 0.000 0.000 0.376 0.008 0.012
#&gt; SRR1274579     1  0.4161    0.62056 0.608 0.000 0.000 0.376 0.004 0.012
#&gt; SRR1274580     1  0.4161    0.62056 0.608 0.000 0.000 0.376 0.004 0.012
#&gt; SRR1274581     5  0.4392    0.68060 0.012 0.004 0.000 0.044 0.716 0.224
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.641           0.847       0.926         0.4801 0.508   0.508
#> 3 3 0.875           0.876       0.950         0.3501 0.735   0.527
#> 4 4 0.632           0.455       0.716         0.1236 0.881   0.682
#> 5 5 0.760           0.725       0.826         0.0718 0.796   0.412
#> 6 6 0.880           0.828       0.916         0.0468 0.952   0.780
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274529     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274530     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274531     1  0.9896      0.363 0.560 0.440
#&gt; SRR1274532     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274533     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274534     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274535     2  0.0376      0.935 0.004 0.996
#&gt; SRR1274536     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274537     2  0.3879      0.863 0.076 0.924
#&gt; SRR1274538     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274539     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274540     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274541     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274542     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274543     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274544     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274545     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274546     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274547     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274548     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274549     1  0.7219      0.828 0.800 0.200
#&gt; SRR1274550     1  0.7219      0.828 0.800 0.200
#&gt; SRR1274551     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274552     1  0.7219      0.828 0.800 0.200
#&gt; SRR1274553     1  0.7219      0.828 0.800 0.200
#&gt; SRR1274554     2  0.9635      0.235 0.388 0.612
#&gt; SRR1274555     1  0.7219      0.828 0.800 0.200
#&gt; SRR1274556     1  0.7219      0.828 0.800 0.200
#&gt; SRR1274557     1  0.7219      0.828 0.800 0.200
#&gt; SRR1274558     2  0.9460      0.473 0.364 0.636
#&gt; SRR1274559     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274560     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274561     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274562     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274563     1  0.7219      0.828 0.800 0.200
#&gt; SRR1274564     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274565     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274566     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274567     1  0.7602      0.805 0.780 0.220
#&gt; SRR1274568     2  0.9754      0.376 0.408 0.592
#&gt; SRR1274569     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274570     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274571     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274572     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274573     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274574     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274575     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274576     2  0.0000      0.939 0.000 1.000
#&gt; SRR1274577     2  0.9998      0.127 0.492 0.508
#&gt; SRR1274578     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274579     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274580     1  0.0000      0.878 1.000 0.000
#&gt; SRR1274581     1  0.0000      0.878 1.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274530     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274531     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274532     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274533     3  0.2878      0.880 0.000 0.096 0.904
#&gt; SRR1274534     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274535     3  0.1529      0.938 0.000 0.040 0.960
#&gt; SRR1274536     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274537     2  0.0237      0.948 0.004 0.996 0.000
#&gt; SRR1274538     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274539     2  0.0237      0.949 0.000 0.996 0.004
#&gt; SRR1274540     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274546     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274549     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274550     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274551     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274552     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274553     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274554     3  0.0424      0.964 0.000 0.008 0.992
#&gt; SRR1274555     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274556     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274557     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274558     1  0.5948      0.439 0.640 0.360 0.000
#&gt; SRR1274559     1  0.0000      0.893 1.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.893 1.000 0.000 0.000
#&gt; SRR1274561     1  0.4796      0.696 0.780 0.000 0.220
#&gt; SRR1274562     1  0.3941      0.778 0.844 0.000 0.156
#&gt; SRR1274563     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274564     3  0.4931      0.682 0.000 0.232 0.768
#&gt; SRR1274565     2  0.3879      0.796 0.000 0.848 0.152
#&gt; SRR1274566     2  0.6291      0.120 0.000 0.532 0.468
#&gt; SRR1274567     3  0.0237      0.967 0.000 0.004 0.996
#&gt; SRR1274568     1  0.6180      0.298 0.584 0.416 0.000
#&gt; SRR1274569     1  0.0000      0.893 1.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.893 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.893 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0237      0.893 0.996 0.000 0.004
#&gt; SRR1274573     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274576     2  0.0000      0.952 0.000 1.000 0.000
#&gt; SRR1274577     2  0.6359      0.233 0.404 0.592 0.004
#&gt; SRR1274578     1  0.0237      0.893 0.996 0.000 0.004
#&gt; SRR1274579     1  0.0237      0.893 0.996 0.000 0.004
#&gt; SRR1274580     1  0.0237      0.893 0.996 0.000 0.004
#&gt; SRR1274581     1  0.2165      0.860 0.936 0.000 0.064
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.4804    0.53253 0.384 0.616 0.000 0.000
#&gt; SRR1274530     2  0.4804    0.53253 0.384 0.616 0.000 0.000
#&gt; SRR1274531     3  0.4103    0.62223 0.000 0.000 0.744 0.256
#&gt; SRR1274532     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274533     3  0.2760    0.55577 0.000 0.128 0.872 0.000
#&gt; SRR1274534     2  0.4933    0.32623 0.000 0.568 0.432 0.000
#&gt; SRR1274535     3  0.3400    0.50643 0.000 0.180 0.820 0.000
#&gt; SRR1274536     4  0.7514   -0.02030 0.384 0.000 0.184 0.432
#&gt; SRR1274537     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0188    0.81793 0.000 0.996 0.004 0.000
#&gt; SRR1274539     2  0.4933    0.32623 0.000 0.568 0.432 0.000
#&gt; SRR1274540     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.4790    0.53611 0.380 0.620 0.000 0.000
#&gt; SRR1274546     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.4331    0.61362 0.288 0.712 0.000 0.000
#&gt; SRR1274548     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274549     3  0.5105    0.58971 0.004 0.000 0.564 0.432
#&gt; SRR1274550     3  0.0000    0.62739 0.000 0.000 1.000 0.000
#&gt; SRR1274551     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.0188    0.62588 0.000 0.004 0.996 0.000
#&gt; SRR1274553     3  0.0000    0.62739 0.000 0.000 1.000 0.000
#&gt; SRR1274554     3  0.6152    0.57850 0.000 0.120 0.668 0.212
#&gt; SRR1274555     3  0.4933    0.59386 0.000 0.000 0.568 0.432
#&gt; SRR1274556     3  0.4933    0.59386 0.000 0.000 0.568 0.432
#&gt; SRR1274557     3  0.4933    0.59386 0.000 0.000 0.568 0.432
#&gt; SRR1274558     1  0.6489    0.31984 0.548 0.372 0.000 0.080
#&gt; SRR1274559     1  0.4804    0.47845 0.616 0.000 0.000 0.384
#&gt; SRR1274560     1  0.4804    0.47845 0.616 0.000 0.000 0.384
#&gt; SRR1274561     4  0.4123    0.13465 0.220 0.000 0.008 0.772
#&gt; SRR1274562     4  0.5594    0.22030 0.100 0.000 0.180 0.720
#&gt; SRR1274563     3  0.4933    0.59386 0.000 0.000 0.568 0.432
#&gt; SRR1274564     4  0.7514   -0.02030 0.384 0.000 0.184 0.432
#&gt; SRR1274565     1  0.9223   -0.24505 0.384 0.304 0.088 0.224
#&gt; SRR1274566     4  0.8156   -0.00363 0.384 0.032 0.156 0.428
#&gt; SRR1274567     4  0.7514   -0.02030 0.384 0.000 0.184 0.432
#&gt; SRR1274568     1  0.6407    0.29838 0.520 0.412 0.000 0.068
#&gt; SRR1274569     1  0.4804    0.47845 0.616 0.000 0.000 0.384
#&gt; SRR1274570     1  0.4804    0.47845 0.616 0.000 0.000 0.384
#&gt; SRR1274571     1  0.4804    0.47845 0.616 0.000 0.000 0.384
#&gt; SRR1274572     4  0.4985   -0.37758 0.468 0.000 0.000 0.532
#&gt; SRR1274573     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0469    0.81414 0.012 0.988 0.000 0.000
#&gt; SRR1274575     2  0.4804    0.53253 0.384 0.616 0.000 0.000
#&gt; SRR1274576     2  0.0000    0.82024 0.000 1.000 0.000 0.000
#&gt; SRR1274577     2  0.9663   -0.12073 0.156 0.360 0.276 0.208
#&gt; SRR1274578     4  0.4933   -0.33476 0.432 0.000 0.000 0.568
#&gt; SRR1274579     4  0.4933   -0.33476 0.432 0.000 0.000 0.568
#&gt; SRR1274580     4  0.4933   -0.33476 0.432 0.000 0.000 0.568
#&gt; SRR1274581     4  0.3464    0.21181 0.076 0.000 0.056 0.868
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.3730     0.6991 0.000 0.288 0.000 0.712 0.000
#&gt; SRR1274530     4  0.3857     0.6806 0.000 0.312 0.000 0.688 0.000
#&gt; SRR1274531     5  0.4452     0.3106 0.000 0.000 0.496 0.004 0.500
#&gt; SRR1274532     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.3573     0.8353 0.000 0.036 0.152 0.000 0.812
#&gt; SRR1274534     5  0.3003     0.7305 0.000 0.188 0.000 0.000 0.812
#&gt; SRR1274535     5  0.3667     0.8317 0.000 0.048 0.140 0.000 0.812
#&gt; SRR1274536     4  0.3730     0.6832 0.000 0.000 0.288 0.712 0.000
#&gt; SRR1274537     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0404     0.8971 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1274539     5  0.3003     0.7305 0.000 0.188 0.000 0.000 0.812
#&gt; SRR1274540     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     4  0.3895     0.6693 0.000 0.320 0.000 0.680 0.000
#&gt; SRR1274546     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.3684     0.4436 0.000 0.720 0.000 0.280 0.000
#&gt; SRR1274548     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     3  0.0880     0.8508 0.000 0.000 0.968 0.032 0.000
#&gt; SRR1274550     5  0.3003     0.8298 0.000 0.000 0.188 0.000 0.812
#&gt; SRR1274551     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.3003     0.8298 0.000 0.000 0.188 0.000 0.812
#&gt; SRR1274553     5  0.3003     0.8298 0.000 0.000 0.188 0.000 0.812
#&gt; SRR1274554     3  0.2149     0.8001 0.000 0.048 0.916 0.000 0.036
#&gt; SRR1274555     3  0.0000     0.8656 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     3  0.0000     0.8656 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274557     3  0.0000     0.8656 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274558     1  0.4171     0.1924 0.604 0.396 0.000 0.000 0.000
#&gt; SRR1274559     1  0.0000     0.7347 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000     0.7347 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.3752     0.3861 0.708 0.000 0.292 0.000 0.000
#&gt; SRR1274562     3  0.3006     0.7484 0.156 0.000 0.836 0.004 0.004
#&gt; SRR1274563     3  0.0000     0.8656 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274564     4  0.3730     0.6832 0.000 0.000 0.288 0.712 0.000
#&gt; SRR1274565     4  0.5199     0.6556 0.000 0.072 0.292 0.636 0.000
#&gt; SRR1274566     4  0.3730     0.6832 0.000 0.000 0.288 0.712 0.000
#&gt; SRR1274567     4  0.3774     0.6775 0.000 0.000 0.296 0.704 0.000
#&gt; SRR1274568     2  0.4283     0.1339 0.456 0.544 0.000 0.000 0.000
#&gt; SRR1274569     1  0.0000     0.7347 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000     0.7347 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000     0.7347 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.4948     0.6545 0.676 0.000 0.000 0.256 0.068
#&gt; SRR1274573     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0162     0.9044 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1274575     4  0.3837     0.6850 0.000 0.308 0.000 0.692 0.000
#&gt; SRR1274576     2  0.0000     0.9080 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274577     2  0.7492     0.0744 0.064 0.460 0.000 0.288 0.188
#&gt; SRR1274578     1  0.6284     0.5943 0.524 0.000 0.000 0.288 0.188
#&gt; SRR1274579     1  0.6284     0.5943 0.524 0.000 0.000 0.288 0.188
#&gt; SRR1274580     1  0.6284     0.5943 0.524 0.000 0.000 0.288 0.188
#&gt; SRR1274581     3  0.7505     0.2773 0.108 0.000 0.484 0.284 0.124
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.2020     0.8297 0.000 0.096 0.000 0.896 0.000 0.008
#&gt; SRR1274530     4  0.3298     0.7465 0.000 0.236 0.000 0.756 0.000 0.008
#&gt; SRR1274531     3  0.4169     0.2104 0.000 0.000 0.532 0.000 0.456 0.012
#&gt; SRR1274532     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.0260     0.9834 0.000 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1274534     5  0.0891     0.9644 0.000 0.024 0.000 0.000 0.968 0.008
#&gt; SRR1274535     5  0.0146     0.9828 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1274536     4  0.2020     0.8142 0.000 0.000 0.096 0.896 0.000 0.008
#&gt; SRR1274537     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0260     0.9380 0.000 0.992 0.000 0.000 0.008 0.000
#&gt; SRR1274539     5  0.0806     0.9692 0.000 0.020 0.000 0.000 0.972 0.008
#&gt; SRR1274540     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0146     0.9411 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1274544     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     4  0.3323     0.7421 0.000 0.240 0.000 0.752 0.000 0.008
#&gt; SRR1274546     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.3103     0.6584 0.000 0.784 0.000 0.208 0.000 0.008
#&gt; SRR1274548     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274549     3  0.3465     0.7426 0.000 0.000 0.804 0.156 0.016 0.024
#&gt; SRR1274550     5  0.0146     0.9828 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1274551     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.0260     0.9834 0.000 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1274553     5  0.0260     0.9834 0.000 0.000 0.000 0.000 0.992 0.008
#&gt; SRR1274554     3  0.2526     0.7594 0.000 0.004 0.876 0.096 0.000 0.024
#&gt; SRR1274555     3  0.0806     0.8422 0.000 0.000 0.972 0.000 0.020 0.008
#&gt; SRR1274556     3  0.0909     0.8407 0.000 0.000 0.968 0.000 0.020 0.012
#&gt; SRR1274557     3  0.0458     0.8421 0.000 0.000 0.984 0.000 0.016 0.000
#&gt; SRR1274558     1  0.1663     0.7962 0.912 0.088 0.000 0.000 0.000 0.000
#&gt; SRR1274559     1  0.0000     0.8898 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000     0.8898 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.1738     0.8417 0.928 0.000 0.052 0.004 0.000 0.016
#&gt; SRR1274562     3  0.3862     0.7199 0.108 0.000 0.792 0.000 0.012 0.088
#&gt; SRR1274563     3  0.0717     0.8423 0.000 0.000 0.976 0.000 0.016 0.008
#&gt; SRR1274564     4  0.2020     0.8142 0.000 0.000 0.096 0.896 0.000 0.008
#&gt; SRR1274565     4  0.2703     0.7677 0.000 0.028 0.080 0.876 0.000 0.016
#&gt; SRR1274566     4  0.0547     0.8068 0.000 0.000 0.020 0.980 0.000 0.000
#&gt; SRR1274567     4  0.1863     0.8117 0.000 0.000 0.104 0.896 0.000 0.000
#&gt; SRR1274568     2  0.5418     0.1018 0.416 0.504 0.008 0.060 0.000 0.012
#&gt; SRR1274569     1  0.0000     0.8898 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000     0.8898 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000     0.8898 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.3864    -0.0504 0.520 0.000 0.000 0.000 0.000 0.480
#&gt; SRR1274573     2  0.0000     0.9436 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0146     0.9408 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1274575     4  0.2743     0.8030 0.000 0.164 0.000 0.828 0.000 0.008
#&gt; SRR1274576     2  0.1732     0.8704 0.000 0.920 0.004 0.072 0.000 0.004
#&gt; SRR1274577     6  0.3351     0.8008 0.004 0.040 0.020 0.096 0.000 0.840
#&gt; SRR1274578     6  0.1075     0.8764 0.048 0.000 0.000 0.000 0.000 0.952
#&gt; SRR1274579     6  0.1267     0.8763 0.060 0.000 0.000 0.000 0.000 0.940
#&gt; SRR1274580     6  0.1387     0.8726 0.068 0.000 0.000 0.000 0.000 0.932
#&gt; SRR1274581     6  0.5279     0.6539 0.100 0.000 0.168 0.052 0.000 0.680
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.902           0.958       0.975         0.4372 0.560   0.560
#> 3 3 0.923           0.932       0.980         0.0447 0.989   0.980
#> 4 4 0.812           0.898       0.929         0.1296 0.956   0.920
#> 5 5 0.661           0.771       0.909         0.0968 0.922   0.847
#> 6 6 0.721           0.819       0.915         0.1253 0.949   0.883
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.977 0.000 1.000
#&gt; SRR1274529     2   0.000      0.977 0.000 1.000
#&gt; SRR1274530     2   0.000      0.977 0.000 1.000
#&gt; SRR1274531     2   0.000      0.977 0.000 1.000
#&gt; SRR1274532     2   0.000      0.977 0.000 1.000
#&gt; SRR1274533     2   0.000      0.977 0.000 1.000
#&gt; SRR1274534     2   0.000      0.977 0.000 1.000
#&gt; SRR1274535     2   0.000      0.977 0.000 1.000
#&gt; SRR1274536     2   0.518      0.879 0.116 0.884
#&gt; SRR1274537     2   0.000      0.977 0.000 1.000
#&gt; SRR1274538     2   0.000      0.977 0.000 1.000
#&gt; SRR1274539     2   0.000      0.977 0.000 1.000
#&gt; SRR1274540     2   0.000      0.977 0.000 1.000
#&gt; SRR1274541     2   0.000      0.977 0.000 1.000
#&gt; SRR1274542     2   0.000      0.977 0.000 1.000
#&gt; SRR1274543     2   0.000      0.977 0.000 1.000
#&gt; SRR1274544     2   0.000      0.977 0.000 1.000
#&gt; SRR1274545     2   0.000      0.977 0.000 1.000
#&gt; SRR1274546     2   0.000      0.977 0.000 1.000
#&gt; SRR1274547     2   0.000      0.977 0.000 1.000
#&gt; SRR1274548     2   0.000      0.977 0.000 1.000
#&gt; SRR1274549     2   0.795      0.705 0.240 0.760
#&gt; SRR1274550     1   0.141      0.982 0.980 0.020
#&gt; SRR1274551     2   0.000      0.977 0.000 1.000
#&gt; SRR1274552     1   0.141      0.982 0.980 0.020
#&gt; SRR1274553     1   0.141      0.982 0.980 0.020
#&gt; SRR1274554     2   0.000      0.977 0.000 1.000
#&gt; SRR1274555     1   0.141      0.982 0.980 0.020
#&gt; SRR1274556     1   0.141      0.982 0.980 0.020
#&gt; SRR1274557     1   0.141      0.982 0.980 0.020
#&gt; SRR1274558     2   0.000      0.977 0.000 1.000
#&gt; SRR1274559     2   0.373      0.923 0.072 0.928
#&gt; SRR1274560     2   0.373      0.923 0.072 0.928
#&gt; SRR1274561     1   0.844      0.636 0.728 0.272
#&gt; SRR1274562     1   0.141      0.982 0.980 0.020
#&gt; SRR1274563     1   0.141      0.982 0.980 0.020
#&gt; SRR1274564     2   0.518      0.879 0.116 0.884
#&gt; SRR1274565     2   0.000      0.977 0.000 1.000
#&gt; SRR1274566     2   0.443      0.904 0.092 0.908
#&gt; SRR1274567     2   0.443      0.904 0.092 0.908
#&gt; SRR1274568     2   0.000      0.977 0.000 1.000
#&gt; SRR1274569     1   0.163      0.978 0.976 0.024
#&gt; SRR1274570     1   0.141      0.982 0.980 0.020
#&gt; SRR1274571     1   0.141      0.982 0.980 0.020
#&gt; SRR1274572     1   0.141      0.982 0.980 0.020
#&gt; SRR1274573     2   0.000      0.977 0.000 1.000
#&gt; SRR1274574     2   0.000      0.977 0.000 1.000
#&gt; SRR1274575     2   0.000      0.977 0.000 1.000
#&gt; SRR1274576     2   0.000      0.977 0.000 1.000
#&gt; SRR1274577     2   0.000      0.977 0.000 1.000
#&gt; SRR1274578     1   0.141      0.982 0.980 0.020
#&gt; SRR1274579     1   0.141      0.982 0.980 0.020
#&gt; SRR1274580     1   0.141      0.982 0.980 0.020
#&gt; SRR1274581     1   0.000      0.963 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274530     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274531     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274532     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274533     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274534     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274535     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274536     2  0.3425      0.869 0.112 0.884 0.004
#&gt; SRR1274537     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274539     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274540     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274546     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274549     2  0.5201      0.691 0.236 0.760 0.004
#&gt; SRR1274550     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274551     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274552     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274553     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274554     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274555     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274556     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274557     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274558     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274559     2  0.2356      0.914 0.072 0.928 0.000
#&gt; SRR1274560     2  0.2356      0.914 0.072 0.928 0.000
#&gt; SRR1274561     1  0.5138      0.499 0.748 0.252 0.000
#&gt; SRR1274562     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274563     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274564     2  0.3425      0.869 0.112 0.884 0.004
#&gt; SRR1274565     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274566     2  0.2945      0.895 0.088 0.908 0.004
#&gt; SRR1274567     2  0.2945      0.895 0.088 0.908 0.004
#&gt; SRR1274568     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274569     1  0.0237      0.964 0.996 0.004 0.000
#&gt; SRR1274570     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274576     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274577     2  0.0000      0.974 0.000 1.000 0.000
#&gt; SRR1274578     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.970 1.000 0.000 0.000
#&gt; SRR1274581     3  0.0000      0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1274528     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274529     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274530     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274531     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274532     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274533     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274534     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274535     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274536     2  0.4282      0.857 0.124 0.816 0.060  0
#&gt; SRR1274537     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274538     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274539     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274540     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274541     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274542     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274543     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274544     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274545     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274546     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274547     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274548     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274549     2  0.5952      0.694 0.124 0.692 0.184  0
#&gt; SRR1274550     3  0.1022      0.991 0.032 0.000 0.968  0
#&gt; SRR1274551     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274552     3  0.1022      0.991 0.032 0.000 0.968  0
#&gt; SRR1274553     3  0.1022      0.991 0.032 0.000 0.968  0
#&gt; SRR1274554     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274555     3  0.1022      0.991 0.032 0.000 0.968  0
#&gt; SRR1274556     3  0.0188      0.947 0.004 0.000 0.996  0
#&gt; SRR1274557     3  0.1022      0.991 0.032 0.000 0.968  0
#&gt; SRR1274558     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274559     2  0.3280      0.891 0.124 0.860 0.016  0
#&gt; SRR1274560     2  0.3280      0.891 0.124 0.860 0.016  0
#&gt; SRR1274561     1  0.7372      0.347 0.524 0.236 0.240  0
#&gt; SRR1274562     1  0.4382      0.693 0.704 0.000 0.296  0
#&gt; SRR1274563     3  0.1022      0.991 0.032 0.000 0.968  0
#&gt; SRR1274564     2  0.4282      0.857 0.124 0.816 0.060  0
#&gt; SRR1274565     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274566     2  0.3821      0.879 0.120 0.840 0.040  0
#&gt; SRR1274567     2  0.3821      0.879 0.120 0.840 0.040  0
#&gt; SRR1274568     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274569     1  0.2589      0.889 0.884 0.000 0.116  0
#&gt; SRR1274570     1  0.2647      0.893 0.880 0.000 0.120  0
#&gt; SRR1274571     1  0.2647      0.893 0.880 0.000 0.120  0
#&gt; SRR1274572     1  0.2647      0.893 0.880 0.000 0.120  0
#&gt; SRR1274573     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274574     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274575     2  0.0000      0.950 0.000 1.000 0.000  0
#&gt; SRR1274576     2  0.0336      0.949 0.008 0.992 0.000  0
#&gt; SRR1274577     2  0.1792      0.938 0.068 0.932 0.000  0
#&gt; SRR1274578     1  0.2647      0.893 0.880 0.000 0.120  0
#&gt; SRR1274579     1  0.2647      0.893 0.880 0.000 0.120  0
#&gt; SRR1274580     1  0.2647      0.893 0.880 0.000 0.120  0
#&gt; SRR1274581     4  0.0000      0.000 0.000 0.000 0.000  1
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR1274528     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274529     2  0.0162      0.896 0.000 0.996 0.000 0.004  0
#&gt; SRR1274530     2  0.0162      0.896 0.000 0.996 0.000 0.004  0
#&gt; SRR1274531     2  0.2674      0.806 0.004 0.856 0.000 0.140  0
#&gt; SRR1274532     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274533     2  0.2179      0.851 0.004 0.896 0.000 0.100  0
#&gt; SRR1274534     2  0.2124      0.853 0.004 0.900 0.000 0.096  0
#&gt; SRR1274535     2  0.2124      0.853 0.004 0.900 0.000 0.096  0
#&gt; SRR1274536     4  0.4307      0.381 0.000 0.500 0.000 0.500  0
#&gt; SRR1274537     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274538     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274539     2  0.2124      0.853 0.004 0.900 0.000 0.096  0
#&gt; SRR1274540     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274541     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274542     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274543     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274544     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274545     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274546     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274547     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274548     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274549     4  0.5236      0.490 0.000 0.380 0.052 0.568  0
#&gt; SRR1274550     3  0.0000      0.997 0.000 0.000 1.000 0.000  0
#&gt; SRR1274551     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274552     3  0.0000      0.997 0.000 0.000 1.000 0.000  0
#&gt; SRR1274553     3  0.0000      0.997 0.000 0.000 1.000 0.000  0
#&gt; SRR1274554     2  0.2124      0.853 0.004 0.900 0.000 0.096  0
#&gt; SRR1274555     3  0.0162      0.997 0.000 0.000 0.996 0.004  0
#&gt; SRR1274556     4  0.4287     -0.603 0.000 0.000 0.460 0.540  0
#&gt; SRR1274557     3  0.0162      0.997 0.000 0.000 0.996 0.004  0
#&gt; SRR1274558     2  0.1892      0.862 0.004 0.916 0.000 0.080  0
#&gt; SRR1274559     2  0.3840      0.732 0.076 0.808 0.000 0.116  0
#&gt; SRR1274560     2  0.3840      0.732 0.076 0.808 0.000 0.116  0
#&gt; SRR1274561     1  0.7075      0.280 0.536 0.200 0.212 0.052  0
#&gt; SRR1274562     1  0.3934      0.568 0.716 0.000 0.276 0.008  0
#&gt; SRR1274563     3  0.0162      0.997 0.000 0.000 0.996 0.004  0
#&gt; SRR1274564     4  0.4307      0.381 0.000 0.500 0.000 0.500  0
#&gt; SRR1274565     2  0.2674      0.806 0.004 0.856 0.000 0.140  0
#&gt; SRR1274566     2  0.4074      0.078 0.000 0.636 0.000 0.364  0
#&gt; SRR1274567     2  0.4074      0.078 0.000 0.636 0.000 0.364  0
#&gt; SRR1274568     2  0.2124      0.853 0.004 0.900 0.000 0.096  0
#&gt; SRR1274569     1  0.0000      0.871 1.000 0.000 0.000 0.000  0
#&gt; SRR1274570     1  0.0162      0.875 0.996 0.000 0.004 0.000  0
#&gt; SRR1274571     1  0.0162      0.875 0.996 0.000 0.004 0.000  0
#&gt; SRR1274572     1  0.0162      0.875 0.996 0.000 0.004 0.000  0
#&gt; SRR1274573     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274574     2  0.0000      0.899 0.000 1.000 0.000 0.000  0
#&gt; SRR1274575     2  0.0162      0.896 0.000 0.996 0.000 0.004  0
#&gt; SRR1274576     2  0.0955      0.887 0.004 0.968 0.000 0.028  0
#&gt; SRR1274577     2  0.2124      0.853 0.004 0.900 0.000 0.096  0
#&gt; SRR1274578     1  0.0162      0.875 0.996 0.000 0.004 0.000  0
#&gt; SRR1274579     1  0.0162      0.875 0.996 0.000 0.004 0.000  0
#&gt; SRR1274580     1  0.0162      0.875 0.996 0.000 0.004 0.000  0
#&gt; SRR1274581     5  0.0000      0.000 0.000 0.000 0.000 0.000  1
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1274528     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274529     2  0.1204      0.866 0.000 0.944 0.000 0.056 0.000  0
#&gt; SRR1274530     2  0.1204      0.866 0.000 0.944 0.000 0.056 0.000  0
#&gt; SRR1274531     2  0.4046      0.793 0.000 0.748 0.000 0.168 0.084  0
#&gt; SRR1274532     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274533     2  0.3509      0.842 0.000 0.804 0.000 0.112 0.084  0
#&gt; SRR1274534     2  0.3419      0.846 0.000 0.812 0.000 0.104 0.084  0
#&gt; SRR1274535     2  0.3419      0.846 0.000 0.812 0.000 0.104 0.084  0
#&gt; SRR1274536     4  0.1531      0.769 0.000 0.068 0.000 0.928 0.004  0
#&gt; SRR1274537     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274538     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274539     2  0.3419      0.846 0.000 0.812 0.000 0.104 0.084  0
#&gt; SRR1274540     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274541     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274542     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274543     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274544     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274545     2  0.0937      0.877 0.000 0.960 0.000 0.040 0.000  0
#&gt; SRR1274546     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274547     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274548     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274549     4  0.2510      0.600 0.000 0.000 0.028 0.872 0.100  0
#&gt; SRR1274550     3  0.0000      0.992 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1274551     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274552     3  0.0000      0.992 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1274553     3  0.0000      0.992 0.000 0.000 1.000 0.000 0.000  0
#&gt; SRR1274554     2  0.3419      0.846 0.000 0.812 0.000 0.104 0.084  0
#&gt; SRR1274555     3  0.0363      0.992 0.000 0.000 0.988 0.000 0.012  0
#&gt; SRR1274556     5  0.1802      0.000 0.000 0.000 0.072 0.012 0.916  0
#&gt; SRR1274557     3  0.0363      0.992 0.000 0.000 0.988 0.000 0.012  0
#&gt; SRR1274558     2  0.3125      0.857 0.000 0.836 0.000 0.080 0.084  0
#&gt; SRR1274559     2  0.4809      0.781 0.068 0.736 0.000 0.112 0.084  0
#&gt; SRR1274560     2  0.4809      0.781 0.068 0.736 0.000 0.112 0.084  0
#&gt; SRR1274561     1  0.6654      0.246 0.528 0.196 0.212 0.052 0.012  0
#&gt; SRR1274562     1  0.3652      0.553 0.720 0.000 0.264 0.000 0.016  0
#&gt; SRR1274563     3  0.0363      0.992 0.000 0.000 0.988 0.000 0.012  0
#&gt; SRR1274564     4  0.1531      0.769 0.000 0.068 0.000 0.928 0.004  0
#&gt; SRR1274565     2  0.4046      0.793 0.000 0.748 0.000 0.168 0.084  0
#&gt; SRR1274566     4  0.2793      0.719 0.000 0.200 0.000 0.800 0.000  0
#&gt; SRR1274567     4  0.2793      0.719 0.000 0.200 0.000 0.800 0.000  0
#&gt; SRR1274568     2  0.3419      0.846 0.000 0.812 0.000 0.104 0.084  0
#&gt; SRR1274569     1  0.0146      0.872 0.996 0.000 0.000 0.000 0.004  0
#&gt; SRR1274570     1  0.0000      0.875 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1274571     1  0.0000      0.875 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1274572     1  0.0000      0.875 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1274573     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274574     2  0.0000      0.901 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274575     2  0.1204      0.866 0.000 0.944 0.000 0.056 0.000  0
#&gt; SRR1274576     2  0.2511      0.872 0.000 0.880 0.000 0.064 0.056  0
#&gt; SRR1274577     2  0.3419      0.846 0.000 0.812 0.000 0.104 0.084  0
#&gt; SRR1274578     1  0.0000      0.875 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1274579     1  0.0000      0.875 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1274580     1  0.0000      0.875 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1274581     6  0.0000      0.000 0.000 0.000 0.000 0.000 0.000  1
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.983       0.990         0.4783 0.525   0.525
#> 3 3 0.517           0.249       0.660         0.3028 0.900   0.817
#> 4 4 0.612           0.657       0.791         0.1507 0.708   0.434
#> 5 5 0.767           0.748       0.837         0.0761 0.867   0.563
#> 6 6 0.809           0.687       0.806         0.0443 0.957   0.801
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274529     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274530     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274531     2  0.3733      0.938 0.072 0.928
#&gt; SRR1274532     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274533     2  0.1843      0.967 0.028 0.972
#&gt; SRR1274534     2  0.0376      0.981 0.004 0.996
#&gt; SRR1274535     2  0.3733      0.938 0.072 0.928
#&gt; SRR1274536     2  0.3733      0.938 0.072 0.928
#&gt; SRR1274537     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274538     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274539     2  0.0376      0.981 0.004 0.996
#&gt; SRR1274540     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274541     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274542     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274543     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274544     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274545     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274546     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274547     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274548     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274549     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274550     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274551     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274552     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274553     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274554     2  0.3733      0.938 0.072 0.928
#&gt; SRR1274555     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274556     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274557     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274558     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274559     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274560     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274561     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274562     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274563     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274564     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274565     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274566     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274567     2  0.4562      0.914 0.096 0.904
#&gt; SRR1274568     2  0.3733      0.938 0.072 0.928
#&gt; SRR1274569     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274570     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274571     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274572     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274573     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274574     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274575     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274576     2  0.0000      0.983 0.000 1.000
#&gt; SRR1274577     2  0.3733      0.938 0.072 0.928
#&gt; SRR1274578     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274579     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274580     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274581     1  0.0000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274529     3   0.628     1.0000 0.000 0.460 0.540
#&gt; SRR1274530     3   0.628     1.0000 0.000 0.460 0.540
#&gt; SRR1274531     2   0.826     0.2115 0.180 0.636 0.184
#&gt; SRR1274532     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274533     2   0.472     0.2901 0.160 0.824 0.016
#&gt; SRR1274534     2   0.457     0.2892 0.160 0.828 0.012
#&gt; SRR1274535     2   0.517     0.2805 0.192 0.792 0.016
#&gt; SRR1274536     2   0.807     0.1979 0.160 0.652 0.188
#&gt; SRR1274537     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274538     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274539     2   0.457     0.2892 0.160 0.828 0.012
#&gt; SRR1274540     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274541     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274542     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274543     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274544     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274545     2   0.621    -0.6009 0.000 0.572 0.428
#&gt; SRR1274546     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274547     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274548     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274549     1   0.853     0.4401 0.604 0.240 0.156
#&gt; SRR1274550     1   0.186     0.7533 0.948 0.052 0.000
#&gt; SRR1274551     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274552     1   0.364     0.7140 0.872 0.124 0.004
#&gt; SRR1274553     1   0.210     0.7539 0.944 0.052 0.004
#&gt; SRR1274554     2   0.472     0.2901 0.160 0.824 0.016
#&gt; SRR1274555     1   0.000     0.7672 1.000 0.000 0.000
#&gt; SRR1274556     1   0.165     0.7598 0.960 0.004 0.036
#&gt; SRR1274557     1   0.341     0.7136 0.876 0.124 0.000
#&gt; SRR1274558     2   0.304    -0.0522 0.000 0.896 0.104
#&gt; SRR1274559     2   0.965    -0.4098 0.380 0.412 0.208
#&gt; SRR1274560     1   0.990     0.4610 0.380 0.352 0.268
#&gt; SRR1274561     1   0.645     0.7128 0.760 0.152 0.088
#&gt; SRR1274562     1   0.475     0.7738 0.784 0.000 0.216
#&gt; SRR1274563     1   0.000     0.7672 1.000 0.000 0.000
#&gt; SRR1274564     2   0.435     0.0598 0.000 0.816 0.184
#&gt; SRR1274565     2   0.429     0.0588 0.000 0.820 0.180
#&gt; SRR1274566     2   0.435     0.0598 0.000 0.816 0.184
#&gt; SRR1274567     2   0.812     0.1971 0.164 0.648 0.188
#&gt; SRR1274568     2   0.434     0.2795 0.136 0.848 0.016
#&gt; SRR1274569     1   0.617     0.7651 0.588 0.000 0.412
#&gt; SRR1274570     1   0.617     0.7651 0.588 0.000 0.412
#&gt; SRR1274571     1   0.617     0.7651 0.588 0.000 0.412
#&gt; SRR1274572     1   0.617     0.7651 0.588 0.000 0.412
#&gt; SRR1274573     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274574     2   0.595    -0.3152 0.000 0.640 0.360
#&gt; SRR1274575     3   0.628     1.0000 0.000 0.460 0.540
#&gt; SRR1274576     2   0.599    -0.3188 0.000 0.632 0.368
#&gt; SRR1274577     2   0.472     0.2901 0.160 0.824 0.016
#&gt; SRR1274578     1   0.617     0.7651 0.588 0.000 0.412
#&gt; SRR1274579     1   0.617     0.7651 0.588 0.000 0.412
#&gt; SRR1274580     1   0.617     0.7651 0.588 0.000 0.412
#&gt; SRR1274581     1   0.493     0.7641 0.768 0.000 0.232
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.5268    0.45149 0.000 0.592 0.012 0.396
#&gt; SRR1274530     2  0.5268    0.45149 0.000 0.592 0.012 0.396
#&gt; SRR1274531     4  0.6524    0.61049 0.004 0.092 0.296 0.608
#&gt; SRR1274532     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274533     4  0.7869    0.64776 0.004 0.228 0.348 0.420
#&gt; SRR1274534     4  0.7723    0.64645 0.000 0.232 0.348 0.420
#&gt; SRR1274535     4  0.7763    0.62244 0.004 0.200 0.376 0.420
#&gt; SRR1274536     4  0.2998    0.54596 0.004 0.080 0.024 0.892
#&gt; SRR1274537     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274539     4  0.7723    0.64645 0.000 0.232 0.348 0.420
#&gt; SRR1274540     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.3377    0.75093 0.000 0.848 0.012 0.140
#&gt; SRR1274546     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0804    0.87201 0.000 0.980 0.012 0.008
#&gt; SRR1274548     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274549     3  0.5980    0.43759 0.044 0.000 0.560 0.396
#&gt; SRR1274550     3  0.3217    0.79571 0.128 0.000 0.860 0.012
#&gt; SRR1274551     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.2699    0.73033 0.068 0.000 0.904 0.028
#&gt; SRR1274553     3  0.3653    0.78819 0.128 0.000 0.844 0.028
#&gt; SRR1274554     4  0.7869    0.64776 0.004 0.228 0.348 0.420
#&gt; SRR1274555     3  0.4391    0.71171 0.252 0.000 0.740 0.008
#&gt; SRR1274556     3  0.4327    0.71616 0.216 0.000 0.768 0.016
#&gt; SRR1274557     3  0.3217    0.79665 0.128 0.000 0.860 0.012
#&gt; SRR1274558     2  0.6694   -0.14122 0.004 0.560 0.088 0.348
#&gt; SRR1274559     4  0.8029    0.35840 0.332 0.016 0.200 0.452
#&gt; SRR1274560     4  0.7755    0.29538 0.368 0.004 0.200 0.428
#&gt; SRR1274561     1  0.7723   -0.13536 0.420 0.000 0.348 0.232
#&gt; SRR1274562     1  0.5294   -0.10969 0.508 0.000 0.484 0.008
#&gt; SRR1274563     3  0.4391    0.71171 0.252 0.000 0.740 0.008
#&gt; SRR1274564     4  0.2859    0.54402 0.000 0.112 0.008 0.880
#&gt; SRR1274565     4  0.2888    0.55049 0.000 0.124 0.004 0.872
#&gt; SRR1274566     4  0.2983    0.54535 0.004 0.108 0.008 0.880
#&gt; SRR1274567     4  0.2998    0.54596 0.004 0.080 0.024 0.892
#&gt; SRR1274568     4  0.7815    0.64386 0.004 0.232 0.312 0.452
#&gt; SRR1274569     1  0.0921    0.77701 0.972 0.000 0.000 0.028
#&gt; SRR1274570     1  0.0921    0.77701 0.972 0.000 0.000 0.028
#&gt; SRR1274571     1  0.0921    0.77701 0.972 0.000 0.000 0.028
#&gt; SRR1274572     1  0.0000    0.77909 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000    0.88549 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.5268    0.45149 0.000 0.592 0.012 0.396
#&gt; SRR1274576     2  0.0779    0.86697 0.000 0.980 0.004 0.016
#&gt; SRR1274577     4  0.7869    0.64776 0.004 0.228 0.348 0.420
#&gt; SRR1274578     1  0.0336    0.77922 0.992 0.000 0.008 0.000
#&gt; SRR1274579     1  0.0336    0.77922 0.992 0.000 0.008 0.000
#&gt; SRR1274580     1  0.0336    0.77922 0.992 0.000 0.008 0.000
#&gt; SRR1274581     1  0.6134    0.00849 0.508 0.000 0.444 0.048
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.5900      0.359 0.000 0.448 0.076 0.468 0.008
#&gt; SRR1274530     4  0.5900      0.359 0.000 0.448 0.076 0.468 0.008
#&gt; SRR1274531     5  0.4026      0.587 0.000 0.020 0.000 0.244 0.736
#&gt; SRR1274532     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.1956      0.798 0.000 0.076 0.008 0.000 0.916
#&gt; SRR1274534     5  0.1956      0.798 0.000 0.076 0.008 0.000 0.916
#&gt; SRR1274535     5  0.1800      0.778 0.000 0.048 0.020 0.000 0.932
#&gt; SRR1274536     4  0.3841      0.646 0.000 0.032 0.012 0.808 0.148
#&gt; SRR1274537     2  0.0162      0.965 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1274538     2  0.0162      0.965 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1274539     5  0.1956      0.798 0.000 0.076 0.008 0.000 0.916
#&gt; SRR1274540     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0162      0.965 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.3466      0.755 0.000 0.844 0.048 0.100 0.008
#&gt; SRR1274546     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0798      0.944 0.000 0.976 0.016 0.000 0.008
#&gt; SRR1274548     2  0.0162      0.965 0.000 0.996 0.004 0.000 0.000
#&gt; SRR1274549     3  0.5613      0.352 0.004 0.000 0.520 0.412 0.064
#&gt; SRR1274550     3  0.3913      0.735 0.032 0.000 0.824 0.036 0.108
#&gt; SRR1274551     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.5368      0.590 0.016 0.000 0.632 0.048 0.304
#&gt; SRR1274553     3  0.5619      0.612 0.032 0.000 0.632 0.048 0.288
#&gt; SRR1274554     5  0.1956      0.798 0.000 0.076 0.008 0.000 0.916
#&gt; SRR1274555     3  0.2351      0.734 0.088 0.000 0.896 0.000 0.016
#&gt; SRR1274556     3  0.2541      0.734 0.068 0.000 0.900 0.020 0.012
#&gt; SRR1274557     3  0.2740      0.740 0.028 0.000 0.876 0.000 0.096
#&gt; SRR1274558     5  0.5215      0.294 0.000 0.444 0.008 0.028 0.520
#&gt; SRR1274559     5  0.6688      0.410 0.244 0.000 0.016 0.212 0.528
#&gt; SRR1274560     5  0.6660      0.392 0.264 0.000 0.016 0.192 0.528
#&gt; SRR1274561     3  0.7651      0.365 0.236 0.000 0.444 0.252 0.068
#&gt; SRR1274562     3  0.4322      0.583 0.260 0.000 0.716 0.012 0.012
#&gt; SRR1274563     3  0.2351      0.734 0.088 0.000 0.896 0.000 0.016
#&gt; SRR1274564     4  0.3608      0.653 0.000 0.040 0.000 0.812 0.148
#&gt; SRR1274565     4  0.3994      0.618 0.000 0.040 0.000 0.772 0.188
#&gt; SRR1274566     4  0.3608      0.653 0.000 0.040 0.000 0.812 0.148
#&gt; SRR1274567     4  0.3841      0.646 0.000 0.032 0.012 0.808 0.148
#&gt; SRR1274568     5  0.3058      0.779 0.008 0.076 0.004 0.036 0.876
#&gt; SRR1274569     1  0.2321      0.920 0.912 0.000 0.008 0.056 0.024
#&gt; SRR1274570     1  0.2251      0.921 0.916 0.000 0.008 0.052 0.024
#&gt; SRR1274571     1  0.2321      0.920 0.912 0.000 0.008 0.056 0.024
#&gt; SRR1274572     1  0.0404      0.938 0.988 0.000 0.012 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.5900      0.359 0.000 0.448 0.076 0.468 0.008
#&gt; SRR1274576     2  0.3398      0.660 0.000 0.780 0.004 0.000 0.216
#&gt; SRR1274577     5  0.1956      0.798 0.000 0.076 0.008 0.000 0.916
#&gt; SRR1274578     1  0.0968      0.936 0.972 0.000 0.012 0.012 0.004
#&gt; SRR1274579     1  0.0968      0.936 0.972 0.000 0.012 0.012 0.004
#&gt; SRR1274580     1  0.0968      0.936 0.972 0.000 0.012 0.012 0.004
#&gt; SRR1274581     3  0.7030      0.297 0.324 0.000 0.484 0.152 0.040
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000     0.9453 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.6256     0.4406 0.000 0.292 0.004 0.428 0.004 0.272
#&gt; SRR1274530     4  0.6256     0.4406 0.000 0.292 0.004 0.428 0.004 0.272
#&gt; SRR1274531     5  0.3929     0.3814 0.000 0.000 0.000 0.272 0.700 0.028
#&gt; SRR1274532     2  0.0000     0.9453 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.0405     0.8048 0.000 0.008 0.004 0.000 0.988 0.000
#&gt; SRR1274534     5  0.0405     0.8048 0.000 0.008 0.004 0.000 0.988 0.000
#&gt; SRR1274535     5  0.0405     0.8010 0.000 0.004 0.008 0.000 0.988 0.000
#&gt; SRR1274536     4  0.1606     0.5840 0.000 0.004 0.000 0.932 0.056 0.008
#&gt; SRR1274537     2  0.0291     0.9425 0.000 0.992 0.004 0.000 0.000 0.004
#&gt; SRR1274538     2  0.0405     0.9417 0.000 0.988 0.004 0.000 0.000 0.008
#&gt; SRR1274539     5  0.0405     0.8048 0.000 0.008 0.004 0.000 0.988 0.000
#&gt; SRR1274540     2  0.0000     0.9453 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9453 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9453 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0405     0.9417 0.000 0.988 0.004 0.000 0.000 0.008
#&gt; SRR1274544     2  0.0000     0.9453 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.4098     0.6353 0.000 0.732 0.008 0.032 0.004 0.224
#&gt; SRR1274546     2  0.0000     0.9453 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.1493     0.8960 0.000 0.936 0.004 0.000 0.004 0.056
#&gt; SRR1274548     2  0.0405     0.9417 0.000 0.988 0.004 0.000 0.000 0.008
#&gt; SRR1274549     4  0.4389    -0.0685 0.000 0.000 0.444 0.536 0.012 0.008
#&gt; SRR1274550     3  0.4115     0.7587 0.016 0.000 0.796 0.020 0.064 0.104
#&gt; SRR1274551     2  0.0000     0.9453 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.6113     0.5824 0.016 0.000 0.564 0.020 0.256 0.144
#&gt; SRR1274553     3  0.6116     0.5997 0.020 0.000 0.576 0.020 0.240 0.144
#&gt; SRR1274554     5  0.0972     0.7984 0.000 0.008 0.000 0.000 0.964 0.028
#&gt; SRR1274555     3  0.0632     0.8037 0.024 0.000 0.976 0.000 0.000 0.000
#&gt; SRR1274556     3  0.1026     0.7974 0.008 0.000 0.968 0.012 0.008 0.004
#&gt; SRR1274557     3  0.1151     0.8032 0.012 0.000 0.956 0.000 0.032 0.000
#&gt; SRR1274558     5  0.5998     0.0948 0.008 0.428 0.004 0.016 0.448 0.096
#&gt; SRR1274559     6  0.7344     0.6894 0.116 0.000 0.008 0.164 0.316 0.396
#&gt; SRR1274560     6  0.7351     0.6898 0.120 0.000 0.008 0.160 0.316 0.396
#&gt; SRR1274561     6  0.7416     0.3699 0.104 0.000 0.288 0.212 0.008 0.388
#&gt; SRR1274562     3  0.3078     0.6789 0.108 0.000 0.836 0.000 0.000 0.056
#&gt; SRR1274563     3  0.0632     0.8037 0.024 0.000 0.976 0.000 0.000 0.000
#&gt; SRR1274564     4  0.1606     0.5872 0.000 0.004 0.000 0.932 0.056 0.008
#&gt; SRR1274565     4  0.2804     0.5164 0.000 0.004 0.000 0.852 0.120 0.024
#&gt; SRR1274566     4  0.1349     0.5872 0.000 0.004 0.000 0.940 0.056 0.000
#&gt; SRR1274567     4  0.1349     0.5872 0.000 0.004 0.000 0.940 0.056 0.000
#&gt; SRR1274568     5  0.2742     0.7232 0.016 0.008 0.000 0.020 0.880 0.076
#&gt; SRR1274569     1  0.3774     0.5220 0.664 0.000 0.008 0.000 0.000 0.328
#&gt; SRR1274570     1  0.3758     0.5259 0.668 0.000 0.008 0.000 0.000 0.324
#&gt; SRR1274571     1  0.3774     0.5220 0.664 0.000 0.008 0.000 0.000 0.328
#&gt; SRR1274572     1  0.1616     0.6909 0.932 0.000 0.020 0.000 0.000 0.048
#&gt; SRR1274573     2  0.0146     0.9440 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0146     0.9440 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR1274575     4  0.6256     0.4406 0.000 0.292 0.004 0.428 0.004 0.272
#&gt; SRR1274576     2  0.4255     0.3044 0.000 0.600 0.004 0.000 0.380 0.016
#&gt; SRR1274577     5  0.0972     0.7984 0.000 0.008 0.000 0.000 0.964 0.028
#&gt; SRR1274578     1  0.0547     0.6969 0.980 0.000 0.020 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0547     0.6969 0.980 0.000 0.020 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0547     0.6969 0.980 0.000 0.020 0.000 0.000 0.000
#&gt; SRR1274581     1  0.6970    -0.0270 0.392 0.000 0.336 0.076 0.000 0.196
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.967       0.986         0.5092 0.491   0.491
#> 3 3 0.673           0.659       0.827         0.2770 0.837   0.678
#> 4 4 0.824           0.861       0.939         0.1388 0.820   0.544
#> 5 5 0.882           0.846       0.925         0.0659 0.911   0.676
#> 6 6 0.862           0.783       0.890         0.0315 0.945   0.759
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274529     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274530     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274531     1  0.5946      0.830 0.856 0.144
#&gt; SRR1274532     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274533     2  0.1414      0.979 0.020 0.980
#&gt; SRR1274534     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274535     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274536     1  0.4431      0.890 0.908 0.092
#&gt; SRR1274537     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274538     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274539     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274540     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274541     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274542     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274543     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274544     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274545     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274546     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274547     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274548     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274549     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274550     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274551     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274552     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274553     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274554     1  0.9850      0.260 0.572 0.428
#&gt; SRR1274555     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274556     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274557     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274558     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274559     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274560     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274561     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274562     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274563     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274564     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274565     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274566     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274567     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274568     1  0.2948      0.930 0.948 0.052
#&gt; SRR1274569     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274570     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274571     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274572     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274573     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274574     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274575     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274576     2  0.0000      0.999 0.000 1.000
#&gt; SRR1274577     1  0.0376      0.969 0.996 0.004
#&gt; SRR1274578     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274579     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274580     1  0.0000      0.972 1.000 0.000
#&gt; SRR1274581     1  0.0000      0.972 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274529     2  0.5465      0.683 0.000 0.712 0.288
#&gt; SRR1274530     2  0.5465      0.683 0.000 0.712 0.288
#&gt; SRR1274531     3  0.0000      0.528 0.000 0.000 1.000
#&gt; SRR1274532     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274533     3  0.5465      0.597 0.000 0.288 0.712
#&gt; SRR1274534     3  0.5465      0.597 0.000 0.288 0.712
#&gt; SRR1274535     3  0.5465      0.342 0.288 0.000 0.712
#&gt; SRR1274536     3  0.6587      0.250 0.352 0.016 0.632
#&gt; SRR1274537     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274539     3  0.5465      0.597 0.000 0.288 0.712
#&gt; SRR1274540     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274545     2  0.1643      0.872 0.000 0.956 0.044
#&gt; SRR1274546     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274549     3  0.5988      0.222 0.368 0.000 0.632
#&gt; SRR1274550     1  0.6302      0.207 0.520 0.000 0.480
#&gt; SRR1274551     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274552     1  0.6302      0.207 0.520 0.000 0.480
#&gt; SRR1274553     1  0.6302      0.207 0.520 0.000 0.480
#&gt; SRR1274554     3  0.6853      0.589 0.064 0.224 0.712
#&gt; SRR1274555     1  0.5327      0.527 0.728 0.000 0.272
#&gt; SRR1274556     1  0.5327      0.527 0.728 0.000 0.272
#&gt; SRR1274557     1  0.6302      0.207 0.520 0.000 0.480
#&gt; SRR1274558     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274559     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274561     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274562     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274563     1  0.5327      0.527 0.728 0.000 0.272
#&gt; SRR1274564     2  0.5968      0.603 0.000 0.636 0.364
#&gt; SRR1274565     2  0.6026      0.589 0.000 0.624 0.376
#&gt; SRR1274566     2  0.6026      0.589 0.000 0.624 0.376
#&gt; SRR1274567     3  0.6252      0.090 0.444 0.000 0.556
#&gt; SRR1274568     1  0.9290     -0.142 0.464 0.164 0.372
#&gt; SRR1274569     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.898 0.000 1.000 0.000
#&gt; SRR1274575     2  0.5465      0.683 0.000 0.712 0.288
#&gt; SRR1274576     2  0.0892      0.881 0.000 0.980 0.020
#&gt; SRR1274577     3  0.6703      0.438 0.236 0.052 0.712
#&gt; SRR1274578     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.761 1.000 0.000 0.000
#&gt; SRR1274581     1  0.0000      0.761 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274529     4  0.2469      0.877 0.000 0.108 0.000 0.892
#&gt; SRR1274530     4  0.2469      0.877 0.000 0.108 0.000 0.892
#&gt; SRR1274531     3  0.4500      0.445 0.000 0.000 0.684 0.316
#&gt; SRR1274532     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274533     3  0.0000      0.804 0.000 0.000 1.000 0.000
#&gt; SRR1274534     3  0.0000      0.804 0.000 0.000 1.000 0.000
#&gt; SRR1274535     3  0.0000      0.804 0.000 0.000 1.000 0.000
#&gt; SRR1274536     4  0.0000      0.918 0.000 0.000 0.000 1.000
#&gt; SRR1274537     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274539     3  0.0000      0.804 0.000 0.000 1.000 0.000
#&gt; SRR1274540     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.0469      0.987 0.000 0.988 0.000 0.012
#&gt; SRR1274546     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274549     4  0.4581      0.705 0.120 0.000 0.080 0.800
#&gt; SRR1274550     3  0.4193      0.655 0.268 0.000 0.732 0.000
#&gt; SRR1274551     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.4222      0.650 0.272 0.000 0.728 0.000
#&gt; SRR1274553     3  0.4356      0.618 0.292 0.000 0.708 0.000
#&gt; SRR1274554     3  0.0000      0.804 0.000 0.000 1.000 0.000
#&gt; SRR1274555     1  0.4564      0.478 0.672 0.000 0.328 0.000
#&gt; SRR1274556     1  0.4564      0.478 0.672 0.000 0.328 0.000
#&gt; SRR1274557     3  0.4222      0.651 0.272 0.000 0.728 0.000
#&gt; SRR1274558     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274559     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274562     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274563     1  0.4543      0.486 0.676 0.000 0.324 0.000
#&gt; SRR1274564     4  0.0000      0.918 0.000 0.000 0.000 1.000
#&gt; SRR1274565     4  0.0000      0.918 0.000 0.000 0.000 1.000
#&gt; SRR1274566     4  0.0000      0.918 0.000 0.000 0.000 1.000
#&gt; SRR1274567     4  0.0000      0.918 0.000 0.000 0.000 1.000
#&gt; SRR1274568     3  0.5130      0.459 0.312 0.020 0.668 0.000
#&gt; SRR1274569     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1274575     4  0.2469      0.877 0.000 0.108 0.000 0.892
#&gt; SRR1274576     2  0.0817      0.975 0.000 0.976 0.024 0.000
#&gt; SRR1274577     3  0.0000      0.804 0.000 0.000 1.000 0.000
#&gt; SRR1274578     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.909 1.000 0.000 0.000 0.000
#&gt; SRR1274581     1  0.0592      0.896 0.984 0.000 0.016 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.2460     0.9160 0.000 0.072 0.024 0.900 0.004
#&gt; SRR1274530     4  0.2460     0.9160 0.000 0.072 0.024 0.900 0.004
#&gt; SRR1274531     3  0.5847     0.0739 0.000 0.000 0.480 0.096 0.424
#&gt; SRR1274532     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.0703     0.9448 0.000 0.000 0.024 0.000 0.976
#&gt; SRR1274534     5  0.0703     0.9448 0.000 0.000 0.024 0.000 0.976
#&gt; SRR1274535     5  0.0880     0.9388 0.000 0.000 0.032 0.000 0.968
#&gt; SRR1274536     4  0.0000     0.9496 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274537     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.0703     0.9448 0.000 0.000 0.024 0.000 0.976
#&gt; SRR1274540     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.1901     0.9120 0.000 0.932 0.024 0.040 0.004
#&gt; SRR1274546     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0865     0.9463 0.000 0.972 0.024 0.000 0.004
#&gt; SRR1274548     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     3  0.2516     0.7624 0.000 0.000 0.860 0.140 0.000
#&gt; SRR1274550     3  0.1670     0.8363 0.012 0.000 0.936 0.000 0.052
#&gt; SRR1274551     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.1740     0.8347 0.012 0.000 0.932 0.000 0.056
#&gt; SRR1274553     3  0.1670     0.8363 0.012 0.000 0.936 0.000 0.052
#&gt; SRR1274554     5  0.0703     0.9448 0.000 0.000 0.024 0.000 0.976
#&gt; SRR1274555     3  0.0865     0.8338 0.024 0.000 0.972 0.000 0.004
#&gt; SRR1274556     3  0.0865     0.8338 0.024 0.000 0.972 0.000 0.004
#&gt; SRR1274557     3  0.1364     0.8370 0.012 0.000 0.952 0.000 0.036
#&gt; SRR1274558     2  0.2462     0.8574 0.112 0.880 0.000 0.000 0.008
#&gt; SRR1274559     1  0.0290     0.8638 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1274560     1  0.0290     0.8638 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1274561     1  0.4304    -0.0330 0.516 0.000 0.484 0.000 0.000
#&gt; SRR1274562     3  0.4210     0.1455 0.412 0.000 0.588 0.000 0.000
#&gt; SRR1274563     3  0.0865     0.8338 0.024 0.000 0.972 0.000 0.004
#&gt; SRR1274564     4  0.0000     0.9496 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274565     4  0.0162     0.9481 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1274566     4  0.0000     0.9496 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274567     4  0.0000     0.9496 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274568     5  0.3861     0.6335 0.284 0.004 0.000 0.000 0.712
#&gt; SRR1274569     1  0.0703     0.8778 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1274570     1  0.0963     0.8790 0.964 0.000 0.036 0.000 0.000
#&gt; SRR1274571     1  0.0703     0.8778 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1274572     1  0.2179     0.8689 0.888 0.000 0.112 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.9650 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.2460     0.9160 0.000 0.072 0.024 0.900 0.004
#&gt; SRR1274576     2  0.4088     0.4164 0.000 0.632 0.000 0.000 0.368
#&gt; SRR1274577     5  0.0404     0.9377 0.000 0.000 0.012 0.000 0.988
#&gt; SRR1274578     1  0.2513     0.8662 0.876 0.000 0.116 0.000 0.008
#&gt; SRR1274579     1  0.2513     0.8662 0.876 0.000 0.116 0.000 0.008
#&gt; SRR1274580     1  0.2513     0.8662 0.876 0.000 0.116 0.000 0.008
#&gt; SRR1274581     3  0.3582     0.6121 0.224 0.000 0.768 0.000 0.008
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     4  0.4209     0.8089 0.008 0.080 0.000 0.760 0.004 0.148
#&gt; SRR1274530     4  0.4209     0.8089 0.008 0.080 0.000 0.760 0.004 0.148
#&gt; SRR1274531     3  0.6410     0.0551 0.000 0.000 0.416 0.208 0.352 0.024
#&gt; SRR1274532     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.1196     0.9367 0.000 0.000 0.008 0.000 0.952 0.040
#&gt; SRR1274534     5  0.0146     0.9486 0.000 0.000 0.004 0.000 0.996 0.000
#&gt; SRR1274535     5  0.1649     0.9162 0.000 0.000 0.032 0.000 0.932 0.036
#&gt; SRR1274536     4  0.0000     0.8755 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274537     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.0146     0.9486 0.000 0.000 0.004 0.000 0.996 0.000
#&gt; SRR1274540     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.4052     0.7091 0.008 0.772 0.000 0.068 0.004 0.148
#&gt; SRR1274546     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.2876     0.7902 0.008 0.836 0.000 0.004 0.004 0.148
#&gt; SRR1274548     2  0.0146     0.9457 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1274549     3  0.2697     0.7166 0.000 0.000 0.812 0.188 0.000 0.000
#&gt; SRR1274550     3  0.1723     0.8164 0.000 0.000 0.928 0.000 0.036 0.036
#&gt; SRR1274551     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.2265     0.8069 0.000 0.000 0.896 0.000 0.052 0.052
#&gt; SRR1274553     3  0.2265     0.8069 0.000 0.000 0.896 0.000 0.052 0.052
#&gt; SRR1274554     5  0.0935     0.9392 0.000 0.000 0.004 0.000 0.964 0.032
#&gt; SRR1274555     3  0.0000     0.8261 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274556     3  0.0146     0.8258 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1274557     3  0.0146     0.8261 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1274558     6  0.4147     0.1590 0.012 0.436 0.000 0.000 0.000 0.552
#&gt; SRR1274559     6  0.3578     0.3991 0.340 0.000 0.000 0.000 0.000 0.660
#&gt; SRR1274560     6  0.3578     0.3991 0.340 0.000 0.000 0.000 0.000 0.660
#&gt; SRR1274561     3  0.4963     0.4469 0.240 0.000 0.636 0.000 0.000 0.124
#&gt; SRR1274562     3  0.3500     0.6373 0.204 0.000 0.768 0.000 0.000 0.028
#&gt; SRR1274563     3  0.0000     0.8261 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274564     4  0.0790     0.8745 0.000 0.000 0.000 0.968 0.000 0.032
#&gt; SRR1274565     4  0.1075     0.8645 0.000 0.000 0.000 0.952 0.000 0.048
#&gt; SRR1274566     4  0.0458     0.8730 0.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1274567     4  0.0458     0.8730 0.000 0.000 0.000 0.984 0.000 0.016
#&gt; SRR1274568     6  0.3885     0.3625 0.044 0.000 0.000 0.000 0.220 0.736
#&gt; SRR1274569     1  0.3043     0.6995 0.792 0.000 0.008 0.000 0.000 0.200
#&gt; SRR1274570     1  0.2948     0.7137 0.804 0.000 0.008 0.000 0.000 0.188
#&gt; SRR1274571     1  0.2948     0.7137 0.804 0.000 0.008 0.000 0.000 0.188
#&gt; SRR1274572     1  0.0891     0.8001 0.968 0.000 0.024 0.000 0.000 0.008
#&gt; SRR1274573     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.9487 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.4209     0.8089 0.008 0.080 0.000 0.760 0.004 0.148
#&gt; SRR1274576     2  0.4640     0.5249 0.000 0.680 0.000 0.000 0.212 0.108
#&gt; SRR1274577     5  0.2191     0.8745 0.004 0.000 0.000 0.000 0.876 0.120
#&gt; SRR1274578     1  0.0632     0.8005 0.976 0.000 0.024 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0632     0.8005 0.976 0.000 0.024 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0632     0.8005 0.976 0.000 0.024 0.000 0.000 0.000
#&gt; SRR1274581     1  0.3861     0.3725 0.640 0.000 0.352 0.000 0.000 0.008
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.887           0.939       0.974         0.5025 0.497   0.497
#> 3 3 0.719           0.697       0.867         0.2247 0.860   0.732
#> 4 4 0.891           0.784       0.895         0.1724 0.809   0.563
#> 5 5 0.848           0.792       0.916         0.0250 0.785   0.425
#> 6 6 0.970           0.896       0.961         0.0716 0.888   0.608
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.975 0.000 1.000
#&gt; SRR1274529     2   0.000      0.975 0.000 1.000
#&gt; SRR1274530     2   0.000      0.975 0.000 1.000
#&gt; SRR1274531     1   0.552      0.843 0.872 0.128
#&gt; SRR1274532     2   0.000      0.975 0.000 1.000
#&gt; SRR1274533     2   0.000      0.975 0.000 1.000
#&gt; SRR1274534     2   0.000      0.975 0.000 1.000
#&gt; SRR1274535     2   0.866      0.589 0.288 0.712
#&gt; SRR1274536     1   0.552      0.843 0.872 0.128
#&gt; SRR1274537     2   0.000      0.975 0.000 1.000
#&gt; SRR1274538     2   0.000      0.975 0.000 1.000
#&gt; SRR1274539     2   0.000      0.975 0.000 1.000
#&gt; SRR1274540     2   0.000      0.975 0.000 1.000
#&gt; SRR1274541     2   0.000      0.975 0.000 1.000
#&gt; SRR1274542     2   0.000      0.975 0.000 1.000
#&gt; SRR1274543     2   0.000      0.975 0.000 1.000
#&gt; SRR1274544     2   0.000      0.975 0.000 1.000
#&gt; SRR1274545     2   0.000      0.975 0.000 1.000
#&gt; SRR1274546     2   0.000      0.975 0.000 1.000
#&gt; SRR1274547     2   0.000      0.975 0.000 1.000
#&gt; SRR1274548     2   0.000      0.975 0.000 1.000
#&gt; SRR1274549     1   0.000      0.969 1.000 0.000
#&gt; SRR1274550     1   0.000      0.969 1.000 0.000
#&gt; SRR1274551     2   0.000      0.975 0.000 1.000
#&gt; SRR1274552     1   0.000      0.969 1.000 0.000
#&gt; SRR1274553     1   0.000      0.969 1.000 0.000
#&gt; SRR1274554     2   0.373      0.909 0.072 0.928
#&gt; SRR1274555     1   0.000      0.969 1.000 0.000
#&gt; SRR1274556     1   0.000      0.969 1.000 0.000
#&gt; SRR1274557     1   0.000      0.969 1.000 0.000
#&gt; SRR1274558     2   0.000      0.975 0.000 1.000
#&gt; SRR1274559     1   0.000      0.969 1.000 0.000
#&gt; SRR1274560     1   0.000      0.969 1.000 0.000
#&gt; SRR1274561     1   0.000      0.969 1.000 0.000
#&gt; SRR1274562     1   0.000      0.969 1.000 0.000
#&gt; SRR1274563     1   0.000      0.969 1.000 0.000
#&gt; SRR1274564     1   0.990      0.212 0.560 0.440
#&gt; SRR1274565     2   0.000      0.975 0.000 1.000
#&gt; SRR1274566     2   0.714      0.752 0.196 0.804
#&gt; SRR1274567     1   0.000      0.969 1.000 0.000
#&gt; SRR1274568     2   0.563      0.843 0.132 0.868
#&gt; SRR1274569     1   0.000      0.969 1.000 0.000
#&gt; SRR1274570     1   0.000      0.969 1.000 0.000
#&gt; SRR1274571     1   0.000      0.969 1.000 0.000
#&gt; SRR1274572     1   0.000      0.969 1.000 0.000
#&gt; SRR1274573     2   0.000      0.975 0.000 1.000
#&gt; SRR1274574     2   0.000      0.975 0.000 1.000
#&gt; SRR1274575     2   0.000      0.975 0.000 1.000
#&gt; SRR1274576     2   0.000      0.975 0.000 1.000
#&gt; SRR1274577     2   0.000      0.975 0.000 1.000
#&gt; SRR1274578     1   0.000      0.969 1.000 0.000
#&gt; SRR1274579     1   0.000      0.969 1.000 0.000
#&gt; SRR1274580     1   0.000      0.969 1.000 0.000
#&gt; SRR1274581     1   0.000      0.969 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274530     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274531     3  0.0000     0.6793 0.000 0.000 1.000
#&gt; SRR1274532     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274533     2  0.6126     0.5183 0.000 0.600 0.400
#&gt; SRR1274534     2  0.6126     0.5183 0.000 0.600 0.400
#&gt; SRR1274535     3  0.5650     0.2657 0.000 0.312 0.688
#&gt; SRR1274536     3  0.0237     0.6784 0.000 0.004 0.996
#&gt; SRR1274537     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274539     2  0.6126     0.5183 0.000 0.600 0.400
#&gt; SRR1274540     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274546     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274549     3  0.0000     0.6793 0.000 0.000 1.000
#&gt; SRR1274550     3  0.0000     0.6793 0.000 0.000 1.000
#&gt; SRR1274551     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274552     3  0.0000     0.6793 0.000 0.000 1.000
#&gt; SRR1274553     3  0.1163     0.6725 0.028 0.000 0.972
#&gt; SRR1274554     2  0.6126     0.5183 0.000 0.600 0.400
#&gt; SRR1274555     3  0.4750     0.5751 0.216 0.000 0.784
#&gt; SRR1274556     3  0.0237     0.6790 0.004 0.000 0.996
#&gt; SRR1274557     3  0.0000     0.6793 0.000 0.000 1.000
#&gt; SRR1274558     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274559     3  0.6126     0.4158 0.400 0.000 0.600
#&gt; SRR1274560     3  0.6126     0.4158 0.400 0.000 0.600
#&gt; SRR1274561     3  0.6126     0.4158 0.400 0.000 0.600
#&gt; SRR1274562     3  0.6126     0.4158 0.400 0.000 0.600
#&gt; SRR1274563     3  0.6079     0.4277 0.388 0.000 0.612
#&gt; SRR1274564     3  0.6295     0.2129 0.000 0.472 0.528
#&gt; SRR1274565     2  0.6126     0.5183 0.000 0.600 0.400
#&gt; SRR1274566     3  0.6154    -0.0528 0.000 0.408 0.592
#&gt; SRR1274567     3  0.0000     0.6793 0.000 0.000 1.000
#&gt; SRR1274568     2  0.6154     0.5037 0.000 0.592 0.408
#&gt; SRR1274569     3  0.6126     0.4158 0.400 0.000 0.600
#&gt; SRR1274570     1  0.4002     0.7350 0.840 0.000 0.160
#&gt; SRR1274571     3  0.6126     0.4158 0.400 0.000 0.600
#&gt; SRR1274572     1  0.0000     0.9536 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274576     2  0.0000     0.8812 0.000 1.000 0.000
#&gt; SRR1274577     2  0.6126     0.5183 0.000 0.600 0.400
#&gt; SRR1274578     1  0.0000     0.9536 1.000 0.000 0.000
#&gt; SRR1274579     1  0.0000     0.9536 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000     0.9536 1.000 0.000 0.000
#&gt; SRR1274581     1  0.0424     0.9465 0.992 0.000 0.008
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274530     2  0.0469     0.9870 0.000 0.988 0.000 0.012
#&gt; SRR1274531     4  0.0000     0.8781 0.000 0.000 0.000 1.000
#&gt; SRR1274532     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274533     4  0.2081     0.8738 0.000 0.084 0.000 0.916
#&gt; SRR1274534     4  0.2081     0.8738 0.000 0.084 0.000 0.916
#&gt; SRR1274535     4  0.2271     0.8756 0.000 0.076 0.008 0.916
#&gt; SRR1274536     3  0.4855     0.4534 0.000 0.000 0.600 0.400
#&gt; SRR1274537     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274539     4  0.2081     0.8738 0.000 0.084 0.000 0.916
#&gt; SRR1274540     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274546     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274549     3  0.2081     0.5722 0.000 0.000 0.916 0.084
#&gt; SRR1274550     3  0.4746     0.0665 0.000 0.000 0.632 0.368
#&gt; SRR1274551     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274552     4  0.2413     0.8505 0.064 0.000 0.020 0.916
#&gt; SRR1274553     4  0.4343     0.6711 0.004 0.000 0.264 0.732
#&gt; SRR1274554     4  0.0000     0.8781 0.000 0.000 0.000 1.000
#&gt; SRR1274555     3  0.0000     0.5653 0.000 0.000 1.000 0.000
#&gt; SRR1274556     3  0.4222     0.3268 0.000 0.000 0.728 0.272
#&gt; SRR1274557     4  0.4855     0.4669 0.000 0.000 0.400 0.600
#&gt; SRR1274558     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274559     3  0.4855     0.4500 0.400 0.000 0.600 0.000
#&gt; SRR1274560     3  0.4855     0.4500 0.400 0.000 0.600 0.000
#&gt; SRR1274561     3  0.4855     0.4500 0.400 0.000 0.600 0.000
#&gt; SRR1274562     3  0.0336     0.5655 0.008 0.000 0.992 0.000
#&gt; SRR1274563     3  0.0000     0.5653 0.000 0.000 1.000 0.000
#&gt; SRR1274564     3  0.6439     0.3401 0.000 0.340 0.576 0.084
#&gt; SRR1274565     4  0.0000     0.8781 0.000 0.000 0.000 1.000
#&gt; SRR1274566     4  0.0000     0.8781 0.000 0.000 0.000 1.000
#&gt; SRR1274567     3  0.4855     0.4534 0.000 0.000 0.600 0.400
#&gt; SRR1274568     4  0.2081     0.8738 0.000 0.084 0.000 0.916
#&gt; SRR1274569     3  0.4855     0.4500 0.400 0.000 0.600 0.000
#&gt; SRR1274570     1  0.3172     0.6497 0.840 0.000 0.160 0.000
#&gt; SRR1274571     3  0.4855     0.4500 0.400 0.000 0.600 0.000
#&gt; SRR1274572     1  0.0000     0.8525 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.0469     0.9870 0.000 0.988 0.000 0.012
#&gt; SRR1274576     2  0.0000     0.9986 0.000 1.000 0.000 0.000
#&gt; SRR1274577     4  0.0000     0.8781 0.000 0.000 0.000 1.000
#&gt; SRR1274578     1  0.0000     0.8525 1.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000     0.8525 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000     0.8525 1.000 0.000 0.000 0.000
#&gt; SRR1274581     1  0.4872     0.4201 0.640 0.000 0.356 0.004
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.0963      0.883 0.000 0.964 0.000 0.036 0.000
#&gt; SRR1274530     4  0.4262      0.355 0.000 0.440 0.000 0.560 0.000
#&gt; SRR1274531     4  0.0000      0.740 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274532     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     2  0.4384      0.502 0.000 0.660 0.016 0.324 0.000
#&gt; SRR1274534     2  0.4384      0.502 0.000 0.660 0.016 0.324 0.000
#&gt; SRR1274535     3  0.5338      0.489 0.000 0.072 0.604 0.324 0.000
#&gt; SRR1274536     4  0.0162      0.741 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1274537     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     2  0.4384      0.502 0.000 0.660 0.016 0.324 0.000
#&gt; SRR1274540     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     4  0.4384      0.363 0.016 0.000 0.324 0.660 0.000
#&gt; SRR1274550     3  0.0000      0.817 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274551     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.5172      0.536 0.060 0.000 0.616 0.324 0.000
#&gt; SRR1274553     3  0.3001      0.750 0.008 0.000 0.844 0.144 0.004
#&gt; SRR1274554     4  0.2208      0.679 0.000 0.072 0.020 0.908 0.000
#&gt; SRR1274555     3  0.0510      0.821 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1274556     3  0.0510      0.821 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1274557     3  0.0510      0.821 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1274558     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274559     1  0.0000      0.933 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.933 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.0000      0.933 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274562     1  0.4171      0.391 0.604 0.000 0.396 0.000 0.000
#&gt; SRR1274563     3  0.0510      0.821 0.016 0.000 0.984 0.000 0.000
#&gt; SRR1274564     4  0.4047      0.522 0.000 0.320 0.000 0.676 0.004
#&gt; SRR1274565     4  0.0162      0.741 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1274566     4  0.0162      0.741 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1274567     4  0.0162      0.741 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1274568     2  0.4074      0.453 0.000 0.636 0.000 0.364 0.000
#&gt; SRR1274569     1  0.0000      0.933 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0162      0.931 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1274571     1  0.0000      0.933 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0510      0.919 0.984 0.000 0.000 0.000 0.016
#&gt; SRR1274573     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.4300      0.263 0.000 0.476 0.000 0.524 0.000
#&gt; SRR1274576     2  0.0000      0.919 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274577     4  0.0510      0.730 0.000 0.000 0.016 0.984 0.000
#&gt; SRR1274578     5  0.0162      0.998 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1274579     5  0.0162      0.998 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1274580     5  0.0162      0.998 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1274581     5  0.0000      0.995 0.000 0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.0937      0.952 0.000 0.960 0.000 0.040 0.000 0.000
#&gt; SRR1274530     4  0.3823      0.336 0.000 0.436 0.000 0.564 0.000 0.000
#&gt; SRR1274531     5  0.3838      0.193 0.000 0.000 0.000 0.448 0.552 0.000
#&gt; SRR1274532     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.0000      0.915 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274534     5  0.0000      0.915 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274535     5  0.0000      0.915 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274536     4  0.0000      0.767 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274537     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.0000      0.915 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274540     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274549     4  0.2454      0.642 0.000 0.000 0.160 0.840 0.000 0.000
#&gt; SRR1274550     3  0.0000      0.929 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274551     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     5  0.0000      0.915 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274553     5  0.2946      0.722 0.004 0.000 0.184 0.000 0.808 0.004
#&gt; SRR1274554     5  0.0000      0.915 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274555     3  0.0000      0.929 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274556     3  0.0000      0.929 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274557     3  0.0000      0.929 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274558     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274559     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274562     3  0.3428      0.565 0.304 0.000 0.696 0.000 0.000 0.000
#&gt; SRR1274563     3  0.0000      0.929 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274564     4  0.0000      0.767 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274565     4  0.0146      0.768 0.000 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1274566     4  0.0146      0.768 0.000 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1274567     4  0.0146      0.768 0.000 0.000 0.000 0.996 0.004 0.000
#&gt; SRR1274568     5  0.1053      0.893 0.020 0.012 0.000 0.004 0.964 0.000
#&gt; SRR1274569     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      1.000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.3860      0.239 0.000 0.472 0.000 0.528 0.000 0.000
#&gt; SRR1274576     2  0.0000      0.997 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274577     5  0.0000      0.915 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274578     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274579     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274580     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274581     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.520           0.814       0.909         0.3564 0.693   0.693
#> 3 3 0.504           0.743       0.862         0.4658 0.756   0.655
#> 4 4 0.471           0.597       0.805         0.2518 0.903   0.805
#> 5 5 0.674           0.674       0.818         0.2036 0.724   0.382
#> 6 6 0.701           0.788       0.831         0.0373 0.913   0.607
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.9286      0.377 0.344 0.656
#&gt; SRR1274529     1  0.8763      0.657 0.704 0.296
#&gt; SRR1274530     1  0.8763      0.657 0.704 0.296
#&gt; SRR1274531     1  0.1414      0.888 0.980 0.020
#&gt; SRR1274532     2  0.0000      0.911 0.000 1.000
#&gt; SRR1274533     1  0.3114      0.873 0.944 0.056
#&gt; SRR1274534     1  0.0672      0.890 0.992 0.008
#&gt; SRR1274535     1  0.1633      0.887 0.976 0.024
#&gt; SRR1274536     1  0.5842      0.824 0.860 0.140
#&gt; SRR1274537     1  0.9754      0.438 0.592 0.408
#&gt; SRR1274538     1  0.9963      0.279 0.536 0.464
#&gt; SRR1274539     1  0.0672      0.890 0.992 0.008
#&gt; SRR1274540     2  0.0000      0.911 0.000 1.000
#&gt; SRR1274541     2  0.0000      0.911 0.000 1.000
#&gt; SRR1274542     2  0.0000      0.911 0.000 1.000
#&gt; SRR1274543     1  0.8144      0.716 0.748 0.252
#&gt; SRR1274544     2  0.0000      0.911 0.000 1.000
#&gt; SRR1274545     1  0.8909      0.638 0.692 0.308
#&gt; SRR1274546     2  0.4690      0.837 0.100 0.900
#&gt; SRR1274547     1  0.9732      0.448 0.596 0.404
#&gt; SRR1274548     1  0.9393      0.546 0.644 0.356
#&gt; SRR1274549     1  0.1414      0.888 0.980 0.020
#&gt; SRR1274550     1  0.0376      0.891 0.996 0.004
#&gt; SRR1274551     2  0.0000      0.911 0.000 1.000
#&gt; SRR1274552     1  0.0376      0.891 0.996 0.004
#&gt; SRR1274553     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274554     1  0.3114      0.873 0.944 0.056
#&gt; SRR1274555     1  0.0376      0.891 0.996 0.004
#&gt; SRR1274556     1  0.1414      0.888 0.980 0.020
#&gt; SRR1274557     1  0.0376      0.891 0.996 0.004
#&gt; SRR1274558     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274559     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274560     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274561     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274562     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274563     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274564     1  0.6148      0.815 0.848 0.152
#&gt; SRR1274565     1  0.6148      0.815 0.848 0.152
#&gt; SRR1274566     1  0.6148      0.815 0.848 0.152
#&gt; SRR1274567     1  0.4939      0.844 0.892 0.108
#&gt; SRR1274568     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274569     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274570     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274571     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274572     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274573     2  0.0000      0.911 0.000 1.000
#&gt; SRR1274574     2  0.7219      0.708 0.200 0.800
#&gt; SRR1274575     1  0.8763      0.657 0.704 0.296
#&gt; SRR1274576     1  0.7815      0.743 0.768 0.232
#&gt; SRR1274577     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274578     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274579     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274580     1  0.0000      0.890 1.000 0.000
#&gt; SRR1274581     1  0.1184      0.889 0.984 0.016
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.5560     0.5393 0.000 0.700 0.300
#&gt; SRR1274529     3  0.0424     0.7510 0.008 0.000 0.992
#&gt; SRR1274530     3  0.0424     0.7510 0.008 0.000 0.992
#&gt; SRR1274531     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274532     2  0.0000     0.7655 0.000 1.000 0.000
#&gt; SRR1274533     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274534     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274535     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274536     3  0.0000     0.7566 0.000 0.000 1.000
#&gt; SRR1274537     3  0.6978     0.4173 0.032 0.336 0.632
#&gt; SRR1274538     2  0.6309     0.0188 0.000 0.504 0.496
#&gt; SRR1274539     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274540     2  0.0000     0.7655 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000     0.7655 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000     0.7655 0.000 1.000 0.000
#&gt; SRR1274543     3  0.4974     0.6557 0.000 0.236 0.764
#&gt; SRR1274544     2  0.0000     0.7655 0.000 1.000 0.000
#&gt; SRR1274545     3  0.0000     0.7566 0.000 0.000 1.000
#&gt; SRR1274546     2  0.1529     0.7467 0.000 0.960 0.040
#&gt; SRR1274547     3  0.4842     0.6620 0.000 0.224 0.776
#&gt; SRR1274548     2  0.6309     0.0188 0.000 0.504 0.496
#&gt; SRR1274549     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274550     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274551     2  0.0000     0.7655 0.000 1.000 0.000
#&gt; SRR1274552     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274553     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274554     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274555     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274556     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274557     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274558     3  0.5760     0.7530 0.328 0.000 0.672
#&gt; SRR1274559     3  0.5497     0.7937 0.292 0.000 0.708
#&gt; SRR1274560     3  0.6286     0.4953 0.464 0.000 0.536
#&gt; SRR1274561     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274562     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274563     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274564     3  0.0000     0.7566 0.000 0.000 1.000
#&gt; SRR1274565     3  0.1031     0.7569 0.000 0.024 0.976
#&gt; SRR1274566     3  0.0000     0.7566 0.000 0.000 1.000
#&gt; SRR1274567     3  0.0000     0.7566 0.000 0.000 1.000
#&gt; SRR1274568     3  0.5760     0.7530 0.328 0.000 0.672
#&gt; SRR1274569     1  0.4931     0.5400 0.768 0.000 0.232
#&gt; SRR1274570     1  0.0424     0.9389 0.992 0.000 0.008
#&gt; SRR1274571     1  0.0424     0.9389 0.992 0.000 0.008
#&gt; SRR1274572     1  0.0424     0.9389 0.992 0.000 0.008
#&gt; SRR1274573     2  0.0000     0.7655 0.000 1.000 0.000
#&gt; SRR1274574     2  0.6008     0.5162 0.000 0.628 0.372
#&gt; SRR1274575     3  0.0424     0.7510 0.008 0.000 0.992
#&gt; SRR1274576     3  0.6225     0.1811 0.000 0.432 0.568
#&gt; SRR1274577     3  0.4887     0.8475 0.228 0.000 0.772
#&gt; SRR1274578     1  0.0424     0.9389 0.992 0.000 0.008
#&gt; SRR1274579     1  0.0424     0.9389 0.992 0.000 0.008
#&gt; SRR1274580     1  0.0424     0.9389 0.992 0.000 0.008
#&gt; SRR1274581     3  0.4887     0.8475 0.228 0.000 0.772
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.5184     0.5373 0.000 0.672 0.304 0.024
#&gt; SRR1274529     4  0.3801     1.0000 0.000 0.000 0.220 0.780
#&gt; SRR1274530     4  0.3801     1.0000 0.000 0.000 0.220 0.780
#&gt; SRR1274531     3  0.3852     0.5931 0.000 0.012 0.808 0.180
#&gt; SRR1274532     2  0.0000     0.8324 0.000 1.000 0.000 0.000
#&gt; SRR1274533     3  0.2976     0.5825 0.000 0.008 0.872 0.120
#&gt; SRR1274534     3  0.2976     0.5825 0.000 0.008 0.872 0.120
#&gt; SRR1274535     3  0.2976     0.5825 0.000 0.008 0.872 0.120
#&gt; SRR1274536     3  0.4933     0.1725 0.000 0.000 0.568 0.432
#&gt; SRR1274537     3  0.5543     0.1501 0.000 0.360 0.612 0.028
#&gt; SRR1274538     2  0.5691     0.2011 0.000 0.508 0.468 0.024
#&gt; SRR1274539     3  0.3032     0.5841 0.000 0.008 0.868 0.124
#&gt; SRR1274540     2  0.0000     0.8324 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.8324 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.8324 0.000 1.000 0.000 0.000
#&gt; SRR1274543     3  0.6277     0.1708 0.000 0.360 0.572 0.068
#&gt; SRR1274544     2  0.0000     0.8324 0.000 1.000 0.000 0.000
#&gt; SRR1274545     3  0.6774     0.1736 0.000 0.120 0.568 0.312
#&gt; SRR1274546     2  0.2760     0.7526 0.000 0.872 0.128 0.000
#&gt; SRR1274547     3  0.7827    -0.0468 0.000 0.316 0.408 0.276
#&gt; SRR1274548     3  0.5697    -0.2320 0.000 0.488 0.488 0.024
#&gt; SRR1274549     3  0.5110     0.5097 0.012 0.000 0.636 0.352
#&gt; SRR1274550     3  0.3400     0.6093 0.000 0.000 0.820 0.180
#&gt; SRR1274551     2  0.0000     0.8324 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.2530     0.6216 0.000 0.000 0.888 0.112
#&gt; SRR1274553     3  0.2530     0.6216 0.000 0.000 0.888 0.112
#&gt; SRR1274554     3  0.2976     0.5825 0.000 0.008 0.872 0.120
#&gt; SRR1274555     3  0.4304     0.5785 0.000 0.000 0.716 0.284
#&gt; SRR1274556     3  0.4936     0.5511 0.012 0.000 0.672 0.316
#&gt; SRR1274557     3  0.3837     0.6026 0.000 0.000 0.776 0.224
#&gt; SRR1274558     3  0.1118     0.6261 0.036 0.000 0.964 0.000
#&gt; SRR1274559     3  0.3156     0.6241 0.048 0.000 0.884 0.068
#&gt; SRR1274560     3  0.2908     0.6247 0.064 0.000 0.896 0.040
#&gt; SRR1274561     3  0.4910     0.5719 0.020 0.000 0.704 0.276
#&gt; SRR1274562     3  0.4910     0.5719 0.020 0.000 0.704 0.276
#&gt; SRR1274563     3  0.4222     0.5845 0.000 0.000 0.728 0.272
#&gt; SRR1274564     3  0.4925     0.1732 0.000 0.000 0.572 0.428
#&gt; SRR1274565     3  0.4464     0.5647 0.000 0.024 0.768 0.208
#&gt; SRR1274566     3  0.4925     0.1732 0.000 0.000 0.572 0.428
#&gt; SRR1274567     3  0.4941     0.1713 0.000 0.000 0.564 0.436
#&gt; SRR1274568     3  0.1118     0.6261 0.036 0.000 0.964 0.000
#&gt; SRR1274569     1  0.3123     0.7051 0.844 0.000 0.156 0.000
#&gt; SRR1274570     1  0.0000     0.9578 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000     0.9578 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000     0.9578 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.8324 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.5458     0.5818 0.000 0.704 0.236 0.060
#&gt; SRR1274575     4  0.3801     1.0000 0.000 0.000 0.220 0.780
#&gt; SRR1274576     3  0.4903     0.4149 0.000 0.248 0.724 0.028
#&gt; SRR1274577     3  0.0376     0.6270 0.004 0.000 0.992 0.004
#&gt; SRR1274578     1  0.0000     0.9578 1.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000     0.9578 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000     0.9578 1.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.5130     0.5504 0.020 0.000 0.668 0.312
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.3048    0.69849 0.000 0.820 0.000 0.004 0.176
#&gt; SRR1274529     4  0.1901    0.81876 0.000 0.012 0.056 0.928 0.004
#&gt; SRR1274530     4  0.1901    0.81876 0.000 0.012 0.056 0.928 0.004
#&gt; SRR1274531     5  0.6964   -0.00651 0.000 0.016 0.368 0.200 0.416
#&gt; SRR1274532     2  0.0000    0.82745 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.1116    0.74969 0.000 0.004 0.028 0.004 0.964
#&gt; SRR1274534     5  0.1412    0.74915 0.000 0.008 0.036 0.004 0.952
#&gt; SRR1274535     5  0.0955    0.74831 0.000 0.000 0.028 0.004 0.968
#&gt; SRR1274536     4  0.3210    0.81481 0.000 0.012 0.132 0.844 0.012
#&gt; SRR1274537     5  0.4054    0.56977 0.000 0.224 0.000 0.028 0.748
#&gt; SRR1274538     2  0.4990    0.29862 0.000 0.580 0.000 0.036 0.384
#&gt; SRR1274539     5  0.1329    0.75001 0.000 0.008 0.032 0.004 0.956
#&gt; SRR1274540     2  0.0000    0.82745 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000    0.82745 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000    0.82745 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     5  0.5990   -0.02982 0.000 0.436 0.024 0.056 0.484
#&gt; SRR1274544     2  0.0000    0.82745 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     4  0.6151    0.68381 0.000 0.064 0.144 0.664 0.128
#&gt; SRR1274546     2  0.1768    0.78817 0.000 0.924 0.000 0.004 0.072
#&gt; SRR1274547     4  0.7542    0.48619 0.000 0.164 0.128 0.520 0.188
#&gt; SRR1274548     2  0.4747    0.06671 0.000 0.500 0.000 0.016 0.484
#&gt; SRR1274549     3  0.3895    0.32533 0.000 0.000 0.680 0.320 0.000
#&gt; SRR1274550     3  0.4066    0.53621 0.000 0.000 0.672 0.004 0.324
#&gt; SRR1274551     2  0.0000    0.82745 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.4367    0.40126 0.000 0.000 0.580 0.004 0.416
#&gt; SRR1274553     3  0.4238    0.48609 0.000 0.000 0.628 0.004 0.368
#&gt; SRR1274554     5  0.0955    0.74831 0.000 0.000 0.028 0.004 0.968
#&gt; SRR1274555     3  0.1106    0.72875 0.000 0.000 0.964 0.024 0.012
#&gt; SRR1274556     3  0.1671    0.70200 0.000 0.000 0.924 0.076 0.000
#&gt; SRR1274557     3  0.2616    0.72344 0.000 0.000 0.880 0.020 0.100
#&gt; SRR1274558     5  0.4574    0.60723 0.008 0.000 0.184 0.060 0.748
#&gt; SRR1274559     3  0.6472    0.16297 0.048 0.000 0.504 0.068 0.380
#&gt; SRR1274560     3  0.6548    0.19591 0.060 0.000 0.492 0.060 0.388
#&gt; SRR1274561     3  0.1799    0.73566 0.020 0.000 0.940 0.012 0.028
#&gt; SRR1274562     3  0.1074    0.73364 0.004 0.000 0.968 0.012 0.016
#&gt; SRR1274563     3  0.1195    0.73586 0.000 0.000 0.960 0.012 0.028
#&gt; SRR1274564     4  0.3018    0.82240 0.000 0.012 0.116 0.860 0.012
#&gt; SRR1274565     4  0.6471    0.62239 0.000 0.036 0.180 0.604 0.180
#&gt; SRR1274566     4  0.3018    0.82234 0.000 0.012 0.116 0.860 0.012
#&gt; SRR1274567     4  0.3858    0.73043 0.000 0.008 0.224 0.760 0.008
#&gt; SRR1274568     5  0.4391    0.62590 0.008 0.000 0.164 0.060 0.768
#&gt; SRR1274569     1  0.0703    0.96999 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1274570     1  0.0000    0.99505 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000    0.99505 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000    0.99505 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000    0.82745 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.7470    0.37960 0.000 0.524 0.112 0.200 0.164
#&gt; SRR1274575     4  0.1901    0.81876 0.000 0.012 0.056 0.928 0.004
#&gt; SRR1274576     5  0.3209    0.64755 0.000 0.180 0.000 0.008 0.812
#&gt; SRR1274577     5  0.3264    0.64542 0.000 0.000 0.164 0.016 0.820
#&gt; SRR1274578     1  0.0000    0.99505 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000    0.99505 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000    0.99505 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.1764    0.70637 0.008 0.000 0.928 0.064 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.1970      0.741 0.000 0.900 0.000 0.000 0.008 0.092
#&gt; SRR1274529     4  0.1204      0.743 0.000 0.056 0.000 0.944 0.000 0.000
#&gt; SRR1274530     4  0.1204      0.743 0.000 0.056 0.000 0.944 0.000 0.000
#&gt; SRR1274531     3  0.4901      0.685 0.000 0.052 0.712 0.068 0.168 0.000
#&gt; SRR1274532     6  0.2969      1.000 0.000 0.224 0.000 0.000 0.000 0.776
#&gt; SRR1274533     5  0.0713      0.832 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1274534     5  0.0713      0.832 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1274535     5  0.0713      0.832 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1274536     4  0.3647      0.536 0.000 0.000 0.360 0.640 0.000 0.000
#&gt; SRR1274537     2  0.1858      0.813 0.000 0.904 0.000 0.000 0.092 0.004
#&gt; SRR1274538     2  0.1806      0.815 0.000 0.908 0.000 0.000 0.088 0.004
#&gt; SRR1274539     5  0.0713      0.832 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1274540     6  0.2969      1.000 0.000 0.224 0.000 0.000 0.000 0.776
#&gt; SRR1274541     6  0.2969      1.000 0.000 0.224 0.000 0.000 0.000 0.776
#&gt; SRR1274542     6  0.2969      1.000 0.000 0.224 0.000 0.000 0.000 0.776
#&gt; SRR1274543     2  0.2218      0.807 0.000 0.884 0.000 0.012 0.104 0.000
#&gt; SRR1274544     6  0.2969      1.000 0.000 0.224 0.000 0.000 0.000 0.776
#&gt; SRR1274545     4  0.3290      0.609 0.000 0.252 0.004 0.744 0.000 0.000
#&gt; SRR1274546     2  0.2883      0.575 0.000 0.788 0.000 0.000 0.000 0.212
#&gt; SRR1274547     2  0.3405      0.549 0.000 0.724 0.004 0.272 0.000 0.000
#&gt; SRR1274548     2  0.1806      0.815 0.000 0.908 0.000 0.000 0.088 0.004
#&gt; SRR1274549     3  0.2151      0.812 0.000 0.000 0.904 0.072 0.016 0.008
#&gt; SRR1274550     3  0.2219      0.821 0.000 0.000 0.864 0.000 0.136 0.000
#&gt; SRR1274551     6  0.2969      1.000 0.000 0.224 0.000 0.000 0.000 0.776
#&gt; SRR1274552     3  0.2416      0.814 0.000 0.000 0.844 0.000 0.156 0.000
#&gt; SRR1274553     3  0.2378      0.817 0.000 0.000 0.848 0.000 0.152 0.000
#&gt; SRR1274554     5  0.0713      0.832 0.000 0.028 0.000 0.000 0.972 0.000
#&gt; SRR1274555     3  0.1847      0.841 0.000 0.008 0.928 0.008 0.048 0.008
#&gt; SRR1274556     3  0.2036      0.815 0.000 0.000 0.912 0.064 0.016 0.008
#&gt; SRR1274557     3  0.1668      0.842 0.000 0.008 0.928 0.004 0.060 0.000
#&gt; SRR1274558     2  0.6532      0.304 0.000 0.532 0.060 0.004 0.224 0.180
#&gt; SRR1274559     3  0.6435      0.553 0.020 0.092 0.596 0.004 0.076 0.212
#&gt; SRR1274560     3  0.6598      0.551 0.032 0.092 0.592 0.004 0.076 0.204
#&gt; SRR1274561     3  0.1908      0.832 0.000 0.020 0.924 0.000 0.012 0.044
#&gt; SRR1274562     3  0.1225      0.837 0.000 0.000 0.952 0.000 0.012 0.036
#&gt; SRR1274563     3  0.1333      0.841 0.000 0.008 0.944 0.000 0.048 0.000
#&gt; SRR1274564     4  0.2562      0.754 0.000 0.000 0.172 0.828 0.000 0.000
#&gt; SRR1274565     4  0.4951      0.687 0.000 0.088 0.116 0.724 0.072 0.000
#&gt; SRR1274566     4  0.2854      0.736 0.000 0.000 0.208 0.792 0.000 0.000
#&gt; SRR1274567     4  0.3774      0.434 0.000 0.000 0.408 0.592 0.000 0.000
#&gt; SRR1274568     5  0.7425      0.325 0.004 0.128 0.268 0.004 0.420 0.176
#&gt; SRR1274569     1  0.2263      0.887 0.900 0.004 0.060 0.000 0.000 0.036
#&gt; SRR1274570     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     6  0.2969      1.000 0.000 0.224 0.000 0.000 0.000 0.776
#&gt; SRR1274574     2  0.2981      0.681 0.000 0.820 0.000 0.160 0.000 0.020
#&gt; SRR1274575     4  0.1204      0.743 0.000 0.056 0.000 0.944 0.000 0.000
#&gt; SRR1274576     2  0.1806      0.815 0.000 0.908 0.000 0.000 0.088 0.004
#&gt; SRR1274577     5  0.6669      0.539 0.008 0.116 0.192 0.000 0.556 0.128
#&gt; SRR1274578     1  0.0146      0.979 0.996 0.004 0.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.982 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.3324      0.781 0.000 0.024 0.840 0.088 0.000 0.048
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.885           0.932       0.971         0.4912 0.508   0.508
#> 3 3 0.662           0.684       0.833         0.2903 0.778   0.596
#> 4 4 0.813           0.891       0.934         0.1585 0.783   0.493
#> 5 5 0.835           0.807       0.887         0.0476 0.963   0.864
#> 6 6 0.816           0.733       0.869         0.0396 0.954   0.812
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.971 0.000 1.000
#&gt; SRR1274529     2   0.000      0.971 0.000 1.000
#&gt; SRR1274530     2   0.000      0.971 0.000 1.000
#&gt; SRR1274531     2   0.605      0.829 0.148 0.852
#&gt; SRR1274532     2   0.000      0.971 0.000 1.000
#&gt; SRR1274533     2   0.000      0.971 0.000 1.000
#&gt; SRR1274534     2   0.000      0.971 0.000 1.000
#&gt; SRR1274535     1   0.991      0.171 0.556 0.444
#&gt; SRR1274536     2   0.625      0.821 0.156 0.844
#&gt; SRR1274537     2   0.000      0.971 0.000 1.000
#&gt; SRR1274538     2   0.000      0.971 0.000 1.000
#&gt; SRR1274539     2   0.000      0.971 0.000 1.000
#&gt; SRR1274540     2   0.000      0.971 0.000 1.000
#&gt; SRR1274541     2   0.000      0.971 0.000 1.000
#&gt; SRR1274542     2   0.000      0.971 0.000 1.000
#&gt; SRR1274543     2   0.000      0.971 0.000 1.000
#&gt; SRR1274544     2   0.000      0.971 0.000 1.000
#&gt; SRR1274545     2   0.000      0.971 0.000 1.000
#&gt; SRR1274546     2   0.000      0.971 0.000 1.000
#&gt; SRR1274547     2   0.000      0.971 0.000 1.000
#&gt; SRR1274548     2   0.000      0.971 0.000 1.000
#&gt; SRR1274549     1   0.000      0.965 1.000 0.000
#&gt; SRR1274550     1   0.000      0.965 1.000 0.000
#&gt; SRR1274551     2   0.000      0.971 0.000 1.000
#&gt; SRR1274552     1   0.000      0.965 1.000 0.000
#&gt; SRR1274553     1   0.000      0.965 1.000 0.000
#&gt; SRR1274554     2   0.760      0.729 0.220 0.780
#&gt; SRR1274555     1   0.000      0.965 1.000 0.000
#&gt; SRR1274556     1   0.000      0.965 1.000 0.000
#&gt; SRR1274557     1   0.000      0.965 1.000 0.000
#&gt; SRR1274558     2   0.000      0.971 0.000 1.000
#&gt; SRR1274559     1   0.163      0.944 0.976 0.024
#&gt; SRR1274560     1   0.000      0.965 1.000 0.000
#&gt; SRR1274561     1   0.000      0.965 1.000 0.000
#&gt; SRR1274562     1   0.000      0.965 1.000 0.000
#&gt; SRR1274563     1   0.000      0.965 1.000 0.000
#&gt; SRR1274564     2   0.000      0.971 0.000 1.000
#&gt; SRR1274565     2   0.000      0.971 0.000 1.000
#&gt; SRR1274566     2   0.000      0.971 0.000 1.000
#&gt; SRR1274567     1   0.767      0.694 0.776 0.224
#&gt; SRR1274568     2   0.327      0.922 0.060 0.940
#&gt; SRR1274569     1   0.000      0.965 1.000 0.000
#&gt; SRR1274570     1   0.000      0.965 1.000 0.000
#&gt; SRR1274571     1   0.000      0.965 1.000 0.000
#&gt; SRR1274572     1   0.000      0.965 1.000 0.000
#&gt; SRR1274573     2   0.000      0.971 0.000 1.000
#&gt; SRR1274574     2   0.000      0.971 0.000 1.000
#&gt; SRR1274575     2   0.000      0.971 0.000 1.000
#&gt; SRR1274576     2   0.000      0.971 0.000 1.000
#&gt; SRR1274577     2   0.839      0.647 0.268 0.732
#&gt; SRR1274578     1   0.000      0.965 1.000 0.000
#&gt; SRR1274579     1   0.000      0.965 1.000 0.000
#&gt; SRR1274580     1   0.000      0.965 1.000 0.000
#&gt; SRR1274581     1   0.000      0.965 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274529     2  0.0000     0.6780 0.000 1.000 0.000
#&gt; SRR1274530     2  0.0000     0.6780 0.000 1.000 0.000
#&gt; SRR1274531     3  0.4842     0.6120 0.000 0.224 0.776
#&gt; SRR1274532     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274533     2  0.9664     0.5978 0.332 0.444 0.224
#&gt; SRR1274534     2  0.6473     0.8548 0.332 0.652 0.016
#&gt; SRR1274535     3  0.5733     0.4877 0.324 0.000 0.676
#&gt; SRR1274536     3  0.5810     0.5660 0.000 0.336 0.664
#&gt; SRR1274537     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274538     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274539     3  0.9942    -0.2676 0.332 0.288 0.380
#&gt; SRR1274540     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274541     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274542     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274543     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274544     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274545     2  0.0000     0.6780 0.000 1.000 0.000
#&gt; SRR1274546     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274547     2  0.0892     0.6922 0.020 0.980 0.000
#&gt; SRR1274548     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274549     3  0.5621     0.5798 0.000 0.308 0.692
#&gt; SRR1274550     3  0.0000     0.6541 0.000 0.000 1.000
#&gt; SRR1274551     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274552     3  0.0000     0.6541 0.000 0.000 1.000
#&gt; SRR1274553     3  0.0000     0.6541 0.000 0.000 1.000
#&gt; SRR1274554     3  0.9452     0.0969 0.284 0.220 0.496
#&gt; SRR1274555     3  0.0000     0.6541 0.000 0.000 1.000
#&gt; SRR1274556     3  0.0000     0.6541 0.000 0.000 1.000
#&gt; SRR1274557     3  0.0000     0.6541 0.000 0.000 1.000
#&gt; SRR1274558     2  0.6204     0.7956 0.424 0.576 0.000
#&gt; SRR1274559     1  0.5785     0.8482 0.668 0.000 0.332
#&gt; SRR1274560     1  0.5785     0.8482 0.668 0.000 0.332
#&gt; SRR1274561     3  0.4842     0.2538 0.224 0.000 0.776
#&gt; SRR1274562     1  0.6295     0.6183 0.528 0.000 0.472
#&gt; SRR1274563     3  0.0000     0.6541 0.000 0.000 1.000
#&gt; SRR1274564     2  0.1860     0.6231 0.000 0.948 0.052
#&gt; SRR1274565     2  0.0000     0.6780 0.000 1.000 0.000
#&gt; SRR1274566     2  0.3038     0.5491 0.000 0.896 0.104
#&gt; SRR1274567     3  0.5948     0.5562 0.000 0.360 0.640
#&gt; SRR1274568     1  0.6215    -0.6521 0.572 0.428 0.000
#&gt; SRR1274569     1  0.5785     0.8482 0.668 0.000 0.332
#&gt; SRR1274570     1  0.5785     0.8482 0.668 0.000 0.332
#&gt; SRR1274571     1  0.5785     0.8482 0.668 0.000 0.332
#&gt; SRR1274572     1  0.5785     0.8482 0.668 0.000 0.332
#&gt; SRR1274573     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274574     2  0.5733     0.8635 0.324 0.676 0.000
#&gt; SRR1274575     2  0.0000     0.6780 0.000 1.000 0.000
#&gt; SRR1274576     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274577     2  0.5785     0.8662 0.332 0.668 0.000
#&gt; SRR1274578     1  0.5785     0.8482 0.668 0.000 0.332
#&gt; SRR1274579     1  0.5785     0.8482 0.668 0.000 0.332
#&gt; SRR1274580     1  0.5785     0.8482 0.668 0.000 0.332
#&gt; SRR1274581     3  0.3412     0.4874 0.124 0.000 0.876
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0592      0.912 0.000 0.984 0.000 0.016
#&gt; SRR1274529     4  0.1716      0.952 0.000 0.064 0.000 0.936
#&gt; SRR1274530     4  0.1716      0.952 0.000 0.064 0.000 0.936
#&gt; SRR1274531     3  0.1284      0.916 0.000 0.012 0.964 0.024
#&gt; SRR1274532     2  0.1389      0.911 0.000 0.952 0.000 0.048
#&gt; SRR1274533     2  0.3494      0.780 0.000 0.824 0.172 0.004
#&gt; SRR1274534     2  0.1902      0.876 0.000 0.932 0.064 0.004
#&gt; SRR1274535     3  0.4761      0.474 0.000 0.332 0.664 0.004
#&gt; SRR1274536     4  0.1557      0.884 0.000 0.000 0.056 0.944
#&gt; SRR1274537     2  0.0188      0.910 0.000 0.996 0.000 0.004
#&gt; SRR1274538     2  0.1792      0.903 0.000 0.932 0.000 0.068
#&gt; SRR1274539     2  0.2197      0.867 0.000 0.916 0.080 0.004
#&gt; SRR1274540     2  0.1716      0.905 0.000 0.936 0.000 0.064
#&gt; SRR1274541     2  0.1211      0.912 0.000 0.960 0.000 0.040
#&gt; SRR1274542     2  0.1389      0.911 0.000 0.952 0.000 0.048
#&gt; SRR1274543     2  0.0817      0.913 0.000 0.976 0.000 0.024
#&gt; SRR1274544     2  0.1474      0.910 0.000 0.948 0.000 0.052
#&gt; SRR1274545     4  0.1792      0.949 0.000 0.068 0.000 0.932
#&gt; SRR1274546     2  0.0921      0.913 0.000 0.972 0.000 0.028
#&gt; SRR1274547     4  0.2011      0.939 0.000 0.080 0.000 0.920
#&gt; SRR1274548     2  0.0592      0.912 0.000 0.984 0.000 0.016
#&gt; SRR1274549     3  0.1716      0.908 0.000 0.000 0.936 0.064
#&gt; SRR1274550     3  0.0000      0.913 0.000 0.000 1.000 0.000
#&gt; SRR1274551     2  0.1867      0.900 0.000 0.928 0.000 0.072
#&gt; SRR1274552     3  0.1004      0.902 0.000 0.024 0.972 0.004
#&gt; SRR1274553     3  0.1004      0.902 0.000 0.024 0.972 0.004
#&gt; SRR1274554     2  0.4699      0.546 0.000 0.676 0.320 0.004
#&gt; SRR1274555     3  0.1389      0.916 0.000 0.000 0.952 0.048
#&gt; SRR1274556     3  0.1557      0.913 0.000 0.000 0.944 0.056
#&gt; SRR1274557     3  0.0592      0.917 0.000 0.000 0.984 0.016
#&gt; SRR1274558     2  0.3583      0.795 0.180 0.816 0.000 0.004
#&gt; SRR1274559     1  0.0000      0.970 1.000 0.000 0.000 0.000
#&gt; SRR1274560     1  0.0000      0.970 1.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.4514      0.775 0.800 0.000 0.136 0.064
#&gt; SRR1274562     1  0.2610      0.885 0.900 0.000 0.088 0.012
#&gt; SRR1274563     3  0.1389      0.916 0.000 0.000 0.952 0.048
#&gt; SRR1274564     4  0.0336      0.934 0.000 0.008 0.000 0.992
#&gt; SRR1274565     4  0.1716      0.951 0.000 0.064 0.000 0.936
#&gt; SRR1274566     4  0.0188      0.931 0.000 0.004 0.000 0.996
#&gt; SRR1274567     4  0.1302      0.896 0.000 0.000 0.044 0.956
#&gt; SRR1274568     2  0.3266      0.805 0.168 0.832 0.000 0.000
#&gt; SRR1274569     1  0.0000      0.970 1.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.970 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.970 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.970 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.1557      0.908 0.000 0.944 0.000 0.056
#&gt; SRR1274574     2  0.4331      0.622 0.000 0.712 0.000 0.288
#&gt; SRR1274575     4  0.1716      0.952 0.000 0.064 0.000 0.936
#&gt; SRR1274576     2  0.0524      0.905 0.000 0.988 0.008 0.004
#&gt; SRR1274577     2  0.1743      0.881 0.000 0.940 0.056 0.004
#&gt; SRR1274578     1  0.0000      0.970 1.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.970 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.970 1.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.4130      0.822 0.108 0.000 0.828 0.064
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0162      0.895 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1274529     4  0.0290      0.939 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1274530     4  0.0290      0.939 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1274531     3  0.4746      0.840 0.000 0.000 0.600 0.024 0.376
#&gt; SRR1274532     2  0.0290      0.895 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1274533     5  0.3752      0.465 0.000 0.292 0.000 0.000 0.708
#&gt; SRR1274534     2  0.4300      0.100 0.000 0.524 0.000 0.000 0.476
#&gt; SRR1274535     5  0.1270      0.745 0.000 0.052 0.000 0.000 0.948
#&gt; SRR1274536     4  0.0404      0.932 0.000 0.000 0.000 0.988 0.012
#&gt; SRR1274537     2  0.0000      0.893 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0510      0.892 0.000 0.984 0.000 0.016 0.000
#&gt; SRR1274539     2  0.4306      0.041 0.000 0.508 0.000 0.000 0.492
#&gt; SRR1274540     2  0.0510      0.892 0.000 0.984 0.000 0.016 0.000
#&gt; SRR1274541     2  0.0290      0.895 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1274542     2  0.0290      0.895 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1274543     2  0.0162      0.895 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1274544     2  0.0290      0.895 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1274545     4  0.1270      0.913 0.000 0.052 0.000 0.948 0.000
#&gt; SRR1274546     2  0.0162      0.895 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1274547     4  0.1197      0.917 0.000 0.048 0.000 0.952 0.000
#&gt; SRR1274548     2  0.0000      0.893 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     3  0.5538      0.788 0.000 0.000 0.504 0.068 0.428
#&gt; SRR1274550     5  0.0963      0.720 0.000 0.000 0.036 0.000 0.964
#&gt; SRR1274551     2  0.0404      0.894 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1274552     5  0.0162      0.763 0.000 0.000 0.004 0.000 0.996
#&gt; SRR1274553     5  0.0290      0.761 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1274554     2  0.5372      0.521 0.000 0.668 0.152 0.000 0.180
#&gt; SRR1274555     3  0.4383      0.829 0.000 0.000 0.572 0.004 0.424
#&gt; SRR1274556     3  0.4029      0.828 0.000 0.000 0.680 0.004 0.316
#&gt; SRR1274557     3  0.3983      0.836 0.000 0.000 0.660 0.000 0.340
#&gt; SRR1274558     2  0.2233      0.822 0.104 0.892 0.000 0.004 0.000
#&gt; SRR1274559     1  0.0703      0.911 0.976 0.000 0.024 0.000 0.000
#&gt; SRR1274560     1  0.0510      0.913 0.984 0.000 0.016 0.000 0.000
#&gt; SRR1274561     1  0.5562      0.477 0.624 0.000 0.300 0.056 0.020
#&gt; SRR1274562     1  0.3476      0.744 0.804 0.000 0.176 0.000 0.020
#&gt; SRR1274563     3  0.4425      0.806 0.004 0.000 0.544 0.000 0.452
#&gt; SRR1274564     4  0.0000      0.936 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274565     4  0.5444      0.579 0.000 0.180 0.160 0.660 0.000
#&gt; SRR1274566     4  0.0404      0.935 0.000 0.000 0.012 0.988 0.000
#&gt; SRR1274567     4  0.1106      0.922 0.000 0.000 0.024 0.964 0.012
#&gt; SRR1274568     2  0.3090      0.800 0.104 0.856 0.000 0.000 0.040
#&gt; SRR1274569     1  0.0000      0.914 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0162      0.914 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274571     1  0.0162      0.914 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274572     1  0.0404      0.913 0.988 0.000 0.012 0.000 0.000
#&gt; SRR1274573     2  0.0290      0.895 0.000 0.992 0.000 0.008 0.000
#&gt; SRR1274574     2  0.1478      0.858 0.000 0.936 0.000 0.064 0.000
#&gt; SRR1274575     4  0.0290      0.939 0.000 0.008 0.000 0.992 0.000
#&gt; SRR1274576     2  0.0703      0.881 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1274577     2  0.4489      0.708 0.004 0.764 0.092 0.000 0.140
#&gt; SRR1274578     1  0.1792      0.892 0.916 0.000 0.084 0.000 0.000
#&gt; SRR1274579     1  0.1792      0.892 0.916 0.000 0.084 0.000 0.000
#&gt; SRR1274580     1  0.1671      0.896 0.924 0.000 0.076 0.000 0.000
#&gt; SRR1274581     3  0.3080      0.536 0.008 0.000 0.844 0.008 0.140
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0260      0.897 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1274529     4  0.0363      0.886 0.000 0.012 0.000 0.988 0.000 0.000
#&gt; SRR1274530     4  0.0146      0.888 0.000 0.004 0.000 0.996 0.000 0.000
#&gt; SRR1274531     3  0.2546      0.831 0.000 0.004 0.896 0.040 0.040 0.020
#&gt; SRR1274532     2  0.0146      0.901 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274533     5  0.3093      0.781 0.000 0.076 0.060 0.000 0.852 0.012
#&gt; SRR1274534     5  0.3900      0.516 0.000 0.232 0.000 0.000 0.728 0.040
#&gt; SRR1274535     5  0.2308      0.812 0.000 0.008 0.108 0.000 0.880 0.004
#&gt; SRR1274536     4  0.0692      0.882 0.000 0.000 0.004 0.976 0.000 0.020
#&gt; SRR1274537     2  0.0260      0.897 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1274538     2  0.0458      0.892 0.000 0.984 0.000 0.016 0.000 0.000
#&gt; SRR1274539     5  0.4112      0.589 0.000 0.200 0.016 0.000 0.744 0.040
#&gt; SRR1274540     2  0.0260      0.899 0.000 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1274541     2  0.0146      0.901 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274542     2  0.0146      0.901 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274543     2  0.0260      0.897 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1274544     2  0.0146      0.901 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274545     4  0.1765      0.825 0.000 0.096 0.000 0.904 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.900 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     4  0.2003      0.800 0.000 0.116 0.000 0.884 0.000 0.000
#&gt; SRR1274548     2  0.0520      0.891 0.000 0.984 0.000 0.000 0.008 0.008
#&gt; SRR1274549     3  0.3864      0.757 0.000 0.000 0.796 0.128 0.044 0.032
#&gt; SRR1274550     5  0.2631      0.762 0.000 0.000 0.180 0.000 0.820 0.000
#&gt; SRR1274551     2  0.0260      0.899 0.000 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1274552     5  0.2048      0.811 0.000 0.000 0.120 0.000 0.880 0.000
#&gt; SRR1274553     5  0.2003      0.812 0.000 0.000 0.116 0.000 0.884 0.000
#&gt; SRR1274554     2  0.6721     -0.381 0.000 0.484 0.220 0.000 0.068 0.228
#&gt; SRR1274555     3  0.1610      0.828 0.000 0.000 0.916 0.000 0.084 0.000
#&gt; SRR1274556     3  0.0713      0.830 0.000 0.000 0.972 0.000 0.000 0.028
#&gt; SRR1274557     3  0.0363      0.838 0.000 0.000 0.988 0.000 0.012 0.000
#&gt; SRR1274558     2  0.2491      0.651 0.164 0.836 0.000 0.000 0.000 0.000
#&gt; SRR1274559     1  0.1655      0.750 0.940 0.032 0.000 0.012 0.004 0.012
#&gt; SRR1274560     1  0.0508      0.774 0.984 0.000 0.000 0.000 0.004 0.012
#&gt; SRR1274561     1  0.4628      0.426 0.648 0.000 0.308 0.016 0.012 0.016
#&gt; SRR1274562     1  0.3217      0.610 0.768 0.000 0.224 0.000 0.008 0.000
#&gt; SRR1274563     3  0.2165      0.813 0.008 0.000 0.884 0.000 0.108 0.000
#&gt; SRR1274564     4  0.0000      0.887 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274565     4  0.7150      0.185 0.000 0.164 0.148 0.492 0.008 0.188
#&gt; SRR1274566     4  0.2002      0.856 0.000 0.000 0.012 0.908 0.004 0.076
#&gt; SRR1274567     4  0.1844      0.864 0.000 0.000 0.024 0.924 0.004 0.048
#&gt; SRR1274568     2  0.4056      0.585 0.028 0.780 0.000 0.000 0.056 0.136
#&gt; SRR1274569     1  0.0146      0.776 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR1274570     1  0.0000      0.776 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.776 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.1444      0.757 0.928 0.000 0.000 0.000 0.000 0.072
#&gt; SRR1274573     2  0.0146      0.901 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR1274574     2  0.0937      0.865 0.000 0.960 0.000 0.040 0.000 0.000
#&gt; SRR1274575     4  0.0146      0.888 0.000 0.004 0.000 0.996 0.000 0.000
#&gt; SRR1274576     2  0.2136      0.793 0.000 0.904 0.000 0.000 0.048 0.048
#&gt; SRR1274577     6  0.5598      0.000 0.000 0.300 0.008 0.000 0.140 0.552
#&gt; SRR1274578     1  0.4169      0.423 0.532 0.000 0.000 0.000 0.012 0.456
#&gt; SRR1274579     1  0.3823      0.470 0.564 0.000 0.000 0.000 0.000 0.436
#&gt; SRR1274580     1  0.3706      0.534 0.620 0.000 0.000 0.000 0.000 0.380
#&gt; SRR1274581     3  0.5391      0.372 0.000 0.000 0.456 0.000 0.112 0.432
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.961       0.983         0.4377 0.575   0.575
#> 3 3 0.678           0.831       0.840         0.2002 0.980   0.966
#> 4 4 0.704           0.670       0.846         0.2523 0.754   0.557
#> 5 5 0.663           0.705       0.846         0.0175 0.904   0.730
#> 6 6 0.693           0.568       0.825         0.0614 0.881   0.652
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274529     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274530     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274531     2  0.4161      0.899 0.084 0.916
#&gt; SRR1274532     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274533     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274534     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274535     2  0.0672      0.969 0.008 0.992
#&gt; SRR1274536     2  0.0376      0.972 0.004 0.996
#&gt; SRR1274537     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274538     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274539     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274540     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274541     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274542     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274543     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274544     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274545     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274546     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274547     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274548     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274549     2  0.5629      0.847 0.132 0.868
#&gt; SRR1274550     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274551     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274552     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274553     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274554     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274555     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274556     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274557     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274558     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274559     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274560     2  0.9129      0.539 0.328 0.672
#&gt; SRR1274561     2  0.9427      0.472 0.360 0.640
#&gt; SRR1274562     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274563     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274564     2  0.0376      0.972 0.004 0.996
#&gt; SRR1274565     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274566     2  0.0376      0.972 0.004 0.996
#&gt; SRR1274567     2  0.0376      0.972 0.004 0.996
#&gt; SRR1274568     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274569     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274570     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274571     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274572     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274573     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274574     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274575     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274576     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274577     2  0.0000      0.975 0.000 1.000
#&gt; SRR1274578     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274579     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274580     1  0.0000      1.000 1.000 0.000
#&gt; SRR1274581     1  0.0000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274529     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274530     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274531     2   0.464      0.749 0.084 0.856 0.060
#&gt; SRR1274532     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274533     2   0.207      0.816 0.000 0.940 0.060
#&gt; SRR1274534     2   0.207      0.816 0.000 0.940 0.060
#&gt; SRR1274535     2   0.249      0.812 0.008 0.932 0.060
#&gt; SRR1274536     2   0.230      0.814 0.004 0.936 0.060
#&gt; SRR1274537     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274538     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274539     2   0.207      0.816 0.000 0.940 0.060
#&gt; SRR1274540     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274541     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274542     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274543     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274544     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274545     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274546     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274547     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274548     2   0.216      0.837 0.000 0.936 0.064
#&gt; SRR1274549     2   0.554      0.697 0.132 0.808 0.060
#&gt; SRR1274550     1   0.348      0.833 0.872 0.000 0.128
#&gt; SRR1274551     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274552     1   0.000      0.932 1.000 0.000 0.000
#&gt; SRR1274553     1   0.000      0.932 1.000 0.000 0.000
#&gt; SRR1274554     2   0.207      0.816 0.000 0.940 0.060
#&gt; SRR1274555     1   0.348      0.833 0.872 0.000 0.128
#&gt; SRR1274556     3   0.540      0.987 0.280 0.000 0.720
#&gt; SRR1274557     1   0.175      0.902 0.952 0.000 0.048
#&gt; SRR1274558     2   0.216      0.837 0.000 0.936 0.064
#&gt; SRR1274559     2   0.207      0.816 0.000 0.940 0.060
#&gt; SRR1274560     2   0.760      0.338 0.328 0.612 0.060
#&gt; SRR1274561     2   0.776      0.264 0.360 0.580 0.060
#&gt; SRR1274562     1   0.348      0.833 0.872 0.000 0.128
#&gt; SRR1274563     1   0.348      0.833 0.872 0.000 0.128
#&gt; SRR1274564     2   0.230      0.814 0.004 0.936 0.060
#&gt; SRR1274565     2   0.000      0.828 0.000 1.000 0.000
#&gt; SRR1274566     2   0.230      0.814 0.004 0.936 0.060
#&gt; SRR1274567     2   0.230      0.814 0.004 0.936 0.060
#&gt; SRR1274568     2   0.207      0.816 0.000 0.940 0.060
#&gt; SRR1274569     1   0.000      0.932 1.000 0.000 0.000
#&gt; SRR1274570     1   0.000      0.932 1.000 0.000 0.000
#&gt; SRR1274571     1   0.000      0.932 1.000 0.000 0.000
#&gt; SRR1274572     1   0.000      0.932 1.000 0.000 0.000
#&gt; SRR1274573     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274574     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274575     2   0.470      0.841 0.000 0.788 0.212
#&gt; SRR1274576     2   0.216      0.837 0.000 0.936 0.064
#&gt; SRR1274577     2   0.207      0.816 0.000 0.940 0.060
#&gt; SRR1274578     1   0.000      0.932 1.000 0.000 0.000
#&gt; SRR1274579     1   0.000      0.932 1.000 0.000 0.000
#&gt; SRR1274580     1   0.000      0.932 1.000 0.000 0.000
#&gt; SRR1274581     3   0.533      0.988 0.272 0.000 0.728
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274530     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274531     4  0.4352    0.57730 0.080 0.104 0.000 0.816
#&gt; SRR1274532     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274533     4  0.4967    0.51664 0.000 0.452 0.000 0.548
#&gt; SRR1274534     4  0.4967    0.51664 0.000 0.452 0.000 0.548
#&gt; SRR1274535     4  0.5257    0.51922 0.008 0.444 0.000 0.548
#&gt; SRR1274536     4  0.1637    0.56985 0.000 0.060 0.000 0.940
#&gt; SRR1274537     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274539     4  0.4967    0.51664 0.000 0.452 0.000 0.548
#&gt; SRR1274540     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274546     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.4761    0.06106 0.000 0.628 0.000 0.372
#&gt; SRR1274549     4  0.2760    0.44026 0.128 0.000 0.000 0.872
#&gt; SRR1274550     1  0.4855    0.53258 0.600 0.000 0.400 0.000
#&gt; SRR1274551     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274552     1  0.0000    0.84386 1.000 0.000 0.000 0.000
#&gt; SRR1274553     1  0.0000    0.84386 1.000 0.000 0.000 0.000
#&gt; SRR1274554     4  0.4972    0.50697 0.000 0.456 0.000 0.544
#&gt; SRR1274555     1  0.4855    0.53258 0.600 0.000 0.400 0.000
#&gt; SRR1274556     3  0.0336    0.94461 0.008 0.000 0.992 0.000
#&gt; SRR1274557     1  0.3444    0.73856 0.816 0.000 0.184 0.000
#&gt; SRR1274558     2  0.4804    0.00817 0.000 0.616 0.000 0.384
#&gt; SRR1274559     4  0.4967    0.51664 0.000 0.452 0.000 0.548
#&gt; SRR1274560     4  0.4543    0.35332 0.324 0.000 0.000 0.676
#&gt; SRR1274561     4  0.4697    0.31070 0.356 0.000 0.000 0.644
#&gt; SRR1274562     1  0.4855    0.53258 0.600 0.000 0.400 0.000
#&gt; SRR1274563     1  0.4855    0.53258 0.600 0.000 0.400 0.000
#&gt; SRR1274564     4  0.1637    0.56985 0.000 0.060 0.000 0.940
#&gt; SRR1274565     2  0.4972   -0.29436 0.000 0.544 0.000 0.456
#&gt; SRR1274566     4  0.1637    0.56985 0.000 0.060 0.000 0.940
#&gt; SRR1274567     4  0.1637    0.56985 0.000 0.060 0.000 0.940
#&gt; SRR1274568     4  0.4967    0.51664 0.000 0.452 0.000 0.548
#&gt; SRR1274569     1  0.0000    0.84386 1.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000    0.84386 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000    0.84386 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000    0.84386 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.0000    0.88426 0.000 1.000 0.000 0.000
#&gt; SRR1274576     2  0.4776    0.04450 0.000 0.624 0.000 0.376
#&gt; SRR1274577     4  0.4967    0.51664 0.000 0.452 0.000 0.548
#&gt; SRR1274578     1  0.0000    0.84386 1.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000    0.84386 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000    0.84386 1.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.1637    0.94575 0.000 0.000 0.940 0.060
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274529     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274530     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274531     4  0.5570      0.493 0.060 0.012 0.296 0.628 0.004
#&gt; SRR1274532     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274533     4  0.0000      0.644 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274534     4  0.0000      0.644 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274535     4  0.0324      0.644 0.004 0.004 0.000 0.992 0.000
#&gt; SRR1274536     4  0.4161      0.455 0.000 0.000 0.392 0.608 0.000
#&gt; SRR1274537     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274538     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274539     4  0.0000      0.644 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274540     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274541     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274542     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274543     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274544     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274545     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274546     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274547     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274548     4  0.2891      0.296 0.000 0.176 0.000 0.824 0.000
#&gt; SRR1274549     4  0.6429      0.333 0.108 0.012 0.396 0.480 0.004
#&gt; SRR1274550     1  0.4341      0.516 0.592 0.004 0.404 0.000 0.000
#&gt; SRR1274551     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274552     1  0.0290      0.836 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1274553     1  0.0290      0.836 0.992 0.000 0.008 0.000 0.000
#&gt; SRR1274554     4  0.0162      0.640 0.000 0.004 0.000 0.996 0.000
#&gt; SRR1274555     1  0.4341      0.516 0.592 0.004 0.404 0.000 0.000
#&gt; SRR1274556     3  0.4171      0.000 0.000 0.396 0.604 0.000 0.000
#&gt; SRR1274557     1  0.3160      0.728 0.808 0.004 0.188 0.000 0.000
#&gt; SRR1274558     4  0.2773      0.334 0.000 0.164 0.000 0.836 0.000
#&gt; SRR1274559     4  0.0000      0.644 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274560     4  0.6735      0.270 0.304 0.012 0.172 0.508 0.004
#&gt; SRR1274561     4  0.6821      0.231 0.336 0.012 0.172 0.476 0.004
#&gt; SRR1274562     1  0.4321      0.521 0.600 0.004 0.396 0.000 0.000
#&gt; SRR1274563     1  0.4341      0.516 0.592 0.004 0.404 0.000 0.000
#&gt; SRR1274564     4  0.4161      0.455 0.000 0.000 0.392 0.608 0.000
#&gt; SRR1274565     4  0.1908      0.504 0.000 0.092 0.000 0.908 0.000
#&gt; SRR1274566     4  0.4161      0.455 0.000 0.000 0.392 0.608 0.000
#&gt; SRR1274567     4  0.4161      0.455 0.000 0.000 0.392 0.608 0.000
#&gt; SRR1274568     4  0.0000      0.644 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274569     1  0.0000      0.838 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.838 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.838 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.838 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274574     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274575     2  0.4201      1.000 0.000 0.592 0.000 0.408 0.000
#&gt; SRR1274576     4  0.2852      0.310 0.000 0.172 0.000 0.828 0.000
#&gt; SRR1274577     4  0.0000      0.644 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274578     1  0.0000      0.838 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.838 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.838 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     5  0.0162      0.000 0.000 0.000 0.004 0.000 0.996
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR1274528     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274529     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274530     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274531     4  0.5195    -0.0463 0.000 0.100 0.000 0.540 0.360  0
#&gt; SRR1274532     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274533     4  0.3717     0.5507 0.000 0.384 0.000 0.616 0.000  0
#&gt; SRR1274534     4  0.3717     0.5507 0.000 0.384 0.000 0.616 0.000  0
#&gt; SRR1274535     4  0.4353     0.5377 0.000 0.384 0.000 0.588 0.028  0
#&gt; SRR1274536     4  0.2053     0.2320 0.000 0.004 0.000 0.888 0.108  0
#&gt; SRR1274537     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274538     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274539     4  0.3717     0.5507 0.000 0.384 0.000 0.616 0.000  0
#&gt; SRR1274540     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274541     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274542     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274543     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274544     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274545     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274546     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274547     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274548     2  0.3823    -0.1232 0.000 0.564 0.000 0.436 0.000  0
#&gt; SRR1274549     4  0.3782    -0.2705 0.000 0.000 0.000 0.588 0.412  0
#&gt; SRR1274550     3  0.0363     0.6719 0.012 0.000 0.988 0.000 0.000  0
#&gt; SRR1274551     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274552     3  0.4084     0.5237 0.400 0.000 0.588 0.000 0.012  0
#&gt; SRR1274553     3  0.4084     0.5237 0.400 0.000 0.588 0.000 0.012  0
#&gt; SRR1274554     4  0.3737     0.5381 0.000 0.392 0.000 0.608 0.000  0
#&gt; SRR1274555     3  0.0363     0.6719 0.012 0.000 0.988 0.000 0.000  0
#&gt; SRR1274556     5  0.3782    -0.3483 0.000 0.000 0.412 0.000 0.588  0
#&gt; SRR1274557     3  0.3190     0.6715 0.220 0.000 0.772 0.000 0.008  0
#&gt; SRR1274558     2  0.3838    -0.1686 0.000 0.552 0.000 0.448 0.000  0
#&gt; SRR1274559     4  0.3717     0.5507 0.000 0.384 0.000 0.616 0.000  0
#&gt; SRR1274560     4  0.5993    -0.4755 0.232 0.000 0.000 0.392 0.376  0
#&gt; SRR1274561     5  0.5986    -0.0397 0.232 0.000 0.000 0.360 0.408  0
#&gt; SRR1274562     1  0.3789     0.2750 0.584 0.000 0.416 0.000 0.000  0
#&gt; SRR1274563     3  0.0363     0.6719 0.012 0.000 0.988 0.000 0.000  0
#&gt; SRR1274564     4  0.2053     0.2320 0.000 0.004 0.000 0.888 0.108  0
#&gt; SRR1274565     4  0.3864     0.3295 0.000 0.480 0.000 0.520 0.000  0
#&gt; SRR1274566     4  0.2053     0.2320 0.000 0.004 0.000 0.888 0.108  0
#&gt; SRR1274567     4  0.2053     0.2320 0.000 0.004 0.000 0.888 0.108  0
#&gt; SRR1274568     4  0.3717     0.5507 0.000 0.384 0.000 0.616 0.000  0
#&gt; SRR1274569     1  0.0622     0.9109 0.980 0.000 0.012 0.000 0.008  0
#&gt; SRR1274570     1  0.0622     0.9109 0.980 0.000 0.012 0.000 0.008  0
#&gt; SRR1274571     1  0.0622     0.9109 0.980 0.000 0.012 0.000 0.008  0
#&gt; SRR1274572     1  0.0458     0.9097 0.984 0.000 0.016 0.000 0.000  0
#&gt; SRR1274573     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274574     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274575     2  0.0000     0.9037 0.000 1.000 0.000 0.000 0.000  0
#&gt; SRR1274576     2  0.3828    -0.1379 0.000 0.560 0.000 0.440 0.000  0
#&gt; SRR1274577     4  0.3717     0.5507 0.000 0.384 0.000 0.616 0.000  0
#&gt; SRR1274578     1  0.0000     0.9101 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1274579     1  0.0000     0.9101 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1274580     1  0.0000     0.9101 1.000 0.000 0.000 0.000 0.000  0
#&gt; SRR1274581     6  0.0000     0.0000 0.000 0.000 0.000 0.000 0.000  1
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.975       0.989         0.4740 0.525   0.525
#> 3 3 0.829           0.889       0.926         0.3837 0.737   0.529
#> 4 4 0.722           0.699       0.822         0.1019 0.960   0.883
#> 5 5 0.724           0.676       0.793         0.0640 0.904   0.703
#> 6 6 0.738           0.683       0.783         0.0524 0.891   0.574
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.992 0.000 1.000
#&gt; SRR1274529     2   0.000      0.992 0.000 1.000
#&gt; SRR1274530     2   0.000      0.992 0.000 1.000
#&gt; SRR1274531     2   0.343      0.936 0.064 0.936
#&gt; SRR1274532     2   0.000      0.992 0.000 1.000
#&gt; SRR1274533     2   0.000      0.992 0.000 1.000
#&gt; SRR1274534     2   0.000      0.992 0.000 1.000
#&gt; SRR1274535     1   0.000      0.982 1.000 0.000
#&gt; SRR1274536     2   0.000      0.992 0.000 1.000
#&gt; SRR1274537     2   0.000      0.992 0.000 1.000
#&gt; SRR1274538     2   0.000      0.992 0.000 1.000
#&gt; SRR1274539     2   0.343      0.936 0.064 0.936
#&gt; SRR1274540     2   0.000      0.992 0.000 1.000
#&gt; SRR1274541     2   0.000      0.992 0.000 1.000
#&gt; SRR1274542     2   0.000      0.992 0.000 1.000
#&gt; SRR1274543     2   0.000      0.992 0.000 1.000
#&gt; SRR1274544     2   0.000      0.992 0.000 1.000
#&gt; SRR1274545     2   0.000      0.992 0.000 1.000
#&gt; SRR1274546     2   0.000      0.992 0.000 1.000
#&gt; SRR1274547     2   0.000      0.992 0.000 1.000
#&gt; SRR1274548     2   0.000      0.992 0.000 1.000
#&gt; SRR1274549     1   0.000      0.982 1.000 0.000
#&gt; SRR1274550     1   0.000      0.982 1.000 0.000
#&gt; SRR1274551     2   0.000      0.992 0.000 1.000
#&gt; SRR1274552     1   0.000      0.982 1.000 0.000
#&gt; SRR1274553     1   0.000      0.982 1.000 0.000
#&gt; SRR1274554     2   0.000      0.992 0.000 1.000
#&gt; SRR1274555     1   0.000      0.982 1.000 0.000
#&gt; SRR1274556     1   0.000      0.982 1.000 0.000
#&gt; SRR1274557     1   0.000      0.982 1.000 0.000
#&gt; SRR1274558     2   0.000      0.992 0.000 1.000
#&gt; SRR1274559     2   0.343      0.936 0.064 0.936
#&gt; SRR1274560     1   0.913      0.501 0.672 0.328
#&gt; SRR1274561     1   0.000      0.982 1.000 0.000
#&gt; SRR1274562     1   0.000      0.982 1.000 0.000
#&gt; SRR1274563     1   0.000      0.982 1.000 0.000
#&gt; SRR1274564     2   0.000      0.992 0.000 1.000
#&gt; SRR1274565     2   0.000      0.992 0.000 1.000
#&gt; SRR1274566     2   0.000      0.992 0.000 1.000
#&gt; SRR1274567     2   0.000      0.992 0.000 1.000
#&gt; SRR1274568     2   0.000      0.992 0.000 1.000
#&gt; SRR1274569     1   0.000      0.982 1.000 0.000
#&gt; SRR1274570     1   0.000      0.982 1.000 0.000
#&gt; SRR1274571     1   0.000      0.982 1.000 0.000
#&gt; SRR1274572     1   0.000      0.982 1.000 0.000
#&gt; SRR1274573     2   0.000      0.992 0.000 1.000
#&gt; SRR1274574     2   0.000      0.992 0.000 1.000
#&gt; SRR1274575     2   0.000      0.992 0.000 1.000
#&gt; SRR1274576     2   0.000      0.992 0.000 1.000
#&gt; SRR1274577     2   0.343      0.936 0.064 0.936
#&gt; SRR1274578     1   0.000      0.982 1.000 0.000
#&gt; SRR1274579     1   0.000      0.982 1.000 0.000
#&gt; SRR1274580     1   0.000      0.982 1.000 0.000
#&gt; SRR1274581     1   0.000      0.982 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0592      0.966 0.000 0.988 0.012
#&gt; SRR1274530     2  0.0592      0.966 0.000 0.988 0.012
#&gt; SRR1274531     3  0.2066      0.888 0.000 0.060 0.940
#&gt; SRR1274532     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274533     3  0.2796      0.890 0.000 0.092 0.908
#&gt; SRR1274534     3  0.2356      0.890 0.000 0.072 0.928
#&gt; SRR1274535     3  0.2050      0.854 0.028 0.020 0.952
#&gt; SRR1274536     3  0.2878      0.885 0.000 0.096 0.904
#&gt; SRR1274537     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274539     3  0.2356      0.890 0.000 0.072 0.928
#&gt; SRR1274540     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0592      0.966 0.000 0.988 0.012
#&gt; SRR1274546     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274548     2  0.2066      0.918 0.000 0.940 0.060
#&gt; SRR1274549     3  0.3192      0.767 0.112 0.000 0.888
#&gt; SRR1274550     1  0.1753      0.917 0.952 0.000 0.048
#&gt; SRR1274551     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274552     1  0.4399      0.877 0.812 0.000 0.188
#&gt; SRR1274553     1  0.3686      0.915 0.860 0.000 0.140
#&gt; SRR1274554     3  0.3038      0.886 0.000 0.104 0.896
#&gt; SRR1274555     1  0.1753      0.917 0.952 0.000 0.048
#&gt; SRR1274556     1  0.2066      0.913 0.940 0.000 0.060
#&gt; SRR1274557     1  0.1753      0.917 0.952 0.000 0.048
#&gt; SRR1274558     2  0.5760      0.440 0.000 0.672 0.328
#&gt; SRR1274559     3  0.2066      0.888 0.000 0.060 0.940
#&gt; SRR1274560     3  0.1529      0.833 0.040 0.000 0.960
#&gt; SRR1274561     3  0.5859      0.295 0.344 0.000 0.656
#&gt; SRR1274562     1  0.0000      0.912 1.000 0.000 0.000
#&gt; SRR1274563     1  0.1753      0.917 0.952 0.000 0.048
#&gt; SRR1274564     3  0.6286      0.196 0.000 0.464 0.536
#&gt; SRR1274565     2  0.2537      0.904 0.000 0.920 0.080
#&gt; SRR1274566     3  0.4235      0.804 0.000 0.176 0.824
#&gt; SRR1274567     3  0.2878      0.885 0.000 0.096 0.904
#&gt; SRR1274568     3  0.3038      0.886 0.000 0.104 0.896
#&gt; SRR1274569     1  0.3267      0.925 0.884 0.000 0.116
#&gt; SRR1274570     1  0.3192      0.925 0.888 0.000 0.112
#&gt; SRR1274571     1  0.3267      0.925 0.884 0.000 0.116
#&gt; SRR1274572     1  0.3192      0.925 0.888 0.000 0.112
#&gt; SRR1274573     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0592      0.966 0.000 0.988 0.012
#&gt; SRR1274576     2  0.0000      0.972 0.000 1.000 0.000
#&gt; SRR1274577     3  0.2356      0.890 0.000 0.072 0.928
#&gt; SRR1274578     1  0.3267      0.925 0.884 0.000 0.116
#&gt; SRR1274579     1  0.3267      0.925 0.884 0.000 0.116
#&gt; SRR1274580     1  0.3267      0.925 0.884 0.000 0.116
#&gt; SRR1274581     1  0.2066      0.913 0.940 0.000 0.060
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.4567    0.71436 0.000 0.740 0.244 0.016
#&gt; SRR1274530     2  0.4661    0.70090 0.000 0.728 0.256 0.016
#&gt; SRR1274531     4  0.3545    0.67268 0.000 0.008 0.164 0.828
#&gt; SRR1274532     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274533     4  0.1109    0.81929 0.004 0.028 0.000 0.968
#&gt; SRR1274534     4  0.1109    0.81929 0.004 0.028 0.000 0.968
#&gt; SRR1274535     4  0.1151    0.80494 0.024 0.000 0.008 0.968
#&gt; SRR1274536     4  0.4955    0.28815 0.000 0.008 0.344 0.648
#&gt; SRR1274537     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.2647    0.82096 0.000 0.880 0.120 0.000
#&gt; SRR1274539     4  0.1004    0.82170 0.004 0.024 0.000 0.972
#&gt; SRR1274540     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.2589    0.82235 0.000 0.884 0.116 0.000
#&gt; SRR1274544     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.3695    0.79442 0.000 0.828 0.156 0.016
#&gt; SRR1274546     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.3024    0.80825 0.000 0.852 0.148 0.000
#&gt; SRR1274548     2  0.5200    0.70654 0.000 0.744 0.184 0.072
#&gt; SRR1274549     4  0.6469    0.44884 0.164 0.000 0.192 0.644
#&gt; SRR1274550     1  0.4989    0.68384 0.528 0.000 0.472 0.000
#&gt; SRR1274551     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274552     1  0.4993    0.56856 0.712 0.000 0.028 0.260
#&gt; SRR1274553     1  0.5003    0.71849 0.768 0.000 0.148 0.084
#&gt; SRR1274554     4  0.1109    0.81929 0.004 0.028 0.000 0.968
#&gt; SRR1274555     1  0.4989    0.68384 0.528 0.000 0.472 0.000
#&gt; SRR1274556     1  0.5000    0.66808 0.500 0.000 0.500 0.000
#&gt; SRR1274557     1  0.4746    0.70723 0.632 0.000 0.368 0.000
#&gt; SRR1274558     2  0.7301   -0.24999 0.000 0.452 0.152 0.396
#&gt; SRR1274559     4  0.0524    0.81368 0.004 0.008 0.000 0.988
#&gt; SRR1274560     4  0.2699    0.77668 0.028 0.000 0.068 0.904
#&gt; SRR1274561     1  0.6137   -0.00967 0.504 0.000 0.048 0.448
#&gt; SRR1274562     1  0.4985    0.68471 0.532 0.000 0.468 0.000
#&gt; SRR1274563     1  0.4989    0.68384 0.528 0.000 0.472 0.000
#&gt; SRR1274564     3  0.7529    0.64235 0.000 0.224 0.488 0.288
#&gt; SRR1274565     2  0.6616    0.40970 0.000 0.584 0.308 0.108
#&gt; SRR1274566     3  0.6495    0.50206 0.000 0.072 0.492 0.436
#&gt; SRR1274567     4  0.4955    0.28815 0.000 0.008 0.344 0.648
#&gt; SRR1274568     4  0.1004    0.82170 0.004 0.024 0.000 0.972
#&gt; SRR1274569     1  0.0921    0.73614 0.972 0.000 0.000 0.028
#&gt; SRR1274570     1  0.0817    0.73651 0.976 0.000 0.000 0.024
#&gt; SRR1274571     1  0.0921    0.73614 0.972 0.000 0.000 0.028
#&gt; SRR1274572     1  0.0817    0.73651 0.976 0.000 0.000 0.024
#&gt; SRR1274573     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000    0.84990 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.4661    0.70090 0.000 0.728 0.256 0.016
#&gt; SRR1274576     2  0.3384    0.81352 0.000 0.860 0.116 0.024
#&gt; SRR1274577     4  0.1004    0.82170 0.004 0.024 0.000 0.972
#&gt; SRR1274578     1  0.0921    0.73614 0.972 0.000 0.000 0.028
#&gt; SRR1274579     1  0.0921    0.73614 0.972 0.000 0.000 0.028
#&gt; SRR1274580     1  0.0921    0.73614 0.972 0.000 0.000 0.028
#&gt; SRR1274581     1  0.5296    0.66803 0.500 0.000 0.492 0.008
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0609      0.811 0.000 0.980 0.020 0.000 0.000
#&gt; SRR1274529     2  0.6225      0.563 0.000 0.544 0.200 0.256 0.000
#&gt; SRR1274530     2  0.6286      0.554 0.000 0.532 0.204 0.264 0.000
#&gt; SRR1274531     5  0.3790      0.420 0.000 0.000 0.004 0.272 0.724
#&gt; SRR1274532     2  0.0000      0.814 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.0000      0.812 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274534     5  0.0000      0.812 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274535     5  0.0404      0.803 0.000 0.000 0.000 0.012 0.988
#&gt; SRR1274536     4  0.3932      0.566 0.000 0.000 0.000 0.672 0.328
#&gt; SRR1274537     2  0.0703      0.810 0.000 0.976 0.024 0.000 0.000
#&gt; SRR1274538     2  0.4020      0.766 0.000 0.796 0.108 0.096 0.000
#&gt; SRR1274539     5  0.0000      0.812 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274540     2  0.0000      0.814 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.814 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.814 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.3967      0.768 0.000 0.800 0.108 0.092 0.000
#&gt; SRR1274544     2  0.0000      0.814 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.4883      0.721 0.000 0.708 0.200 0.092 0.000
#&gt; SRR1274546     2  0.0000      0.814 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.5082      0.711 0.000 0.684 0.220 0.096 0.000
#&gt; SRR1274548     2  0.7454      0.537 0.000 0.536 0.164 0.144 0.156
#&gt; SRR1274549     4  0.6317      0.172 0.144 0.000 0.004 0.496 0.356
#&gt; SRR1274550     3  0.3876      0.904 0.316 0.000 0.684 0.000 0.000
#&gt; SRR1274551     2  0.0000      0.814 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     1  0.7145      0.376 0.548 0.000 0.084 0.140 0.228
#&gt; SRR1274553     1  0.7125      0.350 0.576 0.000 0.136 0.136 0.152
#&gt; SRR1274554     5  0.0000      0.812 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274555     3  0.3876      0.904 0.316 0.000 0.684 0.000 0.000
#&gt; SRR1274556     3  0.3480      0.857 0.248 0.000 0.752 0.000 0.000
#&gt; SRR1274557     3  0.5376      0.642 0.424 0.000 0.520 0.056 0.000
#&gt; SRR1274558     5  0.7694     -0.123 0.000 0.316 0.116 0.128 0.440
#&gt; SRR1274559     5  0.0579      0.803 0.000 0.000 0.008 0.008 0.984
#&gt; SRR1274560     5  0.3835      0.457 0.000 0.000 0.008 0.260 0.732
#&gt; SRR1274561     1  0.7040     -0.023 0.368 0.000 0.008 0.320 0.304
#&gt; SRR1274562     3  0.3949      0.895 0.332 0.000 0.668 0.000 0.000
#&gt; SRR1274563     3  0.3876      0.904 0.316 0.000 0.684 0.000 0.000
#&gt; SRR1274564     4  0.6469      0.558 0.000 0.064 0.132 0.628 0.176
#&gt; SRR1274565     2  0.7607      0.243 0.000 0.388 0.168 0.372 0.072
#&gt; SRR1274566     4  0.6195      0.577 0.000 0.036 0.128 0.632 0.204
#&gt; SRR1274567     4  0.3932      0.566 0.000 0.000 0.000 0.672 0.328
#&gt; SRR1274568     5  0.0290      0.809 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1274569     1  0.1671      0.720 0.924 0.000 0.000 0.076 0.000
#&gt; SRR1274570     1  0.0609      0.738 0.980 0.000 0.000 0.020 0.000
#&gt; SRR1274571     1  0.1410      0.728 0.940 0.000 0.000 0.060 0.000
#&gt; SRR1274572     1  0.0000      0.737 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.814 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.814 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.6286      0.554 0.000 0.532 0.204 0.264 0.000
#&gt; SRR1274576     2  0.5787      0.709 0.000 0.704 0.112 0.092 0.092
#&gt; SRR1274577     5  0.0000      0.812 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274578     1  0.0404      0.738 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1274579     1  0.0404      0.738 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1274580     1  0.0404      0.738 0.988 0.000 0.000 0.012 0.000
#&gt; SRR1274581     3  0.5010      0.812 0.248 0.000 0.676 0.076 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.1053    0.84093 0.000 0.964 0.004 0.012 0.000 0.020
#&gt; SRR1274529     6  0.5100    0.64194 0.000 0.328 0.056 0.020 0.000 0.596
#&gt; SRR1274530     6  0.4965    0.66210 0.000 0.296 0.036 0.036 0.000 0.632
#&gt; SRR1274531     4  0.4532    0.49560 0.004 0.000 0.000 0.508 0.464 0.024
#&gt; SRR1274532     2  0.0000    0.86378 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.0146    0.87136 0.000 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1274534     5  0.0146    0.87136 0.000 0.004 0.000 0.000 0.996 0.000
#&gt; SRR1274535     5  0.0508    0.85961 0.004 0.000 0.000 0.012 0.984 0.000
#&gt; SRR1274536     4  0.5470    0.64831 0.000 0.000 0.016 0.620 0.160 0.204
#&gt; SRR1274537     2  0.1218    0.83453 0.000 0.956 0.004 0.012 0.000 0.028
#&gt; SRR1274538     2  0.4419    0.33237 0.000 0.656 0.028 0.012 0.000 0.304
#&gt; SRR1274539     5  0.0146    0.87009 0.004 0.000 0.000 0.000 0.996 0.000
#&gt; SRR1274540     2  0.0000    0.86378 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000    0.86378 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000    0.86378 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.4401    0.34365 0.000 0.660 0.028 0.012 0.000 0.300
#&gt; SRR1274544     2  0.0000    0.86378 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     6  0.5238    0.49476 0.000 0.436 0.056 0.016 0.000 0.492
#&gt; SRR1274546     2  0.0000    0.86378 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     6  0.5088    0.51939 0.000 0.412 0.036 0.024 0.000 0.528
#&gt; SRR1274548     6  0.6709    0.27491 0.000 0.384 0.040 0.016 0.140 0.420
#&gt; SRR1274549     4  0.4348    0.66501 0.064 0.000 0.000 0.748 0.164 0.024
#&gt; SRR1274550     3  0.2527    0.90764 0.168 0.000 0.832 0.000 0.000 0.000
#&gt; SRR1274551     2  0.0000    0.86378 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     1  0.7786    0.22520 0.380 0.000 0.072 0.312 0.176 0.060
#&gt; SRR1274553     1  0.8017    0.24148 0.384 0.000 0.168 0.276 0.112 0.060
#&gt; SRR1274554     5  0.0436    0.86946 0.000 0.004 0.000 0.004 0.988 0.004
#&gt; SRR1274555     3  0.2527    0.90764 0.168 0.000 0.832 0.000 0.000 0.000
#&gt; SRR1274556     3  0.2488    0.88067 0.124 0.000 0.864 0.008 0.004 0.000
#&gt; SRR1274557     3  0.4632    0.70186 0.276 0.000 0.656 0.064 0.000 0.004
#&gt; SRR1274558     5  0.6854   -0.04000 0.000 0.168 0.044 0.016 0.448 0.324
#&gt; SRR1274559     5  0.1602    0.84405 0.004 0.000 0.016 0.020 0.944 0.016
#&gt; SRR1274560     4  0.4239    0.49624 0.004 0.000 0.004 0.536 0.452 0.004
#&gt; SRR1274561     4  0.5071    0.53657 0.172 0.000 0.004 0.664 0.156 0.004
#&gt; SRR1274562     3  0.3012    0.89198 0.196 0.000 0.796 0.008 0.000 0.000
#&gt; SRR1274563     3  0.2527    0.90764 0.168 0.000 0.832 0.000 0.000 0.000
#&gt; SRR1274564     6  0.5228    0.27782 0.000 0.012 0.024 0.224 0.072 0.668
#&gt; SRR1274565     6  0.5053    0.62306 0.000 0.196 0.048 0.044 0.012 0.700
#&gt; SRR1274566     6  0.5036    0.23764 0.000 0.000 0.024 0.232 0.080 0.664
#&gt; SRR1274567     4  0.5470    0.64831 0.000 0.000 0.016 0.620 0.160 0.204
#&gt; SRR1274568     5  0.1261    0.85194 0.004 0.000 0.028 0.004 0.956 0.008
#&gt; SRR1274569     1  0.2053    0.76947 0.888 0.000 0.000 0.108 0.000 0.004
#&gt; SRR1274570     1  0.0937    0.79861 0.960 0.000 0.000 0.040 0.000 0.000
#&gt; SRR1274571     1  0.1267    0.79435 0.940 0.000 0.000 0.060 0.000 0.000
#&gt; SRR1274572     1  0.0000    0.79952 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000    0.86378 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000    0.86378 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     6  0.4965    0.66210 0.000 0.296 0.036 0.036 0.000 0.632
#&gt; SRR1274576     2  0.6389   -0.00487 0.000 0.516 0.040 0.012 0.124 0.308
#&gt; SRR1274577     5  0.0291    0.87056 0.004 0.000 0.004 0.000 0.992 0.000
#&gt; SRR1274578     1  0.0858    0.79942 0.968 0.000 0.000 0.004 0.000 0.028
#&gt; SRR1274579     1  0.0858    0.79942 0.968 0.000 0.000 0.004 0.000 0.028
#&gt; SRR1274580     1  0.0858    0.79942 0.968 0.000 0.000 0.004 0.000 0.028
#&gt; SRR1274581     3  0.5092    0.77700 0.120 0.000 0.712 0.084 0.000 0.084
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.957       0.984         0.5066 0.497   0.497
#> 3 3 0.976           0.951       0.975         0.2101 0.875   0.752
#> 4 4 0.929           0.903       0.959         0.1219 0.906   0.762
#> 5 5 0.832           0.828       0.860         0.0702 0.916   0.737
#> 6 6 0.817           0.776       0.861         0.0339 0.980   0.923
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.969 0.000 1.000
#&gt; SRR1274529     2   0.000      0.969 0.000 1.000
#&gt; SRR1274530     2   0.000      0.969 0.000 1.000
#&gt; SRR1274531     1   0.000      1.000 1.000 0.000
#&gt; SRR1274532     2   0.000      0.969 0.000 1.000
#&gt; SRR1274533     2   0.327      0.913 0.060 0.940
#&gt; SRR1274534     2   0.955      0.412 0.376 0.624
#&gt; SRR1274535     1   0.000      1.000 1.000 0.000
#&gt; SRR1274536     2   0.000      0.969 0.000 1.000
#&gt; SRR1274537     2   0.000      0.969 0.000 1.000
#&gt; SRR1274538     2   0.000      0.969 0.000 1.000
#&gt; SRR1274539     1   0.000      1.000 1.000 0.000
#&gt; SRR1274540     2   0.000      0.969 0.000 1.000
#&gt; SRR1274541     2   0.000      0.969 0.000 1.000
#&gt; SRR1274542     2   0.000      0.969 0.000 1.000
#&gt; SRR1274543     2   0.000      0.969 0.000 1.000
#&gt; SRR1274544     2   0.000      0.969 0.000 1.000
#&gt; SRR1274545     2   0.000      0.969 0.000 1.000
#&gt; SRR1274546     2   0.000      0.969 0.000 1.000
#&gt; SRR1274547     2   0.000      0.969 0.000 1.000
#&gt; SRR1274548     2   0.000      0.969 0.000 1.000
#&gt; SRR1274549     1   0.000      1.000 1.000 0.000
#&gt; SRR1274550     1   0.000      1.000 1.000 0.000
#&gt; SRR1274551     2   0.000      0.969 0.000 1.000
#&gt; SRR1274552     1   0.000      1.000 1.000 0.000
#&gt; SRR1274553     1   0.000      1.000 1.000 0.000
#&gt; SRR1274554     2   0.000      0.969 0.000 1.000
#&gt; SRR1274555     1   0.000      1.000 1.000 0.000
#&gt; SRR1274556     1   0.000      1.000 1.000 0.000
#&gt; SRR1274557     1   0.000      1.000 1.000 0.000
#&gt; SRR1274558     2   0.000      0.969 0.000 1.000
#&gt; SRR1274559     1   0.000      1.000 1.000 0.000
#&gt; SRR1274560     1   0.000      1.000 1.000 0.000
#&gt; SRR1274561     1   0.000      1.000 1.000 0.000
#&gt; SRR1274562     1   0.000      1.000 1.000 0.000
#&gt; SRR1274563     1   0.000      1.000 1.000 0.000
#&gt; SRR1274564     2   0.000      0.969 0.000 1.000
#&gt; SRR1274565     2   0.000      0.969 0.000 1.000
#&gt; SRR1274566     2   0.000      0.969 0.000 1.000
#&gt; SRR1274567     2   0.000      0.969 0.000 1.000
#&gt; SRR1274568     2   0.992      0.201 0.448 0.552
#&gt; SRR1274569     1   0.000      1.000 1.000 0.000
#&gt; SRR1274570     1   0.000      1.000 1.000 0.000
#&gt; SRR1274571     1   0.000      1.000 1.000 0.000
#&gt; SRR1274572     1   0.000      1.000 1.000 0.000
#&gt; SRR1274573     2   0.000      0.969 0.000 1.000
#&gt; SRR1274574     2   0.000      0.969 0.000 1.000
#&gt; SRR1274575     2   0.000      0.969 0.000 1.000
#&gt; SRR1274576     2   0.000      0.969 0.000 1.000
#&gt; SRR1274577     1   0.000      1.000 1.000 0.000
#&gt; SRR1274578     1   0.000      1.000 1.000 0.000
#&gt; SRR1274579     1   0.000      1.000 1.000 0.000
#&gt; SRR1274580     1   0.000      1.000 1.000 0.000
#&gt; SRR1274581     1   0.000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274530     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274531     1  0.6026      0.397 0.624 0.000 0.376
#&gt; SRR1274532     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274533     3  0.1267      0.920 0.004 0.024 0.972
#&gt; SRR1274534     3  0.0983      0.920 0.004 0.016 0.980
#&gt; SRR1274535     3  0.4842      0.712 0.224 0.000 0.776
#&gt; SRR1274536     2  0.1163      0.973 0.000 0.972 0.028
#&gt; SRR1274537     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274539     3  0.0892      0.915 0.020 0.000 0.980
#&gt; SRR1274540     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274546     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274549     1  0.1289      0.952 0.968 0.000 0.032
#&gt; SRR1274550     1  0.0747      0.960 0.984 0.000 0.016
#&gt; SRR1274551     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274552     1  0.0747      0.960 0.984 0.000 0.016
#&gt; SRR1274553     1  0.0747      0.960 0.984 0.000 0.016
#&gt; SRR1274554     3  0.1411      0.915 0.000 0.036 0.964
#&gt; SRR1274555     1  0.0747      0.960 0.984 0.000 0.016
#&gt; SRR1274556     1  0.0747      0.960 0.984 0.000 0.016
#&gt; SRR1274557     1  0.0747      0.960 0.984 0.000 0.016
#&gt; SRR1274558     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274559     1  0.4346      0.757 0.816 0.000 0.184
#&gt; SRR1274560     1  0.1031      0.946 0.976 0.000 0.024
#&gt; SRR1274561     1  0.0000      0.961 1.000 0.000 0.000
#&gt; SRR1274562     1  0.0000      0.961 1.000 0.000 0.000
#&gt; SRR1274563     1  0.0747      0.960 0.984 0.000 0.016
#&gt; SRR1274564     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274565     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274566     2  0.0747      0.984 0.000 0.984 0.016
#&gt; SRR1274567     2  0.1163      0.973 0.000 0.972 0.028
#&gt; SRR1274568     3  0.4411      0.816 0.016 0.140 0.844
#&gt; SRR1274569     1  0.0000      0.961 1.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.961 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.961 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.961 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274576     2  0.0000      0.997 0.000 1.000 0.000
#&gt; SRR1274577     3  0.1289      0.912 0.032 0.000 0.968
#&gt; SRR1274578     1  0.0000      0.961 1.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.961 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.961 1.000 0.000 0.000
#&gt; SRR1274581     1  0.0747      0.960 0.984 0.000 0.016
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.0188      0.996 0.000 0.996 0.000 0.004
#&gt; SRR1274530     2  0.0188      0.996 0.000 0.996 0.000 0.004
#&gt; SRR1274531     4  0.0804      0.718 0.008 0.000 0.012 0.980
#&gt; SRR1274532     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274533     3  0.0000      0.877 0.000 0.000 1.000 0.000
#&gt; SRR1274534     3  0.0000      0.877 0.000 0.000 1.000 0.000
#&gt; SRR1274535     3  0.3873      0.633 0.228 0.000 0.772 0.000
#&gt; SRR1274536     4  0.0000      0.724 0.000 0.000 0.000 1.000
#&gt; SRR1274537     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274539     3  0.0000      0.877 0.000 0.000 1.000 0.000
#&gt; SRR1274540     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274549     4  0.4866      0.289 0.404 0.000 0.000 0.596
#&gt; SRR1274550     1  0.1211      0.950 0.960 0.000 0.040 0.000
#&gt; SRR1274551     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274552     1  0.1211      0.950 0.960 0.000 0.040 0.000
#&gt; SRR1274553     1  0.1211      0.950 0.960 0.000 0.040 0.000
#&gt; SRR1274554     3  0.0336      0.871 0.000 0.008 0.992 0.000
#&gt; SRR1274555     1  0.1211      0.950 0.960 0.000 0.040 0.000
#&gt; SRR1274556     1  0.1211      0.950 0.960 0.000 0.040 0.000
#&gt; SRR1274557     1  0.1211      0.950 0.960 0.000 0.040 0.000
#&gt; SRR1274558     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274559     1  0.3688      0.734 0.792 0.000 0.208 0.000
#&gt; SRR1274560     1  0.3873      0.685 0.772 0.000 0.000 0.228
#&gt; SRR1274561     1  0.0000      0.953 1.000 0.000 0.000 0.000
#&gt; SRR1274562     1  0.0000      0.953 1.000 0.000 0.000 0.000
#&gt; SRR1274563     1  0.1211      0.950 0.960 0.000 0.040 0.000
#&gt; SRR1274564     4  0.4454      0.499 0.000 0.308 0.000 0.692
#&gt; SRR1274565     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274566     4  0.2647      0.683 0.000 0.120 0.000 0.880
#&gt; SRR1274567     4  0.0000      0.724 0.000 0.000 0.000 1.000
#&gt; SRR1274568     3  0.5610      0.583 0.032 0.008 0.668 0.292
#&gt; SRR1274569     1  0.0000      0.953 1.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.953 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.953 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.953 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.0188      0.996 0.000 0.996 0.000 0.004
#&gt; SRR1274576     2  0.0000      0.999 0.000 1.000 0.000 0.000
#&gt; SRR1274577     3  0.1211      0.857 0.040 0.000 0.960 0.000
#&gt; SRR1274578     1  0.0000      0.953 1.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.953 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.953 1.000 0.000 0.000 0.000
#&gt; SRR1274581     1  0.1211      0.950 0.960 0.000 0.040 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.2771      0.866 0.012 0.860 0.000 0.128 0.000
#&gt; SRR1274530     2  0.2909      0.854 0.012 0.848 0.000 0.140 0.000
#&gt; SRR1274531     4  0.6739      0.404 0.224 0.000 0.288 0.480 0.008
#&gt; SRR1274532     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.0510      0.872 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1274534     5  0.0162      0.874 0.004 0.000 0.000 0.000 0.996
#&gt; SRR1274535     3  0.5142      0.463 0.088 0.000 0.668 0.000 0.244
#&gt; SRR1274536     4  0.1121      0.798 0.044 0.000 0.000 0.956 0.000
#&gt; SRR1274537     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.0510      0.873 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1274540     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.1522      0.938 0.012 0.944 0.000 0.044 0.000
#&gt; SRR1274546     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0324      0.968 0.004 0.992 0.000 0.004 0.000
#&gt; SRR1274548     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274549     3  0.5174      0.335 0.056 0.000 0.604 0.340 0.000
#&gt; SRR1274550     3  0.0000      0.839 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274551     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.0000      0.839 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274553     3  0.0000      0.839 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274554     5  0.0703      0.869 0.024 0.000 0.000 0.000 0.976
#&gt; SRR1274555     3  0.0000      0.839 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     3  0.0000      0.839 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274557     3  0.0000      0.839 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274558     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274559     1  0.6396      0.444 0.512 0.000 0.264 0.000 0.224
#&gt; SRR1274560     1  0.3810      0.583 0.792 0.000 0.168 0.040 0.000
#&gt; SRR1274561     1  0.4300      0.763 0.524 0.000 0.476 0.000 0.000
#&gt; SRR1274562     3  0.3586      0.152 0.264 0.000 0.736 0.000 0.000
#&gt; SRR1274563     3  0.0000      0.839 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274564     4  0.2416      0.702 0.012 0.100 0.000 0.888 0.000
#&gt; SRR1274565     2  0.1877      0.924 0.012 0.924 0.000 0.064 0.000
#&gt; SRR1274566     4  0.0693      0.786 0.012 0.008 0.000 0.980 0.000
#&gt; SRR1274567     4  0.1121      0.798 0.044 0.000 0.000 0.956 0.000
#&gt; SRR1274568     5  0.5605      0.537 0.404 0.000 0.000 0.076 0.520
#&gt; SRR1274569     1  0.4278      0.799 0.548 0.000 0.452 0.000 0.000
#&gt; SRR1274570     1  0.4182      0.863 0.600 0.000 0.400 0.000 0.000
#&gt; SRR1274571     1  0.4182      0.863 0.600 0.000 0.400 0.000 0.000
#&gt; SRR1274572     1  0.4182      0.863 0.600 0.000 0.400 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.2909      0.854 0.012 0.848 0.000 0.140 0.000
#&gt; SRR1274576     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274577     5  0.3427      0.788 0.192 0.000 0.012 0.000 0.796
#&gt; SRR1274578     1  0.4182      0.863 0.600 0.000 0.400 0.000 0.000
#&gt; SRR1274579     1  0.4182      0.863 0.600 0.000 0.400 0.000 0.000
#&gt; SRR1274580     1  0.4182      0.863 0.600 0.000 0.400 0.000 0.000
#&gt; SRR1274581     3  0.0000      0.839 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.4107     0.7778 0.000 0.768 0.024 0.052 0.000 0.156
#&gt; SRR1274530     2  0.4202     0.7617 0.000 0.756 0.012 0.080 0.000 0.152
#&gt; SRR1274531     4  0.5947     0.0802 0.000 0.000 0.404 0.408 0.004 0.184
#&gt; SRR1274532     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.1003     0.8775 0.000 0.000 0.016 0.000 0.964 0.020
#&gt; SRR1274534     5  0.1408     0.8875 0.000 0.000 0.020 0.000 0.944 0.036
#&gt; SRR1274535     3  0.5668     0.5476 0.088 0.000 0.656 0.000 0.140 0.116
#&gt; SRR1274536     4  0.0146     0.6797 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1274537     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.1845     0.8727 0.000 0.000 0.028 0.000 0.920 0.052
#&gt; SRR1274540     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.2730     0.8414 0.000 0.836 0.012 0.000 0.000 0.152
#&gt; SRR1274546     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.1007     0.9243 0.000 0.956 0.000 0.000 0.000 0.044
#&gt; SRR1274548     2  0.0458     0.9392 0.000 0.984 0.000 0.000 0.000 0.016
#&gt; SRR1274549     3  0.5876     0.3720 0.160 0.000 0.476 0.356 0.000 0.008
#&gt; SRR1274550     3  0.2854     0.9022 0.208 0.000 0.792 0.000 0.000 0.000
#&gt; SRR1274551     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     3  0.2994     0.9008 0.208 0.000 0.788 0.000 0.000 0.004
#&gt; SRR1274553     3  0.2994     0.9008 0.208 0.000 0.788 0.000 0.000 0.004
#&gt; SRR1274554     5  0.1713     0.8539 0.000 0.000 0.028 0.000 0.928 0.044
#&gt; SRR1274555     3  0.2854     0.9022 0.208 0.000 0.792 0.000 0.000 0.000
#&gt; SRR1274556     3  0.2854     0.9022 0.208 0.000 0.792 0.000 0.000 0.000
#&gt; SRR1274557     3  0.2854     0.9022 0.208 0.000 0.792 0.000 0.000 0.000
#&gt; SRR1274558     2  0.0260     0.9423 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1274559     1  0.7388     0.0523 0.376 0.000 0.228 0.000 0.264 0.132
#&gt; SRR1274560     1  0.4901     0.5124 0.708 0.000 0.100 0.032 0.000 0.160
#&gt; SRR1274561     1  0.2814     0.6513 0.820 0.000 0.172 0.000 0.000 0.008
#&gt; SRR1274562     1  0.3868    -0.3356 0.504 0.000 0.496 0.000 0.000 0.000
#&gt; SRR1274563     3  0.2854     0.9022 0.208 0.000 0.792 0.000 0.000 0.000
#&gt; SRR1274564     4  0.3881     0.6247 0.000 0.040 0.024 0.784 0.000 0.152
#&gt; SRR1274565     2  0.3399     0.8245 0.000 0.816 0.024 0.020 0.000 0.140
#&gt; SRR1274566     4  0.3084     0.6612 0.000 0.008 0.024 0.832 0.000 0.136
#&gt; SRR1274567     4  0.0146     0.6820 0.000 0.000 0.000 0.996 0.000 0.004
#&gt; SRR1274568     6  0.4376     0.6277 0.036 0.000 0.004 0.056 0.140 0.764
#&gt; SRR1274569     1  0.1967     0.7497 0.904 0.000 0.084 0.000 0.000 0.012
#&gt; SRR1274570     1  0.0622     0.7987 0.980 0.000 0.008 0.000 0.000 0.012
#&gt; SRR1274571     1  0.0622     0.7987 0.980 0.000 0.008 0.000 0.000 0.012
#&gt; SRR1274572     1  0.0260     0.7999 0.992 0.000 0.008 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.9462 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     2  0.4202     0.7617 0.000 0.756 0.012 0.080 0.000 0.152
#&gt; SRR1274576     2  0.0260     0.9424 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1274577     6  0.4426     0.5039 0.004 0.000 0.024 0.000 0.388 0.584
#&gt; SRR1274578     1  0.0458     0.7996 0.984 0.000 0.000 0.000 0.000 0.016
#&gt; SRR1274579     1  0.0458     0.7996 0.984 0.000 0.000 0.000 0.000 0.016
#&gt; SRR1274580     1  0.0458     0.7996 0.984 0.000 0.000 0.000 0.000 0.016
#&gt; SRR1274581     3  0.2883     0.8991 0.212 0.000 0.788 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.823           0.888       0.957         0.4803 0.525   0.525
#> 3 3 0.929           0.913       0.966         0.4073 0.739   0.530
#> 4 4 0.985           0.921       0.968         0.0842 0.916   0.750
#> 5 5 0.857           0.792       0.919         0.0692 0.915   0.697
#> 6 6 0.908           0.829       0.937         0.0202 0.963   0.831
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 3 4
```

There is also optional best $k$ = 3 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.944 0.000 1.000
#&gt; SRR1274529     2   0.000      0.944 0.000 1.000
#&gt; SRR1274530     2   0.000      0.944 0.000 1.000
#&gt; SRR1274531     2   0.969      0.375 0.396 0.604
#&gt; SRR1274532     2   0.000      0.944 0.000 1.000
#&gt; SRR1274533     2   0.118      0.935 0.016 0.984
#&gt; SRR1274534     2   0.118      0.935 0.016 0.984
#&gt; SRR1274535     1   0.983      0.175 0.576 0.424
#&gt; SRR1274536     2   0.969      0.375 0.396 0.604
#&gt; SRR1274537     2   0.000      0.944 0.000 1.000
#&gt; SRR1274538     2   0.000      0.944 0.000 1.000
#&gt; SRR1274539     2   0.184      0.927 0.028 0.972
#&gt; SRR1274540     2   0.000      0.944 0.000 1.000
#&gt; SRR1274541     2   0.000      0.944 0.000 1.000
#&gt; SRR1274542     2   0.000      0.944 0.000 1.000
#&gt; SRR1274543     2   0.000      0.944 0.000 1.000
#&gt; SRR1274544     2   0.000      0.944 0.000 1.000
#&gt; SRR1274545     2   0.000      0.944 0.000 1.000
#&gt; SRR1274546     2   0.000      0.944 0.000 1.000
#&gt; SRR1274547     2   0.000      0.944 0.000 1.000
#&gt; SRR1274548     2   0.000      0.944 0.000 1.000
#&gt; SRR1274549     1   0.000      0.964 1.000 0.000
#&gt; SRR1274550     1   0.000      0.964 1.000 0.000
#&gt; SRR1274551     2   0.000      0.944 0.000 1.000
#&gt; SRR1274552     1   0.000      0.964 1.000 0.000
#&gt; SRR1274553     1   0.000      0.964 1.000 0.000
#&gt; SRR1274554     2   0.118      0.935 0.016 0.984
#&gt; SRR1274555     1   0.000      0.964 1.000 0.000
#&gt; SRR1274556     1   0.000      0.964 1.000 0.000
#&gt; SRR1274557     1   0.000      0.964 1.000 0.000
#&gt; SRR1274558     2   0.000      0.944 0.000 1.000
#&gt; SRR1274559     2   0.969      0.375 0.396 0.604
#&gt; SRR1274560     1   0.722      0.717 0.800 0.200
#&gt; SRR1274561     1   0.000      0.964 1.000 0.000
#&gt; SRR1274562     1   0.000      0.964 1.000 0.000
#&gt; SRR1274563     1   0.000      0.964 1.000 0.000
#&gt; SRR1274564     2   0.000      0.944 0.000 1.000
#&gt; SRR1274565     2   0.000      0.944 0.000 1.000
#&gt; SRR1274566     2   0.000      0.944 0.000 1.000
#&gt; SRR1274567     2   0.969      0.375 0.396 0.604
#&gt; SRR1274568     2   0.184      0.927 0.028 0.972
#&gt; SRR1274569     1   0.000      0.964 1.000 0.000
#&gt; SRR1274570     1   0.000      0.964 1.000 0.000
#&gt; SRR1274571     1   0.000      0.964 1.000 0.000
#&gt; SRR1274572     1   0.000      0.964 1.000 0.000
#&gt; SRR1274573     2   0.000      0.944 0.000 1.000
#&gt; SRR1274574     2   0.000      0.944 0.000 1.000
#&gt; SRR1274575     2   0.000      0.944 0.000 1.000
#&gt; SRR1274576     2   0.000      0.944 0.000 1.000
#&gt; SRR1274577     2   0.163      0.930 0.024 0.976
#&gt; SRR1274578     1   0.000      0.964 1.000 0.000
#&gt; SRR1274579     1   0.000      0.964 1.000 0.000
#&gt; SRR1274580     1   0.000      0.964 1.000 0.000
#&gt; SRR1274581     1   0.000      0.964 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274529     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274530     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274531     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274532     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274533     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274534     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274535     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274536     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274537     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0237      0.996 0.000 0.996 0.004
#&gt; SRR1274539     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274540     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274543     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274544     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274545     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274546     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274547     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274548     2  0.0592      0.988 0.000 0.988 0.012
#&gt; SRR1274549     3  0.6244      0.101 0.440 0.000 0.560
#&gt; SRR1274550     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274551     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274552     1  0.6126      0.382 0.600 0.000 0.400
#&gt; SRR1274553     1  0.0892      0.920 0.980 0.000 0.020
#&gt; SRR1274554     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274555     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274556     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274557     1  0.6095      0.402 0.608 0.000 0.392
#&gt; SRR1274558     3  0.0592      0.933 0.000 0.012 0.988
#&gt; SRR1274559     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274560     3  0.4796      0.692 0.220 0.000 0.780
#&gt; SRR1274561     1  0.0424      0.926 0.992 0.000 0.008
#&gt; SRR1274562     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274563     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274564     3  0.3619      0.804 0.000 0.136 0.864
#&gt; SRR1274565     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274566     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274567     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274568     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274569     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274575     2  0.0000      0.999 0.000 1.000 0.000
#&gt; SRR1274576     2  0.0237      0.996 0.000 0.996 0.004
#&gt; SRR1274577     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR1274578     1  0.0747      0.922 0.984 0.000 0.016
#&gt; SRR1274579     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.931 1.000 0.000 0.000
#&gt; SRR1274581     1  0.4504      0.743 0.804 0.000 0.196
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274529     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274530     2  0.2081      0.905 0.000 0.916 0.000 0.084
#&gt; SRR1274531     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274532     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274533     4  0.0188      0.974 0.000 0.004 0.000 0.996
#&gt; SRR1274534     4  0.0188      0.974 0.000 0.004 0.000 0.996
#&gt; SRR1274535     4  0.2081      0.898 0.000 0.000 0.084 0.916
#&gt; SRR1274536     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274537     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274539     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274540     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274548     2  0.0336      0.982 0.000 0.992 0.000 0.008
#&gt; SRR1274549     1  0.2412      0.839 0.908 0.000 0.008 0.084
#&gt; SRR1274550     3  0.0000      0.911 0.000 0.000 1.000 0.000
#&gt; SRR1274551     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274552     1  0.6538      0.500 0.600 0.000 0.108 0.292
#&gt; SRR1274553     3  0.4955      0.142 0.444 0.000 0.556 0.000
#&gt; SRR1274554     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274555     3  0.0000      0.911 0.000 0.000 1.000 0.000
#&gt; SRR1274556     3  0.0000      0.911 0.000 0.000 1.000 0.000
#&gt; SRR1274557     3  0.0592      0.903 0.016 0.000 0.984 0.000
#&gt; SRR1274558     4  0.2281      0.877 0.000 0.096 0.000 0.904
#&gt; SRR1274559     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274560     1  0.0000      0.912 1.000 0.000 0.000 0.000
#&gt; SRR1274561     1  0.0000      0.912 1.000 0.000 0.000 0.000
#&gt; SRR1274562     3  0.2469      0.825 0.108 0.000 0.892 0.000
#&gt; SRR1274563     3  0.0000      0.911 0.000 0.000 1.000 0.000
#&gt; SRR1274564     4  0.2081      0.885 0.000 0.084 0.000 0.916
#&gt; SRR1274565     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274566     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274567     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274568     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274569     1  0.0000      0.912 1.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.912 1.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.912 1.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.912 1.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.2081      0.905 0.000 0.916 0.000 0.084
#&gt; SRR1274576     2  0.0000      0.989 0.000 1.000 0.000 0.000
#&gt; SRR1274577     4  0.0000      0.976 0.000 0.000 0.000 1.000
#&gt; SRR1274578     1  0.3873      0.693 0.772 0.000 0.000 0.228
#&gt; SRR1274579     1  0.0000      0.912 1.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.912 1.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.0000      0.911 0.000 0.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274529     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274530     4   0.429     0.2276 0.000 0.468 0.000 0.532 0.000
#&gt; SRR1274531     4   0.273     0.6744 0.000 0.000 0.000 0.840 0.160
#&gt; SRR1274532     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274533     5   0.000     0.7818 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274534     5   0.000     0.7818 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274535     5   0.000     0.7818 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274536     4   0.000     0.8239 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274537     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274538     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274539     5   0.000     0.7818 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274540     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274541     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274542     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274543     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274544     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274545     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274546     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274547     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274548     2   0.348     0.6416 0.000 0.752 0.000 0.248 0.000
#&gt; SRR1274549     1   0.632     0.1413 0.444 0.000 0.000 0.400 0.156
#&gt; SRR1274550     3   0.000     0.9134 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274551     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274552     5   0.590    -0.1993 0.444 0.000 0.100 0.000 0.456
#&gt; SRR1274553     3   0.427     0.2024 0.444 0.000 0.556 0.000 0.000
#&gt; SRR1274554     5   0.269     0.6620 0.000 0.000 0.000 0.156 0.844
#&gt; SRR1274555     3   0.000     0.9134 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274556     3   0.000     0.9134 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274557     3   0.000     0.9134 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274558     5   0.637     0.1859 0.000 0.400 0.000 0.164 0.436
#&gt; SRR1274559     5   0.000     0.7818 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274560     1   0.269     0.7805 0.844 0.000 0.000 0.000 0.156
#&gt; SRR1274561     1   0.269     0.7805 0.844 0.000 0.000 0.000 0.156
#&gt; SRR1274562     3   0.202     0.8323 0.100 0.000 0.900 0.000 0.000
#&gt; SRR1274563     3   0.000     0.9134 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274564     4   0.000     0.8239 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274565     4   0.000     0.8239 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274566     4   0.000     0.8239 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274567     4   0.000     0.8239 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274568     5   0.430     0.0695 0.000 0.000 0.000 0.484 0.516
#&gt; SRR1274569     1   0.000     0.8833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1   0.000     0.8833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1   0.000     0.8833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1   0.000     0.8833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274574     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274575     4   0.337     0.6434 0.000 0.232 0.000 0.768 0.000
#&gt; SRR1274576     2   0.000     0.9836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274577     5   0.000     0.7818 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1274578     1   0.191     0.8188 0.908 0.000 0.000 0.000 0.092
#&gt; SRR1274579     1   0.000     0.8833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1   0.000     0.8833 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     3   0.000     0.9134 0.000 0.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274529     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274530     4  0.3857      0.202 0.000 0.468 0.000 0.532 0.000 0.000
#&gt; SRR1274531     4  0.0458      0.788 0.000 0.000 0.000 0.984 0.016 0.000
#&gt; SRR1274532     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274533     5  0.0000      0.888 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274534     5  0.0000      0.888 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274535     5  0.0000      0.888 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274536     4  0.0000      0.797 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274537     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274538     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274539     5  0.0000      0.888 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274540     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274541     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274542     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274543     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274544     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274545     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274546     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274547     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274548     2  0.3126      0.638 0.000 0.752 0.000 0.248 0.000 0.000
#&gt; SRR1274549     1  0.3993      0.333 0.592 0.000 0.000 0.400 0.008 0.000
#&gt; SRR1274550     3  0.0000      0.900 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274551     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274552     1  0.5042      0.473 0.592 0.000 0.100 0.000 0.308 0.000
#&gt; SRR1274553     3  0.3833      0.143 0.444 0.000 0.556 0.000 0.000 0.000
#&gt; SRR1274554     5  0.0260      0.881 0.000 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1274555     3  0.0000      0.900 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274556     3  0.0000      0.900 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274557     3  0.0547      0.890 0.020 0.000 0.980 0.000 0.000 0.000
#&gt; SRR1274558     5  0.5659      0.103 0.000 0.424 0.000 0.152 0.424 0.000
#&gt; SRR1274559     5  0.0000      0.888 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274560     1  0.0260      0.860 0.992 0.000 0.000 0.000 0.008 0.000
#&gt; SRR1274561     1  0.0260      0.860 0.992 0.000 0.000 0.000 0.008 0.000
#&gt; SRR1274562     3  0.1814      0.817 0.100 0.000 0.900 0.000 0.000 0.000
#&gt; SRR1274563     3  0.0000      0.900 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274564     4  0.0000      0.797 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274565     4  0.0000      0.797 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274566     4  0.0000      0.797 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274567     4  0.0000      0.797 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1274568     4  0.3804      0.189 0.000 0.000 0.000 0.576 0.424 0.000
#&gt; SRR1274569     1  0.0000      0.862 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274570     1  0.0000      0.862 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274571     1  0.0000      0.862 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274572     1  0.0000      0.862 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274573     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274574     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274575     4  0.3023      0.584 0.000 0.232 0.000 0.768 0.000 0.000
#&gt; SRR1274576     2  0.0000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274577     5  0.0000      0.888 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1274578     6  0.0146      1.000 0.004 0.000 0.000 0.000 0.000 0.996
#&gt; SRR1274579     6  0.0146      1.000 0.004 0.000 0.000 0.000 0.000 0.996
#&gt; SRR1274580     6  0.0146      1.000 0.004 0.000 0.000 0.000 0.000 0.996
#&gt; SRR1274581     3  0.0146      0.899 0.000 0.000 0.996 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.752           0.916       0.962         0.4702 0.535   0.535
#> 3 3 0.517           0.712       0.858         0.2427 0.755   0.603
#> 4 4 0.533           0.492       0.739         0.1802 0.813   0.597
#> 5 5 0.539           0.474       0.702         0.0914 0.742   0.380
#> 6 6 0.778           0.806       0.837         0.0753 0.840   0.475
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274529     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274530     2  0.7056      0.765 0.192 0.808
#&gt; SRR1274531     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274532     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274533     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274534     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274535     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274536     1  0.8016      0.687 0.756 0.244
#&gt; SRR1274537     2  0.0672      0.957 0.008 0.992
#&gt; SRR1274538     2  0.0672      0.957 0.008 0.992
#&gt; SRR1274539     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274540     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274541     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274542     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274543     2  0.0672      0.957 0.008 0.992
#&gt; SRR1274544     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274545     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274546     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274547     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274548     1  0.0672      0.950 0.992 0.008
#&gt; SRR1274549     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274550     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274551     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274552     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274553     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274554     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274555     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274556     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274557     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274558     1  0.6247      0.802 0.844 0.156
#&gt; SRR1274559     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274560     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274561     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274562     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274563     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274564     1  0.8016      0.687 0.756 0.244
#&gt; SRR1274565     2  0.8016      0.669 0.244 0.756
#&gt; SRR1274566     1  0.8016      0.687 0.756 0.244
#&gt; SRR1274567     1  0.8016      0.687 0.756 0.244
#&gt; SRR1274568     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274569     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274570     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274571     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274572     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274573     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274574     2  0.0000      0.961 0.000 1.000
#&gt; SRR1274575     2  0.7056      0.765 0.192 0.808
#&gt; SRR1274576     1  0.8081      0.671 0.752 0.248
#&gt; SRR1274577     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274578     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274579     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274580     1  0.0000      0.955 1.000 0.000
#&gt; SRR1274581     1  0.0000      0.955 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.2625     0.8869 0.000 0.916 0.084
#&gt; SRR1274529     2  0.2625     0.8868 0.000 0.916 0.084
#&gt; SRR1274530     2  0.5580     0.7220 0.008 0.736 0.256
#&gt; SRR1274531     3  0.3769     0.7594 0.104 0.016 0.880
#&gt; SRR1274532     2  0.0000     0.9132 0.000 1.000 0.000
#&gt; SRR1274533     3  0.1015     0.7756 0.008 0.012 0.980
#&gt; SRR1274534     3  0.1015     0.7756 0.008 0.012 0.980
#&gt; SRR1274535     3  0.2939     0.7613 0.072 0.012 0.916
#&gt; SRR1274536     3  0.4662     0.7424 0.124 0.032 0.844
#&gt; SRR1274537     3  0.6295     0.0783 0.000 0.472 0.528
#&gt; SRR1274538     3  0.5254     0.5620 0.000 0.264 0.736
#&gt; SRR1274539     3  0.1751     0.7741 0.028 0.012 0.960
#&gt; SRR1274540     2  0.0000     0.9132 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000     0.9132 0.000 1.000 0.000
#&gt; SRR1274542     2  0.0000     0.9132 0.000 1.000 0.000
#&gt; SRR1274543     3  0.6225     0.1534 0.000 0.432 0.568
#&gt; SRR1274544     2  0.0000     0.9132 0.000 1.000 0.000
#&gt; SRR1274545     2  0.2625     0.8868 0.000 0.916 0.084
#&gt; SRR1274546     2  0.0424     0.9116 0.000 0.992 0.008
#&gt; SRR1274547     2  0.4887     0.7564 0.000 0.772 0.228
#&gt; SRR1274548     3  0.1765     0.7694 0.004 0.040 0.956
#&gt; SRR1274549     3  0.5070     0.7064 0.224 0.004 0.772
#&gt; SRR1274550     3  0.5926     0.4042 0.356 0.000 0.644
#&gt; SRR1274551     2  0.0000     0.9132 0.000 1.000 0.000
#&gt; SRR1274552     3  0.3618     0.7477 0.104 0.012 0.884
#&gt; SRR1274553     3  0.5493     0.6246 0.232 0.012 0.756
#&gt; SRR1274554     3  0.0592     0.7750 0.000 0.012 0.988
#&gt; SRR1274555     3  0.5926     0.4042 0.356 0.000 0.644
#&gt; SRR1274556     3  0.5926     0.4042 0.356 0.000 0.644
#&gt; SRR1274557     3  0.3918     0.7389 0.120 0.012 0.868
#&gt; SRR1274558     3  0.1031     0.7731 0.000 0.024 0.976
#&gt; SRR1274559     3  0.0592     0.7750 0.000 0.012 0.988
#&gt; SRR1274560     3  0.3879     0.7365 0.152 0.000 0.848
#&gt; SRR1274561     3  0.4555     0.7075 0.200 0.000 0.800
#&gt; SRR1274562     3  0.6168     0.3216 0.412 0.000 0.588
#&gt; SRR1274563     3  0.5926     0.4042 0.356 0.000 0.644
#&gt; SRR1274564     3  0.4121     0.7357 0.040 0.084 0.876
#&gt; SRR1274565     3  0.3412     0.7225 0.000 0.124 0.876
#&gt; SRR1274566     3  0.4092     0.7353 0.036 0.088 0.876
#&gt; SRR1274567     3  0.4519     0.7424 0.116 0.032 0.852
#&gt; SRR1274568     3  0.0592     0.7750 0.000 0.012 0.988
#&gt; SRR1274569     3  0.5201     0.6759 0.236 0.004 0.760
#&gt; SRR1274570     1  0.5621     0.5256 0.692 0.000 0.308
#&gt; SRR1274571     1  0.5785     0.4830 0.668 0.000 0.332
#&gt; SRR1274572     1  0.1163     0.8375 0.972 0.000 0.028
#&gt; SRR1274573     2  0.0000     0.9132 0.000 1.000 0.000
#&gt; SRR1274574     2  0.0000     0.9132 0.000 1.000 0.000
#&gt; SRR1274575     2  0.5580     0.7220 0.008 0.736 0.256
#&gt; SRR1274576     3  0.1964     0.7607 0.000 0.056 0.944
#&gt; SRR1274577     3  0.0829     0.7754 0.004 0.012 0.984
#&gt; SRR1274578     1  0.1163     0.8375 0.972 0.000 0.028
#&gt; SRR1274579     1  0.1163     0.8375 0.972 0.000 0.028
#&gt; SRR1274580     1  0.1163     0.8375 0.972 0.000 0.028
#&gt; SRR1274581     3  0.5926     0.4042 0.356 0.000 0.644
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.4039     0.7621 0.080 0.836 0.000 0.084
#&gt; SRR1274529     2  0.5077     0.7380 0.080 0.760 0.000 0.160
#&gt; SRR1274530     2  0.6546     0.4389 0.080 0.524 0.000 0.396
#&gt; SRR1274531     4  0.5898    -0.3590 0.012 0.016 0.448 0.524
#&gt; SRR1274532     2  0.0000     0.8128 0.000 1.000 0.000 0.000
#&gt; SRR1274533     3  0.5506     0.4901 0.000 0.016 0.512 0.472
#&gt; SRR1274534     3  0.5500     0.4902 0.000 0.016 0.520 0.464
#&gt; SRR1274535     3  0.5427     0.4640 0.000 0.016 0.568 0.416
#&gt; SRR1274536     4  0.2408     0.5100 0.000 0.000 0.104 0.896
#&gt; SRR1274537     2  0.8169    -0.2118 0.080 0.432 0.408 0.080
#&gt; SRR1274538     3  0.9136     0.3071 0.080 0.244 0.404 0.272
#&gt; SRR1274539     3  0.5427     0.4640 0.000 0.016 0.568 0.416
#&gt; SRR1274540     2  0.0000     0.8128 0.000 1.000 0.000 0.000
#&gt; SRR1274541     2  0.0000     0.8128 0.000 1.000 0.000 0.000
#&gt; SRR1274542     2  0.0000     0.8128 0.000 1.000 0.000 0.000
#&gt; SRR1274543     3  0.8795     0.2197 0.080 0.372 0.400 0.148
#&gt; SRR1274544     2  0.0000     0.8128 0.000 1.000 0.000 0.000
#&gt; SRR1274545     2  0.5032     0.7400 0.080 0.764 0.000 0.156
#&gt; SRR1274546     2  0.0336     0.8112 0.000 0.992 0.000 0.008
#&gt; SRR1274547     2  0.6201     0.5998 0.080 0.620 0.000 0.300
#&gt; SRR1274548     3  0.8301     0.4069 0.076 0.096 0.424 0.404
#&gt; SRR1274549     4  0.4212     0.5195 0.012 0.000 0.216 0.772
#&gt; SRR1274550     3  0.0804     0.3658 0.012 0.000 0.980 0.008
#&gt; SRR1274551     2  0.0000     0.8128 0.000 1.000 0.000 0.000
#&gt; SRR1274552     3  0.3893     0.3843 0.008 0.000 0.796 0.196
#&gt; SRR1274553     3  0.3790     0.3767 0.016 0.000 0.820 0.164
#&gt; SRR1274554     3  0.5506     0.4901 0.000 0.016 0.512 0.472
#&gt; SRR1274555     3  0.0937     0.3651 0.012 0.000 0.976 0.012
#&gt; SRR1274556     3  0.0469     0.3595 0.012 0.000 0.988 0.000
#&gt; SRR1274557     3  0.2542     0.3800 0.012 0.000 0.904 0.084
#&gt; SRR1274558     3  0.7118     0.4749 0.052 0.036 0.492 0.420
#&gt; SRR1274559     3  0.5444     0.4955 0.000 0.016 0.560 0.424
#&gt; SRR1274560     4  0.3852     0.4814 0.008 0.000 0.192 0.800
#&gt; SRR1274561     4  0.5268     0.4128 0.012 0.000 0.396 0.592
#&gt; SRR1274562     4  0.6705     0.1206 0.088 0.000 0.440 0.472
#&gt; SRR1274563     3  0.0937     0.3651 0.012 0.000 0.976 0.012
#&gt; SRR1274564     4  0.6703    -0.0480 0.036 0.052 0.292 0.620
#&gt; SRR1274565     3  0.8944     0.3421 0.076 0.184 0.404 0.336
#&gt; SRR1274566     4  0.4456     0.0304 0.000 0.004 0.280 0.716
#&gt; SRR1274567     4  0.2408     0.5100 0.000 0.000 0.104 0.896
#&gt; SRR1274568     3  0.5503     0.4866 0.000 0.016 0.516 0.468
#&gt; SRR1274569     4  0.6552     0.2963 0.096 0.000 0.328 0.576
#&gt; SRR1274570     1  0.7557     0.5008 0.484 0.000 0.284 0.232
#&gt; SRR1274571     1  0.7593     0.4874 0.476 0.000 0.288 0.236
#&gt; SRR1274572     1  0.2011     0.8163 0.920 0.000 0.080 0.000
#&gt; SRR1274573     2  0.0000     0.8128 0.000 1.000 0.000 0.000
#&gt; SRR1274574     2  0.0000     0.8128 0.000 1.000 0.000 0.000
#&gt; SRR1274575     2  0.6546     0.4389 0.080 0.524 0.000 0.396
#&gt; SRR1274576     3  0.7374     0.4677 0.076 0.032 0.488 0.404
#&gt; SRR1274577     3  0.5503     0.4906 0.000 0.016 0.516 0.468
#&gt; SRR1274578     1  0.2011     0.8163 0.920 0.000 0.080 0.000
#&gt; SRR1274579     1  0.2011     0.8163 0.920 0.000 0.080 0.000
#&gt; SRR1274580     1  0.2011     0.8163 0.920 0.000 0.080 0.000
#&gt; SRR1274581     3  0.0592     0.3571 0.016 0.000 0.984 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.2446     0.6066 0.000 0.900 0.000 0.044 0.056
#&gt; SRR1274529     2  0.1043     0.6096 0.000 0.960 0.000 0.040 0.000
#&gt; SRR1274530     2  0.2139     0.5809 0.000 0.916 0.000 0.032 0.052
#&gt; SRR1274531     5  0.4536     0.1791 0.012 0.024 0.008 0.212 0.744
#&gt; SRR1274532     2  0.4305     0.5713 0.000 0.512 0.000 0.488 0.000
#&gt; SRR1274533     5  0.2248     0.5821 0.000 0.088 0.000 0.012 0.900
#&gt; SRR1274534     5  0.2331     0.5792 0.000 0.080 0.000 0.020 0.900
#&gt; SRR1274535     5  0.1788     0.5724 0.000 0.056 0.004 0.008 0.932
#&gt; SRR1274536     5  0.6691     0.1341 0.004 0.180 0.016 0.256 0.544
#&gt; SRR1274537     2  0.3988     0.5230 0.000 0.768 0.000 0.036 0.196
#&gt; SRR1274538     2  0.3954     0.5153 0.000 0.772 0.000 0.036 0.192
#&gt; SRR1274539     5  0.2074     0.5750 0.000 0.060 0.004 0.016 0.920
#&gt; SRR1274540     2  0.4305     0.5713 0.000 0.512 0.000 0.488 0.000
#&gt; SRR1274541     2  0.4450     0.5702 0.000 0.508 0.000 0.488 0.004
#&gt; SRR1274542     2  0.4305     0.5713 0.000 0.512 0.000 0.488 0.000
#&gt; SRR1274543     2  0.3919     0.5212 0.000 0.776 0.000 0.036 0.188
#&gt; SRR1274544     2  0.4305     0.5713 0.000 0.512 0.000 0.488 0.000
#&gt; SRR1274545     2  0.0510     0.6140 0.000 0.984 0.000 0.016 0.000
#&gt; SRR1274546     2  0.4084     0.5997 0.000 0.668 0.000 0.328 0.004
#&gt; SRR1274547     2  0.1117     0.6055 0.000 0.964 0.000 0.020 0.016
#&gt; SRR1274548     2  0.4744     0.1991 0.000 0.572 0.000 0.020 0.408
#&gt; SRR1274549     5  0.7694    -0.3609 0.120 0.044 0.076 0.204 0.556
#&gt; SRR1274550     3  0.1704     0.7795 0.000 0.000 0.928 0.004 0.068
#&gt; SRR1274551     2  0.4302     0.5735 0.000 0.520 0.000 0.480 0.000
#&gt; SRR1274552     5  0.5909     0.0146 0.112 0.000 0.156 0.052 0.680
#&gt; SRR1274553     5  0.6667    -0.1252 0.120 0.000 0.264 0.048 0.568
#&gt; SRR1274554     5  0.2358     0.5828 0.000 0.104 0.000 0.008 0.888
#&gt; SRR1274555     3  0.1197     0.7880 0.000 0.000 0.952 0.000 0.048
#&gt; SRR1274556     3  0.0579     0.7747 0.000 0.000 0.984 0.008 0.008
#&gt; SRR1274557     3  0.5877     0.3583 0.108 0.000 0.596 0.008 0.288
#&gt; SRR1274558     2  0.4744     0.1676 0.000 0.572 0.000 0.020 0.408
#&gt; SRR1274559     5  0.3375     0.5729 0.000 0.104 0.000 0.056 0.840
#&gt; SRR1274560     5  0.5237    -0.1542 0.012 0.004 0.024 0.368 0.592
#&gt; SRR1274561     4  0.7607     0.6399 0.120 0.000 0.104 0.396 0.380
#&gt; SRR1274562     3  0.7221    -0.1007 0.080 0.000 0.504 0.296 0.120
#&gt; SRR1274563     3  0.1357     0.7877 0.000 0.000 0.948 0.004 0.048
#&gt; SRR1274564     2  0.6796    -0.1217 0.000 0.456 0.008 0.220 0.316
#&gt; SRR1274565     2  0.4425     0.4612 0.000 0.716 0.000 0.040 0.244
#&gt; SRR1274566     5  0.6865     0.1435 0.000 0.360 0.008 0.220 0.412
#&gt; SRR1274567     5  0.6691     0.1341 0.004 0.180 0.016 0.256 0.544
#&gt; SRR1274568     5  0.3934     0.4781 0.000 0.244 0.000 0.016 0.740
#&gt; SRR1274569     4  0.8234     0.6741 0.232 0.000 0.152 0.396 0.220
#&gt; SRR1274570     1  0.5097     0.5853 0.708 0.000 0.060 0.212 0.020
#&gt; SRR1274571     1  0.5893     0.4838 0.660 0.000 0.072 0.216 0.052
#&gt; SRR1274572     1  0.1197     0.8058 0.952 0.000 0.048 0.000 0.000
#&gt; SRR1274573     2  0.4305     0.5713 0.000 0.512 0.000 0.488 0.000
#&gt; SRR1274574     2  0.4410     0.5818 0.000 0.556 0.000 0.440 0.004
#&gt; SRR1274575     2  0.2221     0.5782 0.000 0.912 0.000 0.036 0.052
#&gt; SRR1274576     2  0.4238     0.2812 0.000 0.628 0.000 0.004 0.368
#&gt; SRR1274577     5  0.2463     0.5841 0.000 0.100 0.008 0.004 0.888
#&gt; SRR1274578     1  0.0000     0.8243 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000     0.8243 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000     0.8243 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.1924     0.7541 0.004 0.000 0.924 0.064 0.008
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.0260      0.912 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1274529     2  0.0458      0.907 0.000 0.984 0.000 0.000 0.000 0.016
#&gt; SRR1274530     2  0.0405      0.915 0.000 0.988 0.000 0.000 0.008 0.004
#&gt; SRR1274531     4  0.3816      0.671 0.000 0.016 0.000 0.688 0.296 0.000
#&gt; SRR1274532     6  0.3023      0.949 0.000 0.232 0.000 0.000 0.000 0.768
#&gt; SRR1274533     5  0.1967      0.903 0.000 0.012 0.000 0.084 0.904 0.000
#&gt; SRR1274534     5  0.0458      0.869 0.000 0.016 0.000 0.000 0.984 0.000
#&gt; SRR1274535     5  0.0984      0.875 0.000 0.012 0.008 0.012 0.968 0.000
#&gt; SRR1274536     4  0.3259      0.723 0.000 0.012 0.000 0.772 0.216 0.000
#&gt; SRR1274537     2  0.0508      0.910 0.000 0.984 0.000 0.000 0.004 0.012
#&gt; SRR1274538     2  0.0291      0.914 0.000 0.992 0.000 0.004 0.004 0.000
#&gt; SRR1274539     5  0.0976      0.870 0.000 0.016 0.008 0.008 0.968 0.000
#&gt; SRR1274540     6  0.3023      0.949 0.000 0.232 0.000 0.000 0.000 0.768
#&gt; SRR1274541     6  0.3076      0.946 0.000 0.240 0.000 0.000 0.000 0.760
#&gt; SRR1274542     6  0.3023      0.949 0.000 0.232 0.000 0.000 0.000 0.768
#&gt; SRR1274543     2  0.0146      0.915 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1274544     6  0.3023      0.949 0.000 0.232 0.000 0.000 0.000 0.768
#&gt; SRR1274545     2  0.0458      0.907 0.000 0.984 0.000 0.000 0.000 0.016
#&gt; SRR1274546     6  0.3717      0.770 0.000 0.384 0.000 0.000 0.000 0.616
#&gt; SRR1274547     2  0.0405      0.915 0.000 0.988 0.000 0.000 0.008 0.004
#&gt; SRR1274548     2  0.1867      0.864 0.000 0.916 0.000 0.020 0.064 0.000
#&gt; SRR1274549     4  0.1802      0.661 0.000 0.012 0.000 0.916 0.072 0.000
#&gt; SRR1274550     3  0.0508      0.821 0.000 0.000 0.984 0.004 0.000 0.012
#&gt; SRR1274551     6  0.3151      0.940 0.000 0.252 0.000 0.000 0.000 0.748
#&gt; SRR1274552     3  0.5272      0.405 0.004 0.000 0.500 0.420 0.072 0.004
#&gt; SRR1274553     3  0.5423      0.604 0.036 0.000 0.600 0.304 0.056 0.004
#&gt; SRR1274554     5  0.1967      0.903 0.000 0.012 0.000 0.084 0.904 0.000
#&gt; SRR1274555     3  0.0000      0.821 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274556     3  0.1218      0.814 0.000 0.000 0.956 0.004 0.012 0.028
#&gt; SRR1274557     3  0.2595      0.776 0.000 0.000 0.836 0.160 0.000 0.004
#&gt; SRR1274558     2  0.2948      0.724 0.000 0.804 0.000 0.008 0.188 0.000
#&gt; SRR1274559     5  0.1967      0.903 0.000 0.012 0.000 0.084 0.904 0.000
#&gt; SRR1274560     4  0.3521      0.704 0.000 0.000 0.004 0.724 0.268 0.004
#&gt; SRR1274561     4  0.2089      0.644 0.004 0.000 0.012 0.908 0.072 0.004
#&gt; SRR1274562     3  0.3017      0.769 0.052 0.000 0.840 0.108 0.000 0.000
#&gt; SRR1274563     3  0.0000      0.821 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1274564     2  0.4942      0.404 0.000 0.652 0.000 0.192 0.156 0.000
#&gt; SRR1274565     2  0.0777      0.908 0.000 0.972 0.000 0.004 0.024 0.000
#&gt; SRR1274566     4  0.5898      0.312 0.000 0.380 0.000 0.416 0.204 0.000
#&gt; SRR1274567     4  0.3348      0.723 0.000 0.016 0.000 0.768 0.216 0.000
#&gt; SRR1274568     5  0.3780      0.642 0.000 0.020 0.004 0.248 0.728 0.000
#&gt; SRR1274569     1  0.5105      0.362 0.496 0.000 0.048 0.444 0.008 0.004
#&gt; SRR1274570     1  0.1124      0.862 0.956 0.000 0.008 0.036 0.000 0.000
#&gt; SRR1274571     1  0.3507      0.732 0.752 0.000 0.012 0.232 0.000 0.004
#&gt; SRR1274572     1  0.0146      0.873 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR1274573     6  0.3023      0.949 0.000 0.232 0.000 0.000 0.000 0.768
#&gt; SRR1274574     6  0.3659      0.809 0.000 0.364 0.000 0.000 0.000 0.636
#&gt; SRR1274575     2  0.0405      0.915 0.000 0.988 0.000 0.000 0.008 0.004
#&gt; SRR1274576     2  0.1082      0.896 0.000 0.956 0.000 0.004 0.040 0.000
#&gt; SRR1274577     5  0.1967      0.903 0.000 0.012 0.000 0.084 0.904 0.000
#&gt; SRR1274578     1  0.0000      0.873 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274579     1  0.0000      0.873 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0000      0.873 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR1274581     3  0.3342      0.734 0.000 0.000 0.760 0.000 0.012 0.228
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16571 rows and 54 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.982       0.992         0.4626 0.535   0.535
#> 3 3 0.638           0.702       0.849         0.1773 0.913   0.844
#> 4 4 0.599           0.790       0.837         0.2642 0.732   0.493
#> 5 5 0.653           0.700       0.841         0.0641 0.993   0.976
#> 6 6 0.647           0.626       0.815         0.0411 0.844   0.549
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1274528     2   0.000      0.997 0.000 1.000
#&gt; SRR1274529     2   0.000      0.997 0.000 1.000
#&gt; SRR1274530     2   0.000      0.997 0.000 1.000
#&gt; SRR1274531     2   0.295      0.946 0.052 0.948
#&gt; SRR1274532     2   0.000      0.997 0.000 1.000
#&gt; SRR1274533     2   0.000      0.997 0.000 1.000
#&gt; SRR1274534     2   0.000      0.997 0.000 1.000
#&gt; SRR1274535     2   0.278      0.950 0.048 0.952
#&gt; SRR1274536     2   0.000      0.997 0.000 1.000
#&gt; SRR1274537     2   0.000      0.997 0.000 1.000
#&gt; SRR1274538     2   0.000      0.997 0.000 1.000
#&gt; SRR1274539     2   0.000      0.997 0.000 1.000
#&gt; SRR1274540     2   0.000      0.997 0.000 1.000
#&gt; SRR1274541     2   0.000      0.997 0.000 1.000
#&gt; SRR1274542     2   0.000      0.997 0.000 1.000
#&gt; SRR1274543     2   0.000      0.997 0.000 1.000
#&gt; SRR1274544     2   0.000      0.997 0.000 1.000
#&gt; SRR1274545     2   0.000      0.997 0.000 1.000
#&gt; SRR1274546     2   0.000      0.997 0.000 1.000
#&gt; SRR1274547     2   0.000      0.997 0.000 1.000
#&gt; SRR1274548     2   0.000      0.997 0.000 1.000
#&gt; SRR1274549     1   0.000      0.983 1.000 0.000
#&gt; SRR1274550     1   0.000      0.983 1.000 0.000
#&gt; SRR1274551     2   0.000      0.997 0.000 1.000
#&gt; SRR1274552     1   0.000      0.983 1.000 0.000
#&gt; SRR1274553     1   0.000      0.983 1.000 0.000
#&gt; SRR1274554     2   0.000      0.997 0.000 1.000
#&gt; SRR1274555     1   0.000      0.983 1.000 0.000
#&gt; SRR1274556     1   0.000      0.983 1.000 0.000
#&gt; SRR1274557     1   0.000      0.983 1.000 0.000
#&gt; SRR1274558     2   0.000      0.997 0.000 1.000
#&gt; SRR1274559     2   0.000      0.997 0.000 1.000
#&gt; SRR1274560     1   0.891      0.551 0.692 0.308
#&gt; SRR1274561     1   0.000      0.983 1.000 0.000
#&gt; SRR1274562     1   0.000      0.983 1.000 0.000
#&gt; SRR1274563     1   0.000      0.983 1.000 0.000
#&gt; SRR1274564     2   0.000      0.997 0.000 1.000
#&gt; SRR1274565     2   0.000      0.997 0.000 1.000
#&gt; SRR1274566     2   0.000      0.997 0.000 1.000
#&gt; SRR1274567     2   0.000      0.997 0.000 1.000
#&gt; SRR1274568     2   0.000      0.997 0.000 1.000
#&gt; SRR1274569     1   0.000      0.983 1.000 0.000
#&gt; SRR1274570     1   0.000      0.983 1.000 0.000
#&gt; SRR1274571     1   0.000      0.983 1.000 0.000
#&gt; SRR1274572     1   0.000      0.983 1.000 0.000
#&gt; SRR1274573     2   0.000      0.997 0.000 1.000
#&gt; SRR1274574     2   0.000      0.997 0.000 1.000
#&gt; SRR1274575     2   0.000      0.997 0.000 1.000
#&gt; SRR1274576     2   0.000      0.997 0.000 1.000
#&gt; SRR1274577     2   0.000      0.997 0.000 1.000
#&gt; SRR1274578     1   0.000      0.983 1.000 0.000
#&gt; SRR1274579     1   0.000      0.983 1.000 0.000
#&gt; SRR1274580     1   0.000      0.983 1.000 0.000
#&gt; SRR1274581     1   0.000      0.983 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1274528     2  0.0000      0.917 0.000 1.000 0.000
#&gt; SRR1274529     2  0.3551      0.877 0.132 0.868 0.000
#&gt; SRR1274530     2  0.3412      0.878 0.124 0.876 0.000
#&gt; SRR1274531     2  0.8573      0.457 0.116 0.556 0.328
#&gt; SRR1274532     2  0.0237      0.917 0.004 0.996 0.000
#&gt; SRR1274533     2  0.0424      0.916 0.008 0.992 0.000
#&gt; SRR1274534     2  0.0475      0.916 0.004 0.992 0.004
#&gt; SRR1274535     2  0.5882      0.509 0.000 0.652 0.348
#&gt; SRR1274536     2  0.3826      0.875 0.124 0.868 0.008
#&gt; SRR1274537     2  0.0000      0.917 0.000 1.000 0.000
#&gt; SRR1274538     2  0.0424      0.917 0.008 0.992 0.000
#&gt; SRR1274539     2  0.0747      0.913 0.000 0.984 0.016
#&gt; SRR1274540     2  0.0000      0.917 0.000 1.000 0.000
#&gt; SRR1274541     2  0.0000      0.917 0.000 1.000 0.000
#&gt; SRR1274542     2  0.1289      0.908 0.032 0.968 0.000
#&gt; SRR1274543     2  0.0237      0.917 0.004 0.996 0.000
#&gt; SRR1274544     2  0.0592      0.915 0.012 0.988 0.000
#&gt; SRR1274545     2  0.3038      0.889 0.104 0.896 0.000
#&gt; SRR1274546     2  0.0000      0.917 0.000 1.000 0.000
#&gt; SRR1274547     2  0.2796      0.892 0.092 0.908 0.000
#&gt; SRR1274548     2  0.0424      0.917 0.008 0.992 0.000
#&gt; SRR1274549     3  0.3267      0.545 0.116 0.000 0.884
#&gt; SRR1274550     3  0.0000      0.692 0.000 0.000 1.000
#&gt; SRR1274551     2  0.0237      0.917 0.004 0.996 0.000
#&gt; SRR1274552     3  0.0000      0.692 0.000 0.000 1.000
#&gt; SRR1274553     3  0.0892      0.677 0.020 0.000 0.980
#&gt; SRR1274554     2  0.4235      0.802 0.176 0.824 0.000
#&gt; SRR1274555     3  0.0000      0.692 0.000 0.000 1.000
#&gt; SRR1274556     3  0.0000      0.692 0.000 0.000 1.000
#&gt; SRR1274557     3  0.0000      0.692 0.000 0.000 1.000
#&gt; SRR1274558     2  0.0000      0.917 0.000 1.000 0.000
#&gt; SRR1274559     2  0.5012      0.770 0.204 0.788 0.008
#&gt; SRR1274560     2  0.9953     -0.370 0.344 0.368 0.288
#&gt; SRR1274561     3  0.6500     -0.589 0.464 0.004 0.532
#&gt; SRR1274562     3  0.5810     -0.137 0.336 0.000 0.664
#&gt; SRR1274563     3  0.0000      0.692 0.000 0.000 1.000
#&gt; SRR1274564     2  0.3619      0.874 0.136 0.864 0.000
#&gt; SRR1274565     2  0.2711      0.899 0.088 0.912 0.000
#&gt; SRR1274566     2  0.3482      0.877 0.128 0.872 0.000
#&gt; SRR1274567     2  0.3482      0.877 0.128 0.872 0.000
#&gt; SRR1274568     2  0.0000      0.917 0.000 1.000 0.000
#&gt; SRR1274569     3  0.6305     -0.639 0.484 0.000 0.516
#&gt; SRR1274570     1  0.6244      0.761 0.560 0.000 0.440
#&gt; SRR1274571     1  0.6274      0.730 0.544 0.000 0.456
#&gt; SRR1274572     1  0.6244      0.761 0.560 0.000 0.440
#&gt; SRR1274573     2  0.0592      0.915 0.012 0.988 0.000
#&gt; SRR1274574     2  0.0592      0.916 0.012 0.988 0.000
#&gt; SRR1274575     2  0.3412      0.878 0.124 0.876 0.000
#&gt; SRR1274576     2  0.0237      0.916 0.004 0.996 0.000
#&gt; SRR1274577     2  0.0424      0.916 0.008 0.992 0.000
#&gt; SRR1274578     1  0.3619      0.506 0.864 0.000 0.136
#&gt; SRR1274579     1  0.5706      0.717 0.680 0.000 0.320
#&gt; SRR1274580     1  0.6126      0.769 0.600 0.000 0.400
#&gt; SRR1274581     3  0.6267     -0.540 0.452 0.000 0.548
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1274528     2  0.1022      0.863 0.000 0.968 0.000 0.032
#&gt; SRR1274529     4  0.4164      0.821 0.000 0.264 0.000 0.736
#&gt; SRR1274530     4  0.3688      0.851 0.000 0.208 0.000 0.792
#&gt; SRR1274531     4  0.7486      0.486 0.000 0.188 0.348 0.464
#&gt; SRR1274532     2  0.1706      0.862 0.016 0.948 0.000 0.036
#&gt; SRR1274533     2  0.2867      0.814 0.012 0.884 0.000 0.104
#&gt; SRR1274534     2  0.2654      0.815 0.004 0.888 0.000 0.108
#&gt; SRR1274535     2  0.6168      0.326 0.000 0.556 0.388 0.056
#&gt; SRR1274536     4  0.3626      0.850 0.004 0.184 0.000 0.812
#&gt; SRR1274537     2  0.1661      0.847 0.004 0.944 0.000 0.052
#&gt; SRR1274538     2  0.2011      0.836 0.000 0.920 0.000 0.080
#&gt; SRR1274539     2  0.2805      0.819 0.000 0.888 0.012 0.100
#&gt; SRR1274540     2  0.1890      0.853 0.008 0.936 0.000 0.056
#&gt; SRR1274541     2  0.1118      0.862 0.000 0.964 0.000 0.036
#&gt; SRR1274542     2  0.2494      0.853 0.048 0.916 0.000 0.036
#&gt; SRR1274543     2  0.1302      0.860 0.000 0.956 0.000 0.044
#&gt; SRR1274544     2  0.1833      0.862 0.024 0.944 0.000 0.032
#&gt; SRR1274545     4  0.4624      0.747 0.000 0.340 0.000 0.660
#&gt; SRR1274546     2  0.0336      0.865 0.000 0.992 0.000 0.008
#&gt; SRR1274547     4  0.4761      0.700 0.000 0.372 0.000 0.628
#&gt; SRR1274548     2  0.1716      0.850 0.000 0.936 0.000 0.064
#&gt; SRR1274549     4  0.5510      0.465 0.008 0.032 0.276 0.684
#&gt; SRR1274550     3  0.0000      0.981 0.000 0.000 1.000 0.000
#&gt; SRR1274551     2  0.2125      0.839 0.004 0.920 0.000 0.076
#&gt; SRR1274552     3  0.0927      0.967 0.008 0.000 0.976 0.016
#&gt; SRR1274553     3  0.2060      0.921 0.052 0.000 0.932 0.016
#&gt; SRR1274554     2  0.4610      0.748 0.100 0.800 0.000 0.100
#&gt; SRR1274555     3  0.0188      0.980 0.000 0.000 0.996 0.004
#&gt; SRR1274556     3  0.0188      0.980 0.000 0.000 0.996 0.004
#&gt; SRR1274557     3  0.0000      0.981 0.000 0.000 1.000 0.000
#&gt; SRR1274558     2  0.0000      0.864 0.000 1.000 0.000 0.000
#&gt; SRR1274559     2  0.7383      0.123 0.424 0.464 0.024 0.088
#&gt; SRR1274560     1  0.7810      0.603 0.576 0.164 0.216 0.044
#&gt; SRR1274561     1  0.6227      0.756 0.672 0.004 0.212 0.112
#&gt; SRR1274562     1  0.4998      0.497 0.512 0.000 0.488 0.000
#&gt; SRR1274563     3  0.0000      0.981 0.000 0.000 1.000 0.000
#&gt; SRR1274564     4  0.3626      0.850 0.004 0.184 0.000 0.812
#&gt; SRR1274565     4  0.4991      0.667 0.004 0.388 0.000 0.608
#&gt; SRR1274566     4  0.3710      0.852 0.004 0.192 0.000 0.804
#&gt; SRR1274567     4  0.3626      0.850 0.004 0.184 0.000 0.812
#&gt; SRR1274568     2  0.1022      0.861 0.000 0.968 0.000 0.032
#&gt; SRR1274569     1  0.4511      0.798 0.724 0.000 0.268 0.008
#&gt; SRR1274570     1  0.3837      0.817 0.776 0.000 0.224 0.000
#&gt; SRR1274571     1  0.3801      0.818 0.780 0.000 0.220 0.000
#&gt; SRR1274572     1  0.3945      0.819 0.780 0.000 0.216 0.004
#&gt; SRR1274573     2  0.1724      0.862 0.020 0.948 0.000 0.032
#&gt; SRR1274574     2  0.3428      0.746 0.012 0.844 0.000 0.144
#&gt; SRR1274575     4  0.3688      0.851 0.000 0.208 0.000 0.792
#&gt; SRR1274576     2  0.2081      0.832 0.000 0.916 0.000 0.084
#&gt; SRR1274577     2  0.2611      0.822 0.008 0.896 0.000 0.096
#&gt; SRR1274578     1  0.0657      0.705 0.984 0.004 0.000 0.012
#&gt; SRR1274579     1  0.2081      0.772 0.916 0.000 0.084 0.000
#&gt; SRR1274580     1  0.3219      0.810 0.836 0.000 0.164 0.000
#&gt; SRR1274581     1  0.6477      0.585 0.552 0.000 0.368 0.080
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1274528     2  0.1750      0.831 0.000 0.936 0.000 0.036 0.028
#&gt; SRR1274529     4  0.4473      0.604 0.000 0.324 0.000 0.656 0.020
#&gt; SRR1274530     4  0.1768      0.727 0.000 0.072 0.000 0.924 0.004
#&gt; SRR1274531     4  0.5104      0.374 0.000 0.044 0.304 0.644 0.008
#&gt; SRR1274532     2  0.2122      0.823 0.008 0.924 0.000 0.032 0.036
#&gt; SRR1274533     2  0.2818      0.793 0.000 0.856 0.012 0.000 0.132
#&gt; SRR1274534     2  0.3885      0.689 0.000 0.724 0.008 0.000 0.268
#&gt; SRR1274535     2  0.6597      0.225 0.000 0.460 0.296 0.000 0.244
#&gt; SRR1274536     4  0.0955      0.716 0.004 0.028 0.000 0.968 0.000
#&gt; SRR1274537     2  0.0703      0.833 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1274538     2  0.1792      0.806 0.000 0.916 0.000 0.084 0.000
#&gt; SRR1274539     2  0.4790      0.645 0.000 0.676 0.032 0.008 0.284
#&gt; SRR1274540     2  0.2520      0.808 0.000 0.896 0.000 0.056 0.048
#&gt; SRR1274541     2  0.1082      0.831 0.000 0.964 0.000 0.028 0.008
#&gt; SRR1274542     2  0.1740      0.824 0.012 0.932 0.000 0.000 0.056
#&gt; SRR1274543     2  0.1197      0.825 0.000 0.952 0.000 0.048 0.000
#&gt; SRR1274544     2  0.1605      0.828 0.012 0.944 0.000 0.004 0.040
#&gt; SRR1274545     4  0.5065      0.430 0.000 0.420 0.000 0.544 0.036
#&gt; SRR1274546     2  0.0162      0.834 0.000 0.996 0.000 0.000 0.004
#&gt; SRR1274547     4  0.4192      0.487 0.000 0.404 0.000 0.596 0.000
#&gt; SRR1274548     2  0.3346      0.804 0.000 0.844 0.000 0.064 0.092
#&gt; SRR1274549     4  0.3066      0.596 0.008 0.012 0.116 0.860 0.004
#&gt; SRR1274550     3  0.1792      0.836 0.000 0.000 0.916 0.000 0.084
#&gt; SRR1274551     2  0.2172      0.806 0.000 0.908 0.000 0.076 0.016
#&gt; SRR1274552     3  0.3446      0.749 0.004 0.004 0.812 0.008 0.172
#&gt; SRR1274553     3  0.3936      0.744 0.052 0.000 0.800 0.004 0.144
#&gt; SRR1274554     2  0.2529      0.818 0.040 0.900 0.004 0.000 0.056
#&gt; SRR1274555     3  0.0324      0.860 0.004 0.000 0.992 0.000 0.004
#&gt; SRR1274556     3  0.1364      0.829 0.012 0.000 0.952 0.000 0.036
#&gt; SRR1274557     3  0.0451      0.859 0.004 0.000 0.988 0.000 0.008
#&gt; SRR1274558     2  0.0404      0.834 0.000 0.988 0.000 0.000 0.012
#&gt; SRR1274559     2  0.7472      0.223 0.176 0.500 0.008 0.056 0.260
#&gt; SRR1274560     1  0.5800      0.591 0.708 0.064 0.052 0.160 0.016
#&gt; SRR1274561     1  0.5335      0.552 0.676 0.000 0.112 0.208 0.004
#&gt; SRR1274562     1  0.4446      0.327 0.592 0.000 0.400 0.000 0.008
#&gt; SRR1274563     3  0.0579      0.857 0.008 0.000 0.984 0.000 0.008
#&gt; SRR1274564     4  0.1197      0.727 0.000 0.048 0.000 0.952 0.000
#&gt; SRR1274565     4  0.5005      0.497 0.004 0.388 0.000 0.580 0.028
#&gt; SRR1274566     4  0.0880      0.720 0.000 0.032 0.000 0.968 0.000
#&gt; SRR1274567     4  0.1369      0.711 0.008 0.028 0.000 0.956 0.008
#&gt; SRR1274568     2  0.4765      0.697 0.000 0.704 0.000 0.068 0.228
#&gt; SRR1274569     1  0.3619      0.774 0.844 0.000 0.092 0.036 0.028
#&gt; SRR1274570     1  0.1952      0.797 0.912 0.000 0.084 0.004 0.000
#&gt; SRR1274571     1  0.2112      0.796 0.908 0.000 0.084 0.004 0.004
#&gt; SRR1274572     1  0.1544      0.799 0.932 0.000 0.068 0.000 0.000
#&gt; SRR1274573     2  0.0968      0.834 0.012 0.972 0.000 0.012 0.004
#&gt; SRR1274574     2  0.3205      0.693 0.004 0.816 0.000 0.176 0.004
#&gt; SRR1274575     4  0.1410      0.729 0.000 0.060 0.000 0.940 0.000
#&gt; SRR1274576     2  0.2020      0.813 0.000 0.900 0.000 0.000 0.100
#&gt; SRR1274577     2  0.3968      0.681 0.004 0.716 0.004 0.000 0.276
#&gt; SRR1274578     1  0.0703      0.765 0.976 0.000 0.000 0.000 0.024
#&gt; SRR1274579     1  0.0000      0.776 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1274580     1  0.0510      0.786 0.984 0.000 0.016 0.000 0.000
#&gt; SRR1274581     5  0.7136      0.000 0.232 0.000 0.296 0.024 0.448
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1274528     2  0.2830     0.6959 0.000 0.836 0.000 0.020 0.144 0.000
#&gt; SRR1274529     2  0.4960     0.3401 0.000 0.568 0.000 0.376 0.032 0.024
#&gt; SRR1274530     4  0.2400     0.8337 0.000 0.116 0.000 0.872 0.008 0.004
#&gt; SRR1274531     4  0.4818     0.5462 0.000 0.072 0.272 0.648 0.008 0.000
#&gt; SRR1274532     2  0.0790     0.7648 0.000 0.968 0.000 0.000 0.032 0.000
#&gt; SRR1274533     2  0.4483     0.0687 0.000 0.548 0.016 0.004 0.428 0.004
#&gt; SRR1274534     5  0.3672     0.5801 0.000 0.304 0.008 0.000 0.688 0.000
#&gt; SRR1274535     5  0.5032     0.4444 0.000 0.132 0.216 0.000 0.648 0.004
#&gt; SRR1274536     4  0.1296     0.8969 0.004 0.044 0.000 0.948 0.004 0.000
#&gt; SRR1274537     2  0.2416     0.6840 0.000 0.844 0.000 0.000 0.156 0.000
#&gt; SRR1274538     2  0.1320     0.7685 0.000 0.948 0.000 0.036 0.016 0.000
#&gt; SRR1274539     5  0.3895     0.5834 0.000 0.284 0.016 0.004 0.696 0.000
#&gt; SRR1274540     2  0.1313     0.7661 0.000 0.952 0.000 0.016 0.028 0.004
#&gt; SRR1274541     2  0.0508     0.7691 0.000 0.984 0.000 0.012 0.004 0.000
#&gt; SRR1274542     2  0.1881     0.7500 0.008 0.928 0.000 0.012 0.044 0.008
#&gt; SRR1274543     2  0.1564     0.7628 0.000 0.936 0.000 0.024 0.040 0.000
#&gt; SRR1274544     2  0.1194     0.7607 0.004 0.956 0.000 0.008 0.032 0.000
#&gt; SRR1274545     2  0.4514     0.5559 0.000 0.680 0.000 0.264 0.040 0.016
#&gt; SRR1274546     2  0.0972     0.7660 0.000 0.964 0.000 0.008 0.028 0.000
#&gt; SRR1274547     2  0.3945     0.4340 0.000 0.612 0.000 0.380 0.008 0.000
#&gt; SRR1274548     2  0.3993     0.4992 0.000 0.700 0.000 0.024 0.272 0.004
#&gt; SRR1274549     4  0.2372     0.8491 0.008 0.024 0.036 0.908 0.024 0.000
#&gt; SRR1274550     3  0.3383     0.5548 0.000 0.000 0.728 0.004 0.268 0.000
#&gt; SRR1274551     2  0.0790     0.7695 0.000 0.968 0.000 0.032 0.000 0.000
#&gt; SRR1274552     5  0.4491    -0.2367 0.000 0.000 0.476 0.008 0.500 0.016
#&gt; SRR1274553     5  0.5968    -0.2568 0.084 0.000 0.440 0.008 0.440 0.028
#&gt; SRR1274554     2  0.4119     0.6727 0.016 0.800 0.008 0.028 0.120 0.028
#&gt; SRR1274555     3  0.0363     0.8645 0.012 0.000 0.988 0.000 0.000 0.000
#&gt; SRR1274556     3  0.1780     0.8325 0.024 0.000 0.932 0.004 0.004 0.036
#&gt; SRR1274557     3  0.0291     0.8620 0.004 0.000 0.992 0.000 0.004 0.000
#&gt; SRR1274558     2  0.1812     0.7445 0.000 0.912 0.000 0.008 0.080 0.000
#&gt; SRR1274559     2  0.6824     0.4550 0.032 0.616 0.048 0.064 0.164 0.076
#&gt; SRR1274560     1  0.3900     0.6835 0.804 0.056 0.020 0.112 0.008 0.000
#&gt; SRR1274561     1  0.5695     0.3625 0.544 0.000 0.260 0.192 0.000 0.004
#&gt; SRR1274562     1  0.3864     0.2312 0.520 0.000 0.480 0.000 0.000 0.000
#&gt; SRR1274563     3  0.1196     0.8499 0.040 0.000 0.952 0.000 0.008 0.000
#&gt; SRR1274564     4  0.2002     0.8921 0.004 0.052 0.000 0.920 0.012 0.012
#&gt; SRR1274565     2  0.4883     0.3890 0.000 0.588 0.000 0.356 0.040 0.016
#&gt; SRR1274566     4  0.1219     0.8974 0.004 0.048 0.000 0.948 0.000 0.000
#&gt; SRR1274567     4  0.1523     0.8940 0.008 0.044 0.000 0.940 0.008 0.000
#&gt; SRR1274568     5  0.5003     0.2320 0.004 0.440 0.000 0.048 0.504 0.004
#&gt; SRR1274569     1  0.2078     0.7927 0.912 0.000 0.040 0.044 0.004 0.000
#&gt; SRR1274570     1  0.0837     0.8118 0.972 0.000 0.020 0.004 0.000 0.004
#&gt; SRR1274571     1  0.0922     0.8115 0.968 0.000 0.024 0.004 0.000 0.004
#&gt; SRR1274572     1  0.0951     0.8121 0.968 0.000 0.020 0.000 0.004 0.008
#&gt; SRR1274573     2  0.0951     0.7675 0.008 0.968 0.000 0.004 0.020 0.000
#&gt; SRR1274574     2  0.1643     0.7614 0.000 0.924 0.000 0.068 0.008 0.000
#&gt; SRR1274575     4  0.1700     0.8792 0.000 0.080 0.000 0.916 0.004 0.000
#&gt; SRR1274576     2  0.3827     0.4434 0.000 0.680 0.000 0.008 0.308 0.004
#&gt; SRR1274577     5  0.3894     0.5344 0.004 0.324 0.000 0.000 0.664 0.008
#&gt; SRR1274578     1  0.2180     0.7712 0.912 0.004 0.008 0.000 0.048 0.028
#&gt; SRR1274579     1  0.1176     0.7969 0.956 0.000 0.000 0.000 0.024 0.020
#&gt; SRR1274580     1  0.1078     0.8061 0.964 0.000 0.008 0.000 0.016 0.012
#&gt; SRR1274581     6  0.3206     0.0000 0.068 0.000 0.104 0.000 0.000 0.828
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


