# Async API - SignON Project 8.0.1 documentation

* License: [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)
* Default content type: [application/json](https://www.iana.org/assignments/media-types/application/json)

The API describes precisely the communications messages between the Orchestrator and the Pipeline.

## Table of Contents

* [Servers](#servers)
  * [rabbitmq](#rabbitmq-server)
* [Operations](#operations)
  * [PUB SignON](#pub-signon-operation)
  * [SUB SignON](#sub-signon-operation)

## Servers

### `rabbitmq` Server

* URL: `localhost:5672`
* Protocol: `amqp`

RabbitMQ


## Operations

### PUB `SignON` Operation

* Operation ID: `Publish Message`

Payload of received order

#### `amqp` Channel specific information

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| is | - | - | `"routingKey"` | - | - |
| exchange | - | - | - | - | - |
| exchange.name | - | - | `"SignONExchange"` | - | - |
| exchange.type | - | - | `"direct"` | - | - |

#### `amqp` Operation specific information

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| timestamp | - | - | `"true"` | - | - |
| ack | - | - | `"false"` | - | - |
| cc | - | - | - | - | - |
| cc.0 (index) | - | - | `"SignONRoutingKey"` | - | - |

#### Message Message from Orchestrator to Pipeline (WP3) `OrchestratorMessage`

*Message that will be sent from the Orchestrator to the Pipeline*

* Content type: [application/json](https://www.iana.org/assignments/media-types/application/json)

##### Payload

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| (root) | object | Schema for the message sent from the Orchestrator to the Pipeline (WP3) Orchestrator | - | - | **additional properties are allowed** |
| App | object | Built by the App, it contains values regarding the input given by the User | - | - | **additional properties are allowed** |
| App.sourceKey | string | Where to find the video or the audio given by the user, if value not available use "NONE". | - | - | **required** |
| App.sourceText | string | Text that the user wants to be translated, if value not available use "NONE". | - | - | **required** |
| App.sourceLanguage | string | ENUM representing the language in which the message is given by the user. VGT = Flemish Sign Language, SSP = Spanish Sign Language, BFI = British Sign Language, ISG = Irish Sign Language, DSE = Dutch Sign Language, ENG = English, GLE = Irish, NLD = Dutch / Flemish, SPA = Castillan, Spanish (for more info look at ISO 639-3 website https://iso639-3.sil.org/). | allowed (`"VGT"`, `"SSP"`, `"BFI"`, `"ISG"`, `"DSE"`, `"ENG"`, `"GLE"`, `"NLD"`, `"SPA"`, `"DUT"`) | - | **required** |
| App.sourceMode | string | ENUM representing the mode in which the message is given by the user. | allowed (`"VIDEO"`, `"AUDIO"`, `"TEXT"`) | - | **required** |
| App.sourceFileFormat | string | The format in which the file containing data regarding the video or the audio given by the user is saved, if value not available use "NONE". | - | - | **required** |
| App.sourceVideoCodec | string | The codec used to compress the video, if value not available use "NONE". | - | - | **required** |
| App.sourceVideoResolution | string | The resolution used for the video, if value not available use "NONE". | - | - | **required** |
| App.sourceVideoFrameRate | number | The frame rate used for the video, if value not available use "-1". | - | - | **required** |
| App.sourceVideoPixelFormat | string | The pixel format used for the video, if value not available use "NONE". | - | - | **required** |
| App.sourceAudioCodec | string | The codec used to compress the audio, if value not available use "NONE". | - | - | **required** |
| App.sourceAudioChannels | string | The channels used for the audio, if value not available use "NONE". | - | - | **required** |
| App.sourceAudioSampleRate | number | The sample rate used for the audio, if value not available use "-1". | - | - | **required** |
| App.translationLanguage | string | ENUM representing the language in which the message is given by the user. VGT = Flemish Sign Language, SSP = Spanish Sign Language, BFI = British Sign Language, ISG = Irish Sign Language, DSE = Dutch Sign Language, ENG = English, GLE = Irish, NLD = Dutch / Flemish, SPA = Castillan, Spanish (for more info look at ISO 639-3 website https://iso639-3.sil.org/). | allowed (`"VGT"`, `"SSP"`, `"BFI"`, `"ISG"`, `"DSE"`, `"ENG"`, `"GLE"`, `"NLD"`, `"SPA"`, `"DUT"`) | - | **required** |
| App.translationMode | string | ENUM representing the mode in which the message has to be returned to the user. | allowed (`"AVATAR"`, `"AUDIO"`, `"TEXT"`) | - | **required** |
| App.appInstanceID | string | Identifier to recognize which instance of the app has sent the message. | - | - | **required** |
| App.appVersion | string | App Version Number | - | - | **required** |
| App.T0App | number | Timestamp at which the message has been sent from the App to the orchestrator (yyyy-MM-dd HH:mm:ss,SSS). | - | - | **required** |
| OrchestratorRequest | object | Built by the Orchestrator, it contains some additional values | - | - | **additional properties are allowed** |
| OrchestratorRequest.OrchestratorVersion | string | Orchestrator Version Number | - | - | **required** |
| OrchestratorRequest.T1Orchestrator | integer | Timestamp at which the message has been sent from the orchestrator to WP3 in milliseconds | - | format (`int64`) | **required** |
| OrchestratorRequest.bucketName | string | Name of the Minio Bucket which contains the file relative to the object that was sent. | - | - | **required** |

> Examples of payload _(generated)_

```json
{
  "App": {
    "sourceKey": "NONE",
    "sourceText": "Hello Bob, How are you?",
    "sourceLanguage": "SPA",
    "sourceMode": "TEXT",
    "sourceFileFormat": "wav",
    "sourceVideoCodec": "NONE",
    "sourceVideoResolution": "NONE",
    "sourceVideoFrameRate": -1,
    "sourceVideoPixelFormat": "NONE",
    "sourceAudioCodec": "NONE",
    "sourceAudioChannels": "NONE",
    "sourceAudioSampleRate": -1,
    "translationLanguage": "SPA",
    "translationMode": "TEXT",
    "appInstanceID": "instance16",
    "appVersion": "0.1.0",
    "T0App": 1508484583259
  },
  "OrchestratorRequest": {
    "OrchestratorVersion": "0.1.0",
    "T1Orchestrator": 1508484583788,
    "bucketName": "signon"
  }
}
```



### SUB `SignON` Operation

* Operation ID: `Subscribe Message`

Payload of received order

#### `amqp` Channel specific information

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| is | - | - | `"routingKey"` | - | - |
| exchange | - | - | - | - | - |
| exchange.name | - | - | `"SignONExchange"` | - | - |
| exchange.type | - | - | `"direct"` | - | - |

Accepts **one of** the following messages:

#### Message Message from Pipeline (WP5) to Orchestrator `OrchestratorMessage`

*Message that will be sent from the Pipeline to the Orchestrator*

* Content type: [application/json](https://www.iana.org/assignments/media-types/application/json)

##### Payload

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| (root) | object | Schema for the message sent from the Pipeline (WP5) to the Orchestrator | - | - | **additional properties are allowed** |
| App | object | Built by the App, it contains values regarding the input given by the User | - | - | **additional properties are allowed** |
| App.sourceKey | string | Where to find the video or the audio given by the user, if value not available use "NONE". | - | - | **required** |
| App.sourceText | string | Text that the user wants to be translated, if value not available use "NONE". | - | - | **required** |
| App.sourceLanguage | string | ENUM representing the language in which the message is given by the user. VGT = Flemish Sign Language, SSP = Spanish Sign Language, BFI = British Sign Language, ISG = Irish Sign Language, DSE = Dutch Sign Language, ENG = English, GLE = Irish, NLD = Dutch / Flemish, SPA = Castillan, Spanish (for more info look at ISO 639-3 website https://iso639-3.sil.org/). | allowed (`"VGT"`, `"SSP"`, `"BFI"`, `"ISG"`, `"DSE"`, `"ENG"`, `"GLE"`, `"NLD"`, `"SPA"`, `"DUT"`) | - | **required** |
| App.sourceMode | string | ENUM representing the mode in which the message is given by the user. | allowed (`"VIDEO"`, `"AUDIO"`, `"TEXT"`) | - | **required** |
| App.sourceFileFormat | string | The format in which the file containing data regarding the video or the audio given by the user is saved, if value not available use "NONE". | - | - | **required** |
| App.sourceVideoCodec | string | The codec used to compress the video, if value not available use "NONE". | - | - | **required** |
| App.sourceVideoResolution | string | The resolution used for the video, if value not available use "NONE". | - | - | **required** |
| App.sourceVideoFrameRate | number | The frame rate used for the video, if value not available use "-1". | - | - | **required** |
| App.sourceVideoPixelFormat | string | The pixel format used for the video, if value not available use "NONE". | - | - | **required** |
| App.sourceAudioCodec | string | The codec used to compress the audio, if value not available use "NONE". | - | - | **required** |
| App.sourceAudioChannels | string | The channels used for the audio, if value not available use "NONE". | - | - | **required** |
| App.sourceAudioSampleRate | number | The sample rate used for the audio, if value not available use "-1". | - | - | **required** |
| App.translationLanguage | string | ENUM representing the language in which the message is given by the user. VGT = Flemish Sign Language, SSP = Spanish Sign Language, BFI = British Sign Language, ISG = Irish Sign Language, DSE = Dutch Sign Language, ENG = English, GLE = Irish, NLD = Dutch / Flemish, SPA = Castillan, Spanish (for more info look at ISO 639-3 website https://iso639-3.sil.org/). | allowed (`"VGT"`, `"SSP"`, `"BFI"`, `"ISG"`, `"DSE"`, `"ENG"`, `"GLE"`, `"NLD"`, `"SPA"`, `"DUT"`) | - | **required** |
| App.translationMode | string | ENUM representing the mode in which the message has to be returned to the user. | allowed (`"AVATAR"`, `"AUDIO"`, `"TEXT"`) | - | **required** |
| App.appInstanceID | string | Identifier to recognize which instance of the app has sent the message. | - | - | **required** |
| App.appVersion | string | App Version Number | - | - | **required** |
| App.T0App | number | Timestamp at which the message has been sent from the App to the orchestrator (yyyy-MM-dd HH:mm:ss,SSS). | - | - | **required** |
| OrchestratorRequest | object | Built by the Orchestrator, it contains some additional values | - | - | **additional properties are allowed** |
| OrchestratorRequest.OrchestratorVersion | string | Orchestrator Version Number | - | - | **required** |
| OrchestratorRequest.T1Orchestrator | integer | Timestamp at which the message has been sent from the orchestrator to WP3 in milliseconds | - | format (`int64`) | **required** |
| OrchestratorRequest.bucketName | string | Name of the Minio Bucket which contains the file relative to the object that was sent. | - | - | **required** |
| RabbitMQ | object | Parameters needed for the RPC Pattern implemented by RabbitMQ | - | - | **additional properties are allowed** |
| RabbitMQ.correlationID | string | Component generated automatically by rabbitMQ needed by WP2 for the correct handling of messages. | - | - | - |
| RabbitMQ.replyTo | string | Component generated automatically by rabbitMQ needed by WP2 for the correct handling of messages. | - | - | - |
| SourceLanguageProcessing | string | - | - | - | - |
| IntermediateRepresentation | string | - | - | - | - |
| MessageSynthesis | string | - | - | - | - |

> Examples of payload _(generated)_

```json
{
  "App": {
    "sourceKey": "NONE",
    "sourceText": "Hello Bob, How are you?",
    "sourceLanguage": "SPA",
    "sourceMode": "TEXT",
    "sourceFileFormat": "wav",
    "sourceVideoCodec": "NONE",
    "sourceVideoResolution": "NONE",
    "sourceVideoFrameRate": -1,
    "sourceVideoPixelFormat": "NONE",
    "sourceAudioCodec": "NONE",
    "sourceAudioChannels": "NONE",
    "sourceAudioSampleRate": -1,
    "translationLanguage": "SPA",
    "translationMode": "TEXT",
    "appInstanceID": "instance16",
    "appVersion": "0.1.0",
    "T0App": 1508484583259
  },
  "OrchestratorRequest": {
    "OrchestratorVersion": "0.1.0",
    "T1Orchestrator": 1508484583788,
    "bucketName": "signon"
  },
  "RabbitMQ": {
    "correlationID": "signon.rpc.requests_id23",
    "replyTo": "rabbitmq.requests_id23"
  },
  "SourceLanguageProcessing": "string",
  "IntermediateRepresentation": "string",
  "MessageSynthesis": "string"
}
```


#### Message Error Message `OrchestratorMessage`

*Error Message*

* Content type: [application/json](https://www.iana.org/assignments/media-types/application/json)

##### Payload

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| (root) | object | Schema for the Error Message | - | - | **additional properties are allowed** |
| type | string | URI that identifies the problem type | - | - | - |
| title | string | Human readable short description of the error | - | - | - |
| status | integer | Repetition of the response status code | - | - | - |
| detail | string | Human readable full description of the error | - | - | - |
| instance | string | URI reference that identifies the specific occurrence of the problem | - | - | - |
| stackTrace | string | Stack trace of the error | - | - | - |
| timestamp | string | Timestamp of the error | - | - | - |
| parameters | string | Relevant parameter | - | - | - |

> Examples of payload _(generated)_

```json
{
  "type": "urn:error-type:missing-app-instance-id",
  "title": "The AppInstanceID for the message is missing.",
  "status": 400,
  "detail": "The AppInstanceID for the message is missing.",
  "instance": "urn:uuid:1ed5f7c1-e757-49d0-a1ba-4fb017c76e60",
  "stackTrace": "string",
  "timestamp": "2022-09-01T14:06:11.153+00:00",
  "parameters": "null"
}
```



