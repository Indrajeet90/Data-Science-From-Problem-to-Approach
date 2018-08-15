
<a href="https://cognitiveclass.ai"><img src = "https://ibm.box.com/shared/static/9gegpsmnsoo25ikkbl4qzlvlyjbgxs5x.png" width = 400> </a>

<h1 align=center><font size = 5>From Understanding to Preparation</font></h1>

## Introduction

In this lab, we will continue learning about the data science methodology, and focus on the **Data Understanding** and the **Data Preparation** stages.

## Table of Contents

<div class="alert alert-block alert-info" style="margin-top: 20px">
1. [Recap](#0)<br>
2. [Data Understanding](#2)<br>
3. [Data Preparation](#4)<br>
</div>
<hr>

# Recap <a id="0"></a>

In Lab **From Requirements to Collection**, we learned that the data we need to answer the question developed in the business understanding stage, namely *can we automate the process of determining the cuisine of a given recipe?*, is readily available. A researcher named Yong-Yeol Ahn scraped tens of thousands of food recipes (cuisines and ingredients) from three different websites, namely:

<img src = "https://ibm.box.com/shared/static/4fruwan7wmjov3gywiz3swlojw0srv54.png" width=500>

www.allrecipes.com

<img src = "https://ibm.box.com/shared/static/cebfdbr22fjxa47lltp0bs533r103g0z.png" width=500>

www.epicurious.com

<img src = "https://ibm.box.com/shared/static/epk727njg7xrz49pbkpkzd05cm5ywqmu.png" width=500>

www.menupan.com

For more information on Yong-Yeol Ahn and his research, you can read his paper on [Flavor Network and the Principles of Food Pairing](http://yongyeol.com/papers/ahn-flavornet-2011.pdf).

We also collected the data and placed it on an IBM server for your convenience.

------------

# Data Understanding <a id="2"></a>

<img src="https://ibm.box.com/shared/static/89geb3m0ge1z73s92hl8o8wdcpcrggtz.png" width=500>

<strong>Important note:</strong> Please note that you are not expected to know how to program in R. The following code is meant to illustrate the stages of data understanding and data preparation, so it is totally fine if you do not understand the individual lines of code. We have a full course on programming in R, <a href="http://cocl.us/RP0101EN_DS0103EN_LAB3_R">R101</a>, so please feel free to complete the course if you are interested in learning how to program in R.

### Using this notebook:

To run any of the following cells of code, you can type **Shift + Enter** to excute the code in a cell.

Get the version of R installed.


```R
# check R version
R.Version()$version.string
```


'R version 3.3.2 (2016-10-31)'


Download the data from the IBM server.


```R
# click here and press Shift + Enter
download.file("https://ibm.box.com/shared/static/5wah9atr5o1akuuavl2z9tkjzdinr1lv.csv",
              destfile = "/resources/data/recipes.csv", quiet = TRUE)

recipes <- read.csv("/resources/data/recipes.csv") # takes 30 seconds
```

Show the first few rows.


```R
head(recipes)
```


<table>
<thead><tr><th scope=col>country</th><th scope=col>almond</th><th scope=col>angelica</th><th scope=col>anise</th><th scope=col>anise_seed</th><th scope=col>apple</th><th scope=col>apple_brandy</th><th scope=col>apricot</th><th scope=col>armagnac</th><th scope=col>artemisia</th><th scope=col>⋯</th><th scope=col>whiskey</th><th scope=col>white_bread</th><th scope=col>white_wine</th><th scope=col>whole_grain_wheat_flour</th><th scope=col>wine</th><th scope=col>wood</th><th scope=col>yam</th><th scope=col>yeast</th><th scope=col>yogurt</th><th scope=col>zucchini</th></tr></thead>
<tbody>
	<tr><td>Vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>Vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>Vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>Vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>Vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>Vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
</tbody>
</table>



Get the dimensions of the dataframe.


```R
nrow(recipes)
```


57691



```R
ncol(recipes)
```


384


So our dataset consists of 57,691 recipes. Each row represents a recipe, and for each recipe, the corresponding cuisine is documented as well as whether 384 ingredients exist in the recipe or not beginning with almond and ending with zucchini.

We know that a basic sushi recipe includes the ingredients:
* rice
* soy sauce
* wasabi
* some fish/vegetables

Let's check that these ingredients exist in our dataframe:


```R
grep("rice", names(recipes), value = TRUE) # yes as rice
grep("wasabi", names(recipes), value = TRUE) # yes
grep("soy", names(recipes), value = TRUE) # yes as soy_sauce
```


<ol class=list-inline>
	<li>'brown_rice'</li>
	<li>'licorice'</li>
	<li>'rice'</li>
</ol>




'wasabi'



<ol class=list-inline>
	<li>'soy_sauce'</li>
	<li>'soybean'</li>
	<li>'soybean_oil'</li>
</ol>



Yes, they do!

* rice exists as rice.
* wasabi exists as wasabi.
* soy exists as soy_sauce.

So maybe if a recipe contains all three ingredients: rice, wasabi, and soy_sauce, then we can confidently say that the recipe is a **Japanese** cuisine! Let's keep this in mind!

----------------

# Data Preparation <a id="4"></a>

<img src="https://ibm.box.com/shared/static/lqc2j3r0ndhokh77mubohwjqybzf8dhk.png" width=500>

In this section, we will prepare the data for the next stage in the data science methodology, which is modeling. This stage involves exploring the data further and making sure that it is in the right format for the machine learning algorithm that we selected in the analytic approach stage, which is decision trees.

First, look at the data to see if it needs cleaning.


```R
base::table(recipes$country) # frequency table
```


    
                    African                American                   asian 
                        115                   40150                      17 
                      Asian                 Austria              Bangladesh 
                       1176                      21                       4 
                    Belgium            Cajun_Creole                  Canada 
                         11                     146                     774 
                  Caribbean   Central_SouthAmerican                   China 
                        183                     241                     130 
                    chinese                 Chinese              east_asian 
                         86                     226                     951 
               East-African          Eastern-Europe EasternEuropean_Russian 
                         11                     235                     146 
           English_Scottish                  France                  French 
                        204                     268                     996 
                     German                 Germany                   Greek 
                         52                     237                     225 
                      India                  Indian               Indonesia 
                        324                     274                      12 
                       Iran                   Irish                  Israel 
                         21                      86                       9 
                    italian                 Italian                   Italy 
                         74                    1715                    1461 
                      Japan                japanese                Japanese 
                         85                      99                     136 
                     Jewish                   Korea                  korean 
                        320                      32                     767 
                    Lebanon                Malaysia           Mediterranean 
                         31                      18                     289 
                    Mexican                  mexico                  Mexico 
                        622                      14                    1754 
              MiddleEastern                Moroccan             Netherlands 
                        248                     137                      32 
              North-African                Pakistan             Philippines 
                         60                      19                      43 
                   Portugal             Scandinavia            Scandinavian 
                         50                     158                      92 
              South-African           South-America       Southern_SoulFood 
                         16                     103                     346 
               Southwestern                   Spain      Spanish_Portuguese 
                        108                      75                     291 
                Switzerland                    Thai                Thailand 
                         20                     164                     125 
                     Turkey          UK-and-Ireland                 Vietnam 
                         16                     282                      30 
                 Vietnamese            West-African                 western 
                         65                      13                     450 


By looking at the above table, we can make the following observations:

1. Cuisine column is labeled as Country, which is inaccurate.
2. Cuisine names are not consistent as not all of them start with an uppercase first letter.
3. Some cuisines are duplicated as variation of the country name, such as Vietnam and Vietnamese.
4. Some cuisines have very few recipes.

#### Let's fixes these problems.

Fix the name of the column showing the cuisine.


```R
colnames(recipes)[1] = "cuisine"
```

Make all the cuisine names lowercase.


```R
recipes$cuisine <- tolower(as.character(recipes$cuisine))

recipes
```


<table>
<thead><tr><th scope=col>cuisine</th><th scope=col>almond</th><th scope=col>angelica</th><th scope=col>anise</th><th scope=col>anise_seed</th><th scope=col>apple</th><th scope=col>apple_brandy</th><th scope=col>apricot</th><th scope=col>armagnac</th><th scope=col>artemisia</th><th scope=col>⋯</th><th scope=col>whiskey</th><th scope=col>white_bread</th><th scope=col>white_wine</th><th scope=col>whole_grain_wheat_flour</th><th scope=col>wine</th><th scope=col>wood</th><th scope=col>yam</th><th scope=col>yeast</th><th scope=col>yogurt</th><th scope=col>zucchini</th></tr></thead>
<tbody>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋱</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>Yes  </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>Yes  </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>Yes  </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>Yes  </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>Yes  </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>Yes  </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
	<tr><td>japan</td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>⋯    </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td><td>No   </td></tr>
</tbody>
</table>



Make the cuisine names consistent.


```R
recipes$cuisine[recipes$cuisine == "austria"] <- "austrian"
recipes$cuisine[recipes$cuisine == "belgium"] <- "belgian"
recipes$cuisine[recipes$cuisine == "china"] <- "chinese"
recipes$cuisine[recipes$cuisine == "canada"] <- "canadian"
recipes$cuisine[recipes$cuisine == "netherlands"] <- "dutch"
recipes$cuisine[recipes$cuisine == "france"] <- "french"
recipes$cuisine[recipes$cuisine == "germany"] <- "german"
recipes$cuisine[recipes$cuisine == "india"] <- "indian"
recipes$cuisine[recipes$cuisine == "indonesia"] <- "indonesian"
recipes$cuisine[recipes$cuisine == "iran"] <- "iranian"
recipes$cuisine[recipes$cuisine == "israel"] <- "jewish"
recipes$cuisine[recipes$cuisine == "italy"] <- "italian"
recipes$cuisine[recipes$cuisine == "japan"] <- "japanese"
recipes$cuisine[recipes$cuisine == "korea"] <- "korean"
recipes$cuisine[recipes$cuisine == "lebanon"] <- "lebanese"
recipes$cuisine[recipes$cuisine == "malaysia"] <- "malaysian"
recipes$cuisine[recipes$cuisine == "mexico"] <- "mexican"
recipes$cuisine[recipes$cuisine == "pakistan"] <- "pakistani"
recipes$cuisine[recipes$cuisine == "philippines"] <- "philippine"
recipes$cuisine[recipes$cuisine == "scandinavia"] <- "scandinavian"
recipes$cuisine[recipes$cuisine == "spain"] <- "spanish_portuguese"
recipes$cuisine[recipes$cuisine == "portugal"] <- "spanish_portuguese"
recipes$cuisine[recipes$cuisine == "switzerland"] <- "swiss"
recipes$cuisine[recipes$cuisine == "thailand"] <- "thai"
recipes$cuisine[recipes$cuisine == "turkey"] <- "turkish"
recipes$cuisine[recipes$cuisine == "irish"] <- "uk-and-irish"
recipes$cuisine[recipes$cuisine == "uk-and-ireland"] <- "uk-and-irish"
recipes$cuisine[recipes$cuisine == "vietnam"] <- "vietnamese"

recipes
```


<table>
<thead><tr><th scope=col>cuisine</th><th scope=col>almond</th><th scope=col>angelica</th><th scope=col>anise</th><th scope=col>anise_seed</th><th scope=col>apple</th><th scope=col>apple_brandy</th><th scope=col>apricot</th><th scope=col>armagnac</th><th scope=col>artemisia</th><th scope=col>⋯</th><th scope=col>whiskey</th><th scope=col>white_bread</th><th scope=col>white_wine</th><th scope=col>whole_grain_wheat_flour</th><th scope=col>wine</th><th scope=col>wood</th><th scope=col>yam</th><th scope=col>yeast</th><th scope=col>yogurt</th><th scope=col>zucchini</th></tr></thead>
<tbody>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋱</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
</tbody>
</table>



Remove cuisines with < 50 recipes:


```R
# sort the table of cuisines by descending order
t <- sort(base::table(recipes$cuisine), decreasing = T)

t
```


    
                   american                 italian                 mexican 
                      40150                    3250                    2390 
                     french                   asian              east_asian 
                       1264                    1193                     951 
                     korean                canadian                  indian 
                        799                     774                     598 
                    western                 chinese      spanish_portuguese 
                        450                     442                     416 
               uk-and-irish       southern_soulfood                  jewish 
                        368                     346                     329 
                   japanese                  german           mediterranean 
                        320                     289                     289 
                       thai            scandinavian           middleeastern 
                        289                     250                     248 
      central_southamerican          eastern-europe                   greek 
                        241                     235                     225 
           english_scottish               caribbean            cajun_creole 
                        204                     183                     146 
    easterneuropean_russian                moroccan                 african 
                        146                     137                     115 
               southwestern           south-america              vietnamese 
                        108                     103                      95 
              north-african              philippine                   dutch 
                         60                      43                      32 
                   lebanese                austrian                 iranian 
                         31                      21                      21 
                      swiss               pakistani               malaysian 
                         20                      19                      18 
              south-african                 turkish            west-african 
                         16                      16                      13 
                 indonesian                 belgian            east-african 
                         12                      11                      11 
                 bangladesh 
                          4 



```R
# get cuisines with >= 50 recipes
filter_list <- names(t[t >= 50])

filter_list
```


<ol class=list-inline>
	<li>'american'</li>
	<li>'italian'</li>
	<li>'mexican'</li>
	<li>'french'</li>
	<li>'asian'</li>
	<li>'east_asian'</li>
	<li>'korean'</li>
	<li>'canadian'</li>
	<li>'indian'</li>
	<li>'western'</li>
	<li>'chinese'</li>
	<li>'spanish_portuguese'</li>
	<li>'uk-and-irish'</li>
	<li>'southern_soulfood'</li>
	<li>'jewish'</li>
	<li>'japanese'</li>
	<li>'german'</li>
	<li>'mediterranean'</li>
	<li>'thai'</li>
	<li>'scandinavian'</li>
	<li>'middleeastern'</li>
	<li>'central_southamerican'</li>
	<li>'eastern-europe'</li>
	<li>'greek'</li>
	<li>'english_scottish'</li>
	<li>'caribbean'</li>
	<li>'cajun_creole'</li>
	<li>'easterneuropean_russian'</li>
	<li>'moroccan'</li>
	<li>'african'</li>
	<li>'southwestern'</li>
	<li>'south-america'</li>
	<li>'vietnamese'</li>
	<li>'north-african'</li>
</ol>




```R
before <- nrow(recipes) # number of rows of original dataframe
print(paste0("Number of rows of original dataframe is ", before))

recipes <- recipes[recipes$cuisine %in% filter_list,]

after <- nrow(recipes)
print(paste0("Number of rows of processed dataframe is ", after))

print(paste0(before - after, " rows removed!"))
```

    [1] "Number of rows of original dataframe is 57691"
    [1] "Number of rows of processed dataframe is 57403"
    [1] "288 rows removed!"


Convert all of the columns into factors. This is to run the classification model later.


```R
recipes[,names(recipes)] <- lapply(recipes[,names(recipes)], as.factor)

recipes
```


<table>
<thead><tr><th></th><th scope=col>cuisine</th><th scope=col>almond</th><th scope=col>angelica</th><th scope=col>anise</th><th scope=col>anise_seed</th><th scope=col>apple</th><th scope=col>apple_brandy</th><th scope=col>apricot</th><th scope=col>armagnac</th><th scope=col>artemisia</th><th scope=col>⋯</th><th scope=col>whiskey</th><th scope=col>white_bread</th><th scope=col>white_wine</th><th scope=col>whole_grain_wheat_flour</th><th scope=col>wine</th><th scope=col>wood</th><th scope=col>yam</th><th scope=col>yeast</th><th scope=col>yogurt</th><th scope=col>zucchini</th></tr></thead>
<tbody>
	<tr><th scope=row>1</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>2</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>3</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>4</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>5</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>6</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>7</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>8</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>9</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>10</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>11</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>12</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>13</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>14</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>15</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>16</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>17</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>18</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>19</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>20</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>21</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>22</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>23</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>24</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>25</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>26</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>27</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>28</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>29</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>30</th><td>vietnamese</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>⋮</th><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋱</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td></tr>
	<tr><th scope=row>57662</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57663</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57664</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57665</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57666</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57667</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57668</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57669</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57670</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57671</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57672</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57673</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57674</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57675</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57676</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57677</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57678</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57679</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57680</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57681</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57682</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57683</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57684</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57685</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>Yes     </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57686</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57687</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57688</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57689</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57690</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
	<tr><th scope=row>57691</th><td>japanese</td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>⋯       </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td><td>No      </td></tr>
</tbody>
</table>



In R, you can check the structure of your data using the **str** function. Let's check the structure of our dataframe **recipes**.


```R
str(recipes)
```

    'data.frame':	57403 obs. of  384 variables:
     $ cuisine                : Factor w/ 34 levels "african","american",..: 33 33 33 33 33 33 33 33 33 33 ...
     $ almond                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ angelica               : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ anise                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ anise_seed             : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ apple                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ apple_brandy           : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ apricot                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ armagnac               : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ artemisia              : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ artichoke              : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ asparagus              : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ avocado                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ bacon                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ baked_potato           : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ balm                   : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ banana                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ barley                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ bartlett_pear          : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ basil                  : Factor w/ 2 levels "No","Yes": 2 1 1 2 1 2 2 1 1 1 ...
     $ bay                    : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ bean                   : Factor w/ 2 levels "No","Yes": 1 1 1 2 1 1 1 2 1 1 ...
     $ beech                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ beef                   : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 2 1 1 1 1 ...
     $ beef_broth             : Factor w/ 2 levels "No","Yes": 1 1 1 2 1 1 1 1 1 1 ...
     $ beef_liver             : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ beer                   : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ beet                   : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ bell_pepper            : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ bergamot               : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ berry                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ bitter_orange          : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ black_bean             : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ black_currant          : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ black_mustard_seed_oil : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ black_pepper           : Factor w/ 2 levels "No","Yes": 1 2 1 1 1 1 2 2 1 2 ...
     $ black_raspberry        : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ black_sesame_seed      : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ black_tea              : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ blackberry             : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ blackberry_brandy      : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ blue_cheese            : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ blueberry              : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ bone_oil               : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ bourbon_whiskey        : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ brandy                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ brassica               : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ bread                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 2 1 1 ...
     $ broccoli               : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ brown_rice             : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ brussels_sprout        : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ buckwheat              : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ butter                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 2 1 1 ...
     $ buttermilk             : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cabbage                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cabernet_sauvignon_wine: Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cacao                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ camembert_cheese       : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cane_molasses          : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ caraway                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cardamom               : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ carnation              : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ carob                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ carrot                 : Factor w/ 2 levels "No","Yes": 2 1 1 1 1 1 1 2 1 1 ...
     $ cashew                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cassava                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ catfish                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cauliflower            : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ caviar                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cayenne                : Factor w/ 2 levels "No","Yes": 2 2 1 2 2 1 2 2 2 2 ...
     $ celery                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ celery_oil             : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cereal                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ chamomile              : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ champagne_wine         : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ chayote                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cheddar_cheese         : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cheese                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cherry                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cherry_brandy          : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ chervil                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ chicken                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 2 1 1 2 ...
     $ chicken_broth          : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 2 ...
     $ chicken_liver          : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ chickpea               : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ chicory                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ chinese_cabbage        : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ chive                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cider                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cilantro               : Factor w/ 2 levels "No","Yes": 2 1 1 2 1 1 1 1 1 1 ...
     $ cinnamon               : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ citrus                 : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ citrus_peel            : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ clam                   : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ clove                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cocoa                  : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ coconut                : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 2 ...
     $ coconut_oil            : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
     $ cod                    : Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
      [list output truncated]


#### Let's analyze the data a little more in order to learn the data better and note any interesting preliminary observations.

Run the following cell to get the recipes that contain **rice** *and* **soy** *and* **wasabi** *and* **seaweed**.


```R
check_recipes <- recipes[
    recipes$rice == "Yes" &
    recipes$soy_sauce == "Yes" &
    recipes$wasabi == "Yes" &
    recipes$seaweed == "Yes",
]

check_recipes
```


<table>
<thead><tr><th></th><th scope=col>cuisine</th><th scope=col>almond</th><th scope=col>angelica</th><th scope=col>anise</th><th scope=col>anise_seed</th><th scope=col>apple</th><th scope=col>apple_brandy</th><th scope=col>apricot</th><th scope=col>armagnac</th><th scope=col>artemisia</th><th scope=col>⋯</th><th scope=col>whiskey</th><th scope=col>white_bread</th><th scope=col>white_wine</th><th scope=col>whole_grain_wheat_flour</th><th scope=col>wine</th><th scope=col>wood</th><th scope=col>yam</th><th scope=col>yeast</th><th scope=col>yogurt</th><th scope=col>zucchini</th></tr></thead>
<tbody>
	<tr><th scope=row>11307</th><td>japanese  </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>11322</th><td>japanese  </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>11362</th><td>japanese  </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>12172</th><td>asian     </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>Yes       </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>12386</th><td>asian     </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>13011</th><td>asian     </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>13160</th><td>asian     </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>13514</th><td>japanese  </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>13587</th><td>japanese  </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>13626</th><td>east_asian</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
	<tr><th scope=row>14496</th><td>east_asian</td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>⋯         </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td><td>No        </td></tr>
</tbody>
</table>



Based on the results of the above code, can we classify all recipes that contain **rice** *and* **soy** *and* **wasabi** *and* **seaweed** as **Japanese** recipes? Why?
Your Answer:
Double-click __here__ for the solution.
<!-- The correct answer is:
No, because other recipes such as Asian and East_Asian recipes also contain these ingredients.
-->

Let's count the ingredients across all recipes.


```R
# sum the row count when the value of the row in a column is equal to "Yes" (value of 2)
ingred <- unlist(
            lapply( recipes[, names(recipes)], function(x) sum(as.integer(x) == 2))
            )

# transpose the dataframe so that each row is an ingredient
ingred <- as.data.frame( t( as.data.frame(ingred) ))
                
ing_df <- data.frame("ingredient" = names(ingred), 
                     "count" = as.numeric(ingred[1,])
                    )[-1,]
                
ing_df
```


<table>
<thead><tr><th></th><th scope=col>ingredient</th><th scope=col>count</th></tr></thead>
<tbody>
	<tr><th scope=row>2</th><td>almond       </td><td>2306         </td></tr>
	<tr><th scope=row>3</th><td>angelica     </td><td>   1         </td></tr>
	<tr><th scope=row>4</th><td>anise        </td><td> 223         </td></tr>
	<tr><th scope=row>5</th><td>anise_seed   </td><td>  87         </td></tr>
	<tr><th scope=row>6</th><td>apple        </td><td>2422         </td></tr>
	<tr><th scope=row>7</th><td>apple_brandy </td><td>  37         </td></tr>
	<tr><th scope=row>8</th><td>apricot      </td><td> 620         </td></tr>
	<tr><th scope=row>9</th><td>armagnac     </td><td>  11         </td></tr>
	<tr><th scope=row>10</th><td>artemisia    </td><td>  13         </td></tr>
	<tr><th scope=row>11</th><td>artichoke    </td><td> 391         </td></tr>
	<tr><th scope=row>12</th><td>asparagus    </td><td> 460         </td></tr>
	<tr><th scope=row>13</th><td>avocado      </td><td> 660         </td></tr>
	<tr><th scope=row>14</th><td>bacon        </td><td>2169         </td></tr>
	<tr><th scope=row>15</th><td>baked_potato </td><td>   9         </td></tr>
	<tr><th scope=row>16</th><td>balm         </td><td>   3         </td></tr>
	<tr><th scope=row>17</th><td>banana       </td><td> 989         </td></tr>
	<tr><th scope=row>18</th><td>barley       </td><td> 266         </td></tr>
	<tr><th scope=row>19</th><td>bartlett_pear</td><td>  23         </td></tr>
	<tr><th scope=row>20</th><td>basil        </td><td>3842         </td></tr>
	<tr><th scope=row>21</th><td>bay          </td><td>1463         </td></tr>
	<tr><th scope=row>22</th><td>bean         </td><td>1992         </td></tr>
	<tr><th scope=row>23</th><td>beech        </td><td>   1         </td></tr>
	<tr><th scope=row>24</th><td>beef         </td><td>4902         </td></tr>
	<tr><th scope=row>25</th><td>beef_broth   </td><td> 845         </td></tr>
	<tr><th scope=row>26</th><td>beef_liver   </td><td>  10         </td></tr>
	<tr><th scope=row>27</th><td>beer         </td><td> 307         </td></tr>
	<tr><th scope=row>28</th><td>beet         </td><td> 233         </td></tr>
	<tr><th scope=row>29</th><td>bell_pepper  </td><td>5979         </td></tr>
	<tr><th scope=row>30</th><td>bergamot     </td><td>   7         </td></tr>
	<tr><th scope=row>31</th><td>berry        </td><td> 183         </td></tr>
	<tr><th scope=row>⋮</th><td>⋮</td><td>⋮</td></tr>
	<tr><th scope=row>355</th><td>thyme                  </td><td> 3043                  </td></tr>
	<tr><th scope=row>356</th><td>tomato                 </td><td> 9920                  </td></tr>
	<tr><th scope=row>357</th><td>tomato_juice           </td><td>  176                  </td></tr>
	<tr><th scope=row>358</th><td>truffle                </td><td>   52                  </td></tr>
	<tr><th scope=row>359</th><td>tuna                   </td><td>  463                  </td></tr>
	<tr><th scope=row>360</th><td>turkey                 </td><td>  901                  </td></tr>
	<tr><th scope=row>361</th><td>turmeric               </td><td> 1291                  </td></tr>
	<tr><th scope=row>362</th><td>turnip                 </td><td>  188                  </td></tr>
	<tr><th scope=row>363</th><td>vanilla                </td><td> 9010                  </td></tr>
	<tr><th scope=row>364</th><td>veal                   </td><td>  197                  </td></tr>
	<tr><th scope=row>365</th><td>vegetable              </td><td> 1703                  </td></tr>
	<tr><th scope=row>366</th><td>vegetable_oil          </td><td>11105                  </td></tr>
	<tr><th scope=row>367</th><td>vinegar                </td><td> 8060                  </td></tr>
	<tr><th scope=row>368</th><td>violet                 </td><td>    5                  </td></tr>
	<tr><th scope=row>369</th><td>walnut                 </td><td> 2729                  </td></tr>
	<tr><th scope=row>370</th><td>wasabi                 </td><td>  135                  </td></tr>
	<tr><th scope=row>371</th><td>watercress             </td><td>  150                  </td></tr>
	<tr><th scope=row>372</th><td>watermelon             </td><td>  110                  </td></tr>
	<tr><th scope=row>373</th><td>wheat                  </td><td>20781                  </td></tr>
	<tr><th scope=row>374</th><td>wheat_bread            </td><td>   82                  </td></tr>
	<tr><th scope=row>375</th><td>whiskey                </td><td>  148                  </td></tr>
	<tr><th scope=row>376</th><td>white_bread            </td><td>  370                  </td></tr>
	<tr><th scope=row>377</th><td>white_wine             </td><td> 2205                  </td></tr>
	<tr><th scope=row>378</th><td>whole_grain_wheat_flour</td><td>  731                  </td></tr>
	<tr><th scope=row>379</th><td>wine                   </td><td> 1026                  </td></tr>
	<tr><th scope=row>380</th><td>wood                   </td><td>   33                  </td></tr>
	<tr><th scope=row>381</th><td>yam                    </td><td>   85                  </td></tr>
	<tr><th scope=row>382</th><td>yeast                  </td><td> 3385                  </td></tr>
	<tr><th scope=row>383</th><td>yogurt                 </td><td> 1033                  </td></tr>
	<tr><th scope=row>384</th><td>zucchini               </td><td> 1102                  </td></tr>
</tbody>
</table>



Now we have a dataframe of ingredients and their total counts across all recipes. Let's sort this dataframe in descending order.


```R
ing_df_sort <- ing_df[order(ing_df$count, decreasing = TRUE),]
rownames(ing_df_sort) <- 1:nrow(ing_df_sort)

ing_df_sort
```


<table>
<thead><tr><th scope=col>ingredient</th><th scope=col>count</th></tr></thead>
<tbody>
	<tr><td>egg          </td><td>21025        </td></tr>
	<tr><td>wheat        </td><td>20781        </td></tr>
	<tr><td>butter       </td><td>20719        </td></tr>
	<tr><td>onion        </td><td>18080        </td></tr>
	<tr><td>garlic       </td><td>17353        </td></tr>
	<tr><td>milk         </td><td>12870        </td></tr>
	<tr><td>vegetable_oil</td><td>11105        </td></tr>
	<tr><td>cream        </td><td>10171        </td></tr>
	<tr><td>tomato       </td><td> 9920        </td></tr>
	<tr><td>olive_oil    </td><td> 9876        </td></tr>
	<tr><td>black_pepper </td><td> 9828        </td></tr>
	<tr><td>pepper       </td><td> 9230        </td></tr>
	<tr><td>vanilla      </td><td> 9010        </td></tr>
	<tr><td>cayenne      </td><td> 8254        </td></tr>
	<tr><td>vinegar      </td><td> 8060        </td></tr>
	<tr><td>cane_molasses</td><td> 7741        </td></tr>
	<tr><td>bell_pepper  </td><td> 5979        </td></tr>
	<tr><td>cinnamon     </td><td> 5594        </td></tr>
	<tr><td>parsley      </td><td> 5552        </td></tr>
	<tr><td>chicken      </td><td> 5436        </td></tr>
	<tr><td>lemon_juice  </td><td> 5065        </td></tr>
	<tr><td>beef         </td><td> 4902        </td></tr>
	<tr><td>corn         </td><td> 4828        </td></tr>
	<tr><td>cocoa        </td><td> 4799        </td></tr>
	<tr><td>scallion     </td><td> 4782        </td></tr>
	<tr><td>bread        </td><td> 4571        </td></tr>
	<tr><td>ginger       </td><td> 4358        </td></tr>
	<tr><td>mustard      </td><td> 4119        </td></tr>
	<tr><td>rice         </td><td> 3857        </td></tr>
	<tr><td>basil        </td><td> 3842        </td></tr>
	<tr><td>⋮</td><td>⋮</td></tr>
	<tr><td>holy_basil      </td><td>3               </td></tr>
	<tr><td>hop             </td><td>3               </td></tr>
	<tr><td>mutton          </td><td>3               </td></tr>
	<tr><td>rapeseed        </td><td>3               </td></tr>
	<tr><td>roasted_almond  </td><td>3               </td></tr>
	<tr><td>jasmine_tea     </td><td>2               </td></tr>
	<tr><td>laurel          </td><td>2               </td></tr>
	<tr><td>long_pepper     </td><td>2               </td></tr>
	<tr><td>pimenta         </td><td>2               </td></tr>
	<tr><td>raw_beef        </td><td>2               </td></tr>
	<tr><td>red_algae       </td><td>2               </td></tr>
	<tr><td>sheep_cheese    </td><td>2               </td></tr>
	<tr><td>soybean_oil     </td><td>2               </td></tr>
	<tr><td>strawberry_juice</td><td>2               </td></tr>
	<tr><td>angelica        </td><td>1               </td></tr>
	<tr><td>beech           </td><td>1               </td></tr>
	<tr><td>emmental_cheese </td><td>1               </td></tr>
	<tr><td>geranium        </td><td>1               </td></tr>
	<tr><td>jamaican_rum    </td><td>1               </td></tr>
	<tr><td>kaffir_lime     </td><td>1               </td></tr>
	<tr><td>lilac_flower_oil</td><td>1               </td></tr>
	<tr><td>mate            </td><td>1               </td></tr>
	<tr><td>muscat_grape    </td><td>1               </td></tr>
	<tr><td>pelargonium     </td><td>1               </td></tr>
	<tr><td>roasted_hazelnut</td><td>1               </td></tr>
	<tr><td>roasted_nut     </td><td>1               </td></tr>
	<tr><td>roasted_pecan   </td><td>1               </td></tr>
	<tr><td>strawberry_jam  </td><td>1               </td></tr>
	<tr><td>sturgeon_caviar </td><td>1               </td></tr>
	<tr><td>durian          </td><td>0               </td></tr>
</tbody>
</table>



#### What are the 3 most popular ingredients?
Your Answer:
1.

2.

3.
Double-click __here__ for the solution.
<!-- The correct answer is:
// 1. Egg with 21,025 occurrences. 
// 2. Wheat with 20,781 occurrences. 
// 3. Butter with 20,719 occurrences.
-->

However, note that there is a problem with the above table. There are ~40,000 American recipes in our dataset, which means that the data is biased towards American ingredients.

**Therefore**, let's compute a more objective summary of the ingredients by looking at the ingredients per cuisine.

#### Let's create a *profile* for each cuisine.

In other words, let's try to find out what ingredients Chinese people typically use, and what is **Canadian** food for example.


```R
# create a dataframe of the counts of ingredients by cuisine, normalized by the number of 
# recipes pertaining to that cuisine
by_cuisine_norm <- aggregate(recipes, 
                        by = list(recipes$cuisine), 
                        FUN = function(x) round(sum(as.integer(x) == 2)/
                                                length(as.integer(x)),4))
# remove the unnecessary column "cuisine"
by_cuisine_norm <- by_cuisine_norm[,-2]

# rename the first column into "cuisine"
names(by_cuisine_norm)[1] <- "cuisine"
                            
head(by_cuisine_norm)
```


<table>
<thead><tr><th scope=col>cuisine</th><th scope=col>almond</th><th scope=col>angelica</th><th scope=col>anise</th><th scope=col>anise_seed</th><th scope=col>apple</th><th scope=col>apple_brandy</th><th scope=col>apricot</th><th scope=col>armagnac</th><th scope=col>artemisia</th><th scope=col>⋯</th><th scope=col>whiskey</th><th scope=col>white_bread</th><th scope=col>white_wine</th><th scope=col>whole_grain_wheat_flour</th><th scope=col>wine</th><th scope=col>wood</th><th scope=col>yam</th><th scope=col>yeast</th><th scope=col>yogurt</th><th scope=col>zucchini</th></tr></thead>
<tbody>
	<tr><td>african     </td><td>0.1565      </td><td>0           </td><td>0.0000      </td><td>0.0000      </td><td>0.0348      </td><td>0e+00       </td><td>0.0696      </td><td>0e+00       </td><td>0           </td><td>⋯           </td><td>0.0000      </td><td>0.0087      </td><td>0.0435      </td><td>0.0087      </td><td>0.0174      </td><td>0e+00       </td><td>0.0087      </td><td>0.0174      </td><td>0.0000      </td><td>0.0348      </td></tr>
	<tr><td>american    </td><td>0.0406      </td><td>0           </td><td>0.0030      </td><td>0.0006      </td><td>0.0521      </td><td>6e-04       </td><td>0.0113      </td><td>1e-04       </td><td>0           </td><td>⋯           </td><td>0.0030      </td><td>0.0069      </td><td>0.0308      </td><td>0.0148      </td><td>0.0110      </td><td>7e-04       </td><td>0.0014      </td><td>0.0682      </td><td>0.0169      </td><td>0.0186      </td></tr>
	<tr><td>asian       </td><td>0.0075      </td><td>0           </td><td>0.0008      </td><td>0.0025      </td><td>0.0126      </td><td>0e+00       </td><td>0.0050      </td><td>0e+00       </td><td>0           </td><td>⋯           </td><td>0.0008      </td><td>0.0017      </td><td>0.0386      </td><td>0.0017      </td><td>0.1249      </td><td>0e+00       </td><td>0.0017      </td><td>0.0042      </td><td>0.0109      </td><td>0.0117      </td></tr>
	<tr><td>cajun_creole</td><td>0.0000      </td><td>0           </td><td>0.0000      </td><td>0.0000      </td><td>0.0068      </td><td>0e+00       </td><td>0.0000      </td><td>0e+00       </td><td>0           </td><td>⋯           </td><td>0.0000      </td><td>0.0068      </td><td>0.0822      </td><td>0.0000      </td><td>0.1918      </td><td>0e+00       </td><td>0.0068      </td><td>0.0342      </td><td>0.0068      </td><td>0.0000      </td></tr>
	<tr><td>canadian    </td><td>0.0362      </td><td>0           </td><td>0.0000      </td><td>0.0000      </td><td>0.0362      </td><td>0e+00       </td><td>0.0026      </td><td>0e+00       </td><td>0           </td><td>⋯           </td><td>0.0026      </td><td>0.0039      </td><td>0.0297      </td><td>0.0207      </td><td>0.0039      </td><td>0e+00       </td><td>0.0013      </td><td>0.0672      </td><td>0.0194      </td><td>0.0116      </td></tr>
	<tr><td>caribbean   </td><td>0.0164      </td><td>0           </td><td>0.0109      </td><td>0.0000      </td><td>0.0109      </td><td>0e+00       </td><td>0.0000      </td><td>0e+00       </td><td>0           </td><td>⋯           </td><td>0.0000      </td><td>0.0000      </td><td>0.0601      </td><td>0.0055      </td><td>0.0000      </td><td>0e+00       </td><td>0.0000      </td><td>0.0273      </td><td>0.0109      </td><td>0.0164      </td></tr>
</tbody>
</table>



As shown above, we have just created a dataframe where each row is a cuisine and each column (except for the first column) is an ingredient, and the row values represent the percentage of each ingredient in the corresponding cuisine.

**For example**:

* *almond* is present across 15.65% of all of the **African** recipes.
* *butter* is present across 38.11% of all of the **Canadian** recipes.

Let's print out the profile for each cuisine by displaying the top four ingredients in each cuisine.


```R
for(nation in by_cuisine_norm$cuisine){
    x <- sort(by_cuisine_norm[by_cuisine_norm$cuisine == nation,][-1], decreasing = TRUE)
    cat(c(toupper(nation)))
    cat("\n")
    cat(paste0(names(x)[1:4], " (", round(x[1:4]*100,0), "%) "))
    cat("\n")
    cat("\n")
}
```

    AFRICAN
    onion (53%)  olive_oil (52%)  garlic (50%)  cumin (43%) 
    
    AMERICAN
    butter (41%)  egg (41%)  wheat (40%)  onion (29%) 
    
    ASIAN
    soy_sauce (50%)  ginger (49%)  garlic (48%)  rice (41%) 
    
    CAJUN_CREOLE
    onion (70%)  cayenne (56%)  garlic (49%)  butter (36%) 
    
    CANADIAN
    wheat (40%)  butter (38%)  egg (35%)  onion (34%) 
    
    CARIBBEAN
    onion (51%)  garlic (51%)  black_pepper (31%)  vegetable_oil (31%) 
    
    CENTRAL_SOUTHAMERICAN
    garlic (57%)  onion (54%)  cayenne (52%)  tomato (41%) 
    
    CHINESE
    soy_sauce (69%)  ginger (53%)  garlic (53%)  scallion (48%) 
    
    EAST_ASIAN
    garlic (55%)  soy_sauce (50%)  scallion (50%)  cayenne (48%) 
    
    EASTERN-EUROPE
    wheat (53%)  egg (52%)  butter (48%)  onion (45%) 
    
    EASTERNEUROPEAN_RUSSIAN
    butter (60%)  egg (51%)  wheat (49%)  onion (38%) 
    
    ENGLISH_SCOTTISH
    butter (67%)  wheat (62%)  egg (53%)  cream (41%) 
    
    FRENCH
    butter (50%)  egg (44%)  wheat (37%)  olive_oil (28%) 
    
    GERMAN
    wheat (65%)  egg (61%)  butter (47%)  onion (35%) 
    
    GREEK
    olive_oil (76%)  garlic (44%)  onion (36%)  lemon_juice (34%) 
    
    INDIAN
    cumin (60%)  turmeric (51%)  onion (50%)  coriander (48%) 
    
    ITALIAN
    olive_oil (61%)  garlic (53%)  tomato (39%)  onion (33%) 
    
    JAPANESE
    soy_sauce (57%)  rice (44%)  vinegar (37%)  vegetable_oil (35%) 
    
    JEWISH
    egg (59%)  wheat (49%)  butter (31%)  onion (30%) 
    
    KOREAN
    garlic (59%)  scallion (52%)  cayenne (52%)  soy_sauce (49%) 
    
    MEDITERRANEAN
    olive_oil (80%)  garlic (51%)  onion (39%)  tomato (35%) 
    
    MEXICAN
    cayenne (74%)  onion (68%)  garlic (62%)  tomato (59%) 
    
    MIDDLEEASTERN
    olive_oil (60%)  garlic (47%)  wheat (38%)  lemon_juice (36%) 
    
    MOROCCAN
    olive_oil (73%)  cumin (55%)  onion (50%)  garlic (46%) 
    
    NORTH-AFRICAN
    onion (55%)  olive_oil (50%)  cumin (48%)  garlic (47%) 
    
    SCANDINAVIAN
    butter (64%)  wheat (58%)  egg (53%)  cream (29%) 
    
    SOUTH-AMERICA
    onion (43%)  garlic (37%)  egg (35%)  milk (31%) 
    
    SOUTHERN_SOULFOOD
    butter (58%)  wheat (49%)  egg (42%)  corn (30%) 
    
    SOUTHWESTERN
    cayenne (81%)  garlic (62%)  onion (61%)  cilantro (52%) 
    
    SPANISH_PORTUGUESE
    olive_oil (58%)  garlic (54%)  onion (47%)  bell_pepper (35%) 
    
    THAI
    garlic (60%)  fish (53%)  cayenne (47%)  cilantro (42%) 
    
    UK-AND-IRISH
    butter (60%)  wheat (58%)  egg (48%)  milk (33%) 
    
    VIETNAMESE
    fish (74%)  garlic (73%)  rice (49%)  cayenne (43%) 
    
    WESTERN
    egg (51%)  wheat (46%)  butter (46%)  black_pepper (36%) 
    


At this point, we feel that we have understood the data well and the data is ready and is in the right format for modeling!

-----------

### Thank you for completing this lab!

This notebook was created by [Polong Lin](https://ca.linkedin.com/in/polonglin) and revised by [Alex Aklson](https://www.linkedin.com/in/aklson/). We hope you found this lab session interesting. Feel free to contact us if you have any questions!

This notebook is part of the free course on **Cognitive Class** called *Data Science Methodology*. If you accessed this notebook outside the course, you can take this free self-paced course, online by clicking [here](http://cocl.us/DS0103EN_LAB3_R).

<hr>
Copyright &copy; 2018 [Cognitive Class](https://cognitiveclass.ai/?utm_source=bducopyrightlink&utm_medium=dswb&utm_campaign=bdu). This notebook and its source code are released under the terms of the [MIT License](https://bigdatauniversity.com/mit-license/).
