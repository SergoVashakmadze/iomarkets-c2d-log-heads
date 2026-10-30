# IoMarkets compute-to-data: verified log heads

Every 6 hours, a monitor checks the IoMarkets compute-to-data coordinator's public receipt log
(`https://coordinator.c2d.iomarkets.ai/v1/log`): it must be signed by the pinned log key and must only
ever grow. Each signed tree head the monitor verifies is appended to `heads.jsonl` here, one JSON
object per line: `{"log_pub": "<hex>", "sth": {"head": {...}, "signature": "<hex>"}}`.

**Why it is public.** A log operator could show one customer a different (forked) history from
everyone else, with every head signed and valid on its own. It cannot sign a head that extends both
that fork and a head published here. To check a receipt, ask the log for a consistency proof from
your receipt's head, and one from the newest head here, to the same current head; both must verify.

**Pinned log key:** `5a883d028d32e07c2089130416a0d101a448f2808650a40cf0ee3e08454a9fe0`
(compare with `https://coordinator.c2d.iomarkets.ai/v1/log/keys`).

This file only grows. Commits are made by the monitor alone.
