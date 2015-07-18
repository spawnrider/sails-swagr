sails-swagr
=========

Originally forked from [swagger-express](https://github.com/fliptoo/swagger-express), however, heavily 
customized to meet Swagger 2.0 specifications and to work with sails. At the moment this repo only works 
with YML doc files.

[Swagger](https://developers.helloreverb.com/swagger/) is a specification and complete framework 
implementation for describing, producing, consuming, and visualizing RESTful web services.
View [demo](http://petstore.swagger.wordnik.com/).

__sails-swagr__ is a simple and clean solution to integrate swagger with express or sails.

## Installation

    $ npm install sails-swagr --save

## Quick Start

Configure sails-swagr as express middleware.


`apiVersion`      -> Your api version.

`swaggerVersion`  -> Swagger version.

`swaggerURL`      -> Path to use for swagger ui web interface.

`swaggerJSON`     -> Path to use for swagger ui JSON.

`basePath`        -> The basePath for swagger.js

`info`            -> [Metadata][info] about the API

`apis`            -> Define your api array.

`middleware`      -> Function before response.

## Sails Integration

Modify the `config/http.js` to look like:

```
customMiddleware: function (app) {
    var swagger = require('sails-swagr');  
    var express = require('sails/node_modules/express');

    app.use(swagger.init(express, app, {
        apiVersion: '1.0',
        swaggerVersion: '2.0',
        swaggerURL: '/api/docs',
        swaggerJSON: '/api-docs.json',
        basePath: sails.getBaseurl(),
        info: {
          title: ' API Swagger Documentation',
          description: 'Sails Swagr'
        },
        apis: [
          './api/docs/Cards.yml', 
          './api/docs/Stories.yml',
          './api/docs/Users.yml',
        ]
    })); 
  }

```

[info]: https://github.com/wordnik/swagger-spec/blob/master/versions/1.2.md#513-info-object


## Read from yaml file

Example 'api.yml'

```yml

paths:
  /login:
    post:
      summary: Login with username and password
      notes: Returns a user based on username
      responseClass: User
      nickname: login
      consumes: 
        - text/html
      parameters:

      - name: username
        dataType: string
        paramType: query
        required: true
        description: Your username

      - name: password
        dataType: string
        paramType: query
        required: true
        description: Your password

definitions:
  User:
    properties:
      username:
        type: String
      password:
        type: String    
```
    
# Credits

- [Express](https://github.com/visionmedia/express)
- [swagger-jack](https://github.com/feugy/swagger-jack)

## License

(The MIT License)

Copyright (c) 2015 qbanguy &lt;heyadrian@gmail.com&gt;

Copyright (c) 2013 Fliptoo &lt;fliptoo.studio@gmail.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
