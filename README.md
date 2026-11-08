# DevAgent AI Designer — Downloads & Installation

**AI-assisted engineering for Ignition Designer — evaluation releases**

> **Release status:** No public installation package is available until a tested, signed `.modl` is published under [Releases](https://github.com/tomha85/devagent-releases/releases). Do not install unsigned developer test packages in production. The six-month trial is a planned feature and is **not guaranteed** until a release explicitly confirms it has passed testing.

## 1. Requirements

- Ignition Gateway and Designer already installed; use an **isolated TEST Gateway**, not a production plant.
- Administrator access to the Gateway to install third-party modules.
- A supported Ignition version **explicitly listed in the chosen DevAgent release notes**. Do not assume an 8.1 build is compatible with 8.3 or vice versa.
- Internet access to download the release; AI use may require separate access to your chosen model provider (BYOM).
- A Gateway/project backup before installing, upgrading, or uninstalling any module.

**Operating systems:** Installing an Ignition `.modl` is done through the Gateway web interface on Windows, macOS, or Linux. iOS cannot host Ignition Gateway/Designer; supported Perspective apps may be viewed on mobile separately.

## 2. Download DevAgent

1. Visit **[DevAgent Releases](https://github.com/tomha85/devagent-releases/releases)**.
2. Open the newest release marked suitable for your **exact Ignition version**.
3. Under **Assets**, download the signed `.modl` file (not `Source code.zip` and not an unsigned test ZIP).
4. Read the release notes, requirements, beta limitations and any required dependencies.
5. If a `SHA256SUMS` file is provided, verify the downloaded file:

   **Windows PowerShell**
   ```powershell
   Get-FileHash -Algorithm SHA256 .\DevAgent-<version>.modl
   ```
   
   **Linux**
   ```bash
   sha256sum DevAgent-<version>.modl
   ```

   **macOS**
   ```bash
   shasum -a 256 DevAgent-<version>.modl
   ```
   
   Compare the output with the checksum published for **that exact file**. A checksum is not a substitute for checking the publisher's signing certificate.

**If the Releases page is empty, there is nothing ready to install yet.**

## 3. Back up your Gateway first

1. Open the Gateway web page, commonly `http://localhost:8088` **when browsing on the Gateway host**. For a remote Gateway, use its actual hostname, protocol and port.
2. Log in as a Gateway administrator.
3. Create and securely store a **full Gateway backup** using the backup interface appropriate to your Ignition version.
4. If upgrading an existing DevAgent module, record its current version and keep the last working, signed release available.
5. Use a TEST Gateway and maintenance window; installing/upgrading modules can require connected Designers/Vision Clients to restart.

## 4A. Install on Ignition 8.3

1. Open the **Ignition Gateway web page** and log in.
2. Navigate to **Platform → System → Modules**.
3. Click **Install or Upgrade Module (+)**.
4. Select the downloaded signed `.modl` file using **Choose File**.
5. Click **Install** and follow the displayed prompts.
6. Check the module's publisher certificate and trust warnings. **Do not disable signature checks or enable unsigned-module developer mode** just to install the public Beta.
7. If the Gateway asks for a restart, schedule and complete it. Restart/reopen Designer sessions as required.
8. Return to **Modules** and confirm DevAgent is listed, enabled and in an appropriate active state. Capture any error message if installation fails.

Official Ignition 8.3 instructions: https://www.docs.inductiveautomation.com/docs/8.3/getting-started/installing-and-upgrading/installing-or-upgrading-a-module

## 4B. Install on Ignition 8.1

1. Open the **Ignition Gateway web page** and log in.
2. Navigate to **Config → Modules**.
3. Scroll down and click **Install or Upgrade a Module**.
4. Click **Choose File**, select the downloaded signed `.modl`, then click **Install**.
5. Review publisher trust prompts and the installed module's status; do not bypass module-signature safeguards for a public Beta.
6. Restart/reopen connected Designers as required.

Official Ignition 8.1 instructions: https://www.docs.inductiveautomation.com/docs/8.1/getting-started/installing-and-upgrading/installing-or-upgrading-a-module

## 5. Open Ignition Designer

1. Open the Gateway home page and launch **Designer** using the Designer Launcher for your Gateway.
2. Select a **TEST project**, or create a disposable test project.
3. Confirm the DevAgent module loaded. Its actual menu/panel location and available actions depend on the release; consult the release notes if you do not see it.
4. If the released module supports BYOM settings, configure your AI provider/model in DevAgent, test the connection, and do not paste private keys into project scripts or public issue reports.
5. Begin with a **read-only** task, such as inspecting a single Perspective View or a Tag/UDT definition.
6. Only after checking proposed changes should you try creation/modification in the TEST project, using backups and explicit approvals.

### Suggested safe smoke test

- Inspect a named Perspective View and request an explanation of its bindings.
- Inspect an existing Tag or UDT definition.
- Request a **proposed** new TEST View and examine any generated bindings before approval.
- Verify results in Designer and, if applicable, a TEST Gateway/browser runtime.

Do **not** interpret AI-generated text or simulated FAT as verified physical PLC mappings, production approval, or proof of operational safety.

## 6. Free trial information

A **six-month evaluation trial** is planned. The actual start/expiration mechanism must be implemented and tested in the module and disclosed in the individual release notes before it can be offered. **Downloading a build alone does not enable a trial license.** No payment or license key is required merely to access this public download repository.

If a future release implements trial expiration, it should restrict DevAgent engineering actions rather than disrupt already-deployed Ignition HMI, PLC, alarms, or other runtime operations. Do not rely on this behavior until it has been validated for the release.

## 7. Troubleshooting

| Issue | What to check |
| --- | --- |
| No downloadable file | There is no published release yet; check the Releases page later. |
| Downloaded a ZIP, not `.modl` | Select the module under **Assets**. Do not upload GitHub's auto-generated source ZIP to Gateway. |
| `Module is unsigned` / trust warning | Obtain an appropriately signed official build. Do not bypass security controls on a customer Gateway. |
| Module cannot install | Verify Ignition version, dependency list, package integrity, signing, and Gateway logs. |
| Module pending restart | Follow the Gateway's restart notice, then reopen Designer. |
| DevAgent not visible in Designer | Confirm the Gateway module is active, match Designer/Gateway versions, restart Designer, and check release-specific menu instructions/logs. |
| AI connection fails | Check provider URL, model, credential validity, TLS/network/proxy and permitted data-sharing rules. |
| Existing module behaves unexpectedly | Stop testing, preserve logs, and restore the previous compatible module/backup using an approved maintenance process. |

**When reporting a bug:** include the Ignition version, OS, DevAgent release version, steps to reproduce, error message and a **sanitized** log excerpt. Remove API keys, credentials, PLC addresses, tag lists, database secrets and proprietary plant data.

## 8. Upgrade / uninstall

**Upgrade:** Back up the Gateway, download the compatible newer signed `.modl`, and repeat the version-specific **Install or Upgrade Module** steps. Verify the module state and your TEST project afterward.

**Uninstall:** Back up first, then use the Gateway **Modules** page to uninstall DevAgent. Follow all required restart prompts. Never uninstall a module used by a live runtime without assessing dependencies and scheduling maintenance.

Official guide: https://www.docs.inductiveautomation.com/docs/8.3/getting-started/installing-and-upgrading/installing-or-upgrading-a-module

## 9. Feedback and safety

This repository distributes builds; source code is maintained privately. Beta evaluation should be carried out only on isolated or otherwise approved test systems. Do not connect synthetic simulation or AI-suggested write commands to production PLCs.

To report feedback, use the repository's **Issues** tab if enabled, or the contact channel stated in your release notes. Never attach unredacted Gateway backups, private project exports or customer credentials.

---

**Maintainers:** Before announcing a new Beta, publish a signed `.modl` and checksums; specify tested Ignition versions, test evidence, feature limitations, trial conditions, and exact Designer entry point in release notes.
