# bun-monorepo-server-issue

### Install deps for the workspace without a bug

```sh
cd workspace-success
bun install
```

### Run Successfull Example

```sh
bun --filter "*" dev
```

#### You'll see next result ✅

```sh
➜ bun --filter "*" dev
not-a-server dev $ bun run --hot index.ts
│ Hello from Not-a-Server!
└─ Running...
client dev $ bun run --hot index.ts
│ Hello from Client!
└─ Running...
```

### Install deps for the workspace with a bug

```sh
cd workspace-bug
bun install
```

### Run an Example with a bug

```sh
bun --filter "*" dev
```

#### You'll see result with an issue ❌

```sh
➜ bun --filter "*" dev
server dev $ bun run --hot index.ts
│ Hello via Bun!
└─ Running...
client dev $ bun run --hot index.ts
└─ Waiting for 1 other script(s)
```

### Conclusion

So, looks like a folder called `server` breaks something in Bun.

### Important Notice

If I remove `"dependencies"` section in `client` I still can use `server` as a dependency.
Bun doesn't hang in this case, but it looks strange to import something from workspace and doesn't rely on it in `package.json`.

```sh
❯ bun --filter "*" dev
server dev $ bun run --hot index.ts
│ Hello via Bun!
└─ Running...
client dev $ bun run --hot index.ts
│ Hello via Bun!
│ Hello from Client!
│ Hello from Server!
└─ Running...
```
