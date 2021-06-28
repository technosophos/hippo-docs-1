---
title: HIPPOFACTS Format
description: The HIPPOFACTS file format
type: docs
---

A HIPPOFACTS file must be written in [TOML].
See [Configure an application with HIPPOFACTS][configure] for additional details on how this file is used.

```toml
# Define metadata about the application
[bindle]
  name = "Name of the application"
  version = "1.2.3" # Must be semver v2, without leading v prefix
  description = "Optional description of the application"
  authors = ["Your Name", "Another Name"] # Optional list of application authors

# Define one or more request handlers
[[handlers]]
  route = "/endpoint1" # Request path that should be handled by a WebAssembly module
  name = "bin/myapp1.wasm" # Relative path to a WebAssembly module that should handle the request
  files = ["images/*.jpg", "images/logos/myapp1.png"] # Optional list of files to deploy with the module
```

### \[bindle\]

The bindle section defines metadata about your application:

* **name**: The name of the application
* **version**: The application version. Follows [semver v2] and does not allow a leading v prefix.
* **description**: OPTIONAL. A plaintext description of the application.
* **authors**: OPTIONAL. A list of author names.

### [[handler]]

The handler entries can be repeated as many times as needed.
Handlers define endpoints for your application and the WebAssembly module that should receive requests.

* **route**: The request path. It should start a leading forward slash "/", and does not support wildcards.
* **name**: Relative path to the WebAssembly module (*.wasm file) that should handle the request.
* **files**": OPTIONAL. A list of relative file paths of static files that should be deployed with the WebAssembly module. These files are available to the module when it is serving requests.

[TOML]: https://toml.io/
[configure]: {{< relref "configuration.md" >}}