<p align="center">
  <img
    src="https://raw.githubusercontent.com/dart-sys/dart-sys-branding-assets/main/dart-sys%20header.png"
    alt="Dart-sys brand header"
  >
  <br/>
  <br/>
</p>

# Dart-sys

[![Crates.io](https://img.shields.io/crates/v/dart-sys.svg)](https://crates.io/crates/dart-sys)
[![Docs.rs](https://docs.rs/dart-sys/badge.svg)](https://docs.rs/dart-sys)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![License: GNU GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Examples tests](https://github.com/dart-sys/dart-sys/actions/workflows/examples_tests.yml/badge.svg)](https://github.com/dart-sys/dart-sys/actions/workflows/examples_tests.yml)
[![Rust Tests](https://github.com/dart-sys/dart-sys/actions/workflows/rust_tests.yml/badge.svg)](https://github.com/dart-sys/dart-sys/actions/workflows/rust_tests.yml)

> _Rust bindings to the [Dart native extensions api](https://dart.dev/server/c-interop-native-extensions)_

## Getting Started 🚀

### Prerequisites 🔧

You will need the following tools available on your system:

- [Dart](https://dart.dev/get-dart) version 2.12 or higher
- [Rust](https://www.rust-lang.org/tools/install) version 1.51 or higher
- [Cargo](https://doc.rust-lang.org/cargo/getting-started/installation.html)
- [Git](https://git-scm.com/downloads)

### Installing 📦

Run the following Cargo command in your project directory:

```bash
cargo add dart-sys
```

Or add the following line to your Cargo.toml:

```toml
dart-sys = "3.1.5"
```

Source code releases for each SemVer tag are also available on the
[GitHub releases page](https://github.com/dart-sys/dart-sys/releases).

## Usage 💻

### Examples 📚

An extremely straightforward example of using `dart-sys` would be like such:

```rust
use dart_sys::{Dart_Handle, Dart_NewIntegerFromI64};

#[no_mangle]
/// Adds two integers together.
pub extern "C" fn dart_sys_example_extension_sum(
    a: Dart_Handle,
    b: Dart_Handle,
) -> Dart_Handle {
    let a = unsafe { Dart_NewIntegerFromI64(a) };
    let b = unsafe { Dart_NewIntegerFromI64(b) };
    a + b
}

#[no_mangle]
/// Multiplies two integers together.
pub extern "C" fn dart_sys_example_extension_product(
    a: Dart_Handle,
    b: Dart_Handle,
) -> Dart_Handle {
    let a = unsafe { Dart_NewIntegerFromI64(a) };
    let b = unsafe { Dart_NewIntegerFromI64(b) };
    a * b
}
```

```dart
import 'dart:ffi';

// open and link to the native library
final DynamicLibrary nativeLib = DynamicLibrary.open('libdart_sys_example_extension.so');

// lookup the sum function in the native library
final int Function(int, int) sum = nativeLib
    .lookup<NativeFunction<Int32 Function(Int32, Int32)>>('dart_sys_example_extension_sum')
    .asFunction();

// lookup the product function in the native library
final int Function(int, int) product = nativeLib
    .lookup<NativeFunction<Int32 Function(Int32, Int32)>>('dart_sys_example_extension_product')
    .asFunction();

void main() {
    print(sum(1, 2)); // 3
    print(product(1, 2)); // 2
}
```

While this example is certainly possible, you are not likely to ever use Dart-sys for this purpose.
See the [examples](https://github.com/dart-sys/dart-sys/tree/main/examples) directory for more in-depth
examples of how to use Dart-sys. All of the examples are tested using GitHub Actions and documented verbosely.

## Built With 🛠️

- [Rust](https://www.rust-lang.org/) - A systems programming language that runs
 blazingly fast, prevents segfaults, and guarantees thread safety.
- [Dart](https://dart.dev/) - A client-optimized language for fast apps on any platform.
- [Dart Native Extensions](https://dart.dev/server/c-interop-native-extensions) - A mechanism
 for writing native code in C/C++ and calling it from Dart.
- [bindgen](https://crates.io/crates/bindgen) - A Rust library for generating
 bindings to C and C++ APIs.

## Contributing ✏️

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct,
and the process for submitting pull requests. If you have any questions, please
open an issue, or contact admin <gutenfries@gmail.com> directly.

## Versioning 🪧

We use [SemVer](http://semver.org/) for versioning. For the versions available,
see the [tags on this repository](https://github.com/your/project/tags).

## License 📜

Dart-sys is open-sourced and released under the terms and conditions of the following three licenses:

- [MIT License](LICENSE-MIT.md)
- [Apache License (Version 2.0)](LICENSE-APACHE-2.0.md)
- [GNU General Public License (Version 3)](LICENSE-GPL-3.0.md)

## Acknowledgments 🙏

- [README starter](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2) by [@PurpleBooth](https://gist.github.com/PurpleBooth)
