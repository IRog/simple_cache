# SimplerCache

[![Build Status](https://travis-ci.com/IRog/simpler_cache.svg?branch=master)](https://travis-ci.com/IRog/simpler_cache)
[![Coverage Status](https://coveralls.io/repos/github/IRog/simpler_cache/badge.svg?branch=master)](https://coveralls.io/github/IRog/simpler_cache?branch=master)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Hex pm](http://img.shields.io/hexpm/v/simpler_cache.svg?style=flat)](https://hex.pm/packages/simpler_cache)
[![hexdocs.pm](https://img.shields.io/badge/docs-latest-green.svg?style=flat)](https://hexdocs.pm/simpler_cache/)

## Description

A very simple cache. It uses timers for the ttl and ets for the storage. No locks are used and there is a fix to prevent thundering herd issues when the cache is warm and pre-emptively refresh the cache (it triggers in low ttl left of item situations). There is also a thundering herd fix for when the cache is cold using a sentinel key and a sleep.
Mostly wrapper around ets and kept very simple by using newer apis and recent erlang improvements.

Using property model testing and property tests to verify the cache via propcheck.

## Installation

[available in Hex](https://hex.pm/packages/simpler_cache), the package can be installed
by adding `simpler_cache` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:simpler_cache, "~> 0.1.7"}
  ]
end
```

- Sample configs
```
config :simpler_cache,
  cache_name: :simpler_cache_test,
  global_ttl_ms: 100_000
```

### 100 processes concurrently hitting cache on 1 key with get_or_store
![iterations](https://github.com/IRog/simpler_cache/blob/benchmark/images/100_iterations.png)

![runtime](https://github.com/IRog/simpler_cache/blob/benchmark/images/100_runtime.png)