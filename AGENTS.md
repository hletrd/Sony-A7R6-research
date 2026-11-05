# Repository instructions

## Research scope

Investigate the firmware structure and modification options of the Sony A7R VI (ILCE-7RM6). Use the A7R V (ILCE-7RM5) for comparison. Distinguish camera models, firmware versions, regions, and input hashes. A method demonstrated on another camera is not a verified A7R VI result.

This repository contains public research records. Keep original firmware, extracted files, device dumps, and execution environments in a separate local workspace. The current work is static file analysis. Analysis commands must not write to or reboot a camera. Follow the scope of any additional work the user requests.

## Workflow

1. Read `README.md` and the relevant research records. Check existing conclusions and open questions.
2. Verify changing information, including tools, APIs, options, and compatibility, against official documentation and current source code.
3. Wait for input copies to finish, then record file sizes and SHA-256 hashes. If filenames conflict with internal model information, compare the internal metadata with official release information.
4. Record the tool repository, branch, commit, execution environment, command, exit code, and error.
5. Preserve inputs and write outputs separately. Validate the relevant result, then update the research record and README status.

## Evidence and conclusions

| Classification | Required evidence |
| --- | --- |
| Direct observation | A reproducible command or source inspection against an input identified by its hash |
| External report | A third-party result with an author, date, and URL |
| Inference | An interpretation supported by observations but not directly verified |
| Unverified | A question for which the necessary evidence or experiment is missing |

Label conclusions with their evidence and classification. When local results differ from external reports, compare inputs and environments first. Track decryption, extraction, repacking, signature validation, installation, and runtime behavior as separate stages. Success at one stage does not establish success at later stages.

When a key or tool fails, distinguish input corruption, container format, supported keys, and implementation errors. A failure log alone does not establish the cause. Do not claim comparison of a local SHA-256 with an official firmware hash unless that comparison was actually made.

## Repository layout

| Path | Purpose |
| --- | --- |
| `README.md` | Research scope, current status, and links to records |
| `docs/research/` | Dated experiments and compatibility investigations |
| `docs/sources.md` | External sources, their uses, and applicability |
| `data/` | Public hashes and structured measurements |

Research records should contain the relevant question, inputs, environment, method, observations, conclusion, limitations, next checks, and sources. Include only useful sections. Link to detailed records instead of duplicating results across documents. Do not create empty directories or placeholder plans without supporting material.

Keep firmware and extracted binaries out of this public repository. Keep device identifiers, credentials, personal files, dumps, and raw logs local. Publish only reviewed information and metadata needed to reproduce the result. Preserve provenance and license information for third-party code and material.

## Implementation and validation

Use Python 3.14 or later managed with `uv`. Check the registry for current stable versions and compatibility before adding dependencies. Record the versions actually used for reproducible experiments. Pin external tools to a commit and distinguish unmodified results from results produced with local patches.

When changing parsers, check lengths, offsets, byte order, and boundary conditions. Validate the behavior affected by code changes. For documentation, verify links, numbers, and evidence. Never report a check as passed if it was not run.

## Writing and Git

Write all project documentation and research records in clear, plain English. Use short descriptive headings. Preserve numbers, model names, addresses, and commands when editing prose.

Keep `AGENTS.md` as the source of repository instructions. Keep `CLAUDE.md` as a symlink whose relative target is `AGENTS.md`.

Make one commit per logical change and sign it with `git commit -S`. Use an imperative commit title in the form `<type>(<scope>): <gitmoji> <description>`, under 72 characters. Do not add AI attribution. Run `git pull --rebase` immediately before pushing. For an initial push, check whether the remote branch exists.
