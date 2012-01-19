---
layout: default
title: Tickets API
description: API to retrieve, create and search tickets
categories: tickets
---

Tickets API
===========

### Retrieving Tickets

#### GET /tickets.json

*returns 15 tickets of the company in the order of their last activity*

#### Status Codes

Success: 200

Failure: 500

#### Parameters

**per_page (optional)**

Specifies the number of tickets to retrieve. 

Must be less than 100. 

Defaults to 15

**page (optional)**

Specifies the page of tickets to retrieve.

Defaults to 1

**spam (optional)**

If _true_, retrieved tickets contain tickets marked as spam.

Defaults to false

**replies (optional)**

If _true_, retrieved tickets contain only tickets with replies.

If _false_, retrieved tickets contain only tickets without replies.

**max_replies (optional)**

Specifies the number of replies that a ticket must have.

This cannot be used with _replies = false_

**assigned_user (optional)**

If _me_, retrieves only the tickets assigned to the current user

If _agent\_id_, retrieves only the tickets assigned to the Agent with id _agent\_id_

If _none_, retrieves only the unassigned tickets

**assigned_group (optional)**

If _mine_, retrieves all the tickets assigned to all the groups of the current user

If _group\_id_, retrieves only the tickets assigned to the group with id _group\_id_

**starred (optional)**

If _true_, retrieves only the starred tickets of the current user

If _false_, retrieves only the non starred tickets assigned to the current user

**label (optional)**

Set to _label\_name_, retrieves only the tickets with the label _label\_name_

#### Example

GET /tickets.json?per_page=10&assigned_user=none&label=unaswered

````
{
  "total":1,
  "current_page":1,
  "per_page":10,
  "total_pages":1,
  "tickets":[
    {
      "id":1,
      "subject":"Welcome to SupportBee",
      "replies_count":0,
      "comments_count":0,
      "last_activity_at":"2012-01-18T15:17:33Z",
      "created_at":"2012-01-18T15:17:32Z",
      "unanswered":true,
      "archived":false,
      "spam":false,
      "starred":false,
      "summary":"test -- Regards, Agent",
      "cc":[],
      "labels":[],
                      
      "requester":{
        "id":21,
        "email":"person37@example.com",
        "name":"Requester",
        "agent":false,
        "picture":{
          "thumb20":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=20",
          "thumb24":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=24",
          "thumb32":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=32",
          "thumb48":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=48",
          "thumb64":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=64",
          "thumb128":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=128"
        }
      },
                  
      "content":{
        "body":"test\n\n-- \nRegards,\nAgent",
        "html":"test<br><div><br></div>-- <br>Regards,<div>Agent</div>",
        "attachments":[
          {
            "id":2,
            "created_at":"2012-01-18T15:17:33Z",
            "filename":"logo.jpg",
            "content_type":"image/jpeg; charset=UTF-8; name=logo.jpg",
              "url":{
                "original":"http://company10.example.com/attachments/2",
                "thumb":"http://company10.example.com/attachments/2?version=thumb"
              }
          }
         ]
      }
                  
    }
  ]                  
}
````

If the ticket is assigned to an agent then the ticket object in the response will contain 

````

"current_assignee":{
  "user":{
    "id":19,
    "email":"person37@example.com",
    "name":"Agent,10",
    "agent":true,
    "picture":{
      "thumb20":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=20",
      "thumb24":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=24",
      "thumb32":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=32",
      "thumb48":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=48",
      "thumb64":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=64",
      "thumb128":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=128"
    }
  }
}

````

If the ticket is assigned to a group then the ticket object in the response will contain 

````
"current_assignee":{
  "group":{
    "id":1,
    "name":"Group 1",
    "picture":{
      "thumb20":"/images/groups/speech-balloon-orange-g20.png",
      "thumb24":"/images/groups/speech-balloon-orange-g24.png",
      "thumb32":"/images/groups/speech-balloon-orange-g32.png",
      "thumb48":"/images/groups/speech-balloon-orange-g48.png",
      "thumb256":"/images/groups/speech-balloon-orange-g256.png"
    }
  }
}
````



#### Searching Tickets

### GET /tickets/search.json

*returns 15 tickets of the company in the order of their last activity matching the search query*

#### Error Codes

Success: 200

Failure: 500

Query Missing: 400


#### Parameters

**query**

Specifies the query or keywords to searched

**per_page (optional)**

Specifies the number of tickets to retrieve. 

Must be less than 100. 

Defaults to 15

**page (optional)**

Specifies the page of tickets to retrieve.

Defaults to 1

**spam (optional)**

If _true_, retrieved tickets contain tickets marked as spam.

Defaults to false

#### Example

The response is similar to ``GET /tickets.json``

GET /tickets.json?per_page=10&query=SupportBee

