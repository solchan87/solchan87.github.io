# Swift 문법
> 2018.03.16 업데이트   

## URL Schem

```swift
private func openURL() {
    let URL = URL(string: "urlString")!
    // white list에 등록해야만 canOpenURL에서 true 값을 받아올 수 있다.
    if UIApplication.shared.canOpenURL(URL) {
        UIApplication.shared.open(URL)
    }
}
```

```XML
// info.plist 내 <dict> 에 white list 등록
<key>LSApplicationQueriesSchemes</key>
    <array>
        <string>urlString</string>
    </array>
```

