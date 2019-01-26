### http-fake-backend
---
https://github.com/micromata/http-fake-backend

```
{
  "response": "Yeah"
}
```

```
npm install

npm install -g yo
npm install -g generator-http-fake-backend
npm run start:dev
npm start
```

```js
module.exports = SetupEndpoint({
  name: 'simpleExample',
  urls: [{
    requests: [
      { response: '/response-files/simpleExample.json' }
    ]
  }]
});

module.exports = SetupEndpoint({
  name: 'anotherExample',
  urls: [{
    params: '/read',
    requests: [{
      method: 'GET',
      response: '/response-files/anotherExample.json'
    }]
  }, {
    params: '/updata/{id}',
    requests: [{
      method: ['PUT', 'PATCH'],
      response: {
        success: true
      }
    }, {
      method: 'DELETE',
      response: {
        deleted: true
      }
    }]
  }, ]
});

// /server/api/fileTypes.js
module.exports = SetupEndpoint({
  name: 'fileTypes',
  urls: [{
    params: '/json',
    requests: [{
      response: '/response-files/simpleExample.json'
    }]
  }, {
    params: '/text',
    requests: [{
      response: '/response-files/example.txt',
      mimeType: 'text/plain'
    }]
  }, {
    params: '/html',
    requests: [{
      response: '/response-files/example.html',
      mimeType: 'text/html'
    }]
  }, {
    params: '/pdf',
    requests: [{
      response: '/response-files/example.pdf',
      sendFile: true
    }]
  }]
});

// /server/api/fakingStatuscodes.js
module.exports = SetupEndpoint({
  name: 'statusCodes',
  urls: [
    {
      params: '/boomError',
      requests: [{
        statusCode: 402
      }]
    },
    {
      params: '/customError',
      requests: [{
        response: { error: true },
        statusCode: 406
      }]
    },
    {
      params: '/regularResponse',
      requests: [{
        response: '/response-files/anotherExample.json'
      }]
    }
  ],
  statusCode: 401
});

// .env
NODE_ENV=development
SERVER_PORT=8081
TEST_PORT=9090
API_PREFIX=/api
#CUSTOM_HEADER_NAME=Authorization
CUSTOM_HEADER_VALUE=Bearer xxxxxxxxxxxxxx
```


