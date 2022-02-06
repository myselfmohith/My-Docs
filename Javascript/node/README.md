[Go back](./../README.md)

## Contents

- [Mongoose](#mongoose)
- [Socket.io](#socketio)

### Mongoose

Mongoose is a mongodb driver for node js

| **CRUD** |                          |                                              | Return       |
| :------- | :----------------------- | :------------------------------------------- | :----------- |
| CREATE   | `new`                    | Initialize new document model with schema    |              |
|          | `.save()`                | Save the Document to Data base               | doc saved    |
| READ     | `.find({ /* .. */ })`    | Find all the documents Matching              | Array of doc |
|          | `findOne({ /* .. */ })`  | Find a single document                       | Single doc   |
|          | `findById({ /* .. */ })` | Find a single document by ID                 | Single doc   |
| UPDATE   |                          | Best method is to find the doc and           |              |
|          |                          | use `.save()`                                |              |
| DELETE   | `.remove()`              | Find the doc and use this method             | \*\*Clarify  |
| TIPS     | `.select(<str>)`         | Using this we can select only required filed |              |

```javascript
// .select(<str>) example, <str> is the list of attribute you need separate by space
//                         If you specify "-"before attribute it will exclude it from the data
User.find()
    .select("username -password dob")   // return only username and dob ,not password
    .then(user => ... )
    .catch(err => ...)
```

**NOTE :** The above function are all promises they always return data or return `null`

#### POPULATE

The best part of **SQL** is joins, with the help of mongoose we can implement joins in **NO-SQL** too.To do so, add the `{ type: Schema.Types.ObjectId, ref: '<Collection Name>' }`.

```javascript
// consider the schema ==========
const UserSchema = new mongoose.Schema({
  username: String,
  posts: [
    {
      type: mongoose.Schema.Types.ObjectId,
      ref: "Post",
    },
  ],
});
const PostSchema = new mongoose.Schema({
  content: String,
  author: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "User",
  },
});
const Post = mongoose.model("Post", PostSchema, "posts");
const User = mongoose.model("User", UserSchema, "users");

// TO use populate ===============

// EX - 1
User.find().populate("posts"); // Join the posts to results

// EX - 2
User.find().populate({ path: "posts", select: "content" }); // Joins the posts with only content

// EX - 3 [NESTED]
User.find().populate({
  path: "posts",
  populate: {
    path: "author",
    select: "username",
  },
}); // Joins the posts and inside the posts it again populate author with only username
```

### Socket.io

```javascript
io.on("connection", (socket) => {

  ...
  ...

});
```

| Methods                                            | Note                                                                                                                                                                   |
| :------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `socket.emit(/* ... */);`                          | basic emit                                                                                                                                                             |
| `socket.broadcast.emit(/* ... */)`                 | to all clients in the current namespace except the sender                                                                                                              |
| `socket.to("room1").emit(/* ... */)`               | to all clients in room1 except the sender                                                                                                                              |
| `socket.to("room1").to("room2").emit(/* ... */)`   | to all clients in room1 and/or room2 except the sender                                                                                                                 |
| `io.in("room1").emit(/* ... */)`                   | to all clients in room1                                                                                                                                                |
| `io.of("myNamespace").emit(/* ... */)`             | to all clients in namespace "myNamespace"                                                                                                                              |
| `io.of("myNamespace").to("room1").emit(/* ... */)` | to all clients in room1 in namespace "myNamespace"                                                                                                                     |
| `io.to(socketId).emit(/* ... */)`                  | to individual socketid (private message)                                                                                                                               |
| `io.local.emit(/* ... */)`                         | to all clients on this node (when using multiple nodes)                                                                                                                |
| `io.emit(/* ... */)`                               | to all connected clients                                                                                                                                               |
| **WARNING**                                        | `socket.to(socket.id).emit()` will NOT work, as it will send to everyone in the room named `socket.id` but the sender. Please use the classic `socket.emit()` instead. |
| `socket.emit("question", (answer) => { ... })`     | with acknowledgement                                                                                                                                                   |
| `socket.compress(false).emit(/* ... */)`           | without compression                                                                                                                                                    |
| `socket.volatile.emit(/* ... */)`                  | a message that might be dropped if the low-level transport is not writable                                                                                             |

<h6 align="right"><a href="https://socket.io/docs/v3/emit-cheatsheet/" target="_blank">Source</a> </h6>

> **SILLY HACK :** We can assign the `io` to a `app.io` and use it in the routes.
