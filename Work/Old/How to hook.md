This is a short example on how to set up and use .githooks for formatting in POS.

## Setup

You need to run this command inside your repo once after cloning it.
```bash
git config --local core.hooksPath .githooks/
```

## Checking if hooks work

1. Check if hook directory is set:
```bash
git config --local --get core.hooksPath
// it should show .githooks/
```

2. Checking in action. We will test 1 swiftFormat rule (braces) and 1 swiftLint rule (legacy constructor). Create a swift file inside POS/POS with this code inside:
```swift
// swiftformat violation
if x
{
let foo = 8
}

// swiftlint violation
GCPointMake(10,10)
```

3. Try to make a commit.
```bash
git add .
git commit -m "ABC-123: Test Commit"
```

4. Confirm that the file got formatted into this:
```swift
// swiftformat violation
if x {
let foo = 8
}

// swiftlint violation
CGPoint(x: 10, y: 10)
```
## Running manually

Both swiftformat and swiftlint binaries are inside `POS/BuildTools/bin`, so you can call them directly to format or check errors.
```bash
./BuildTools/bin/swiftformat --help  
./BuildTools/bin/swiftlint --help  
```

Specific commands for running formatters are:
```bash
# --fix says to auto fix problems
# config passes path to config
# unnamed argument is path which files to lint. it can be file or folder
./BuildTools/bin/swiftlint --fix --config .swiftlint.yml ./POS/hookTest.swift

# config passes path to config
# unnamed argument is path which files to lint. it can be file or folder
./BuildTools/bin/swiftformat --config .swiftformat ./POS/hookTest.swift
```

## xCode, VSCode, Source Tree
No additional setup is needed. If you use VSCode UI to commit, the hook works automatically.

