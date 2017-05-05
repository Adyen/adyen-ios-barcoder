# AdyenBarcoder
Use Verifone Barcode scanner over MFi

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Installation

### CocoaPods

AdyenBarcode will be available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod "AdyenBarcoder"
```

### Manual

Copy files from `AdyenBarcoder` folder.

## Usage

You need to add `com.verifone.pmr.barcode` in the `Supported external accessory protocols` into `Info.plist` file

### Initializing

To initialize Barcoder library simply get the shared instance and set your `BarcoderDelegate`.
```swift
let barcoder = Barcoder.sharedInstance
barcoder.delegate = self
```

### BarcoderDelegate

The only mandatory method is `didScan(barcode:)`. This is where the result of the scan will be delivered. You can also receive state updates on `didChange(status:)`. 

```swift
@objc public protocol BarcoderDelegate {
    func didScan(barcode: Barcode)
    @objc optional func didChange(status: BarcoderStatus)
    @objc optional func didReceiveLog(message: String)
}
```

### SoftScan
For starting a soft scan: 
```swift
barcoder.startSoftScan()
```

To stop the soft scan: 
```swift
barcoder.stopSoftScan()
```

### Logging

There are five log levels available: None, Error, Info, Debug, Trace. 
To set the log level simply set the variable on your `Barcoder` instance: 
```swift
barcoder.logLevel = .debug
```
You will receive each new log message via `BarcoderDelegate` method `didReceiveLog(message:)`.
