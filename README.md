# Lorem Ipsum

[![](https://travis-ci.org/mgeisler/lipsum.svg?branch=master)][travis-ci]
[![](https://ci.appveyor.com/api/projects/status/github/mgeisler/lipsum?branch=master&svg=true)][appveyor]
[![](https://codecov.io/gh/mgeisler/lipsum/branch/master/graph/badge.svg)][codecov]
[![](https://img.shields.io/crates/v/lipsum.svg)][crates-io]
[![](https://docs.rs/lipsum/badge.svg)][api-docs]

Lipsum is a small Rust library for generating pseudo-Latin [lorem
ipsum filler text][lorem ipsum]. This is a standard placeholder text
used in publishing. It starts with:

> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
> eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
> ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
> aliquip ex ea commodo consequat…

The text is generated using a [Markov chain] that has been trained on
the first book in Cicero's work _De finibus bonorum et malorum_ (_On
the ends of good and evil_), of which the lorem ipsum text is a
scrambled subset.

## Usage

Add this to your `Cargo.toml`:

```toml
[dependencies]
lipsum = "0.8"
```

## Documentation

Please see the **[API documentation][api-docs]**.

## Getting Started

Use the `lipsum` function to generate lorem ipsum text:

```rust
use lipsum::lipsum;

fn main() {
    // Print 25 random words of lorem ipsum text.
    println!("{}", lipsum(25));
}
```

This generates the lorem ipsum text show above:

> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
> eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
> ad minim veniam, quis nostrud exercitation ullamco…

The text becomes random after 18 words, so you might not see exactly
the same text.

Use `lipsum_title` instead if you just need a short text suitable for
a document title or a section heading. The text generated by that
function looks like this:

> Refugiendi et Omnino Rerum

Small words are kept uncapitalized and punctuation is stripped from
all words.

## Release History

This is a changelog with the most important changes in each release.

### Version 0.8.1 (2022-04-19)

* [#73](https://github.com/mgeisler/lipsum/pull/73): Add
  `lipsum_from_seed` and tweak capitalization. Thanks @reknih!
* [#77](https://github.com/mgeisler/lipsum/pull/77): Update to Rust
  2021 edition.

### Version 0.8.0 — May 30th, 2021

The random number generator has been separated from the `MarkovChain`
implementation to allow using the same trained model to generate
multiple outputs with different seeds. Thanks @Diggsey!

### Version 0.7.0 — July 8th, 2020

-   The code has been updated to the [Rust 2018 edition][rust-2018].

-   Each new release will only support the latest stable version of
    Rust. Trying to support older Rust versions has proven to be a
    fool's errand: our dependencies keep releasing new patch versions
    that require newer and newer versions of Rust.

-   [#65](https://github.com/mgeisler/lipsum/pull/65): A new
    `lipsum_words_from_seed` function was added. It generates random but
    deterministic lorem ipsum text. This is useful in unit tests when
    you need fixed inputs.

### Version 0.6.0 — December 9th, 2018

The new `lipsum_words` function can be used to generate random lorem
ipsum text that doesn't always start with "Lorem ipsum".

Dependencies were updated and the oldest supported version of Rust is
now 1.22.

### Version 0.5.0 — April 22nd, 2018

The new `lipsum_title` function can be used to generate a short string
suitable for a document title or a section heading.

Dependencies were updated and the oldest supported version of Rust is
now 1.17.

### Version 0.4.0 — September 24th, 2017

The `generate` and `generate_from` now always generate proper
sentences, meaning that they generate sentences that start with a
capital letter and end with `.` or some other punctuation character.
Use `iter` and `iter_from` directly if you need more control.

### Version 0.3.0 — July 28th, 2017

Performance is improved by about 50% when generating text, but
training the Markov chain now takes about twice as long as before.

The `MarkovChain` struct has many new methods:

-   `new_with_rng` makes it possible to specify the random number
    generator used by the Markov chain. Use this to get deterministic
    and thus reproducible output for tests. `MarkovChain` now owns the
    RNG it uses and as a consequence, it has an extra type parameter.
    This is a breaking change if you used struct directly in your code.

-   `iter` and `into_from` return iterators over words in the Markov
    chain. The `generate` and `generate_from` methods are now
    straight-forward convenience wrappers for the iterators.

-   `len` tells you the number of stats in the Markov chain and
    `is_empty` tells you if the Markov chain is empty, meaning that it
    hasn't been trained on anything yet.

### Version 0.2.0 — July 10th, 2017

Rust version 1.6.0 is now supported. This is checked with TravisCI.

### Version 0.1.0 — July 2nd, 2017

First public release.

## License

Lipsum can be distributed according to the [MIT license][mit].
Contributions will be accepted under the same license.

[crates-io]: https://crates.io/crates/lipsum
[api-docs]: https://docs.rs/lipsum/
[codecov]: https://codecov.io/gh/mgeisler/lipsum
[lorem ipsum]: https://en.wikipedia.org/wiki/Lorem_ipsum
[markov chain]: https://en.wikipedia.org/wiki/Markov_chain
[travis-ci]: https://travis-ci.org/mgeisler/lipsum
[appveyor]: https://ci.appveyor.com/project/mgeisler/lipsum
[rust-2018]: https://doc.rust-lang.org/edition-guide/rust-2018/
[mit]: LICENSE
