Terraform Enterprise (TFE) Glossary

## API

"Application Programming Interface". Any interface designed to allow programatic manipulation of some kind of software system. For most software developers today, the most common kinds of APIs are based on HTTP requests.

Terraform relies on cloud service provider APIs to manage resources; each service's Terraform provider is responsible for mapping Terraform's resource model to the series of actual API calls necessary to create, check, modify, or delete a real infrastructure resource in that cloud service.

Terraform Enterprise also offers its own API, for managing resources like team membership, policies, and workspaces. That API, in turn, is used by the `tfe` Terraform provider, so you can use Terraform to manage the system that runs Terraform for you.

- [TFE docs: API](/docs/enterprise/api/index.html)
- [Terraform providers: `tfe`](/docs/providers/tfe/index.html)

## Apply (noun)

One of the stages of a [run][], in which changes are made to real infrastructure resources in order to make them match their desired state. The counterpart of a [plan][].

In Terraform's CLI, applies are performed with the `terraform apply` command. TFE runs `terraform apply` using a plan file (2) as its input.

- [Terraform docs: The `terraform apply` command](/docs/commands/apply.html)
- [TFE docs: About Runs](/docs/enterprise/run/index.html)

## Apply (verb)

To make changes to real infrastructure in order to make it match the desired state (as specified by a Terraform config and set of variables).

In conversation, it's common to refer to "applying a plan" (usually in the context of TFE's workflow) or "applying a configuration" (usually in the context of the Terraform CLI workflow).

- [Terraform docs: The `terraform apply` command](/docs/commands/apply.html)
- [TFE docs: About Runs](/docs/enterprise/run/index.html)

## Backend

The part of Terraform's core that determine how Terraform stores state and performs operations (like plan, apply, import, etc.). Backends are not plugins (and there are no third-party backends), but Terraform has multiple backends to choose from, which can be configured in a variety of ways.

In a general computer science sense, a backend is any lower-level implementation that enables a higher-level feature. But in the context of Terraform, "backend" always means the built-in code that handles state and operations.

- [Terraform docs: Backends](/docs/backends/index.html)

## Blob Storage

An API service for storing and retrieving arbitrary chunks of data using opaque addresses.

## Branch

In some version control systems: a semi-independent history of changes to content in a repository. A branch generally shares some history with other branches in the same repository, but eventually diverges to include changes that aren't yet present elsewhere.

A repository usually has a default branch (whose name, in Git, defaults to `master`), which successful changes are eventually merged into. Most modern development workflows also include topic branches (where a specific set of changes is explored, iterated on, and verified), and some workflows include long-lived branches other than the default branch (usually for maintaining older but still supported versions of software).

## CLI

Command-line interface. The `terraform` tool and its subcommands use a CLI to accept instructions and return text output.

We often use "Terraform CLI" to refer to the core open source Terraform binary when we need to distinguish it from other parts of the Terraform ecosystem (like Terraform Enterprise or the Terraform GitHub Actions).

