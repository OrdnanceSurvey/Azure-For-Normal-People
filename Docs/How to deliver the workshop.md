# Azure for "Normal" People


## The General Idea:
The following is adapted from a presentation given at the National DevOps Conference in 2019, and thus is in a semi-conversational style.

Participants enter the room and sit down in teams, at their tables, one table per team. We normally run with about 20 people, so roughly 4 groups of 5.
There's a screen at the front that everyone can see and that the facilitator controls.
There are tables nearby, covered with all of the paper resources the teams will need.

The facilitator tells a story, which is backed up by the slides on the screen. 

The story is the core of the whole thing. It's crafted to introduce problems, needs, and solutions, one at a time.

The problems, needs, and solutions are all things engineers would recognise: 
* the problem of being afraid to experiment with code for fear of accidentally breaking it, and how that stifles innovation,
    * which draws out the need to be able to restore it back to previous (working) versions if we make a mistake,
        * which is met by the concept of versioning source code, and implemented, for us, by git.
* the problem of keeping our environments in sync,
    * which means we have a need for repeatable deployments, 
        * This is met by having deployment pipelines, and infrastructure as code.

The solutions to the problems are artefacts or processes that we want to introduce to the teams to. The story is so powerful because it _pulls_ in the next solution. Everything we introduce solves a problem that the teams have; so the purpose of everything much clearer.  
Discovering and identifying all these problems, needs, and solutions takes the team on something like the software engineer's journey. Many of the practices that we adopt as professionals have been hard won from experience. Taking non-technical staff on that same journey gives them some context for why we do the things we do, and gives a justification for some of the practices we're so passionate about and insistent about on!

The only real problem with the story is it's not super realistic.  
It's orientated around the purpose creating problems and needs in a specific, logical order, which means it isn't orientated around being realistic - we make some generalisations take some artistic license. You might need to give your audience a heads up on this, and ask them to go with you! 

Accordingly, you'll to extend the same indulgence to me, as I'm going to take you on a whistle stop tour of the workshop, so you can get a feel for it. I'll be summarising and skimming over the content - I'm not intending to give you a good introduction to the Azure - but I will give you a high-level overview to the approach by which we do introduce Azure and some DevOps practices. In the real workshop we go more slowly, and break all the content down and explain it at an appropriate level. In the workshop, teams are tasked with solving problems by putting artifacts and processes in place as they come up.

## The Story Starts
The story is at the heart of it all, and our story starts with: The business has a new idea for a software product they want to create.
And they give us some requirements.
And to start the workshop off, we establish that all the business process prerequisites have been satisfied.

The first problem is evident - we need a developer!
This is where our teams first start to get involved. Each team is sent to collect a developer, and a laptop, and name their developer.
We then talk about the developer starting to work locally on their laptop, storing the code on their hard-drives, and using hardcoded test data. So, teams collect an "Application" and put it on the developer's laptop.
From there we introduce that need for versioning source code. We talk about git; teams collect "a git", put it on the laptop, and store the application "in" it.

Now, the problem is the Product Owner wants to see the software working. They can't take the developer's laptop to play with whenever they want, and we wouldn't expect our customers to do that. So we _need_ to deploy it to the cloud for the Product Owner to try out.
To do that, we need some space in Azure, which we get with Azure's Subscriptions and Resource Groups. We talk about Authorisation and Authentication for access.

Once we have space in Azure, we need something in which we can run our code - it could be any number of execution environments, but for our website scenario, we introduce an Azure WebApp.

With our code running in Azure, the problem we're now facing is that we're using fake, sample data. We need real data, and somewhere to store it - we introduce Table Stores in Storage Accounts.
The problem is now, how do we securely store the sensitive connection data for the Storage Account? We need a KeyVault (another Azure resource).

By this stage, our groups have built this.

The story introduces more requirements, enhancing the system.
This brings in more problems and needs like:
* the need for two developers to work simultaneously, without breaking each other's stuff, where the solution is isolation - so two development environments.
* this isolation creates its own problems - these two environments have the latest features each developer is working on. We need to bring the features together, so the solution is integration - so teams build a continuous integration environment.

* now we have ci environment, but it's liable to break if something goes wrong with integration, it's not stable. We need a stable environment for our producut owner and customers, that we happen to call prod.
* building all these environments manually is a pain, and there's huge risk of them getting out of sync, so we need to introduce infrastructure as code and pipelines so we can reliably and repeatability deploy.

This is hugely powerful moment for illustrating the need for automation - the teams have an understanding of what is to have to manually deploy environments because they've been up and down collecting bits of paper. It's really quite grating by the end. 

And they have an inkling of the challenges of keeping environments in sync; they've been manually inspecting environments to make sure they are the same, and they do make mistakes. They learn that it's harder than it sounds, and human intervention can introduce errors.

So introducing infrastructure as code is a logical step. And showing them how deployment pipelines take the infrastructure and application code, and deploy to each of the environments, makes sense.
    
We congratulate the teams on their system, which is hugely popular. So much so, in fact, that the site is getting dangerously close to its traffic capacity, and everyone it panicking, and it's about to fall over.
But it's actually not a problem, and again we can show the power of infrastructure as code, as we simply scale our instance _up_ to a more powerful box which can better handle the traffic.
We repeat the traffic surge later on in the workshop, when scaling up is no longer sufficient, and show how the cloud can scale _out_ as well.
This is a great way of dispelling the idea that the cloud just the same computers in someone else's data centre, and that it can be treated as such. Showing how simple this scaling, up and down, out and in, can be, and contrasting it to on-prem hardware provisioning and configuration, is really powerful.

The power of the workshop really comes in at the end, when teams have built a big, comprehensive picture out of tiny details. 

