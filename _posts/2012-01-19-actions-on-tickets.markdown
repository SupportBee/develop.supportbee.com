---
layout: default
title: Tickets API
description: Describes the Actions on a ticket
categories: tickets
---

Archiving / Un-Archiving Tickets
===============================

### Archiving Tickets

#### POST /tickets/_ticket\_id_/archive.json
*Archives an unarchived ticket*

#### Status Codes

Success: 204

Failure: 500

#### Example

POST /tickets/1/archive.json

Response is Success with no body

### Un-Archiving Tickets

#### DELETE /tickets/_ticket\_id_/archive.json
*Un-archives an archived ticket*

#### Status Codes

Success: 204

Failure: 500

#### Example

DELETE /tickets/1/archive.json

Response is Success with no body


Assigning tickets to a User/Group
=================================

Assigning a ticket to a User or Group involves make a POST call to the
same resource URL but different POST data

#### POST /tickets/_ticket\_id_/assignments.json

#### Status Code

Success: 201

Failure: 500

Validation Error: 400

### Assigning a User to a ticket

#### POST Data

````
  {
    "assignment" : {
      "user_id" : 1
    }
  }
````

#### Response

````
  {
    "assignment":{
      "id":2,
      "created_at":"2012-01-19T16:53:40Z",
      "ticket":{"id":1},
      "assignee":{
        "user":{
          "id":3,
          "email":"person4@example.com",
          "name":"Agent,2",
          "agent":true,
          "picture":{
            "thumb20":"https://secure.gravatar.com/avatar/1a112eb69f35030f97639280fe246aee.png?r=PG&s=20",
            "thumb24":"https://secure.gravatar.com/avatar/1a112eb69f35030f97639280fe246aee.png?r=PG&s=24",
            "thumb32":"https://secure.gravatar.com/avatar/1a112eb69f35030f97639280fe246aee.png?r=PG&s=32",
            "thumb48":"https://secure.gravatar.com/avatar/1a112eb69f35030f97639280fe246aee.png?r=PG&s=48",
            "thumb64":"https://secure.gravatar.com/avatar/1a112eb69f35030f97639280fe246aee.png?r=PG&s=64",
            "thumb128":"https://secure.gravatar.com/avatar/1a112eb69f35030f97639280fe246aee.png?r=PG&s=128"
          }
        }
      }
    }
  }
````

### Assigning a Group to a ticket

#### POST Data

````
  {
    "assignment" : {
      "group_id" : 1
    }
  }
````

#### Response

````
  {
    "assignment":{
      "id":2,
      "created_at":"2012-01-19T17:29:50Z",
      "ticket":{
        "id":1
      },
      "assignee":{
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
    }
  }
````


Starring / Unstarring Tickets
===============================

### Starring Tickets

#### POST /tickets/_ticket\_id_/star.json
*Stars' an unstarred ticket*

#### Status Codes

Success: 204

Failure: 500

#### Example

POST /tickets/1/star.json

Response is Success with no body

### Unrchiving Tickets

#### DELETE /tickets/_ticket\_id_/star.json
*Un-stars' a starred ticket*

#### Status Codes

Success: 204

Failure: 500

#### Example

DELETE /tickets/1/star.json

Response is Success with no body

Spamming / Un-Spamming Tickets
===============================

### Spamming Tickets

#### POST /tickets/_ticket\_id_/spam.json
*Spams' an un-spammed ticket*

#### Status Codes

Success: 204

Failure: 500

#### Example

POST /tickets/1/spam.json

Response is Success with no body

### Un-Spamming Tickets

#### DELETE /tickets/_ticket\_id_/spam.json
*Un-spams' a spammed ticket*

#### Status Codes

Success: 204

Failure: 500

#### Example

DELETE /tickets/1/spam.json

Response is Success with no body

