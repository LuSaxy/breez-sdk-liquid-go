# Breez Liquid SDK – Go Package

The [Breez Liquid SDK](https://github.com/breez/breez-sdk-liquid) enables developers to integrate Liquid into their apps with a very shallow learning curve. More information can be found [here](https://github.com/breez/breez-sdk-liquid).

## 👨‍🔧 Installation

To install the package:

```sh
$ go get github.com/breez/breez-sdk-liquid-go
```

### Supported platforms

This package embeds the Breez Liquid SDK runtime compiled as shared library objects, and uses [`cgo`](https://golang.org/cmd/cgo/) to consume it. A set of precompiled shared library objects are provided. Thus this package works (and is tested) on the following platforms:

<table>
  <thead>
    <tr>
      <th>Platform</th>
      <th>Architecture</th>
      <th>Triple</th>
      <th>Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4">Android</td>
      <td><code>amd64</code></td>
      <td><code>x86_64-linux-android</code></td>
      <td>✅</td>
    </tr>
    <tr>
      <td><code>aarch64</code></td>
      <td><code>aarch64-linux-android</code></td>
      <td>✅</td>
    </tr>
    <tr>
      <td><code>aarch</code></td>
      <td><code>armv7-linux-androideabi</code></td>
      <td>✅</td>
    </tr>
    <tr>
      <td><code>386</code></td>
      <td><code>i686-linux-android</code></td>
      <td>✅</td>
    </tr>
    <tr>
      <td rowspan="2">Darwin</td>
      <td><code>amd64</code></td>
      <td><code>x86_64-apple-darwin</code></td>
      <td>✅</td>
    </tr>
    <tr>
      <td><code>aarch64</code></td>
      <td><code>aarch64-apple-darwin</code></td>
      <td>✅</td>
    </tr>
    <tr>
      <td rowspan="2">Linux</td>
      <td><code>amd64</code></td>
      <td><code>x86_64-unknown-linux-gnu</code></td>
      <td>✅</td>
    </tr>
    <tr>
      <td><code>aarch64</code></td>
      <td><code>aarch64-unknown-linux-gnu</code></td>
      <td>✅</td>
    </tr>
    <tr>
      <td>Windows</td>
      <td><code>amd64</code></td>
      <td><code>x86_64-pc-windows-msvc</code></td>
      <td>✅</td>
    </tr>
  </tbody>
</table>

## 📄 Usage

``` go
package main

import (
	"github.com/breez/breez-sdk-liquid-go/breez_sdk_liquid"
)

func main() {
  mnemonic := "abandon abandon abandon abandon abandon abandon abandon abandon abandon abandon abandon about"

  sdk, err := breez_sdk_liquid.Connect(breez_sdk_liquid.ConnectRequest{
	  Mnemonic: mnemonic,
		DataDir: nil,
		Network: breez_sdk_liquid.NetworkLiquidTestnet,
	})
}
```

## Bundling

For some platforms the provided binding libraries need to be copied into a location where they need to be found during runtime.

### Android

Copy the binding libraries into the jniLibs directory of your app
```bash
cp vendor/github.com/breez/breez-sdk-liquid-go/breez_sdk_liquid/lib/android-386/*.so android/app/src/main/jniLibs/x86/
cp vendor/github.com/breez/breez-sdk-liquid-go/breez_sdk_liquid/lib/android-aarch/*.so android/app/src/main/jniLibs/armeabi-v7a/
cp vendor/github.com/breez/breez-sdk-liquid-go/breez_sdk_liquid/lib/android-aarch64/*.so android/app/src/main/jniLibs/arm64-v8a/
cp vendor/github.com/breez/breez-sdk-liquid-go/breez_sdk_liquid/lib/android-amd64/*.so android/app/src/main/jniLibs/x86_64/
```
So they are in the following structure
```
└── android
    ├── app
        └── src
            └── main
                └── jniLibs
                    ├── arm64-v8a
                        ├── libbreez_sdk_liquid_bindings.so
                        └── libc++_shared.so
                    ├── armeabi-v7a
                        ├── libbreez_sdk_liquid_bindings.so
                        └── libc++_shared.so
                    ├── x86
                        ├── libbreez_sdk_liquid_bindings.so
                        └── libc++_shared.so
                    └── x86_64
                        ├── libbreez_sdk_liquid_bindings.so
                        └── libc++_shared.so
                └── AndroidManifest.xml
        └── build.gradle
    └── build.gradle
```

### Windows

Copy the binding library to the same directory as the executable file or include the library into the windows install packager.
```bash
cp vendor/github.com/breez/breez-sdk-liquid-go/breez_sdk_liquid/lib/windows-amd64/*.dll build/windows/
```

## 💡 Information for Maintainers and Contributors

This repository is used to publish a Go package providing Go bindings to the Breez Liquid SDK's [underlying Rust implementation](https://github.com/breez/breez-sdk-liquid). The Go bindings are generated using [UniFFi Bindgen Go](https://github.com/NordSecurity/uniffi-bindgen-go).

Any changes to the Breez Liquid SDK, the Go bindings, and the configuration of this Go package must be made via the [breez-sdk-liquid](https://github.com/breez/breez-sdk-liquid) repo.
