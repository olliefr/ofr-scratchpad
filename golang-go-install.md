# Compile and install Go packages

Install tagged versions, not the latest snapshot from `main`. Example:

```bash
go install github.com/google/oauth2l@v1.2.2
```

To see what's been installed,

```bash
ls $(go env GOPATH)/bin
```

Make sure this directory is in the system's `$PATH`.
