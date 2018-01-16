const line = require('@line/bot-sdk');
const express = require('express');
const axios = require('axios');
 
const config = {
  channelAccessToken: "W8w8ycLOVUEK93ol8d11zwDaIWYOnilqPIudmg9HpczDD8rGuiHeh5wCJy9s6yWpkd4ccUUIrk+tYoPzy898okcu1hBOOJaWsC0X3gkUUPBIiSFhYMKaRBo8q1oSS8FuIQeX93dL/eGIPFSpn/264wdB04t89/1O/w1cDnyilFU=",
  channelSecret: "d102d9d6e93fceb298f869b30cf0573a",
};
 var Datastore = require("nedb");
var db = {};
// create LINE SDK client
const client = new line.Client(config);
const app = express();
 db.chats = new Datastore({ filename: 'path/to/datafile', autoload: true });
 
// register a webhook handler with middleware
// about the middleware, please refer to doc
app.post('/callback', line.middleware(config), (req, res) => {
  Promise
    .all(req.body.events.map(handleEvent))
    .then((result) => res.json(result))
    .catch((e)=>{
      console.log(e);
    });
 
});
 
function handleEvent(event);
     
    var pesan = event.message.text.toLowerCase();
 
    if(pesan == "hai"){
      const echo = { type: 'text', text: "hai juga#" };
      return client.replyMessage(event.replyToken, echo);
    }
     if(pesan.search("hello") > -1
     && pesan.search("bos") > -1)
     {
      const echo = { type: 'text', text: "po undang undang" };
      return client.replyMessage(event.replyToken, echo);
    }
 
    const echo = { type: 'text', text: "Koe ngomong opo to?" };
    return client.replyMessage(event.replyToken, echo);
}
 
// listen on port
const port = 3000;
app.listen(port, () => {
  console.log(`listening on ${port}`);
});