- [Wikipedia: Command-line Interface](https://en.wikipedia.org/wiki/Command-line_interface)
- [Terraform docs: Commands (CLI)](/docs/commands/index.html)

## Commit

In a version control system: A coherent set of changes saved to a repository's version history.

In Git, commits act like a complete snapshot of the contents of a repo, on a specific branch (or group of branches with shared history) and at a specific moment in time. Each commit also records the identity of its parent(s), which enables viewing the entire history of the repo up to any specific moment. Additionally, comparing a commit to its parent(s) can reveal the exact changes introduced by that commit; if those changes are applied as a diff, they can be added to a different branch in the repo without merging in the entire history of the commit in question.

## (Terraform) Configuration

Also "config".

Code written in Terraform's configuration language that declaratively describes the desired state of your infrastructure. A complete config consists of a root module, which can optionally call any number of child modules.

- [Terraform docs: Configuration Language](/docs/configuration/index.html)
- [Introduction to Terraform](/intro/index.html)

## Configuration Version

-> Terraform Enterprise

Also "config version".

The contents of a Terraform config at a specific moment in time. This concept only applies to Terraform Enterprise, since the Terraform CLI doesn't have any visibility into repeated runs over a period of time.

Every stage of a given run uses one specific configuration version.

Config versions can be automatically imported when new commits are merged to a workspace's repo, uploaded via the API, or uploaded by running `terraform plan` or `terraform apply` as a remote operation. Adding a new config version is sometimes called "ingressing."

## Fork

Also "forked repository" or "forked repo".

A VCS repository that was created by copying content and history from another repository.

Different VCS providers handle forks differently, but a fork is usually owned by a different person or organization than the original repo, and a fork usually does not inherit all of the original repo's access permissions.

Terraform Enterprise makes extensive use of VCS repos, and assumes that forks of a trusted repo are not necessarily trusted. As such, TFE avoids evaluating any code from external forks, which prevents TFE from running speculative plans for pull requests from forks.

## Git

A distributed version control system for tracking changes in source code during software development. It is designed for coordinating work among programmers, but it can be used to track changes in any set of files.

- [Wikipedia: Git](https://en.wikipedia.org/wiki/Git)

## HCL

HashiCorp Configuration Language. The structured configuration syntax that serves as the basis for Terraform's configuration language, as well as the configuration layer for several other HashiCorp products.

HCL establishes the syntax Terraform uses for things like attributes, blocks, literal values, and expressions. But what most people think of as the Terraform language extends beyond just the syntax; the built-in functions, Terraform-specific block types (like `resource` and `variable`), and Terraform-specific named values available in expressions are all implementation details of Terraform itself.

- [GitHub: HCL](https://github.com/hashicorp/hcl)
- [Terraform docs: Configuration Language](/docs/configuration/index.html)

## ID

-> Terraform Enterprise

Also "external ID".

An identifier; an opaque string permanently associated with a specific object, which doesn't contain any information about the object but which can be used to retrieve information about it or perform actions on it via the API.

Most application objects within Terraform Enterprise (like workspaces, users, policies, etc.) can be identified by both a name and an opaque, permanent ID. Most API endpoints use IDs instead of names, since names sometimes change.

You can usually copy an ID from the URL bar when viewing an object in TFE's UI. Workspaces don't display an ID in the URL bar, but their general settings page includes a UI control for viewing and copying the ID.

## Ingress

-> Terraform Enterprise

The process of bringing content into Terraform Enterprise. Usually that content is a [configuration version][], but it can also be a private module version or some other kind of content.

This term comes from TFE's internal subsystems. Most documentation and UI avoids using "ingress," but it can sometimes appear in API contexts or support conversations.

## JSON

"JavaScript Object Notation". A popular text-based data interchange format, which can represent strings, numbers, booleans, null, arrays, and objects/maps.

Terraform and Terraform Enterprise often interact with JSON data in order to consume or provide APIs. Terraform also supports JSON as an alternate format for configurations.

- [Wikipedia: JSON](https://en.wikipedia.org/wiki/Json)
- [Terraform docs: JSON Configuration Syntax](/docs/configuration/syntax-json.html)

## Locking

-> Terraform Enterprise

The ability to prevent new runs from starting in a given workspace. Workspaces are automatically locked while a run is in progress, and can also be manually locked.

Some other Terraform backends can also lock state during runs.

## Log

The text-based output of actions taken within a run. For example, the output of running `terraform plan`.

## Module

Also "Terraform module".

A self-contained collection of Terraform configurations that manages a collection of related infrastructure resources.

Other Terraform configurations can _call_ a module, which tells Terraform to manage any resources described by that module.

Modules define input variables (which the calling module can set values for) and output values (which the calling module can reference in expressions).

- [Terraform docs: Modules](/docs/modules/index.html)

## OAuth

An open standard for token-based authorization between applications on the internet.

Terraform Enterprise uses OAuth to connect your organization to your VCS provider. Generally takes an `id` and `secret` from your VCS provider to give access to TFE and allow it to download configuration from the provider.

- [TFE docs: VCS Integration](/docs/enterprise/vcs/index.html)

## OAuth Client

-> Terraform Enterprise

The set of configuration that a TFE organization needs in order to connect to a specific VCS provider.

An OAuth client needs an OAuth token in order to actually access data belonging to a user or organization in that VCS provider. The client can be created with an existing token (when created via the API), or it can be created with the details TFE needs in order to request a token. Requesting a token requires a user to click through and approve access with their VCS provider account.

- [TFE docs: VCS Integration](/docs/enterprise/vcs/index.html)
- [TFE API docs: OAuth Clients](/docs/enterprise/api/oauth-clients.html)

## OAuth Token

-> Terraform Enterprise

The access token that a TFE organization needs in order to access data belonging to a user or organization in a specific VCS provider. The token is granted by the VCS provider, and allows access with whatever permissions that VCS provider assigns to the token.

An OAuth token has a one-to-one relationship with an OAuth client, but the client can outlive a specific token, to allow revoking and re-requesting VCS access.

Workspaces that are linked to a VCS repo have a relationship with one OAuth client.

- [TFE docs: VCS Integration](/docs/enterprise/vcs/index.html)
- [TFE API docs: OAuth Tokens](/docs/enterprise/api/oauth-tokens.html)

## Organization

-> Terraform Enterprise

TFE's fundamental unit for controlling access and grouping things together; meant to represent a company or a business unit within a company. An organization contains a group of workspaces, a group of teams, a group of Sentinel policies, and a variety of settings. Adding users to an organization is done via teams.

- [TFE docs: Organizations](/docs/enterprise/users-teams-organizations/organizations.html)

## Output Values

Also "outputs".

Data exported by a Terraform module, which can be displayed to a user and/or programmatically used by other Terraform code.

## OSS

"Open-Source Software". Terraform and the publicly available Terraform providers are open-source. Terraform Enterprise is closed-source commercial software.

- [Wikipedia: Open-Source Software](https://en.wikipedia.org/wiki/Open-source_software)

## Permissions

-> Terraform Enterprise

Specific levels of access allowed within TFE. Can be managed at the workspace and/or organization level. For example, a "read" user role has "permission" to see a list of runs but cannot approve a run like a "write" user can.

- [TFE docs: Permissions](/docs/enterprise/users-teams-organizations/permissions.html)

## Plan (verb)

Also "queue plan".

To start a new run.

- [TFE docs: About Runs](/docs/enterprise/run/index.html)

## Plan (noun, 1)

One of the stages of a run, in which Terraform compares the managed infrastructure's real state to the configuration and variables, determines which changes are necessary to make the real state match the desired state, and presents a human-readable summary to the user. The counterpart of an [apply][].

In Terraform's CLI, plans are performed by all of the following commands:

- `terraform plan`, which only performs a plan. It can optionally output a plan file, which `terraform apply` can use to perform that exact set of planned changes.
- `terraform apply`, which performs a plan and then, if a user approves, immediately applies it.
- `terraform destroy`, which is similar to `terraform apply` but uses a desired state in which none of the managed resources exist; if the plan is approved, those resources are destroyed.

In Terraform Enterprise, plans are performed by committing changes to a workspace's configuration, running `terraform plan` or `terraform apply` with the remote backend enabled, manually queueing a plan, or uploading a configuration via the API.

TFE's workflow always creates a [plan file][], which can be auto-applied or can wait for a user's approval. TFE also supports [speculative plans][speculative plan], which are for informational purposes only and cannot be applied.

- [Terraform docs: The `terraform plan` command](/docs/commands/plan.html)
- [TFE docs: About Runs](/docs/enterprise/run/index.html)

## Plan (noun, 2)

Also "plan file" or "`.tfplan`".

A binary artifact optionally produced by the `terraform plan` command, which `terraform apply` can use to carry out the exact changes that were decided at the time of the plan.

TFE always uses a saved plan as the input to an apply, so that applies never make changes that weren't shown to the user after the plan (in cases where the config or the variables changed in the meantime).

## Policy Check

-> Terraform Enterprise

Part of a run. After gathering the configuration, state, and plan (2) for a run, TFE runs Sentinel to check that data against the active policies. Policy checks end in success or failure. If a failure occurs in a required item, this can prevent the run from proceeding to the apply stage.

- [TFE docs: Run States and Stages](/docs/enterprise/run/states.html)

## Policy

-> Terraform Enterprise

Sentinel code that can be enforced on runs. Combined into policy sets.

- [TFE docs: Managing Sentinel Policies](/docs/enterprise/sentinel/manage-policies.html)

## Policy Set

-> Terraform Enterprise

A list of Sentinel policies to enforce globally or on specific workspaces.

- [TFE docs: Managing Sentinel Policies](/docs/enterprise/sentinel/manage-policies.html)

## Private Terraform Enterprise

-> Terraform Enterprise

Also "PTFE".

Private Terraform Enterprise is software provided to customers that allows full use of Terraform Enterprise in a private, isolated environment.

- [TFE docs: Private Terraform Enterprise](/docs/enterprise/private/index.html)

## Private Terraform Registry

-> Terraform Enterprise

A version of the [Terraform Registry][] that is built-in to TFE, to enable code sharing within an organization. It includes a Configuration Designer, which lets you combine and configure modules to generate Terraform configuration for them.

- [TFE docs: Private Registry](/docs/enterprise/registry/index.html)

## (Terraform) Provider

A plugin for Terraform that makes a collection of related resources available. A provider plugin is responsible for understanding API interactions with some kind of service and exposing resources based on that API.

Terraform providers are generally tied to a specific _infrastructure provider,_ which might be an infrastructure as a service (IaaS) provider (like AWS, GCP, Microsoft Azure, OpenStack), a platform as a service (PaaS) provider (like Heroku), or a software as a service (SaaS) provider (like Terraform Enterprise, DNSimple, CloudFlare).

There are many existing providers available, but providers can also be custom-built to work with any API.

- [Terraform docs: Providers](/docs/providers/index.html)

## TFE Provider

A Terraform provider that manages Terraform Enterprise. Allows you to manage TFE using a Terraform configuration.

- [Provider docs: tfe](/docs/providers/tfe/index.html)

## Pull Request (PR)

A mechanism created by GitHub to review and discuss changes made to a Git repository branch that a user wants to merge into another branch. Other collaborators can request changes, approve, or reject these changes. GitLab calls this a Merge Request.

## Queue

-> Terraform Enterprise

The list of runs waiting to be processed. TFE uses several queues of runs, including a per-workspace queue (since only one run at a time is allowed in a given workspace, to avoid conflicts and state corruption) and a global per-instance queue (since compute resources are finite and TFE only has access to so many VMs).

## Terraform Registry

A repository of modules written by the Terraform community, which can be used as-is within a Terraform configuration or forked and modified. The registry can help you get started with Terraform more quickly, see examples of how Terraform is written, and find pre-made modules for infrastructure components you require.

- [Terraform docs: The Terraform Registry](/docs/registry/index.html)

## Remote Operations

-> Terraform Enterprise

The ability to start a run (or perform a few other tasks) from your local CLI and view output inline, while still allowing TFE to perform the actual operation.

TFE performs Terraform runs in its own disposable VMs, where it can capture information, control access to secrets, etc., but many users are accustomed to running Terraform on their local machines. Remote operations exist to help split the difference.

- [Terraform docs: Remote Operations](/docs/backends/operations.html)

## Remote Backend

A Terraform CLI feature that lets Terraform connect to TFE, by specifying in the Terraform configuration which organization and workspace(s) to use. Used for remote operations in TFE workspaces, and used for state storage in TFE's free tier.

See also [backend][]. Older documentation sometimes refers to backends like `s3` or `consul` as "remote backends," since they store Terraform's state in a remote service instead of the local filesystem, but today this term usually means the specific backend whose name is `remote`.

- [Terraform docs: The `remote` Backend](/docs/backends/types/remote.html)

## Repository

Also "repo".

A collection of files and a history of the changes to them. In Terraform Enterprise, a "repo" is a Git repository that contains a Terraform configuration.

- [Wikipedia: Repository (version control)](https://en.wikipedia.org/wiki/Repository_(version_control))

## Root Module

The place where Terraform begins evaluating a configuration. The root module consists of all of the configuration files in Terraform's working directory.

The root module's variables and outputs are handled directly by Terraform (unlike child modules, whose variables and outputs are handled by the calling module). Root variable values can be provided with Terraform Enterprise, `.tfvars` files, CLI options, or environment variables. Root outputs are printed after a run and stored in the state.

## Root Outputs

Also "root-level outputs".

The output values of a configuration's root module. A configuration can access the root outputs of another configuration with a `terraform_remote_state` data source.

## Run

Also "Terraform Run".

The process of using Terraform to make real infrastructure match the desired state (as specified by the contents of the config and variables at a specific moment in time).

In Terraform Enterprise, runs are performed in a series of stages (plan, policy check, and apply), though not every stage occurs in every run. TFE saves information about historical runs.

- [Learn Terraform: Getting Started](https://learn.hashicorp.com/terraform/getting-started/install.html)
- [TFE docs: About Runs](/docs/enterprise/run/index.html)

## S3

Amazon Web Services' "Simple Storage Service", a service for storing and retrieving arbitrary blobs of data.

Many other cloud or self-hosted services provide APIs that are compatible with S3's API, which allows them to be used with software that was designed to work with S3.

Terraform's `aws` provider can manage S3 resources.

Private Terraform Enterprise uses an S3-compatible blob storage service when configured to use external services for storage.

- [AWS: S3](https://aws.amazon.com/s3/)

## SAML

-> Terraform Enterprise

SAML is an XML-based standard for authentication and authorization. Terraform Enterprise can act as a service provider (SP) (or Relying Party, RP) with your internal SAML identity provider (IdP). The SAML Single Sign On feature is only available with the Premium tier on private installs.

- [PTFE docs: SAML Single Sign-On](/docs/enterprise/saml/index.html)

## Service Account

-> Terraform Enterprise

An account (with API token) that doesn't belong to a human user but to an entity in TFE. Terraform Enterprise provides two types of service accounts: team and organization. These accounts can access Terraform Enterprise APIs, but cannot be used interactively. The service accounts are designed to support server-to-server API calls using the service identity as opposed to individual user identities.

- [TFE docs: Service Accounts](/docs/enterprise/users-teams-organizations/service-accounts.html)

## Sentinel

-> Terraform Enterprise

A language and runtime for managing policy as code. Allows you to define rules around operations in TFE.

- [TFE docs: Sentinel](/docs/enterprise/sentinel/index.html)

## Site Admin

-> Terraform Enterprise

An administrator of a Private Terraform Enterprise instance, who has access to application settings that affect all organizations using the instance.

- [PTFE docs: Administration](/docs/enterprise/private/admin/index.html)

## Speculative Plan

-> Terraform Enterprise

A run that is only intended to show possible changes to infrastructure, when using a given config version and set of variables. Speculative plans can never be applied, and are usually started as a result of pull requests to a workspaces' repo, or by running `terraform plan` on the command line  with remote operations configured.

## SSH Key

A type of access credential based on public key cryptography, used to log into servers.

TFE uses SSH private keys for two kinds of operations:

- Downloading private Terraform modules with Git-based sources during a Terraform run. Keys for downloading modules are assigned per-workspace.
- Bringing content from a connected VCS provider into TFE, usually when downloading a Terraform configuration for a workspace or importing a private module into the registry. Only some VCS providers require an SSH key, but others can optionally use SSH instead of the provider's normal API.

- [Wikipedia: SSH](https://en.wikipedia.org/wiki/Secure_Shell)
- [TFE docs: SSH Keys for Cloning Modules](/docs/enterprise/workspaces/ssh-keys.html)

## State

Terraform must store state about your managed infrastructure and configuration. This state is used by Terraform to map real world resources to your configuration, keep track of metadata, and improve performance for large infrastructures.

- [Terraform docs: State](/docs/state/index.html)

## State Version

-> Terraform Enterprise

A snapshot of your infrastructure's state at a point in time. Can be manually uploaded to TFE or created as the result of an apply.

Unlike TFE, Terraform CLI doesn't track historical state versions, and only retains the most recent state.

## Team

-> Terraform Enterprise

A group of TFE users, which can be given permission to access and/or edit various objects (workspaces, policies, etc.) within an organization. A team belongs to a single organization. Users can belong to any number of teams in any number of organizations.

- [TFE docs: Teams](/docs/enterprise/users-teams-organizations/teams.html)

## Terraform

A tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing and popular service providers as well as custom in-house solutions.

- [Intro to Terraform](/intro/index.html)

## TFE

Terraform Enterprise.

- [TFE docs](/docs/enterprise/index.html)

## Trigger

-> Terraform Enterprise

Something that causes a new run to queue. Can be UI/VCS-, API- or CLI-driven.

- [TFE docs: UI/VCS-based Run Workflow](/docs/enterprise/run/ui.html)

## (API) Tokens

-> Terraform Enterprise

Revocable alphanumeric strings that allow a user to authenticate itself in order to use the API. Different kinds of tokens grant different permissions. Can be granted by User, Team and/or Organization.

- [TFE docs: User Tokens](/docs/enterprise/users-teams-organizations/users.html#api-tokens)
- [TFE docs: Team Tokens](/docs/enterprise/users-teams-organizations/teams.html#api-tokens)
- [TFE docs: Organization Tokens](/docs/enterprise/users-teams-organizations/organizations.html#api-tokens)

## Tool Version

-> Terraform Enterprise

A particular version of the `terraform` binary, aka "Terraform Version". Specifies a URL, a SHA256 checksum and enabled/beta flags.

Available Terraform versions are configured at a per-instance level in Private Terraform Enterprise, and can be managed by site admins.

## Variables

Also "input variables".

Key/value pairs used in a run. Terraform modules can declare variables to allow customization. For child modules, the parent module provides a value when calling the module; for the root module, values are provided at run time.

TFE lets you set root input variables in a workspace, so all collaborators can use the same values. Variable values marked as "sensitive" become unreadable in the UI and API, and all variable values are protected by Vault.

- [Terraform docs: Input Variables](/docs/configuration/variables.html)
- [TFE docs: Variables](/docs/enterprise/workspaces/variables.html)

## VCS

Version Control System, like Git. Software that tracks changes over time to a collection of files, making it possible to keep track of changes, undo changes, and combine changes made in parallel by different users. Usually used for any non-trivial code effort, including infrastructure as code.

Different VCSes use different models for history; Git models changes as a directed acyclic graph of commits, and parallel changes that begin from the same parent commit become diverging branches (which might later be merged together).

- [Wikipedia: Version Control](https://en.wikipedia.org/wiki/Version_control)

## VCS Provider

-> Terraform Enterprise

A specific service that provides VCS features, with the goal of enabling teams to collaborate on code. TFE can integrate with VCS providers to access your Terraform configurations and modules, and currently supports GitHub, GitHub Enterprise, GitLab.com, GitLab EE and CE, Bitbucket Cloud, and Bitbucket Server.

- [TFE docs: Connecting VCS Providers](/docs/enterprise/vcs/index.html)

## Webhook

A server-to-server HTTP request, in which one system responds to a change in its internal state by asking another system to perform some kind of action.

The recipient of a webhook might return information to the requesting system, call other webhooks in response, perform its action silently, or ignore the request entirely.

Terraform Enterprise uses webhooks in multiple ways. Most notably:

- TFE creates webhook configurations on VCS providers, so that they send webhook requests to TFE whenever linked repositories receive pull requests or new commits. ([TFE docs: UI/VCS-driven Runs](/docs/enterprise/run/ui.html))
- Users can create webhook configurations on TFE workspaces, so that TFE will send run notification webhooks to Slack or other external services. ([TFE docs: Run Notifications](/docs/enterprise/workspaces/notifications.html))

## Working Directory

The directory where `terraform init` runs, creating a `.terraform` subdirectory. All subsequent commands for the same configuration should then be run from the same working directory.

The [root module][] consists of all of the configuration files in the top level of Terraform's working directory. Subdirectories of the working directory can contain child modules.

## Workspace

In Terraform CLI, a workspace is an isolated instance of state data. Using multiple workspaces lets you manage multiple non-overlapping sets of infrastructure from a single configuration in a single working directory.

In Terraform Enterprise, a workspace is a complex object that represents everything needed to manage a specific collection of infrastructure resources over time. In particular, this includes:

- A Terraform configuration (which has multiple versions over time, and which can come from a repo or from manual uploads)
- A set of variables
- State data that represents the current and historical condition of the infrastructure
- Historical information about runs.

All TFE runs occur in the context of a workspace — they use that workspace's config data, use that workspaces' state to identify the real infrastructure being managed, and edit that workspaces' state to match any infrastructure changes during the run. A workspace belongs to an organization.

- [TFE docs: Workspaces](/docs/enterprise/workspaces/index.html)
- [Terraform docs: Workspaces](/docs/state/workspaces.html)
