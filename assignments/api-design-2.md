## API Design Assignment (Part 2)

**HEADS UP - Please don't freak out by the length of this assignment, its actually not that much work!  This material is actually lecture material that I will be covering to help you with the design objectives of what I am asking you to do for this assignment.**

### Directions
For this assignment we will be examining how to extend our Voter API into a more workable election platform.

If you recall, we have been working on a simple Voter API that manages voter information about people, and maintains a collection of the polls that they participated in and the date that they voted.  The Voter API does not manage the polls themselves, nor does it keep track of exactly what a voter selected in a poll.

For a reminder the key data structures in the Voter API are:

```go
type voterPoll struct {
	PollID   uint
	VoteDate time.Time
}

type Voter struct {
	VoterID     uint
	FirstName   string
	LastName    string
	VoteHistory []voterPoll
}
```

We already covered this, but some sample code to create a hard-coded sample voter could be achieved as follows:

```go
func NewSampleVoter() *Voter {
	return &Voter{
		VoterID:     1,
		FirstName:   "John",
		LastName:    "Doe",
		VoteHistory: []voterPoll{
			{PollID: 1, VoteDate: time.Now()},
		},
	}
}
```

The above creates a new voter named "John Doe", gives him an ID of 1, and captures that he voted in a poll with ID of 1 right now (`time.Now()`)

### Taking it to the next level

Our ultimate goal is to create 2 additional APIs:

1. `PollAPI`: An API to create simple polls,
2. `VotesAPI`: An API to collect the result from a voter (aka making a vote) on a specific poll.  

Lets look at these next.

### The `Poll` API

The purpose of the `Poll API` is to create and maintain a collection of _Polls_.  To keep things simple our polls will be a simple question with one or more allowable answers.

Using go we can use something like the following data structures to manage individual Polls:

```go
type pollOption struct {
	PollOptionID    uint
	PollOptionText string
}

type Poll struct {
	PollID       uint
	PollTitle    string
	PollQuestion string
	PollOptions  []pollOption
}
```

Note that this is a very similar approach to the one we took for voters.  A `Poll` has an ID, Title, Question, and a slice of `pollOptions`.
A `pollOption` has an ID, and string for the text of the answer.

To make this a little less abstract, look at the function below that creates a hard-coded Poll:

```go
func NewSamplePoll() *Poll {
	return &Poll{
		PollID:       1,
		PollTitle:    "Favorite Pet",
		PollQuestion: "What type of pet do you like best?",
		PollOptions: []pollOption{
			{PollOptionID: 1, PollOptionValue: "Dog"},
			{PollOptionID: 2, PollOptionValue: "Cat"},
			{PollOptionID: 3, PollOptionValue: "Fish"},
			{PollOptionID: 4, PollOptionValue: "Bird"},
			{PollOptionID: 5, PollOptionValue: "NONE"},
		},
	}
}
```

This poll has an ID of `1` and is setup to ask a voter to select their favorite type of pet from the 5 options shown - Dog, Cat, Fish, Bird, or NONE.

### The `Votes` API

The purpose of the `Votes API` is to create and maintain a collection of _Vote_ records.  To keep things simple our vote records will capture a unique ID for the vote itself, the ID of the Voter, the ID of the Poll, and the selection the voter made (`VoteValue`).  See below:

```go
type Vote struct {
	VoteID    uint
	VoterID   uint
	PollID    uint
	VoteValue uint
}
```

As an example, consider the following code:

```go
func NewSampleVote() *Vote {
	return &Vote{
		VoteID:    1,
		PollID:    1,
		VoterID:   1,
		VoteValue: 1,
	}
}
```

### Tying it all Together

In our ultimate application, and design challenge here, we are seeing a realistic aspect of APIs in that they need to work together.  Considering the above:

1. Calling `NewSampleVoter()` would create a new voter named John Doe with ID=1, and a record that he voted on a Poll with ID=1 right now.
2. Calling `NewSamplePoll()` would create a new poll with ID=1 that asks voters about their favorite Pet.  They can pick Dog, Cat, Fish, Bird or NONE, each has an respective `PollOptionID` number.
3. Finally calling `NewSampleVote()` would record that Voter 1 who is John Doe, Voted on Poll 1, which is the Favorite Pet poll, and selected VoteValue 1  which is Dog.  Thus John Does favorite pet is a Dog!

Now that we have the _big picture_ lets dive in and look at what these 3 APIs can do on their own, and where they must interact with each other.

What can be done independently?
1. We can use the Voter API to create a new Voter, but only with an empty `VoteHistory`.
2. We can use the Poll API to create a new Poll.  This is actually the only completely independent API.

Where are the API dependencies?
1. Before we can record a `VoteHistory` record for a voter, we must have that Voter create a `Vote`.
2. But before we create a `Vote` we must create a `Poll` and and have a valid `Voter` because the `Vote` structure must reference a valid `Voter` (by ID), and a valid `Poll` (by ID).

An example:

Our objective is to have Voter John Doe vote in the favorite pet poll and indicate that his favorite pet is a dog.

1. We need to create a new Voter record for John Doe via `POST /voters` and a new favorite pet poll via `POST /polls`.  Note these can be done in any order.
2. Now we can collect the vote that John Doe's favorite type of pet is a dog.  We can do this via `POST /votes`.
3. We can now conclude, by registering that vote in John Doe's `VoteHistory` via `POST /voters/1/polls` indicating that John Doe voted in the favorite pet poll.

We can look at these graphically:

```
                ┌──────────┐               
                │          │               
      ┌────────▶│ Poll API │◀───────┐      
      │         │          │        │      
      │         └──────────┘        │      
      │                             │      
┌───────────┐                 ┌───────────┐
│           │                 │           │
│ Voter API │◀────────────────│ Votes API │
│           │                 │           │
└───────────┘                 └───────────┘
```

### Conclusion

The above highlighted how APIs need to work together to implement realistic systems.  We used identifiers to link these resources together, very similar to an approach you would use with databases. 

While this design approach is OK, it requires somebody using these collection of APIs to understand how they relate to each other.  For example, if I call `GET /voters/1/polls` and get back that voter 1 voted on a poll with ID=1, I would then have to know to call `GET /polls/1` to get information on this poll.  Also, if I called `GET /votes/` and one of the records came back like above with VoterID=1, PollID=1, and VoteValue=1, I would have to know the right APIs to get more details to recover that John Doe (Voter 1), voted on the Favorite Pet Poll (Poll 1), and chose Dog (PollOptionID 1).

While this is commonly done, there is a better way.  That is the goal of your assignment.

### The Assignment - FINALLY

Finally, this is what you need to do.

For reference, remember part 1 of this assignment involved reviewing this video - https://www.youtube.com/watch?v=P0a7PwRNLVU.

For this assignment I want you to do some independent research on Hypermedia as the engine of application state (HATEOAS).  Here is the wikipedia page - https://en.wikipedia.org/wiki/HATEOAS.  You can also use ChatGPT, other google resources, etc.  Other keywords that can help you are `hypermedia`.

After you grasp some of these concepts, please do the following:

1. Make some proposals to change the APIs above to incorporate hypermedia into the design of our voting application.  Note I dont want you creating new APIs (stick to the 3 above), but describe how you would change the API structures to better support a hypermedia driven approach.  Note you can add additional fields to support the `hypermedia` concepts or change existing fields.  
2. Write a brief description of how these APIs would work together a little better using these concepts. Focus on the perspective of the user of your API, how would this better support the interactions between the APIs supporting an application?
3. Provide at least 2 references that you found helpful during this activity.  Note you dont need to formally cite them, just a link would be OK.  





