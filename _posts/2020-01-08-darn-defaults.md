---
layout: post
title: Darn Defaults
state: draft
---
I want to share a short tale about about an adventure with Java & Spring properties, in the hopes I can prevents others for falling for the same
issues my team did. This is a story about defaults-gone-wrong.

## The Setup

A little bit of background is needed to have a comprehensive picture. This story revolves around our `Product API`, our `Authorization API`, 
and the company's `Authorization Management System` or `ams` for short.

The `Product API` is how clients interact with product data, assuming they are authorized.
The company's `ams` is the source-of-truth on whether a client is authorized or not. The `Authorization API` exists
to mediate interactions between our Product API and this source-of-truth.


The `Authorization API` supports an in-memory cache of previously authorized clients, and a database fallback in case 
the cache is empty _and_ `ams` is down.

So the auth flow is like this:

```go
function isUserAuthorizedForResource(userID, resourceID) bool {
  var isAuthorized bool
  var err error
  
  isAuthorized, err = inMemoryCache.getAuthorization(userID, resourceID)
  if err == nil {
    // user was in our cache, return their auth state
    return isAuthorized
  }
  
  // user not in cache, check the auth system
  
  isAuthorized, err = authSystem.getAuthorization(userID, resourceID)
  if err == nil {
    return isAuthorized
  }
  
  // could not get to auth system, fall back to database
  isAuthorized, err = database.getAuthorization(userID, resourceID)
  if err == nil {
    return isAuthorized
  }
  
  // something really went wrong. cannot authorize user.
  return false
}
```

## The Problem

A client reached-out about an authorization error they were receiving. They had recently submitted a request to the
`Authorization Management System`, `ams`, to gain access to a particular API resource. But when attempting to access
said resource, they received an auth error.

Thinking over the list of possible explanations for the problem, I first checked our source-of-truth, the `ams`. And yes, they did in fact have the correct authorization. So that's not the problem.

Next, I replicated the request to our `Authorization Server`. Bingo! Unauthorized.

The server's in-memory cache must have their userID and available resources cached without the most recent addition. Simply
clear the cache for that user, let it repopulate, and everything's right with the world... Right?

Wrong.

Clearing the cache did not help. So either the `ams` is broken, and reports the correct authorization setup in the UI but not the API (unlikely), or we are falling back to our database. But that should only happen is the `ams` is down...
