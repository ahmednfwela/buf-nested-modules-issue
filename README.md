this repo showcases an issue with buf CLI v1.34.0 where one of the path modules contains other path modules

note that `nested-dep` can come from a different repo, via git submodules, where we have no control over the files.

running `buf lint` in root shows:

```
nested-dep\m1\sample\v1\service.proto:3:1:Files with package "sample.v1" must be within a directory "sample\v1" relative to root but were in directory "m1\sample\v1".
nested-dep\m1\sample\v1\service.proto:3:1:Multiple directories "m1/sample/v1,m2/sample/v1" contain files with package "sample.v1".
nested-dep\m2\sample\v1\service.proto:3:1:Files with package "sample.v1" must be within a directory "sample\v1" relative to root but were in directory "m2\sample\v1".
nested-dep\m2\sample\v1\service.proto:3:1:Multiple directories "m1/sample/v1,m2/sample/v1" contain files with package "sample.v1".
```

however editing [buf.yaml](buf.yaml) to also include the modules of [nested-dep/buf.yaml](nested-dep/buf.yaml) will fix the issue.