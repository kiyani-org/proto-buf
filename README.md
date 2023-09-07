# proto-buf
proto demo using buf


## Steps

 1. Install the following:

    ```console
    $ go install github.com/bufbuild/buf/cmd/buf@v1.26.1       
    $ go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.28 
    ```

 2. Init go module

    ```console
    $ go mod init github.com/kiyani-org/proto-buf
    ```
 
 3. Init the buf yaml file

    ```console
    $ buf mod init
    ```

 4. Create a `buf.gen.yaml` file and add the following content

    ```console
    $ # Documentation: https://docs.buf.build/configuration/v1/buf-gen-yaml
      version: v1
      plugins:
        - name: go # see https://buf.build/docs/configuration/v1/buf-gen-yaml#plugin
          out: gen/go
          opt: paths=source_relative
    ```

 4. Add user.proto file

    ```
      syntax = "proto3";

      package user.v1;

      option go_package = "github.com/kiyani-org/proto-buf/gen/user/v1;userpb";

      message User {
        string uuid       = 1;
        string full_name  = 2;
        int64  birth_year = 3;
      }
    ``` 

 6. Run `buf lint` to verify proto is valid

 7. Run `buf generate` to generate compiled protos

 8. Run `go mod tidy` to update the go mod file for recent package references in `user.pb.go`
