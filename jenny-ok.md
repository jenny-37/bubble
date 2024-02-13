
# THE ULTIMATE GUIDE TO BUBBLE PERFORMANCE

## HOW TO BUILD FAST, SCALABLE APPLICATIONS IN BUBBLE

## Content

### Notes on the revision

### Introduction
- [How to read this book](#how-to-read-this-book)
  - [What performance is](#performance)
  - [Knowing the platform](#capacity)
  - [How to build for performance](#how-to-build-for-performance)

### Concepts, definitions and fineprint
- [Performance](#performance)
- [Capacity](#capacity)
- [Server-side and client-side](#server-side-and-client-side)
- [Responsiveness](#responsiveness)
- [Third-party services](#third-party-services)
- [Editor performance](#editor-performance)
- [Experience level](#experience-level)
- [A word on planning](#a-word-on-planning)
- [The difference between best practices and tools](#the-difference-between-best-practices-and-tools)

### What is an app?

### How performance is perceived
- [Perceived vs actual performance](#perceived-vs-actual-performance)
- [Developer-perceived performance (a.k.a. watching grass grow)](#developer-perceived-performance)
- [Performance is a feature](#performance-is-a-feature)
  - **Bubble plans**
    - [Are you investing in performance or capacity?](#bubble-plans)
  - [The research phase](#the-research-phase)
    - [The tool for your project](#the-tool-for-your-project)
    - [Asking the right questions](#asking-the-right-questions)
  - [Understanding Bubble's capacity dilemma](#understanding-bubbles-capacity-dilemma)
    - [A jack of all trades](#a-jack-of-all-trades)
    - [Bubble's history of performance](#bubbles-history-of-performance)
    - [Bubble official documentation and guides](#bubble-official-documentation-and-guides)
  - [Bubble performance vs. device performance](#bubble-performance-vs-device-performance)
    - [RAM usage](#ram-usage)
    - [CPU usage](#cpu-usage)
    - [Download size](#download-size)
  - [Bubble's servers and Cloudflare](#bubbles-servers-and-cloudflare)

### Bubble's performance limitations
- [Manipulating large data sets quickly](#manipulating-large-data-sets-quickly)
- [Working visually with long lists of records](#working-visually-with-long-lists-of-records)
- [Complex searches](#complex-searches)
- [Server-side Javascript](#server-side-javascript)
- [Loading UX](#loading-ux)

### How Bubble's database works
- [Understanding indexing](#understanding-indexing)
- [How Bubble chooses what to index](#how-bubble-chooses-what-to-index)
- [How indices work on your app](#how-indices-work-on-your-app)
- [Structured and unstructured data](#structured-and-unstructured-data)

### How a page is loaded
- [Page load sequence](#page-load-sequence)
- [How the page is rendered by the browsers](#how-the-page-is-rendered-by-the-browsers)
  - [Repaints](#repaints)
- [Priority of general event workflows and page load](#priority-of-general-event-workflows-and-page-load)
  - [Page is loaded](#page-is-loaded)
  - [Current User is logged out](#current-user-is-logged-out)
  - [Do every X seconds](#do-every-x-seconds)
  - [Do when condition is true](#do-when-condition-is-true)
- [Workflow sequence priority: server-side](#workflow-sequence-priority-server-side)
- [Workflow sequence priority: client-side](#workflow-sequence-priority-client-side)
  - [Custom events](#custom-events)
- [Back-end workflows/API workflows](#back-end-workflows-api-workflows)
- [How Bubble determines that the page is finished loading](#how-bubble-determines-that-the-page-is-finished-loading)
  - [Page loaded (entire)](#page-loaded-entire)
  - [Page loaded (above fold)](#page-loaded-above-fold)
- [Client-side vs server-side operators](#client-side-vs-server-side-operators)

### The Page
- [RAM usage and download size](#ram-usage-and-download-size)
  - [How small should a website be?](#how-small-should-a-website-be)
- [Downloads](#downloads)
  - [The Bubble engine](#the-bubble-engine)
  - [Images](#images)
  - [Fonts](#fonts)
  - [Icon packs](#icon-packs)
  - [Javascript libraries (plugins)](#javascript-libraries-plugins)
  - [CSS (styles)](#css-styles)
- [Measuring the size of the page and all assets](#measuring-the-size-of-the-page-and-all-assets)
  - [Identifying searches](#identifying-searches)
  - [Reading the waterfall chart](#reading-the-waterfall-chart)
    - [How to identify different types](#how-to-identify-different-types)
      - [Images](#images)
      - [Plugins](#plugins)
      - [Fonts](#fonts)
      - [Icon libraries](#icon-libraries)
  - [Single-page app versus multi-page app](#single-page-app-versus-multi-page-app)
  - [Rendering lists](#rendering-lists)
    - [Info saved directly on the list Thing](#info-saved-directly-on-the-list-thing)
    - [Info saved on a Sub-Thing](#info-saved-on-a-sub-thing)
    - [Processing on Sub-Things](#processing-on-sub-things)
    - [Conditions](#conditions)
    - [Setting up fast lists](#setting-up-fast-lists)
  - [The Repeating Group trap](#the-repeating-group-trap)
    - [Full load vs partial load](#full-load-vs-partial-load)
    - [Hiding by default](#hiding-by-default)
    - [Lazy loading](#lazy-loading)

### CPU usage
- [Rendering the page](#rendering-the-page)
- [Leveraging client-side data processing](#leveraging-client-side-data-processing)

### Measuring page rendering
- [Paint flashing](#paint-flashing)
- [Checking Layers](#checking-layers)
- [Measuring the frame rate](#measuring-the-frame-rate)

### The database
- [What slows the database down](#what-slows-the-database-down)
  - [Download size](#download-size)
    - [What determines the size of a database record?](#what-determines-the-size-of-a-database-record)
  - [Complexity](#complexity)
- [Introduction to structuring](#introduction-to-structuring)
  - [Planning your database](#planning-your-database)
    - [Balancing the need for advanced database structuring](#balancing-the-need-for-advanced-database-structuring)
    - [Don't use Bubble for note taking](#dont-use-bubble-for-note-taking)
    - [Get away from the screen](#get-away-from-the-screen)
    - [Always build with Privacy Rules in mind](#always-build-with-privacy-rules-in-mind)
    - [Keep your user in the center of things](#keep-your-user-in-the-center-of-things)
  - [The process of creating a Data Type](#the-process-of-creating-a-data-type)
    - [Terms we'll use](#terms-well-use)
      - [Data Concept](#data-concept)
      - [Data Weight](#data-weight)
      - [Requirement Conflicts](#requirement-conflicts)
      - [Satellite data types](#satellite-data-types)
        - [Search data types](#search-data-types)
        - [Content data types](#content-data-types)
        - [Link Data Type](#link-data-type)
      - [Merged data types](#merged-data-types)
    - [Scenario 1: Vendors and Clients in a CRM](#scenario-1-vendors-and-clients-in-a-crm)
      - [Step 1 - Define the Data Concept](#step-1-define-the-data-concept)
      - [Step 2 - Identify requirements](#step-2-identify-requirements)
      - [Step 3. Identifying conflicts](#step-3-identifying-conflicts)
      - [The User's perspective](#the-users-perspective)
    - [Scenario 2: Travel App](#scenario-2-travel-app)
      - [Step 1: Define Data Concept](#step-1-define-data-concept)
      - [Step 2: Identify requirements](#step-2-identify-requirements)
      - [Step 3: Identify conflicts](#step-3-identify-conflicts)
      - [The User's perspective](#the-users-perspective-1)
    - [Syncing data between different Data Types](#syncing-data-between-different-data-types)
  - [Searching efficiently](#searching-efficiently)
    - [More constraints is better](#more-constraints-is-better)
    - [Duplicate searches](#duplicate-searches)
    - [Bubble downloads only the data you need](#bubble-downloads-only-the-data-you-need)
    - [Using lists as saved searches](#using-lists-as-saved-searches)
  - [How the :filtered (and other) operators works](#how-the-filtered-and-other-operators-works)
  - [Nested structures](#nested-structures)
    - [In searches](#in-searches)
    - [In Repeating Groups](#in-repeating-groups)
  - [Searches and lists](#searches-and-lists)
    - [Lists](#lists)
    - [Searches](#searches)
    - [Which is faster?](#which-is-faster)
  - [Option sets](#option-sets)
    - [Creative uses of Option Sets for performance](#creative-uses-of-option-sets-for-performance)
      - [Replacing database entries for quicker loading](#replacing-database-entries-for-quicker-loading)
      - [Building an app menu and User privileges in the same Option Set](#building-an-app-menu-and-user-privileges-in-the-same-option-set)
      - [Option Set as a Message Popup](#option-set-as-a-message-popup)

### Workflows
- [What are workflows?](#what-are-workflows)
- [Front-end and back-end workflows](#front-end-and-back-end-workflows)
  - [Front-end workflows](#front-end-workflows)
  - [Backend workflows](#backend-workflows)
  - [How backend workflows affect the front-end](#how-backend-workflows-affect-the-front-end)
    - [Scheduling backend workflows](#scheduling-backend-workflows)
    - [Bubble is optimized for front-end actions](#bubble-is-optimized-for-front-end-actions)
    - [So... never use backend workflows then?](#so-never-use-backend-workflows-then)
  - [Client-side and server-side actions](#client-side-and-server-side-actions)
  - [What slows workflows down?](#what-slows-workflows-down)
- [Action response design](#action-response-design)
  - [Immediate response](#immediate-response)
  - [Delayed response](#delayed-response)
  - [Future response](#future-response)
- [Immediate response](#immediate-response-1)
- [Delayed response](#delayed-response-1)
  - [Action sequence order](#action-sequence-order)
- [Background triggering](#background-triggering)
- [Spacing out workflows](#spacing-out-workflows)
  - [Multi-step](#multi-step)
  - [Process spreading](#process-spreading)
  - [Using process spreading for error messages](#using-process-spreading-for-error-messages)
- [Do Not Repeat Yourself (DRY)](#do-not-repeat-yourself-dry)
  - [Custom events](#custom-events)
  - [Reusable elements](#reusable-elements)
  - [Sharing Custom Events across your app with Reusable Elements](#sharing-custom-events-across-your-app-with-reusable-elements)
- [Leveraging the Bubble back-end](#leveraging-the-bubble-back-end)
  - [Schedule workflow on a list vs. recursive workflows](#schedule-workflow-on-a-list-vs-recursive-workflows)
    - [Recursive workflow delays](#recursive-workflow-delays)
  - [Backend triggers](#backend-triggers)
    - [Deleting complex data](#deleting-complex-data)
    - [Using back-end triggers to keep data in sync](#using-back-end-triggers-to-keep-data-in-sync)
    - [Combining Option sets and triggers to automate workflows](#combining-option-sets-and-triggers-to-automate-workflows)
    - [When to use back-end triggers](#when-to-use-back-end-triggers)
- [Communicating clearly](#communicating-clearly)
  - [Action received](#action-received)
  - [A process is running](#a-process-is-running)
  - [A process is finished](#a-process-is-finished)
- [Performance is a war of a thousand battles](#performance-is-a-war-of-a-thousand-battles)
- [Performance is a feature](#performance-is-a-feature-1)




=======



# Introduction

## How to read this book

This book is split into three sections:


### What performance is

How you perceive an app's performance is determined by a complex combination of Bubble's software, Amazon's hardware, your user's device, app design and psychology.
In other words, the process of building an efficient app requires an understanding of all of these factors and how they play together. While tutorials certainly have their use, I'm hoping this guide can give you a deeper understanding of the underlying philosophy behind making efficient applications.


### Knowing the platform

Whatever you build in Bubble, it's probably not just for fun. Most projects are built on some kind of business or project idea that you expect will give you a return on the time and money you have invested. While Bubble is a fantastic tool, that doesn't automatically mean it's the right tool for every project. Knowing the pros, cons and limitations of the platform you choose, how to weigh your decisions and compromises and spotting challenges before they arise can save you months of going down the wrong path. This section also goes through some of Bubble's core features and explains how they work.



### How to build for performance

With an understanding of what performance actually is and what Bubble brings to the table, we can start digging into the juicy stuff: how to build an app that performs and scales well. We'll go through a range of different methods that lean on the preceding chapters for support: how to load pages quickly, how to structure your database for speed, making wise UX choices, leveraging back-end workflows, spacing out processes and plan for scaling.





### Concepts, definitions and fineprint

Throughout this book, I'll be referring to a lot of different terms and concepts. Since some of them can have a different meaning in another context, I'll list them here to clarify what I mean in the context of this book.

### Performance

Determines how smooth different parts of your app seem to your users. For example:

• Loading a page
• Finishing a workflow when a button is pushed
• Maintaining the frame rate during scrolling, animations, etc
• Scrolling through lists
• Navigating your app
• Saving an entry in the database


### Capacity

How much work you can give your app before it starts to visibly affect performance or time out. For example:
• Changing a list of things
• Performing complex and/or nested searches
• Scheduling back-end workflows on a list
• Scheduling recursive workflows
• Having lots of users in your system at the same time

### Server-side and client-side

Server-side and client-side describe whether something is happening on the server or in the browser on the user's device. We'll come back to this repeatedly, as balancing these two are a key component to creating snappy applications.



### Responsiveness

In this guide, I'll be using Responsiveness to describe how responsive a system feels: that is, the time it takes from an action is initiated until the user can see a reaction. Not to be confused with responsiveness as often used in Bubble to describe how the page responds to different screen sizes.


( IMAGE =

**Server-side** stuff happens
on Bubble's servers

**Client-side** stuff happens
on the user's device

)



### Third-party services

Some of the challenges outlined in this guide can be fixed or optimized using third-party services. Speeding up searches with Algolia or manipulating data sets with Parabola are examples of this. I also avoid mentioning specific plugins or custom code.
Solutions like this are outside of the scope of this guide, but are worth researching if you're running into challenges.

### Editor performance

A known issue with the Bubble editor is that it can slow down when editing pages with a lot of elements and/or workflows (one-page apps often suffer from this). This guide will focus on the front-end, and not the editor.

### Experience level

This guide assumes that you know your way around Bubble. You don't need to be an expert by any means, but to keep the guide streamlined I avoid explaining any of the core Bubble functionality.

### A word on planning

Many lessons in this book boil down to the same point: planning is essential. While I won't incessantly repeat this point throughout the book, I want you to approach the book with that in mind: jumping into the database structure and app design without a plan is the quickest way to lose track of why your app starts slowing down. For newer users, I would also politely point out that your first app is probably not going to be performing as well as you hope. Bubble is easy to use, but there is a learning curve, and some lessons are hard-earned. While I hope this guide can save you from making some
of the mistakes that I have made over the years, it's just a fact of life with Bubble as with most things, that you'll get better with practice. Don't invest your kid's college funds in your first app, and be open to the possibility that it might just suck. Not trying to build the perfect app your first time around gives you freedom to experiment, so don't box yourself in with ideas of perfection.

Your app may end up being pretty good. But the next one will be better.

### The difference between best practices and tools

Those who have seen any of my presentations or attended a coaching session know that I stress this point: this book presents a list of tools. Sometimes they are worth implementing, sometimes they're not. Treat every tip in this book as another tool in your box, not a religion you should adopt or the officially sanctioned "best way to do things".

• Some you may want to implement right away
• Some you may want to implement after your initial launch as an added feature
• Some may not be right for your app at all



---

## What performance is

The difference between actual performance and user-perceived performance


## What is an app?

It may sound silly. Of course you know what an app is, or you wouldn't be here trying to build one. But let's still take a quick glance at it, as I find it's often helpful to break things down to their simplest parts to understand them better.
Let's first look at the word. App. Depending on whom you ask, most will agree that the word app is defined loosely enough to include both a calculator on your mobile and a billion-dollar CRM system. As long as it's a piece of software that has a user interface, it's an app. Simple.

The web browser has in many ways become a new kind of operating system. Where you used to install software on your computer to run, an increasing amount of these applications now exist 100% in your browser. There are many reasons for this: the fact that you can pick up your work on any device with an internet connection, that you can exploit the hardware of massive server parks where uptime and security is taken care of, and that your work increasingly is backed up for every single action you perform (like a Google Doc or indeed a Bubble app).

So what does an app do? Well, most ideas, from your homemade cake recipe catalogue system to the global social network with billions of users are really the same thing: a new way to manipulate and visualize information stored in a database. Facebook is just a spreadsheet of User profiles saved in a server park somewhere, and every image, every like, every happy birthday-post, as social as they may feel to us, are all simply a way to visualize the server's data in a way that we find appealing.

Other apps focus more on the processing of information to speed up tasks that would otherwise be cumbersome. The exchange of map coordinates, user reviews and secure payment tokens has made Uber one of the biggest commercial successes of our time.
Uber doesn't actually drive you anywhere, it simply searches its database for someone who can, provides basic communication and arranges a financial transaction. Storing, indexing and transferring the content of audio files has made Spotify a household
name. It didn't invent music, it just made it simpler to navigate by finding ways to make a database search efficient and visually pleasing.

These apps are so different, we forget they are all the same.

They all work on two layers. One layer is hidden and one is visible: one is complex to the point where a human brain cannot even begin to process it - the other working solely and intentionally to hide that fact. Ordering an Uber is a preposterously complex process of ongoing information exchange between devices all over and above the planet, but for you, it's no more than a few clicks at the screen. Hello. Goodbye, Thanks for the ride.

The fact that the complicated inner workings are invisible to you is not a bug, but the app's main feature. Your job as a designer and developer is to break the chain between the two layers and make complicated stuff seem easy. More settings, more choice and more insight into how the process looks would make the app worse, not better.

So what does that tell us?

It tells us that in the stage show that is your app, you are the magician. You get to tell the user what to do and where to direct their attention. You get to prepare the stage, the machinery, the tools and equipment and train the beautiful assistant to do exactly
what you want to avoid breaking the illusion. The user doesn't need to know what's going on backstage.

If you do your job right, they'll believe it's magic. If you reveal your trick, or complain how hard it is to do, you're not helping your audience - you're ruining their evening.


## What performance is

Performance can be separated into two parts: Actual performance, and user-perceived performance (often abbreviated to UPP). Actual performance is how well your app is optimized to complete a given process within a set amount of time. In most cases, the final processing time is not the result of one single factor, but the combined work time or delays that each step adds.

1. Button clicked = 0ms
2. Send query to server= 200ms
3. Server processing query = 200ms
4. Send result back = 200ms
5. Render result = 50ms


In this simplified example we follow a process going through different steps. A user clicks a button, and 650 ms later, the result is visible on the screen. The steps marked with a **red clock** are delays that add no value to the process. They're simply a necessary
part of the process, some of them governed by the laws of nature more than anything else.

When the user clicks the button, the user's web browser sends a query to the Bubble server. This little packet travels at near the speed of light through fiber optic cables across the country, continent or planet, depending on where you live and where the server is located. Bubble's server receives the query and processes the request, and then has to send the information back through the same web of cables, before your device receives it and your CPU goes to work to render the changes on the screen.
The important thing to note here is that while there is a total processing time of 650 ms, Bubble's servers and software are only responsible for 200 of them.

An important mindset to take in as you prepare to optimize your app is that performance is a war of a thousand battles. There are few things you can do in isolation that will drastically change your performance, but a thousand right decisions can lead to significant improvements.


## How performance is perceived

### Perceived vs actual performance

User-perceived performance is the only performance that matters. Your users will bring their own expectations, and provide your app with input as they click, write and drag their way around it. In return, you give them an output that they can see, hear or feel.
User-perceived performance is not the time, but the quality of the output that comes in response to a user's input.
Whether your app is fine-tuned to process 100.000 database records in a second, or if it struggles to process a single one is irrelevant if your user can never tell the difference. If given a choice between an app that feels quick and responsive, but is inefficient under the hood and one that breaks world records in data processing, but feels choppy and slow, they would pick the first one every time.
User-perceived performance can be manipulated by all sorts of tricks to hide the fact that your app doesn't operate at lightning speed, and many of them have nothing to do with performance at all. Loading screens, animations, asking for user input and other distractions are all perfectly valid ways to hide the fact that your app needs some time to finish a process, and it's being done to you constantly without you being aware.

In the end, your job as a developer is to build a **first layer** that is optimized for quick loading, low memory usage and quick processing, and a **second layer** that offers an experience that your users enjoy regardless of the limitations of the hidden layer beneath.

### Developer-perceived performance (a.k.a. watching grass grow)

We can't discuss the psychology of perceived performance without bringing your perspective as the developer into the conversation.
We can all agree that performance is an important set of metrics for your application, but as with all things in life, a bit of perspective makes sense. Watching and timing every click of a button and agonizing over a workflow that takes longer than you hoped
can help you create a faster app, but it can also kick you down to OCD town where you waste months obsessing over something that your users will tolerate just fine (maybe
not even notice).
Let's get two things out of the way first: a watched kettle will never boil, and your own app is always going to seem slow. Let's say you click the Create user button in your app, and the seconds pass. You switch between watching the grass grow outside and staring at the screen while Bubble sets the user up for you. Hopeless.

But is it?

How long did it take to set up your Gmail account? Your LinkedIn profile? Your Apple ID? I bet you have no idea. You didn't think about the five seconds it took, because it wasn't your app. In most cases, your app likely performs on par with any other app. It's just that you're not obsessively timing those.

**Loading Gmail**

Even Gmail needs a few moments to load

The insight that you can easily get lost staring at your own work also applies to making realistic comparisons: searching on Google is insanely fast, because Google has had the best engineers on the planet looking into that since 1998. It’s literally the only thing Google.com does. Twitter runs like clockwork for hundreds of millions of users simultaneously because they’ve invested massive resources over many years making sure that it does. Try searching in another app, such as your CRM or some internal company sotware that you use, and you’ll see that they perform just like your app – average. Searching in databases is pretty slow. It can be solved with complex indexing, caching and algorithms, but to really specialize in a specific area like search probably requires more tech talent than you can aford.

### Performance is a feature

Your app consists of features. Some of them will be ready in time for the app’s first release, many will not. You’ve compromised, and you’re probably already looking forward to writing blog posts and tweets to your future loyal users describing the new features you just deployed.
Performance is another feature. There are lots of small improvements you can implement to fine-tune your page load. Some of them will take a bit of extra time, others a lot. Some are worth doing before the first launch, others aren’t, even if they’re worth doing later.

Developing eiciently means knowing when you’re becoming your own worst enemy – be mindful of your priorities, and keep in mind that the best product, ater all, is the one that ships.

### Bubble plans

**Are you investing in performance or capacity?**

Many curious users ask themselves if their app will perform better on a more expensive plan. This is a natural question: Bubble’s plans are described in vague terms, mentioning a number of units that doesn’t really tell you much about how it will afect your app. In Bubble’s defense, referencing their actual hardware is the only thing they can do, since every app is diferent and it’s impossible to predict how the hardware setup will predict your specific scenario.

We can still try to answer the most burning question though: will your app’s performance improve on a more expensive plan?

Somewhat. But not that much.

The simple, boring truth is: if you’re writing angry tweets that your app is slow on the Professional plan, you’re probably going to keep writing angry tweets when you see that it’s still slow on a Dedicated plan.

What you will get is capacity. You can handle more users, more recursive worklows without timing out and larger file imports. Will it not afect speed at all? Yes, it will. But it’s not going to turn a wooden cart into a Ferrari. Don’t make that investment unless you need it to handle a big user base or unavoidably perform consistently heavy server workloads, and keep in mind that the realistic diference is measured in milliseconds.

For a startup or most apps in general, that’s simply not worth the added hosting cost. A dedicated server is one thing you can do to speed up your app, not the thing.



## Knowing the platform

**Getting to know Bubble, and determining whether it's right for your project**

### The research phase

Bubble is a fantastic tool. A game-changer. It may just end up powering a large portion of the web in the years to come.
You know another tool that’s great? A hammer. But I wouldn’t use a hammer to eat spaghetti, and I wouldn’t use a fork to hammer in a nail. And none of them will help me build the next Facebook.

Researching what tools to use may end up being your project’s most important decision, and you’re probably gonna make thousands of those in the coming months. So the first thing we're going to look at is how to determine whether Bubble is the right tool for your project.

**The tool for your project**

Can I scale with Bubble? is a typical question I get. The question makes perfect sense, and no sense at all. What does your app do? If your app handles purely client-side actions, you can handle hundreds of millions of users. It’s also very easy to set up an app that cannot even handle the one user it has, by having that user start some impossibly complex worklows. So where does your app fall on the scale?

Luckily, you have a fantastic resource available: the no-code community. And if you’re polite and describe your question well, you’ll get the most amazingly detailed and thought out responses.

So get the question right.

Whether Bubble is “good” or not has been asked countless times online. And the worst part isn’t that you won’t get a response. The worst part is that you will. People will tell you that it’s great. They’ll tell you that it sucks. They’ll tell you that their production app has been running smoothly for five years. They’ll tell you that their app couldn’t even handle five users before slowing down, and Bubble is hopeless. They’ll tell you that Customer Service is amazing, and they’ll tell you that it’s a fraud. Any answer to a vague question you ask is likely to simply relect the current emotional state of the respondent as they are succeeding or struggling in their own project.
What you need to ask is not whether Bubble is a good tool. What you need to ask is if it is the right tool for your project.

**Asking the right questions**

Describe your app and what you want it to do. Take a look at the examples below. These are both apps that could be built on Bubble, but they are very diferent projects and can trigger equally diferent responses when you ask experienced users for advice.

By describing your app with this level of detail, you’ll be able to shed light on important strengths and weaknesses before you start developing,

[
**My app needs**
- To serve about 5000 clients per day
- Shopping cart
- Efficient product search
- Great SEO performance
- Work with Google Data Studio

**My app needs**
- Two-way 4k video streaming
- Push notifications
- Screen recording on mobile
- Send and play audio snippets
- Chat
]

Look at it this way: there’s nothing worse than working on a project for two months, only to discover that the platform you’re using doesn’t support a key feature you need.

As we’ve already seen, performance and capacity can mean very diferent things to diferent projects: try to highlight what kind of performance you are actually looking for. Loading a page quickly and making changes on thousands of database entries are not the same thing. Scaling means nothing if we don’t know exactly what you’re scaling: number of users? Number of worklows? Number of products?

Put your questions out there – on the forum, on Twitter, in Slack channels. You’ll be amazed at how much you can learn in a few hours. I guarantee the time is worth the investment.



### Understanding Bubble’s capacity dilemma

Bubble is a walled garden. You can use it for whatever creative endeavor you want, but you can never leave, and you can’t change how Bubble performs its actions. While you celebrate new Bubble features, some of the most important work they do is going on under the hood, making sure that hundreds of thousands of applications have 99,9% uptime, stable performance and industry standard security. Now, while this deserves applause in itself, when you’re launching your new SaaS MVP on ProductHunt, you don’t really care about handing out gold medals – you care that it works. But bear with me, because understanding the thought process that led to Bubble becoming what it is, is helpful when you make your own decisions in app design.

To make a long story short, when it comes to capacity, Bubble is focused on two things:

• Making sure that one app can't mess up the capacity of everyone else's app
• Making sure that users don't mess up their own apps

No matter what kind of hardware beast you have for a server, running it into the ground is very easy. Create a worklow. Loop it with no delay and no end. Watch the server crash and burn. Educated, experienced developers sometimes do this by mistake. Inexperienced, technically uneducated Bubble developers, let to their own devices, would crash every Bubble server before lunch.


So what do Bubble do? They place a lot of safeguards that stop this from happening. If you’ve been Bubbling for a while, you’ll know that Bubble chooses stability over functionality any day, and then slowly lifts restrictions over time as they have proved to work stably. Recursive workflows (which is just a fancy term for loop) was blocked until 2019, even though it’s a cornerstone of programming, because there was a risk that any of the thousands of workflows created every day would run amok and max out everyone’s capacity. User’s trust in the platform is a fragile thing, and frequent downtime would rightly scare users away: so Bubble stays on the safe side.

Flexibility comes at the cost of Bubble sometimes needing to protect users from themselves. On dedicated servers, the restrictions are less strict, but I can tell from experience that sending a dedicated server to 100% cpu usage is something you can easily do with a simple typo. The opening up of running workflows without delay doesn’t mean that you can run them without delay: just that Bubble won’t stop you from trying.

So, as you can see, Bubble makes a lot of decisions for you, and you don’t have a say in that process. For good reason, when we bring hundreds of thousands of apps into the mix. One of the downsides of a closed system is that when you reach its limitations, there’s not much you can do to expand them. What you see is what you get.

Still, for a visual programming system, Bubble is mindboggingly flexible, and there are plenty of things you can do both to mess up and optimize your app for performance.

**A jack of all trades**

Another point worth bringing up is that Bubble is a system that allows you to create almost any kind of database-driven web application. This kind of flexibility means that the platform has to be great at a lot of things - not just one.
Algolia is great at fast indexing and searching. Parabola is great at making sense of complex data. Looker is great for aggregating analytics. Zapier is awesome for visualizing automations between different online services. They’re all better at the slim field in which they operate - but Bubble can do most of the things that they can and lots more.

Flexibility comes at a cost that’s two-fold: 1) you can’t expect Bubble to be the best available platform for every thinkable feature out of the box, and 2) even if Bubble is easy to use, creating efficient apps takes experience and creative thinking, just like any other programming language.

**Bubble’s history of performance**

At the time of writing this, I’ve been Bubbling full time for five years, and I can tell you: there have not been many a-ha moments where Bubble’s performance suddenly increased noticeably from one day to the next. But boy, is the platform a lot faster than

it was five years ago. The first app I ever built was a mobile e-commerce platform. From a performance perspective, my work was horrible of course, but Bubble’s performance in general at the time was painful. Simple database changes could take several seconds to complete. Making changes on a list would freeze the system for ten seconds. Whenever I demoed something, I prayed to higher powers to not bring up the top loading bar of death. Several times per day, the app didn’t load at all and I frantically messaged Bubble’s support channels while wiping the sweat from my forehead in an investor meeting.

Over time, slowly and gradually, it has improved a great deal. Many of the changes are precisely things that this guide teaches: Bubble now seems to render changes to the screen before the database processing is actually finished, for example. You can see this whenever you use the Make changes on a list action: the results seem instant and users are happy: they changed the visible layer while the layer underneath may just be the same.

It won’t stop there of course - Bubble will keep improving the performance of their core features, and hopefully, some of the advice given in this guide will over time become redundant. Other parts never will: Bubble’s flexibility gives you the opportunity to build the next big app - but also to set up an inefficient resource hog. It’s your job to learn how to avoid the latter.


**Bubble official documentation and guides**

Bubble focuses on ease of use, because they want anyone to be able to build an app. It’s not hard to understand their perspective: the low learning curve and ease of entry means more apps actually hit the market instead of getting stuck in a development quagmire.

The downside is that while the official documentation will help you set up an app that works, it doesn’t necessarily promote best practices for performance. Since most developers have learned Bubble studying the documentation and each other, methods that are not very well optimized are still used by a majority of users, including professional agencies. Several lessons in this book take a different or even contradictory approach to what Bubble’s documentation recommends.

That’s not to say Bubble’s approach is wrong and this book is right. Development is a game of compromises: deviating from Bubble’s documentation can have a great effect on your app’s performance and scalability, but sometimes it comes with the cost of extending development time or requiring maintenance.


**Bubble performance vs. device performance**

An app can slow down for all sorts of reasons, and many of them are not actually related to Bubble. Remember the terms client-side and server-side that we discussed earlier? Let’s bring some more detail into it.


  graph TD
      Performance --> Client
      Performance --> Server

      Client --> RAM_usage[RAM usage]
      RAM_usage -->|Affects:| Frame_rate[Frame rate (sluggishness)]
      RAM_usage -->|Affects:| Responsiveness
      RAM_usage -->|Affects:| Can_lead_to_browser_freezing[Can lead to browser freezing]

      Client --> CPU_usage[CPU usage]
      CPU_usage -->|Affects:| Frame_rate2[Frame rate (sluggishness)]
      CPU_usage -->|Affects:| Responsiveness2[Responsiveness]
      CPU_usage -->|Affects:| Can_lead_to_browser_freezing2[Can lead to browser freezing]

      Client --> Download_size[Download size]
      Download_size -->|Affects:| Initial_page_load[Initial page load]
      Download_size -->|Affects:| RAM_usage2[RAM usage]

      Server --> Searches
      Server --> Conditions
      Server --> Workflows
      Workflows --> Engine

The chart above shows our two columns of performance. We’ll focus on the left side for now, marked in **blue**. The points in this section are all factors that can slow down your app, but they are unrelated to Bubble as a platform: they would slow down your app no matter what system they were built with.


**RAM usage**

Everything that you add to your application will be stored in the memory of the user’s device after it has been downloaded, and can start slowing things down if it grows too big. Bubble contributes a bit with the engine and other resources required to run a Bubble app, and everything a ter that is up to you. The table below shows an unscientific snapshot of the current RAM usage of a few different pages:

| Page                         | RAM usage in MB |
|------------------------------|-----------------|
| Blank html file              | 1.3             |
| Blank Bubble page            | 6               |
| Complex one-page Bubble app  | 135             |
| Facebook                     | 420             |



As you can see, Bubble is not a particularly poor performer when it comes to memory usage. Continued use of a page (as you keep loading new lists and Things) will be added on top of the already spent RAM. As Facebook shows, adding lots of high-res photos puts a higher strain on the user’s device.

Adding to the total RAM spent will also add to the total CPU spent, as the user’s processor will have more data to work with when scrolling and navigating the page.


**CPU usage**

Everything that is calculated client-side will use the CPU on your user’s device. The CPU is used to render the look of the page (including fancy stuff like drop shadows, transparency and animations) and to perform calculations to your data that are applied after the data has been received from the Bubble server. For example, in the search below, the Search for Users with all of its conditions will be performed server-side, and the filtered and count will be performed client-side.

  `Search for Users:filtered:count`

The :count in this case happens client-side instead of on the server, since the client-side constraint :filtered is applied first.

This can be used to great effect to speed up your app, as we’ll explore later, but it can also slow it down substantially if you use it in the wrong way or fail to predict how your app will scale. You’ll also have to take into account that the user might be using a less powerful device than your own, such as an old computer or a cell phone/tablet.

**Download size**

The download size is the total amount of data that has to be downloaded before and while your app is used. High-resolution images, fonts, illustrations, video and sound files will make your page load slower, increase the RAM and CPU usage and punish your SEO score.

### Bubble’s servers and Cloudflare

In October of 2019, Bubble introduced the new Cloudflare integration. You may already be familiar with the term Content Delivery Network, or CDN, and this provided a very welcome boost to the performance of Bubble apps globally.
As we saw in an earlier chart, information has to travel repeatedly between the server and your device, and the distance between the two creates a delay. The purpose of a CDN is to intelligently and automatically spread information out on different servers across the globe, so that the distance between your device and the server is as short as possible.

Great! So if I’m in Australia and need to load a Bubble page, the info will now come from a server close by?

Yes. But also no.

Your Bubble app in simplified terms depends on three things to function:

• Assets (files like the Bubble code base, images, fonts, css stylesheets, etc)
• The database (for retrieving and storing information)
• The Bubble engine (the engine that actually processes requests on the server)

Since the database and the Bubble engine always need to stay in sync, they can’t be spread out across different server locations. So while the CDN can speed up the fetching of files and other assets, it doesn’t shorten the distance between the device and Bubble’s actual database and engine.

Everytime you interact with the database or send a workflow to Bubble, you are communicating with the Bubble server, and not the CDN.







Bubble’s performance limitations

Now that we know there are a number of non-Bubble factors that can contribute to an app slowing down, let’s talk about what kind of limitations you may run into with Bubble.

What the issues below have in common is that they will be challenging in any platform you choose. But with Bubble, being a locked system, you may find yourself in a situation where you’re unable to make improvements in specific areas. The upside is that you don’t have to pay for performance improvements that Bubble invests in - the downside is that you don’t have a say in what those investments are.

Manipulating large data sets quickly

Bubble is generally not optimized for rapidly manipulating data sets that exceed a thousand records. This doesn’t mean that a Bubble app can’t handle databases that are much larger than that, but if a main feature of your planned app is to frequently and quickly iterate on entries numbering in the thousands or more, you may find Bubble to be too slow. The best way to make changes on 1.000+ records is to use recursive workflows, and you’ll need to experiment to see how long a delay you need between each loop to keep the system from reaching its limits. Depending of course on the complexity of the workflow being performed, most workflows will need a second or more in-between, quickly pushing operations on 1.000 records to take about 15 minutes to complete.

Working visually with long lists of records

Using repeating groups to display a list of 50-100 things will work just fine in Bubble, but once you reach a few hundred entries displayed on the screen at once, you may start experiencing slowdowns (depending on the elements you have in your group of course). Apps like a Google spreadsheet are optimized for displaying potentially huge amounts of data on the screen at the same time, but trying to do the same with Bubble would have the browser struggling as the number of DOM elements would be too high.

Complex searches

Searching for records in the database with simple criteria like Product name or Published=true is quick and stable. More advanced searches are not always readily available without setting up a complex scheme of merging and intersecting multiple searches into one list. Not only does this force the server to perform multiple searches, but can also lead to moving parts of the processing client-side, slowing down searches with a lot of entries.
 48

 
Server-side Javascript
Bubble opened up for running Javascript server-side about a year back, and it was a welcome addition for both Bubble developers and plugin creators. Alas, so far, what we’ve been seeing is that it can lead to delays stretching over several seconds for even minor calculations. This will likely improve over time.
Loading UX
A specifically challenging thing about working with performance and UX in Bubble is that we have no clear way to tell when the page is really finished loading. Bubble can let us know when all the data is finished loading with the Page loaded (entire) condition, but personally I find the labeling to be somewhat misleading, as the page is not necessarily finished rendering, even if Bubble has finished downloading the data.

This is obviously not an exhaustive list, but simply relevant points to bring up when discussing performance. In the end, what you need to do for your app is to ask the questions

● WhatdoImeanwhenIsayperformance?
● Isthatamainfeatureofmyapplication?

Only by defining clearly what kind of performance you are looking for and how important that is for your app can you determine whether Bubble will meet your criteria or not.

How Bubble’s database works

Bubble’s database is built on SQL (Structured Query Language), which is a language widely used for managing data stored in a relational database. As many web standards, it has a longer history than many realize: databases were a thing long before the internet after all.
In the 1960’s, the first computer databases were being developed, and the structured storage and retrieval of data was considered a very important field at the time. After all, the world had gone through a second world war in which the power of computers had a major impact: Alan Turing and his team being able to decrypt German communication with a computer gave the Allies an advantage that turned out to shape world history. The war had cemented the US as the world’s major superpower and the cold war was on everyone’s mind: spies and their data were considered so important and cool, we’re still releasing James Bond movies 60 years later. All that intel they gathered needed to be saved and searchable somehow and information startet to move from paper archives to databases.

Traditionally, the databases were built like hierarchies, where the database segments are bound together in a parent/child relationship where each parent record can have many children, but each child record can only have one parent, kind of like the folders on your computer . This is known as a one-to-many relationship.

This way of thinking changed in 1970 when Edgar Frank Codd, an English computer scientist at IBM, released his paper A Relational Model of Data for Large Shared Data Banks. Codd’s idea was to make databases more  lexible by allowing many-to-many relationships. He  lattened the traditional tree structure and instead suggested that records can be related to each other. Each record in the database has a unique identifier (a primary key) that never changes, and by referencing that key elsewhere (at which point it’s called a foreign key), we can give each record a relationship with one or more other records, without any hierarchy needed. In Bubble the Unique ID field is a record’s primary key.

In some ways, Bubble has taken the relational database model one step further by removing the need to understand primary and foreign keys. In Bubble, database relations are set up in a visual way where the foreign key is hidden and you can choose which field to display using the Primary fields setting.

 
For users with no database experience, this feels intuitive, but for new Bubblers who have spent some time with databases before, the lack of foreign keys can be confusing. What’s important to note here is that this is purely a visual change.

Under the hood, Bubble’s database works like any other relational database, using a foreign key to reference the primary key of another record. Using the primary key setting simply tells Bubble what field to show you - it doesn’t actually change the underlying foreign key. Saving a list of Things is done in the same way, by simply saving a list of Unique ID’s - the data saved on those Things still has to be fetched from the foreign record.

The relational database model and SQL language allow for  lexible queries where you can search your database with clear and understandable constraints. The example below could easily be translated into a humanly readable sentence like “Search for Users who’s email is mail@example.com”

Understanding indexing

It could be argued that SQL databases are inherently slow, and it would be partially true. Like most computer-related issues, the efficiency of a database hasn’t improved simply because hardware has become more powerful. It has also improved massively because thousands of developers have spent decades building better ways of working with large databases efficiently. An important part of fast queries is the use of indexing. Indexes have one purpose - t0 make a query fast. A common misunderstanding is that an index is a kind of “saved query result” in which Bubble takes common queries and simply saves the result as a list of records that can be quickly sent over when a similar search is made. But this is not quite how indexing works.

Indexes actually have more to do with how data is sorted than anything else, and like many points in this book, it’s a game of compromise. The easiest way to visualize a database is like a spreadsheet. Now, let’s assume you’ve added a lot of users to it with email, name and age. They’ve been added as the need came up, so your spreadsheet would be in a random order: that’s the database with no indices.

To make efficient use of that spreadsheet you would likely sort it by last name; that’s an index. Both searching and sorting for a row by name is now a lot faster, because you don’t need to read the whole spreadsheet - you can do a binary search where you narrow in the name you’re looking for. Technically, this can be done on a sorted list by repeatedly dividing the search interval in half, beginning with the full list. If the value of the search constraint is less than the middle item in the interval, you can narrow the interval to the lower half - otherwise, narrow it to the upper half. In a single step, you’ve reduced the number of records to search through by 50%, and you can repeat this process several times to drastically reduce the searchable data.

Now, that’s great if all you need to do is search by name. But what if you want to search by age? That means the name sorting isn’t helpful anymore, and we’ll need to sort everyone by their age instead - and that requires a new, separate index. This way of using sorting to quickly rule out huge parts of the database in a query is  lexible enough to support multiple columns, like sorting by name and then age to use the same method of elimination, but each index requires the database to create and maintain copies of the same data.

Herein lies the compromise: creating an index sorted in a specific way makes the query faster, but it also takes up server space and resources. You don’t need to copy the whole database for each index - only the columns needed - but for every copy you add the time and resources needed to create, edit and delete records grows, potentially slowing those actions down and increasing the server costs.

How Bubble chooses what to index

With that understanding of indices in mind, Bubble needs to set up a system of rules for what queries “deserve” to be indexed. First, they look at the app database overall: if the app consists of just a few hundred records, then a custom sorting won’t speed up the search in any meaningful way.
Then, the system starts to empirically detect queries that are not performing well. At the time of writing this, a query is considered slow if it repeatedly takes more than 20ms to complete over the course of an hour. It then analyzes whether an index would actually help speed it up, and creates one if it does and one doesn’t exist. Behind the scenes, Bubble uses PostgreSQL, an open source system that has been in development for more than thirty years and is the second most widely used database management system in the world after MySQL according to a 2019 Stackoverflow survey.

How indices work on your app

As indices are built by demand, not by default, you can see a variation in query speed over time. Queries that were slow at one point may become faster as they fulfil the requirements for setting up a separate index. Ironically, that logic can also mean that an app with more users can actually perform faster queries, since the increased search volume pushes Bubble to structure the database towards faster queries. Keep in mind the first rule of Bubble’s indexing: it only happens on apps with substantial amounts of data.

Structured and unstructured data

Information can be stored in two different types of systems: structured and unstructured. This is not a Bubble-specific definition, but a general way to think about the storage of information.
Structured data means it is organized into a catalogue system where each piece of information has consistent content and labelling. A spreadsheet is an obvious example. Each cell can only contain a certain type of information labelled by its row and column. Another one is the contact list in your phone, where fields like first name, last name and email never change. From the perspective of a computer, this data is easy to sort, search through and aggregate, and structured data sets are typically lightweight, since they only contain short strings and numbers.

Unstructured data is information stored in a format that would be harder to understand for a computer, such as a Word document, a written note or book page. Unstructured data is more difficult to catalog and search through and can grow unpredictably in download size since its content can take whichever form the user gives it.

Bubble databases will typically consist of a mix between the two: structured data records containing unstructured fields. For example, on a Product, you may want to have a field called Description, or if you build a blog, your blog post record will surely contain the content of the post itself in HTML or another format.

Thinking about database records in terms of structured and unstructured data is helpful when planning your database for fast searching.

How a page is loaded

Page load sequence

As a page is loaded, Bubble goes through a sequence of steps to prepare it and share information with the browser.
1. First, the server looks up information on the Current User and current Page Thing. Then, it generates the page HTML and sends it along with that data.
 57

 
2. ThepageHTMLincludesreferencestoseveraljavascriptfiles.Thesecurrently load synchronously, meaning that they have to finish before the browser renders the page. That said, most modern browsers will do the download of those files in parallel.
3. Allelementsarethendrawnonthepagehierarchically,startingwiththepage and working through its children. This happens in a single (sometimes long for big pages) “tick” of the client javascript engine and the elements render all at once. A lot of work for rendering invisible elements is deferred until they become invisible, but there is some overhead in this initial pass. At this stage, repeating groups are considered single-celled.
4. Imagesdisplayedbyelementsstartdownloading,andanydatafetches necessary to render the elements start
5. Thecontentofrepeatinggroupsarerendered(repeatingsteps3-5)
   
How the page is rendered by the browsers

As your browser renders the page, it goes through a series of predictable steps. These steps are not determined by Bubble, but by the browser and the HTML and CSS frameworks.

● DownloadandparsetheHTMLandCSS
● Applystylestoallelements
● Calculatelayout(dimensionsandpositionsofelements)
● Paintallelementsonthescreen
● Compositing(combinealllayersintoacompositedimage-whatyouseeonthe
screen)

As we discussed in the previous section, Bubble generates the HTML on the server and sends it to the browser. Modern web browsers use an interface called the Document Object Model, or DOM. This is basically a tree-structure where every branch ends in a node, which contains an object. An object is any part of your page structure: the html itself, the page’s header, the page’s body, a group, a text... you name it. Everything that you place on the page is an object contained within the body element.

 
The example above shows a page that contains a single group with one text object and one image object inside of it. The hierarchical structure represents the page as you’ve designed it in the visual editor.

Each of these elements need some sort of styling (the color, border, padding, font size etc), and the first thing the browser does is to apply the style to each element. The reason this is the first step, is that the browser next needs to calculate how much space each element needs and where to place it. Several properties affect the layout:
- Width
- Height
- Margin
- Padding
- Placement coordinates
- 
Bubble elements are positioned absolutely, using X and Y coordinates that tell the browser where to render it relative to its parent. It takes the information from the previous steps and moves on to the paint step. If you’re familiar working with software like Photoshop and Illustrator, you might recognize the terms vector and rasterizing - the browser takes the vector boxes (the type and style information stored in each element) and rasterizes them (turns them into actual pixels to be displayed on the screen).

In the final step, the browser turns all the layers on your page into a single image that’s displayed on the screen.

Repaints

When something changes on the screen (by hiding/showing or animating an element for example), the browser may need to repaint certain areas. Repaints are done in layers and will usually be applied only to the parts of the screen that are affected by the change. Depending on the device and User’s browser settings, this is usually handled by the GPU, which means in most cases it’s very fast.

     Later in the book, we’ll explore how you can measure how elements and rendering affect the performance of your app. If you’d like to jump right into that section now, click here.
Don’t worry, there’s a link there too that will take you right back there.

   Priority of general event workflows and page load

There is no definite order of sequence of general events (as opposed to element-dependent workflows like a button click), but they’re related to the sequence in which the page loads as described in the steps above. The descriptions below provide a general understanding of how they are triggered:
Page is loaded

The Page is loaded Event triggers as soon as the page is finished rendering (as described in step 3).

Current User is logged out

This workflow is triggered as soon as the status can be determined, and is expected to finish before the page is rendered. It’s important to note that it doesn’t stop the page from rendering - just that the workflow will be triggered. So information can be rendered on the page before the workflow can have any meaningful impact (such as navigating to a different page).

Do every X seconds

This workflow is executed as soon as it’s recognized by the Bubble engine, which happens during step 2. It’s useful to note that the first step also adds an X second delay, meaning that if it’s set to run every 2 seconds, it will wait 2 seconds before triggering even the first time.
Do when condition is true


This one will run as soon as all the data needed to generate a true value are loaded.
While these may seem like predictable rules, it’s important to remember that the sequence in which they run can vary depending on your browser, connection, device and changes in Bubble’s codebase. They’re a useful guide to understand the general logic of how workflows are triggered, but should not be considered permanent, sequential rules.


Workflow sequence priority: server-side

Bubble enforces that workflows wait for any actions in other workflows to finish server-side that had already ran client-side prior to the workflow being kicked off: in other words, if Workflow A has a “Change Thing” action, and that “Change Thing” action runs client-side, then Workflow B starts client-side, Bubble makes sure that the “Change Thing” action from workflow A finishes server-side before any actions in Workflow B run server-side.

This is to ensure consistency between client-side and server-side execution and make sure both sides perform actions in the right order. In cases where you place a lot of workflows in one place (if you have a lot of actions running on page load for example) a queue can pile up on the server that creates a slowdown. Whether this is noticeable by the end user depends on what the workflows actually do, but it’s worth keeping in mind that it can create spikes in your overall capacity.

Workflow sequence priority: client-side

The same logic doesn’t always apply for actions on the client-side. Bubble will focus on finishing as quickly as it can without sacrificing consistency. Actions do execute in the order you have provided in the workflow, but they don’t necessarily wait for the last step to finish before moving on to the next. If it relies on information from a previous step (such as when you reference a Thing from Result of step X), it will wait for it to finish.
This logic can sometimes create challenges if you expect all steps to actually complete their action before moving on. If one action uses the Go to page action to change a URL parameter and a later step references that new parameter for example, it may not actually have time to keep up and the later step will find an old or empty parameter instead of the expected one. The same can happen if a later step depends on a search that includes a Thing created/changed in a previous step - you should reference that step directly instead of relying on a search since there’s no guarantee that the previous database operation has finished before the search starts.

Both of these sequence inconsistencies can be avoided by placing the latter step in a custom event that’s scheduled to run a little bit later, but making sure to tell Bubble to wait until a step has finished (by using Result of Step X for example is a safer and usually faster method).

Custom events

Custom events always run sequentially, meaning that Bubble will complete all actions in the Custom Event before moving on to the next action in the workflow that triggered it. So If Workflow A runs a custom event that starts Workflow B, Workflow B will complete before the remaining actions in Workflow A run.

This means that you can use Custom Events as a safeguard against inconsistencies in database operations, like in the example below with back-end workflows.

Back-end workflows/API workflows

Scheduling Back-end workflows (or API workflows) works differently triggering on-page actions: unless they rely on a previous step, they are triggered as soon as the workflow is triggered. In other words, their place in the sequence of steps is actually irrelevant unless they rely on a condition or reference from previous steps. This is important in several scenarios where database operations may not have had time to finish before the back-end workflow starts, and it can cause inconsistencies. To get around this, you can place the Schedule API workflow action in a Custom Event placed as the last step in the previous workflow.

If you schedule several Back-end workflows by using the Schedule API workflow on a list action, they will all run in parallel, not sequentially. In other words, one workflow instance will not wait for another to finish or even start. Once scheduled, they are completely separate from each other.


How Bubble determines that the page is finished loading
Page loaded (entire)
Two criteria are needed for the Page loaded to be returned as true:
1. Every visible element’s properties are known and not waiting on loading data. If
an element’s property contains a Do a Search for... for instance, that search must
be complete before the element is considered done loading
1. Everyvisibleelementthathaschildrenhasdrawnthosechildren.Inother
words, a Repeating Group needs to
a. Completethesearchthatloadstheinitialdata
b. Drawitsinitialsetofchildcells(initialmeaningthenumberofrecordsits
set to display)
Page loaded (entire) currently does not take into account assets loaded by the browser (like images) - but focuses on things that depend on Bubble code.

Page loaded (above fold)

Above the fold basically means everything that is visible on the screen as the page loads. In other words, anything that the user needs to scroll to is considered below the fold. This will return yes using the same conditions as above, except that it only takes into consideration the elements that are actually visible to the user.


 
Client-side vs server-side operators

The table below shows where a Bubble expression operator takes place.

**Operations and How They Happen**

| **Operation**        | **How it happens**                            |
| -------------------- | --------------------------------------------- |
| Do a Search for:count | Server-side (returning number)                |
| Do a Search for:first item | Server-side (returning 1 item)            |
| Do a Search for:random item | Server-side (returning 1 item)          |
| Do a Search for:filtered | Regular constraints performed on the server, advanced filters performed on the client-side |
| Do a Search for:sorted | Server-side, as long as Bubble can fit it into one query |
| Do a Search for:Group by | Server-side                               |
| Do a Search for:merge with | Client-side, though this is efficient: if you're displaying the list in a repeating group and showing the first 10 items, Bubble just needs the first 10 items from the first search, and doesn't start loading data from the second search until the first search is exhausted |
| Do a Search for:intersect with | Client-side, with same comments as above, although intersection generally requires loading more data, making this expansive easily |


How to build for performance

Structuring your app and database for top performance


Now for the interesting stuff: how to set up your app for performance. Let’s return to our chart of what slowdowns are caused by:

 Every decision you make in the coming weeks of development will affect your app’s performance in some way, and they’ll all be connected to one of the boxes above. So let’s go through each one.


The Page

RAM usage and download size

The RAM is the working memory of your user’s device and is used by the device’s processor to temporarily store information. The reason you can switch quickly between apps and websites, is that all the content of the site or app is saved in the RAM for quick retrieval. The RAM is fast - very fast - but a finite resource. When all the space has been used, your operating system will start using the device’s hard drive to temporarily store information instead, and you’ll start noticing your system slowing down.
When you load a Bubble page, a range of different resources are downloaded from a server to your computer, and stored in the device’s RAM:
● TheBubbleengine
● Imagesandothermediafiles
● Fonts
● Iconpacks
● Javascriptlibraries
● CSS
● Pagedesign(elementsonyourpage)
● Yourapplogic:conditionsandworkflows


The more you ask the browser to store in device memory, the more processing power is needed to render elements on the page. So even if you’re not spending all available memory, adding more information into the pile will make its wheels turn slower.

How small should a website be?

What kind of app you’re building needs to be taken into consideration: for example, an e-commerce website that relies on SEO performance will need to be lightweight, whereas it may not be as important for a business app. Generally though, if the total download size of your page exceeds 6 megabytes, you’re on the heavier side. At around 8-10 megabytes, your SEO ranking will start to suffer and users will start to notice. Keep 2-4 megabytes as your goal, but know that there can be perfectly valid reasons to exceed that size.

Downloads

The Bubble engine

The Bubble engine is the codebase that your app is running on. This is Bubble’s secret sauce, and there’s not much you can do about its size. The good news is that it’s pretty lightweight, and that this asset is delivered through the Cloudflare CDN.


 
Images

Images are also downloaded through Cloudflare. Four simple rules should guide your use of images:

● Don’tusethem
Simple enough. The most efficient use of images is to not use them. Obviously you want to use them sometimes, but keep it minimal. Using images in Repeating Groups for example, can quickly add several megabytes to the page size.
● Enablecompression
Whether you use Photoshop or something else, your export settings can dramatically affect how large the file ends up. I take all images through two steps:
1) Compress in Photoshop: I’ve found most images can take about 40% compression before they start to look bad, depending on the image. Experiment a bit and find the right balance between size and quality.
2) Next, run the image through www.tinypng.com. Despite the name, the service also handles JPG’s just fine, and can reduce the file size of your images considerably, without any loss of quality.

● Usetherightformat

There’s no right and wrong when it comes to picking the file format of your images, as long as it’s supported by the major browsers. Generally, you have three options: JPG, PNG and SVG.
The last one is a vector format, which means you can’t use it for photos. The good thing about vector images is that they can be scaled to any size with no loss of quality. Use this for logos and illustrations: often you’ll find that the file size can be a lot smaller than a bitmap image, and you can use it in different sizes across your app without having to upload multiple copies.
● Considerdevicesize
Use conditions to download smaller images on smaller screens. There’s no reason to download a desktop size background image to a mobile device.
Fonts
Every font that you use in your app, even if only used in one place, needs to be downloaded and stored in memory, so keep it to a minimum. Preferably, use just one font. The file size for most fonts varies between 100 to 200 kb.

Icon packs

Icon packs behave much like fonts: they’re not downloaded individually, letter by letter, but as a package containing all the icons. In other words, it makes sense to pick one icon collection and stick with it, rather than picking from different libraries.

Javascript libraries (plugins)

A lot of Bubble plugins depend on a Javascript library, which is a fancy term for re-using code. For example, there are millions of image sliders on different websites, and each website builder didn’t code their own slider, but relied on the code that someone else already wrote. So, a library is simply a JavaScript file that adds some functionality to your website, ranging from calendars to image editing to chat windows to analytics. Each one has to be downloaded and stored in memory to work, adding slightly to the total download.

Here, we also touch upon another important metric to optimize app performance: the number of server requests that are made from a page. Libraries that add functionality to your page will not usually be stored on your Bubble server. In other words, the browser has to connect to a different server to download the file. The total number of requests that your app has to make to different servers not only affects your app’s performance, but can also degrade your SEO score. When using an external library, you’re at the mercy of a third-party: there’s of course no denying that it can sometimes add great value to your app, but as everything else it comes at a cost: keep it minimal.


 
CSS (styles)

CSS in Bubble terms is called Styles. It dictates what your elements look like. Using Styles is to save the information once instead of repeating it, meaning for example that you only have to define what a certain type of button should look like once, and then re-use that style for every button in your app. This is not just a timesaver for you as a developer but also a performance trick: imagine placing fifty text elements on a page (easily done with a repeating group for example). Without styles, you would have to load the style setting for each of those elements - fifty times in total. With styles, you’ll load it just once, and then apply it to all of the fifty elements.
Measuring the size of the page and all assets
Popular web browsers include tools that can provide you with detailed information about your page total download size, as well as the isolated size and download time of different assets on your page. Run the test in a fresh Private Window (Firefox) or Incognito Mode (Chrome) as ad blockers/other extensions and cached assets can skew your results.

● Firefox:Atthetimeofwriting,you’llfinddownloaddetailsunderTools->Web Developer -> Network
● Chrome:GotoView-Developer->DeveloperToolsandclicktheNetworktab.

 Let’s look at how the Network tab can help us identify some culprits in a random Bubble app. We’re going to use Chrome for this example:

For Chrome to record the network activity, the Developer Tools need to be open. Click the Network Tab.

To measure the download size, make sure to hold the mouse button over the reload and hold the mouse button to expose the menu. Select Empty cache and hard to reload, which tells Chrome to re-download all resources used on your page (as opposed to the files cached from earlier page visits).
Emptying the cache and applying a hard reload gives you the most precise result since it forces Chrome to re-download all assets.
  Chrome will reveal a list of assets downloaded. Sorting by Size by clicking that tab is an easy way to find the biggest assets on the page. Just a quick glance at the network tab in this example reveals that we are downloading three separate icon packages (FontAwesome, Material Icons and Feather Icons, marked in red) totalling about 141 kb - optimally we shouldn’t use more than one to reduce the page size and number of connections. You can also see several JavaScript libraries loaded here: Quill (Rich Text Editor), Moment (used to do calculations on datetimes).
The total download size of this page was 1.8 mb, meaning I could reduce its size by about 15% (220kb) simply by removing some icon packs and plugins (assuming they aren’t used of course). In the world of SEO, 220 kb is not a trivial number, and this was just from spending one minute in the Network tab.
Identifying searches
The network tab can also be used to identify the total download size of a given Do a Search for, helping you measure how well-optimized your database structure is for efficient searching. It’s not unusual that the search itself on Bubble’s servers is performed quickly, but the size of the download still makes it seem slow. Bubble uses Elastic.io for searching, and it’s easily recognizable in the Networks tab as named either search or msearch. The easiest way to single them out in the networks tab is by using the Filter and simply typing search.



 
Using that method, we can quickly see searches that are bloated or that take longer to load:
Here we have four searches on a single page, totalling almost 400 kb and contributing 4,3 seconds to the page load time - pretty significant. If we delayed one or more of those searches to be performed later, we could speed up the initial page load.
      This section is closely related to the guide on how to structure your database to make the search download size smaller. If you’d like to read that now, click here.
Don’t worry, there’s a link there too that will take you right back there.
   Reading the waterfall chart

To the rightmost side in the Networks tab you’ll find the Waterfall chart. This tool may feel a bit overwhelming to read at first, but it’s a very useful way to identify the biggest load speed culprits on your page.
 
Waterfall is such a perfect name for this chart, as it shows the order in which every request on your page was made, and how long it took for it to complete.
This again let’s you with a quick glance identify assets that slow your website down. Keep in mind that the waterfall chart will continue to record requests as you navigate the page, allowing you to find assets that are not fetched on page load.

 
How to identify different types
So, I’ve told you that resources such as fonts, images and plugins can add to your page load time - but what do those resources look like? Let’s identify the usual suspects:

Images

Let’s start with the easiest one: images. You can single out image requests by clicking the Img filter at the top of the network pane.

Plugins

Plugins often rely on a third-party Javascript library that’s usually clearly named. Note that it may not carry the exact name of the plugin - but rather the library it uses. The simplest way to find them is to activate the JS filter (Javascript). Some plugins will also have an accompanying CSS file, so remember to take this asset too into account when you calculate the total size of a plugin. By Command/Control clicking a filter, you can add more than one, as illustrated below.

Among Javascript resources you’ll also find analytical tools if you have them installed - tools like Tag Manager, Google Analytics and Hotjar. While analytics tools can be an incredibly important tool for your website, they do add to your total page size and load time - only keep it around if you’re actually using it.

If you’re unsure of what a specific file actually does, the easiest thing is to simply Google it: usually you’ll recognize a feature in your plugin when you find the accompanying JS library.

Fonts

It’s incredibly easy to add another font to your app without really being aware of it. Simply forgetting to apply a style to an element may mean it has a different font applied than everything else. Web fonts are saved in the compressed Web Open Font Format, carrying the suffix woff2 and can be filtered with the Font filter.

Icon libraries

Icon libraries are saved in the same format as fonts (woff2) and they're especially important to keep an eye on for two reasons: 1) they are usually the biggest font files on your page, and 2) they’re not served by Google Fonts (unlike regular fonts), but are stored on an external CDN, increasing the total number of requests.

The two icon libraries loaded on this page have the biggest download size and longest loading times.

Single-page app versus multi-page app

One of the major decisions you will have to make in Bubble, is whether to build your application as a single-page-app, or as a multi-page app. The first thing I’d like to do here is to pop that balloon: this is not a black-and-white question. As we’ve discussed earlier, the performance of your app is a feature among many others, and as such, it should be optimized in a way that doesn’t blindly prioritize speed.

We have two things to consider here:

● Single-pageappscanbeincrediblyquicktonavigate
● Atsomepoint,theycanbecomebloatedandslowdownthesystem

In other words, setting your app up as a single-page app can be one of the biggest performance boosting decisions you make, but including too much on one page can slow the system down. This is a client-side challenge: it relies on the internet connection and hardware of your users, which means what runs fine on a modern computer may not be running as smoothly on an older cell phone.
It all comes down to user behavior. Which features does the user need frequently, and which can you o  load to another page?
 
You’ll find that other companies compromise to keep their main app page lightweight: the top features of the app are loaded on the main page for quick navigation, but features that are not needed as frequently require a page change. Typical features that are left out of the limelight are app settings, profile settings, help systems/documentation, password recovery, etc.

Take Google again: Gmail, Contacts, Calendar and all other parts of that ecosystem are all stored on separate pages, so that each one of them loads quickly. Features within each app on the other hand, like writing an email or adding an appointment, are available without reloading the page.
 
No matter which Google app you click from Gmail - even Contacts - it will open in a new window. This is not a design  law, but how Google keeps Gmail loading quickly and running smoothly.
Www.booking.com, a page that relies heavily on page load speed as a part of their SEO strategy, keeps the app’s core features (like searching for hotels) within the same page, while less-accessed features and content such as their privacy policy and login form are stored on separate pages.

Rendering lists

We’ve been over the fact that a long list can multiply the total number of elements on your page more than you realize when you’re building your app. Different fields on your data types can also contribute to how fast Bubble is able to render a list in a Repeating Group. There are a few different ways information is usually prepared for rendering:

Info saved directly on the list Thing

This is the fastest way to display information from the database in the list. If you are showing a list of Users, showing their First name (saved on the data type) will generally be very quick.
Example: User ➞ First name (1 step)
Info saved on a Sub-Thing

Forcing Bubble to look up an additional Thing saved on the first Thing will add a slight delay to the process.

Example: User ➞ Company ➞ Company name (2 steps) For every step you add, a bit more time is needed:
User ➞ Company ➞ Parent Company ➞ Name (3 steps) Processing on Sub-Things
A slightly longer delay will be added whenever you ask Bubble to perform some sort of data processing on a Sub-Thing. For example, we might want to know how many Accounts a User is managing:

Example: User ➞ Account list ➞ :count (2 steps + count operator)

Conditions

Conditions can add very little or quite a bit to your loading, depending on what the condition is and how many you have added. Keep in mind again that every condition you add will be multiplied by the number of rows in your list. If the conditions depend on database lookups or Searches, you’re giving Bubble a lot to do for each row.

Setting up fast lists

Lists will load quickly if each row is set up as efficiently as possible. In some cases, optimizing your app to display lists quickly may mean setting up both separata Data Types (Search Data Types) with as few and light fields as possible, and to keep those Things updated “manually”. For example, you may want to save a User’s number of Accounts as a number on the User instead of forcing Bubble to count them every time. You can keep this number up to date using on-page workflows or Back-end Triggers.

The Repeating Group trap

Full load vs partial load

One of the most common mistakes that I see in bloated apps is how a single Repeating Group can drastically increase the number of elements on your page. One of the reasons this mistake is so easy to make is the simple fact that while you’re working on your app, there’s usually not that much data in it. A repeating group may show a few rows and work just fine, but as your app is deployed to the real world and user’s start adding data to it, the Repeating Group suddenly grows into showing hundreds of rows or more. Using pagination is very common across most apps not just to keep the screen from cluttering, but because developers know that loading and displaying too much at the same time can lead to performance degradation.

Let’s take the following scenario: you’ve added one repeating group on your page showing a list of users. Within it there are three text elements: first name, last mail and email address. The first thing your client does after having the app handed over is to import all of his employees into the system: all three hundred of them.

How many elements are on your page now?

The three, innocent text elements you drew have suddenly multiplied into 900. Let’s take the example even further just to illustrate how this can quickly go off the rails: let’s imagine that each of those users have a non-compressed profile picture of 1 MB that’s nicely displayed next to their name on each row. Their combined size is now 300 megabytes and the browser needs to download 300 separate files before it can show the list. And you’re wondering why things are slowing down!
The way to avoid it is of course in planning and compromises. Gmail is not going to render a list of all your 35.000 emails on the screen - just the most recent ones. In any other app you use, you’ll also see that lists are kept short by default, as developers know that a long list will put a higher strain on both the server and the client’s browser. Repeating Groups have a built-in pagination feature, and it’s there for a reason: plan ahead for how much data your app will be displaying in the future.

Hiding by default

This brings us to another broader question: how much info should your app display by default? Hiding elements and lists when they are not immediately needed is not just best practice, but a necessity to keep your app nice and light. Going back to the example above: do we need to load all 300 users when the page is loaded? Do we need to load the profile picture of every user? Do we need to even see a list of users on every page load at all, or could you hide behind an action, such as the clicking of a tab or button:

A simple design choice like hiding a list by default can do a lot for both performance and capacity.
The loading of your page is one event out of many that your users will execute as he uses your app. Not all data needs to be fetched by that first event. Let your users tell you what data they need to see, rather than showing everything by default.
  91

 
Lazy loading

Much in the same way that you can hide lists and other “heavier” elements on your page until the user clicks them, lazy loading is a technique where instead of loading all page content on page load, you load only the parts that are required, and delay the loading of other assets until later. A typical case is to wait for the user to scroll down a page before loading content that is below the typical screen height, or to use continued loading as the user scrolls, like Facebook and Instagram.
Lazy loading can be applied to both elements that take up bandwidth (such as images) and to fetching data (such as Bubble database searches).

CPU usage

The CPU on your user’s device is responsible for processing everything happening in your app after the data has left the Bubble server; rendering the page correctly, making client-side calculations and filtering data.

Rendering the page

All elements on your page are rendered to the screen: basically, the CPU of the user’s device is used by the web browser to calculate what every pixel on your screen should look like at any given time. Adding more complexity to the design means giving the processor more work to do. Think about it like a computer game. Better graphics and more special effects require more processing power. Some devices have the newest graphics cards, some are ten years old.

The total size of a page in the device’s memory is closely linked to its CPU usage. Scrolling a page with a lot of elements puts a higher strain on the processor than scrolling fewer elements. How complex you make your elements adds to this: transparency, drop shadows, gradients and animations all add to the total workload and can make your page seem unresponsive.

Again, take two things into consideration: what kind of device your users may be using (older computers and phones), and how the amount of data in your application increases the processing load. Rendering one single user profile photo is not too demanding on your device, but rendering three hundred of them in a Repeating Group can slow it down.

Web design showcased on https://dribbble.com/ frequently features fancy animations, beautifully soft shadows and other effects, making commercial apps seem bland in comparison. But there’s a reason they go for a more simplistic approach: being lightweight and compatible with all devices trumps looking like a rockstar.

Leveraging client-side data processing

Instead of seeing the user’s hardware as a limitation, let’s see it as a resource that you can use to speed up your page. Knowing what kind of computations happen server-side and what happens client-side let’s you assign tasks between them, and exploit the strengths of each one. Let’s go over a few key facts:

The server:

● Isincrediblypowerfulandcanhandlelargeamountsofdata
● Maybelocatedfaraway,andthedataneedstotraveloveradistanceaddinga
delay to every query
● Hasrestrictionsinplacetomakesureoneappdoesn’tuseupallavailable
capacity
The client device:
● Isnotaspowerfulastheserver:itcanhandleonlyalimitedamountofdata
before slowing down
● Resultsareimmediate,asthedataneverleavesthelocaldevice
● Hasnorestrictions:itwillsimplyusealltheprocessingpoweravailableuntilit
finishes
● Hastorelyontheservertogetthedatainthefirstplace.Itdoesn’tpermanently
store anything.

So, as you can see, making calculations locally instead of passing them on to the server can speed up things a great deal, but it comes with limitations and is not easily scalable.

Let's look at a search in Bubble to determine what’s happening on the server and the device:
 In this example, we’re looking for Users that belong to the same Company as the Current User, and we’re asking for that list to be sorted by the User’s Last name. Everything going on in this window is happening server-side: we tell the server that we’re looking for sorted data based on specific criteria, and the server returns the result to the user’s device.

Now let’s extend the Search a bit:

In this example, everything in the red brackets happens server-side, and everything in the blue brackets happens client-side: we receive a list of Users from the Bubble server, and then apply additional advanced filters to that list, and tell our text element to only show the first five entries. This means our entire list is still downloaded and stored in the device memory, but we’re only showing the first five.

(Note that the illustration above does not cover all scenarios. If you add a :count to the end of a search for example, the actual counting is happening server-side)

It’s common advice to never use client-side filtering, as it will slow down your app. This is only true to some extent. Depending on how you use it, client side filtering can be a lot faster than performing another server-side search, since the data never has to leave the local device. Done right, it’s lightning fast. Done wrong, it’s slow and insecure.
 
Client-side filtering is great for:

● Filteringlistsofdatacontainingnomorethanafewhundreditemsatmost ● Simplefilters:themorecomplexityyouadd,thesloweritbecomes
● Non-sensitivedata
Avoid client-side filtering for:
● Largedatasets
● Sensitivedate:sincethefulllistofdataissenttoyourbrowserbeforethefilters
are applied, the data is not secure
● Complexfiltering:leavetheheavyliftingtotheserver

As an experienced Bubbler, client-side filtering can be used to great effect to speed up your app’s performance, but if you’re just starting out, it’s best summed up with these three words: use with caution.

Measuring page rendering

Everything that you add to a page will add to the total download size and RAM spending on your user’s device, as the browser needs to keep it stored in memory and render it correctly on the screen. It means that for every element and condition you add to your page canvas and every workflow and action you add in the workflow builder, your page becomes a little bit more heavy to handle.

The irony of working with performance from a rendering perspective is that even though it can slow down your page, it’s still fast enough to escape your eyes as it's happening.
Chrome Developer Tools have a truly great set of tools to measure your performance in various ways, including page rendering. Let’s have a look.

Paint  lashing

As we discussed in the section about how the browser renders your page, the process of rendering it as pixels on the screen is called painting. The browser attempts to avoid re-painting the whole screen and only render the parts that it needs to.

     This section is closely related to the guide on how your browser renders your page. If you'd like to repeat that before moving on, click here.
Don’t worry, there’s a link there too that will take you right back there.

 
Paint  lashing tells Chrome to show a brightly colored rectangle around any element that’s being painted or re-painted (rendered for the first time or re-rendered as something changes on the screen). As you load the page for the first time, you’ll see everything  lash in green as the browser paints the whole screen. After that process is done, you’ll be able to identify changes as they are happening.

Since this text element has a When this text is hovered condition that changes its color, Chrome shows that it’s repainted as I hover it with the mouse.

Big layout changes and repaints can be taxing on your performance, which is one reason why Single Page Applications can slow your page down if they’re too massive. Here’s how to access it:

1. Open Chrome Developer Tools
2. Whenopen,clickCommand+Option+P(Mac)orControl+Shift+P(PC)toopen
the Command menu.
1. TypeinRenderingtopopentheRenderingdrawer
2. ChecktheboxthatsaysPaintflashing
3. Reloadyourpageandwatchhoweachelementflashes.Asyouhover,clickand
navigate around, you’ll see every paint clearly

 
Checking Layers

As we’ve also explored, your app page consists of layers - this is how the browsers knows how the elements on your page should overlap. Chrome also has a built-in tool that lets you look at all the layers on your page and even rotate it to see it in a 3D
environment.

The Layers tab lets you rotate your page in 3D to see how layers are rendered.
Hovering a layer in the layer tab highlights the corresponding section of the page. An interesting feature of this tab is that you can click a specific layer to check its Memory estimate. A quick test on the page illustrated above shows that Bubble’s debugging bar takes up about 450kb of system memory, whereas the main window that contains a Repeating Group with a list of Users takes up 9MB - a nice reminder of how Repeating Groups can greatly increase memory usage (although the 9 MB’s in this case is not too bad).

 
To access it:
1. Open Chrome Developer Tools
2. Whenopen,clickCommand+Option+P(Mac)orControl+Shift+P(PC)toopen
the Command menu.
1. TypeinLayersandclickthePanel:ShowLayersoption
To navigate in 3D, click the rotate button.

Measuring the frame rate

The frame rate tells you how many times per second your screen updates per second, measured in FPS (Frames Per Second). How many frames per second your screen is able to render depends on how complex the page is and the power of your User’s device. Optimally, on a modern device this value should hover somewhere around 60 FPS, and any time you scroll or re-paint the page, it can slow down as the GPU and processor calculates how the pixels on the screen change. Variations in FPS as you scroll the page down to 30 FPS is perfectly normal, and the faster you scroll, the more the value will drop.

 
Measuring the frame rate is useful to check whether your page contains too much information for the GPU to handle efficiently. This is affected by the number of elements on the page, effects such as shadows, transparency and blurring and by media such as images and video.
The Frame Rate usually hovers around 60 FPS on a modern device. Chrome’s FPS monitor also shows how much of the GPU memory (not to be confused with RAM) the current page demands.
The database

What slows the database down

Two things will affect the speed at which Bubble can find, download and present the data that you request: complexity and download size.

 
Download size

Download size means the total amount of data that Bubble has to download as you fetch a certain number of records. For example, a data Type called User may contain a few short fields called First name, Last name and Phone number, while a blog post may contain a short header and a long html text containing the post (like we discussed in the previous section about structured and unstructured data). Even a long article doesn’t contain that much information in itself, but multiplied with thousands or more of records, this can add up to a substantial amount of kilobytes or megabytes to download. The hidden Any field field will also increase in size with all data added to any field.
     In an earlier section, we explored how you can use the Chrome network tab to quickly identify searches and their total download size. If you’d like to read that now, click here.

Don’t worry, there’s a link there too that will take you right back there.

   Now, remember that we are referring to the data stored in the database in the examples below. Adding an image field to a record for example, doesn’t actually add the image itself, but only a text record of that image’s URL. While that image may of


 
course add to the total download size of the page, for the search it only adds a few bytes of text.
What determines the size of a database record?
Let’s look at a newly created record containing only Bubble’s basic info:


+----------------+---------------------------------------+------------+
| > **Field**    | > **Data**                            | **Size in  |
|                |                                       | bytes**    |
+----------------+---------------------------------------+------------+
| > Unique ID    | > 1603117061285x169136262540796830    | 32         |
+----------------+---------------------------------------+------------+
| > Created date | > 1607264748                          | 10         |
+----------------+---------------------------------------+------------+
| > Modified     | > 1607264748                          | 10         |
| > date         |                                       |            |
+----------------+---------------------------------------+------------+
| > Created by   | > 1603168031285x169136262540796987    | 32         |
+----------------+---------------------------------------+------------+
| > All fields   | > All data in fields above            | 84         |
+----------------+---------------------------------------+------------+
| > **Total      |                                       | **168**    |
| > size**       |                                       |            |
+----------------+---------------------------------------+------------+



Bubble saves dates in seconds since Jan 1st 1970 UTC, explaining the numerical values
The download size of this one record is approximately 168 bytes. To see how data scales, let’s assume you ask Bubble to download 10.000 records. That would give us a total download size of 168 bytes multiplied by 10.000: +
**1,6 megabytes**.

Let’s add a First name, Last name and US phone number to that:


| **Field**      | **Data**                               | **Size in bytes**       |
| ---------------| --------------------------------------| ------------------------|
| First name     | John                                   | 4                       |
| Last name      | Smith                                  | 5                       |
| Phone number   | \(XXX\) XXX-XXXX                       | 14                      |
| Unique ID      | 1603117061285x169136262540796830       | 32                      |
| Created date   | 1607264748                             | 10                      |
| Modified date  | 1607264748                             | 10                      |
| Created by     | 1603168031285x169136262540796987       | 32                      |
| All fields     | All data in fields above               | 84                      |
| **Total size** |                                        | **191**                 |





Adding a few more fields increased the download size for this record by around 14%.
The record size grew to 191 bytes - still pretty light. Multiplying that by 10.000 records, we would be looking at a total download size of **1,8 megabytes.**.

Let’s add a blog post to it. This is a random newspaper article saved as plain text:


| **Field**      | **Data**                             | **Size in bytes** |
| ---------------| ------------------------------------| ------------------ |
| Article        | Content of article                   | 5322              |
| First name     | John                                 | 4                 |
| Last name      | Smith                                | 5                 |
| Phone number   | \(XXX\) XXX-XXXX                     | 14                |
| Unique ID      | 1603117061285x169136262540796830     | 32                |
| Created date   | 1607264748                           | 10                |
| Modified date  | 1607264748                           | 10                |
| Created by     | 1603168031285x169136262540796987     | 32                |
| All fields     | All data in fields above             | 84                |
| **Total size** |                                    | **5513**          |

Adding a longer text ﬁeld increased the size of the record by **3.181%**


By adding this article, the record has grown to 5,3 kb, and 10.000 records would give a download size of about 55 megabytes - a sizable download.

Now of course in most cases, you will not be downloading every single record in a search. The whole purpose of adding constraints to a search is to tell Bubble to only download the data you actually need. But it serves as an illustration of how easily we can give both Bubble and the user’s device a lot of extra data to search, process, download, store in RAM and display, and it’s important to be aware that Bubble will download all fields of a Data Type even if you’re not showing them on the screen.

Complexity

Data type complexity is related to how many fields your data records have, and what kind of data they contain.

How the number of fields affects your searches is best visualized like an Excel spreadsheet: search performance is not only affected by the number of rows (records in your database), but also the number of columns (fields on each record).


 
The content in each field of your Data Type will also affect how much Bubble has to go through. As usual, size and complexity are closely related.

Bubble’s default fields

Let’s separate field complexity into three categories:

Light

Light fields contain information that adds very little complexity to your Data Type. Fields like First name, Yes/No and Date of Birth are quick and easy to search through.

 Medium

 The First name field doesn’t give Bubble a very challenging search.
We’ll go back to our blog post example. A field of medium complexity may contain longer strings of text such as a news article, forcing Bubble to go through more data. The search below would put more strain on the server, as, even if it’s just one field:
 
 This search gives Bubble more work to do, since you’re searching through unstructured data
Bubble has to go through potentially massive amounts of text to find what you’re looking for, and you may be better off finding your article using other constraints.

High

High complexity data types are those that contain lists of other Things that Bubble has to go through in order to find what you’re looking for.
Let’s say that you want to keep track of Users who have read an article. You add a field on that Article called Reader, containing a list of Users.
 
 This search forces Bubble to download an additional list of Things for each record in the search you’re performing.

In this example, for every row, Bubble has to go through an additional list (potentially long) of Users and check if the current user is in that list. Quite a job!
The complexity added by adding lists of Things to a data type does not only affect searches, but the amount of data that Bubble has to handle in general. If you load a list of Things, each containing a field with another list of Things, Bubble will load the ID of all of them, adding to download size, RAM usage and client-side processing.

For an Article, loading a list of tags on each article (2-3) may be fine, but loading a list of Readers (potentially thousands) can lead to slowdowns.

Introduction to structuring

Knowing the reasons a search may slow down, let’s look at how we can work to avoid those pitfalls.
Again we return to an important point: since Bubble is so easy to use, it’s tempting to jump straight into the work and set up your database type as you go along. As the project moves into a more mature (and complex) stage, you may find that you have to go back and make changes for different reasons. These changes can take a lot of time, and leave your database less organized than what’s optimal.

When planning your structure, there are many factors to consider, and many of them will be unique to your app. Many developers have contacted me over the years and asked for a set of “best practices” for structuring the database, but like most questions I try to answer in this guide, a straight answer would probably do more harm than good: there simply is no one way to cover every scenario. What I will attempt is to highlight the facts about how different decisions affect your database performance, and then present possible solutions to scenarios that may or may not apply to your particular needs.
 
So now, let’s talk about structure.

Planning your database

The Lean Startup (a book I warmly recommend) launched the MVP way of thinking that the tech industry in particular has taken to heart. Building for a fast launch, getting early user feedback and experimenting rapidly is both a great strategy and - I’ve found - a lot of fun. But keep in mind that it, like any other tool at your disposal, shouldn’t be used on autopilot. Structuring your database in the wrong way can set you up for time-consuming corrections and have long-term consequences for your product and business. With some experience, you’ll finish your database plan in a day - that’s worth it for the long-term health of your app.
Let’s spend a little time discussing how you should approach that question as you get ready to work on your database.

Balancing the need for advanced database structuring
The consequences of a poorly structured database are not necessarily visible at launch, but months or even years later as the workload and data volume grows. Decisions regarding your data structure are among the most important you’ll make.

 
That being said, the scenarios I’ll outline below are meant to speed up apps that manage large volumes of data and have specific client requirements: they’re not a blueprint, and they’re not best practices - they’re just examples to show how we can structure our database by taking it through some simple steps. For an MVP that you’re not planning to scale, you can in principle build your database in the fastest, simplest way possible simply to get the job done, and then re-think it as you’re developing the final product.
Don’t use Bubble for note taking
Setting up things in Bubble is done so quickly, it’s easy to use it almost as a note taking tool - you need to remember what Data Types to add, so you simply add them to keep track. The problem arises when you start working on those records - and in my experience that’s exactly what people start doing. Dust off your notepad and sketch out your database there first.
Get away from the screen
There are plenty of tools for drawing out your database on the screen, but in this first phase, nothing really beats pen and paper for quick drawing and revisions. I find the screen of a tablet to be too small and to hinder the free  low of the pen, but pick the tool that you find suits you best.

 
Always build with Privacy Rules in mind

If you don’t protect your data with Privacy Rules, you’re not protecting it. Every database record in your app that is not public needs to be designed with those rules in mind. Sometimes that means adding fields to a data type that you’d prefer to store somewhere else. Security supersedes performance in this case. If you don’t plan for Privacy Rules early on, you will find yourself making inconsistent decisions on the database design later on.

Keep your user in the center of things

Let’s return to our metaphor on the two layers of app development for a bit. Your database is not something that your users care about or will ever see. Don’t design it for them. All they have access to is what you choose to show them in your app’s UI. In other words, the database doesn’t need to be a neat and pretty spreadsheet - you can hack it in any way you deem necessary to get the right info displayed for the user when they need it.

 
The process of creating a Data Type

I want to take you through the mental journey that it is to plan for a new Data Type, because it affects how you plan for it. We’ll introduce some new terms that refer to different parts of that journey.

As you can see in the diagram below, our goal is to get from the conceptual idea of the information your app will manage to a structured database that can store and present that data efficiently.
Data Structuring Chart

 
Terms we’ll use
First, I want to introduce a few new terms that we’ll use as we explore how our app idea translates into a database.

Data Concept

The Data Concept represents the actual features that your database is there to support. For example, a CRM might include Clients and Vendors, but as we’ll see, it’s not given how these two concepts will look in the database. The Data Concept is a User Experience - not a database record. It’s how we think about the data. A Data Concept will result in one or more Data Types when this process is done.
Data Weight

Data Weight is the term I use to describe the metaphorical weight of a type’s total amount of data. If a data type contains fields that potentially hold lots of data (unstructured data like product descriptions and blog posts and long lists), that would give the type a potentially high data weight. A small amount of data (email, first name and last name) would indicate a low data weight.
Requirement Conflicts

Requirement conflicts is the process of looking over your data concepts from different angles to see potential challenges from a database perspective.
 
Satellite data types

Satellite data types are “extra” data types that you add to your database to separate data in order to solve a requirement conflict. Typically, they consist of one of three types:

Search data types

Search data types are set up as an extra “representative” of one or more data types when you need to either reduce the data weight on one specific type, or combine several data types into one efficient search. A typical case of the latter is if you’re building an app-wide search that covers multiple types (such as Contacts, Tasks and Projects). Instead of setting up a complex list with multiple searches through data-heavy records, you set up one lightweight data type that covers all types and they’ll all be displayed in the same Repeating Group.

Content data types

The Content data Type is a satellite that you set up for storing data that adds a lot of data weight. For example, if you have a blog platform, you may have a need to quickly search through blog posts, but the same posts also have to contain a lot of unstructured data. Separating the searchable records from the content helps you achieve both goals.

Link Data Type

A data type that’s used as an extra representative of multiple other data types. This is useful in cases where you need to link data to each other without setting up a high number of extra fields. For example, let’s say you are building a project management system: you may want to link a Task to multiple data types: users, contacts and projects for internal linking. By creating a separate Link Data Type you would be able to tag a task with any other data type, stored in a single field. In another scenario, you may want to display several types of Things on the same Page using that Page’s Thing: you can only do this with one Data Type at a time, but a Link Data Type solves that. This type can sometimes be combined with the Search Data Type to cover both needs.

Merged data types

Merging Data Types means to take two or more data types that share commonalities and merge them together. We then use another field (usually an Option Set) to separate them from each other. We’ll look into this in the scenarios below.
Phew! That was a mouthful of new techie-sounding jargon - but bear with me, I promise they’ll be useful. Let’s bring some more context into it by going over some scenarios:
Scenario 1: Vendors and Clients in a CRM
Step 1 - Define the Data Concept
A Client (I’ll call them Partner from now on to avoid confusion) asks you to build a CRM, and lays out different Data Concepts that they will need. Let’s focus for now on two of

 
them: Client and Vendor. We’re now in the first step of the Data Structuring Chart, where we define the Data Concepts: the data from our Client’s perspective.
 You immediately grasp what your Partner wants, and being the efficient Bubble builder that you are, you rush in and set up your two Data Types: Client and Vendor.
But stop for a second - let’s take this through the Data Structuring Chart. We’ve completed the first stage of identifying our Data Concepts, but now let’s run it through the second step of determining its requirements.
 
Step 2 - Identify requirements
You can think of these requirements similarly as you would think about doing User Stories: how will your users interact with this Data Concept? Generally, most requirements for a Data Concept can be split into one of these columns:

      Searching/Displaying
Privacy
Data Weight
Volume
How will I search for and display this Data Concept?
How should this Data Concept be kept private?
How much data will I be storing for this Data Concept?
How many records do I expect this Concept to hold over time?
  Using those pointers, a simplified look at our Client and Vendor Data Concept might look something like this:
     Client
Vendor
Searching/Displaying
Must be quickly searchable and displayed in a list
Must be quickly searchable and displayed in a list
Privacy
Only creator can see, but can share with colleagues
All users within the same company can see.
Data Weight
Must contain contact info like email, phone, billing address, office, address, description, notes and files. Must hold invoices.
Must contain contact info like email, phone, billing address, office, address, description, notes and files. Must hold purchase orders.
Volume
With many users in the system, the number of Clients may grow into hundreds of thousands
With many users in the system, the number of Vendors may grow into hundreds of thousands


 
Hold on! Are you seeing what I’m seeing? These are almost the same thing!

They’re both companies, needing the same fields to be stored, and only separated by what relationship they have with the CRM owner. Thinking about them one step further, couldn’t a Client also be a Vendor in some cases? How do we keep those two records in constant sync?

The answer is of course staring us in the face: these shouldn’t be two Data Types, but one, called Company. Recognizing that Vendors and Clients are Data Concepts, and not necessarily Data Types stopped us from rushing into Bubble and setting up a structure that wasn’t optimal. We can simply separate them with an Option Set field called Company type, and even set that field up to be a list to allow one Company to be both a Vendor and Client. Following our Data Structuring Chart, that would look like this:

 Great! So let’s set that up! Nope. Not yet. Remember, just because you’ve recognized one challenge doesn’t mean you’ve found them all.

Step 3. Identifying conflicts

Now that we’ve decided that our two Concepts have merged into one Data Type, it’s time to start looking for Requirement Conflicts. This means we need to look through our requirement table and ask ourselves: are any of these points in conflict with each other?
 122

 
    Company

Searching/Displaying

Must be quickly searchable and displayed in a list

Privacy

Only creator can see, but can share with colleagues
Data Weight
Must contain contact info like email, phone, billing address, office, address, description, notes and files.

Volume

With many users in the system, the number of Clients may grow into hundreds of thousands
     From what we know about how the download size of a given search can increase, these three points are in conflict: we’ve indicated that we want to store a lot of data on Companies and that the number of records can become big, but also that we want to search for them quickly. What to do?
The solution in this case could be two introduce one or more Satellite Data Types. In the case of our Company Data Type, we could structure it as two data types: one meant for searching, and another for holding all the data: one Search Data Type and one Container Data Type. How they each relate to data weight and search friendliness can be illustrated like this:
 
 Remember that the Volume also played a part here: because we expect the Company Data Type to grow into potentially hundreds of thousands of records, we need to make sure the total download size is as small as it can be.
And recognize the irony here: we went through one step of the Data Structuring Chart to reduce our number of Data Types, but then identified a conflict and increased it back to two:
 124

 
 Quite a journey our Clients and Vendors have taken in just a few minutes. The Data Type fields of these two types could be looking something like this:

 A real-life app would likely contain more fields, but here we see the Data Type and the Satellite Data Type bound together and can be referenced from both sides. The searchString field is an optional field you can add if you want to customize exactly what Bubble should search through. You can populate this with a text representation of the most important fields on the companyData record, like Company name + industry + country to give Users a  lexible search result.

The User’s perspective

Now, let’s remind ourselves: the User is unaware of this process, and how the data actually looks encrypted in a server far, far away. An isolated user journey for our Clients and Vendors might look like this:
 
 Up until the last step, the User is filtering and browsing a potentially long list of records, and we keep it light - in the last step we’re displaying a single record in isolation and we switch over to another Data Type unbeknownst to the User.
Scenario 2: Travel App
We’ll change our example app a bit for this one. Your Partner has now requested the building of TravlrTM, an app that sets out to take the throne from TripAdvisor as the number one tourist destination catalogue. The app will allow users to find new exciting destinations and check out local points of interest such as restaurants and hotels.
A key feature in this app, your Partner explains, is that it’s based around search. Users need to be able to search for not just one type of thing, but all the information stored in the database, just like TripAdvisor:
 
 TripAdvisor showing a Destination, a Hotel, a Point of Interest and a search category, all in the same list
He also wants the site to get organic search traffic, and wants every record to be displayable on its own page.
Step 1: Define Data Concept
Let’s have a look at the Partner’s Data Concepts and see what kind of data points we are talking about:
● Continent
● Country
● Destination
● Restaurant
● Hotel

You may already start to see similar Requirements and Conflicts as we did in our last scenario, but keep in mind our Partner’s requests: we need to search all records from the same search bar and take our User to a unique URL when clicked in the search results.
Step 2: Identify requirements
Let’s first look at the three geographical records that intuitively seem to have a lot in common:
      Continent
Country
Destination
Searching/ Displaying
Must be quickly searchable and displayed in a list along with all other Data Concepts
Must be quickly searchable and displayed in a list along with all other Data Concepts
Must be quickly searchable and displayed in a list along with all other Data Concepts
Privacy
Public information
Public information
Public information
Data Weight
Must contain a name, description, photos, travel tips and travel data
Must contain a name, description, photos, travel tips and travel data
Must contain a name, description, photos, travel tips and travel data
Volume
Less than 10
About 200

Potentially thousands or more

     As suspected, they are fairly similar. We can assume that they can potentially become fairly data heavy, since they’ll contain lots of unstructured data for the search engines.

Their volume is low (and more or less static), except for the Destination, which is harder to predict.

Should we merge these, like we did with Clients and Vendor? After all, these are not the same thing, and you may want to sort your Restaurants into Country and Destination for quick searching. Still, there are several reasons for why this makes sense:
- We can assume that we’ll be displaying all of these three categories simultaneously on many pages: if we combine them, we can get away with performing one database search instead of three
- Page Things: A Page can only load Things of a certain type. If you set up a page called www.travlr.com/location with Page Thing set to Destination, then this page can only show Destinations. Showing a Country or Continent page would need to load a new page with a different name where the Page Thing is different.
- The same logic applies to Groups: instead of having to set up a bunch of different Groups each catering to the different data types Destination, Country and Continent, you can load all three of them into one, lowering the number of elements on your page and speeding up the design.
Ok, so it seems to make sense to combine these three pieces of geographical data. Before we make a decision, let’s look at the rest of the Data Concepts:

 
Let’s first look at how the continents, countries and destinations might look like as a data type. It’s important to note that the three we show below here are the same Data Type - we’re displaying it thrice to illustrate how they are linked together.

 The geoContainer data type is used to represent all kinds of geographical data. I've left out fields like Description to simplify the example.
 
How do we know which ones are Continents, Countries and Destinations? The answer lies in the bottom row: by setting up an Option Set called dataType, we can easily separate our geoContainers into what type they are.
We only need one attribute on this Option set - the built-in Display value - to separate our three geographical Data Concepts.
 
Let’s return to the Data Structuring Chart to see visually what kind of journey they’ve had:
 We still have three Data Concepts, but the actual Data Types in our database have been reduced to just one.

 
Ok, so we’ve set up our geographical Data Concepts. Let’s look at the other types:

     Restaurant
Hotel
Searching/ Displaying
Must be quickly searchable and displayed in a list along with all other Data Concepts
Must be quickly searchable and displayed in a list along with all other Data Concepts
Privacy
Public information
Public information
Data Weight
Must contain a name, description, review score, photos, destination, country and continent
Must contain a name, description, rating photos, destination, country and continent
Volume

Possibly hundreds of thousands

Possibly hundreds of thousands

     Again, we’re looking at records that are fairly similar, and it makes sense to merge these two data types to one to reduce the number of searches we need to do in our app. We’ll do exactly what we did with our geographical Data Concepts, leaving the Data Structure Chart looking like this:
 
The name poiContainer comes from Point of Interest - a common term in the travel industry.
 
Step 3: Identify conflicts

Now let’s address our Partner’s request: all Data Concepts must be easily searchable from a prominent search bar. Just like in our last example, our main conflict in this app is that we have Data Types that both have a lot of Data Weight and must be searchable. How do we approach this?

 
We’ll solve this by adding a Satellite Data Type called Search. To illustrate this, we’ll remove the Data Concept and Requirement Part of our structure to simplify it a bit. We then add the Search Data Type as a Satellite:

We’re adding one extra Data Type (search) that we’ll use to allow app-wide searching for all kinds of Data Concept with just one server query.

For the Search type, we’ll again use the dataType Option Set to determine what kind of record we’re looking at in the list (and filter the search if needed). For that, let’s add our two extra data types to that Option Set:

Spending just a few minutes thinking about what our Data Concepts Requirements are, we’ve set up a data structure completely different from the initial setup suggested by our Partner.
The User’s perspective:

Not unlike our first example, our Users are being exposed to different data types along their journey to the actual record, but they have no idea it’s happening:

 
Syncing data between different Data Types

All this sounds great, but presents a challenge: how do I make sure that these separate data types are updated whenever the main data type is? For example, if we change the name of a Restaurant, how can we be sure that the accompanying Search Data Type is updated as well?

The answer lies in Backend triggers. For each change you want to keep in sync, set up a back-end trigger:

The trigger above will execute whenever a Restaurant’s name is changed. Triggers can be used not only to change things as needed, but also to create them. For example, a back-end trigger can create a new Search data type whenever a new Restaurant is added.

If you want to learn more about using Option Sets, you’ll find an in-depth tutorial about them on our website.

Searching efficiently

As your database is set up, it’s time to look at exactly what makes an efficient search. This section provides general rules of thumb for setting up your searches efficiently.

More constraints is better

Bubble searches work by excluding records that do not match a certain condition. In other words, the more conditions you provide, the faster Bubble can rule out records and shorten down the list of potential candidates.

Duplicate searches

I often see developers load their list into one element (such as a hidden Repeating Group), and then reference this element when they want to show the same list in multiple places. This is not necessary, as Bubble is already clever enough to only perform duplicate searches only once as long as the constraints match.

 
Bubble downloads only the data you need

If you are fetching data by Do a Search:First item or using a Repeating Group showing only a set number of records, then Bubble doesn’t download more than it needs to display the info, as well as a few more records to prepare for the user scrolling the Repeating Group.

Using lists as saved searches

Sometimes you will perform searches that are very complex, relying on nested structures, intersecting multiple searches or client-side processing. In cases like that, it can be useful to save a search as a list instead. This is a method we rarely use, as it goes against our general policy of securing searches with Privacy Rules. But since Bubble’s search capabilities will sometimes force you to perform the most complex filtering server-side, it deserves mention as an option.

How the :filtered (and other) operators works

The :filtered operator can be a source of some understandable confusion, since this is where the lines between what's performed server-side and client-side is the most blurred. Like in most things, Bubble will attempt to make the search as efficient and secure as it can, and as a general rule of thumb, that means performing it on the server.

 
It’s easy to assume that any kind of filtering you apply after the original search is performed will be client-side, but that’s only the case under specific conditions. Take a look at the example below:
There are no conditions on this search, but we apply a filter afterwards to search for an email. One might think in this example that Bubble downloads the full list of Users and then filters them client-side by the email field. But Bubble actually applies the condition on the server - but with one key difference: it takes the results of the first list (with no conditions) and then applies the second condition from the filter. Bubble converts that expression behind the scenes. This of course means a slight performance difference on the server, but unnoticeable unless you’re working with a lot of data.

What Bubble can’t run on the server is advanced filters. You know - these:

Using the advanced filter forces Bubble to filter the list client-side: less efficient and less secure

Bubble currently doesn't have the capability to convert arbitrary expressions into SQL. If you chain a sequence of searches and filters (as well as sorted, groupings, merges, intersections, unique elements etc, then Bubble will do its best to condense all of them into a single query that can run efficiently and push the majority of the work onto the server. That said, the longer or more complicated the chain is, the less likely it’s able to successfully do that.

If you need to apply operators after a search, do it step by step and make a conscious effort to notice whenever it slows down: at that point, you may have set it up in a way that Bubble was not able to run as a single query.

 
Nested structures

Nested structures apply to both searches and how you display Repeating Groups and describe any scenario where you force Bubble to perform a task on each row of a list of things.

In searches

In searches, a nested structure would apply to any search that contains another search as a constraint.

 In this example, for every User that Bubble goes through to find the right one, it has to perform a second search to find a specific article.

 Original search Number of Users
1
Total number of searches

   500
501
It may feel like you’re performing two searches. That’s what you set up, right? But in reality, you’re now performing 501 searches. The first one, and then one for each row of users.

In Repeating Groups

As you display a list in a Repeating Group, it’s also easy to lose track of just how many searches you’re asking Bubble to perform.

In this example, we are showing a list of Users in the system. The total number of searches is 1:


 
In the second example, all we want to do is show the number of articles a user has read:

How many searches is this? We’re performing one search to find all the Users, and then one search per row, to count that User’s Articles, totaling 5 searches.

Be mindful of setting up nested searches, as they’re the quickest way to throw your app’s performance off the rails.

 
The trigger above will execute whenever a Restaurant’s name is changed. Triggers can be used not only to change things as needed, but also to create them. For example, a back-end trigger can create a new Search data type whenever a new Restaurant is added.

Searches and lists

There are two ways to retrieve a list of Things in Bubble: perform a search, or fetch a list already saved on a Thing. List fields are created by checking the box below as you set up a new Field:

 
Lists and Searches have different pros and cons, as listed below:
Lists
Max out at 10.000 records
Do not adhere to privacy rules Are downloaded in their entirety Use client-side hardware to filter Must be manually updated
Lists
Number of records

Searches

Have no upper limit on number of records Info is guarded by privacy rules
Only downloads the needed records Uses server resources to index and filter Are dynamic

 
A saved list in Bubble at the time of writing this can only contain 10.000 records. This may sound like a lot, but for our list of Readers of an Article, this would quickly be exhausted.

Privacy rules

Privacy rules do not actually hide records in themselves, but apply an extra filter to a search looking for a record that matches that search. You can look at privacy rules as an extra search condition added on top of those you already have. In other words, any record fetched from a saved list will be fully visible to anyone, regardless of privacy rules. Performing searches makes sure that the information stays private. Keep in mind that even if you place a :filter on a downloaded list before displaying it, the information is still available in the browser for anyone looking for it.
Downloading and filtering

Filters currently can’t be applied server-side to a List, which means we can unknowingly put a lot of strain on the User’s device if we’re not careful. Let’s take our list of Readers again and assume that 10.000 readers have read the article.

If you want to learn more about using Privacy Rules, you’ll find an in-depth guide about them on our website.


You want to fetch the list of Readers (Users) but you only want those from the same country as you to show reading statistics. In this case, Bubble will:

● Downloadtheentirelistof10.000userstoyourbrowser
● Haveyourbrowser(client-side)filterthoseusersbyCountry

For a search of this size, the browser will at best become sluggish, and at worst it may crash the current tab. For this reason, lists are best suited for a low number of records and may not be your best choice when the number of entries exceeds 100.

 
Maintenance

A list will always contain the records you save on it, and will never automatically update their content. If the list needs an update, you will have to do that yourself through a workflow. The exception is deleted records, but keep in mind that they may sometimes simply leave an empty record in the list, leading to errors in :count results.

Searches

Number of records

There’s no upper limit on how many records Bubble can search through and retrieve.

Privacy rules

Privacy rules are applied to all searches as the first step, stopping the information from ever reaching the browser no matter what. For a search, Bubble will:
● Applyprivacyrulesconditions ● Applyallotherconditions
● Sendtobrowser

Downloading and filtering

When you perform a search, all conditions you place on that search are applied on the server, and then the information is sent to the browser. This means that conditions are safer (regardless of privacy rules) than filters, and you stop Bubble from downloading

more information than it has to. As we saw in the earlier section, download size can quickly grow when we reach a high number of records.

Let’s take the same example from before and look at how a Search would complete that same task:
You’ll see that we’re turning things around. Instead of asking the Article who’s read it, we’re asking the Reader which articles he’s read. The list of Articles a User has read is likely to be a lot shorter than the list of Users who have read an article. Even if the total number of Users in the system is high, this is the more efficient method of the two to retrieve the list, as we’re not relying on the User’s device to filter a long list.

 
Maintenance

Searches are 100% dynamic: whenever information on a record changes (even if done by another User) that is relevant to the conditions of the list, the list will instantly update. As an example, if you changed the Country on a user in the illustration above, the User would vanish from the Searched list, but would remain in the saved list.

Which is faster?

There’s a theoretical performance gain to be had from using a saved List when the list of records is short - but it’s doubtful that it translates into meaningful performance gain. The added work of maintaining them, the added data saved on the record and the loss of Privacy Rules is more than enough to justify not using Lists. There can of course be good reasons to use Lists for all sorts of stuff - but don’t implement them in the hope of improving performance - the tradeoff is very unlikely to be worth it.

Option sets

Options sets are like a database light for your application. You can’t make any changes to it without re-deploying your app, but on the  lipside they don’t rely on your database and are in fact included in the Bubble code downloaded to the browser. This means not only that you don’t have to query the Bubble database to retrieve their information, but also that they are delivered through Cloudflare as a cacheable JavaScript file, leveraging the global CDN coverage.

 
If you want to learn more about using Option Sets, you’ll find an in-depth tutorial about them on our website.


Option sets are frequently used at its most basic level to set up static values around your app. For example, we used Option Sets in our earlier example to separate GeoTypes in the Travlr app. Since these values will rarely or never change, we don’t mind that it would require re-deploying our app.
Naturally, Option Sets are not meant to store a big database. While your Bubble database only downloads the information that it needs, the full option sets will be downloaded every time a user accesses any page in your app. Also remember that any sort of filtering you do on Option Sets is applied client-side.

Creative uses of Option Sets for performance

Apart from populating dropdown lists and categorizing GeoTypes, Option sets can be used in different creative ways to speed up the page load and add more  lexibility to certain parts of your page.

 
Replacing database entries for quicker loading

For pages where load speed is particularly important, like the front page of an eCommerce store, Option Sets can be used as a replacement for a database search. I’ve worked on pages where the goal on the front page was to avoid having any database references at all, and where Products were added and maintained as an exact copy of their database counterparts. Having no database references on the front page cut the loading time by nearly two seconds and left the entire page depending only on Cloudflare’s CDN. Best practice? Hardly - but it served its purpose. The page loads quickly and retains a valuable SEO performance.

Building an app menu and User privileges in the same Option Set
Building a menu for a SaaS CRM application, we looked at different ways of making a flexible menu that would also serve as a user privilege check and only show the menu options that the currently logged in User should have access to. We set up an Option Set called Privileges that included entries like Contacts, Projects and Company Settings.

● WesetupafieldoneachUsercalledPrivileges,containingalistoftheseoption sets. Each entry added to the least would mean the User has access to that menu option.

● Theleft-handmenuintheappdashboardwassetupasaRepeatingGroup, showing the Current User’s list of Privileges. Clicking on a menu Option would use the Go To Page with a slug saved on the Privilege being clicked.

 
● Intheusersettingwindowoftheapp,wecouldsimplylistallPrivilegesina Repeating Group under a user profile, to allow an admin to add or remove Privileges from a User.

Option Set as a Message Popup

Option Sets can also be used to set up popup screens with different messages and actions to reduce the number of elements on the page and ensure workflow consistency. In the example below from a real-life application, we set up a Reusable Popup that can be used to run a range of actions from any page in the app:

Below is the Option Set called Message Setting, with some different attributes we’ll use in the popup:

Create a Popup, and set its data type to the newly created Option Set. Before showing the popup, we’ll Display the correct Option set to determine what message to show:
 

We can then populate each field in the popup with the field from the currently loaded Option:

The popup will show one or two buttons, based on whether the Button: low emphasis is empty or not, and the two text fields get their content from the Header and Message fields.

Finally, the currently loaded Option determines which workflow is triggered when the User clicks. Workflows are stored in separate Custom Events:

This way, we’ve set up a single popup to display a wide range of different messages, and we’re also making sure that some of the key operations of the app are contained within a reusable element and can be triggered from anywhere in the app as needed.

 
Workflows

What are workflows?

A workflow is a collection of sequential actions that are triggered by some kind of input, scheduled at a set time or triggered by a certain condition. How well a workflow is optimized for performance depends on many factors: what exactly it does, how it does it, when it does it and conditions. Workflows, like everything else in your app, also adds to the total amount of data Bubble downloads and stores in the memory of the user’s device.

From a UX standpoint, workflows are one of the most visible tests of how your app performs, since the time between start and finish is so easy to quantify and an action typically attracts a user’s full attention. As we’ve covered earlier in the book, workflow performance is as much about the illusion of progress as it is about actual performance,

This chapter will look into optimizing for both of these perceptions.
 
Front-end and back-end workflows
Not to be confused with server-side and client-side, we’ll separate processes into two camps:
Front-end workflows
Front-end workflows are the workflows that are triggered on a page, run on that page and stop running if the page is closed. They are everything that is contained within the workflow editor when you have a page open. Then are triggered by:
● Pageload
● Useractions
● RepeatedeveryXseconds
● Triggeredbycondition(suchasdatachanging)
Front-end workflows can be instant or produce visible delays for the user as he uses the app, depending on the actions it performs.

Backend workflows

These are the workflows that reside in the backend workflow editor. They are not contained within a specific page, but can be triggered or scheduled by any page in your app, making them globally available. They are triggered by:

● Schedulingimmediatelyorinthefuturebyafront-endaction
● AnexternalserviceconnectingtoyourappthroughanAPI
● TriggeredbyconditionsonaBackendTrigger
● Regularintervals
● BeingrunonalistofThings
● Self-scheduling(recursiveworkflows)

How backend workflows affect the front-end

The beauty of backend workflows is that in principle, they don’t affect a User’s perception of the application’s performance, as long as they don’t overspend your app’s total capacity. Great! So let’s move all actions to the backend!

As always, there are some caveats and common misunderstandings. Let’s clear them up.

If you want to read more about back-end workflows, we have an in-depth guide on our website. Click here to read it.

 
Scheduling backend workflows

Running an action on the page does in itself not cause any delays, except for the time it takes to actually perform the instructed action. Confused? Look at it this way: when you instruct Bubble to execute an action, you are in principle scheduling it to run immediately. While the action itself may not be instant, the scheduling itself is. Scheduling a backend workflow on the other hand, can be considered an action in itself, and is not necessarily instantaneous. In other words, it takes a few milliseconds to schedule a backend workflow, and many actions performed on the page will finish quicker than that. So don’t move all your actions to the backend just yet.

Bubble is optimized for front-end actions

As we’ve touched upon earlier in the book, Bubble is well optimized for its front-end actions and are performing a bit of magic on your page without you having to set it up:

● Bubblewillusuallyimmediatelyrenderchangestooneormoredatabase records to the screen, as long as they are performed by a front-end action. Database changes will seem instant, even if they’re not
● Searchresultsarequicklyandconsistentlyupdatedforanychangeyoumaketo records contained within in - if an update on a record fails to meet the search criteria, it will immediately disappear from the list
● Schedulingabackendworkflowcausesadelayinitself,inadditiontowhichever time the action takes to actually complete - the total time will be longer
● Bubblewillshowrecordchangesperformedonthebackendfairlyquickly,but not instantly. You may find it can take up to a few seconds before a change made in the backend is visible in the front-end.

So... never use backend workflows then?

All that being said, backend workflows are still a powerful feature for your app. Indeed many app actions, such as performing changes on a lot of records, are not possible without them.

Below are some common scenarios and possible solutions:

Scenario
Change made on a single Thing
Change made on a short list of Things (100 items or less) Actions performing searches to finish
Workflows with a long range of actions
Cascading actions*
Changes made on a long list of Things (100+ items)
What to use
Page action
Page action
Consider both Consider both or a mix Backend

Backend

 * Actions that lead to more actions. Example: Deleting a User requiring to delete all the Users data saved in other Data Types

Two useful questions to ask yourself is:

● Willmyusersexpectaninstantresponsetotheiraction?
● CanIproduceaninstantresponse?

 
Remember what we discussed in the section about User-Perceived Performance. A response is not necessarily a finished workflow: it’s just communication. If you’re performing a workflow that your user’s are unaware of, or don’t expect to finish immediately, consider moving it to the backend and away from the page. Find ways in the front-end to make the results seem instantaneous, and then finish it up leisurely in the backend.

Client-side and server-side actions

Some actions in your app will rely on the server to complete, while others are performed client-side. Knowing that difference can help you optimize workflows to avoid having to communicate with the server, but keep in mind that client-side data is lost when the user navigates away from your page.

Most of the client-side actions are kept within the Navigation and Element actions:

Examples of client-side actions are: ● Showingandhidingelements ● Settingstates
● Animations
● Stylechanges
● Scrolling
● RefreshthePage
● GotoPreviousPage
● OpenanExternalWebsite
● AddaPausebeforenextAction
● TerminatethisWorkflow


 
An easy rule to remember is that a client-side action will mostly execute without problems even if you disconnect your device from the internet.

Some of these actions can be considered a hybrid of client-side and server-side. For example: showing the next page in a Repeating Group is technically a client-side action, but if Bubble hasn’t loaded the data yet, it will fetch what it needs from the server to display it. Likewise, showing an invisible group may lead to Bubble loading its data source.

What slows workflows down?

Workflows are mostly very quick. Remember the magician from earlier in the book, hiding what’s really going on backstage? Bubble applies all sorts of tricks to make it seem like processes are instant, while in reality they may take some time to finish in the database. One of the most visible examples of this is if you show a list of Things in a repeating group - let’s say a list of Users - and then use the Make changes to a list of Things action to change everybody’s first name to Joe: voila! The entire list will change instantly, even though it’s safe to assume this operation takes a bit more time to finish on the server.

 
There is no unknown information in this action - Bubble already has everything downloaded
The reason this can be done so quickly is that there are no unknowns: Bubble already has the full list of users downloaded, since we are showing them in a Repeating Group. It also knows that everybody’s name is now Joe, and can apply this change client-side to show the result instantly. Just like a technically client-side action can trigger a server-side action, a purely server-side action can also trigger a client-side response to communicate efficiently with your Users.
The challenge, and delays, arise when we introduce an unknown into the mix:

Bubble doesn’t know what the first name will be, and needs to complete the search before it can display the results

In this example, we’ll be adding a slight delay, since the workflow forces Bubble to perform a search before it knows what the new first name will be. Once that is found, the result will be instantly applied to all Users visible on the screen.

This illustrates how you can plan out your workflows keeping in mind what information Bubble already has. As Bubble is already optimized to show changes on screen immediately, you can leverage this by making sure Bubble has all the information it needs before the process even begins.

 
Action response design
When a user clicks a button, you get to design what happens. Awesome, no? In this section, we’ll return to the concept of having two layers in your app.
Layer 1 is what’s actually going on
Layer 2 is the user-perceived performance (UPP)
Action response design is about planning and designing what kind of response your user gets when he initiates an action. Your users will bring certain expectations, but you also have the power to set those expectations.



First, let’s go through the three types of responses an action can give a user:

Immediate response

The process takes no time to finish. Users will see the change happening or get a confirmation that the process is finished immediately.

Delayed response

The process takes some time to finish, typically ranging from a few tenths of a second to a few seconds. Users expect a sign of progress, such as a loading bar, button or icon animation or UI skeleton.

Future response

The process takes significantly longer, typically caused by database operations such as importing a large CSV file. User’s expectations are set by communicating a message like: This will take some time. We will email you when it’s finished.

What the last two have in common is that users accept more than you might expect, as long as it’s clearly communicated.

Immediate response

An immediate response would follow the pattern below:


 
There is no perceived delay between the user clicking and the process being finished. Whether to communicate that it has finished or not depends on what the action is.
Delayed response
This is the kind of workflow that causes most concern for Bubble developers. There are a few different ways a delayed response can play out from the perspective of User-Perceived Performance:

 
In the illustration above, the user clicks a button, and you simply wait until the process is finished before you communicate anything. This can work just fine for shorter delays, or when the standard Bubble load bar communicates sufficiently.

The second type let’s the user see one type of communication as the button is clicked, and a second to confirm that it’s done. This can be two separate messages, or they can be joined together by something like a popup with a progress bar, depending on the process and duration. This solution works best with processes that actually take a bit of time to finish. If the duration is 1 second or less, the communication may simply  lash unnecessarily on the screen.

 
The third type communicates instantly that a process is done, and then quietly finishes it without the user ever knowing how long it actually took. Note that communication doesn’t always have to be a message: it can simply be a change on the screen such as going to the next step in a sign-up form. The important thing for the user is the confirmation that something has been done.

Action sequence order

The order in which actions in a workflow are executed can have a major impact on UPP. While Bubble seems to perform certain tasks synchronously (at the same time) to speed things up, they are mostly completed asynchronously, meaning that it completes one step before moving on to the next. In other words, you need to be strategic about what action comes where to hide delays from the user. Take a look at this workflow:

 
The final step is the one that communicates to the User - moving it can improve the User-Perceived Performance

Bubble will sign the user up, Create a few other Data Types, and then set the state required to go to step 2 in the sign-up form. As these processes finish up, the user may experience a lag. By moving Step 5 to the beginning of the workflow, Bubble will go to part 2 of the sign-up form and then perform the database operations. Note that Bubble’s loading bar will still show.

Background triggering

Bubble is set up by default to notify the user that a database operation is in progress by showing the blue loading bar at the top of the page. If the user didn’t directly start that process, on the other hand, you can avoid showing the bar by triggering the operation in the background instead of by a button click. This also allows you to delay a process

 
and run it when the user’s attention is elsewhere. This way, you can make it seem like an instant process even if it takes a moment to finish.

Instead of placing the Sign the User up and Create a new Thing actions on the button, the button will simply set a state to jump to the next step of the sign-up form.

 
Then, we silently trigger the database actions by a workflow that was not directly initiated by the user, such as when Step 2 of the form is visible. It’s a few minutes of extra work and maintenance, but makes the UPP more responsive.

Spacing out workflows

Spacing out workflows is the concept of taking a time-consuming workflow and spacing it out so that each step is acceptably short or even unnoticeable. In the end, the server has done exactly the same job, but we can avoid spikes in the user’s lag experience, and sometimes also in your app’s total capacity.

Multi-step

The most obvious way to space out workflows is to split them up into several actual steps that the user has to go through before a process is finished, like our example with

 
the sign-up form in the last chapter. Instead of having a large, scrollable sign-up form with lots of fields that culminates in a long workflow creating a number of different Things, we can strategically split the form up in a few steps. Not only do we avoid running all the actions all at once, but we also keep the user preoccupied with inputting new data into the form while the process finishes in the background.

Keep in mind that multi-step processes can sometimes lead to saving redundant information. For example, the User may not finish all the steps, leaving you with ghost records in your database.

Process spreading

Process spreading is my term for finishing a search or conditional statement before it’s actually needed, to speed up the workflow that relies on that information.
In this example, we want to add new tags to our system, but we only want to add tags with unique names. We perform a search to check if a tag by that name already exists, and Bubble needs to finish that search before it knows if it should move on to create the new Thing.

 
By using process spreading, we can finish that search before the user has clicked the Create button, and speed up this process.

 
We do this by creating a group like illustrated above. Give this group number as the type of content and then place the search there. As soon as the user enters a tag name into the input field, Bubble will filter the search and return a number. The user never notices as the loading bar will not show and the user’s attention is focused on typing a name and clicking the button.

 
 Now when we perform the conditional check in the Create Tag step, we simply check the number stored in the group. The server is performing the same task, but because we spaced out the workflows, the interface feels snappier.
 180

 
Using process spreading for error messages
Taking this method a step further, you can use process spreading to generate error messages in your app. For an advanced form, a button can generate a range of different error messages (tag name is empty, you don’t have the privileges to create tags, etc, etc), which would typically involve a lot of conditions having to be checked when the user clicks the button. To speed this up and simplify it using process spreading, we need to make a few changes:
1. Change the Group’s Type of content to text and leave the data source blank 2. Addconditionsforeveryerrormessagethatyouwouldneedtodisplay
  181

 
Here we have two conditions: one checking if a Tag already exists, and the second one checking if the tag name is empty.

Now, instead of checking if the number is 0 before creating a Tag, we check if the error message is empty. If it is, simply proceed with the Create workflow.

 
If the content of the Group is not empty on the other hand, we display its text content in an Alert element. Again, we avoid placing multiple and/or complicated conditions inside a workflow where the user will notice a delay, and instead tell Bubble to finish checking all the conditions before the workflow has started.

 
Do Not Repeat Yourself (DRY)
In programming, there’s a principle often abbreviated to DRY. For Bubble, it simply means that any resource you set up in your app (elements, workflows, styles) should not be repeated.
Not only does repeating them force Bubble to load the same resource multiple times, but it opens up for errors down the road. You change something in the action step of a repeated workflow, and have to change it in other places as well. It takes time and let’s face it, we sometimes forget to make the necessary changes.

Custom events

Custom events are the most basic ways of avoiding repetition. They allow you to set up a step of actions, and then run those actions from anywhere. You can also trigger a Custom Event inside of a Reusable Element from its parent, making it one of the few ways to communicate directly with reusable elements. We’ll get back to how you can leverage this to structure your app and avoid repeating yourself.

Use them. Not only do they help you avoid repetition, they’ll also make your workflow editor easier to navigate. I usually give Custom Events a color to separate them from the rest of the page, and then use a simple logic structure to sort and name them.


Giving custom events names like Thing: Action sorts them together and makes them easy to navigate
By having a set workflow for saving an Article, you can easily add new ways for the user to save it without setting up any new workflows.

Reusable elements

Reusable elements have an obvious use in parts of your page that’s repeated on multiple pages (such as a footer), but should also, like Custom events, be used to avoid any kind of repetition. Reusable elements do not only contain page elements, but workflows too, meaning that certain parts of your page’s functionality can in principle be stored away in Reusable elements.

Let’s say for example that you have a popup for creating a new User. By setting up that popup in a Reusable Element, you ensure that:

● Youcanaddusersinanypartofyourapp,regardlessofpage
● AllworkflowsassociatedwithcreatingaUseriscontainedwithinthatReusable ● YoucantriggerworkflowsassociatedwithUsersfromoutsideofthatReusable
 185

 
○ Evenloadingpopupcontentandshowingthepopupcanbestoredinside of the Reusable itself, avoiding repetition even to display it
Reusable elements do come with some restrictions that you should be aware of. This guide will not go into detail on that, but for new Bubble developers, the process of exchanging information from inside and outside of a Reusable element can be confusing. I’ve written a guide on advanced reusable that you can check out here.
Sharing Custom Events across your app with Reusable Elements

Knowing that Reusable elements can contain Custom Events, and these Events can be triggered from outside of the element, we can use that to share Custom Events across your app.

Remember, a Reusable Element doesn’t have to actually contain any Elements. You can set up a completely empty, invisible Reusable Element and then store Custom Events inside of it that can be triggered on any page where the Reusable is placed. I often create a Reusable Element called actions and place all my oft-used workflows inside of it.



The Reusable Element is no bigger than 1x1 pixels and can be invisible on page load.
If needed, the Reusable can also contain elements that are used across your app, such as Popups.
Both the workflow and the edit user popup are stored within the Reusable

 
This method ensures that you are consistent with where your workflows are stored, and keeps the workflow editor for the Page itself a lot lighter and easier to work with.
A word of caution before you start moving all your workflows into a Reusable Element: the method does demand planning. Sending information into the Reusable and then back to the page when it’s done can require a complex setup of states being passed back and forth, and you may end up with adding more actions than you saved in the first place. While I highly recommend the method for setting up efficient pages, I would encourage beginners to experiment with it first to learn the pros and cons. Be mindful also that if not planned well, you may end up loading a large number of workflows on every page in your app, even when they’re not needed.

Leveraging the Bubble back-end

We’ve discussed how front-end and backend workflows both have pros and cons, and now we can look a bit closer at some scenarios where you can leverage backend workflows:
Backend workflows in Bubble serve three purposes:
1. to schedule workflows that will run even if the user closes your app 2. toallowthird-partyservicestoreachyourappthroughanAPI
2. Torunloopedworkflows(eitheronalistorrecursively)


 
From a UPP perspective, they have a big upside: no matter how big a job you throw at it (staying inside of your app’s total capacity), your users will never notice any lag or slowdowns because of a workflow running. You can make changes to a million records, and your user won’t notice.
Back-end workflows run independently of your app’s front-end, and thus can be used to hide demanding processes from the user.

Schedule workflow on a list vs. recursive workflows

For processing hundreds of database records or more (up to millions), back-end workflows are not only the best way to do it, but the only way, realistically. There are two ways to perform a workflow on a List of things:
Schedule back-end workflow on a list will let you set up a workflow that is run once on every Thing on the List you provide. I’ll refer to this as WOL (Workflow On a List)
Recursive workflows are technically run on just one Thing, but include an action that schedules itself to work on the next record in the list as the last step in the workflow. I’ll refer to this as RW)
In principle, they are the same. You can see recursive workflows as a “manual” way of scheduling workflows on a List. What you’ll find is that this manual setup gives you a lot more control over the processing than you would have using the Schedule API workflow on a List action. In short, while I encourage you to find ways that work for you, I personally only use RW’s. The main reasons for doing so are:

● WhileWOL’scantimeout,anRWwillalwaysfinish
● YouhavenowaytoknowwhenaWOLisdone,butyoucaneasilytellorschedule a different workflow when an RW reaches the end of its list Let’s use our example from earlier with a Future response. If your user imports a large CSV file and you need to run a workflow on each row of that CSV (such as setting up a new User), then you would need to use an RW in order to email the user when the process is done. Using a WOL, there would be no way to tell when it was done.

Recursive workflow delays

With recursive workflows, you can play around with what your system can handle in terms of capacity. Start out with about five seconds in between each loop for heavy workflows, and adjust down if you feel comfortable that the server can handle it. Personally, I store these delays in an option set that lets me categorize workflows into Light, Medium and Heavy tasks. Each of them has a set amount of seconds that I can adjust as needed. This way, if my capacity is working fine with a hundred Users in the system, but starts struggling with 300, I can simply increase the value a little bit, and with just a keystroke I’ve changed the delay on maybe hundreds of different back-end workflows, ensuring that my app keeps running smoothly without upgrading capacity.

Backend triggers

Backend triggers, in my view, are one of the most strangely undercommunicated Bubble features, but let me be the first to tell you: they are a godsend for setting up efficient apps and an immensely powerful feature.

 
The reason is simple: a backend trigger can react to something that your user does, but without adding any lag or more workflows to your page load. You can start a massive operation backstage in your magic show, and your audience has no idea.
It’s not unusual that one action or workflow in Bubble triggers another. Usually, we don’t think too much about it, as we see it simply as the way a workflow works - the follow each other one after another. But let’s go over a couple of principles from this book:
● Don’tRepeatYourself:weshouldtrytoavoidsettingupidenticalworkflows
● Keepyourpagelight:additionalactionsaddtoourpage’stotalresourceusage
on the device
Our analogy from earlier about the two layers of Actual Performance and UPP is also helpful to illustrate the power of backend triggers:
  192

 
Let’s have a look at how we can exploit backend triggers to move workflows away from your page (Layer 2) and into the Bubble back-end (Layer 1)

Deleting complex data

Deleting Users is a typical process that can demand a lot from your system, since a User often has a lot of associated data spread out in different Data Types. If you are running a CRM for example, deleting a User can also mean deleting all of that User’s data: Accounts, Contacts, Messages, Projects, Notes, Tasks etc.

You can of course schedule an API workflow from your page, but apart from adding a delay and an extra workflow on the page, there are some downsides to this. Typically, you’ll need to delete all the User’s content before you delete the User itself (to be able to locate it), which means that the User will remain visible in your app until a potentially big workflow has finished running.
By using a combination of Privacy rules and triggers, we can make it seem like the User is deleted immediately, while we allow the back-end to digest the process for as long as it needs to.

 
The process looks like this:
1. Set up a Yes/No field on the User called Deleted.
2. SetupPrivacyrulesthathidesUserswithDeletedsettoYes.Thiswillhidethe
User from all lists as soon as the field changes. You can also set up Privacy rules on the User’ other Data Types, to hide them immediately.
1. CreateaBackendTriggerthatwatchestheUser’sDeletedfield.Wheneverthe field changes from No to Yes, the trigger schedules the API workflow that deletes all the User’s content and finally the User itself

From a UPP perspective, we’re using the third workflow model for this:

You can trigger the confirmation message immediately, and your user is unaware of how long the process actually takes.
This method also allows you to  lexibly add additional functionality to your app. You can easily set up a way to Undo the user deletion for example, by having the Back-end Trigger schedule the Delete workflow 20 seconds into the future, and set an Only if to check if the User’s Deleted is still set to Yes. To Undo, simply change Deleted back to No within 20 seconds, and voila, you have yourself an undo feature.

Back-end triggers will execute even if you use the Make changes on a List action. In other words, as long as the list is not too long, you can seemingly instantly delete 20 Users, and then let a recursive workflow in the back-end slowly work its way through deleting everything without overspending your capacity.

 
Keep in mind that the condition on a back-end trigger will run every single time any change is made to that Data Type. If you edit a User’s credentials in 10 input fields that are Autobound, Bubble will check the condition on the Trigger every time: keep the conditions light, or it alone can create a spike in your capacity chart. Also, get to know the restrictions on Triggers: there are plenty of them. Countless times I’ve been told that triggers are not reliable. They are, but they come with several pitfalls. Get to know them here.

Using back-end triggers to keep data in sync

Remember the Search Data Type we discussed earlier, where we set up a Data Type that only contains the data needed to find and display it in a search? Back-end triggers allow you to always keep two data types in sync, without having to add any extra workflows to your page. Going back to our blog website, you may have set up a Search Data Type for all your Articles. What happens when you change the header in an article? You’ll need to change the header in the Search Data Type to match: by using triggers, you ensure that not only are they always in sync, but you avoid placing extra workflows on the page where the Article is edited, keeping thap page nice and light.
Combining Option sets and triggers to automate workflows
The idea of triggering workflows whenever data changes can also be used without that data serving any other purpose than that. You can see this is kind of a command saved directly on the Thing. Using our CRM example again, you may want to add a few ways to manipulate a Lead. Set up these different commands in an Option set that we’ll call Commands:
On the Lead data type, we’ll set up a field for this command:

 
Now, every time you want to apply one of these commands to a Lead, you simply use Make Changes to a Thing to give the Command field a Value. A back-end trigger will watch for the field to change and execute the corresponding workflow when it does:

When to use back-end triggers

Use it when you can make your app more responsive by moving big operations to the back-end, and to ensure data stays in sync no matter where in your app it has changed. If your Delete command only uses the Delete a Thing action, there’s no reason to set up a complex trigger system to run that simple command: simply place it on the page. But if it triggers a cascade of different actions like in our User example, it’s one way to speed things up for the user. Get to know how triggers can fail to execute in different scenarios, how they affect your apps privacy and security and how to avoid them being a capacity thief in themselves.


 
Communicating clearly

We’ve talked a lot about communication throughout the book, and I’ve tried to illustrate that you can hide processes and delays behind different ways of communicating.

Imagine that you are at the office and your spouse is in your home. You have agreed that he or she will prepare dinner for you at 5 pm, and at 2 pm you start realizing that you may be late. You don’t say anything, and come home at 7 pm to a cold dinner and fuming spouse. Ragnarok ensues.

Now take the same scenario, but this time you communicate at 2 pm that you may be late, and that maybe dinner can wait until 7 pm. Peace on earth.

The circumstances are the same, but communication was different.
Silly as the metaphor may seem when talking about app development, the similarities are actually helpful when you think about it. Great and transparent communication builds trust and goodwill.

 
Take a look at how global money transfer service TransferWise shows progress as money is transferred to someone:

We’re missing the animation here, but it shows the money going from you, to TransferWise and on to the recipient as if a physical object was being moved. Similarly named file sending service WeTransfer has a more traditional upload progress bar:


 
Both are processes that can take up to a few minutes, but not only do you accept that it can take a while before it’s done, but the design is so well-made you almost want to look at it until it’s finished even if you don’t have to.

Communication is there to maintain a relationship with your user. It’s the only tool you have to control how a user feels about your app and its performance, but luckily it’s incredibly powerful.

Three basic functions are covered by communication in workflows:
● Anactionhasbeenreceived(i.e.buttonclicked)
● Aprocessisrunning(i.e.loadingbar)
● Aprocessisfinished(i.e.popupmessage)

What all three of them have in common is simply to say to the user that the app is receiving his commands, has not crashed and will finish the task.

A full guide on how to design user interfaces performance-friendly is out of the scope of this book, but numerous examples are included below to show how you can communicate through different parts of the process.

 
Action received
As soon as a user has initiated a process, he will expect your app to confirm it. It would be weird to press a button with nothing happening afterwards, right?
Communication can be subtle: a slight change in the color or shadow of a button can be enough:
Simply changing the color of a button when clicked confirms to your users that the trigger is received.
The animated ripple effect is how Google's Material Design confirms a button click
   203

 
A simple text confirmation can be enough to show that an action is received and being processed.
Bubble’s own Alert element sticks to the top of the screen and can even automatically confirm autobound saving without additional workflows.

A process is running

The next step is a bit different, especially if the process is time consuming. You’re not only telling your user that something has happened, but that a process is ongoing and maybe how close you are to finishing it. This step may make the first step redundant.


 
 A loading bar is a great way to let your users know that the app hasn’t crashed, but needs a bit more time to finish.
One of the simplest ways to show a process underway. Great for simple processes, but lacking in information on what’s going on and how long it will take.
  205

 
 A popup can be particularly helpful if you want to stop your users from taking any more actions until the work is done. Can easily be combined with a progress bar, animation or illustration.
A process is finished
Positive, quirky illustrations can make your app seem more friendly and approachable. Apps like Notion use this to great effect.



 
 Sometimes, telling users a process may take some time, and they’ll receive an email when it’s done is perfectly acceptable.


 
Conclusion

I’d like to close with a few statements made earlier in the book that I hope will be helpful as you Bubble your way to an awesome app:

Performance is a war of a thousand battles

After reading this book, you may want to read it one more time to take in the different lessons. Performance is about making a lot of decisions, and some of them may be difficult to backtrack. Setting something up right the first time is a lot more efficient than going back to make changes later. With experience, you’ll start to see that some things are optimally implemented when the app is first set up, while others can easily be set up post-launch, so that you can stick to your deadline. This brings us to our second point.
Performance is a feature
If you make performance the #1 priority of your app, you risk doing so at the cost of other features and meeting your deadline. For some apps, that may be a sound strategy, for others it may be the wrong priority. I stress the points frequently that getting an app to the market should be your main goal: let your users tell you what to prioritize from there.
I’ve spent a great deal of time compiling this book. I sincerely hope it can save you from having to learn some of the painful lessons I have, and nothing would make me happier than to know that it has brought your project to fruition and success.
I would love to hear your thoughts: if you’d like to give me some feedback, feel free to use this form to share your suggestions on how this or future books can be improved. You can follow me on Twitter to get updates on new articles and guides, and you’ll find a growing archive of tutorials on www.amliesolutions.com.
Lastly, if you found this book useful, please consider giving it a rating on Gumroad - it really does help me out!
Happy Bubbling :)




# Primera Tabla

| **Field**      | **Data**                             | **Size in bytes** |
| ---------------| ------------------------------------| ------------------ |
| Unique ID      | 1603117061285x169136262540796830     | 32                |
| Created date   | 1607264748                           | 10                |
| Modified date  | 1607264748                           | 10                |
| Created by     | 1603168031285x169136262540796987     | 32                |
| All fields     | All data in fields above             | 84                |
| **Total size** |                                    | **168**           |

> Bubble saves dates in seconds since Jan 1st 1970 UTC, explaining the numerical values
>
> The download size of this one record is approximately 168 bytes. To see how data scales, let's assume you ask Bubble to download 10.000 records. That would give us a total download size of 168 bytes multiplied by 10.000: **1,6 megabytes**.

# Segunda Tabla

| **Field**      | **Data**                             | **Size in bytes** |
| ---------------| ------------------------------------| ------------------ |
| First name     | John                                 | 4                 |
| Last name      | Smith                                | 5                 |
| Phone number   | \(XXX\) XXX-XXXX                     | 14                |
| Unique ID      | 1603117061285x169136262540796830     | 32                |
| Created date   | 1607264748                           | 10                |
| Modified date  | 1607264748                           | 10                |
| Created by     | 1603168031285x169136262540796987     | 32                |
| All fields     | All data in fields above             | 84                |
| **Total size** |                                    | **191**           |

> Adding a few more ﬁelds increased the download size for this record by around 14%.
>
> The record size grew to 191 bytes - still pretty light. Multiplying that by 10.000 records, we would be looking at a total download size of **1,8 megabytes**.

# Tercera Tabla

| **Field**      | **Data**                             | **Size in bytes** |
| ---------------| ------------------------------------| ------------------ |
| Article        | Content of article                   | 5322              |
| First name     | John                                 | 4                 |
| Last name      | Smith                                | 5                 |
| Phone number   | \(XXX\) XXX-XXXX                     | 14                |
| Unique ID      | 1603117061285x169136262540796830     | 32                |
| Created date   | 1607264748                           | 10                |
| Modified date  | 1607264748                           | 10                |
| Created by     | 1603168031285x169136262540796987     | 32                |
| All fields     | All data in fields above             | 84                |
| **Total size** |                                    | **5513**          |

> Adding a longer text ﬁeld increased the size of the record by **3.181%**
