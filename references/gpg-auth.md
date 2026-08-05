# Commit authentication: GPG + DCO

These are **two distinct, independent mechanisms**; this project adopts both:

## GPG signing (authenticates the author)

Every commit must be signed with GPG (`git commit -S`, or automatically through configuration):

```
git config --global user.signingkey {{GPG_KEY_ID}}
git config --global commit.gpgsign true
```

Configure GitHub to accept only signed commits, through protection rules in the repository's Branches section, on the main branch (main or master) and on any development branch (develop, staging, ...). This guarantees that the identity of each change's author can be verified.

Also add a `docs/GPG_KEY.md` document explaining how to generate a GPG key, how to configure it in Git and GitHub, and how to verify the authenticity of signed commits (`git log --show-signature`).

## DCO (certifies the right to contribute)

The DCO (Developer Certificate of Origin) is not a cryptographic signature: it is a legal statement that the contributor has the right to submit their contribution under the project's license.

- Add a `DCO` file at the root of the repository with the full text of the Developer Certificate of Origin 1.1 (https://developercertificate.org/).
- Every commit must carry the `Signed-off-by: Name <email>` trailer, added with `git commit -s` (lowercase; different from GPG's `-S` — they can be combined: `git commit -s -S`).
- Optionally, it can be enforced in CI with the "DCO" GitHub App or an equivalent action that rejects PRs containing commits without a sign-off.
- CONTRIBUTING.md must explain the sign-off as a requirement of the PR process.
