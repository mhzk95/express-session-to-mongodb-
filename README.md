# express-session-to-mongodb-
Connecting express-session to mongodb database using connect-mongo

```js
//npm install express express-session mongodb connect-mongo

const express = require('express')
const app = express()
const session = require('express-session')
const MongoStore = require('connect-mongo')

app.use(session({
    secret: 'keyboard cat',
    resave: false,
    saveUninitialized: true,
    cookie: { maxAge : 200000 },
    store: MongoStore.create({ mongoUrl:'mongodb://localhost:27017/sampleDB'  })
  }))

  //counting the number of visits to the website
  
app.get('/',(req,res) => {
    if(req.session.viewcount){
        req.session.viewcount = req.session.viewcount + 1
    }
    else req.session.viewcount = 1
    res.send(`you have visited the page ${req.session.viewcount} times`)
})

app.listen(3000, () => console.log('listening to port 3000'))

```
