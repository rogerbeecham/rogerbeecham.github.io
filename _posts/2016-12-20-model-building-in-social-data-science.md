---
layout: default
title: "Towards explanatory model building in Social Data Science"
published: true
---

## Towards explanatory model building in social data science

## An underwhelming social data science

Whilst the opportunity for social science research of new, passively collected data has generated [plenty of excitement](https://www.wired.com/2008/06/pb-theory/), several commentators (e.g. [King 2011](http://science.sciencemag.org/content/331/6018/719)) have been lukewarm about the contributions to scientific knowledge. A common criticism is that social behaviours identified through new, data-driven studies are seldom generalised beyond the idiosyncratic populations they represent and only offer descriptions, not explanations or new understanding, into social processes.

It's easy to speculate about the reasons for this, and again many of the challenges have  been outlined in detail [elsewhere](http://link.springer.com/article/10.1007/s10708-014-9602-6). [Porway's](https://hbr.org/2013/03/you-cant-just-hack-your-way-to) view is that a paucity of compelling 'science' might be due to a relative lack of subject-matter-experts participating in this work: any serious scientific endeavour should "_start with a question, NOT the data_" (Porway 2013) -- or perhaps that trendy technique the data scientist is desperate to expose to the world. At the same time, when you're repurposing a dataset rather than creating one in advance, the traditional _modus operandi_ for doing science -- specify hypotheses, generate dataset, exploratory analysis (not too much as it's easy to slip into a [circular analysis](http://www.nature.com/news/scientific-method-statistical-errors-1.14700)), confirmatory analysis and findings  -- feels like a recipe manqu&eacute;.


### _Data:theory-driven_ model building in social data science
So. Where am I going with this? I think I'm arguing, rather predictably, for a compromise, which remembers some important tenets of the scientific method -- posing questions, generating hypotheses and coming up with scientific claims with quantified levels of uncertainty. But one that can cope with the fact that many of the questions will be data-driven, as well as informed by theory, and most likely not specified in advance. That recognises it might be necessary to supplement _new_, population-level datasets, which are typically very sparse, with context from auxiliary data and/or derived through clever analytical innovations. That is alert to the fact that repurposing datasets means certain concepts will gain new levels of importance, the most obvious being _measurement validity_: does the dataset that is being repurposed record the behaviours that you think it does (or want it to)? And that also realises some creativity in addressing simple statistical issues is necessary when working with very large data.

### A real example: my PhD thesis (but also some new analysis)
I'd argue this was something attempted in my [PhD thesis](http://www.gicentre.net/rogerbeecham/thesis). Here I (and [Jo Wood](http://www.gicentre.net/jwo/index)) analysed individual-level journey data from the London Cycle Hire Scheme: a population-level dataset consisting at the time of c.20 million journeys made by c.200,000 people. The thesis demonstrated that analysis of these data can provide useful and new contributions to literature in Transport Studies on urban cycling -- there were important observations made around [gender and urban cycling](http://www.tandfonline.com/doi/abs/10.1080/03081060.2013.844903) and new insights into [group cycling](http://www.sciencedirect.com/science/article/pii/S0968090X14000734), a behaviour that would be very difficult to investigate in more traditionally-collected datasets. _Explaining_ these observed behaviours formally, with quantified measures of effect and uncertainty, was more challenging. Toward the end of the project we made [an attempt](http://openaccess.city.ac.uk/13003/). Whilst an interesting piece of work, this seemed to result in more questions than it answered -- not a bad outcome for a data analysis, but certainly a bit of scope creep from the paper's title.

After not touching this for two years, we very recently returned to the bikeshare data and the problem of formally explaining observed behaviour. I want to quickly sketch out our approach because I think it is at least cognisant of the challenges outlined above and also by [Goodchild and Miller](http://link.springer.com/article/10.1007/s10708-014-9602-6) (2015) when considering a new _data-driven geography_ (a worthwhile read by the way!). In order to make the case for _data:theory-driven_ model building more persuasive,  I'll also try here to provide some quick analytic context -- or provenance -- for the variables that inform our model: both the outcome we wish to explain and the variables with which we hope to explain it.

### An explanatory model for observed spatial cycling behaviours with quantified measures of effect

#### Outcome variable: spatial travel behaviours of men and women
<figure> <img alt="gender bikeshare" src="{{ site.url }}/img/posts/bikeshare_gender.jpg" id="gender_bikeshare" ><figcaption>Relative proportions of male/female London bikeshare cycling by origin-destination pair.</figcaption></figure>

I mentioned that early in our analysis we identified gendered patterns of cycling in the bikeshare scheme that were compelling. We observed  differences in how men and women seem to use the scheme -- the types of journeys they make, the frequency with which they make them. But these  differences were most obviously manifest in the _spatial_ travel behaviours of cyclists (as above). However we cut the data, these very different <em>spatial</em> patterns of travel between men and women seemed to persist.

Although slightly redefined given the constraints of our dataset, the outcome that we wish to explain is thus the observed spatial patterns of bikeshare cycling for men and women.

#### Explanatory variable #1: where cyclists live

When first discovering these spatial differences, we thought a little about why they  might exist -- both given existing literature on gender and urban cycling, but also factors that are particular to the bikeshare scheme. A really substantial usage function is of commuting -- and peculiar to the bikeshare scheme, commuting to solve the 'last mile problem'. This is where cyclists use the scheme to complete the final leg of a journey from major train station to workplace. Clearly to arrive at a major rail terminal you need to be travelling in a reasonable distance from outside central London. We compared the home locations of men and women and found that they were different, with women bikeshare users really underrepresented amongst those living in locations likely to require travel via commuter rail. The spatial differences we observe might, then, be explained by  differences in origin rather than any essential differences between men's and women's attitudes, perceptions or approaches to cycling.

So, an important explanatory variable to be considered in our model (also investigated in the original work) is _where cyclists live_. Fortunately we have access to this information -- the full home postcodes of users -- via information provided by bikeshare customers when registering with the scheme.

#### Explanatory variable #2: where cyclists work (and the geography of opportunity)

Realising that spatial differences in travel behaviour are partly a function of where people live, we made the obvious assertion that they will also be determined by where people wish or need to travel to access work and other facilities. The bikeshare usage data do not provide _a priori_ detail on the workplaces of users, so we [later](http://www.sciencedirect.com/science/article/pii/S0198971513001014) tried to estimate locations for bikeshare cyclists’ workplaces from observed usage behaviours. Assuming our method for estimating workplaces was valid, we again observed gendered differences in the geography of men’s and and women’s workplaces, which weren’t surprising given the cycling behaviours we’d already observed, but seemed to relate to the geography of men’s and women’s _real_ employment in London: not all locations in London are filled equally with male and female workers.

A second explanatory variable is, then, the geography of (employment) opportunities available to men and women in London. This information is provided by the 2011 Census travel-to-work data.

#### Explanatory variable #3: cycling infrastructure (bikeshare)

A more prosaic observation, but nevertheless one that is supported by the data: bikeshare cycling behaviours can only exist within the constrains of the bikeshare infrastructure. So the provision of docking points and bikes given the likely competition for those spaces is an important consideration. We can model this reasonably well via the usage data and additional context from the 2011 Census.

#### Explanatory variable #4: cycling infrastructure (general)

Finally, the provision of cycle infrastructure or ‘agreeableness’ of possible routes between bikeshare stations may, to an extent, explain observed spatial cycle behaviours. Modelling for this infrastructure needs a little more thought than I have given it. Previously we extracted estimated routes for every cycled journey in the bikeshare dataset using the [cyclestreets](https://www.cyclestreets.net) algorithm. As well as extracting coordinates representing the routes, we stored meta-data describing the _nature_ of routes. As an initial attempt, we use [route quietness](https://www.cyclestreets.net/journey/help/howitworks/#quietness), a single score based on a subjective classification, as our measure of general cycle infrastructure<sup>*</sup>.

<p style=font-size:0.7em>*Unfortunately, <em>quietness</em> doesn't necessarily capture what we want -- shared use facilities, not always suitable for cycling, are rewarded with a very high quietness score -- and this is reflected in our analysis results.</p>

#### Model specification (and redefined outcome)

The way in which we specify our model is constrained by the way in which we are able to approximate these outcome / explanatory variables. We first need to slightly redefine the outcome. We take estimates of bikeshare workplaces -- essentially job counts made possible through the bikeshare scheme -- as a ground-truth, and try to _explain the geography of 'bikeshare jobs'_ separately for men and women. We do so using the variables/concepts suggested above: the jobs available at locations covered by the bikeshare scheme (control #2) and accessed from the same home locations (resident population) as bikeshare users (control #1); the provision of bikeshare cycling infrastructure (control #3); and the provision of more general cycling infrastructure (control #4). We then compare the observed geography of bikeshare jobs to an expected geography derived from these assumptions. Gradually weighting our assumptions dataset by the explanatory variables listed above, and paying attention to how model fit improves with each of these additions, we hope to make quantified claims about the importance of certain explanatory variables.</p>

The lowest level at which could easily get access to Census travel-to-work data was [Lower Super Output Area](http://webarchive.nationalarchives.gov.uk/20160105160709/http://www.ons.gov.uk/ons/guide-method/geography/beginner-s-guide/census/super-output-areas--soas-/index.html) (LSOA). So we aggregate our estimates of bikeshare jobs, the ground-truth, to the LSOA level to come up with observed counts for bikeshare jobs at each LSOA. Our model aims to predict these counts using the explanatory variables outlined above:
<p><pre>
<strong>total jobs at lsoa_i </strong>=
<strong>&emsp;Census jobs at lsoa_i </strong>
&emsp;[travel-to-work flows | lsoa_i...n bikeshare homeplaces, 2011 Census]
<strong>&emsp;+ bikeshare infrastructure at lsoa_i</strong>
&emsp;[density of  docking spaces | competition, Census 2011 and LCHS]
<strong>&emsp;+ provision of 'cycle-friendly' routes to lsoa_i</strong>
&emsp;[quietness scores summarised over lsoa_i, cyclestreets.net]
</pre></p>

In order to control for origin (the home locations of bikeshare users), we weight the origins in the Census 2011 travel-to-work data in the same proportions of bikeshare commuting cyclists. Thus, in the unlikely case that a single LSOA in rural North Yorkshire supplies 20% of bikeshare commuters, we would ensure that flows originating from that LSOA represent 20% of all flows in the  Census travel-to-work data. Our expected counts therefore describe where in London, and in what quantity, we would expect residents living in the same locations as bikeshare cyclists to be working. This assumptions dataset is then further weighted according to the remaining explanatory variables: bikeshare infrastructure and general cycling infrastructure.

### Early views on the model output

We wish to explore how well our assumptions dataset fits the observed geography of bikesare workplaces. We also want to know _where_ (in which LSOAs) the assumptions data performs  well and not so well, and also _by how much_. We can do this using standardised residuals from the Chi-statistic. Here our observed value is the number of bikeshare jobs in an LSOA and the expected value is derived from a contingency table that assumes independence between the two count distributions for our observed and assumptions dataset:

<p><pre>
std.residual[lsoa_i] = (obs[lsoa_i] - exp[lsoa_i]) / sqrt(exp[lsoa_i])
</pre></p>

<p>If we want an estimate of effect size for these differences across all of London, we can use Cramer’s V. This is simply the square root of the sum of residuals (squared to remove the sign) divided by sample size (in this instance):</p>

<p><pre>
Cramer's V = sqrt(sum(residual_i...n)) / N
</pre></p>

#### Within-scheme comparison

Just to demonstrate that the geography of men's and women's workplaces is indeed different, let's first create a map of residuals calculated in the same way as above but comparing the LSOA-level counts of  men's versus women's workplaces _within_ the bikeshare scheme. The darker the blue, the more men’s bikeshare workplaces than would be expected given the geography of women’s. The corollary is true where there's more red.

This view isn’t that surprising given what we'd observed previously: there are relatively more jobs filled by bikeshare men in City of London-type LSOAs; relatively more filled by bikeshare women in West London LSOAs; some around the  Vauxhall and  Bloomsbury areas. Notice the power-law distribution in the legend: a small number of LSOAs account for many of the jobs. This power-law is to be expected, but probably made more extreme by the fact that LSOA boundaries are a residential geography -- they are roughly equal in residential population size, not workplace population size. [Workplace Zones](http://webarchive.nationalarchives.gov.uk/20160105160709/http://www.ons.gov.uk/ons/guide-method/geography/beginner-s-guide/census/workplace-zones--wzs-/index.html) would be a more appropriate geography; however the full OD travel-to-work data by gender is proving somewhat elusive (advice here appreciated).

<figure> <img alt="residuals bikeshare" src="{{ site.url }}/img/posts/residuals_gender.png" id="residuals_bikeshare" ><figcaption>Comparison of observed bikeshare jobs (relative counts, men vs women)</figcaption></figure>

#### Between-scheme and assumptions comparison

Of course we're most interested in seeing <em>where</em> the distribution of bikeshare workplaces is different to what would be expected given the controls/assumptions I mentioned earlier.

Below are two sets of maps corresponding to two assumptions data and coloured according to standardised residuals. The more green, the more bikeshare jobs filled in those LSOAs than would be expected given the assumptions data; the more purple, the fewer than would be expected. To allow comparisons between the expected counts generated from the different assumptions data, a global diverging colour scale is used. Additionally, since the residuals vary partly as a function of sample size, the data have been scale-weighted; this allows comparison between the models for men and women.

First, we use as our assumptions data Census counts for jobs filled in each LSOA, weighted by the home locations of bikeshare commuters. Now we get a different view of the data: that despite the real dominance of the City in the bikeshare dataset, we actually find fewer than expected bikeshare men in the City, and also Westminster/Whitehall area, given the jobs available there and relatively more jobs filled in peripheral locations. This is the same for bikeshare women.

<figure> <img alt="residuals map 1" src="{{ site.url }}/img/posts/residuals_map_1.png" id="residuals_map_1" ><figcaption>Comparison of observed bikeshare jobs with assumptions data (Census jobs given home locations of bikeshare commuters)</figcaption></figure>

This feels like it could be a capacity-limit problem – that there’s so many jobs in LSOAs in the City and other areas that competition for bikes is more likely to limit the number of ‘bikeshare jobs’ that can exist. So we add a bikeshare-infrastructure assumption (or weight) to our expected counts. Notice now that  colour lightness increases -- suggesting there’s less variation between the observed workplaces and our assumptions dataset (the residuals tend more towards zero). This is confirmed by the Cramer’s V (effect size), which was small in any case, but has reduced further. Notice also that the sign on the residuals has reversed in the City -- we now observe a greater number of bikeshare jobs than would be expected when we control for the number of jobs available in those areas and the provision of bikeshare cycling facilities.

<figure> <img alt="residuals map 2" src="{{ site.url }}/img/posts/residuals_map_2.png" id="residuals_map_2" ><figcaption>Comparison of observed bikeshare jobs with assumptions data (Census jobs given home locations of bikeshare commuters+ bikeshare infrastructure )</figcaption></figure>

At this point it would be great to add a cycle infrastructure weight that allows us to further improve model fit (even smaller residuals) and identify LSOA-level changes that can be convincingly explained given their spatial context. This unfortunately did not happen and exploratory analysis of our aggregated 'quietness' scores suggests we might need to think more carefully about the way this concept/variable is modelled.

#### Regression model

One of the main ambitions was to end up with explanations for the geography of observed bikeshare workplaces with _quantified measures of effect_. As well as the visual analysis presented above, we fit log-log models to our bikeshare and assumptions data separately for men and women. Studying how model fit (R&#94;2, prediction intervals) and regression coefficients vary both between men and women, and as we add more assumptions, is instructive and some summary charts are below.

<figure> <img alt="regression output" src="{{ site.url }}/img/posts/regression_output.png" id="regression_output" ><figcaption>Example regression output. Bands around regression line represent prediction intervals</figcaption></figure>




### Isn't this (model building with repurposed data) all just secondary data analysis?

If you managed to get through the discussion and analysis above, well done. I tried to keep it brief whilst hopefully exposing an analysis process that, in my view, is sensitive to the high-level discussion at the start of the post. However, you may also be thinking that this category of work and approach is simply [secondary data analysis](http://sociology.about.com/od/Research-Methods/a/Secondary-Data-Analysis.htm): the nod to Data Science is an unnecessary embellishment.

Maybe. But I think secondary data analysis in social research has traditionally involved repurposing quite familiar  centrally-administered census or survey data. There is something different about the contemporary class of publicly available datasets: those like bikeshare or smartcard that continuously describe usage of a city-wide transport system, or the arguably more problematic data made available via social media. In my mind these data bring a new analytic _milieu_ that requires us as analysts to reconfigure and be alert to a different set of priorities and incentives. This is something I briefly provided a position on in the [methods]({{ site.url }}/papers/thesis_methods.pdf) section of my thesis. This has been a long post -- so more on this (plus more data analysis) to follow.
