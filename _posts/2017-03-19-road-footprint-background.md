---
title: "UK road surface area: Part 1"
date: "2017-02-27"
tags:
  - transport
bibliography: /Users/markruddy/Documents/Research/Data/Bibliography/bibliodb.bib
---

This post is the first in a series that will look at the amount of land space the UK has handed over to motor vehicles. I'm not a transport professional but one of the things that interests me is the urban environment and how we travel around it. I also like doing data science and needed a project to flex my muscles after a few months away from coding. 

I'll go into some background and get hold of some raw data. Later posts will contain more meat and bones data analysis.

## Roads and the places we live

I use whatever type of transport seems best - car, bus, train, hovercraft (sadly not hovercraft) - depending on what I have to do and how far I have to go. But I mainly ride a bike and walk because they tend to be the most convenient and attractive modes. It's pretty evident that building roads for motor vehicles - not pedestrians or bicycles - is central to how our world has developed [^1]. The benefits to economies and quality of life this brings are set against an escalating series of problems: local air pollution, CO2 emissions, sedentary lifestyle issues, and road traffic mortality. There's a need for an urgent, fundamental shift away from decades of road-centred policy choices that have shaped the places we live in. Unfortunatley, legacy issues of [car dependency](https://en.wikipedia.org/wiki/Automobile_dependency) are hard to overcome and there is generally strong [local opposition](http://www.cs11.london/) to all but the weakest attempts to take road space from motor vehicles and give it to pedestrians and bicycle users.

One aspect of how road design impacts people is the amount of space given over to motor vehicles, especially in places where people live. The design of our public space influences so much about society - culture, economy, well-being - and road infrastructure is the portion of public space that [frames everything else](https://www.theguardian.com/books/2011/oct/14/jane-jacobs-death-and-life-rereading) (Jacobs, 1961). In fact, increasing numbers of cars mean that not only road space but duplicated [parking space](https://aseasyasridingabike.wordpress.com/2012/09/04/the-effect-of-private-car-dependence-on-land-use/) is also needed, seizing even more land.

Electric or hydrogen-powered vehicles may provide a solution to pollution and transport sector CO2 emissions, but the other [externalities](https://en.wikipedia.org/wiki/Externalities_of_automobiles) associated with motorised transport remain. Electric cars are just as capable of killing and seriously injuring people or dividing neighbourhoods - see this lovely graphic in Figure 1 by Appleyard et al. (1981) - as petrol-powered ones.

<figure class="align-centre">
  <a href="/assets/images/general/appleyard-1981-fig3.png"><img src="/assets/images/general/appleyard-1981-fig3.png" alt="Intra-street social connections with differing traffic volumes. (Appleyard et al., 1981)"></a>
  <figcaption>Figure 1. Intra-street social connections with differing traffic volumes (Appleyard et al., 1981)</figcaption>
</figure>


## What is the surface area of the UK road network?

It was a conversation with my 6 year-old daughter that got me to thinking about exactly how much of the surface area of the places we live in is occupied by roads. I have a little time on my hands at the moment so decided to try and work it out. Here's two broad aims for what I want to achieve:

1. How much surface area is taken up by the UK road network?
2. How does this vary spatially at different scales?

## Data

Some googling uncovered a few datasets that might be useful. Ideally we'd want to use actual measurements of both road length and width. This is available from the [Ordnance Survey (OS)](https://www.ordnancesurvey.co.uk/), but the OS's [MasterMap](https://www.ordnancesurvey.co.uk/business-and-government/products/os-mastermap-highways-network-routing-asset-management-information.html) product costs £££s. There are no alternative open access datasets with length and widths (that I can find) so we'll have to take another approach.

### Road length datasets

Having no readily available road length with measured width data, the alternative is to use road length data with assumed widths dependant on the type of road (motorway, dual carriageway, single carriageway, etc.). A number of options exist for obtaining purely road length data.

*Office for National Statistics*    

The 'official' source of information on this for the UK is the [Office for National Statistics (ONS)](https://www.gov.uk/government/statistical-data-sets/rdl02-road-lengths-kms). Figures on road length are presented for all road types, split by Local Authority, from 2005 to 2015. Local Authority areas are fairly large and inconsistently sized, so comparing between them is far from ideal, and there's no opportunity to drill down into finer grained geographic detail. A supplement also lists road lengths, with various gaps, dating back to 1914. All are available under the Open Government Licence v3.0 ([OGL](http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)). 

*Ordnance Survey*    

The OS [Open Roads](https://www.ordnancesurvey.co.uk/business-and-government/products/os-open-roads.html) product is a spatial vector point and line dataset covering the whole of the UK, with roads coded by [class](https://www.ordnancesurvey.co.uk/docs/user-guides/os-open-roads-user-guide.pdf). Like the ONS data this is made available under OGL, but with a required attribution to the OS. Open Roads contains all roads excluding ['private roads and shorter cul-de-sacs'](https://www.ordnancesurvey.co.uk/business-and-government/products/os-open-roads.html), which should be a negibible omission in the context of what we want to achieve. This spatial dataset could be analysed on whatever level of geographic detail required - in contrast with the ONS data. 

*OpenStreeMap*    

[OpenStreetMap](https://www.openstreetmap.org) (OSM) is a digital map built through [volunteered geographic information](https://en.wikipedia.org/wiki/Volunteered_geographic_information) (VGI), freely available under the [Open Database Licence](http://wiki.osmfoundation.org/wiki/Licence). Roads are represented spatially as lines with a width attribute [sometimes](http://stackoverflow.com/a/25330995/2802810) - not always - present. The quality and coverage of OSM is often very good (Haklay, 2010) but the risks of gaps in coverage make it unsuitable as a main dataset for our task. 

### Approach

The ONS and OS Open Roads datasets look to be useful. The ONS estimate includes OS data and additionally draws on information from Local Authorities, the Scottish and Welsh governments, and the Highways Agency. Although with ONS there's no opportunity to do more detailed geographic analysis. 

Both datasets require assumptions on the widths of different road types, which we'll look at in a later post. I have an initial thought that although the OSM include an optional width attribute, where width is present it might be useful for sense-checking (?).

As a first pass let's use the ONS data and have a go with OS Open Roads later. I'll be using R to import, tidy, and explore the data. That'll be the subject of the next post.


<div id="references" class="section level2">
<h2>References</h2>
<!-- rnb-text-end -->
<div id="refs" class="references">
<div id="ref-appleyard:1981aa">
<p>Appleyard, D., Gerson, S., and Lintell, M. 1981. <em>Livable streets, protected neighborhoods</em>. University of California Press.</p>
</div>
<div id="ref-haklay:2010aa">
<p>Haklay, M. 2010. “How good is volunteered geographical information? A comparative study of OpenStreetMap and Ordnance Survey datasets.” <em>Environment and Planning B: Planning and Design</em> 37 (4). SAGE Publications Sage UK: London, England: 682–703. doi:<a href="https://doi.org/10.1068/b35097">10.1068/b35097</a>.</p>
</div>
<div id="ref-jacobs:1961aa">
<p>Jacobs, J. 1961. <em>The Death and Life of Great American Cities</em>. Random House.</p>
</div>
<div id="ref-tidy-data">
<p>Wickham, H. 2014. “Tidy Data.” <em>The Journal of Statistical Software</em> 59 (10). doi:<a href="https://doi.org/10.18637/jss.v059.i10">10.18637/jss.v059.i10</a>.</p>
</div>
</div>
</div>

[^1]: [Although they were originally built for bicycles](http://www.roadswerenotbuiltforcars.com/)

