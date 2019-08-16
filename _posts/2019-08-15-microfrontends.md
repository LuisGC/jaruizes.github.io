---
author: jaruizes
layout: post
title: "Microfrontends"
date: 2019-08-15 01:30
category : Microfrontends
comments: false
tags:
    - microservices
    - microfrontends
---

Today we're hearing "microservices" everywhere. Sometimes the experience is positive, sometimes is negative but the word is in the air. If you don't know what they are, summarizing, this term is usually related to backend architecture and how a system could be decomposed in autonomous and independent pieces, owned and developed by single teams, deployed independently and working all together.

But, when we are developing a product or a feature, we shouldn't forget that the most of them contains backend and frontend services and, if we want to deliver value to our customers we have to deliver end-to-end features. 
Just applying an architectural style to our backend, based on microservices (or not), we won't get enough autonomy to deliver (and maintain) end-to-end features. 

It seems that the next step is being able to delivering value end-to-end. In this context, the term **Microfrontend** really begins to make sense

# End-to-end perspective

Many companies have staterd their way to modernize their architectures in order to build better applications, more scalables and more evolvables. 

Some of theses companies have "adopted" Microservices, others have decided to back to monolith and others are thinking about how improve the way to build software. In the most of them there is something common: they think about services, independent teams, agility, etc but focused on backend systems (APIs, backend services, migration HOST to (micro) services, etc...). 

In this "technical transformation", having an end-to-end perspective is very important:

![why_microfrontends](/images/microfrontends/why_microfrontends.jpg)

- If you build wonderful (backend) services around business capabilities but you don't build an UI associated to those business capabilities your are not building unique business capabilities. You are building differents flavours of the same business capability, that means, you are consuming the same services but you are building similar views in different apps. 

  For instance, in a banking environment, why do you have to develop the account movements view in the main consumer application and you also develop a similar view in the backoffice application or in another application also used by the customers? 

  

- If you achieve a great autonomy in backend systems but you don't do the same in the frontend apps, your (backend) autonomy is not real because you can not deliver end-to-end features to the end user without depending others. 

# Building (little) products not just "services"

Usually when we talk about a software productswe are talking about something with an user interface (UI) with which an end user interacts to perform any action. The user doesn't know how the system is getting data or wether the UI calls an API or no. UI hides backend calls to the end user. 

The end-user interact with the UI and the UI is only the user sees but the UI needs to perform API calls to backend services in order to complete the user requests (get data, update or create data,..., etc). 

If backend services don't work well (or not exist) the UI doesn't provide any value to the user. If backend services work great but there is no UI or the UI doesn't work, the system doesn't provide any value to the user. If several applications have similar business need (features) and the UI looks different in each one or works differently (because UI or services), the user experience is so bad

 ![why_microfrontends](/images/microfrontends/products.jpg)

Well, you can be thinking about APIs and products based on APIs. Your right. This could be a kind of product that a company provide to an other company in order to that company builds an UI over this APIs and provide applications to an end user or only to integrate those two companies. 

The product of the first company is the API but this API, in the most of cases, isn't going to be consumed directly by an end user, so an UI needs to be built becoming a product. The product is offered by the last company but it's an end-to-end product, so we're talking about the same: __providing end-to-end products__.  

# Microfrontends

> __if we could build independent and fully functional components, composed of all the necessary elements (data, services, integrations and user interface), versionables, developed, owned and maintained by a team and integrated at runtime in the application used by end users? They would be like little products or "Microfrontends"__

![why_microfrontends](/images/microfrontends/microfrontends_idea.jpg)

# Microfrontends

I would like to introduce Microfrontends talking about some principles instead of talking about implementations. Why? Microfrotends goes beyond frontend frameworks and their power fight: Angular vs React vs Vue vs ...

> Building microfrontends means adopting an archytecture style, building end-to-end business pieces to be consumed, in runtime, within a frontend application or even by other microfrontends.

Microfrontends are about an architecture style not about an specific implementation. Like some architecture styles, it's important to set:

- which **kind of problems or challenges could resolve** and when it's worth applying or not.
- which are the **main principles and patterns**

Fowler and Lewis wrote a post in 2014 talking about Microservices and what they mean. It was some years ago but I think it is a "master post" we always have to keep in mind. In this post, nine principles are set:

