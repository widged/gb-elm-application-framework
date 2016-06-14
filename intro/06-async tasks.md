**Elm 0.??**, **please ignore** 

# TASKS

- describe async operations
- may fail or succeed
- composable


# COMPOSABILITY

```elm
getOffers : String -> Task Http.Error (List Offer)
getOffers customerName =
  let
    url = "http://some.api/customer?name=" ++ customerName
    offersUrl id = "http://some.api/customer/" ++ id ++ "/offer"
  in
    Http.get customerDecode url
      `andThen` (\c -> Http.get offersDecoder (offersUrl c.id))
```

This code does not send any request:

```elm
getSiiliOffice : Task Http.Error String
getSiiliOffice =
  Http.getString "http://api.zippopotam.us/pl/50-073"
```

(source: ???)

# Tasks

_See the [docs](http://package.elm-lang.org/packages/elm-lang/core/4.0.0/Task) will give a partial overview._

Tasks make it easy to describe asynchronous operations that may fail. It is useful for HTTP requests, writing to a database, getting the current time, or printing things out to the console. For example, maybe we have a task with the type (`Task String User`). Generally stuff that interacts with services outside your program, takes a long time, or may fail. 

When we perform the task, it will either fail with a `String` message or succeed with a `User`. So this could represent a task that is asking a server for a certain user.

For more information, see the [Elm documentation on Tasks](http://guide.elm-lang.org/error_handling/task.html).

(source: [an introduction to elm](https://evancz.gitbooks.io/an-introduction-to-elm/content/error_handling/task.html) and [source code comments](https://github.com/elm-lang/core/blob/4.0.0/src/Task.elm))

### Building Blocks

One of the simpler tasks is getString which tries to get a string from a given URL. The type is like this:

```elm
getString : String -> Task Error String
```

So we see the URL as the argument, and it is giving back a task. Again, this does not mean we are actually making the GET request. We are just describing what we want to do, like how writing down “buy milk” does not mean it magically appears in your fridge.

The interesting thing here is the return type Task Error String. This is saying: I have a task that may fail with an Http.Error or succeed with a String. This makes it impossible to forget about the bad possibilities. The server may be down. The internet connection may be down. The server may respond with bad data. Etc. By making these possibilities explicit, an Elm programmer has to consider these cases. In the end, it means they build more reliable applications.

Note: This is very similar to the Result type we saw in the previous section. You explicitly model failure and success. You then put things together with map and andThen. The key difference is that a Result is already done and a Task is not. You can pattern match on a Result and see if it is Ok or Err because it is complete. But a task still needs to be performed, so you do not have that ability anymore.

Another one of the simpler tasks is Time.now which just gets the current time:

```elm
Time.now : Task x Time
```

There are a few things to notice here. First, notice that Time.now has no arguments. There is nothing to configure here, you just have “get the current time” described as a task. Second, notice that the error type is the type variable x. When we saw Http.getString it had a concrete error type Http.Error. The Time.now task is different in that it will not fail in a special way. You will always get the time back. This type variable x is basically saying “I am not going to force you to handle a particular type of errors” because it does not produce any.


(source: [an introduction to elm](https://evancz.gitbooks.io/an-introduction-to-elm/content/error_handling/task.html))

### Chaining Tasks

It is great to do one task, but to do anything interesting, you probably need to do a bunch of tasks in a row. This is where the andThen function comes in:

andThen : Task x a -> (a -> Task x b) -> Task x b
The short summary is: we try one task and then we try another task.

But to break it down a bit more, andThen takes two arguments:

A task that may succeed with a value of type a
A callback that takes a value of type a and produces a new task.
First you try to do Task x a. If it fails, the whole thing fails. If it succeeds, we take the resulting a value and create a second task. We then try to do that task too. This gives us the ability to chain together as many tasks as we want.

For example, maybe we want to GET stock quotes from a particular time. We could do something like this:

```elm
getStockQuotes =
  Time.now `andThen` \time ->
    Http.getString ("//www.example.com/stocks?time=" ++ toString time)
```

So we get the current time and then we make a GET request.

(source: [an introduction to elm](https://evancz.gitbooks.io/an-introduction-to-elm/content/error_handling/task.html))