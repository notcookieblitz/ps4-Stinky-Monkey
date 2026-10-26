# Teacher notes (Allan Bayntun) – maintaining this template

## Publish it as a template repository
1. Create a **public** repo under the account/org you choose and push this folder.
2. Repo **Settings → General →** tick **Template repository**.
3. Share the repo link on Canvas. Students then click **Use this template → Open in a codespace** (no fork or repo needed; their codespace is billed to *their* free quota).
   - Docs: <https://docs.github.com/en/codespaces/developing-in-a-codespace/creating-a-codespace-from-a-template>
   - Template repos: <https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository>
4. Optional: add an "Open in GitHub Codespaces" badge to the README:
   `[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/OWNER/REPO?quickstart=1)`

Who pays: codespaces are billed to the person who creates them, unless an **organization** owns the repo *and* has opted in to pay for members. Organization plans get **no** free Codespaces quota, so an org-owned repo whose org pays means real money. Leave org billing off and students use their personal free quota.
Source: <https://docs.github.com/en/billing/concepts/product-billing/github-codespaces>

## Costs & quotas (verified 2026-10-20)
| Plan | Compute / month | Storage / month |
|---|---|---|
| GitHub Free (personal) | 120 core-hours (= **60 h on a 2-core**) | 15 GB-month |
| GitHub Pro (incl. Student Developer Pack) | 180 core-hours (= 90 h on 2-core) | 20 GB-month |

- Overage price: 2-core $0.18/h, storage $0.07/GB-month. **Without a payment method on file, usage is simply blocked** at the limit (no charge).
- Because this uses a custom image (not the default universal image), the image counts toward storage. Measured on the box: base image 1.66 GB + installed packages ≈ 0.6 GB, so **≈ 2.5–3 GB per codespace** with extensions. That's about 3 of the 15 GB-month even if it's kept all month.
- Defaults: idle timeout **30 min** (closing the tab doesn't stop it); stopped codespaces are **auto-deleted after 30 days**; max active lifetime 12 h.
  - <https://docs.github.com/en/codespaces/setting-your-user-preferences/setting-your-timeout-period-for-github-codespaces>
  - <https://docs.github.com/en/codespaces/setting-your-user-preferences/configuring-automatic-deletion-of-your-codespaces>
  - <https://docs.github.com/en/codespaces/troubleshooting/troubleshooting-included-usage>
- GitHub accounts require age 13+ (GitHub Terms of Service).

## Prebuilds (probably not needed)
Creation without a prebuild was measured at **~20 s for the pip install** on top of the container start (see test log below), well under GitHub's "> 2 minutes → consider prebuilds" guideline.
If you enable them anyway (Settings → Codespaces → Set up prebuild):
- Each prebuild **uses storage billed to the repo owner** (your quota, or paid if org-owned), plus GitHub Actions minutes every time it rebuilds (by default on every push). Set the trigger to "on configuration change" to limit that.
- The install is in `onCreateCommand` (not `postCreateCommand`) on purpose: prebuilds run `onCreateCommand` but **skip** `postCreateCommand`.
- It's not verified whether prebuilds are used when students choose **Use this template → Open in a codespace** (as opposed to **Code → Codespaces** on your repo).
- Docs: <https://docs.github.com/en/codespaces/prebuilding-your-codespaces/about-github-codespaces-prebuilds>

## Updating the pins (once per semester, not mid-unit)
1. Open a codespace on the template from **Code → Codespaces** (so you can commit back).
2. Edit `requirements.txt` (bump `qiskit`, `qiskit-aer`, etc. together). Check `qiskit-aer` supports the new `qiskit` major version.
3. In the terminal: `pip install -r requirements.txt`, then **Run All** on `notebooks/00_check_setup.ipynb` and `PS4_template.ipynb`.
4. Headless check: `pip install nbconvert && jupyter nbconvert --to notebook --execute notebooks/*.ipynb --output-dir /tmp/out`
5. Commit and push. Existing student codespaces keep their old versions; students get the new ones only when they create a new codespace (or run `pip install -r requirements.txt`).

**Don't change the image to the Debian *trixie* variant** (`python:3-3.12` currently resolves to trixie). On trixie, `import qiskit_aer` fails with
`libgomp-….so.1.0.0: cannot allocate memory in static TLS block` (tested with qiskit-aer 0.18.0 and 0.17.2). The pinned `3-3.12-bookworm` works. If you ever must move off bookworm, the known workaround is
`"containerEnv": {"GLIBC_TUNABLES": "glibc.rtld.optional_static_tls=4096"}` in `devcontainer.json` (it worked in testing).

## Real IBM hardware (later)
Uncomment `qiskit-ibm-runtime` in `requirements.txt`. Students need IBM Quantum credentials. **Never commit API tokens** to the repo. Have students store them as a personal Codespaces secret (GitHub → Settings → Codespaces → Secrets), which shows up as an environment variable.

## Copilot
Not installed by this config (AI is allowed in class, but not pre-installed). Students with Copilot access can still add it themselves.