- Componentization via Services
- Organized around Business Capabilities
- Products not Projects
- Smart endpoints and dumb pipes
- Decentralized Governance
- Decentralized Data Management
- Infrastructure Automation
- Design for failure
- Evolutionary Design

 Let's try to apply microservices principles to frontend world



### Componentization via Services

We're used to build UI components, package them into libraries and publish them in the NPM (or bower) repository. This means that every application uses these components by importing them in build time, packaging all together. Although you are using lazy loading and components are loaded on demand, the application consist on a single package "deployed" in the same location. If a component changes, the whole application has to be rebuilt to get the changes and redeployed.

So, in this scenario, autonomy isn't the main characteristic…But, the idea behind "microfrontends" is just the opposite:

> __what if we'd build artifacts that encapsulate end-to-end features and we could consume them at runtime by http calls?__ The idea behind Micro frontends is building "headfull services", that means, delivering end-to-end features by components consumed in runtime by http calls.

Consuming frontends as services means that:

- Microfrontends encapsulate all the backend API calls they need, so they aren't just UI. They are end-to-end components
- Microfrontends expose contracts as services do, input and outputs, events and styles.
- Microfrontends are tested individually
- Microfrontends are deployed independently, so it's not necessary to rebult the parent application is something change in the microfrontend
- Microfrontends are developed and owned by a team



### Organized around Business Capabilities

Microfrontends aren't UI components (later we'll see the differences between them). Microfrontends means implementing end-to-end business features "as a service". Descomposing the system into business capabilities should be the first step if we want to adopt this architecural style.

We do this exercise when we're defining microservices associated to our system but we do not do the same from the UI point of view and we build the same views in many applications. 

It's also true that, in some companies, business capabilities are treated from the frontend but sometimes this exercise is done taking only one application.

In this point, the key is delivering a complete business feature to consumers instead of offering business APIs to the final applications implements the UI. Not confusing this with Open APIs.



### Products not Projects

Building Microfrontends means building products, not projects. A team builds and maintain one or more microfrontends of which is the owner. The team is responsible for the "UI Service" over its full lifecycle.

As the Microfrontend encapsulates backend API calls and the user of the Micro frontend only "receives" the UI Service, the team is also responsible to maintain these API calls updated and working. 

Besides that, several versions of a Microfrontend could be published and be consumed, so the team also has to keep in mind this aspect and managing the retirement of versions out-of-date.



### Smart endpoints and dumb pipes

Currently there are a lot of frameworks or products to build frontend applications and its business logic (ok, presentation logic). Communication between components within the application is supported by the framework choosen capabilities. 

In a Microfrontend style, components are designed and developed as decoupled as possible, so components has to be independent, loaded in runtime and communications between components couldn't be supported by a framework. 

Microfrontends communications must be supported by DOM standards: html tags, attributes and DOM events. It's possible to use some libraries to abstract the frontend event bus but this tool only has to be used to provide publish/sibscribe capabilities. Application logic never is in the event bus.



### Decentralized Governance

Similar to Microservices, a centralized governance implies a single technology o framework. Once a framework is choosen then libraries or some components are built to be delivered to development teams in order to get more productivity. When several applications have been developed, changing the framework becomes a big challenge.

Choosing just one technology or framework we could cause several problems like:

- Not using the best tool to solve a problem
- People gets bore because "it's always the same"
- Locking to a framework, components or even a way (the framework way) to develop.

> If we can load components in runtime by a http call and these components are used as the same way as other HTML components, why do I have to centralize the technology or frameworks?
>

So adopting Microfrontends is not adopting one framework or technology. It's adopting a way to build UI Services that can be consumed at runtime by any application, similar to backend services (http) are consumed.

Microfrontends associated to business features can be developed with the best technology or framework according to the complexity, requirements or business context. 

This doesn't mean that there is no Governance. Governace means principles, rules, patterns,...,etc not technical implementations. Normally, some "core actions" need to be defined to be implemented in every microfrontend. For instance, actions like language changing to suppont multilanguage sites: your company can set the principle that every Microfrontends should listen to an "language changed" event and reacting to it.

Similar with Security concerns. This needs to be defined globally and teams in charge of microfrontends must follow the patterns and rules.



