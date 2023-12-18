Hi,
It's repo of real struggle to make protobuf working on windows or linux as a beginner and I made it.
It is based on the official documentation of protobuf repo.

If you use vcpkg, then download VS Community edition and open CMakeProject, you should be able to successfully configure and run the code.
In Windows VCPKG has tons of variables that are to be reverse engineered and migrated to Cmake file to make it work properly with Os type, triplet, static or dynamic config.

In case you are in trouble with error on linux "build.make:65: *** target pattern contains no '%'.  Stop." You are missing protoc compiler package.
Its super unobvious but proto-c and proto-c are different programs:
```text
protoc-c --version
protobuf-c 1.4.1
libprotoc 3.21.12
protoc --version
libprotoc 3.21.12
```

On Debian it can be installed with\
sudo apt-get install protobuf-c-compiler\
sudo apt-get install protobuf-compiler\
