# protobuf-gen
gen Protobuf type to typescript type

## Installation

```bash
$ npm install @seasonjs/grpc-helper --save-dev
```

## Example

Protobuf file hero-proto/hero.proto:

```proto
syntax = "proto3";

package hero;

service HeroesService {
  rpc FindOne (HeroById) returns (Hero) {}
}

message HeroById {
  int32 id = 1;
}

message Hero {
  int32 id = 1;
  string name = 2;
}
```

Generate interfaces:

```bash
$ tsproto --path ./hero-proto
```

Output:

```ts

export namespace hero {
  export interface HeroService {
    findOne(data: HeroById): Promise<Hero>;
  }
  export interface HeroById {
    id?: number;
  }
  export interface Hero {
    id?: number;
    name?: string;
  }
}


```

## Usage

Base usage:
```bash
$ pb --path grpc-proto
```
Output dir:
```bash
$ pb --path grpc-proto --output any-dir
```
Target files:
```bash
$ pb --path grpc-proto --target one.proto two.proto
```
Ignore directories or files:
```bash
$ pb --path grpc-proto --ignore grpc-proto/ignore-dir
```

## Options

The following options are available:

```
  --version, -v   Show version number                                  [boolean]
  --help, -h      Show help                                            [boolean]
  --path, -p      Path to root directory                      [array] [required]
  --output, -o    Path to output directory                              [string]
  --target, -t    Proto files                      [array] [default: [".proto"]]
  --ignore, -i    Ignore file or directories
                                      [array] [default: ["node_modules","dist"]]
  --comments, -c  Add comments from proto              [boolean] [default: true]
  --verbose       Log all output to console            [boolean] [default: true]
  --keepCase, -k  keep property case                   [boolean] [default: true]
```
