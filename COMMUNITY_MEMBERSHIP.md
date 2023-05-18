# Community membership

This doc outlines the responsibilities of contributor roles in CloudWeGo. 

The CloudWeGo project is subdivided into subprojects under:
- Kitex (Kitex & Kitex ecosystem & kitex-contrib)
- Hertz (Hertz & Hertz ecosystem & hertz-contrib)
- Volo (Volo & Volo ecosystem & volo-rs & Motore & Pilota)
- Netpoll (Netpoll & Netpoll ecosystem)
- Monoio (Monoio & Monoio ecosystem)
- Serdes (Thriftgo & Frugal & Fastpb & Sonic & thrift-gen-validator)
- Shmipc (shmipc-spec & shmipc-go)
- Website & Docs (cloudwego.github.io & community)
- Others if may. 

Responsibilities for roles are scoped to these subprojects (repos) defined by GitHub team.

| **Role**   | **Responsibilities**                                         | **Requirements**                                             | **Defined by**                    |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------------- |
| Member     | Active contributor in the community.                         | Sponsored by two approvers or maintainers. Multiple contributions to the project. | GitHub org member                 |
| Committer  | Active code contributor and/or issue reply in the subproject. | Sponsored by two approvers or maintainers. Multiple code contributions to the project. | GitHub subproject committer Team  |
| Reviewer   | Review contributions from other members and give feedback and instructions. | Continuous history of review and authorship in a subproject. | GitHub subproject reviewer Team   |
| Approver   | Approve accepting contributions.                             | Highly experienced and active reviewer and contributor to a subproject. | GitHub subproject approver Team   |
| Maintainer | Set direction and priorities for a subproject                | Demonstrated responsibility and excellent technical judgement for the subproject. | GitHub subproject maintainer Team |

## New contributors

New contributors should be：
- welcomed to the community by existing members
- helped with PR workflow
- directed to relevant documentation and communication channels (Feishu & Slack).
  

Active contributors may apply to become Members or Committers, see below requirements for details

## Member

