# MosHub VPN parser runner

GitHub Actions runs the parser and publishes `output/sub.txt` to the `main` branch of the MosHub repository as `sub.txt`.

## GitHub repository secrets required

Add these under **Settings → Secrets and variables → Actions → New repository secret**:

- `MOSHUB_REPO` — HTTPS clone URL, e.g. `https://hub.mos.ru/cheesyx/test.git`
- `MOSHUB_USERNAME` — username associated with the MosHub project access token (use the exact token username shown by MosHub)
- `MOSHUB_TOKEN` — MosHub project access token; never commit or share it

The MosHub token needs repository read and write access. The target repository must have a `main` branch.

## Run

Open **Actions → Update MosHub subscription → Run workflow**. This initial version runs manually only; it does not schedule periodic runs and does not trigger from MosHub webhooks yet.

The workflow will not publish if the parser fails to produce a non-empty `output/sub.txt` containing at least one proxy URL. Existing MosHub subscription remains untouched on validation failure.

## Important

- The parser's source list and pinned configs are currently still embedded in `merge_subscriptions.py` from the supplied project.
- This runner publishes only `sub.txt` to MosHub; it does not push parser code to MosHub.
- The MosHub token is stored only as a GitHub Actions secret.
