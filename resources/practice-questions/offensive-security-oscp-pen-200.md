---
last-updated: 2026-08-09
difficulty: advanced
---

# OSCP (PEN-200) - Practice Questions

15 questions on the concepts behind the OSCP: enumeration, exploitation, privilege escalation, pivoting, and Active Directory attacks. The exam itself is a 24-hour hands-on penetration test against authorized lab machines, so these questions test method and judgment rather than a fact bank.

These questions assume an authorized engagement or the PEN-200 lab. Every technique here is for systems you have explicit written permission to test.

> **Cert page:** [exams/offensive-security/oscp-pen-200/](../../exams/offensive-security/oscp-pen-200/)

---

### Question 1
**Scenario:** You have just gained access to a target network range for an authorized test. What comes first?

A. Run a single automated vulnerability scanner across the range and treat its findings as the full picture of what is exposed
B. Attempt privilege escalation on the first reachable host, since gaining root early gives the widest view of the network from the inside
C. Thorough enumeration: discover live hosts, then per host enumerate open ports, services, and versions
D. Launch the exploits you already know against every host in range, and see which of them return a shell to your listener

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** The OSCP mantra is try harder, and its practical form is enumerate more. The majority of the work is discovery, because a missed service is a missed path. Firing exploits blindly is noisy, unreliable, and skips the information that tells you which exploit to pick.
</details>

---

### Question 2
**Scenario:** An `nmap` scan shows port 80 and 443 open. What is the productive next step?

A. Assume it is patched, because a service on a standard web port that is reachable from the internet will have been kept up to date by the owner and then reviewed
B. Move on, since web applications are rarely exploitable compared with the services that run on non-standard ports or the older network daemons on the host
C. Brute force SSH on port 22 with a large password list
D. Enumerate the web application: directory and file discovery, technology fingerprinting, and manual review of the application's functionality

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Web applications are one of the richest initial-access surfaces in the labs and the exam. Content discovery finds the admin panels, upload forms, and forgotten endpoints that a default page hides, which is where the actual foothold usually lives.
</details>

---

### Question 3
**Scenario:** A web form appears to build a SQL query from user input.

A. Test for SQL injection systematically, starting with error-based and boolean detection before attempting extraction
B. Ignore it, because a form that only builds a query from input is a normal part of the application and will not be exploitable in practice
C. Only run an automated scanner such as `sqlmap` with default options
D. Assume it is safe because the page uses HTTPS

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Manual confirmation tells you the injection type, which decides the extraction technique. On the exam, understanding the injection lets you adapt when an automated tool stalls, which it frequently does against non-trivial filters.
</details>

---

### Question 4
**Scenario:** You have a low-privilege shell on a Linux host. What is the first escalation step?

A. Reboot the machine so that any pending kernel or service changes apply, then reconnect and check whether the shell now has more rights
B. Enumerate systematically: kernel and OS version, SUID binaries, sudo rights, cron jobs, writable files, and running services
C. Delete the logs first so that nothing you do afterwards can be traced
D. Guess the root password with a short list of common passwords against `su`

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** Privilege escalation is enumeration again. A single `sudo -l` misconfiguration or an unusual SUID binary is often the whole path, and enumeration scripts surface candidates, but you still have to understand each one to exploit it correctly.
</details>

---

### Question 5
**Scenario:** A shell is unstable and dies on certain commands.

A. Ignore it and keep typing, because the instability is a network quirk that goes away once enough commands have run over the connection
B. Give up on this host and look for a different foothold, as a shell that dies cannot be made reliable enough for any escalation work
C. Upgrade to a fully interactive TTY, for example by spawning a PTY with Python and fixing the terminal settings
D. Reconnect repeatedly by re-running the exploit until one of the shells happens to stay alive for the whole of the task you need to do

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A raw reverse shell has no job control, no tab completion, and breaks on interactive prompts. Stabilizing it first is what makes privilege escalation and editing files viable, and it is a routine early step after any foothold.
</details>

---

### Question 6
**Scenario:** An exploit from an online database fails against the target.

A. Run it again unchanged a few times, since public exploits can fail on timing
B. Conclude the target is not vulnerable, because a failed public exploit shows it is patched
C. Read and understand the exploit: check target version, offsets, hardcoded IPs and ports, and architecture, then adapt it
D. Try a completely different host, because public exploit code should work as published

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** Public exploits routinely need edits: the return address, the listener IP, or the payload rarely match your target as-is. Blindly running exploit code is also a stability and safety risk, which is why understanding before executing is a graded habit.
</details>

---

### Question 7
**Scenario:** You need to reach a host that is only accessible from a machine you have already compromised.

A. Pivot: use port forwarding or a tunneling tool through the compromised host to route traffic into the internal segment
B. Attack it directly from your own machine, using the same tools and addresses that worked against the hosts you could already reach
C. Skip it, because hosts that cannot be reached from the attacking machine are out of scope for the exam
D. It is unreachable, since a host on an internal segment can only be contacted by machines on that segment with a physical connection

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Dual-homed hosts are the bridge into segments your attacking machine cannot route to. SSH forwarding, or a tool such as chisel or ligolo, turns the foothold into a gateway, and pivoting is a required skill for the exam's internal hosts.
</details>

---

### Question 8
**Scenario:** In an Active Directory environment, you have compromised one domain user.

