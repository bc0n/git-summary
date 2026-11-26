# git-summary

This tool quickly and prettily summarises the state of all the git repos in some folder (non-recursively).  The summary
tells you which branch is checked out, and how dirty the repo is.

The motivation for writing it was that I was working on a project involving a number of microservices, so I had a folder
with about 20 repos in it and I wanted a good way to summarise their respective states.

It has some nice features:

  - For speed, queries each repo concurrently (may be disabled).
  - For prettiness, updates each repo's output line concurrently using fancy ANSI shiz (may be disabled).
  - For speed, doesn't fetch from remotes by default (but can).
  - For prettiness, coloured output using fancy ANSI shiz (may be disabled, for monochrome output).
  - For convenience, disables all the fancy ANSI shiz automatically if it detects that output is being piped out.
  - For convenience, a default target path can specified in an env var (was handy in my microservices case).

The combination of the first two features (concurrent queries and concurrent output updates) means that by default the
tool is rather fast and feels pleasantly responsive.  Either of these features may be disabled if they're causing
problems; if they're both disabled it simply trudges through the repos one at a time, writing output as it goes, like a
peasant.

The built-in help is extensive, so either run the tool with the `--help` flag or examine the source for more details.

## Example output

![Demo session SVG](https://gimbo.github.io/git-summary/git-summary-demo.svg "Demo Session SVG")

## Requirements

  - Python 3.9 or newer.
  - `git` available on your `PATH`.

## Installation

Install it with [pipx](https://pipx.pypa.io/), which puts `git-summary` on your `PATH` in its own isolated environment:

```bash
pipx install git+https://github.com/bc0n/git-summary
```

Or, from a clone of this repo:

```bash
pip install .
```

(Don't use `python setup.py install`: it's deprecated and won't install the dependencies.)

## Caveats

  - I use this in iTerm2 under MacOS and it works well. In other terminals and other operating systems, the "fancy
    ANSI shiz" may be less good, in particular the thing that tries to work out the cursor's position when the
    program starts (which is needed to get the fancy updates working) might fail.  But that's OK, you can always
    just disable it or fix it.  :-)

  - On Windows the cursor-position check doesn't work, so fancy mode clears the screen before drawing.  Use
    `--simple`/`-s` if you'd rather keep your scrollback.

  - [git-extras](https://github.com/tj/git-extras) contains a "git-summary" tool which does something entirely
    different.  Oops, my bad.  Ah well, never mind...

--

Andy Gimblett
October 2018 (though the codebase is a couple of years old now)
