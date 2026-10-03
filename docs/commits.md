# Commit messages

Documents organizational policy for writing commit messages.

## Goals

TODO

## Format

```
[scope(s)] Description (#PR-number, conditional)

Body, optional
```

Example: `[auth] Fix broken login when the session cookie expires`

### Scope(s):

A conceptual domain of the code, not necessariy a directory name. Should usually just be one, though a comma separated list is allowed. e.g. auth, checkout, config, tests, global, etc.

### Description:

A one-line summary of the changes in the commit, starting with an imperative verb. The message should be geared toward developers trying to identify where exactly a certain change was introduced.

Special note on **the leading verb**: A capitalized imperative verb that kicks off the description. Should mostly be from below list, though other verbs are allowed if it flows more naturally.

- Secure
- Add
- Remove
- Deprecate
- Change
- Fix
- Refactor
- Document
- Test
- Bump
- Revert
- Release

Whenever multiple verbs would fit, the description should prioritize the most important change. The framing should generally favor options further up the above list. When applicable,
- Security is more specific than fix.
- Fix is more specific than change (it implies the previous state was not intentional).
- Add/Remove/Deprecate are more specific than change.
- Most features will include some amount of documentation and tests; in these cases just describe the feature.
- Refactor and bump imply no user-visible changes. If there are any, they MUST be included in the body at least, though if the driving force was the behavior change itself, rather than general updates or maintenance, that should be the subject line.

### PR Number

Always on squash commits, never locally. Handled automatically by Github.

### Body

 The body may be used, but only if more space is necessary to adequately describe the change. "Adequate", in addition to describing the over-arching technical changes, means that enough information is recorded to ensure a _user-centric_, [Keep-a-Changelog][1] compliant changelog can be generated without looking at the diff. The type of user (i.e. developer using a library or api, vs web application user) heavily influences what kind of information this involves.

## Enforcement

### Locally

Since we use Zed as our IDE, we will utilize its ai commit message generation feature to write messages. It will be configured to have access to this doc at the point of generation.

### CI

We will enforce squash merging on PR via github. A github workflow will run on every push to the PR'd branch, synthesizing the included commit messages into one that summarizes them all and updating the PR with it. That summary should follow all the commit rules as if it were it's own commit (again, the PR number is handled by Github).

If you ever want to manually override the auto-generated squash commit message, it must be done right before merging; otherwise a future push could overwrite your changes.

[1]: https://keepachangelog.com/en/2.0.0/
