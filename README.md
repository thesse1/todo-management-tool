# todo-management-tool

The aim of this project is to explore the functionality of Furo: https://furo.pro.

It was created following the approach described in the e-book: [eBook.pdf](./eBook.pdf) [eBook.epub](./eBook.epub).

Please note: The last commit to the upstream project https://github.com/theNorstroem/todo-management-tool broke the web client. Therefore I have created this demo branch off the last working commit in the main branch.

Please note: The commands for starting the gRPC back-end and the gRPC Gateway did not work for me. Please use the following commands:

```
cd grpc-backend
go run ./cmd/tmt-grpc/grpcserver.go
```

```
cd api
GW_SERVER_ADDRESS=localhost:8481 GRPC_SERVER_ADDRESS=localhost:7070 go run ./dist/grpc-gateway/cmd/cmd.go
```

As described in the e-book, this project includes Furo muspecs for a simple to-do list application (/api/muspecs), generated long-format specs (/api/specs), generated protobuf type and gRPC service specs (/api/dist/protos), a generated Swagger file for a REST version of the service (/api/dist/openapi/all-services.swagger.json), a Go server application (/grpc-backend) including generated Go service stubs (/api/dist/pb), a Go package for gRPC-Gateway (/api/dist/grpc-gateway) and a Furo Web-based web application (/client) including the generated env.js file (/client/src/configs) with the generated Furo JavaScript types and services.

Run the back-end application and the gRPC Gateway with the commands given above, and the web application with the following commands:

```
cd client
npm i
npm run start
```

This will automatically open the web app in the configured standard browser.

# Creating an enterprise-flavoured ToDo application from scratch with the Furo Web Stack

- _eBook_: [eBook.pdf](./eBook.pdf) [eBook.epub](./eBook.epub)
- _Repository_: https://github.com/theNorstroem/todo-management-tool
- _Furo Web Stack_: https://furo.pro/

## Getting Started
We recommend 2+ years of programming experience in JavaScript / HTML / CSS and a basic knowledge of Protocol Buffers. Experiences in Go is also a plus. But don’t worry, you don’t have to be an expert.

> chapter 01: git checkout c01_todos_api_contract
 
## Final Project Structure
.
|-- LICENSE
|-- README.md
|-- api
|-- client
`-- grpc-backend

## Local API Development

### Use local container build
[Furo build environment docker container](https://github.com/theNorstroem/furoBEC)

https://hub.docker.com/r/thenorstroem/furo-bec

```shell script
docker pull thenorstroem/furo-bec:v1.28.5
```

Example Usage: docker run -it --rm -v $(pwd):$pwd/specs thenorstroem/furo-bec:v1.28.5

Commands: https://furo.pro/docs/commands/

**start the furo build environment container from /api**

## Local Web Application Development
All the web application source is located in the subfolder `client`.

### Install dependencies
```
npm i
```

### Starting Web Application in mock mode
```
npm run start:mock
```

### Starting Web Application with backend proxy (backend for frontend)
```
npm run start
```

## Local gRPC Server Development
All the gRPC server code is located in the subfolder `/grpc-backend`.

```
cd grpc-backend
go run ./...
```

or with the built version
```
cd grpc-backend
go install ./cmd/...
tmt-grpc
```

## Local gRPC Gateway
All the gRPC gateway code is located in the subfolder `/api/dist/grpc-gateway`.

```
cd api
go run ./...
```

or with the built version
```
cd api
go install ./dist/grpc-server/cmd/...
GW_SERVER_ADDRESS=localhost:8481 GRPC_SERVER_ADDRESS=localhost:7070 cmd

```

