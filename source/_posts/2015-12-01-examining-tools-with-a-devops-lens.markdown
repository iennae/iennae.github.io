---
layout: post
title: "Examining Tools With a Devops Lens"
date: 2015-12-01 21:03:41 -0800
comments: true
categories: 
---

Please enjoy my [Sysadvent](http://sysadvent.blogspot.com/2015/12/day-2-examining-tools-with-devops-lens.html) offering for 2015.

Over the last few years I have had the opportunity to attend a variety of conferences, meeting people and hearing diverse stories about work environments and challenges. It is fascinating to hear the variety of explanations about devops and its ongoing impact on the industry and the workplace. As I worked to gain a better appreciation of others' experiences, I realized the challenge of misinformation about devops. How do we expect individuals to understand and choose devops when we have so many competing themes? 

Two big themes I have heard: 
* Devops is culture not tools.
* Devops is automation.

In this article, I will tackle one aspect of the challenge focusing on examining tools within the industry with a devops lens.

## Devops is culture not tools.

What is culture? Culture is the totality of **learned, socially transmitted customs**, **knowledge**, **objects**, and **behaviors**. It includes the ideas, values, customs, and artifacts of a group of people. Culture encompasses everything about how we live and work, and how life and work evolve to meet the challenges we have in our environments. It gives meaning to social, political, economic, aesthetic, religious norms, and modes of organization that distinguishes us from others.

> "We become what we behold, we shape our tools and then our tools shape us."
>
> Father John Culkin

What are tools? Tools are a vital component of our identity, how we interact with the world around us, how we use and conserve energy, and how we buffer ourselves from harm. Tools shape our thoughts and behaviors including our transparency, level of exertion over our environment, and conflict response. Tools are a cultural artifact.

Consider the introduction of automobiles and the changes to city landscapes that came about because of them; new cities have wider streets to accommodate vehicles with less care taken to provide pedestrians with safe walking. Automobiles impacted how we work and where we work. As [commute times](http://www.citylab.com/commute/2015/11/why-the-wealthy-have-been-returning-to-the-city-center/416397/) have increased in densely populated regions, the value of owning a car has decreased and the landscape will transform again.

<img src="http://www.jendavis.org/assets/public-domain-images-free-stock-photos-light-sky-silo-windows-lillyphotographer.jpg" width="300" alt="Concrete Light Sky Silo Windows Sunlight Rays" align="left"></a>

Prior to the introduction of devops, an organization might incentivize and reward teams based on each team's particular priorities; developers strove to build features quickly, operations stabilized systems, security minimized risk and controlled access, and so on across the organization. When the bonus for the VP of Operations is driven by uptime, system administrators will be incentivized to ensure stability and availability. When the bonus for the VP of Development is driven by meeting deadlines, developers will be incentivized to deliver features. This leads to a fundamental conflict in deciding highest priority between individuals trying to work together across organizational boundaries. 

Organizations have created islands of culture based on their existing individual and collective values. For example, the roles and responsibilities of an operations engineer at one organization may significantly differ at another. Consequentially, operations engineers at different companies often have substantially disparate skill sets. Over time, the roles and concerns within an organization change leading to fractured capabilities even within a single organization.

As organizations grow larger, each team's individual focus narrows further. Each team adopts a specific tool that meets their requirements, leading to multiple tools that overlap in purpose. This proliferation of tools both hinders transparency within the organization and stifles collaboration.

For example, bug tracking within development teams led to the development of tools like [JIRA](https://www.atlassian.com/software/jira/) and [bugzilla](https://www.bugzilla.org/). Ticket tracking within operations teams led to development of tools like [Request Tracker(RT)](https://www.bestpractical.com/rt/).  Bugs and tickets are both issues. While a single _issues tracking tool_ can be selected at the organizational level, the tool can impact the cognitive load of teams unequally as a team tries to adopt a tool that isn't specific to their domain.

The problem of tool proliferation continues today with the belief that a specific tool might solve all the problems an organization may have. When people say _Devops is culture not tools_, it is in part to focus on solving the organizational issues that can not be solved with a change in technology alone.

**What is Devops?**

Devops is an ideology that seeks to change how individuals **think about work**,  **value the diversity** of work done, **develop deliberate acceleration** of business value, and **measure the effect** of social and technical change.

In [Effective Devops](http://shop.oreilly.com/product/0636920039846.do), [Katherine Daniels](https://twitter.com/beerops) and I introduced the 5 pillars of devops: **Collaboration**, **Hiring**, **Affinity**, **Tools**, and **Scale**.

These 5 pillars form the foundation for effective devops and the **devops compact**, the **continuous building of a shared mutual understanding** within a team, organization, and across the industry.

With the devops compact, we commit to working together, communicate our intentions and any issues, and adjust our work in order to work towards shared organizational goals. We answer questions like: what is the value of what we are we trying to do, how are we going to do it, and what exactly are we doing? We don't just decide to do devops, and then we’re done. The nature of doing devops, means that we are commiting to adjusting to change.

**Devops is culture which includes tools and their use**. Tools are not devops. How tools are used, and the ease with which they can be used impacts the acceptance and proliferation of specific aspects of culture. When we talk about devops tools, we mean the tools and the manner of their use--not fundamental characteristics of the tools themselves.

**Devops tools stress "We" over "Me"**; they allow teams and organizations to build mutual understanding to get work done. Your choice of tools is a choice in a common language. Is this language one that benefits your organization as a whole or merely a subset of specific teams? At times, due to the lack of availability of an equally balanced tool, a choice must be made that has a higher cognitive cost to one team over another. Be aware of the cost and empathetic to the teams impacted.

The devops culture that we embrace is one of collaboration across teams, across organizations, and across industries. When developing solutions, I think about my team instead of thinking about the easiest thing for me to do now. This sometimes means adjusting my expectations for the good of the organization and choosing something a little more difficult than my current working structure. 

### Tool Examination

<a href="https://blackstock.co/collection/young-girl-tilting-camera-up/"><img src="http://www.jendavis.org/assets/girl_lens_camera.jpg" width="300" alt="Young Girl tilting camera up." align="left"></a>

Let's examine a few tools with the devops lens. First we'll look at version control systems and then infrastructure automation. Please note that this examination of tooling is not meant as a judgement or advocacy of a specific tool in your environment. Without understanding your organization's culture, noone can tell you the right tool to choose.

Version control systems record changes to a set of files over time. CollabNet founded the Subversion project in 2000 as an open source software versioning and revision control system that was architected to be compatible with the widely used Concurrent Versions System (CVS). Subversion 1.0 (svn) was released in February of 2004. Technology and habits at the time dictated svn's use and features. Core to svn's architecture is the concept of a centralized repository. This central repository allowed users to control who was and was not allowed to commit changes.

<img src="http://www.jendavis.org/assets/svn_vs_git.png" width="400">

A year later in 2005, Git was released. It’s also an open source software version control system with a focus on decentralized revision control, speed, data integrity, and support for distributed nonlinear workflows. This gives every developer full local control. While you can adopt a centralized workflow and establish a "central" repository, the processes can be flexible allowing you to use technology as you wish rather than having it defined for you. While the ramp up time may be a little longer, the functionality allows for quicker organizational changes.

Andy Peatling shared the WordPress [technical refresh](https://developer.wordpress.com/2015/11/23/the-story-behind-the-new-wordpress-com/) in migrating from svn to git in 2015, and the desirable changed behaviors that included:

* improved developer communication through code reviews and hangouts
* improved development practices of reviewing code prior to committing to the repository because of the availability of the *pull request* with git
* increased collaboration between designers and developers on a daily basis
* greater feedback on individual work,
* customized workflows

The technical merits between git and svn aside, significant value is derived from increased cross-team collaboration.

In many organizations, system configuration is a manual process. Individuals document the process and upgrade with a checklist. A missed step can lead to systems in an unknown state requiring considerable effort to recover.

Chef is an infrastructure automation system. Infrastructure automation is creating systems that reduce the burden on people to manage services and increase the quality, accuracy, and precision of a service to the consumers of a service.

When Adam Jacob was developing Chef software, he was [trying to create a solution that could work across different organizations](https://www.youtube.com/watch?v=Ia2ItmjRsw8&feature=plcp). Chef was built to provide abstractions for configuration and management, creating a language allowing individuals to define its infrastructure and policies with code.

Trying to create a language that allows for the nuanced views of developers, system administrators, security operations, and quality assurance engineers is difficult. With Chef, rather than reusing terminology that shows preference to one role over another, we have new terminology including resources and recipes.

**Resources** make up the basic building blocks of our infrastructure. We can use resources as provided by Chef core libraries, use resources provided by the larger Chef community, or we can build and customize our own.

**Recipes** describe a specific piece of an application that we want to have running on a system. It's the ordered set of resources and potentially additional procedural code. Just as with a recipe for baking chocolate chip or oatmeal cookies, the recipe will be specific to what we want to create.

<img src="http://www.jendavis.org/assets/chef_example.png" width="450">

In this simple _webserver.rb_ recipe from the [Learn Chef](https://learn.chef.io/tutorials/) website, we use 3 resources: **package**, **service**, and **file**. These resources describe everything needed to stand up an apache web server, have it run at boot time, and have it serve a simple "hello world" page.

More complex tasks like opening specific ports in a firewall or deploying Hadoop can be abstracted into a common language that allows for comprehension across teams. Because this code is stored in your standard version control, you can take advantage of the same ease of use and transparency that the rest of your source code is afforded.

**Devops is not limited to infrastructure.** A lot of focus is on tools that improve collaboration between development and operations teams as those teams are where the devops movement originated. As other teams begin adopting devops methodology, we'll see tools that support the devops compact between new teams.
For example, Chef has released [Chef Delivery](https://www.chef.io/delivery/) this year. Chef Delivery simplifies organizational complexity by creating a common language to describe the process of promoting products between teams. This common language allows us to codify "delivery as code".

## Devops is Automation

When people say _Devops is Automation_, it is due in part because many tools in devops, while codifying understanding to bridge the chasm between teams and increase velocity, have resulted in **automation** for repetitive tasks. Automation is a result of improved technology focused on repeatable tasks.

While reviewing the aviation industry in 1977, the House Committee on Science and Technology identified cockpit automation as a leading safety concern. Studies of the aviation field discovered that while pilots could still fly planes, the automation in use was causing an atrophy to critical thinking skills. Pilots were losing the ability to track position without the use of a map display, decide what should be done next, or recognize instrument system failures. This is a warning for us as we implement automation within our environments. Tools change our behavior and the way that we think.

In July 2013, Asiana Airlines flight 214 struck a seawall at San Francisco International Airport, resulting in three fatalities. During the investigation, the National Transportation Safety Board (NTSB) identified a number of issues, among them that there was insufficient monitoring of airspeed due to an overreliance on automated systems that they didn't fully understand.

>“In their efforts to compensate for the unreliability of human performance, the designers of automated control systems have unwittingly created opportunities for new error types that can be even more serious than those they were seeking to avoid.”
>James Reason, Managing the Risks of Organizational Accidents

Automation is critical to us as systems become more complex and organizations become interdependent due to shared services. Without shared mutual context or concern for human needs, automation creates unknown additional risk.

**Devops enabled automation may make work faster, but more importantly it has increased transparency, collaboration, and understanding.**

In summary, devops is **culture** which includes **tools and their use**. Tools help us progress from **manual** to **continuous** processes. Effective devops tools enable **automation** without isolating humans from the automation process so that the mutual understanding occurs across time, ensuring that the "we" of tomorrow understands the "we" of today.

## What Next?

Find a local [DevOpsDays](http://www.devopsdays.com), [CoffeeOps](http://www.coffeeops.org), or other cross-functional meetups that facilitates people coming together to build strong foundations of common understanding.

The [devops community calendar](http://www.devopsdays.org/events/calendar/) also lists upcoming conferences and events.

### Study

* [Github git tutorial](https://try.github.io/levels/1/challenges/1)
* [Atlassian Git tutorial](https://www.atlassian.com/git/tutorials/)
* [History of Chef](https://www.youtube.com/watch?v=Ia2ItmjRsw8&feature=plcp)
* [Learn Chef](https://learn.chef.io/tutorials/)

### Watch

* [DevOpsDays Silicon Valley 2015 Videos](https://www.youtube.com/channel/UChZXJu3ZGfsQYkJBJvlDjEA)
* [Tools for Effective Change Webinar](https://www.chef.io/blog/event/webinar-effective-tools-for-effective-change/)

### Listen

* [Arrested DevOps](http://www.arresteddevops.com/)
* [Foodfight Show](http://foodfightshow.org/)
* [DevOps Cafe](http://devopscafe.org)

### Read

* [devops Weekly](http://www.devopsweekly.com/) - weekly newsletter of curated devops news from [Gareth Rushgrove](https://twitter.com/garethr)
* [Comparison of Issue Tracking Systems](https://en.wikipedia.org/wiki/Comparison_of_issue-tracking_systems)
* [Comparison of Version Control Software](https://en.wikipedia.org/wiki/Comparison_of_version_control_software)
* [NTSB report for Asiana Airlines flight 214](http://www.ntsb.gov/news/events/Pages/2014_Asiana_BMG-Abstract.aspx)
* [Effective Devops](http://shop.oreilly.com/product/0636920039846.do)

### Share

I'd love to hear your feedback! What tools are you using in your environment and how do they impact organizational culture?

Tweet at @sigje with hashtag #sysadvent, email me at sparklydevops@chef.io, or add a comment to the article. 

## Thank yous

Many thanks to [Greg Poirier](https://twitter.com/grepory) for being my Sysadvent Editor. Additional thanks to [Nathen Harvey](https://twitter.com/nathenharvey), [Peter Nealon](https://twitter.com/peternealon), [Amye Scavarda](https://twitter.com/amye), and [H. Waldo Grunenwald](https://twitter.com/gwaldo) for peer review and aditional edits.

* Image Credits
 * Young Girl Tilting Camera Up. Licensed from Kenneth Wiggins on https://blackstock.co/collection/young-girl-tilting-camera-up/
 * Light Sky Silo Windows Sunlight Rays from Public Domain Archive