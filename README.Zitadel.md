# Internal Developer Onboarding

This quick reference summarizes how we expect teammates to spin up ZITADEL locally and work on the login application.

## 1. Enable WSL (Ubuntu)
Follow the short video walkthrough: https://youtu.be/bRW5r7TK6KM?si=SqOUEZMTVBTkLenY. Once Ubuntu is installed and initialized, open the Ubuntu terminal for every command below.

## 2. Clone the Repository
```bash
cd /home/<your user>
git clone https://t2development.visualstudio.com/Falcon/_git/falcon-core-identity-svc
cd falcon-core-identity-svc
```
> All remaining commands assume you stay inside `/home/<your user>/falcon-core-identity-svc`.

## 3. Install Node.js inside WSL
Install the Node.js version recommended by the upstream README/CONTRIBUTING guide (we usually track the current LTS release). Confirm availability with `node -v` and `pnpm -v`.

## 4. Follow the Official Quick Start
Work through https://github.com/zitadel/zitadel/blob/main/CONTRIBUTING.md#quick-start to install Go, PNPM dependencies, and initialize the dev database. Whenever that guide references scripts, run them from the Ubuntu terminal.

## 5. Focus on the Login App
Continue with the login-specific instructions in https://github.com/zitadel/zitadel/blob/main/CONTRIBUTING.md#contribute-to-login. This section covers building, running, and testing the Next.js login experience.

### Important Command Override
When the guide tells you to run `pnpm nx run @zitadel/api:prod`, use the following instead so the Go toolchain path is available and we skip the Nx cache:
```bash
cd /home/<your user>/falcon-core-identity-svc
PATH="/usr/local/go/bin:$PATH" pnpm nx run @zitadel/api:prod --skip-nx-cache
```
Keep the `PATH` prefix for every Go-based command if `$GOROOT/bin` is not already on your environment.

## 6. Troubleshooting Notes
- Always execute commands from the Ubuntu shell (not Windows PowerShell) so path casing and binaries resolve correctly.
- If Go binaries are not found, re-run `export PATH="/usr/local/go/bin:$PATH"` in your terminal session.
- For reproducibility, do **not** mix Windows Node.js installs with the WSL workspace; keep dependencies inside Ubuntu.

Once you reach a stable local run of `@zitadel/api:prod` and `@zitadel/login:dev`, you are ready to contribute.
