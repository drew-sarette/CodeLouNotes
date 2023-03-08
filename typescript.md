# Typescript
TS is a statically typed language based on JavaScript, developed at Microsoft.  It is a superset of JS, and is transpiled into plain JS before being run. It can be used for both frontend and backend applications. Some useful features: 
- more reliable due to static types
- better autocomplete
- more efficient for larger projects

## Setup
First make sure Node.js is installed. Then 
```
npm i -g typescript
```

You can test the installation by checking  the version of the TS compiler:
```
tsc -v
```

## Hello World
Start with an index.ts file, and write
```
const greeting: string = "Hello world!"
```
then run the tsc command to compile it to js:
```
tsc index.ts
```
This generates a new file index.js in the same folder.
By default the js file will conform to ES5, use the var keyword, etc...

## Configuring the compiler
To generate a tsconfig.json file, run 
```
tsc --init
```
You can change target to a later version of ES if needed. ES2016 is the safest.

To configure the input and output directories, use  the rootDir and outDir settings. A good choice would be src and dist

other good settings include:
removeComments: true
noEmitOnError: true

To compile all ts files, just use ```tsc```
Note that after setting up a src folder, tsc index.ts will no longer work. Use tsc, ant it will compile everything in the src folder.

## Debugging
in tsconfig.json set sourceMap: true

go to Debug panel, and seclect "create launch.json" 

between program and outfiles, enter 
```
"preLaunchTask": "tsc: build - tsconfig.json",
```

Then you can select breakpoints and start debugging.