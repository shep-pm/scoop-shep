# scoop-shep

The Scoop bucket for [shep](https://github.com/shep-pm/shep), a process manager
that keeps a flock of long-running processes alive.

```powershell
scoop bucket add shep https://github.com/shep-pm/scoop-shep
scoop install shep
```

The manifest installs the portable x64 build from shep's GitHub release and
shims `shep.exe` only. `shep-runtime.exe` and `shep-dev.exe` are container
entrypoint aliases, so they land in the install directory without shims.

## Three things shep will not do on Windows

- `shep startup` is not built. Boot-time supervision on Windows needs a Service
  Control Manager service. Run `shep start` in your own session, or wrap
  `shep runtime` in NSSM or WinSW.
- `shep stop` has no SIGTERM equivalent to send, so it waits out the app's whole
  `kill_timeout` before terminating it. An app that opts into the shepherd
  channel with `shutdown_with_message` gets a graceful stop instead.
- The `user` and `group` Flockfile fields refuse permanently.

## This repository is generated

`bucket/shep.json` is pushed here by shep's release workflow on every release.
Its source of truth is `packaging/scoop/shep.json` in the main repository, so
open pull requests against
[shep-pm/shep](https://github.com/shep-pm/shep) instead of against this
repository. Anything committed here directly is overwritten by the next
release.

## License

MIT or Apache-2.0, at your option, matching shep itself.
