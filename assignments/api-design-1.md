## API Design Assignment (Part 1)


### Directions
Now that we have been played with the basic concepts of APIs, for example, implementing them and understanding how we interact with them via routes and HTTP verbs, we are now going to place a little more emphasis on API design best practices.

In the real world, APIs tend not to be one-off HTTP endpoints, to create realistic applications APIs come in "families", and often time have to work together.  

Consider the diagram below highlighting a simple e-commerce application:

```
┌─────────────┐       ┌────────┐                
│             ├──────▶│Shopping│                
│             │       │Cart API│                
│             │       └────────┘     ┌─────────┐
│   Mobile    │            ▲         │Inventory│
│ Application │            │         │   API   │
│             │            │         └─────────┘
│             │       ┌────────┐          ▲     
│             │       │Catalog │          │     
│             ├──────▶│  API   │──────────┘     
└─────────────┘       └────────┘                
```

In the simple picture shown above we have 3 different APIs supporting a hypothetical e-commerce mobile application.  The main objective is to understand that APIs can be executed in different contexts.  For example:

1. The `Shopping Cart` and `Catalog` APIs can be executed directly from the external mobile application.  Thus, these APIs provide, a secure, and useful service to the mobile application itself.
2. The `Shopping Cart` API is also used by `Catalog` API to enrich its capabilities.  For example, a reasonable approach could have the CartAPI export a `POST /cart/checkout` endpoint to complete a purchase directly from the mobile app, and another endpoint `POST /cart/item` to add a product from the catalog to the shopping cart.  In this scenario, the 2 endpoints are intended to be used by different clients - one the external application, the other from an API.
3. The `Inventory API` is an example of a _Backend API_, in that its purpose is to support other APIs and is not intended to be executed by the external application directly.

Over the next few weeks we will be covering API design best practices.  This assignment will help establish some context for API design.

### Assignment

Start by watching the following video from the 2018 Google Cloud Next Conference on Designing Quality APIs - https://www.youtube.com/watch?v=P0a7PwRNLVU.  This video does a nice job introducing some API best practices that we will be incorporating into our voting application.

The purpose of this assignment is to provide you some background on this topic before we discuss in class. After viewing the video, please submit the following:

1. No more than a one paragraph (a few sentence summary) of the video highlighting one key API design aspect that you took away from the content
2. Any questions that you have after watching this video.  I don't expect you to understand everything, and this part will help me prepare our in-class discussion on the topic. If you got the general idea, you can just say that you have no questions.

These are basically _free_ points, there is no real way to get things right or wrong with this assignment as its intended to provide a foundation for our work on API design moving forward. 

