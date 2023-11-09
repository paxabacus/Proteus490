---
geometry: margin=2cm
author:
- Katie Ortiz
- AB (Revisement for Markdown)
date: '11/8/2023'
title: 'Swift Proteus Install'
numbersections: true
---
# WINDOWS!!!!!!

# Downlaods Stuff

## Cloning the Swift-Repo

```
git clone https://github.com/csun-tavlab/swift-proteus
```

## VSCODE

### Open the Repo in VSCode

If you can't do that, then do:
- File -> Options -> Integration se as Default for vscode


### Plugins!

#### C/C++ and C/C++ Extensions Pack

Just find these in the extensions tab in VScode, and download
![image](https://github.com/paxabacus/Proteus490/assets/64762646/98734a99-5cae-46aa-8535-3ec281d14881)


### Developer Mode

**disable it**

On windows Search, look up "Developer Settings" Open it, and disable developer mode
![image](https://github.com/paxabacus/Proteus490/assets/64762646/bda38c66-f008-4987-81e1-704aa0c2373d)
>I didn't need to disable it - AB

## Swift and Swift for Windows

[Swift Developer Kit](https://www.swift.org/download/)
- Keep default tbh
  
[Swift For Windows](https://swiftforwindows.github.io/)
- Keep everything to default in installation

## Tools for Visual Studio 

[Visual Studio Tools](https://visualstudio.microsoft.com/downloads/#other)

Scroll to bottom download, BUILD TOOLS FOR VISUAL STUDIO 2022
![image](https://github.com/paxabacus/Proteus490/assets/64762646/86159628-5464-4bc4-ab9b-e32667cc9b1c)

### C++ with Visual Studio

- Check **Dekstop Development with C++**
- On search box
  - Look up **Universal C Runtime**
  - Check the box for it
- Click that install


# PATH ENVIRONMENT EDITING

## Finding Environment Edit

![image](https://github.com/paxabacus/Proteus490/assets/64762646/23362d4d-6c43-42e8-b7e1-f3e24d917744)
> Ignore my gis work -AB

## Swift Path

By default, Swift's Directory is `C:\Swift\bin"

## Setting PATHS

### User Path

1. Double Click Path
![image](https://github.com/paxabacus/Proteus490/assets/64762646/872dc209-1e72-4dec-988f-6cf71dadf4fd)

2. Enter Swift's Path as a New Variable
![image](https://github.com/paxabacus/Proteus490/assets/64762646/3647555b-7176-4634-88b8-a16f3d293411)


### System Variables

1. Double Click Path in System Variables
![image](https://github.com/paxabacus/Proteus490/assets/64762646/f93b7042-57d3-4fd0-b732-c7437f835142)

2. ADD SWIFT
![image](https://github.com/paxabacus/Proteus490/assets/64762646/1e9b8cd7-3abf-4345-a9e7-9b37f9572b94)

### Apply and hope it works

![image](https://github.com/paxabacus/Proteus490/assets/64762646/0d553348-1a2c-4bf7-8db3-5282b60f432e)

# VSCode again

## Creating a new file - PROTEUS PACKAGE

Paste the folloiwng into a new file called "**Proteus.swift**"

```
// swift-tools-version:5.6.2

import PackageDescription

let package = Package(
    name: "Proteus",
    products: [
        .executable(name: "Proteus", targets: ["Proteus"]),
    ],
    dependencies: [
        .package(url: "https://github.com/apple/swift-argument-parser.git", from: "1.0.0"),
    ],
    targets: [
        .target(
            name: "Proteus",
            dependencies: [.product(name: "ArgumentParser", package: "swift-argument-parser")],
            path: "Sources"
        )
    ]
)
```

Example of how it should look:
![image](https://github.com/paxabacus/Proteus490/assets/64762646/4225b52b-2f2f-4bf8-8d2e-a081a9b466f0)

## Sources Folder - MAIN.SWIFT

1. Go to the sources folder
2. Change the file called "**main.swift**" to have the following

```
//
//  main.swift
//  Proteus
//
//  Created by Matthew Fuller on 9/30/21.
//  Copyright © 2022 CSUNTAVLAB. All rights reserved.
//

import ArgumentParser
import Foundation

var errorStream = StandardErrorOutputStream()

struct ProteusCompiler: ParsableCommand {
    static var configuration = CommandConfiguration(
        abstract: "A Proteus language compiler written in Swift.",
        version: "0.0.1",
        subcommands: [Build.self]
    );
}

@main
extension ProteusCompiler {
    struct Build: ParsableCommand {
        static var configuration = CommandConfiguration(
            abstract: """
                Build a `.proteus` file into a valid C language \
                output file that utilizes QPC.
                """)

        @Argument(help: "The input `.proteus` file to build.")
        var inputFile: String

        mutating func run() {
            build(inputFile)
        }
    }
}

private func build(_ inputFile: String) {
    // guard let QPC = ProcessInfo.processInfo.environment["QPC"] else {
    //     print(
    //         """
    //         QPC path needs to be defined as an ENVIRONMENT variable for \
    //         swift-proteus to work.
    //         """,
    //         to: &errorStream
    //     )
    //     return
    // }

    let inputResult: InputResult
    do {
        inputResult = try readInput(inputFile)
    } catch {
        print("Error info: \(error)", to: &errorStream)
        return
    }

    let inputFileContents: String
    do {
        inputFileContents = try inputResult.get()
    } catch {
        print("Error info: \(error)", to: &errorStream)
        return
    }

    let result: LexerResult = Lexer(input: inputFileContents).lexify()
    var tokens: Array<Sourced<Token>> = Array()
    switch result {
    case .success(let data):
        tokens = data
    case .failure(let data):
        print(data.getWhat(), to: &errorStream)
        return
    }

//    if case let .success(tokens) = result {
//        print(tokens.count)
//        print("The tokens are:\n")
//        var stringTokens = String()
//        for token in tokens[0..<tokens.count - 1] {
//            stringTokens += token.getInner().printDebugToken()
//            stringTokens += " "
//        }
//        stringTokens += tokens.last!.getInner().printDebugToken()
//        stringTokens += "\n"
//
//        print(stringTokens)
//    }

    let parserInput: ParserInput
    do {
        parserInput = try ParserInput(tokens: tokens)
    } catch let error {
        print("Error info: \(error.localizedDescription)", to: &errorStream)
        return
    }

    let parser = Parser(parserInput: parserInput)
    let program: Program
    do {
        program = try parser.parseProgram().get()
    } catch let error {
        print("Parser Error: \(error)", to: &errorStream)
        return
    }

//    switch parser.parseProgram() {
//    case .success(let data):
//        program = data
//    case .failure(let data):
//        print()
//        print("parser failure dump:")
//        print(data.getErrorType())
//        print(data.getLocation().getSourceFirst().line)
//        print(data.getLocation().getSourceSecond().line)
//        print(data.getLocation().getSourceFirst().column)
//        print(data.getLocation().getSourceSecond().column)
//        print(data.getLocation().getSourceFirst().index)
//        print(data.getLocation().getSourceSecond().index)
//        print(data.getWhat())
//        return
//    }

    let typeEnvironment: TypeEnvironment
    do {
        let typechecker = try TypeChecker(program: program)
        switch try typechecker.typecheck() {
        case .success(let data):
            typeEnvironment = data
        case .failure(let data):
            print("typechecker failure dump:")
            print(data.getErrorType())
            print(data.getLocation().getSourceFirst().line)
            print(data.getLocation().getSourceSecond().line)
            print(data.getLocation().getSourceFirst().column)
            print(data.getLocation().getSourceSecond().column)
            print(data.getLocation().getSourceFirst().index)
            print(data.getLocation().getSourceSecond().index)
            print(data.getWhat())
            return
        }
    } catch TypecheckerError.error(let string) {
        print("Typechecker: \(string)", to: &errorStream)
        return
    } catch TypeEnvironmentError.error(let string) {
        print("TypeEnvError: \(string)", to: &errorStream)
        return
    } catch ScopeError.error(let string) {
        print("ScopeError: \(string)", to: &errorStream)
        return
    } catch GenEnvironmentError.error(let string) {
        print("GenEnvError: \(string)", to: &errorStream)
        return
    } catch FuncBuilderError.error(let string) {
        print("FuncBuilderError: \(string)", to: &errorStream)
        return
    } catch BuiltinFunctionError.error(let string) {
        print("BuiltinFunctionError: \(string)", to: &errorStream)
        return
    } catch LValueCheckerError.error(let string) {
        print("LValueCheckerError: \(string)", to: &errorStream)
        return
    } catch let unknownError {
        print("Error: \(unknownError)", to: &errorStream)
        print("Error type: \(unknownError.localizedDescription)", to: &errorStream)
        if let dispStyle = Mirror(reflecting: unknownError).displayStyle {
            print("Error type displaystyle: \(dispStyle)", to: &errorStream)
        }
        return
    }

    print("Success!")
}

//ProteusCompiler.main()
```
Exampel of how it should look:
![image](https://github.com/paxabacus/Proteus490/assets/64762646/e2144dfe-e171-409b-89b3-7ea013fcd2b4)

## Building the Proteus


1. Open a temrinal in VS Code
2. Run the following command in the **Sources Directory** where **main.swift** is located in
```
swift build
```
![image](https://github.com/paxabacus/Proteus490/assets/64762646/537cf0d0-290d-428c-a104-be8ffb0954dc)


## Error Handling

![image](https://github.com/paxabacus/Proteus490/assets/64762646/b343a779-6fc1-47c6-88f5-587b152cf861)

Use this terminal:
![image](https://github.com/paxabacus/Proteus490/assets/64762646/002f1288-dd9e-4964-ba90-539150077e3f)

1. cd to repo
2. Rerun `swift build`
3. check main.swift syntax again

# Running example code

1. cd .build\debug
2. Create 1.proteus with the following code;
```
event CLOCK{int};

actor Man {
    statemachine {
        initial Awake;

        int wake_count = 0;

        state Awake {
            on CLOCK{hour} {
                goif (hour == 22) Asleep {}
            }
        }

        state Asleep {
            on CLOCK{hour} {
                goif (hour == 7) Awake {
                    wake_count = wake_count + 1;
                }
            }
        }
    }
}
```

# fixng my paths hold up.
