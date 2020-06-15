# OPS – the Octave Production Server

The Octave Production Server is the Octave equivalent of the [Matlab Production Server](https://www.mathworks.com/products/matlab-production-server.html). It would allow you to deploy and run Octave code on a server that presents an HTTP/JSON web service interface for calling your Octave code.

## This Is a Hypothetical Project

This project does not exist yet! I'm only creating this repo as a placeholder to see if there's any interest in having me (or other people) build this thing. If you would like to see Octave Production Server exist, head on over to [the survey Issue](https://github.com/apjanke/OPS/issues/1) and leave a comment expressing your interest and use cases.

## What It Would Do

The Octave Production Server would allow you to deploy and run Octave code on a server that presents an HTTP/JSON web service interface for calling your Octave code. It would manage a pool of Octave worker processes and user-supplied Octave code that you could call remotely from a web service client, to run Octave workloads on a server.

### Features

* An HTTP endpoint
* JSON-based web service protocol for submitting Octave code and data structures as queries, and receiving Octave data structures as responses
* A pool of warm, concurrent Octave worker processes to run the tasks
  * Configurable refreshing of workers to deal with memory fragmentation issues etc.
* Registration of multiple Octave runtimes for running the code
  * With some nice friendly default
* Deployment of user code as named programs or packages
  * Versioning of deployed user code units
  * Transactional, zero-downtime user code deployment mechanism
* A single-file user code bundling and deployment format
  * Maybe this is just a `pkg` archive file; maybe it's something else
* Runs on Linux, Windows, and macOS
* A Discovery API for getting metadata about deployed user code
* A Statistics API for getting info and metrics about the server process
* A Management API for remotely controlling the server and managing the worker pool
* Synchronous service call support
* Asynchronous service call support
  * Submit your task in one async service call, then poll for completion and pick up results in additional service calls
* Logging

#### Maybe Features

* Client authentication and access controls?
* A utilization-aware load balancer?
* A human-usable web page control panel front-end?
* A native Octave client?
* Apache Arrow support?

### Open Questions

* Is this actually a good idea? Maybe people writing Octave programs should just package them up as regular applications, deploy those, and write their own custom web front-ends for them.
* Is there some generic "run a language interpreter behind a web service" tool or framework we should be using instead of building something custom?
* Should it run its own embedded web server, or run behind a regular web server like Apache httpd or nginx?
* How will the association of deployed code units to defined Octave runtimes be done?
* Should it support multiple Octave runtimes of a given version?
  * E.g. to support Octave builds with different options
* How should MEX and OCT files in deployed code be handled?
  * Should compilation be done as part of the code package deployment? Or should we require them to be precompiled? Would compilation be done against each registered Octave runtime? How to handle DLL linkage dependencies on specific Octave installation paths?
* How will dependencies on Octave packages be handled?
  * This includes both standard Octave Forge packages and user-supplied custom packages.
  * And what about multiple package versions?
* There's probably some locale or character-encoding issue I'm not thinking of.
* Should worker processes be re-used between queries, or should we just fire up a clean process for each service call?
  * Re-using processes supports caching with `persistent` and `constant` variables and is more resource-efficient, but complicates state management and debugging.

## Architecture

Probably written in Java, because that's an easy language, has libraries for all the web stuff we'd need, and is cross-platform.

## License

This would be GNU GPL, like Octave itself.

## Author

Nobody has written any actual code yet, but this survey project was set up by [Andrew Janke](https://apjanke.net).

The project home page is [apjanke/OPS on GitHub](https://github.com/apjanke/OPS).
