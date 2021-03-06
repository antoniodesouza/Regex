[![by Crossroad Labs](./header.png)](http://www.crossroadlabs.xyz/)

# Regex

![🐧 linux: ready](https://img.shields.io/badge/%F0%9F%90%A7%20linux-ready-red.svg)
[![GitHub license](https://img.shields.io/badge/license-Apache 2.0-lightgrey.svg)](https://raw.githubusercontent.com/crossroadlabs/Regex/master/LICENSE)
[![Build Status](https://travis-ci.org/crossroadlabs/Regex.svg?branch=master)](https://travis-ci.org/crossroadlabs/Regex)
[![GitHub release](https://img.shields.io/github/release/crossroadlabs/Regex.svg)](https://github.com/crossroadlabs/Regex/releases)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![CocoaPods version](https://img.shields.io/cocoapods/v/CrossroadRegex.svg)](https://cocoapods.org/pods/CrossroadRegex)
![Platform OS X | iOS | tvOS | watchOS | Linux](https://img.shields.io/badge/platform-Linux%20%7C%20OS%20X%20%7C%20iOS%20%7C%20tvOS%20%7C%20watchOS-orange.svg)

## Advanced regular expressions for Swift

## Goals

[<img align="left" src="https://raw.githubusercontent.com/crossroadlabs/Express/master/logo-full.png" hspace="20" height=128>](https://github.com/crossroadlabs/Express) Regex library was mainly introduced to fulfill the needs of [Swift Express](https://github.com/crossroadlabs/Express) - web application server side framework for Swift.

Still we hope it will be useful for everybody else.

[Happy regexing ;)](#examples)

## Getting started

### Installation

#### [Package Manager](https://swift.org/package-manager/)

Add the following dependency to your [Package.swift](https://github.com/apple/swift-package-manager/blob/master/Documentation/Package.swift.md):

```swift
.Package(url: "https://github.com/crossroadlabs/Regex.git", majorVersion: 0)
```

Run ```swift build``` and build your app. Package manager is supported on OS X, but it's still recommended to be used on Linux only.

#### [CocoaPods](http://cocoapods.org/)
Add the following to your [Podfile](http://guides.cocoapods.org/using/the-podfile.html):

```rb
pod 'CrossroadRegex'
```

Make sure that you are integrating your dependencies using frameworks: add `use_frameworks!` to your Podfile. Then run `pod install`.

#### [Carthage](https://github.com/Carthage/Carthage)
Add the following to your [Cartfile](https://github.com/Carthage/Carthage/blob/master/Documentation/Artifacts.md#cartfile):

```
github "crossroadlabs/Regex"
```

Run `carthage update` and follow the steps as described in Carthage's [README](https://github.com/Carthage/Carthage#adding-frameworks-to-an-application).

#### Manually
1. Download and drop ```/Regex``` folder in your project.  
2. Congratulations! 

### Examples

#### Hello Regex:

All the lines below are identical and represent simple matching. All operators and `matches` function return Bool

```swift
//operator way, can match either regex or string containing pattern
"l321321alala" =~ "(.+?)([1,2,3]*)(.*)".r
"l321321alala" =~ "(.+?)([1,2,3]*)(.*)"

//similar function
"(.+?)([1,2,3]*)(.*)".r!.matches("l321321alala")
```
Operator `!~` returns `true` if expression does **NOT** match:

```swift
"l321321alala" !~ "(.+?)([1,2,3]*)(.*)".r
"l321321alala" !~ "(.+?)([1,2,3]*)(.*)"
//both return false
```

#### Accessing groups:

```swift
// strings can be converted to regex in Scala style .r property of a string
let digits = "(.+?)([1,2,3]*)(.*)".r?.findFirst(in: "l321321alala")?.group(at: 2)
// digits is "321321" here
```

#### Named groups:

```swift
let regex:RegexType = try Regex(pattern:"(.+?)([1,2,3]*)(.*)",
                                        groupNames:"letter", "digits", "rest")
let match = regex.findFirst(in: "l321321alala")
if let match = match {
	let letter = match.group(named: "letter")
	let digits = match.group(named: "digits")
	let rest = match.group(named: "rest")
	//do something with extracted data
}
```

#### Replace:

```swift
let replaced = "(.+?)([1,2,3]*)(.*)".r?.replaceAll(in: "l321321alala", with: "$1-$2-$3")
//replaced is "l-321321-alala"
```

#### Replace with custom replacer function:

```swift
let replaced = "(.+?)([1,2,3]+)(.+?)".r?.replaceAll(in: "l321321la321a") { match in
	if match.group(at: 1) == "l" {
		return nil
	} else {
		return match.matched.uppercaseString
	}
}
//replaced is "l321321lA321A"
```

#### Split:

In the following example, split() looks for 0 or more spaces followed by a semicolon followed by 0 or more spaces and, when found, removes the spaces from the string. nameList is the array returned as a result of split().

```swift
let names = "Harry Trump ;Fred Barney; Helen Rigby ; Bill Abel ;Chris Hand"
let nameList = names.split(using: "\\s*;\\s*".r)
//name list contains ["Harry Trump", "Fred Barney", "Helen Rigby", "Bill Abel", "Chris Hand"]
```

#### Split with groups:

If separator contains capturing parentheses, matched results are returned in the array.

```swift
let myString = "Hello 1 word. Sentence number 2."
let splits = myString.split(using: "(\\d)".r)
//splits contains ["Hello ", "1", " word. Sentence number ", "2", "."]
```

## Roadmap

* v1.0: stable release (once we will see that no issues are coming)

## Changelog

* v0.7
	* Support of Swift 3.0 preview 1
	* Regex options support (like case sensetivity)
	* Breaking change (Swift 3.0ish syntax)
	* Renamed module in Pod from `CrossroadRegex` to `Regex`
* v0.6
	* Swift 3.0 support
* v0.5.1
	* Minor linux build related fixes
* v0.5
	* package manager support
	* full linux support 🐧
* v0.4.1
	* support for optionally present groups
* v0.4
	* iOS, tvOS and watchOS support
	* Pod supports watchOS
	* automated pod deployment
* v0.3
	* Split
	* Matches
	* CocoaPod
	* Syntactic sugar operators (`=~` and `!~`)
* v0.2
	* Replace functions
	* Carthage support
* v0.1
	* basic find functions for OS X and iOS

## Contributing

To get started, <a href="https://www.clahub.com/agreements/crossroadlabs/Regex">sign the Contributor License Agreement</a>.

## [![Crossroad Labs](http://i.imgur.com/iRlxgOL.png?1) by Crossroad Labs](http://www.crossroadlabs.xyz/)
