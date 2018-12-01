+++
title = "The easiest part of programming: Naming things"
Description = ""
Tags = ["coding"]
Categories = []
date = "2018-12-01T09:51:55+01:00"
+++

Each system has its own believes and "common truths". With system, I mean areas or professions. Education, Science, cooking etc. Each place where people come together and build a closed system where they operate in. From within, it's almost impossible to change a system, it's just possible from the outside and by letting the old system die and create parallel to that a new one.

Programming is a system for me. With its own paradigms, models and behaviours. One commin believe is that "naming things" is hard. And I followed along, had big arguments about how and what to name variables, methods, classes and whatnot. 

Though, at my current projected I encouterned something strange: I reviewed a Pull Request from a team mate and suggested a name change. The person commented a few minutes later and said: "I don't particularly care about the name, so I'll change it and update the PR." 

I was a bit buffled. Since in my head it was not about the name but what the variable represented. I did a bit of thinking since then and figured out common misconceptions about naming things. <a href="https://www.slideshare.net/pirhilton/how-to-name-things-the-hardest-problem-in-programming">Some people go even so far to take advice from famous writers about how to name things</a>.

Which, in the end, is not the point. 

You sometimes don't even have to read a whole book about programming, sometimes the golden nuggets are already in the preface. Like in <a href="https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book.html">"Structure and Interpretation of Computer Programs"</a>. There it states:

*"We control complexity by building abstractions that hide details when appropriate. We control complexity by establishing conventional interfaces that enable us to construct systems by combining standard, well-understood pieces in a ``mix and match'' way. We control complexity by establishing new languages for describing a design, each of which emphasizes particular aspects of the design and deemphasizes others."*

### If there are talks/blog posts about solving a particual problem, then thats rarly the problem to solve

If there is a common problem to solve within a complex system (like the programming community), and its not yet solved, then   
a) That's not the problem to solve but has some underlying issue   
b) Our closed mindset doesn't allow us to think outside of the box to solve the underlaying issue  

With naming things, my take is we have to handle option a) here. 

### Form follows function aka architecture

So if we accept that "naming things" is hard and not yet solved, and there are still tons of talks and blog posts about it (red flag), then thats not the actual issue but we need to find the underlaying one. 

If we go one level higher (or deeper, depending on how you see it :)), we got to realise that the abstraction we are trying to hide is  
- not clear to us  
- not obvious and easy to understand  
- has to operate within an already complex, not well understood system (aka code base)  
 
The problem I encountered in 10 years of programming now is not calling a variable `Scheduler` but `TaskManager`. Maybe the reason is that I am not a native english speaking person, but my guess is that in a clear defined and well architectured code base, I would understand both abstractions and would carry on to the problem I actually have to solve.

However, I encountered two large "naming" problems. 

1. Calling a NodeJS/koa middleware `validateUser()` with the following signature:

```
const validateuser = () => async (ctx, next) => {
  const user = await userModel.get(ctx.params.userId);

  if (!user) {
    ctx.throw(404, `User does not exist: ${ctx.params.userId}`);
  }

  // Set the user to the ctx to be available for later
  ctx.request.user = user;

  await next();
};
```

A typical argument here is: The name validateUser doesn't represent the full behind-the-scenes work done from the function. We have a database call to get the user with the id, if it's not found we return a 404 and if the user is found we add it to the request to have access to it later in the app.

Because once you created this function, and call it every time on your routes:
```
app
  .get(
    '/v1/users/:userId',
    validateUser(),
    async ctx => {...

app
  .put(
    '/v1/users/:userId',
    validateUser(),
    async ctx => {...
```

then a future developer in a year from now will look at the code and trying to figure out how to set the user to the request object so he or she can use it later on in the program. The name `validateUser` doesn't indicate at all that the `user` is added to the request object here.

You have to options now:   
1. Thinking about a better name which includes the behaviour of adding the user to the request object  
2. Split the function into two or three pieces, and calling it like this:  

```
app
  .get(
    '/v1/users/:userId',
    validateUser(),
    addUserToRequest(),
    async ctx => {...`
```

From there, you can even question the name `validateUser` again and call it `checkIfUserExists`:

```
app
  .get(
    '/v1/users/:userId',
    checkIfUserExists(),
    addUserToRequest(),
    async ctx => {...`
```

Which is more precise and represents actually what it does. 

You could call this "naming problems", but I think naming things is actually a writers or poets dilemma, because of audiences and target groups mixed with own feelings and representations of the world.

As a software engineer, you are not a poet. You can sometimes get away with a bit more ugly names (like `checkIfUserExists`), because I much rather read this during my hunt for a bug then `validateUser`, since it is:
- Not the solely purpose of the function 
- Validating is not really happening here since we don't do checks if the user typed in its first and last name and such

2. My second "naming" problem was the following:

```
class User {
    constructor(yamlPath) {
        this.yamlPath = yamlPath;
    }

    init(roles) {
        const defPath = path.join(__dirname, '..', this.yamlPath);
        const yamlFile = fs.readFileSync(defPath, 'utf-8');
        const yamlContent = yaml.safeLoad(yamlFile);
        this.permissions = yamlContent;
        this.roles = roles;
    }
}

const initRolesAndPermissions = async (yamlPath) => {
    user = new User({ path: yamlPath});
    user.init();
}

module.exports = {
  initRolesAndPermissions,
};

```

You can argue about the "bad" code of course, but the first discussion I was bringing up was: The method `user.init()` doesn't init the user but is just setting roles. You can call this "discussing about names" but in my view, it's not about naming, it's about abstracting meaning so I don't have to look behind the abstraction any more. And of course, the method `init` is just a typical `setter` of a class so lets rename it to `setRoles` and done. 

### The purpose of naming things in Programming

It is about abstracting meaning and knowledge. Also from the <a href="https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book-Z-H-7.html">preface</a>:

"They should know what not to read, and what they need not understand at any moment. They should feel secure about modifying a program, retaining the spirit and style of the original author." 

So if I have a filter to find a specific user:

```
const findUser = (id) => {
    const listOfUsers = db.getUsers();
    return listOfUsers.filter(a => a.id === id);
}
```

Some people might say "Don't call it `a` in the filter but `filteredUser` or something like that. But my take is: I will probably never ever touch this method again. It's small, it's precise, and sort of nice looking. A developer who comes into the project in a year from now immediately knows what's going on and she can use this method without second guessing. 

You can argue to abstract the db access and make it obvious that it's a bit expensive to run this, but it has nothing to do with the name of the method nor the name of the variable inside the filter. 

### Summary

To go back to my previous statement: It's not about naming but "something else", an underlaying issue. The underlaying issue is most of the time the understanding of the system by the developer. If you get hired to do a project or join a company and have to contribute code on your first day: It's never about your ability to name things. It's much harder then that. It's understanding what the code you wrote does, what it should express.

Always remember: You don't name things, you abstract meaning. Which is much harder to do. But once you are realsing this task, you will write more precise code, ask more questions along the way and treat the code base what it is: A construction manual for the developer who joins the project in 5 years and has no idea why certain things happen.

But if you have one goal in mind, **to abstract meaning**, then your code will be more precise, you will naturally use smaller methods and functions, and you will have a gut feeling of when to stop using OOP and put a combination of functional programming and classes to use. 

Bad names will come harder to your mind, because if you look at your produced code you will know what you abstracted and why. 