Members are continuously active contributors in the community.
- Enabled [two-factor authentication](https://help.github.com/articles/about-two-factor-authentication) on their GitHub account
- They can have issues and PRs assigned to them.
- Members are expected to participate in community discussions and remain active contributors to the community.
  Defined by: Member of the CloudWeGo GitHub organization

### Requirements

- Have made multiple contributions to the project or community. Contributions may include, but is not limited to:
  - Filling or commenting on issues on GitHub
  - Contributing to subprojects, or community discussions (e.g. meetings, chat, etc.)
  - Introduction and promotion, e.g. Deliver multiple talks in tech meetup/conference regarding to this project
- Have read the [contributor guide](https://github.com/cloudwego/community/blob/master/CONTRIBUTING.md)
- Sponsored by two approvers or maintainers (sponsors). Note the following requirements for sponsors:
  - Sponsors must have close interactions with the prospective member - e.g. code/design/proposal review, coordinating on issues, etc
  - Sponsors must be approvers or maintainers in at least one team in the CloudWeGo organization
- Open an [issue](https://github.com/cloudwego/community/issues) against the CloudWeGo/community repo
  - Ensure your sponsors are @mentioned on the issue
  - Complete every item on the checklist (preview the current version of the template)
  - Make sure that the list of contributions included is representative of your work on the project
- Have your sponsoring reviewers reply confirmation of sponsorship: +1
- Once your sponsors have responded, your request will be reviewed by the project management team (people with OWNER role). Any member among them can review the requirements and add Members to the GitHub org

### Responsibilities and privileges

- Continously contribute to the community (inactivity for more than 2 month may result in suspension until active again)

## Committer

Committers are continously active code contributors in the subproject(s).

**Defined by:** *committers* team of subproject.

- Enabled [two-factor authentication](https://help.github.com/articles/about-two-factor-authentication) on their GitHub account
- They can have issues and PRs assigned to them.
- Committers are expected to participate in community discussions and remain active code contributors to the community.
  Defined by: Member of subproject committer team

### Requirements

- Have made multiple contributions to the project or community. Contributions may include, but is not limited to:
  - Authoring or reviewing PRs on GitHub
  - Filling or commenting on issues on GitHub
  - Contributing to subprojects, or community discussions (e.g. meetings, chat, etc.)
  - Introduction and promotion, e.g. Deliver multiple talks in tech meetup/conference regarding to this project
  - For those subprojects, at least one contribution to a **new feature** is a must
- Have read the [contributor guide](https://github.com/cloudwego/community/blob/master/CONTRIBUTING.md)
- Sponsored by two approvers or maintainers (sponsors). Note the following requirements for sponsors:
  - Sponsors must have close interactions with the prospective member - e.g. code/design/proposal review, coordinating on issues, etc
  - Sponsors must be approvers or maintainers in at least one team in the subproject.
- Open an [issue](https://github.com/cloudwego/community/issues) against the CloudWeGo/community repo
  - Ensure your sponsors are @mentioned on the issue
  - Complete every item on the checklist (preview the current version of the template)
  - Make sure that the list of contributions included is representative of your work on the project
- Have your sponsoring reviewers reply confirmation of sponsorship: +1
- Once your sponsors have responded, your request will be reviewed by the project management team (people with OWNER role). Any member among them can review the requirements and add Members to the subproject team.

### Responsibilities and privileges

- Responsive to issues and PRs assigned to them (inactivity for more than 1 month may result in suspension until active again)
- Active owner of code contributed by them (unless ownership is explicitly transferred)
  - Code is well tested
  - Tests consistently pass
  - Addresses bugs or issues discovered after code is accepted
  - Members are encouraged to review and approve via the GitHub workflow. This review work, while not sufficient to merge a PR, does accrue toward the Member becoming an Approver. Merge approval and final review are performed by an Approver
- Members can be assigned to issues and PRs, and people can ask members for reviews with a /cc @username
- Tests can be run against their PRs automatically. No approval is needed.
- Members can triage issues such as add labels to them.

**Note:** members who frequently contribute code are expected to proactively perform code reviews and work towards becoming a primary *reviewer* for the subproject that they are active in.

## Reviewer

Code reviewers are able to both review and approve code contributions. They are knowledgeable about both the codebase and software engineering principles.

**Defined by:** *reviewers* team of subproject.

Reviewer status can be scoped to a part of the codebase.

**Note:** Acceptance of code contributions requires at least one approver in addition to the assigned reviewers.

### Requirements

The following apply to the part of the codebase for which one would be an reviewer in the subproject:

- Committer for at least 1 month
- Primary reviewer for at least 5 PRs to the codebase
- Reviewer for, or author of, at least 10 substantial PRs to the codebase, with the definition of substantial area to the maintainer's discretion (e.g. refactors/adds new functionality rather than one-line pulls)
- Sponsored by a subproject maintainer
  - With no objections from other maintainers

- May either self-nominate, be nominated by an maintainer in this subproject

### Responsibilities and privileges

The following apply to the part of the codebase for which one would be an reviewer in the subproject.

- Code reviewer status may be a precondition to accepting large code contributions
- Responsible for project quality control via code reviews
  - Focus on code quality and correctness, including testing and factoring
  - May also review for more holistic issues, but not a requirement
- Assigned PRs to review related to subproject of expertise
- Assigned test bugs related to subproject of expertise
- Granted "write access" to the subproject

## Approver

Code approvers are able to both review and approve code contributions. While code review is focused on code quality and correctness, approval is focused on holistic acceptance of a contribution including: backwards/forwards compatibility, adhering to API and conventions, performance and correctness issues, interactions with other subprojects, etc.

**Defined by:** *approvers* team of subproject.

Approver status can be scoped to a part of the codebase. For example, critical core components may have higher bar for becoming an approver.

### Requirements

The following apply to the part of the codebase for which one would be an approver in the subproject:
- Reviewer of the codebase for at least 3 month
- Primary reviewer for at least 10 substantial PRs to the codebase
- Reviewed at least 30 merged PRs to the codebase
- Nominated by a subproject maintainer:
  - With no objections from other maintainers

### Responsibilities and privileges

The following apply to the part of the codebase for which one would be an approver in the subproject.
- Approver status may be a precondition to accepting large code contributions
- Demonstrate sound technical judgement
- Responsible for project quality control via code reviews
  - Focus on holistic acceptance of contribution such as dependencies with other features, backwards / forwards compatibility, API and conventions, etc
- Expected to be responsive to review requests (inactivity for more than 1 month may result in suspension until active again)
- Mentor contributors and reviewers
- May approve code contributions for acceptance

## Maintainer

**Note:** This is a generalized high-level description of the role, and the specifics of the subproject maintainer role's responsibilities and related processes *MUST* be defined for individual subprojects.

Maintainers are the technical authority for a subproject. They *MUST* have demonstrated both good judgement and responsibility towards the health of that subproject. Maintainers *MUST* set technical direction and make or approve design decisions for their subproject - either directly or through delegation of these responsibilities.

**Defined by:** *maintainers* team in subproject.

### Requirements

The process for becoming a Maintainer should be defined by the Maintainers of each subproject. Unlike the roles outlined above, the Maintainers of a subproject are typically limited to a relatively small group of decision makers and updated as fits the needs of the subproject.

The following apply to the subproject for which one would be a maintainer.

- Deep understanding of the technical goals and direction of the subproject
- Deep understanding of the technical domain of the subproject
- Sustained contributions to design and direction by doing all of:
  - Authoring and reviewing proposals
  - Initiating, contributing and resolving discussions (emails, GitHub issues, meetings)
  - Identifying subtle or complex issues in designs and implementation PRs
- Directly contributed to the subproject through implementation and / or review

### Responsibilities and privileges

The following apply to the subproject for which one would be a maintainer.

- Make and approve technical design decisions for the subproject.
- Set technical direction and priorities for the subproject.
- Define milestones and releases.
- Mentor and guide approvers, reviewers, committers, and contributors to the subproject.
- Ensure continued health of subproject
  - Adequate test coverage to confidently release
  - Tests are passing reliably (i.e. not flaky) and are fixed when they fail
- Ensure a healthy process for discussion and decision making is in place.
- Work with other subproject maintainers to maintain the project's overall health and success holistically

## Inactive members

*Members are continuously active contributors in the community.*

A core principle in maintaining a healthy community is encouraging active participation. It is inevitable that people's focuses will change over time and they are not expected to be actively contributing forever.

However, being a member of one of the CloudWeGo GitHub organizations comes with an elevated set of permissions. These capabilities should not be used by those that are not familiar with the current state of the CloudWeGo project.

Therefore members with an extended period away from the project with no activity will be removed from the CloudWeGo Github Organizations and will be required to go through the org membership process again after re-familiarizing themselves with the current state.

### How inactivity is measured

Inactive members are defined as members of one of the CloudWeGo Organizations with **no** contributions across any organization within 6 months.

After an extended period away from the project with no activity those members would need to re-familiarize themselves with the current state before being able to contribute effectively.
