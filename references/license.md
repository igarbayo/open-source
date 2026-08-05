# LICENSE

> **IMPORTANT: do not generate the license text by hand.** Long license texts
> (GPL-3.0, AGPL-3.0, Apache-2.0, etc.) are tens of KB. Reproducing them word by
> word in the model output is slow, error-prone and may be blocked by the
> provider's output filters, which makes the whole artifact fail.
> **Always download the text from its canonical source** so the file is
> byte-for-byte identical to the official one:
>
> ```bash
> mkdir -p LICENSES
> # Replace {{LICENSE_ID}} and the URL with the chosen license:
> #   MIT           -> https://raw.githubusercontent.com/spdx/license-list-data/main/text/MIT.txt
> #   Apache-2.0    -> https://www.apache.org/licenses/LICENSE-2.0.txt
> #   BSD-3-Clause  -> https://raw.githubusercontent.com/spdx/license-list-data/main/text/BSD-3-Clause.txt
> #   GPL-3.0       -> https://www.gnu.org/licenses/gpl-3.0.txt
> #   AGPL-3.0      -> https://www.gnu.org/licenses/agpl-3.0.txt
> curl -sSL {{URL}} -o LICENSE
> cp LICENSE LICENSES/{{LICENSE_ID}}.txt
> ```
>
> For MIT/BSD (which carry `[year]`/`[fullname]` slots) download the template and
> then edit only those fields in the downloaded file; the rest of the text is
> never typed by hand.
>
> **Careful with `curl -o`: it overwrites without warning.** If step 0 of SKILL.md
> found that a `LICENSE` (or `LICENSES/{{LICENSE_ID}}.txt`) already exists and the user
> did not ask to overwrite it, download to the agreed path (`LICENSE.new`, etc.) instead
> of to `LICENSE`.

The license file goes both at the root of the repository and in the LICENSES folder. Inside that folder it uses the .txt extension. The LICENSES/ folder must also contain any additional clause the software or the license type requires, such as BSD-3-Clause.txt.

Keep in mind:
- Add SPDX headers in source files where possible, or use `.license` sidecar files when not.
- Keep license texts in `LICENSES/` named by SPDX identifiers (e.g. `LICENSES/Apache-2.0.txt`).
- Ensure every license used has a corresponding text file and that no unused licenses are included.
- Use OSI-approved licenses and correct SPDX license expressions.

Add a `docs/COMPONENTS_LICENSE.md` document explaining in full why a particular license was chosen for the project, including any legal consideration or compatibility concern with other licenses. "Other licenses" here means the licenses of every library, dependency and asset used in the project, as well as any extra restriction or requirement the chosen license imposes.

## Summary table for choosing a license

**Before asking the user which license they want, print this table on screen as it is** to help them decide:

| License | Type | In one sentence |
|----------|------|--------------|
| **MIT** | Permissive | The simplest and most popular one: do whatever you want with the code, just keep the copyright notice. Maximum adoption, no patent clause. |
| **Apache-2.0** | Permissive | Like MIT but with an explicit patent grant and protection against lawsuits; recommended for projects with patent implications or corporate backing. |
| **BSD-3-Clause** | Permissive | Very close to MIT, adding a clause that forbids using the authors' names to promote derivatives without permission. |
| **GPL-3.0** | Copyleft | Any derivative work must be distributed under the same license (open source is mandatory). It protects the software's freedom, but reduces commercial adoption. |
| **AGPL-3.0** | Network copyleft | GPL-3.0 extended to network services: if you offer the software as a web service, you must publish the source code to its users. Ideal for SaaS that wants to avoid closed appropriation. |

After printing the table, ask the user which one they choose and remind them that all these open source products are delivered with *no warranties*.

The most common OSI-approved open source licenses are:
- Permissive: MIT, BSD, Apache 2.
- Copyleft: a product derived from a piece of software must carry the same license or one with GPL-compatible terms, such as GPL v2 or GPL v3. The GPL is the FSF's most purist license, which also makes technology under it less likely to be adopted.
- Network copyleft: AGPL. A copyleft license that applies to software running on servers and accessed over the network. If users can reach a service over the web, they must also be able to reach the source code. It is essentially a GPL project plus a web API. For something deployed on the network, AGPL 3 is the most common choice to prevent other companies from appropriating the software.

It is worth stressing that all open source products come with no warranties.

The result is a project license plus REUSE-compliant licensing metadata.
