<h1 align="center">Log Viewer</h1>

<h3 align="center">A framework for monitoring requests and events on iOS.</h3>

<p align="center">
  Get a clear view of all requests made to your app and easily locate issues and crashes.
  <br />
  Create custom logs for any important event, such as user interactions, data sent to the server, or any other event service.
</p>

<p align="center">
<img src="https://github.com/FliperProjects/LogViewerDoc/blob/main/img/LogViewerSimulator.png" width="750px">
</p>

## Installation

<details><summary>CocoaPods</summary><ul>
<br />
  
In your `Podfile`

* If you want the library in binary format:

<br />

```ruby
target '<Your Target Name>' do
  pod 'LogViewer', :git => 'https://<LOG_VIEWER_TOKEN>@github.com/FliperProjects/LogViewerFramework.git', :tag => '1.0.0'
end
```

* If you want the library with source code:

<br />

```ruby
target '<Your Target Name>' do
  pod 'LogViewer', :git => 'https://<LOG_VIEWER_TOKEN>@github.com/FliperProjects/LogViewer.git', :tag => '1.0.0'
end
```

</ul></details>

<details><summary>Swift Package Manager</summary><ul>
<br />

In the top menu of Xcode, click on `File` then `Add Package Dependencies...` and paste the git URL:

* If you want the library in binary format:

<br />

```bash
https://<LOG_VIEWER_TOKEN>@github.com/FliperProjects/LogViewerFramework.git
```

* If you want the library with source code:

<br />

```bash
https://<LOG_VIEWER_TOKEN>@github.com/FliperProjects/LogViewer.git
```

<p align="left">
<img src="https://github.com/FliperProjects/LogViewerDoc/blob/main/img/LogViewerSPMImage.png" width="600px">
</p>
<hr>

To add it as a dependency of another package:

In your `Package.swift`:

* If you want the library in binary format:

<br />
  
```swift
dependencies: [
  .package(url: "https://<LOG_VIEWER_TOKEN>@github.com/FliperProjects/LogViewerFramework.git", .exact("1.0.0"))
]
```

* If you want the library with source code:

<br />

```swift
dependencies: [
  .package(url: "https://<LOG_VIEWER_TOKEN>@github.com/FliperProjects/LogViewer.git", .exact("1.0.0"))
]
```

To depend on the LogViewer target:

```swift
.product(name: "LogViewer", package: "LogViewer")
```

</ul></details>

<details><summary>Manually</summary><ul>
<br />
  
In terminal, open the root folder of your project:
  
```bash
cd MyProject
```

Download file `LogViewer.xcframework` with the command:

```bash
curl -O https://<LOG_VIEWER_TOKEN>@raw.githubusercontent.com/FliperProjects/LogViewerFramework/refs/heads/main/LogViewer.xcframework.zip && unzip LogViewer.xcframework.zip > /dev/null && rm LogViewer.xcframework.zip
```

Open the project and, next, select your application project in the Project Navigator (blue project icon) to navigate to the target configuration window and select the application target under the `Targets` heading in the sidebar.

In the tab bar at the top of that window, open the `General` panel.

Click on the `+` button under the `Framework, Libraries, and Embedded Content` section.

Add `LogViewer.xcframework` and mark `Embed & Sign` option.
<p align="left">
<img src="https://github.com/FliperProjects/LogViewerDoc/blob/main/img/LogViewerFrameworkImage.png" width="600px">
</p>

</ul></details>

## Configuration

<details><summary>UIKit</summary><ul>
<br />
  
In an AppDelegate based UIKit app, initialize LogViewerProvider inside:
  
```swift
import UIKit
import LogViewer

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?

    func application(
        _ application: UIApplication,
        didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
    ) -> Bool {
        window = UIWindow(frame: UIScreen.main.bounds)

        // Call LogViewerProvider after window was created.
        LogViewerProvider.setEnableInDebug(true)
        LogViewerProvider.setEnableInRelease(false)
        
        return true
    }
}
```

</ul></details>

<details><summary>SwiftUI</summary><ul>
<br />
  
In a SwiftUI app, initialize LogViewerProvider inside @main struct:
  
```swift
import SwiftUI
import LogViewer

@main
struct MyApp: App {
    init() {
        LogViewerProvider.setEnableInDebug(true)
        LogViewerProvider.setEnableInRelease(false)
    }

    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

</ul></details>

## Usage

<details><summary>Record Network</summary><ul>
<br />

<details><summary>Native</summary><ul>
<br />
  
Just send the `modelType` parameter to the default function that makes the requests in your application:
* The `modelType` is expected model for the task response. This can be any type that conforms to `Decodable`, or `nil` / `void`  if a response model is not expected.

#### session.dataTask
```swift
  session.dataTask(with: urlRequest, modelType: Model.self) { data, response, error in
  ...
```
#### session.uploadTask
```swift
  session.uploadTask(with: urlRequest, from: uploadData, modelType: Model.self) { data, response, error in
  ...
```
#### session.data
```swift
  session.data(for: urlRequest, modelType: Model.self)
  ...
```
#### session.upload
```swift
  session.upload(for: urlRequest, from: uploadData, modelType: Model.self)
  ...
```

</ul></details>
  
<details><summary>Manual</summary><ul>
<br />

Call LogViewerProvider to register request in your custom request function:

```swift
  LogViewerProvider.recordNetwork(
      urlRequest: urlRequest,
      uploadData: uploadData, //If is a upload request
      responseData: data,
      response: response,
      error: error,
      modelType: Model.self
  )
```

</ul></details>

</ul></details>

<details><summary>Record Custom</summary><ul>
<br />

Record any other information you deem necessary. Analytics for example:

```swift
  LogViewerProvider.recordCustom(
      iconChar: "🔖",
      title: "Analytics",
      payload: "Custom Event",
      data: eventData //Optional
  )
```

</ul></details>


## Author

Lucas Siqueira: lucassiqueira.ap@gmail.com

## License

LogViewer is available under the Custom license. See the LICENSE file for more info.
