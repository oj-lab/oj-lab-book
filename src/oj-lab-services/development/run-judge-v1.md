# Run Judge V1

⚠️ This function is still under develop now,
not promising the usage will be changed in the future.

## Usage with Judger

You should run both `oj-lab-services` and `judger` in the same network.

By default `judger` will listen on `:8000`,
if you change it,
you should also change `judger.host` in `oj-lab-services`'s config
(an override config is more recommended, see `override.example.toml`).

### Run `judger`

```bash
cargo run --bin judge-server
```

### Run `oj-lab-services`

```bash
make run
```

### Test APIs

Both `judger` and `oj-lab-services` provide a `postman` API collection in project root.

Import them into Postman and test.