With the technology quite literally on the table, we spend some time talking about culture, and how we need our non-technial stakeholders to support and empower our developers in our DevOps cultural change.

--------------------------------------------------------------------------------------------------------------------------------------------

This gives you a flavour of how the workshop works - name a problem, capture a need, satisfy the need with a tool or process that you want your participants to understand.
As much as possible, the scenario is rigged to let participants discover the problems and needs on their own, thereby taking ownership of the solutions.

## Metaphors
The workshop is full of metphors, both explicit and implicit.
* For example, we explicitly compare Authorisation with Role Base Access Control with a bouncer at a music festival, who allows (or disallows) access to different areas, depending on the role (or the type of ticket held) by anyone trying to get in. A person in the role of festival goer will be allowed access to the public areas, people in the role of VIP, that is, with a VIP ticket, will be allowed in the public areas, and backstage to meet the bands. Stagehands won't be allowed to mix in the VIP lounges, and only the administrators (insert sysadmin joke here) are allowed in the privalleged offices. And people who have no role at the festival can't access _any_ areas.
* Authentication is proving who you are. Normally this is with a password, but there is also Multi-factor authentication, where you're texted a code, or where you have to put your bank card into one of those little card readers. It's all about proving you are who you say you are.  
Authentication in Azure is commonly done with Azure Active Directory. In the workshop, Active Directory becomes a literal directory; authoritative book of identities into which the teams write names and arrange security groups.

More important, to me at least, are the implicit metaphors.
* Teams have to self-provision all the resources, just like how we want to empower DevOps teams with DevOps practices.
* The participants work in teams, just like developers, and have the same tasks of coordinating efforts in complicated systems.
* They have to go through manually building environments, and they see how easy it is to accidentally let environments get out of sync when the deployments are not automated.


Metaphors like these allow us to delve into technical topics we'd otherwise have to skim over. We don't go into massive detail, but we do do enough to empower technical and non-technical staff to be informed and make good decisions.





    
That's what is in the box for you to peruse. You're free to use it - it's open-source. It should be enough to get you started. Like I say, compiling the narrative, the story in the middle of it, is the hardest part.
We'd love to get feedback if you do decide to use the resources, and if you generate something that could be useful to others, we hope you'll consider contributing it for the community.


We've seen great feedback from running the workshop, and our participants have reported a greater understanding of the conversations going on around them.
We've shared our resources, and we hope you find them useful.

## Logistics and stuff:    
### Time:
* At the minimum: 1hr
    * Not recommended. It works, but delegates have to save their questions until the end, and they don't get as much out of it.
    * Recommended: 2hr  
    We tend to book the session for 2hrs, finish the content after 1h30, have 10 minutes of intense questions and filling in the sheets, and then let people drift off when their questions are answered. The last delegate leaves around 1h50.  
    We only recently upped our time slot, and our next iteration will have a break in about half way through the time slot.
* Delegates
    * Up to four groups of 4-6 people
        * more people than this can mean the questions really slow the flow of the workshop
        * more than 6 people in a group mean that there isn't enough to occupy everyone - people sit out
* Room layout:
    * one table per group
        * the table needs to comfortably accommodate a Subscription and still have space around the Subscription for the other resources
        * we pushed two 1x2m tables together to make a 2x2m surface
        surfaces upon which to lay out the resources
        * about 4m2 is enough for up to four groups' worth of resources
        
* Resources:
    * Staff:
        * A facilitator:
            * This does need to be a technical person that knows your organisation well enough that they could modify the workshop to your organisations tools and workflows.
        * Helpers:
            * This really depends on the current knowledge of your workshop delegates. We find the workshop goes most smoothly when we have a helper per group, but you might get away with fewer. In our experience, they end up answering a lot of questions from groups, and they are also invaluably useful for making sure things go in the right places. Resources have to go in Resource Groups, not straight on to the Subscription. Azure DevOps doesn't go into the Subscription.
        
    * Caveats:
        The workshop has each group building into one Subscription (paper size constraints)
        

        
## Scenario Patterns

* For the Ordnance Survey narrative flow, the system:
    * is Query driven  
    * holds data in Table storage  
    * Displays on Webpage (request goes in, table storage queried, data returned to webpage)

* Next iteration Requirements
    * Enhance data with data from another service
        * where the service is developed and deployed by another team in the organisation

* Further iteration requirements
    * Enhance with yet another service
        * where the data is 
            * provided by a third party 
            * posted to blob storage
            * then unpacked to table  
            It makes sense for this to be a cyclic data update, something like Addresses? Population Data? IMDB? DVLA?

* Ideas in this pattern:
    * School
        1. Pupil roster
        2. Enhance with grades
        3. Enhance with addresses, to see if place of residence is correlated with grade
    * Customers
        1. List of customers
        2. Enhance with their order histories
        3. Enhance with cookie/tracking data to see what ads might be having an effect
    * Cars
        1. List of cars
        2. Enhance with mechanic reports
        3. Enhance with weekly national sales update
        

## Wider Context
At Ordnance Survey, we start by spending a couple of minutes explaining some more context around business change. Our move to the cloud has coincided with other business process changes, and sometimes the lines between the sources of change get blurred, so we spend a few moments making it clear what is in and out of scope for the session.

## To Dos for this documentation
* mention the instructions at the bottom of the slides
* mention reflection - we reflected after each and every session, making changes


Logistics  
&nbsp;&nbsp;&nbsp;&nbsp;room etc.  
Format  
&nbsp;&nbsp;&nbsp;&nbsp;paper  
Resources  
&nbsp;&nbsp;&nbsp;&nbsp;Narrative  
Structure  
&nbsp;&nbsp;&nbsp;&nbsp;Metaphors  
Concepts  

Scenario