### Decentralized Data Management

In Microservices, when we talk about this subject we mean how to manage data associated to each microservice:  which database or which model the service is going to use.

In Microfrontends, __data management means "backend API calls"__. How the microfrontend is going to get its data? Technically speaking you can be thinking about REST or GraphQL for instance, but the key isn't that, the key is getting autonomy end-to-end in order to deliver a complete business feature. 

Patterns like Backend For Frontends are really helpful in this target because if a microfrontend needs to manage data from several domains to solve some business feature, it's necessary a piece to encapsulate this logic. Or for instance, it could be necessary that the microfrontend shows different amount of information depending of the channel.

Maybe you are wondering about security and how the microfrontends get their data in a secure way. Microfrontends are loaded in runtime, dinamically, some of then in public areas and some of then in private areas. To access this private areas is neccessary that the user is authenticated. This is responsability of the main application, not of the microfrontends. 

Microfrontends need to know if the user is athenticated and how to get the tokens (or whatever you use) in order to invoke backend APIs. In this point, two strategies are possible:

- The main app intercepts all the backend calls and adds the security headers so microfrontends don't have to implement it
- Microfrontends are allowed to get the tokens received when the user is authenticated and they are responsible for generating the security headers they need to access to the backend services.



### Infrastructure Automation

As microfrontends are independent and fully deployable pieces of software, they also need independent processes for build, deploy and publish. 

Remember that the key principle is autonomy so every microfrontend has to be its own CI/CD process. Within a company could be a common pipeline but depending of the technology it's possible that some changes have to be made to adapt CI/CD processes. 

Teams will also manage their microfrontends in production environments, releasing new versions and maintaining current ones.



### Design for failure

In a microfrontends context, where components are loaded in runtime and backend API calls are managed directly by microfrontends it's important to think what happens if something goes wrong. It's necessary to defing a microfrontend's lifecycle in order to know if the microfrontend is ready to be shown or the parent application (or event the parent microfrontend) has to take additional actions like showing a default component or hidiing this area to the user in order to the user isn't conscious of the fail.

As I said, Microfrontends must be associated to a concrete runtime lifecycle to determine if the microfrontend is ready to be shown or not. For instance:

1. Load microfrontend main file
2. Register component
3. Microfrontend ready event received

Besides that, microfrontends must define a contract in which both input attributes and output events (even exceptions) should be defined. With these tools we can react to failure situations and manage them.



### Evolutionary Design

Working with microfrontends means working with components loaded in runtime, totally decoupled. There is pros and cons in this way of working. A relevant pro is that it's possible to change easily every component without affecting others (keeping the contract). It's also easy technology changes. 

But thinking about how to divide the system is crucial, not considering just one application but a set of domains, subdomains and applications so that microfronteds could be consumed by several applications. 

Build a microfrontend just for being consumed in runtime instead building the same functionality inside the application or in a package, could make sense if that business component has many changes or if it should be implemented in other technology, but if you don't have these kind of problems, only are adding complexity. 


# UI Components VS Microfrontends

It's habitual in many companies having a set of components to be used in the different applications. These components could be from tables, layouts, buttons, inputs, etc to complex headers, tables with a lot of UI functionalities or menus structures. This components can be Web Components and being loaded in runtime but they aren't Microfrontends.

When we talk about Microfrontends we are talking about end-to-end business components:

- UI components, views and behaviours
- Backend API calls
- Logic or State

A Microfrontend is a piece that makes sense for the end user. If the final user access to the Microfrontend directly, the final user gets value from that Microfrontend and he could do a business operation. For instance: 

- Microfrontend - Account Detail: UI views and backend API calls for getting the account info
- Microfrontend - Products Catalog: UI views and backend API calls for showing the products catalog
- Microfrontend - Customer Profile: UI views and backend API calls for managing customer profile

UI Components packaging as Web Components could be used in Microfrontends in order to have a common palette of basics components. Web Components are instantiated in runtime and they could be consumed in every HTML application, so they are framework agnostics

# Roadmap to Microfrontends

![why_microfrontends](/images/microfrontends/roadmap.jpg)



# Microfrontends styling 

Bla bla bla ....

# Microfrontends contract 

Bla bla bla ..

# A silver bullet? 

Bla bla bla ....