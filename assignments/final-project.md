## Final Project

We have so far in this class created CLIs, simple APIs, and containerized our APIs.  We also integrated our APIs via containers with off-the-shelf services such as Redis.

In the last non-programming assignment we looked at HATEOS and some of the benefits that hypermedia can provide with respect to creating collections of APIs that work together. 

In that homework specifically, I showed a conceptual relationship between the `Voters`, `Polls` and `Votes` resources:

```
                ┌──────────┐               
                │          │               
      ┌────────▶│ Poll API │◀───────┐      
      │         │          │        │      
      │         └──────────┘        │      
      │                             │      
┌───────────┐                 ┌───────────┐
│           │                 │ Votes API │
│ Voter API │◀────────────────│           │
│           │                 │           │
└───────────┘                 └───────────┘
```

Note that this design offers maximum flexibility, in that all resources can be used as a starting point to interact with other APIs using hypermedia.  This solution can support simplifying client applications with navigation to any other dependant resource. 

While nice, having excessive flexibility can also lead to more complexity as client applications need to be able to interpret API results and then either use documentation to manually code what to do next, or hypermedia help to drive the integration between APIs.

Sometimes the best API designs are opinionated into how collections of APIs can be used with each other.  While this restricts flexibility, it can make using your APIs easier in the long run. 

Consider if we changed things a little:

```
               ┏━━━━━━━━━━━┓               
      ┌───────▶┃ Votes API ┃◀────────┐     
      ▼        ┗━━━━━━━━━━━┛         ▼     
┌───────────┐        │         ┌──────────┐
│ Voter API │        │         │ Poll API │
└───────────┘        │         └──────────┘
      │              │                │    
      ▼              ▼                ▼    
┌─────────────────────────────────────────┐
│              Cache (Redis)              │
└─────────────────────────────────────────┘
```

The above puts the `Votes` API front and center as the primary abstraction.  From `Votes` we can get collections of polls, and collections of `Voters`.  This also allows us to then dig into specific `Voters` and `Polls`.

For the final assignment, we are going to implement this voting system with these 3 APIs.  You may either stick to the design work from a previous homework or pivot to the design shown above.

#### What you need to do

1. Construct your final system consisting of the 3 APIs that allow appropriate interaction between the APIs.
2. Your solution should use hypermedia to support the intra-API integration
3. The APIs should be able to be deployed using full automation with Docker Compose or Kubernetes. 
4. You should have a simple CLI or scripts that can be executed via the command line or the make utility to demonstrate your solution. 

Please submit your final project in a directory in your git repository that you have been using all term and provide a link to this in the submission.