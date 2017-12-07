Taiwan's society has been going through massive fundamental shifts during the past decade, and changes to its population structure is one of them. Here, we analyze Taiwan population data from 2004 to 2016 for interesting, noteworthy trends and phenomena.

The post below presents only the findings. My full analysis is available [here](roywangtw.github.io/files/2017-11-19-Changes-in-Taiwan-Population-Visualized.Rmd).

## Data exploration and visualization

![center](http://roywangtw.github.io/images/2017-11-19-male-female-births.png)

Two interesting things pop out from the plot above:

1. ***Taiwan as a country has slightly more male births than female births***: As statistically perplexing as it might sound, this, in fact, aligns with the global sex ratio at birth of 107 male births per 100 female births, as reported by the [World Bank](https://data.worldbank.org/indicator/SP.POP.BRTH.MF?view=chart). Virtually no points on the plot sits significantly above the black 45-degree gender parity line, which testifies to the robustness of such sex disparity phenomenon across Taiwan.

2. ***The larger the number of births in a certain administrative region, the bigger the gap between the numbers of male and female births***: New Taipei City has consistently by far the highest numbers of births, regardless of gender. However, *the disparity between the numbers of male and female births there is the largest as well*, as evidenced by the wider gaps between the city's dark blue points and the black 45-degree gender parity line. In contrast, the regions with the lowest numbers of births (e.g. Lienchaing County, Kinmen County, Penghu County) are surprisingly more gender balanced. In fact, other more metropolitan areas like Taipei City and Taichung City also exhibit such bias towards male births. This probably goes directly against what many people would have guessed without looking at the data; one would assume the populous urban areas, with a relatively higher average of education level and better access to advanced medical treatments, are more likely to have less gender imbalance in child births, while the more rural places would show a stronger inclination towards male newborns. Instead, here we observe the opposite.

![center](http://roywangtw.github.io/images/2017-11-19-male-female-deaths.png)

The numbers of male deaths versus female deaths paint an even more intriguing picture. 

1. ***Taiwan as a country has witnessed a much higher death count for men than women***: All the points on the plot are beneath the 45-degree parity line

2. ***The gender differences in death counts are much more prononunced in the most populous regions***: Apparently, in New Taipei City, Kaohsiung City (SM), and Taichung City (SM), 3 of the most highly populated administrative regions (as indicated by the larger sizes of their points), men on average have been dying at a glaringly higher number than women.

![center](http://roywangtw.github.io/images/2017-11-19-numbers-marriages-births.png)

When we plot the numbers of total births against those of marriages, the basic math behind Taiwan's dwindling birth rates and population growth becomes very clear. 

Over half of the points on the plot, especially those representing the largest numbers of births, fall below the grey dash line with a slope of 1.5. That means an overwhelming portion of marriages, on average, don't produce more than 1.5 children, quite possibly because more and more couples are either delaying childbearing plans or abandoning the idea altogether. To a typical 2-parent marriage, that replacement level fertility is below that at which a population exactly replaces itself from one generation to the next, not to mention the equally worrisome slide in marriage rate.

As is the case with many other developed countries nowadays, Taiwan's ongoing demographic crisis shows no sign of abating, and the fact that no point on the plot is above the steeper black line with a slope of 2 speaks volumes. In other words, virtually no administrative region across Taiwan has achieved a meaningfully large replacement level fertility to help stem the tide of nationwide population decline.

![center](http://roywangtw.github.io/images/2017-11-19-natural-social-increases.png)

As seen in the plot above, the obvious pattern is that big cities like New Taipei City, Taichung City, Taipei City, and the emerging Taoyuan City have been steadily attracting more outside residents, all the while maintaining a comparatively health number of newborns. The rest of the country, however, has languished in prolonged population decline, with perennially low natural increases and often negative social increases.  

This seems to confirm with an overall irreversible trend of ongoing urbanization.

![center](http://roywangtw.github.io/images/2017-11-19-transnational-marriages.png)

![center](http://roywangtw.github.io/images/2017-11-19-transnational-divorces.png)

The 2 bar plots above show that transnational marriages saw a sharp decline from 2004 to 2006, but has been gradually edging back up in the past few years.

Interestingly and perhaps not coincidentally, the years during which the numbers of transnational marriages dropped to the lower point were also exactly the time when the numbers of transnational divorces soared to the top. 

The ebb and flow of transnational marriages and divorces nicely complement each other in our time frame.

![center](http://roywangtw.github.io/images/2017-11-19-transnational-marriages-divorces.png)

When plotting the numbers of transnational marriages and divorces against each other, what is interesting is that the least populous regions see the their marriage-divorce ratio closest to 1:1, as their points cluster around the black, 45-degree parity line whereas the big metropolitan areas' points steer much further away from the 1:1 ratio. 

In other words, when it comes to transnational relationships in the more rural regions, there tends to be nearly as many marriages as divorces going around.

![center](http://roywangtw.github.io/images/2017-11-19-births-moms.png)

The plot above shows births given by non-Taiwanese mothers remain still more prevalent in the less populated regions whose points stick closer to the black line with a slope of 0.25 (i.e. a 1:4 ratio between births by non-Taiwanese mothers and Taiwanese mothers). In contrast, most of the points for the more populated regions don't even touch the less steep grey line with a slope of 0.15 (i.e. a roughly 1:6.7 ratio between births by non-Taiwanese mothers and Taiwanese mothers). 

In other words, whereas those less populated regions naturally have lower numbers of newborns in absolute terms, their newborns are more likely to be given by non-Taiwanese mothers *in percentage terms* compared with the highly populated urban regions where Taiwanese mothers still account for the vast majority of births.  

In light of what we just noticed in the previous plot, the implication is worth pondering; transnational marriages seem less stable and enduring in the less populated, rural areas, but their births stand for a higher percentage of all local newborns than their counterparts in metropolitan regions. Besides seemingly contradictory, this phenomenon perhaps underscores a larger degree of tension and strain in transnational relationships within the more rural regions as well.

## Conclusions

This analysis only presents a cursory look into some of the intriguing trends and changes of Taiwan population throughout more than the past decade. Further investigation may well uncover more insights on detailed demographic shifts and social changes. 

In addition, a host of many other types of public Taiwan data are freely available [here](http://sowf.moi.gov.tw/stat/month/list.htm) at the website of the Ministry of the Interior, Taiwan. 

> Anyway, the most interesting tidbits of our findings are summarized as follows:

- Consistent with the global sex ratio, Taiwan's male births have consistently outnumbered female births, albeit only slightly. ***The degree of outnumbering is notably much more prominent in the most metropolitan and populous regions***.

- ...However, Taiwanese men as a whole have been dying in markedly greater numbers than their opposite sex, ***especially in the most populous metropolitan regions as well***.

- As nationwide birth rate continues to plummet to new lows, ***the most populous, urban regions are not at all helping with their particularly low replacement level fertility***.

- ...and the picture gets grimmer as more and more people are moving to the cities.

- ***The ebb and flow in the numbers of transnational marriages and divorces have been mutually complementary***. A rise in transnational newlyweds has coincided nicely with a drop in marital separations, and vice versa. 

- ...but ***those cross-national relationships seem more shaky and fragile in the less populated, rural regions***, which have seen their transnational marriage-divorce ratio persistently close to 1:1 throughout the years.

- ...Meanwhile, also in those same regions, newborns delivered to non-Taiwanese mothers, as opposed to Taiwanese mothers, are much more prevalent. ***Combined with a less stable marital state, the social implication might be profound and worth contemplation***.