````
{
  "total":1,
  "current_page":1,
  "per_page":10,
  "total_pages":1,
  "tickets":[
    {
      "id":1,
      "subject":"Welcome to SupportBee",
      "replies_count":0,
      "comments_count":0,
      "last_activity_at":"2012-01-18T15:17:33Z",
      "created_at":"2012-01-18T15:17:32Z",
      "unanswered":true,
      "archived":false,
      "spam":false,
      "starred":false,
      "summary":"test -- Regards, Agent",
      "cc":[],
      "labels":[],
      "current_assignee":{
        "user":{
          "id":19,
          "email":"person37@example.com",
          "name":"Agent,10",
          "agent":true,
          "picture":{
            "thumb20":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=20",
            "thumb24":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=24",
            "thumb32":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=32",
            "thumb48":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=48",
            "thumb64":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=64",
            "thumb128":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=128"
          }
        }
      },
                      
      "requester":{
        "id":21,
        "email":"person37@example.com",
        "name":"Requester",
        "agent":false,
        "picture":{
          "thumb20":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=20",
          "thumb24":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=24",
          "thumb32":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=32",
          "thumb48":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=48",
          "thumb64":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=64",
          "thumb128":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=128"
        }
      },
                  
      "content":{
        "body":"test\n\n-- \nRegards,\nAgent",
        "html":"test<br><div><br></div>-- <br>Regards,<div>Agent</div>",
        "attachments":[
          {
            "id":2,
            "created_at":"2012-01-18T15:17:33Z",
            "filename":"logo.jpg",
            "content_type":"image/jpeg; charset=UTF-8; name=logo.jpg",
              "url":{
                "original":"http://company10.example.com/attachments/2",
                "thumb":"http://company10.example.com/attachments/2?version=thumb"
              }
          }
         ]
      }
                  
    }
  ]                  
}
````



### Creating Tickets

#### POST /tickets.json

*Creates a ticket for the company*

#### Error Codes

Success: 201

Failure: 500

Validation Errors: 400

#### Post Data

This specifies the data in JSON required to create a ticket. A sample JSON request object is 

````
{
  "ticket":{
    "subject" : "Subject",
    "requester_name": "John Doe",
    "requester_email": "john@example.com",
    "content_attributes":{
      "body": "Creating a ticket",
      "body_html":"<p>Creating a ticket</p>",
      "attachment_ids":[1240, 1241]
    }
  }
}
````

**subject**

Specifies the subject of the ticket.

Required

**requester_name**

Specifies the name of the requester of the ticket.

Required

**requester_email**

Specifies the email of the requester of the ticket.

**body/body_html**

Specifies the content of the ticket. Either body or body_html must be present

**attachment_ids**

Specifies the attachments of the ticket. See Attachment API to upload attachments to SupportBee

#### Example Response

````
"ticket":{
  "id":1,
  "subject":"Welcome to SupportBee",
  "replies_count":0,
  "comments_count":0,
  "last_activity_at":"2012-01-18T15:17:33Z",
  "created_at":"2012-01-18T15:17:32Z",
  "unanswered":true,
  "archived":false,
  "spam":false,
  "starred":false,
  "summary":"test -- Regards, Agent",
  "cc":[],
  "labels":[],
    "current_assignee":{
      "user":{
        "id":19,
        "email":"person37@example.com",
        "name":"Agent,10",
        "agent":true,
        "picture":{
          "thumb20":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=20",
          "thumb24":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=24",
          "thumb32":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=32",
          "thumb48":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=48",
          "thumb64":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=64",
          "thumb128":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=128"
        }
      }
    },
                    
  "requester":{
    "id":21,
    "email":"person37@example.com",
    "name":"Requester",
    "agent":false,
    "picture":{
      "thumb20":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=20",
      "thumb24":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=24",
      "thumb32":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=32",
      "thumb48":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=48",
      "thumb64":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=64",
      "thumb128":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=128"
    }
  },
                
  "content":{
    "body":"test\n\n-- \nRegards,\nAgent",
    "html":"test<br><div><br></div>-- <br>Regards,<div>Agent</div>",
    "attachments":[
      {
        "id":2,
        "created_at":"2012-01-18T15:17:33Z",
        "filename":"logo.jpg",
        "content_type":"image/jpeg; charset=UTF-8; name=logo.jpg",
        "url":{
          "original":"http://company10.example.com/attachments/2",
          "thumb":"http://company10.example.com/attachments/2?version=thumb"
        }
      }
    ]
  }
                
}
````


### Showing a Ticket

#### GET /tickets/_id_.json

*Retrieves the ticket specified by the _id_*

#### Error Codes

Success: 200

Failure: 500

Not Found: 404

#### Example 

GET /tickets/1.json

````
"ticket":{
  "id":1,
  "subject":"Welcome to SupportBee",
  "replies_count":0,
  "comments_count":0,
  "last_activity_at":"2012-01-18T15:17:33Z",
  "created_at":"2012-01-18T15:17:32Z",
  "unanswered":true,
  "archived":false,
  "spam":false,
  "starred":false,
  "summary":"test -- Regards, Agent",
  "cc":[],
  "labels":[],
    "current_assignee":{
      "user":{
        "id":19,
        "email":"person37@example.com",
        "name":"Agent,10",
        "agent":true,
        "picture":{
          "thumb20":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=20",
          "thumb24":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=24",
          "thumb32":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=32",
          "thumb48":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=48",
          "thumb64":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=64",
          "thumb128":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=128"
        }
      }
    },
                    
  "requester":{
    "id":21,
    "email":"person37@example.com",
    "name":"Requester",
    "agent":false,
    "picture":{
      "thumb20":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=20",
      "thumb24":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=24",
      "thumb32":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=32",
      "thumb48":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=48",
      "thumb64":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=64",
      "thumb128":"https://secure.gravatar.com/avatar/08a668f83cd9e933edca2beb59aa57e2.png?r=PG&s=128"
    }
  },
                
  "content":{
    "body":"test\n\n-- \nRegards,\nAgent",
    "html":"test<br><div><br></div>-- <br>Regards,<div>Agent</div>",
    "attachments":[
      {
        "id":2,
        "created_at":"2012-01-18T15:17:33Z",
        "filename":"logo.jpg",
        "content_type":"image/jpeg; charset=UTF-8; name=logo.jpg",
        "url":{
          "original":"http://company10.example.com/attachments/2",
          "thumb":"http://company10.example.com/attachments/2?version=thumb"
        }
      }
    ]
  }
                
}
````
