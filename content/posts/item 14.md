---
title: 'Confessions of a reformed Omeka acolyte. Minimalist options for digital exhibitions'
intro: "Minimalist computing approaches to digital exhibitions and implications for services and undergraduate instruction"
published: true
date: "2019-11-18"
publish_date: '11-18-2019 00:00'
taxonomy:
    tag:
        - blog
        - minimalist computing
        - practice
        - pedagogy
        - digital services
---

While a Digital Projects Coordinator at the University of Windsor in 2015-16, I remember thinking that Omeka would revolutionize the way we create and teach about digital exhibits, metadata, and the subtle acts involved in digital collecting. Here was a relatively lightweight CMS that enabled us to spin up new instances almost immediately. With set-up a breeze, we could focus our attention on the intellectual work of arrangement, description, and narrative. I was also excited by the opportunity that Omeka offered for pedagogy. At the same time as the public humanities picked up steam, Omeka lowered the barrier of entry for humanities instructors to introduce digital scholarship and create assignments revolving around the platform. In this context, and perhaps as a result of the interesting and deep relationship that I had created with the faculty at Windsor, we found ourselves in the classroom more often. 

> "Oh yeah, we'll just spin up an Omeka instance and be on our way. Digital exhibits? Sure. Collectons? Sure. Custom themes? Sure.

I became an Omeka acolyte.
 
I'm writing this because I recognize a similar optimism about recent software that embrace and advance the 'minimalist computing' paradigm. Here I'm thinking specifically of Wax and CollectionBuilder. 

Wax is essentially a Jekyll theme that uses Ruby gems to create "an extensible workflow for producing scholarly exhibitions with minimal computing principles." The exhibition sites created by Wax are static, meaning that they consist of flat HTML, CSS, and JavaScript files that do not require a database for file storage. As Wax documentation makes clear, this apprach "makes them cheaper, safer, and generally easier to maintain—as long as you’re willing to learn some new skills."

Arguably the skills needed to create Wax sites are more basic than those needed to run an Omeka instance. Wax involves learning a little about modern web development, the command line, spreadsheets, data management, GitHub (if you choose to use Github for hosting), and some plain text editing.

For more on Wax, visit their [documentation](https://minicomp.github.io/wiki/wax/).
![Wax Workflow](https://minicomp.github.io/wiki/assets/wax_workflow.jpeg)

CollectionBuilder is an even more robust exhibit builder that offers additional functionality "out of the box." CollectionBuilder also leverages the power of Jekyll and Ruby gems, as well as some additional open source Javascript libraries — like Leaflet — to create static websites of interactive digital exhibits rich in metadata. Similar to Wax, CollectionBuilder requires some knowledge of the command line, basic web development principles, and metadata. Check out their webpage for documentation and [examples](https://collectionbuilder.github.io/).

These are two examples of approaches inspired by the 'minimalist computing' paradigm put forward by [Alex Gil](http://go-dh.github.io/mincomp/thoughts/2015/05/21/user-vs-learner/) and [Jentery Sayers](https://go-dh.github.io/mincomp/thoughts/2016/10/03/tldr/). The paradigm is centered on a set of questions that we must ask ourselves and our collaborators before jumping headfirst into an exciting new project. They are:

>“What do we need?”; “What don’t we need?”; “What do we want?”; “What don’t we want?” 

The answer to this question can now be modified by the adjectives "minimal" or "maximal": "minimal design" / "minimal dependencies" / "maximal collaboration" / "maximal accessibility." We've reached a point in the ebb and flow of design and aesthetics where minimalism is appreciated and encouraged. Moreover, with tools like Wax and CollectionBuilder, we have the ability to create elaborate projects that feature attractive and accessible front-ends without the added infrastructural baggage. As Gil writes, the culture of "user friendly" interfaces has 

>...also led to some basic misunderstandings of what computers can and should do. In the case of writing, the expectation that you should get what you see continues to distance producers from their tools.

I think we can extend this to critique the way we "build" content management systems that privilege easy administration (GUIs, DBs) over direct interaction with the process of building (a command line, a spreadsheet, a text editor). Ultimately, I think this is an exciting period for library services as well as an opportunity to refocus our library instruction. We've been experimenting with integrating minimalist solutions in our workflow. You can see some of our work with Wax [here](https://dss.ncf.edu/pei/) and [here](https://dss.ncf.edu/constitution/).

I'm currently in the process of integrating Wax and CollectionBuilder in my instructional collaborations with willing faculty. Some students have expressed interest in creating digital exhibits, as well. For example, a student this term wanted to create an interactive digital exhibit of 49 printing shirt screens made and used by New College of Florida students and staff. As they state on the project's main page, "Screenprinting is a printing method used to reproduce designs on fabric, primarily t-shirts. The designs on the screenprints below would have been reproduced multiple times for different people. New College students made these printing screens because they thought the design was important enough to not only produce but reproduce and distribute. Therefore, by looking at these screens we can find out what kind of things New College students thought important enough to commemorate." You can check that out [here](https://carolinenewberg.github.io/ncf-screenprints/). 

Building on this, in the Spring I'll work with a class on creating a collaborative digital collection using CollectionBuilder for an *Introduction to the Humanities* class. The idea is to follow through the entire collection lifecycle, from the archive, through digitization and description, to the technical components (including metadata, spreadsheets, and some command line) of digital exhibit building. 

Finally, I've noticed a gradual change in how I approach digital scholarship. In my current role I oversee the technical as well as the pedagogical side of digital projects. Sustainability, minimialism, and small technical-footprints are important principles that orient my work as I seek to shepherd projects that will add value (to a person, a class, a community, etc) at a reasonable cost with respect to technical and human resourcing. I also accept that these projects will not last forever, but they might outlast me in this position. I think I'm responsible for ensuring that the next person in this role inherits a clean (leave my desk out of this!) and sustainable environment that allows them to continue/pivot/change without interruption. 

The work that I did with Omeka was key because it shaped the way I approached library involvement in the classroom. Many of the sites we worked on then are still online, though they've started to show their age. And so, while many things have changed since, the energy that I receive from instruction sessions that go beyond library databases has remained a constant. Software like Wax and CollectionBuilder will only work to augment the connection between library technology and the classroom, and that, to me, is an exciting proposition.