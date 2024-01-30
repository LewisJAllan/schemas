# The Steps to Windows Protobuf

1. Get googles protobuf for the service  
   a. `$ go get google.golang.org/protobuf`  
   b. `$ go get google.golang.org/protobuf/proto`
2. Follow the protocol buffer installation; use the manual download for "Other OS"  
   a. https://grpc.io/docs/protoc-installation/
3. Extract the .zip into the $GOPATH and ensure the Environment Variables have the $GOPATH/bin within the $PATH
4. Install the go modules for protoc-gen-go and protoc-gen-grpc  
   a. `$ go install google.golang.org/protobuf/cmd/protoc-gen-go@latest`                                                                        
   b. `$ go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest`
5. Restart you command terminal
6. Check you have correctly installed protoc and protoc-gen-go  
   a. `$ protoc --version`  
   b. `$ protoc-gen-go --version`  

# Creating Proto3 GRPC

The very first, non-comment, line within the message needs to be  
`syntax = "proto3";`  
  
Then we want to point to the repositories master address  
`option go_package = "https://github.com/LewisJAllan/schemas/blob/master/playground";`

and then we can create the proto message after declaring the package  
```
package playground;

// The greeting service definition.
service Greeter {
// Sends a greeting
rpc SayHello (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name.
message HelloRequest {
string name = 1;
}

// The response message containing the greetings
message HelloReply {
string message = 1;
}
```

# Generating the protocol buffer
We want to call protoc and pass in values to show the desired location, of which we need to have pre-created the empty directory, and then the `source_relative` path, finally pointing to the file we are generating:
```
protoc --go_out=playgroundpb --go_opt=paths=source_relative --go-grpc_out=playgroundpb --go-grpc_opt=paths=source_relative playground/helloworld.proto
```
This will create two files; `playgroundpb/playground/helloworld.pb.go` & `playgroundpb/playground/helloworld_grpc.pb.go`