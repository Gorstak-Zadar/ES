<!-- description: ES.ps1: copies self to C:\Windows\Setup\Scripts\Bin, SYSTEM logon task, qwinsta/rwinsta loop in Start-Job—job lacks function scope. -->

# ES

**`ES.ps1`** (author comment: **session terminator** theme):

1. **`Register-SystemLogonScript`** — copies the script to **`C:\Windows\Setup\Scripts\Bin\ES.ps1`** and registers **`RunESAtLogon`** (PowerShell at **user logon**, **SYSTEM**, highest).

2. **`Terminate-NonConsoleSessions`** — parses **`qwinsta`** output and calls **`rwinsta`** on session IDs whose name is **not** **`console`** (regex parsing is fragile).

3. **`Start-Job`** runs **`Terminate-NonConsoleSessions`** every **5** seconds forever.

**Bug:** **`Terminate-NonConsoleSessions`** is **not** defined inside the **job scriptblock**, so the job **will not see** the function unless you merge definitions into the block or use a single script without `Start-Job`. As checked in, the background job is **likely to error** every loop.

**Logging:** **`%TEMP%\SessionTerminator.log`**

**Warning:** **`rwinsta`** can **disconnect** or **terminate** other users’ sessions and **RDP**—dangerous on shared machines.

---

## Usage

```powershell
# Elevated Administrator
.\ES.ps1
```

Refactor the job block if you need reliable execution.

---

## Disclaimer

**NO WARRANTY.** THERE IS NO WARRANTY FOR THE PROGRAM, TO THE EXTENT PERMITTED BY APPLICABLE LAW. EXCEPT WHEN OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR OTHER PARTIES PROVIDE THE PROGRAM "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU. SHOULD THE PROGRAM PROVE DEFECTIVE, YOU ASSUME THE COST OF ALL NECESSARY SERVICING, REPAIR OR CORRECTION.

**Limitation of Liability.** IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING WILL ANY COPYRIGHT HOLDER, OR ANY OTHER PARTY WHO MODIFIES AND/OR CONVEYS THE PROGRAM AS PERMITTED ABOVE, BE LIABLE TO YOU FOR DAMAGES, INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING OUT OF THE USE OR INABILITY TO USE THE PROGRAM (INCLUDING BUT NOT LIMITED TO LOSS OF DATA OR DATA BEING RENDERED INACCURATE OR LOSSES SUSTAINED BY YOU OR THIRD PARTIES OR A FAILURE OF THE PROGRAM TO OPERATE WITH ANY OTHER PROGRAMS), EVEN IF SUCH HOLDER OR OTHER PARTY HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.

---

## Disclaimer (read this; it matters)

This software and documentation are provided **“as is”**, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. **Use at your own risk.**

- Nothing here is professional security, legal, medical, or financial advice.
- The authors and contributors are **not liable** for any direct, indirect, incidental, special, exemplary, or consequential damages (including loss of data, profits, goodwill, or business interruption) arising from use or inability to use this material, **even if advised of the possibility** of such damages.
- You are solely responsible for compliance with laws and policies that apply to you. Do not use these tools to violate privacy, computer misuse laws, or terms of service.
- “Detection,” “monitoring,” and “hardening” features can be wrong (false positives), miss real threats (false negatives), and change system behavior. **Test in a safe environment** before relying on anything important.

If you do not agree, **do not use** this repository.
