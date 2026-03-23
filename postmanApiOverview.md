title: Integrate Postman into your development toolchain
-------

Use the [Postman API](https://api.postman.com/) to programmatically manage your Postman assets and integrate Postman into your development toolchain. You can manage collections, environments, monitors, and other Postman elements. You can also access data stored in your Postman account and combine the Postman API with the [Postman CLI](/docs/postman-cli/postman-cli-overview/) or [Newman](/docs/collections/using-newman-cli/continuous-integration/) to integrate Postman with your CI/CD workflow.

For more details, see the [Postman API documentation](https://api.postman.com/). You'll also need an [API key](/docs/developer/postman-api/authentication/#generate-a-postman-api-key) to access the Postman API.

<Info class="iconless-callout">
  The Postman API is [rate limited](/docs/developer/postman-api/postman-api-rate-limits/).
</Info>

## Postman API features

The Postman API supports the following Postman features:

* [Workspaces](#workspaces)
* [Collections](#collections)
* [Environments and variables](#environments-and-variables)
* [Specifications](#specifications)
* [Mock servers](#mock-servers)
* [Monitors](#monitors)
* [Comments](#comments)
* [Forks](#forks)
* [Pull requests](#pull-requests)
* [User and usage data](#user-and-usage-data)
* [Users and user groups](#users-and-user-groups)
* [Roles](#roles)
* [Billing](#billing)

<Info class="plan">
  Additional Postman API endpoints are available, depending your Postman plan. For more information, see [API plan availability](#API-plan-availability).
</Info>

### Workspaces

Use the [Workspaces APIs](https://www.postman.com/postman/postman-public-workspace/folder/wppke9j/workspaces) to manage your [Postman workspaces](/docs/collaborating-in-postman/using-workspaces/create-workspaces/). These endpoints enable you to create temporary workspaces to test, which you can then delete when you're finished. You can also save a backup of another workspace or specific resources (such as collections or APIs) using the Postman API.

### Collections

Use the [Collections APIs](https://www.postman.com/postman/postman-public-workspace/folder/b7pojjp/collections) to manage your [Postman Collections](/docs/collections/collections-overview/) and simplify collection-related workflows. You can use these endpoints to add, delete, or update your collections. You can also use these endpoints to:

* Update an entire collection or a collection's requests, folders, and responses.
* Transfer collection items between collections or folders.
* Manage your collection forks, pull requests, and [published documentation](/docs/publishing-your-api/publishing-your-docs/).
* Manage [collection access keys](/docs/collaborating-in-postman/manage-public-elements/#collection-access-keys).

You can also use these endpoints to import an OpenAPI definition to create a collection or transform an existing collection into an OpenAPI definition. This lets you automatically generate a collection from your source code or API definition so you can then automatically sync it with Postman. Any resources that depend on that collection, such as monitors or mock servers, will also see the updated requests and responses.

### Environments and variables

The [Environments API](https://www.postman.com/postman/postman-public-workspace/folder/t1fblas/environments) enable you to programmatically manage your [Postman environments](/docs/sending-requests/variables/managing-environments/). You can use this API to manage your [global variables](https://www.postman.com/postman/postman-public-workspace/folder/pfngjbr/global-variables), which scope your work to different environments (such as local development, testing, or production). You can also manage [collection variables](https://www.postman.com/postman/postman-public-workspace/request/augwzgq/update-part-of-a-collection), which are available throughout a collection's requests.

### Specifications

The [Specs APIs](https://www.postman.com/postman/postman-public-workspace/folder/4qpsuuz/specs) enable you to manage your API specifications created in Postman's [Spec Hub](/docs/design-apis/specifications/overview/). With these endpoints, you can programmatically:

* Create, update, or get the complete definition of an API specification.
* Generate collections from specs, or generate specs from an existing Postman Collection.
* Synchronize your collections and specs with their source so they reflect your latest changes.
* Get details about API specifications in a workspace.
* List all the collections generated from an API specification or a collection's generated API specification.

### Mock servers

In addition to performing CRUD (Create, Read, Update, and Delete) operations on your [mock servers](/docs/design-apis/mock-apis/set-up-mock-servers/), you can use the [Mocks API](https://www.postman.com/postman/postman-public-workspace/folder/zueaxnn/mocks) to:

* Set a mock server to public or private.
* List all calls received by a mock server.
* Manage mock server responses for 5XX errors.

### Monitors

The [Monitors API](https://www.postman.com/postman/postman-public-workspace/folder/uu45lzt/monitors) enables you to programmatically run collections, depending on specific events on your CI/CD pipelines. You can also create and run a [webhook](/docs/collections/running-collections/collection-webhooks/), which is a special monitor that runs a collection.

With [Private API Monitoring](/docs/monitoring-your-api/runners/overview/), you can use the [Runners API](https://www.postman.com/postman/postman-public-workspace/folder/i540q3m/runners) to get metrics for a runner, such as the last date the runner sent monitor results to the Postman cloud. You can also use the Runners API to get all instances of a runner polling Postman for upcoming monitor runs.

### Comments

The **Comments** endpoints enable you to manage comments on Postman [APIs](https://www.postman.com/postman/postman-public-workspace/folder/kyjatxe/comments) and [API-based collections](https://www.postman.com/postman/postman-public-workspace/folder/w1qmprr/comments), [Postman Collections](https://www.postman.com/postman/postman-public-workspace/folder/ep2yw7r/comments) and collection [folders](https://www.postman.com/postman/postman-public-workspace/folder/fd7zaih/comments), [requests](https://www.postman.com/postman/postman-public-workspace/folder/2895un3/comments), and [responses](https://www.postman.com/postman/postman-public-workspace/folder/u9loyiz/comments). You can use [comments](/docs/collaborating-in-postman/comments/) to collaborate and discuss your work with your teammates in Postman.

### Forks

Use the **Forks** endpoints to manage [forks](/docs/collaborating-in-postman/using-version-control/forking-elements/) of Postman [collections](https://www.postman.com/postman/postman-public-workspace/folder/yrtfwkg/forks) and [environments](https://www.postman.com/postman/postman-public-workspace/folder/c4xsfxv/forks). Forks are new instances of an element that you can change without making any changes to the parent element. You can use these endpoints to find all forks for a specific [Postman Collection](https://www.postman.com/postman/postman-public-workspace/request/pydminp/get-a-collection-s-forks) or [environment](https://www.postman.com/postman/postman-public-workspace/request/h7jr1y9/get-an-environment-s-forks), or get the [current status](https://www.postman.com/postman/postman-public-workspace/request/3g3r320/get-source-collection-s-status) of a forked collection's source collection. You can also use these endpoints to programmatically create or merge forks and pull source changes.

### Pull requests

The **Pull Requests** endpoints enable you to manage your [pull requests](/docs/collaborating-in-postman/using-version-control/creating-pull-requests/) in Postman. Pull requests enable reviewers to look at your changes, leave comments on them, and decide whether to approve and merge them into the parent element. With these endpoints, you can [create a pull request](https://www.postman.com/postman/postman-public-workspace/request/9wzo1v1/create-a-pull-request) for a collection and [update](https://www.postman.com/postman/postman-public-workspace/request/fhin0wu/update-a-pull-request) existing pull requests. You can also [get information](https://www.postman.com/postman/postman-public-workspace/request/py30fhv/get-a-pull-request) about a pull request, such as its merge status, whether you can access it, and details about its source and destination.

### User and usage data

The [Get authenticated user API](https://www.postman.com/postman/postman-public-workspace/request/ay0ymqy/get-authenticated-user) returns information about the API key's owner. Use this endpoint to get details about your account and current usage information, such as how many API requests you can perform until the end of the month.

### Users and user groups

Use the [Users](https://www.postman.com/postman/postman-public-workspace/folder/gpu5rwc/users) and [Groups](https://www.postman.com/postman/postman-public-workspace/folder/y69vws8/groups) endpoints to manage user and user groups. These endpoints enable you to get basic information about [your team's users](https://www.postman.com/postman/postman-public-workspace/request/9ikp2vm/get-all-team-users) or your [team's user groups](https://www.postman.com/postman/postman-public-workspace/request/cy8f5dd/get-all-groups).

### Roles

[Roles](/docs/administration/roles-and-permissions/) define user permissions within Postman elements, such as workspaces, collections, and APIs. These endpoints enable you to programmatically manage user permissions:

* With the [Workspace Roles API](https://www.postman.com/postman/postman-public-workspace/folder/c5hrwtj/roles) you can manage user and user group permissions within a specific workspace. Use these endpoints to help you with onboarding or off-boarding, automating [role](/docs/administration/roles-and-permissions/#workspace-roles)-based workflows, and simplifying compliance and auditing processes by ensuring the right team members have access to sensitive information.
* The [Collections Roles API](https://www.postman.com/postman/postman-public-workspace/folder/9wltkx0/roles) enables you to manage your collection's [roles](/docs/administration/roles-and-permissions/#collection-roles). You can use them to view all users, teams, and groups with access to a collection or manage access permissions.

### Billing

The [Billing API](https://www.postman.com/postman/postman-public-workspace/folder/7iix2ud/billing) enables you to get information about your Postman billing account. You can use these endpoints to help with account and compliance. You can also use these endpoints to integrate with your internal systems, such as [SAP](https://www.sap.com/about/what-is-sap.html).

## API plan availability

Availability of the following APIs varies depending on if the applicable feature is available with your plan. For more information, see the [pricing page](https://www.postman.com/pricing/).

* [Private API Network](#private-api-network)
* [Tags](#tags)
* [Secret Scanner](#secret-scanner)
* [SCIM (System for Cross-domain Identity Management)](#scim)
* [API security and governance](#api-security-and-governance)
* [Audit logs](#audit-logs)

### Private API Network

The [Private API Network API](https://www.postman.com/postman/postman-public-workspace/folder/2guzk9z/private-api-network) enables you to programmatically manage your [Private API Network](/docs/collaborating-in-postman/private-api-network/overview/). Use these endpoints to automate the management of your team's internal documentation, integrate it with CI/CD, and ensure that the documentation is always up-to-date. This API also enables you to get all user requests to add elements to your Private API Network and approve or reject them.

### Tags

Use the [Tags APIs](https://www.postman.com/postman/postman-public-workspace/folder/ab29tvd/tags) to manage your Postman tags programmatically. You can use these endpoints to add or remove tags from Postman [collections](/docs/collections/use-collections/collaborate-with-collections/#tag-a-collection) and [workspaces](/docs/collaborating-in-postman/using-workspaces/internal-workspaces/use-workspaces/#tag-a-workspace). You can also use this API to get all Postman elements that match a given tag and then operate on them programmatically.

{/* vale postman-style-guide.Headings = NO */}

### Secret Scanner

{/* vale postman-style-guide.Headings = YES */}

The [Secret Scanner API](https://www.postman.com/postman/postman-public-workspace/folder/35jon94/secret-scanner) programmatically provides the same functionality as the [Secret Scanner](/docs/administration/managing-your-team/secret-scanner/overview/) dashboard. These endpoints enable Enterprise customers to manage secrets detected by the Postman Secret Scanner. Use it to:

* Search detected secrets (paginated).
* Find the location of a detected secret.
* Update the resolution status of a detected secret.
* Build automatic notification systems.
* Programmatically resolve detected secrets.

### SCIM

The [SCIM API](https://www.postman.com/postman/postman-public-workspace/folder/l6yozde/scim) supports [SCIM](/docs/administration/scim-provisioning/scim-provisioning-overview/) (System for Cross-domain Identity Management), which enables you to automate the provisioning of your team. You can deploy Postman at scale across your organization and control access to it with your identity provider. You can use these endpoints to integrate your onboarding process and automatically provision users and groups.

### API security and governance

The [API Security API](https://www.postman.com/postman/postman-public-workspace/folder/31xluzv/api-security) enables you to manage your API's security by running security checks and tracking your API definition's governance and security rule violations. For example, you can use the [API definition security validation endpoint](https://www.postman.com/postman/postman-public-workspace/request/1kl63um/api-definition-security-validation) to validate an OpenAPI definition. You can also use it to publish a new version of your API.

### Audit logs

Use the [Audit Logs API](https://www.postman.com/postman/postman-public-workspace/folder/tl4rymv/audit-logs) to monitor and analyze your Postman Enterprise teams. [Admins](/docs/administration/roles-and-permissions/#team-roles) can review audit logs, filter by specific criteria, and get information about:

* When users were added to, removed from, or invited to your team.
* Which user performed a specific action—and when they did so.

## Deprecated endpoints

Deprecated Postman API endpoints reside in the [DEPRECATED](https://www.postman.com/postman/postman-public-workspace/folder/0a4bnwe/deprecated) folder of the Postman API collection. In the [Postman API OpenAPI definition](https://www.postman.com/postman/postman-public-workspace/specification/3001f4e4-5f9d-4bac-9f57-b2c4d483508f/file/1f4ad1bf-697f-4be6-a167-dc1f3cf2abf2?view=documentation\&ctx=preview), they're marked by the `deprecated: true` property or, in some cases, removed from the definition.

Deprecated endpoints are unsupported and don't receive any updates. At a future time they will be removed and no longer be available. **It's recommended that you don't use deprecated endpoints.**
