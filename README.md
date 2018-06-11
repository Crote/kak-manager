# kak-manager: Kakoune session management made easy

## What is kak-manager?

`kak-manager` is a small tool which makes it easier to keep track of your [Kakoune](http://kakoune.org/) sessions, making it trivially easy to join a Kakoune session for a project, even when you're in a different directory.

## Example

Let's say you have the following directory structure:

```
/foo
  /bar
    /baz
  /quux
```

There are a couple of different cases which may occur. First, if you have a session in `/foo/bar` and you start a new session in the same directory, you probably want to join the existing session. This is quite obvious, and this behaviour is implemented in [alexherbo2/project.kak](https://github.com/alexherbo2/project.kak) and even mentioned in the [Kakoune wiki](https://github.com/mawww/kakoune/wiki/Kak-daemon-helper-:-1-session-per-project). Kak-manager aims to be a subset of this.

Let's say your project root is at `/foo/bar` and you started your first session in that directory. If you were to start a new editor in `/foo/bar/baz`, you probably want to join the existing session.

Similarly, if your first session was started in `/foo/bar/baz` and you're now starting an editor in `/foo/bar`, you probably want to join the existing session, but relabel it as a session in `/foo/bar`, because that's the real root.

If your project root is at `/foo/bar` and you have a session there, but you start a session in `/foo/quux`, you probably want to create a new session, because it's an unrelated directory.

However, if your project root were to be `/foo`, you probably want to join the existing session and relabel it to have it's root at `/foo`. This is a bit less likely than the previous one, though.

Finally you may have created your own non-project specific session and you may want to join it, or you may want to create a new session even though one of the previous options exists.

When used, `kak-manager` looks up all existing Kakoune sessions and asks the user which one they want to join. The default option is determined according to the rules described above, so in most cases you can simply press enter to do what you want to do. This should result in a hassle-free editing experience, even when traversing your project directory structure.

## FAQ

### Does it alter the working directory?

No.

## Dependencies

- Kakoune should be installed and available as `kak`.
- A recent version of Python (probably 3.6 or later) should be installed.

## Installation

Place the file `kak-manager` somewhere where it can be executed. If you do not know a suitable location, you can use `echo "$PATH"` to find one. `~/.local/bin/` is probably a good choice. Make sure that the file is executable.

`kak-manager` only outputs which Kakoune flags to use. To make this useful, you should probably add the following alias to your `~/.bashrc`:

```
alias kakm='eval $(kak-manager)'
```

This allows you to simply type `kakm` instead of `kak` to automatically handle your sessions. Passing arguments, such as the files to open, will work as usual, with the exception of the `-e` flag, which will not work.

Note that you can not alias this as `kak`: this will result in an infinite loop.

## Contributing

The primary repository for kak-manager is on [GitLab](https://gitlab.com/Crote/kak-manager), a mirror exists on [Github](https://github.com/Crote/kak-manager). Issues and pull requests are accepted on either of them, but GitLab is preferred.

## Licence

This project is licenced under LGPLv3. If you are not familiar with this licence, please read `LICENCE_LGPL` and `LICENCE_GPL`.