A. Stop and report that more access is needed, because nothing useful can be done from a standard domain user account without elevated rights
B. Enumerate the domain: users, groups, sessions, ACLs and attack paths, using your context to map routes to higher privilege
C. Attack the domain controller directly with whatever exploits are available, since it holds the credentials for every account in the domain
D. Brute force the domain admin password from the user account, accepting the lockouts as the price of a fast result

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** AD compromise is a graph problem: one user's group memberships and delegated rights often chain to a privileged account. Mapping the paths first is far more reliable than guessing, and it is the intended approach for the exam's AD set.
</details>

---

### Question 9
**Scenario:** You capture a user's password hash. What determines whether you can use it directly?

A. The hash type and the attack: NTLM hashes can sometimes be passed or relayed without cracking, others need offline cracking
B. Hashes are always crackable instantly with a modern GPU
C. You must always crack it to recover the plaintext
D. Nothing; hashes are one-way values and useless without the original password

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Pass-the-hash works for NTLM in the right conditions, so cracking is not always necessary. When it is, wordlists with mutation rules beat brute force, because human-chosen passwords are not uniformly random.
</details>

---

### Question 10
**Scenario:** A file upload accepts your file but you need code execution.

A. Assume it is safe because the application accepted the file without an error
B. Upload a plain text file and check that it is stored, since a stored file proves that the upload feature is working as designed and is exploitable by anyone
C. Determine what the server executes: try language-appropriate extensions, content-type and magic byte tricks, and find where uploads are served
D. Give up if the application renames the file, because a renamed upload can never be reached or interpreted by the server

<details>
<summary>Answer</summary>

**Correct: C**

**Why:** A webshell only helps if the server interprets it, so the extension, the upload directory, and the server's handler configuration are what matter. Enumerating where the file lands and how it is served is the step that turns an upload into execution.
</details>

---

### Question 11
**Scenario:** Documentation and note-taking during the exam.

A. Rely on memory and write the report afterwards, as the commands are easy to recall once you have rooted each machine and the notes would only slow you down
B. Document continuously: commands, output and screenshots per host, since missing evidence loses points even for a rooted box
C. Notes are optional, because the proctors record the whole session and the graders can review everything that was done during the exam window
D. Take notes only at the end of the exam, once you know which machines were rooted and which steps were useful enough to include in the report

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** OSCP is pass-or-fail on a report as well as on access, and a compromise you cannot evidence and reproduce does not count. Contemporaneous notes also save you when you need to recreate a step under time pressure.
</details>

---

### Question 12
**Scenario:** You are stuck on a host after hours of effort.

A. Step back and re-enumerate: revisit overlooked ports, re-read output, and question an assumption you made early
B. Assume it is not exploitable and move on, because hours without progress show the host is hardened
C. Keep attacking the same service indefinitely with new wordlists and payloads
D. Attack a different network range, on the basis that a stuck host has no path to a foothold

<details>
<summary>Answer</summary>

**Correct: A**

**Why:** Tunnel vision on one service is the classic OSCP trap. The path is usually in something already in front of you that got dismissed, which is why re-enumeration beats hammering the same door harder.
</details>

---

### Question 13
**Scenario:** Which describes the safest payload choice during an authorized test?

A. A destructive payload that wipes a test file
B. Ransomware-style encryption of a sample folder, to demonstrate the business risk in terms the client will easily understand and act upon
C. A denial of service against the running service
D. A minimal payload that gives access without damaging data or degrading the system, within the rules of engagement

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** The goal is demonstrating access, not causing harm, and the rules of engagement bound what you may do. This is professional practice as much as exam etiquette: a real client's production system is not a place for destructive proofs.
</details>

---

### Question 14
**Scenario:** Which enumeration of SMB is most useful early?

A. Only check whether port 445 is closed, then record the host as having no SMB exposure and move on to the next one
B. None, because SMB is obsolete and current Windows hosts have it disabled so that there is nothing to enumerate
C. Brute force the administrator account immediately with a large wordlist, before looking at what the service exposes
D. List shares, check null or guest access, enumerate users, and check the version against known flaws

<details>
<summary>Answer</summary>

**Correct: D**

**Why:** Anonymously readable shares leak credentials, configuration, and sometimes a direct foothold. SMB version and signing state also decide whether relay attacks are viable, which is a common AD escalation route.
</details>

---

### Question 15
**Scenario:** Time management for a 24-hour exam with multiple targets.

A. Ignore easier targets in favour of the highest-value ones, since the hardest machines carry the most points toward the pass mark
B. Allocate time per target, move on when stuck, bank the achievable points first, and reserve time for the report
C. Work on every box at the same time, switching between them every few minutes so that no machine is left idle for long
D. Spend all the time on the hardest box

<details>
<summary>Answer</summary>

**Correct: B**

**Why:** The points are distributed, so banking the reachable ones beats sinking the whole window into one machine. Reserving report time is non-negotiable, because an unreported compromise scores nothing.
</details>

---

## Where to go deeper

- [OSCP cert page](../../exams/offensive-security/oscp-pen-200/) - notes, practice plan, strategy
- [Security+ practice questions](./comptia-security-plus.md) - defensive fundamentals that inform offense
- [Prompt injection explained](https://ai.noblerworks.com/safety/security/prompt-injection-explained/) - an application-layer attack class in the AI era
- [AI threat modeling](https://ai.noblerworks.com/safety/security/ai-threat-modeling/) - structured thinking about attack surface
- **[📖 OffSec PEN-200](https://www.offsec.com/courses/pen-200/)** - official course and exam page
