# protobuf

Google Protocol Buffers home page is [Protocol Buffers](https://developers.google.com/protocol-buffers/). There is what looks like an official git repo at [google/protobuf](https://github.com/google/protobuf).

This is not source you would include in your program, this is the source used to build the protoc compiler. So as
a package this needs a trampoline mechanism we don't have yet, "source to a tool that is run at compile time on
other files that are in a package".
