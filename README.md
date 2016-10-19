logger [![Build Status](https://secure.travis-ci.org/iron/logger.png?branch=master)](https://travis-ci.org/iron/logger)
====

> [Morgan](https://github.com/expressjs/morgan)-inspired logging middleware for the [Iron](https://github.com/iron/iron) web framework.

## Example

```rust
extern crate iron;
extern crate logger;

use iron::prelude::*;
use logger::Logger;

fn main() {
    let (logger_before, logger_after) = Logger::new(None);

    let mut chain = Chain::new(no_op_handler);

    // Link logger_before as your first before middleware.
    chain.link_before(logger_before);

    // Link logger_after as your *last* after middleware.
    chain.link_after(logger_after);

    Iron::new(chain).http("127.0.0.1:3000").unwrap();
}

fn no_op_handler(_: &mut Request) -> IronResult<Response> {
    Ok(Response::with(iron::status::Ok))
}
```

## Overview

Logger is a part of Iron's [core bundle](https://github.com/iron/core).

Logger emits request and response information using standard rust [log facade](https://doc.rust-lang.org/log/log/index.html), formatted with default format or a custom format string.

Format strings can specify fields to be logged (ANSI terminal colors and attributes is no longer supported since [#82](https://github.com/iron/logger/issues/82)).

## Installation

If you're using a `Cargo.toml` to manage dependencies, just add logger to the toml:

```toml
[dependencies.logger]

git = "https://github.com/iron/logger.git"
```

Otherwise, `cargo build`, and the rlib will be in your `target` directory.

## [Documentation](http://ironframework.io/doc/logger/)

Along with the [online documentation](http://ironframework.io/doc/logger/),
you can build a local copy with `make doc`.

## [Examples](/examples)

## Log implementations

To actually log anything, you will need to use some log implementation that will deliver the logs to your desired location, like standard output, a file or log collecting service. This is not responsibility of iron-logger alone. There are numerous such implementations to choose from, from simple ones that just write to standard error like [stderrlog](https://crates.io/crates/stderrlog), more configurable ones like [simplelog](https://crates.io/crates/simplelog) to ultimate solutions like [slog](https://crates.io/crates/slog). You can find more on [crates.io](https://crates.io/keywords/logging).

If you are looking for turn-key solution, just follow example from [simplelog](https://github.com/drakulix/simplelog.rs).


## Get Help

One of us ([@reem](https://github.com/reem/), [@zzmp](https://github.com/zzmp/),
[@theptrk](https://github.com/theptrk/), [@mcreinhard](https://github.com/mcreinhard))
is usually on `#iron` on the mozilla irc. Come say hi and ask any questions you might have.
We are also usually on `#rust` and `#rust-webdev`.

