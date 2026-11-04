# Changelog

## [Unreleased]

Compatibility fixes for omp (oh-my-pi) and Windows. Behaviour on pi is unchanged.

- `terminal` resolves its shell instead of hardcoding `/bin/bash`: `HARNESSMM_SHELL`, then the POSIX path, then a
  Git for Windows bash. No resolution returns a 127 receipt naming `HARNESSMM_SHELL` instead of an ENOENT spawn.
- `timeout_sec` and abort kill the whole process tree on win32 (`taskkill /t /f`); a timed-out command used to keep
  running until it finished on its own.
- `before_agent_start` keeps pi's sections path and appends the authoring instruction as one more section when a host
  passes the assembled prompt as an array (omp), instead of throwing on a missing `systemPromptOptions`.
- Candidates are validated against the extension's terminal contract when the host's tool `parameters` is an opaque
  builder rather than JSON Schema (omp), so a bank is no longer rejected as `arguments_do_not_match_tool_schema`.
- Admitted actions go through `runTerminal` when the host exposes no nested `ctx.executeTool` (omp).
- A rejected bank names the rule it violated (`unknown_predecessor`, `arguments_do_not_match_tool_schema`, ...).
- The cwd test compares the directory leaf name, so shells that report `/tmp` for the Windows temp directory pass.

## [0.1.0] - 2026-11-02

Initial port of HarnessMM (arXiv 2610.32813) to pi.

- `terminal` tool returning native `{return_code, stdout, stderr}` receipts with separated streams.
- `<CHISEL_PLAN>` Executable Decision Graph contract, byte-identical authoring instruction for policy versions 1-11.
- Guarded decision reuse: `localGuard` and `receiptGuard`, deterministic admission with the 1024-token net-saving
  threshold, priors-based admission for versions 8 and 10 that fails closed without frozen TRAIN medians.
- Certified callback substitution: `certified-native-substitution/v1` certificates binding arguments, receipt and
  the bypassed reasoning callback.
- Bank removal from the slow context, preserving reasoning and native actions.
- `/harnessmm` ledger command.
