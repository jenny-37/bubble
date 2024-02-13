
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






# Concepts, definitions and fineprint


## Performance


## Capacity


## Server-side and client-side


## Responsiveness


## Third-party services


## Editor performance


## Experience level


## A word on planning


## The difference between best practices and tools






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

