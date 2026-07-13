# Integrate Postman into your development toolchain

Use the [Postman API](https://api.postman.com/) to programmatically manage your Postman assets and integrate Postman into your development toolchain. You can manage collections, environments, monitors, and other Postman elements. You can also access data stored in your Postman account and combine the Postman API with the [Postman CLI](/docs/postman-cli/postman-cli-overview/) to integrate Postman with your CI/CD workflow.

You can get started by [forking](/docs/collaborating-in-postman/using-version-control/forking-elements/) the Postman API collection in the Postman Public Workspace.

For more details, see the [Postman API documentation](https://api.postman.com/). You'll also need an [API key](/docs/reference/postman-api/authentication/#generate-a-postman-api-key) to access the Postman API.

The Postman API is [rate limited](/docs/reference/postman-api/postman-api-rate-limits/).

## Postman API features

The Postman API supports the following Postman features:

* [Analytics](#analytics)
* [Billing](#billing)
* [Collections](#collections)
* [Comments](#comments)
* [Environments and variables](#environments-and-variables)
* [Forks](#forks)
* [Mock servers](#mock-servers)
* [Monitors](#monitors)
* [OAuth 2.0](#oauth-20)
* [Pull requests](#pull-requests)
* [Roles](#roles)
* [Specifications](#specifications)
* [User and usage data](#user-and-usage-data)
* [Users and user groups](#users-and-user-groups)
* [Workspaces](#workspaces)

Additional Postman API endpoints are available depending on your Postman plan. For more information, see [API plan availability](#api-plan-availability).

### Analytics

The [Analytics API](https://www.postman.com/postman/postman-public-workspace/folder/12959542-1ab1ba03-7183-4732-8fdb-ddf1e1f3e2b7) enables you to explore Postman's analytics reports programmatically. Use these endpoints to discover usage patterns, workspace and collection activity, API performance, license distribution, and partner onboarding flows. You can use these endpoints to integrate Postman's analytics with your internal analytics systems and create custom reports and dashboards.

### Billing

The [Billing API](https://www.postman.com/postman/postman-public-workspace/folder/7iix2ud/billing) enables you to get information about your Postman billing account. You can use these endpoints to help with accounting and compliance. You can also use these endpoints to integrate with your internal systems, such as [SAP](https://www.sap.com/about/what-is-sap.html).

### Collections

Use the [Collections APIs](https://www.postman.com/postman/postman-public-workspace/folder/b7pojjp/collections) to manage your [Postman Collections](/docs/use/use-collections/overview/) and simplify collection-related workflows. You can use these endpoints to add, delete, or update your collections. You can also use these endpoints to:

* Update an entire collection or a collection's requests, folders, and responses.
* Transfer collection items between collections or folders.
* Manage your collection forks, pull requests, and [published documentation](/docs/publishing-your-api/publishing-your-docs/).
* Manage [collection access keys](/docs/collaborating-in-postman/manage-public-elements/#collection-access-keys).

You can also use these endpoints to import an OpenAPI definition to create a collection or transform an existing collection into an OpenAPI definition. This lets you automatically generate a collection from your source code or API definition so you can then automatically sync it with Postman. Any resources that depend on that collection, such as monitors or mock servers, will also see the updated requests and responses.

### Comments

The **Comments** endpoints enable you to manage comments on Postman [APIs](https://www.postman.com/postman/postman-public-workspace/folder/kyjatxe/comments), [API-based collections](https://www.postman.com/postman/postman-public-workspace/folder/w1qmprr/comments), [Postman Collections](https://www.postman.com/postman/postman-public-workspace/folder/ep2yw7r/comments), collection [folders](https://www.postman.com/postman/postman-public-workspace/folder/fd7zaih/comments), [requests](https://www.postman.com/postman/postman-public-workspace/folder/2895un3/comments), and [responses](https://www.postman.com/postman/postman-public-workspace/folder/u9loyiz/comments). You can use [comments](/docs/collaborating-in-postman/comments/) to collaborate and discuss your work with your teammates in Postman.

### Environments and variables

The [Environments API](https://www.postman.com/postman/postman-public-workspace/folder/t1fblas/environments) enables you to programmatically manage your [Postman environments](/docs/use/send-requests/variables/managing-environments/). You can use this API to manage your [global variables](https://www.postman.com/postman/postman-public-workspace/folder/pfngjbr/global-variables), which scope your work to different environments (such as local development, testing, or production). You can also manage [collection variables](https://www.postman.com/postman/postman-public-workspace/request/augwzgq/update-part-of-a-collection), which are available throughout a collection's requests.

### Forks

Use the **Forks** endpoints to manage [forks](/docs/collaborating-in-postman/using-version-control/forking-elements/) of [collections](https://www.postman.com/postman/postman-public-workspace/folder/yrtfwkg/forks) and [environments](https://www.postman.com/postman/postman-public-workspace/folder/c4xsfxv/forks). Forks are new instances of an element that you can change without making any changes to the parent element. You can use these endpoints to find all forks for a specific [Postman Collection](https://www.postman.com/postman/postman-public-workspace/request/pydminp/get-a-collection-s-forks) or [environment](https://www.postman.com/postman/postman-public-workspace/request/h7jr1y9/get-an-environment-s-forks), or get the [current status](https://www.postman.com/postman/postman-public-workspace/request/3g3r320/get-source-collection-s-status) of a forked collection's source collection. You can also use these endpoints to programmatically create or merge forks and pull source changes.

### Mock servers

In addition to performing CRUD (Create, Read, Update, and Delete) operations on your [mock servers](/docs/design-apis/mock-apis/set-up-mock-servers/), you can use the [Mocks API](https://www.postman.com/postman/postman-public-workspace/folder/zueaxnn/mocks) to:

* Set a mock server to public or private.
* List all calls received by a mock server.
* Manage mock server responses for 5XX errors.

### Monitors

The [Monitors API](https://www.postman.com/postman/postman-public-workspace/folder/uu45lzt/monitors) enables you to programmatically run collections, depending on specific events on your CI/CD pipelines. You can also create and run a [webhook](/docs/tests-and-scripts/running-collections/collection-webhooks/), which is a special monitor that runs a collection.

With [Private API Monitoring](/docs/monitoring-your-api/runners/overview/), you can use the [Runners API](https://www.postman.com/postman/postman-public-workspace/folder/i540q3m/runners) to get metrics for a runner, such as the last date the runner sent monitor results to the Postman cloud. You can also use the Runners API to get all instances of a runner polling Postman for upcoming monitor runs.

### OAuth 2.0

Use the [OAuth 2.0 API](https://www.postman.com/postman/postman-public-workspace/folder/12959542-878ff397-f0f3-4a47-a2f8-4a251c9edc21) to generate and revoke [OAuth 2.0 authentication tokens](/docs/use/send-requests/authorization/oauth-20/) in Postman.

### Pull requests

The **Pull Requests** endpoints enable you to manage your [pull requests](/docs/collaborating-in-postman/using-version-control/creating-pull-requests/) in Postman. Pull requests enable reviewers to look at your changes, leave comments on them, and decide whether to approve and merge them into the parent element. With these endpoints, you can [create a pull request](https://www.postman.com/postman/postman-public-workspace/request/9wzo1v1/create-a-pull-request) for a collection and [update](https://www.postman.com/postman/postman-public-workspace/request/fhin0wu/update-a-pull-request) existing pull requests. You can also [get information](https://www.postman.com/postman/postman-public-workspace/request/py30fhv/get-a-pull-request) about a pull request, such as its merge status, whether you can access it, and details about its source and destination.

### Roles

[Roles](/docs/administration/roles-and-permissions/) define user permissions within Postman elements, such as workspaces, collections, and APIs. These endpoints enable you to programmatically manage user permissions:

* With the [Workspace Roles API](https://www.postman.com/postman/postman-public-workspace/folder/c5hrwtj/roles), you can manage permissions for users and user groups within a specific workspace. Use these endpoints to help you with onboarding or off-boarding, automating [role](/docs/administration/roles-and-permissions/#workspace-roles)-based workflows, and simplifying compliance and auditing processes by ensuring the right team members have access to sensitive information.
* The [Collections Roles API](https://www.postman.com/postman/postman-public-workspace/folder/9wltkx0/roles) enables you to manage your collection's [roles](/docs/administration/roles-and-permissions/#collection-roles). You can use these endpoints to view all users, teams, and groups with access to a collection or manage access permissions.

### Specifications

The [Specs APIs](https://www.postman.com/postman/postman-public-workspace/folder/4qpsuuz/specs) enable you to manage your API specifications created in Postman's [Spec Hub](/docs/design-apis/specifications/overview/). With these endpoints, you can programmatically:

* Create, update, or get the complete definition of an API specification.
* Generate collections from specs, or generate specs from an existing Postman Collection.
* Synchronize your collections and specs with their source so they reflect your latest changes.
* Get details about API specifications in a workspace.
* List all the collections generated from an API specification or a collection's generated API specification.

### User and usage data

The [Get authenticated user API](https://www.postman.com/postman/postman-public-workspace/request/ay0ymqy/get-authenticated-user) returns information about the API key's owner. Use this endpoint to get details about your account and current usage information, such as how many API requests you can perform until the end of the month.

### Users and user groups

Use the [Users](https://www.postman.com/postman/postman-public-workspace/folder/gpu5rwc/users) and [Groups](https://www.postman.com/postman/postman-public-workspace/folder/y69vws8/groups) endpoints to manage users and user groups. These endpoints enable you to get basic information about [your team's users](https://www.postman.com/postman/postman-public-workspace/request/9ikp2vm/get-all-team-users) or your [team's user groups](https://www.postman.com/postman/postman-public-workspace/request/cy8f5dd/get-all-groups).

### Workspaces

Use the [Workspaces APIs](https://www.postman.com/postman/postman-public-workspace/folder/wppke9j/workspaces) to manage your [Postman workspaces](/docs/collaborating-in-postman/using-workspaces/create-workspaces/). These endpoints enable you to create temporary workspaces to test, which you can then delete when you're finished. You can also save a backup of another workspace or specific resources (such as collections or APIs) using the Postman API. You can programmatically manage your [workspace updates](https://www.postman.com/postman/postman-public-workspace/folder/53qg224/workspace-updates).

## API plan availability

The availability of the following APIs varies depending on whether the feature is included in your Postman plan. For more information, see the [pricing page](https://www.postman.com/pricing/).

* [API Catalog](#api-catalog)
* [API Governance](#api-governance)
* [Audit logs](#audit-logs)
* [Components](#components)
* [Private API Network](#private-api-network)
* [SCIM (System for Cross-domain Identity Management)](#scim)
* [SDKs](#sdks)
* [Secret Scanner](#secret-scanner)
* [Service accounts](#service-accounts)
* [Tags](#tags)
* [Teams](#teams)

### API Catalog

The [API Catalog API](https://www.postman.com/postman/postman-public-workspace/folder/12959542-662c6651-adb3-4894-8a14-cdd4e28e98b3) enables you to programmatically manage your [API Catalog](/docs/api-catalog/overview/). Use these endpoints to connect your source code to the API Catalog. The API Catalog then automatically shows you all your APIs in one place. You can also manage your team's [system environments](https://www.postman.com/postman/postman-public-workspace/folder/12959542-f5b8a51f-c8a2-4d2d-a903-6969924d838b) and [discover](https://www.postman.com/postman/postman-public-workspace/folder/12959542-8ff967a1-6bf8-41a4-9a4c-23aae22d203e) APIs and services within your organization.

### API Governance

The [API Governance API](https://www.postman.com/postman/postman-public-workspace/folder/31xluzv/api-governance) enables you to run checks and track governance for your API definitions. For example, you can use the [API definition validation](https://www.postman.com/postman/postman-public-workspace/request/1kl63um/api-definition-validation) to validate an OpenAPI definition.

### Audit logs

Use the [Audit Logs API](https://www.postman.com/postman/postman-public-workspace/folder/tl4rymv/audit-logs) to monitor and analyze your Postman Enterprise teams. [Admins](/docs/administration/roles-and-permissions/#team-roles) can review audit logs, filter by specific criteria, and get information about:

* When users were added to, removed from, or invited to your team.
* Which user performed a specific action—and when they did so.

### Components

Use the [Components API](https://www.postman.com/postman/postman-public-workspace/folder/jikrw8a/components) to manage specification components in the Postman [Component Library](/docs/design-apis/specifications/component-library/). Components are reusable elements you can use across multiple API specifications. You can use these endpoints to create, update, and delete components in your Postman workspace. You can also use these endpoints to get all components in a workspace or get details about a specific component.

### Private API Network

The [Private API Network API](https://www.postman.com/postman/postman-public-workspace/folder/2guzk9z/private-api-network) enables you to programmatically manage your [Private API Network](/docs/collaborating-in-postman/private-api-network/overview/). Use these endpoints to automate the management of your team's internal documentation, integrate it with CI/CD, and ensure that the documentation is always up-to-date. This API also enables you to get all user requests to add elements to your Private API Network and approve or reject them.

### SCIM

The [SCIM API](https://www.postman.com/postman/postman-public-workspace/folder/l6yozde/scim) supports [SCIM](/docs/administration/scim-provisioning/scim-provisioning-overview/) (System for Cross-domain Identity Management), which enables you to automate the provisioning of your team. You can deploy Postman at scale across your organization and control access to it with your identity provider. You can use these endpoints to integrate your onboarding process and automatically provision users and groups.

### SDKs

Use the [SDKs API](https://www.postman.com/postman/postman-public-workspace/folder/2h9uw5x/sdks) to manage your [Postman SDKs](/docs/sdk-generator/overview/). You can use these endpoints to create, update, and delete SDKs in your Postman workspaces. You can also use these endpoints to get all SDKs in a workspace or get details about a specific SDK. You can also manage your [SDK Git connections](https://www.postman.com/postman/postman-public-workspace/folder/zshpkjb/sdk-git-connections), which enable you to automatically sync your SDKs with your source code.

### Secret Scanner

The [Secret Scanner API](https://www.postman.com/postman/postman-public-workspace/folder/35jon94/secret-scanner) programmatically provides the same functionality as the [Secret Scanner](/docs/administration/managing-your-team/secret-scanner/overview/) dashboard. These endpoints enable Enterprise customers to manage secrets detected by the Postman Secret Scanner. Use it to:

* Search detected secrets (paginated).
* Find the location of a detected secret.
* Update the resolution status of a detected secret.
* Build automatic notification systems.
* Programmatically resolve detected secrets.

### Service accounts

The [Service Accounts API](https://www.postman.com/postman/postman-public-workspace/folder/ryjfi8x/service-accounts) enables you to programmatically manage your Postman [service accounts](/docs/administration/service-accounts/), which are non-human accounts designed for automation, integrations, and system-to-system interactions.

### Tags

Use the [Tags APIs](https://www.postman.com/postman/postman-public-workspace/folder/ab29tvd/tags) to manage your Postman tags programmatically. You can use these endpoints to add or remove tags from [collections](/docs/use/use-collections/collaborate-with-collections/#tag-a-collection) and [workspaces](/docs/collaborating-in-postman/using-workspaces/internal-workspaces/use-workspaces/#tag-a-workspace). You can also use this API to get all Postman elements that match a given tag and then operate on them programmatically.

### Teams

The [Teams API](https://www.postman.com/postman/postman-public-workspace/folder/12959542-6ef68efb-993c-414e-b514-535ba1d439ae) enables you to manage your Postman organization's teams. Use these endpoints to create or manage teams, get information about teams, and manage team members and their roles within teams.

## Deprecated endpoints

Deprecated Postman API endpoints reside in the [DEPRECATED](https://www.postman.com/postman/postman-public-workspace/folder/0a4bnwe/deprecated) folder of the Postman API collection. In the [Postman API OpenAPI definition](https://www.postman.com/postman/postman-public-workspace/specification/3001f4e4-5f9d-4bac-9f57-b2c4d483508f/file/1f4ad1bf-697f-4be6-a167-dc1f3cf2abf2?view=documentation\&ctx=preview), they're marked by the `deprecated: true` property or, in some cases, removed from the definition.

Deprecated endpoints are unsupported and don't receive any updates. At a future time they will be removed and no longer be available. **It's recommended that you don't use deprecated endpoints.**
