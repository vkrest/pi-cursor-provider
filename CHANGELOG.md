# Changelog

## 0.7.0

### Models

* Refresh the bundled fallback catalog from Cursor discovery with Fable 5.1, Claude Opus 5 and Sonnet 5, Cursor Grok 4.6, GPT 5.6 variants, Composer 2.5, newer Gemini Flash variants, GLM 5.2, and Kimi K3.
* Preserve Cursor's `NO ZDR` labels on Fable models. Catalog visibility is not a privacy guarantee or proof of access for every account.
* Resolve reasoning tiers to exact advertised model IDs, including both positions of the thinking suffix, fast variants, Gemini minimal effort, and GPT extra high effort.
* Preserve raw Grok IDs without adding a second reasoning suffix. Cursor Auto continues to ignore effort settings.
* Separate extra high from maximum effort and hide thinking off when the catalog does not offer it.
* Update recent model price estimates from Cursor's public cards and use its 272 k default context for GPT 5.6. Billing totals remain approximate.

### Security

* Authenticate the loopback proxy with an ephemeral random bearer token rather than a fixed placeholder.
* Reject browser Origin headers, unexpected Host headers, malformed chat requests, unsupported media types, and oversized request bodies before resolving upstream credentials.
* Create debug logs with private permissions, reject symlink targets, and avoid printing payloads when logging fails. Debug logs remain opt in and may contain sensitive conversation content.
* Restrict snapshot refresh output to normalized model metadata so arbitrary cache fields cannot enter the published catalog.
* Refresh the development dependency lockfile and replace obsolete Pi peers.
* Stop the proxy and clear its credential callback on shutdown, including running bridge processes and late callbacks.

### Reliability

* Display Cursor's own protobuf error title, detail, and additional information through Pi's error handling path. Fall back to the raw upstream message without a local error message catalog.
* Preserve explicit Cursor retryability and avoid relabeling native rate limits as context overflow.
* Send real HTTP/2 PING frames instead of relying on unsupported Node connection options.
* Do not retry a crashed bridge after output has already reached the client.
* Handle child process launch and stdin failures without uncaught error events.

### Compatibility and packaging

* Require Node.js 22.19 or newer and Pi 0.84 or newer using the `@earendil-works` package namespace.
* Run typechecking and offline tests before packing or publishing.
* Include the model routing helper and documented maintenance scripts in the package.
* Add an explicit opt in synthetic live smoke test for streaming and tool result replay.
* Correct documentation about preserving server checkpoints during local compaction and about estimated model limits and costs.

Fable requests were blocked by Cursor's administrative model access controls. The adapter now surfaces the supplied explanation, "Model Blocked: Please ask your admin to enable access to Claude Fable 5." This text comes from Cursor, not a model specific rewrite. Privacy settings were not weakened.

Astra was absent from the account catalog used for this snapshot. It is not advertised as tested or enabled by this release without a verified Cursor ID. Live discovery will register it when Cursor exposes it to the account.
