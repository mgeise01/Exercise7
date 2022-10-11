# Upload a sound file
Uploads a selected sound file to the user's profile.


### URL
`POST https://api.sounddate.com/profile/sound`

### Headers
| Header Name | Description | Required | Values |
|----------------|---|---|---|
| **Bearer** | Access token | Required | See Authorization section |
| **Content-Type** | Sound file format | Optional | Can be audio/mpeg for mp3 or audio/x-wav for wav. Default is audio/mpeg. |
| **Accept** | Format of returned data | Optional | Can be application/xml or application/json. Default is JSON. |

### POST Body
The sound file. Maximum length of the sound file is 5 minutes.

### Sample Request
`POST https://api.sounddate.com/profile/sound`

``
Bearer: {Access token}  
Content-Type: audio/mpeg  
Accept: application/json
``
``
{sound file}
``

### Response
| Element | Description | Type | Notes |
|---|---|---|---|
| **id** | ID of the new sound file | integer | |
| **length** | Length of the new sound file | float | Length in seconds |

### Sample Response
``
{
  "id": 8746
  "length": 125.3
}
``

# Retrieve sound file list
---
Retrieves a list of profile sound URLs and lengths from a specific user.

### URL
`Get https://api.sounddate.com/user/{user id}/profile/sound/`
``
where {user id} is the ID of the target user profile containing sound files.
``

### Query Parameters
Parameter | Description | Type | Required | Notes |
---|---|---|---|---
**sortOrder** | The order sound files are returned | string | Optional | Valid values: mostRecent, earliest, shortest, longest. Default is mostRecent |

**Note**
* **mostRecent**: Returns most recent sound file to the earliest.
* **earliest**: Returns earliest sound file to most recent.
* **shortest**: Returns shortest length sound file to longest.
* **longest**: Returns longest length sound file to shortest.

### Headers
Header Name | Description | Required | Values
---|---|---|---
**Bearer** | Access token | Required | See Authorization section
**Accept** | Format of returned data | Optional | Can be application/xml or application/json. Default is JSON.

### Sample Request
`GET https://api.sounddate.com/user/12345/profile/sound?sortOrder=earliest`

``
Bearer: {access token}
Accept: application/json
``

### Response
Element | Description | Type | Notes
---|---|---|---
**soundFiles** | List of sound file information | array | 
  id | ID of the sound file | integer |
  url | URL of the sound file | string | 
  length | Length of the sound file | float | Length in seconds

### Sample Response
``
{
  "soundFiles": [
  {
    "id": 23456,
    "url": "https://api.sounddate.com/profile/sound/23456.mp3",
    "length": 11.2
  },
  {
    "id": 24559,
    "url": "https://api.sounddate.com/profile/sound/24559.mp3",
    "length": 19.8
  }
  ]
}
``

### Status Codes and Errors
The following table lists the returned HTTP status codes.

Code | Description | Notes 
---|---|---
**200** | OK | Sound file uploaded successfully
**401** | Unauthorized | Access token is invalid
**413** | Payload Too Large | Uploaded sound file is longer than 5 minutes