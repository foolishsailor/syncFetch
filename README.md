# SyncQ

Synchronous queue for asynchronous Javascript Fetch() - when you need sequential execution but still want all that async promise goodness.

## Example

Usable Example here: [SyncQ](https://sync-q.vercel.app/)

#### Instantiate

```.js
import { SyncQ } from "./dist/syncQ.js";
const syncQ = SyncQ();

```

#### Create callback functions

```.js
const success = (data) => {
    console.log("Successful result", data);
}

const fail = (data) =>{
    console.error("Failed result", data);
}
```

#### Add queue item to queue

```.js
const queueItemObj = {
    url: 'http://httpbin.org/get',
    success: success,
    fail: fail
};

syncQ.add(queueItemObj);
```

## Methods

#### clearAll()

Clear all items in queue.

#### clearByName(name)

Clear all items in queue that have item.name = name.

#### add(item)

Add item to queue and begins execution. Execution continues until all items in queue are executed.

Returns object:

```.js
   {
       request, //Original request
       result, //Response
       content, //Body of response
       headers //Array of headers
   }
```

### item options

#### Required

| Option      | Type     | Description                             | Default |
| ----------- | -------- | --------------------------------------- | ------- |
| **url**     | string   | Url of request                          |         |
| **success** | function | Callback function on successful request |         |
| **fail**    | function | Callback function on failed request     |         |

#### Optional

| Option           | Type     | Description                                            | Default                           |
| ---------------- | -------- | ------------------------------------------------------ | --------------------------------- |
| **responseType** | string   | How to parse the reponse                               | 'json', 'text' - default = 'json' |
| **header**       | bool     | Get header data from repsone                           | false                             |
| **headers**      | [string] | String names of headers to look for                    |                                   |
| **retry**        | bool     | Retry item if request fails                            | false                             |
| **maxRetries**   | integer  | Number of times to retryRetry item if request fails    | 3                                 |
| **name**         | string   | Name of queue item. Allows items to be removed by name |                                   |
| **priority**     | bool     | If true item is added to top of queue                  | false                             |
| **debug**        | bool     | Turn debug on and sends data to debugData callback     | false                             |
| **debugData**    | function | Callback function to receive debug data                |                                   |
