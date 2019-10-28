# ansible-galaxy-install

A simple wrapper script that calls `ansible-galaxy install` but also enables transitive role requirement 
(dependency) downloads.

## How does it work?

It's a simple bash script that wraps the call to `ansible-galaxy install`, passing in all the same options and 
arguments.  The wrapper script just delegates to that command.

However, once `ansible-galaxy install` is finished running, if anything has been downloaded, the script
checks to see if any downloaded roles have a `meta/requirements.yml` file.  If so, the wrapper script
calls `ansible-galaxy install` on *those* requirements.yml files, passing along the same exact options that 
you specified.  It continues this process for all downloaded roles, walking the dependency tree 
until all transitive requirements have been resolved via `ansible-galaxy`.

## Install

git clone https://github.com/lhazlewood/ansible-galaxy-install
export PATH="ansible-galaxy-install/bin:$PATH"

## Usage

Once the `ansible-galaxy-install/bin` location is added to your `$PATH`, just call `ansible-galaxy-install` 
(with two dashes) instead of the native `ansible-galaxy install` (one dash, one space) command.

Use it identically to `ansible-galaxy install`, with all the same options and arguments.  The wrapper script
just delegates to that command.
