# Security Release Process

Kubernetes is a large growing community of volunteers, users, and vendors. The Kubernetes community has adopted this security disclosures and response policy to ensure we responsibly handle critical issues.


**Table of Contents**

- [Product Security Committee (PSC)](#product-security-committee-psc)
  * [Product Security Committee Membership](#product-security-committee-membership)
    + [Joining](#joining)
      - [PSC Lazy Consensus Selection](#psc-lazy-consensus-selection)
    + [Stepping Down](#stepping-down)
    + [Responsibilities](#responsibilities)
    + [Roles](#roles)
      - [Release/Project Manager](#releaseproject-manager)
      - [Triage](#triage)
      - [Infra](#infra)
      - [Disclosure](#disclosure)
      - [Associate](#associate)
    + [Per-Issue Assignment Options](#per-issue-assignment-options)
      - [Scheduled Rotation](#scheduled-rotation)
      - [Queue](#queue)
    + [Release Manager Role](#release-manager-role)
- [Disclosures](#disclosures)
  * [Private Disclosure Processes](#private-disclosure-processes)
  * [Public Disclosure Processes](#public-disclosure-processes)
- [Patch, Release, and Public Communication](#patch-release-and-public-communication)
  * [Fix Team Organization](#fix-team-organization)
  * [Fix Development Process](#fix-development-process)
  * [Fix Disclosure Process](#fix-disclosure-process)
  * [Retrospective](#retrospective)
- [Private Distributors List](#private-distributors-list)
- [Severity Thresholds - How We Do Vulnerability Scoring](#severity-thresholds---how-we-do-vulnerability-scoring)
  * [Server](#server)
    + [Critical](#critical)
      - [Elevation of privilege](#elevation-of-privilege)
      - [Information disclosure (targeted)](#information-disclosure-targeted)
    + [High](#high)
      - [Denial of service](#denial-of-service)
      - [Elevation of privilege](#elevation-of-privilege-1)
      - [Information disclosure (targeted)](#information-disclosure-targeted-1)
    + [Medium](#medium)
    + [Low](#low)
      - [Tampering](#tampering)
  * [Client](#client)
    + [Critical](#critical-1)
      - [Elevation of privilege](#elevation-of-privilege-2)
      - [Information disclosure (targeted)](#information-disclosure-targeted-2)
    + [High](#high-1)
      - [Denial of service](#denial-of-service-1)
      - [Elevation of privilege](#elevation-of-privilege-3)
      - [Tampering](#tampering-1)
    + [Medium](#medium-1)
      - [Tampering](#tampering-2)
    + [Low](#low-1)
      - [Denial of service](#denial-of-service-2)
      - [Tampering](#tampering-3)
  * [Glossary](#glossary)
    + [Adjacent Network Access](#adjacent-network-access)
    + [Authenticated User](#authenticated-user)
    + [Local Access](#local-access)
    + [Remote Anonymous User](#remote-anonymous-user)
    + [High Value Asset](#high-value-asset)
    + [Service Failure](#service-failure)

## Product Security Committee (PSC)

Security vulnerabilities should be handled quickly and sometimes privately. The primary goal of this process is to reduce the total time users are vulnerable to publicly known exploits.

The Product Security Committee (PSC) is responsible for organizing the entire response including internal communication and external disclosure but will need help from relevant developers and release managers to successfully run this process.

The initial Product Security Committee will consist of volunteers subscribed to the private [Kubernetes Security](https://groups.google.com/a/kubernetes.io/forum/#!forum/security) list. These are the people who have been involved in the initial discussion and volunteered:

- Brandon Philips (**[@philips](https://github.com/philips)**) `<bphilips@redhat.com>` [4096R/154343260542DF34]
- CJ Cullen (**[@cjcullen](https://github.com/cjcullen)**) `<cjcullen@google.com>`
- Tim Allclair (**[@tallclair](https://github.com/tallclair)**) `<tallclair@google.com>` [4096R/0x5E6F2E2DA760AF51]
- Jordan Liggitt (**[@liggitt](https://github.com/liggitt)**) `<jordan@liggitt.net>` [4096R/0x39928704103C7229]
- Joel Smith (**[@joelsmith](https://github.com/joelsmith)**) `<joelsmith@redhat.com>`
- Jonathan Pulsifer (**[@jonpulsifer](https://github.com/jonpulsifer)**) `<jonathan.pulsifer@shopify.com>`

[Associate](#Associate) members include:

- Micah Hausler (**[@micahhausler](https://github.com/micahhausler)**) `<mhausler@amazon.com>`
- Luke Hinds (**[@lukehinds](https://github.com/lukehinds)**) `lhinds@redhat.com`
- Swamy Shivaganga Nagaraju (**[@swamymsft](https://github.com/swamymsft)**) `<gaswamy@microsoft.com>`

### Contacting the Team

There are a number of contact points for the PSC and release managers in charge of security releases. Please use the correct forum for the best and fastest response.

| List or Group | Visibility | Uses |
| ------------- | ---------- | ---- |
| security@kubernetes.io | Private | Kubernetes security disclosures. This list is closely monitored and triaged by the PSC. [See the disclosure guide for full details.](http://kubernetes.io/security) |
| [kubernetes-security-discuss Google Group](https://groups.google.com/forum/#!forum/kubernetes-security-discuss) | Public | Discussion about security disclosure handling, this document, and other updates. |
| security-release-team@kubernetes.io | Private | Release manager private discussion. All members are subscribed to security@kubernetes.io. |
| security-discuss-private@kubernetes.io | Private | PSC private discussion. All members are subscribed to security@kubernetes.io |

### Product Security Committee Membership

#### Joining

New potential members to the PSC will first fill a minimum of a 3 month rotation in the [Associate](#Associate) role.

These individuals will be nominated by individuals on steering committee, PSC, or release manager lead and patch release manager.

The PSC has a goal to expand the PSC to 7 members by end of year (2018) or
early 2019. [Please delete this when this has been done :)].

To encourage diversity members will also abide by a 1/2 maximal representation from any one company at any time. If representation changes due to job shifts or mergers then members are encouraged to grow the team or replace themselves through mentoring new members. Being overlimit should not continue for longer than 12 months to give time to identify and mentor new members.

##### PSC Lazy Consensus Selection

Selection of new members from the associates will be done by lazy consensus.

- Use lazy consensus amongst members for adding new people up to 7 from pool of associate members with fallback on majority vote.
- Use lazy consensus amongst other members with fallback on majority vote to accept proposal on step down.

#### Stepping Down

Members may step down at anytime and propose a replacement from pool of eligible associate members.

#### Responsibilities

- Members should remain active and responsive in their Roles.
- Members taking an extended leave of 1 or more months should coordinate with other members to ensure the role is adequately staffed during the leave.
- Members going on leave for 1-3 months may identify a temporary replacement.
- Members of a role should remove any other members that have not communicated a leave of absence and either cannot be reached for more than 1 month or are not fulfilling their documented responsibilities for more than 1 month. This may be done through a super-majority vote of members.


#### Roles

Membership on the Product Security Committee is based on filling a specific role.
These are defined below to make sure everyone "carries water".

##### Release/Project Manager

Per issue, sees it through to the end. The sheep herder.
A rotating role so we can make sure everyone helps and no one is stuck constantly with the sheep herding.

##### Triage

Makes sure the people who should be in "the know" (aka notified) are notified, also responds to issues that are not actually issues and lets the OP know that.
This person is the escalation path for a bug if it is one.
The on-call PSC member should triage the request. If the on-call member is unavailable then it is first come first serve on the alert escalation.

##### Infra

Making sure we can test the fixes appropriately. This person is the build cop.
Who do you call when the cluster is not well or you gotta test something weird, or the release branch is all messed up? This person.

##### Disclosure

Handles public messaging around the bug. Documentation on how to upgrade. Changelog. Explaining to public the severity. Notifications of bugs sent to mailing lists etc. Requests CVEs.

##### Associate

A role for those wishing to join the PSC. They should not currently be a member
of security@kubernetes.io.

Their rotation will involve the following:

- lead disclosures that are publicly disclosed on a public GitHub issue tracker
    (often done because of reporter request, a low CVSS score, or design issue
    that requires long-term refactoring).
- assisting in process improvements, bug bounty administration, audits, or other non-disclosure activities

#### Per-Issue Assignment Options

##### Scheduled Rotation

Each week has a primary & secondary for each role. If something comes up that week, primary owns it. Secondary is there if we can't get a hold of the primary, or if primary has a really good reason why they can’t handle it.

##### Queue

Each role has an ordered list of “who’s handling the next issue.” If something comes up, top of the list takes it. If we can’t contact them, or they have a good reason not to, we go down the list. We’d probably need some coordination of vacation schedules to make sure we don’t leave a role unstaffed.

#### Release Manager Role

Also included on the private [Security Release Team](https://groups.google.com/a/kubernetes.io/forum/#!forum/security-release-team) list are all [Release Managers](/release-managers.md).

It is the responsibility of the Release Managers to add and remove people from the Security Release Team group as Kubernetes minor releases created and deprecated.

## Disclosures

### Private Disclosure Processes

The Kubernetes Community asks that all suspected vulnerabilities be privately and responsibly disclosed via the Private Disclosure process available at [https://kubernetes.io/security](https://kubernetes.io/security).

### Public Disclosure Processes

If you know of a publicly disclosed security vulnerability please IMMEDIATELY email [security@kubernetes.io](mailto:security@kubernetes.io) to inform the Product Security Committee (PSC) about the vulnerability so they may start the patch, release, and communication process.

If possible the PSC will ask the person making the public report if the issue can be handled via a private disclosure process. If the reporter denies the PSC will move swiftly with the fix and release process. In extreme cases you can ask GitHub to delete the issue but this generally isn't necessary and is unlikely to make a public disclosure less damaging.

## Patch, Release, and Public Communication

For each vulnerability a member of the PSC will volunteer to lead coordination
with the Fix Team, Release Managers and is responsible for sending disclosure
emails to the rest of the community. This lead will be referred to as the Fix Lead.

The role of Fix Lead should rotate round-robin across the PSC.

All of the timelines below are suggestions and assume a Private Disclosure.
The Fix Lead drives the schedule using their best judgment based on severity,
development time, and release manager feedback. If the Fix Lead is dealing with
a Public Disclosure all timelines become ASAP. If the fix relies on another
upstream project's disclosure timeline, that will adjust the process as well.
We will work with the upstream project to fit their timeline and best protect
our users.

### Fix Team Organization

These steps should be completed within the first 24 hours of Disclosure.

- The Fix Lead will work quickly to identify relevant engineers from the affected projects and packages and CC those engineers into the disclosure thread. This selected developers are the Fix Team. A best guess is to invite all assignees in the OWNERS file from the affected packages.
- The Fix Lead will get the Fix Team access to private security repos in the kubernetes-security GitHub org to develop the fix.

Note: The kubernetes-security GitHub org is co-owned and viewable by the PSC and Kubernetes Release Managers. Management of the org is done by SIG Contributor Experience's [GitHub management subproject](https://git.k8s.io/community/github-management).

### Fix Development Process

These steps should be completed within the 1-7 days of Disclosure.

- The Fix Lead and the Fix Team will create a [CVSS](https://www.first.org/cvss/specification-document) using the [CVSS Calculator](https://www.first.org/cvss/calculator/3.0). They will also use the [Severity Thresholds - How We Do Vulnerability Scoring](#severity-thresholds---how-we-do-vulnerability-scoring) to determine the effect and severity of the bug. The Fix Lead makes the final call on the calculated risk; it is better to move quickly than make the perfect assessment.
- The Fix Lead will request a CVE from the [Kubernetes CVE Numbering Authority](cve-requests.md).
- The Fix Team will notify the Fix Lead that work on the fix branch is complete once there are LGTMs on all commits in the private repo from one or more relevant assignees in the relevant OWNERS file.

If the CVSS score is under ~4.0
([a low severity score](https://www.first.org/cvss/specification-document#i5))
or the assessed risk is low the Fix Team can decide to slow the release process
down in the face of holidays, developer bandwidth, etc. These decisions must be
discussed on the security@kubernetes.io mailing list.

If the CVSS score is under ~7.0 (a medium severity score), the Fix Lead may
choose to carry out the fix semi-publicly. This means that PRs are made directly
in the public kubernetes/kubernetes repo, while restricting discussion of the
security aspects to private channels. The fix lead will make the determination
whether there would be user harm in handling the fix publicly that outweighs the
benefits of open engagement with the community.

Note: CVSS is convenient but imperfect. Ultimately, the fix lead has discretion
on classifying the severity of a vulnerability.

No matter the CVSS score, if the vulnerability requires
[User Interaction](https://www.first.org/cvss/user-guide#5-4-User-Interaction),
especially in client components like kubectl, or otherwise has a
straightforward, non-disruptive mitigation, the Fix Lead may choose to disclose
the vulnerability before a fix is developed if they determine that users would
be better off being warned against a specific interaction.

### Fix Disclosure Process

With the Fix Development underway the Fix Lead needs to come up with an overall communication plan for the wider community. This Disclosure process should begin after the Fix Team has developed a Fix or mitigation so that a realistic timeline can be communicated to users.

**Optional Fix Disclosure to Private Distributors List** (Completed within 1-14 days of Disclosure):

- The Fix Lead will make a determination with the help of the Fix Team if an issue is critical enough to require early disclosure to distributors. Generally this Private Distributor Disclosure process should be reserved for remotely exploitable or privilege escalation issues. Otherwise, this process can be skipped.
- The Fix Lead will email the patches to distributors-announce@kubernetes.io so distributors can prepare builds to be available to users on the day of the issue's announcement. Distributors should read about the [Private Distributors List](#private-distributors-list) to find out the requirements for being added to this list.
- **What if a vendor breaks embargo?** The PSC will assess the damage. The Fix Lead will make the call to release earlier or continue with the plan. When in doubt push forward and go public ASAP.

**Fix Release Day** (Completed within 1-21 days of Disclosure)

- The [Private Distributors List](#private-distributors-list) will be notified at least 24 hours in advance of a pending release with the public messaging, date, and time of the announcement.
- The Fix Lead will cherry-pick the patches onto the master branch and all relevant release branches. The Fix Team will `/lgtm` and `/approve`.
- The Release Managers will merge these PRs as quickly as possible. Changes shouldn't be made to the commits at this point, to prevent potential conflicts with the patches sent to distributors, and conflicts as the fix is cherry-picked around branches.
- The Release Managers will ensure all the binaries are built, publicly available, and functional.
- The Fix Lead will announce the new releases, the CVE number, severity, and impact, and the location of the binaries to get wide distribution and user action. As much as possible this announcement should be actionable, and include any mitigating steps users can take prior to upgrading to a fixed version. The recommended target time is 4pm UTC on a non-Friday weekday. This means the announcement will be seen morning Pacific, early evening Europe, and late evening Asia. The announcement will be sent via the following channels:
  - kubernetes-dev@googlegroups.com
  - kubernetes-announce@googlegroups.com
  - kubernetes-security-announce@googlegroups.com
  - [#announcements slack channel](https://kubernetes.slack.com/messages/C9T0QMNG4)
  - [discuss.kubernetes.io](https://discuss.kubernetes.io/c/announcements) forum
- The Fix Lead will remove the Fix Team from the private security repo.

## Private Distributors List

This list is used to provide actionable information to multiple distribution
vendors at once.

See the [private distributor list doc](private-distributors-list.md) for more information.

### Retrospective

These steps should be completed 1-3 days after the Release Date. The retrospective process [should be blameless](https://landing.google.com/sre/book/chapters/postmortem-culture.html).

- The Fix Lead will send a retrospective of the process to kubernetes-dev@googlegroups.com including details on everyone involved, the timeline of the process, links to relevant PRs that introduced the issue, if relevant, and any critiques of the response and release process.
- The Release Managers and Fix Team are also encouraged to send their own feedback on the process to kubernetes-dev@googlegroups.com. Honest critique is the only way we are going to get good at this as a community.

## Severity Thresholds - How We Do Vulnerability Scoring

The content presented below outlines basic criteria when considering the effect
of bugs disclosed to the Product Security Committee and their severity. These apply
mostly to items in "core" but could be abstractly applied to those in other
repos as well.

### Server

The "server" pertains to any "server-side components" (see below) we distribute,
but you can specifically think of `kube-apiserver` and `kubelet` being the main ones.

"Server-side components" pertains to:

- Components built from source in the `kubernetes` github organization and
  [all current organizations in use](https://git.k8s.io/community/github-management/README.md#actively-used-github-organizations)
- Container images under the `k8s.gcr.io` repository
- Containers included in the [core addons directory](https://git.k8s.io/kubernetes/cluster/addons)

The server classification is usually not appropriate when user interaction
is part of the exploitation process, those should fall under the
[client](#client) classifications as "client" implies user interaction with a
client.
If a "Critical" vulnerability exists only on server
components, and is exploited in a way that requires user interaction and results
in the compromise of the server, the severity may be reduced from "Critical" to
"High" in accordance with the data definition of extensive user
interaction presented at the start of the client severity pivot.

#### Critical

Network worms or _unavoidable_ cases where the server is "compromised."

##### Elevation of privilege

The ability to either execute arbitrary code or obtain more privilege than
authorized.

- [Remote Anonymous User](#remote-anonymous-user)
    - Unauthorized access. Examples:
        - read, write, or delete access to sensitive API objects
        - arbitrary writing/deletion to the file system or anywhere in the
          cluster that should not typically be modifiable
        - getting data from the server or server components
    - Execution of arbitrary code (remote code execution in the server)

This includes all write access violations.

##### Information disclosure (targeted)

Cases where an unprivileged user can locate and read highly sensitive
information from anywhere on the system, including system information that was
not intended or designed to be exposed.

- [Remote Anonymous User](#remote-anonymous-user)
    - Unauthorized access. Examples:
        - Personally identifiable information (PII) disclosure
          (email addresses, cloud provider credentials)
        - Attacker can collect private data without user consent or in a covert fashion
        - Secrets data
        - System credentials

#### High

"Critical" attacks are downgraded to "High" when requiring
[adjacent network access](adjacent-network-access).

Non-default (or non-typical) critical scenarios or cases where
mitigations exist that can help prevent critical scenarios.

##### Denial of service

Must be "easy to exploit" by sending a small amount of data or be otherwise
quickly induced.

- [Remote Anonymous User](#remote-anonymous-user)
    - Persistent DoS. Examples:
        - Sending a single malicious request results in
          [service failure](#service-failure)
        - Sending a small number of requests that causes a
          [service failure](#service-failure)
    - Temporary DoS. Examples:
        - Sending a small number of requests that causes the system to be
          unusable for a period of time
        - Server being down for a minute or longer
        - A single remote client consuming all available resources
          (sessions, memory) on a server by establishing sessions and keeping them open

- [Authenticated User](#authenticated-user)
    - Persistent DoS against a [high value asset](#high-value-asset). Example:
        - Sending a small number of requests that causes a
          [service failure](#service-failure) for a
          [high value asset](#high-value-asset)

##### Elevation of privilege

The ability to either execute arbitrary code or obtain more privilege than
authorized. This includes all write access violations.

- [Authenticated User](#authenticated-user)
    - Unauthorized access. Examples:
        - arbitrary writing to the file system or server components like etcd,
          where the user should not have the ability to write
        - reading or writing to API objects where the user should not be able
          to
        - getting data from the server or server components, where the user
          should not have the ability to read
        - execution of arbitrary code (like creating a pod or remote code execution
          attacks)

Breaking or bypassing any security feature provided. A vulnerability in a
security feature is rated “High” by default, but the rating may be adjusted
based on other considerations as documented here.

Examples:
- Disabling or bypassing a `NetworkPolicy` or `PodSecurityPolicy` without
winforming users or gaining consent
- Reconfiguring a `NetworkPolicy` and allowing connections to other processes
without consent

An entity (computer, server, user, process) is able to masquerade as a
specific entity (user or computer) of his/her choice.

Examples:
- Service masquerades as the API server for the cluster and effectively
  man-in-the-middle's the real API server.
- API server uses client certificate authentication (SSL) improperly to allow
  an attacker to be identified as any user of his/her choice
- RBAC bug that allows a malicious remote user to be seen as a different user
  of his or her choice


##### Information disclosure (targeted)

Cases where an anonymous user can easily read sensitive information on the
system from specific locations, including system information that was not
intended/designed to be exposed.

Examples:

- Targeted disclosure of the existence of an arbitrary file
- Arbitrary filesystem or application data that should not typically be accessed
- Arbitrary API resources that should not typically be accessed
- Workload & namespace names or identifying metadata
- System & workload logs that are not typically exposed
- Workload or user-created metrics

#### Medium

"High" attacks are downgraded to "Medium" when requiring [local
access](#local-access) or when there is a straight-forward mitigation.

##### Information disclosure (targeted)

Cases where an anonymous user can easily read anonymous (non-sensitive)
information on the system, including system metrics that were not intended to be
exposed.

Examples:

- System metrics common to most Kubernetes installs that were not intended to be
  public
- Non-identifying workload metadata (e.g. UIDs, creationTimestamps,
  resourceVersions)

#### Low

"Medium" attacks are downgraded to "Low" when there is a straight-forward
mitigation and the attack requires quite a few non-default or very untypical
scenarios to trigger.

##### Tampering

Temporary modification of data in a specific scenario that does not persist.

### Client

"User interaction" can only happen in client-driven scenario.

Using `kubectl` or a client library are considered user interaction.

The target is a user or user's computer in these scenarios.

The effect of user interaction is not one level reduction in severity,
but is a reduction in severity in certain circumstances where user interaction
is required.

The distinction exists to help differentiate
fast-spreading and wormable attacks from those where because
the user interacts, the attack is slowed down.

#### Critical

Network worms or _unavoidable_ cases where the client is "compromised" without
warnings or prompts.

##### Elevation of privilege

The ability to either execute arbitrary code or obtain more privilege than
authorized. This includes all write access violations.

- [Remote Anonymous User](#remote-anonymous-user)
    - Unauthorized access. Examples:
        - read, write, and delete access to sensitive API objects
        - arbitrary writing/reading/deletion to/from the file system
    - Execution of arbitrary code (remote code execution on the client's system)

##### Information disclosure (targeted)

Cases where the attacker can locate and read information from anywhere on the
system, including system information that was not intended or designed to be
exposed.

- [Remote Anonymous User](#remote-anonymous-user)
    - Unauthorized access. Examples:
        - Personally identifiable information (PII) disclosure (email addresses, local data)
        - Client "phone-ing home" without permission

#### High

Non-default critical scenarios or cases where mitigations exist that can help
prevent critical scenarios.

##### Denial of service

System corruption DoS requires re-installation of system and/or components.

Examples:

- Calling a `kubectl` command makes the local machine unbootable.

##### Elevation of privilege

The ability to either execute arbitrary code or obtain more privilege than
authorized. This includes all write access violations.

- [Authenticated User](#authenticated-user)
    - Unauthorized access. Examples:
        - arbitrary writing/deletion on the file system,
          where the user should not have the ability to do so
        - reading or writing to API objects where the user should not be able
          to
        - local low privilege user can elevate themselves to another user,
          administrator, or local system.
    - Execution of arbitrary code (remote code execution via the client)

Breaking or bypassing any security feature provided. A vulnerability in a
security feature is rated “High” by default, but the rating may be adjusted
based on other considerations as documented here.

Examples:
- Disabling or bypassing a RBAC without informing users or gaining consent
- Reconfiguring RBAC without consent

##### Tampering

Modification of any user data or data used to make trust decisions
in a common or default scenario where the modification persists.
This includes permanent or persistent modification of any user or system data
used in a common or default scenario.

Examples:

- Modification of application data files such as `~/.kube` in a specific
  scenario
- Modification of cluster or objects without user consent in a specific scenario

#### Medium

##### Tampering

Modification of any user data or data used to make trust decisions
in a specific scenario where the modification persists.
This includes permanent or persistent modification of any user or system data
used in a specific scenario.

Examples:

- Modification of application data files such as `~/.kube` in a specific scenario
- Modification of cluster or objects without user consent in a specific scenario

#### Low

##### Denial of service

Temporary DoS requires restart of the client application.

Example:

- Running a `kubectl` command crashes itself or the API server in a way that is
  recoverable.

##### Tampering

Temporary modification of data in a specific scenario that does not persist.

### Glossary

#### Adjacent Network Access

On the private network. They can access internal IP addresses.

#### Authenticated User

An authenticated user can be:

- Unprivileged: authenticated, but with no privileges
- Privileged: authenticated, with some privileges

#### Local Access

On the same physical host (or VM).

#### Remote Anonymous User

Remote implies from an arbitrary network location. The attacker can only access
externally exposed, public facing IP addresses.

Anonymous implies the attacker requires no credentials or Authentication.

#### High Value Asset

A mission critical component such that if/when it has failed the entire cluster
is unusable. For example, if the master services/nodes are
unreachable or in a failure mode, the entire cluster is basically unusable.

#### Service Failure

Failure in such a way that the system/service requires intervention from
a human operator to recover.
