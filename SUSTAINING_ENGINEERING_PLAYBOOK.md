# Sustaining Engineering Playbook

## Overview

Sustaining Engineering (SE) is part of Experience Engineering (XE) organization. Our mission is to improve long-term support for Red Hat products, developing a model that extends across the Red Hat product portfolio.

### Our Purpose

> To provide important updates for earlier releases so that customers have the freedom to upgrade in a way that helps meet their business goals.

### Scope

- **Critical and Important** impact security updates (CVEs)
- **Urgent-priority** bug fixes
- Extended life streams/offerings: EUS, TUS, E4S, AMC/AUS, and ELS

---

## Table of Contents

1. [Team Structure](#team-structure)
2. [Communication Channels](#communication-channels)
3. [Onboarding](#onboarding)
4. [Product Areas](#product-areas)
5. [Tools & Infrastructure](#tools--infrastructure)
6. [Workflows & Processes](#workflows--processes)
7. [Release Process](#release-process)
8. [Quality Engineering (QE)](#quality-engineering-qe)
9. [How-To Guides](#how-to-guides)
10. [Troubleshooting](#troubleshooting)
11. [Reference Materials](#reference-materials)
12. [Glossary](#glossary)

---

## Team Structure

### Leadership & Points of Contact

| Role | Name | Contact |
|------|------|---------|
| VP of Sustaining Engineering | James Moran | - |
| Product Manager | Grant Herbon | - |
| Program Manager | Purcella Smith | - |
| Senior Data Analyst | Sneja Snah | - |
| RHEL SE Lead | Renu Jhamtani | @Renu Jhamtani |
| OCP SE Lead | Stephen de Courcy | @Stephen de Courcy |

### Team Organization

```
Sustaining Engineering
├── RHEL Sustaining Engineering
│   ├── SE Kernel
│   │   ├── Kernel Dev
│   │   ├── Kernel QE
│   │   └── SST Teams (Storage, Networking, Virtualization, etc.)
│   └── SE Userspace
│       ├── SSG Core Services
│       ├── SSG Display
│       ├── SSG Filesystems+Storage
│       ├── SSG IDM
│       ├── SSG Networking
│       ├── SSG Platform Tools
│       ├── SSG Security
│       └── SSG Virtualization
│
├── OpenShift Sustaining Engineering
│   ├── ART (Automated Release Tooling)
│   ├── QE (Quality Engineering)
│   ├── CNV (Container Native Virtualization)
│   ├── Storage
│   └── Networking
│
├── OpenJDK Sustaining
│
├── Satellite Sustaining
│
└── RHOAI Sustaining
```

---

## Communication Channels

### Mailing Lists

| List | Purpose | Link |
|------|---------|------|
| `sustaining-engineering-forum@redhat.com` | Department members + external stakeholders | [Google Group](https://groups.google.com/a/redhat.com/g/sustaining-engineering-forum) |
| `sustaining-engineering@redhat.com` | All SE department (reports to Jim Moran) | [Google Group](https://groups.google.com/a/redhat.com/g/sustaining-engineering) |
| `sustaining-engineering-rhel@redhat.com` | RHEL SE team | [Google Group](https://groups.google.com/a/redhat.com/g/sustaining-engineering-rhel) |
| `sustaining-engineering-ocp@redhat.com` | OCP SE team | - |

### Slack Channels

#### General SE
- `#forum-sustaining-engineering` - Main forum channel

#### RHEL SE
- `#team-kernel-se` - Kernel SE team
- `#se-userspace` - Userspace SE team

#### OCP SE
- `#sustaining-engineering-ocp-internal` - Private channel for OCP SE engineers
- `#sustaining-engineering-ocp` - Public channel
- `#sustaining-ocp-release` - ART OCP SE Engineers
- `#sustaining-art-onboarding` - ART and OCP Engineers
- `#ocp-sustaining-cnv` - OCP CNV SE Engineers
- `#sustaining-ocp-storage` - OCP Storage SE Engineers
- `#sustaining-engineering-ocp-qe` - OCP QE SE Engineers

#### External Teams
- `#forum-ocp-art` - Build questions
- `#forum-ocp-release` - Release questions
- `#forum-ocp-release-oversight` - TRT Team
- `#forum-ocp-testplatform` - OCP Platform CI team

### Calendars

- **Sustaining Engineering Calendar** - Add via Google Calendar search for "SustainingEngineering"

---

## Onboarding

### General Onboarding Checklist

- [ ] Request access to relevant mailing lists
- [ ] Join Slack channels
- [ ] Set up Kerberos authentication (`kinit`)
- [ ] Create/link GitHub account on Rover profile
- [ ] Request access to OpenShift GitHub Organization
- [ ] Create Quay.io account with Red Hat email
- [ ] Set up VPN access
- [ ] Complete Brew/Errata tool access requests

### GitHub Access Setup

1. Create an account on [github.com](https://github.com) if not existing
2. Add GitHub link to your [Rover](https://rover.redhat.com) profile (Professional Social Media section)
3. Connect to VPN
4. Request access via [Dev Services](https://devservices.redhat.com) - "Request access to Github organizations"
   - Requestor team: `OCP Sustaining Engineering` (or your team)
   - Requesting access to: `openshift`
5. Verify access at GitHub → Your Organizations

### Product-Specific Onboarding

- **RHEL Kernel SE**: See [SE Kernel Onboarding](#se-kernel-onboarding)
- **RHEL Userspace SE**: See [Userspace Onboarding Guide](#userspace-onboarding)
- **OCP SE**: See [OCP Onboarding](#ocp-onboarding)
- **OpenJDK**: See [OpenJDK Getting Started](#openjdk-getting-started)

---

## Product Areas

### RHEL Sustaining Engineering

Responsible for handling defects/bugs and CVEs in extended life streams/offerings of RHEL.

#### Supported Versions
See [RHEL Long Life Offerings Single Source of Truth](#reference-materials) and [Product Pages](#reference-materials)

#### Key Resources
- [RHEL Life Cycle](https://access.redhat.com/support/policy/updates/errata)
- [RHEL Top Support Policies](https://access.redhat.com/articles/rhel-top-support-policies)
- [RHEL EUS Overview](https://access.redhat.com/support/policy/updates/errata#Extended_Update_Support)

### OpenShift Sustaining Engineering

Supporting OCP EUS/ELS versions with CVE workload and maintenance of selected components.

#### Supported Versions
- OCP 4.12 EUS
- OCP 4.14 EUS
- OCP 4.16 EUS
- Additional versions as released

#### Responsibilities
- End-to-end delivery of z-stream releases
- Backporting CVEs and bug fixes
- Testing, Patch Manager/TRT, Build & Release (ART)

### OpenJDK Sustaining

Supporting OpenJDK 11 ELS and related container images.

#### Key Areas
- Building and testing OpenJDK
- CPU errata handling
- Container image updates
- tzdata testing

---

## Tools & Infrastructure

### Jenkins

**Main URL**: [ART Jenkins](https://art-jenkins.apps.prod-stable-spoke1-dc-iad2.itup.redhat.com/job/aos-cd-builds/)

#### Key Jobs
| Job | Purpose |
|-----|---------|
| `build/gen-assembly` | Generate assembly definition |
| `build/build-sync` | Sync builds to image streams |
| `build/build-sync-konflux` | Konflux build sync |
| `build/prepare-release` | Prepare release advisories |
| `build/prepare-release-konflux` | Konflux release preparation |
| `build/promote-assembly` | Promote release to production |
| `build/drop_advisories` | Drop advisories |

### Konflux

**Konflux UI**: [https://konflux-ui.apps.kflux-ocp-p01.7ayg.p1.openshiftapps.com/](https://konflux-ui.apps.kflux-ocp-p01.7ayg.p1.openshiftapps.com/)

**Cluster Console**: [https://console-openshift-console.apps.kflux-ocp-p01.7ayg.p1.openshiftapps.com/](https://console-openshift-console.apps.kflux-ocp-p01.7ayg.p1.openshiftapps.com/)

#### Key Resources
- [Konflux Release Data (GitLab)](https://gitlab.cee.redhat.com/releng/konflux-release-data)
- [OCP Shipment Data (GitLab)](https://gitlab.cee.redhat.com/hybrid-platforms/art/ocp-shipment-data)
- [Shipment CI (GitLab)](https://gitlab.cee.redhat.com/hybrid-platforms/art/shipment-ci)

### Release Controller

| Architecture | URL |
|--------------|-----|
| AMD64 (Default) | [amd64.ocp.releases.ci.openshift.org](https://amd64.ocp.releases.ci.openshift.org/) |
| ARM64 | [arm64.ocp.releases.ci.openshift.org](https://arm64.ocp.releases.ci.openshift.org) |
| S390X | [s390x.ocp.releases.ci.openshift.org](https://s390x.ocp.releases.ci.openshift.org) |
| PPC64LE | [ppc64le.ocp.releases.ci.openshift.org](https://ppc64le.ocp.releases.ci.openshift.org) |

### ART Tools (Elliott, Doozer)

#### Installation
```bash
git clone git@github.com:openshift-eng/art-tools.git
cd art-tools
make venv
source .venv/bin/activate
```

#### Common Elliott Commands
```bash
# Verify conforma
elliott -g openshift-4.19 --data-path=https://github.com/openshift-eng/ocp-build-data \
  verify-conforma --pullspec registry.ci.openshift.org/ocp/release:4.19.0-0.nightly-YYYY-MM-DD-HHMMSS

# Pin builds
elliott -g openshift-4.14 --assembly 4.14.61 --build-system brew \
  pin-builds runc-1.2.9-1.rhaos4.16.el9 runc-1.2.9-1.rhaos4.16.el8 --why "pin rpm"

# Attach CVE flaws
elliott --group=openshift-4.15 --assembly=4.15.57 --build-system=konflux \
  attach-cve-flaws --use-default-advisory=image --reconcile --output=yaml
```

### Errata Tool

**URL**: [https://errata.devel.redhat.com/](https://errata.devel.redhat.com/)

### Brew

**URL**: [https://brewweb.engineering.redhat.com/brew/](https://brewweb.engineering.redhat.com/brew/)

### Beaker

Used for QE testing on RHEL systems.

### Testing Farm

Used for automated testing workflows.

---

## Workflows & Processes

### Jira Ticket Processing

1. **Triage**: Review incoming tickets for severity and priority
2. **Assignment**: Route to appropriate team/engineer
3. **Analysis**: Investigate the issue
4. **Fix Development**: Develop and test the fix
5. **Backporting**: Apply fix to relevant streams
6. **Testing**: QE verification
7. **Release**: Include in z-stream release

### Backporting Workflow

#### Overview

Backporting is the process of applying fixes from a newer version (Y-stream) to an older, supported version (Z-stream). This workflow ensures that security fixes and critical bug patches reach customers using extended support releases.

#### Prerequisites

1. **Repository Setup**
   - Clone the target kernel/component repository
   - Create a personal fork for your workspace
   - Add your fork as a remote:
   ```bash
   git remote add fork git@gitlab.com:<your-username>/<repo>.git
   ```

2. **Required Access**
   - GitLab account linked to Rover profile
   - Brew/Errata tool permissions
   - Kerberos authentication active

#### Step 1: Jira Ticket Preparation

1. **Assign yourself** to the Z-stream issue
2. **Set yourself as the Developer** on the issue
3. **Find a QA colleague** to handle verification
4. **Update AssignedTeam** to your team (e.g., "rhel-se-kernel")
5. **Set issue status** to "In Progress"
6. **Handle CVE twins**: For kernel CVEs, also update the corresponding kernel-rt issue

> **Important**: Do not start backporting until the Y-stream fix is merged. Verify by checking:
> - The Y-stream issue has an MR with "readyForMerge" label
> - The MR content has been approved

#### Step 2: Identify the Upstream Fix

1. Locate the Y-stream issue via the CVE label or search tools:
   ```bash
   # Example: Find Y-stream issues for a CVE
   git kmt-ticket-cache -f RHEL-12345
   ```

2. Find the Y-stream MR under the issue's "Development" tab

3. Review the commits that need to be backported

4. Assess compatibility:
   - Are the same code paths present in the target branch?
   - Are there dependency commits that must also be included?
   - Will manual conflict resolution be needed?

#### Step 3: Perform the Backport

**Using KMT (Kernel Maintenance Tool) for Kernel:**

```bash
# Checkout target branch
git checkout <target-branch>   # e.g., 8.6

# Clear and update caches
git kmt-clear-caches
git kmt-update-caches
git kmt-ticket-cache -f RHEL-12345

# Generate patchlist
git kmt-generate RHEL-12345 > patchlist

# Create working branch
git checkout -b <branch>-<issue-id>   # e.g., 8.6-12345

# Apply patches with automatic metadata amendment
git kmt-apply -a patchlist
```

**Manual Cherry-Pick Method:**

```bash
# Create working branch
git checkout -b <branch>-<issue-id>

# Cherry-pick the commit(s)
git cherry-pick -x <upstream-commit-sha>

# If conflicts occur, resolve them and continue
git cherry-pick --continue
```

**Verify Commit Metadata** (required fields):
- `JIRA:` URL to the Z-stream issue
- `Y-JIRA:` URL to the Y-stream issue
- `CVE:` CVE identifier (if applicable)
- `Y-Commit:` ID of the backported commit
- `Signed-off-by:` Your name and email

#### Step 4: Handle Merge Conflicts

If `git kmt-apply` fails due to conflicts:

```bash
# Apply patchlist (will stop at conflict)
git kmt-apply patchlist

# Manually cherry-pick the conflicting commit
git cherry-pick -s <commit-sha>

# Resolve conflicts using your preferred tool (meld, kdiff3, etc.)
# Then continue the cherry-pick
git cherry-pick --continue

# Save the resolved patch
mkdir -p refreshed/
git format-patch -1 --stdout HEAD > refreshed/<commit-sha>

# Reset and reapply with the refreshed patch
git reset --hard origin/<branch>
git kmt-apply -a patchlist
```

#### Step 5: Create Merge Request

**Using KMT:**
```bash
git kmt-mr-create -D fork
```

**MR Description Format:**
```
JIRA: <URL to Z-stream issue>
CVE: <CVE-ID>

* List of commits being backported:
- <subsystem>: <commit message> (*author*) [*z-issue* *y-issue*] {*cve*}

Y-Commit: <upstream commit ID>
Signed-off-by: <Your Name> <your.email@redhat.com>
```

**To update an existing MR:**
```bash
git kmt-mr-create fork --update <MR-id> -f
```

#### Step 6: MR Review and Labels

The MR goes through automated checks indicated by labels:

| Label State | Meaning |
|-------------|---------|
| **Red** | Blocking issue, not ready |
| **Yellow** | In progress, awaiting action |
| **Blue** | Requirement satisfied |
| **Green** | Fully ready for merge |

**Key Labels to Monitor:**
- `CKI::*` - CI build and test status
- `Acks::*::NeedsReview` - Requires approval from subsystem maintainers
- `readyForQA` - Development complete, ready for pre-verification
- `readyForMerge` - All checks passed, ready for integration

**Developer Actions:**
1. Keep MR in **Draft** mode until all initial labels are blue
2. Mark as **Ready** once CKI passes
3. Chase approvals from required reviewers (Y-stream author, SE peer, content reviewer)
4. Monitor CKI pipeline results

#### Step 7: QA Pre-Verification

Once `readyForQA` label is applied:

1. QE receives notification via "Preliminary Testing = Requested" on the Jira
2. QE uses the CKI build artifacts to verify the fix
3. QE sets "Preliminary Testing = Pass" on the ticket
4. MR automatically receives `readyForMerge` label

> **CVE Note**: For CVE fixes, both the stock kernel and kernel-rt Jira tickets must be pre-verified before `readyForMerge` is applied.

#### Step 8: Integration and Build

**Maintainer Process:**
1. Maintainers collect all `readyForMerge` MRs weekly
2. A "Build MR" is created combining all ready changes
3. The Build MR runs through CKI to verify combined compatibility
4. Upon success, changes are merged to the target branch
5. Weekly builds are triggered

#### Step 9: Track Through Release

1. Monitor the build through Errata Tool
2. Verify QE completes release testing
3. Track advisory progress to `REL_PREP` state
4. Confirm release via Release Controller

#### Product-Specific Notes

**Kernel Backports:**
- Use KMT tools for efficient workflow
- Handle stock kernel and RT kernel together
- ZStreamBuild label identifies weekly build MRs

**OpenJDK Backports:**
- Refer to internal GitLab wiki for JDK-specific procedures
- CPU (Critical Patch Update) releases follow quarterly schedules

**OCP/OpenShift Backports:**
- Work through the ART (Automated Release Tooling) pipeline
- Use `releases.yml` for assembly configuration
- Monitor via Release Controller dashboards

**IDM Components (389-ds-base, sssd, etc.):**
- Use upstream → downstream → dist-git workflow
- Module builds may require additional steps
- Coordinate with Product QE for regression testing

#### Resources

- **KMT User Guide**: [KMT Documentation](https://redhat.gitlab.io/rhel/sst/kernel-maintainers/kmt/kmt-docs/userguide.html)
- **Kernel Maintainers Docs**: [Z-Stream Workflow](https://redhat.gitlab.io/rhel/sst/kernel-maintainers/docs/kernel-maintainers-docs/zstream_workflow/introduction.html)
- **Internal Sessions**: Recorded training sessions available on internal wiki

### Z-Stream Release Process

See [Release Process](#release-process) for detailed steps.

---

## Release Process

### OCP Z-Stream Release (Konflux)

#### Prerequisites
- Green nightly in Release Controller
- Access to Jenkins, GitHub, GitLab
- Kerberos authentication active

#### Step 1: Verify Conforma (Optional but Recommended)
```bash
elliott -g openshift-4.19 --data-path=https://github.com/openshift-eng/ocp-build-data \
  verify-conforma --pullspec registry.ci.openshift.org/ocp/release:4.19.0-0.nightly-YYYY-MM-DD-HHMMSS
```

#### Step 2: Gen Assembly
1. Go to [Jenkins gen-assembly](https://art-jenkins.apps.prod-stable-spoke1-dc-iad2.itup.redhat.com/job/aos-cd-builds/job/build%252Fgen-assembly/)
2. Parameters:
   - `BUILD_VERSION`: e.g., `4.19`
   - `ASSEMBLY_NAME`: e.g., `4.19.9`
   - `BUILD_SYSTEM`: `konflux`
   - `TRIGGER_BUILD_SYNC`: `true`
   - `DATE`: Release date (YYYY-Mon-dd)

#### Step 3: Build Sync
- Automatically triggered by Gen Assembly
- Or run manually at [build-sync-konflux](https://art-jenkins.apps.prod-stable-spoke1-dc-iad2.itup.redhat.com/job/aos-cd-builds/job/build%252Fbuild-sync-konflux/)

#### Step 4: Merge GitHub PR
1. Find PR at [ocp-build-data PRs](https://github.com/openshift-eng/ocp-build-data/pulls)
2. Verify changes to `releases.yml`
3. Add labels: `/lgtm` and `/approve`
4. Wait for merge

#### Step 5: Prepare Release
1. Go to [prepare-release-konflux](https://art-jenkins.apps.prod-stable-spoke1-dc-iad2.itup.redhat.com/job/aos-cd-builds/job/build%252Fprepare-release-konflux/)
2. Parameters:
   - `BUILD_VERSION`: e.g., `4.19`
   - `ASSEMBLY`: e.g., `4.19.9`

#### Step 6: Verify Stage Pipeline
1. Find GitLab MR at [ocp-shipment-data MRs](https://gitlab.cee.redhat.com/hybrid-platforms/art/ocp-shipment-data/-/merge_requests)
2. Check Pipeline tab → Latest pipeline
3. Verify `image.create` and `image.watch` are **GREEN**

#### Step 7: Promote Assembly
1. Go to [promote-assembly](https://art-jenkins.apps.prod-stable-spoke1-dc-iad2.itup.redhat.com/job/aos-cd-builds/job/build%252Fpromote-assembly/)
2. Parameters:
   - `VERSION`: e.g., `4.19`
   - `ASSEMBLY`: e.g., `4.19.9`
3. Verify release appears in Release Controller

#### Step 8: Production Push (Release Day)
1. Verify all stage pipelines are green
2. Get approvals from ART, ERT, and Docs teams
3. Trigger prod push from GitLab MR pipeline

---

## How-To Guides

### How to Drop an Advisory
Use the [drop_advisory job](https://art-jenkins.apps.prod-stable-spoke1-dc-iad2.itup.redhat.com/job/aos-cd-builds/job/build%252Fdrop_advisory/) with:
- VERSION: e.g., `4.14`
- ADVISORIES: comma-separated list

### How to Pin a Build
Add to `releases.yml`:
```yaml
members:
  images:
    - distgit_key: component-name
      why: Pin because <reason>
      metadata:
        is:
          nvr: component-container-v4.16.0-YYYYMMDDHHMMSS.p0.gXXXXXXX.assembly.stream.el9
```

### How to Paint a Release Green
1. Go to [accept-release job](https://art-jenkins.apps.prod-stable-spoke1-dc-iad2.itup.redhat.com/job/aos-cd-builds/job/build%252Faccept-release/)
2. Provide release version and parameters
3. Reference: [ART Docs - Paint Release](https://art-docs.engineering.redhat.com/sop/paint/)

### How to Use a Blue Nightly
In Gen Assembly, select `ALLOW_PENDING` checkbox to use pending (blue) nightlies.

### How to Exclude a Jira from Release
Add to `releases.yml`:
```yaml
issues:
  exclude:
    - id: OCPBUGS-XXXXX
```

### How to Include a Jira in Release
Add to `releases.yml`:
```yaml
issues:
  include:
    - id: OCPBUGS-XXXXX
```

---

## Quality Engineering (QE)

### QE Team Structure

QE is integral to the Sustaining Engineering workflow, ensuring releases meet quality standards before shipping.

#### OCP QE Contacts
- **Slack**: `#sustaining-engineering-ocp-qe`
- **Dashboard**: [OCP SE QE Dashboard](https://redhat.atlassian.net)

### QE Workflow Overview

```
CVE/Bug Assigned → Development Fix → Build Available → QE Verification → Release Testing → Ship
```

### Testing Process

#### 1. CVE/Bug Verification
- QE Contact receives notification when fix is available in 'Accepted' nightly build
- Verify the fix addresses the reported issue
- Document verification steps and results in Jira

#### 2. Release Testing Activities
- **Sustaining QE Release Lead** performs all errata release testing activities
- Push errata to `REL_PREP` once all tasks complete
- Coordinate with ART for stable build creation

### Testing Tools & Infrastructure

#### Beaker
- **Purpose**: Inventory of bare-metal servers for testing
- **Usage**: Use reservation system to request servers
- **Documentation**: [Beaker Overview](https://beaker-project.org/)

#### Testing Farm
- **URL**: [Testing Farm Dashboard](https://api.testing-farm.io/v0.1/login/redhat)
- **CLI Installation**:
```bash
sudo dnf copr enable @testing-farm/stable
sudo dnf install testing-farm
testing-farm version
```

- **API Token**: Generate at Testing Farm dashboard after SSO login

- **Example Test Request**:
```bash
export TESTING_FARM_API_TOKEN=<your-token>
testing-farm request \
  --compose RHEL-9.0.0-Nightly \
  --git-url "https://gitlab.cee.redhat.com/toolchain-qe/tests/golang.git" \
  --plan /plans/ci \
  --redhat-brew-build golang-1.20.12-14.el9 \
  --redhat-brew-build delve-1.20.2-1.el9 \
  --context distro=rhel-9.0 \
  --context go_version=1.20 \
  --arch=x86_64,aarch64,ppc64le,s390x
```

#### TPS (Test Package Signing)
- Used for verifying RPM packages in errata
- Required for RHSA (Security Advisory) releases
- Run TPS tests before pushing to CDN

#### Report Portal
- **Purpose**: Test results aggregation and analysis
- **Automated filtering**: LEVEL0, Installer, Upgrade tests
- **Failure notification**: Critical failures flagged automatically

### Test Environments

#### Cluster Bot
- **Purpose**: Spin up short-lived temporary clusters
- **Access**: Direct message the `Cluster Bot` app in Slack
- **Commands**:
  - `help` - List available commands
  - `launch <version> <arch>` - Create cluster (e.g., `launch 4.18.0-0.nightly amd64`)
  - `list` - Show available clusters
  - `test e2e-image-ecosystem <build>/<pr>` - Run tests

- **Limitations**:
  - Max ~80 clusters available (first come, first served)
  - Cluster lifetime ~180 minutes
  - Specify architecture to avoid multi-arch provider selection

#### Resource Hub
- Good for short-lived testing
- Quick setup with minimal steps

#### PSI OpenStack
- **URL**: [cloud.psi.redhat.com](https://cloud.psi.redhat.com/dashboard/project/instances/)
- **Project**: `ocp-sustaining`
- **Authentication**: SSO or Keystone (KerbID + pin+token)

### Running Tests

#### OpenShift Origin Tests
```bash
# Clone and build
git clone https://github.com/openshift/origin
cd origin
make WHAT=cmd/openshift-tests

# Dry run to list tests
./openshift-tests run openshift/image-ecosystem --dry-run

# Run specific tests
./openshift-tests run openshift/image-ecosystem --dry-run | grep -F '[Feature:ImageEcosystem][ruby]' | ./openshift-tests run -f -
```

#### CI Testing via PR
- Use `/test <test-name>` comment in GitHub PR
- Use `/retest` to retry failed tests
- Use `/override <test-name>` for test override (requires approval)

### QE Verification for Releases

#### Z-Stream Release QE Checklist

- [ ] Verify nightly build contains the fix
- [ ] Run component-specific tests
- [ ] Verify CVE/bug is resolved
- [ ] Update Jira with verification results
- [ ] Coordinate with release lead for errata testing

#### Errata Testing Tasks (RHBA/RHSA)

1. **Details Verification**
   - Correct package owner, QA owner, doc reviewer
   - Populate bugs/CVEs

2. **CDN Repos Setup**
   - Set CDN repos for advisory metadata

3. **Brew Builds Verification**
   - Cross-verify with pipeline logs

4. **Security Alerts Check**
   - Verify no security alerts

5. **Move to QE State**
   - Change advisory state to QE

6. **TPS Tests** (for RHSA)
   - Run and verify TPS tests

7. **Documentation Approval**
   - Request doc approval

8. **CDN Staging Push**
   - Push to staging and verify

9. **Production Push**
   - Move to REL_PREP state

### Cloud Accounts for Testing

| Provider | Account | Purpose |
|----------|---------|---------|
| AWS | pge-cloud-aws-xe-se-ocp-412-test | Auto-release pipeline 4.12/4.13 |
| AWS | pge-cloud-aws-xe-se-ocp-412-preprod | Manual testing 4.12.z |
| Azure | OCP Sustaining 4.12 | Auto-release pipeline |
| Azure | OCP Sustaining 4.12-2 | Manual testing |
| GCP | it-cloud-gcp-osus-dev-412test | Auto-release pipeline |
| GCP | it-cloud-gcp-osus-dev-412ci | Manual testing |

### QE Tools Repository

- **Report Portal Alert Tool**: [GitLab Repository](https://gitlab.cee.redhat.com/sustaining-engineering/ocp-sustaining-tools/ocp-se-qe-tools/reportportal_alert)
- **Jira Integrator**: [GitLab Repository](https://gitlab.cee.redhat.com/sustaining-engineering/ocp-sustaining-tools/ocp-se-qe-tools/ocpse-jira-integrator)

### AI-Assisted Testing Tools

#### Claude Code

Claude Code is a CLI tool that uses the Claude AI model for coding directly in your terminal. It can help build features from descriptions, debug issues, navigate codebases, and automate tasks.

**Prerequisites:**
Before installing, review and confirm you have read:
- Guidelines for Responsible Use of AI Code Assistants
- Legal guidelines for using code assistant tools
- Claude Code Best Practices for Agentic Coding
- Anthropic's Usage Policy
- Red Hat Policy on the Use of AI Technology
- Guidelines on Use of AI Generated Content

**Installation (Fedora/MacOS):**

1. **Install Google Cloud CLI** following the [Google Cloud Guide](https://cloud.google.com/sdk/docs/install)

2. **Initialize gcloud** and sign in with your Red Hat email:
   ```bash
   gcloud init
   ```
   - Select option to sign in with Red Hat email
   - When prompted for GCP project, select [1]

3. **Find your project ID** from the [GCP Projects Spreadsheet](https://docs.google.com/spreadsheets/d/1qWoCx3i5jZ-t6BUD-2AIdutk9sMmkytoXqjBXh2oi4U/edit?gid=0#gid=0)
   - Projects align with organizational reporting lines
   - Find the project matching your closest upline manager

4. **Set up authentication:**
   ```bash
   gcloud auth application-default login
   gcloud auth application-default set-quota-project cloudability-it-gemini
   ```

5. **Set environment variables** (replace `$GCP_PROJECT_ID` with your team's project ID):

   **Linux (bash):**
   ```bash
   echo 'export CLAUDE_CODE_USE_VERTEX=1' >> ~/.bashrc
   echo 'export CLOUD_ML_REGION=us-east5' >> ~/.bashrc
   echo 'export ANTHROPIC_VERTEX_PROJECT_ID=$GCP_PROJECT_ID' >> ~/.bashrc
   source ~/.bashrc
   ```

   **MacOS (zsh):**
   ```bash
   echo 'export CLAUDE_CODE_USE_VERTEX=1' >> ~/.zshrc
   echo 'export CLOUD_ML_REGION=us-east5' >> ~/.zshrc
   echo 'export ANTHROPIC_VERTEX_PROJECT_ID=$GCP_PROJECT_ID' >> ~/.zshrc
   source ~/.zshrc
   ```

6. **Install Claude Code:**

   **Mac/Linux/WSL:**
   ```bash
   curl -fsSL https://claude.ai/install.sh -o claude-install.sh
   chmod +x claude-install.sh
   ./claude-install.sh
   ```

   **Windows (PowerShell):**
   ```powershell
   irm https://claude.ai/install.ps1 | Out-File claude-install.ps1
   .\claude-install.ps1
   ```

7. **Launch Claude Code:**
   ```bash
   cd <your-working-directory>
   claude
   ```

**Verification:**
- Run `/status` to verify GCP project and provider is "Google Vertex AI"
- Run `/init` to generate a CLAUDE.md file with codebase documentation

**Getting Help:** Slack channel `#help-rh-code-assist`

#### Claude for Test Failure Analysis (TFA)

Configure Claude to analyze CI/CD test failures with Jira integration.

**Prerequisites:**
1. **Install omc (OpenShift Must-Gather Client):**
   ```bash
   # Install from https://github.com/gmeghnag/omc/
   # Verify installation
   omc
   # Default install location: $HOME/go/bin - add to $PATH if needed
   ```

2. **Install uv** (Python package manager):
   ```bash
   pip install uv
   ```

**Configuration:**

1. **Generate Jira API Token:**
   - Go to your Jira profile
   - Generate an access token

2. **Set environment variables:**

   **Linux:**
   ```bash
   echo 'export JIRA_API_TOKEN=<your-token>' >> ~/.bashrc
   echo 'export JIRA_USERNAME=<your-email>' >> ~/.bashrc
   source ~/.bashrc
   ```

   **MacOS:**
   ```bash
   echo 'export JIRA_API_TOKEN=<your-token>' >> ~/.zshrc
   echo 'export JIRA_USERNAME=<your-email>' >> ~/.zshrc
   source ~/.zshrc
   ```

3. **Configure Atlassian MCP for Claude:**

   Edit `~/.claude.json` to add the Atlassian MCP configuration:
   ```json
   {
     "mcpServers": {
       "mcp-atlassian": {
         "command": "uvx",
         "args": ["mcp-atlassian"],
         "env": {
           "JIRA_URL": "https://redhat.atlassian.net"
         }
       }
     }
   }
   ```

4. **Verify installation:**
   - Launch Claude: `claude`
   - Run `/mcp` to verify the Atlassian MCP is configured

**Usage:**
```bash
# Analyze CI job failures
/ci:analyze-failures <job-url>
```

**Resources:**
- [omc GitHub Repository](https://github.com/gmeghnag/omc/)
- [mcp-atlassian GitHub Repository](https://github.com/sooperset/mcp-atlassian)

---

## Troubleshooting

### Common Release Errors

#### "No attached builds found in advisories for tracker bugs"
**Cause**: Bug references a component not in the release
**Solution**: 
1. Check if pscomponent label is correct
2. Either exclude the bug or add the correct `art:pscomponent` label
3. Update `releases.yml` and rerun prepare-release

#### "ValueError: Preparing a release from a stream assembly is no longer supported"
**Cause**: PR from previous step not merged
**Solution**: Merge the PR and rerun the job

#### "Image stream not found"
**Cause**: Build sync didn't complete properly
**Solution**: Rerun build-sync with appropriate parameters

#### Advisory in NEW_FILES state
**Cause**: Advisory has no builds attached
**Solution**: Use drop_advisory job to remove it

### Konflux-Specific Issues

#### FBC Pipeline Fails on Friday
Request exception via [konflux-release-data MR](https://gitlab.cee.redhat.com/releng/konflux-release-data) to update `effectiveUntil` date.

#### OOM-killed Tasks
Increase memory in ReleasePlanAdmission YAML files.

---

## Reference Materials

### Key URLs

| Resource | URL |
|----------|-----|
| Source Page | [source.redhat.com/groups/public/se](https://source.redhat.com/groups/public/se) |
| ART Docs | [art-docs.engineering.redhat.com](https://art-docs.engineering.redhat.com) |
| Konflux Docs | [konflux.pages.redhat.com/docs](https://konflux.pages.redhat.com/docs/users/getting-started.html) |
| Release Schedule | [Smartsheet Calendar](https://app.smartsheet.com/b/publish?EQBCT=970c5ff6c67a4ca7a153e3a6ef993e77) |

### GitHub Repositories

| Repository | Purpose |
|------------|---------|
| [ocp-build-data](https://github.com/openshift-eng/ocp-build-data) | Release definitions and assembly configs |
| [art-tools](https://github.com/openshift-eng/art-tools) | Elliott, Doozer, and other ART tools |
| [aos-cd-jobs](https://github.com/openshift-eng/aos-cd-jobs) | Jenkins job definitions |

### Jira Dashboards

- [Non-EUS CVE Dashboard](https://redhat.atlassian.net) - SE/PE Dashboard Overview
- [EUS CVE Dashboard](https://redhat.atlassian.net) - SE/PE Dashboard Overview
- [SE OCP Operational Dashboard](https://redhat.atlassian.net)
- [OCP SE Activity Dashboard](https://redhat.atlassian.net)

---

## Glossary

| Term | Definition |
|------|------------|
| **ART** | Automated Release Tooling - Tools and processes for building and releasing OCP |
| **CVE** | Common Vulnerabilities and Exposures |
| **ELS** | Extended Lifecycle Support |
| **EUS** | Extended Update Support |
| **FBC** | File-Based Catalog |
| **Konflux** | Red Hat's build and release platform |
| **NVR** | Name-Version-Release (package identifier) |
| **SE** | Sustaining Engineering |
| **SST** | Subsystem Team |
| **TRT** | Technical Release Team |
| **Z-stream** | Minor version update release (e.g., 4.16.z) |

---

## Document Information

| Field | Value |
|-------|-------|
| **Last Updated** | March 2026 |
| **Maintainers** | Sustaining Engineering Team |
| **Confluence Source** | [Sustaining Engineering](https://redhat.atlassian.net/wiki/x/AoB9F) |

---

*This playbook is a living document. Please contribute updates and corrections via the standard review process.*
