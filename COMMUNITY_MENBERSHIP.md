# Community membership

This doc outlines the responsibilities of contributor roles in CloudWeGo. 
The CloudWeGo project is subdivided into sub-projects under kitex (kitex & kitex-benchmark & kitex-example), netpoll(netpoll & netpoll-benchmark), thriftgo(thriftgo & thfit-gen-validator), docs(cloudwego.github.io & community) and others if may. 
Responsibilities for roles are scoped to these sub-projects (repos).

| **Role**   | **Responsibilities**                                  | **Requirements**                                             | **Defined by**                                               |
| ---------- | ----------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Member     | Active contributor in the community.  Reviewer of PRs | Sponsored by two approvers or maintainers. Multiple contributions to the project. | GitHub org member|
| Approver   | Approve accepting contributions                       | Highly experienced and active reviewer and contributor to a subproject.           | CODEOWNERS in GitHub |
| Maintainer | Set direction and priorities for a subproject         | Demonstrated responsibility and excellent technical judgement for the subproject. | CODEOWNERS, GitHub Team and repo ownership in GitHub |

## New contributors

New contributors should be：
- welcomed to the community by existing members
- helped with PR workflow
- directed to relevant documentation and communication channels (Feishu & Slack).
  
Active contributors may apply to become Members, see below requirements for details

## Member

Members are continuously active contributors in the community.
- They can have issues and PRs assigned to them.
- Members are expected to participate in community discussions and remain active contributors to the community.
  Defined by: Member of the CloudWeGo GitHub organization

### Requirements

- Have made multiple contributions to the project or community. Contributions may include, but is not limited to:
  - Authoring or reviewing PRs on GitHub
  - Filing or commenting on issues on GitHub
  - Contributing to sub-projects, or community discussions (e.g. meetings, chat, etc.)
- Have read the contributor guide
- Actively contributing to 1 or more sub-projects
- Sponsored by two approvers or maintainers (sponsors). Note the following requirements for sponsors:
  - Sponsors must have close interactions with the prospective member - e.g. code/design/proposal review, coordinating on issues, etc
- Sponsors must be approvers or maintainers in at least one CODEOWNERS file in any repo in the CloudWeGo organization
- Open an issue against the CloudWeGo/community repo
  - Ensure your sponsors are @mentioned on the issue
  - Complete every item on the checklist (preview the current version of the template)
  - Make sure that the list of contributions included is representative of your work on the project
- Have your sponsoring reviewers reply confirmation of sponsorship: +1
- Once your sponsors have responded, your request will be reviewed by the project management team (people with OWNER role). Any member among them can review the requirements and add Members to the GitHub org

### Responsibilities and privileges

- Responsive to issues and PRs assigned to them (inactivity for more than 1 month may result in suspension until active again)
- Active owner of code contributed by them (unless ownership is explicitly transferred)
  - Code is well tested
  - Tests consistently pass
  - Addresses bugs or issues discovered after code is accepted
  - Members are encouraged to review and approve via the GitHub workflow. This review work, while not sufficient to merge a PR, does accrue toward the Member becoming an Approver. Merge approval and final review are performed by an Approver
- Members can be assigned to issues and PRs, and people can ask members for reviews with a /cc @username

## Approver

Code approvers are able to both review and approve code contributions, as well as help maintainers triage issues and do project management.
While code review is focused on code quality and correctness, approval is focused on holistic acceptance of a contribution including: backwards/forwards compatibility, adhering to API and conventions, performance and correctness issues, interactions with other sub-projects, etc.
Approver status can be scoped to a part of the codebase. For example, critical core components may have higher bar for becoming an approver.

### Requirements

The following apply to the part of the codebase for which one would be an approver in the CODEOWNERS files:
- Reviewer of the codebase for at least 1 month
- Reviewer for, or author of, at least 5 substantial PRs to the codebase, with the definition of substantial area to the maintainer's discretion (e.g. refactors/adds new functionality rather than one-line pulls)
- Nominated by a maintainer:
  - With no objections from other maintainers
  - Done through PR to update the CODEOWNERS

### Responsibilities and privileges

The following apply to the part of the codebase for which one would be an approver in the CODEOWNERS files.
- Approver status may be a precondition to accepting large code contributions
- Demonstrate sound technical judgement
- Responsible for project quality control via code reviews
  - Focus on holistic acceptance of contribution such as dependencies with other features, backwards / forwards compatibility, API and conventions, etc
- Expected to be responsive to review requests (inactivity for more than 1 month may result in suspension until active again)
- Mentor contributors and reviewers
- May approve code contributions for acceptance
