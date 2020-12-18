# Pluralsight Course: SignalR

Project code: <https://github.com/brcrista/Wired-Brain>

I went through the course, but also decided to half-rewrite the examples myself.  I basically started from an ASP.NET Core template in VS 2019 and copied in the important bits, but refactored some of the code to make it easier to understand.  For example, the code from the course didn't use async / await in JavaScript.  It also had some straight-up bugs: it wasn't sending the body of the POST correctly in JavaScript (the args were always null), it didn't actually use the order number for anything, and you couldn't submit a new order without refreshing the page.

It took much longer, but I ended up learning a lot more from doing this rather than just passively learning.

What did I learn?
* Wiring up a basic ASP.NET Core controller with a JavaScript client
* OPTIONS requests in the browser's CORS flow
* JavaScript's Fetch API
* Refresher on setting up an ASP.NET Core project: controller routes, data binding
* How to read the request body in pure Node
* How System.Random works in .NET
* Working with thread-safe data structures in .NET
* Lookahead with iterators
