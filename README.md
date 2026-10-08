### Sujal Sharma

Software engineer in Hyderabad. I build the data infrastructure behind AI products at
Orbital — a ClickHouse → Postgres sync running on BullMQ workers under Kubernetes.

**One idea runs through everything below: each project refuses to report a conclusion its
measurement doesn't support.** That sounds like a slogan until you look at what it costs —
`restore-proof` writes `UNVERIFIED` even when the backup command exits 0, and `evalgate`
declines to name a winner on a difference it can't resolve.

| | |
|---|---|
| **[restore-proof](https://github.com/jai-bhardwaj/restore-proof)** | A backup you haven't restored isn't a backup, it's a claim. Postgres replication + WAL archiving, and a verifier that restores every backup into a throwaway instance and queries it. Three states: `VERIFIED`, `UNVERIFIED`, `FAILED`. |
| **[driftscan](https://github.com/jai-bhardwaj/driftscan)** | A sync job that reports success has told you it didn't crash — not that the two stores agree. Bucketed count+XOR comparison; finding 6 bad rows in 50,000 reads 1,195 of them. |
| **[evalgate](https://github.com/jai-bhardwaj/evalgate)** | An eval harness for LLM and agent systems that separates *"no difference"* from *"not measured"*. Detecting a +3-point improvement on a 73% baseline needs ~3,300 cases per variant; most published comparisons use 50–100. |
| **[mach-zero](https://github.com/jai-bhardwaj/mach-zero)** | C++20 algorithmic trading system — order book, pre-trade risk gate, strategy engine, Aeron IPC, SBE wire format, QuestDB. ~11k lines of hand-written C++, 173 tests. |
| **[spsc-queue](https://github.com/jai-bhardwaj/spsc-queue)** | Wait-free single-producer/single-consumer ring buffer. Release/acquire ordering verified by a 500k-item soak under ThreadSanitizer. |
| **[k8secret](https://github.com/jai-bhardwaj/k8secret)** | Native macOS client for the Kubernetes API. Signed DMG, sha256-gated updater, fail-closed TLS. MIT. |

**I publish the corrections too.** mach-zero's README carries a latency table I withdrew:
the harness timed a single operation between two `steady_clock` reads, and on Apple silicon
that clock's 41.7 ns tick meant every figure I'd published was one or two ticks of the
instrument rather than a measurement of the code. `restore-proof` caught its own failure
mode the same way — a permissions mistake made the restored container run `initdb`, and it
came up as a pristine empty cluster that passed every health check and contained nothing.

**I use AI seriously in the loop** — design, debugging, review. The architecture decisions
and the bugs are mine.

`C++20` · `Python` · `TypeScript / Next.js` · `PostgreSQL` · `ClickHouse` · `Kubernetes` · `Linux`

[sujalsharma.com](https://sujalsharma.com) · [LinkedIn](https://www.linkedin.com/in/sharmasujal/)
