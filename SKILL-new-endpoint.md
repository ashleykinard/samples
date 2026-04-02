---
name: new-endpoint
description: Scaffold a new, compliant OpenAPI operation and insert it into the current location in the specification.
---

Invocation format: `/new-endpoint <METHOD> <PATH> <FEATURE>`

- `<METHOD>` — The HTTP verb (GET, POST, PUT, PATCH, DELETE).
- `<PATH>` — The endpoint's path (for example, `/user/{userId}/account`).
- `<FEATURE>` — The feature area (for example, `users`).

## Providing definition context (recommended)

Most users already have their API design defined. Provide it using one of these methods:

**Inline** — Paste an existing specification directly in the message after running the command. Accepts raw YAML, raw JSON, or a partial specification. No stringification needed.

```bash
/new-endpoint POST /user/{userId}/account users

<insert definition>
```

This method is recommended for definitions less than 300 lines. For files greater than 300 lines, use `--from` instead.

**File** — Points to a local file using the `--from <filepath>` command. Preferred for larger specifications (300+ lines) to avoid pasting large blocks into the conversation. Accepts the `.json`, `.yaml`, and `.yml` file types.

```bash
/new-endpoint POST /user/{userId}/account users --from ~/Downloads/spec-file.yaml
```

When context is provided with either method, use it to derive schema property names, types, descriptions, and example values. Read only the sections needed (such as request body or response schemas) rather than processing the entire file upfront.

When no context is provided, generate structurally correct scaffolding with placeholder values.

## Step 1 — Verify branch

Run `git branch --show-current` and check the current branch name.

- If the current branch is `main`, stop immediately and tell the user: "This command cannot be run on the `main` branch. Create a feature branch first (for example, `feature/JIRA-123-new-endpoint`) and run the command again."
- If the current branch does not start with `feature/`, warn the user: "This command is intended for `feature/` branches. You are currently on `<branch>`. Consider switching to a properly-named branch before continuing." Then ask the user whether to process or to cancel.
- If the current branch starts with `feature/`, continue.

## Step 2 — Resolve feature files

**If `<FEATURE>.yml` exists** in a given component directory, use that file for all additions:

- `paths/<FEATURE>.yml`
- `components/examples/<FEATURE>.yml`
- `components/parameters/<FEATURE>.yml`
- `components/schemas/<FEATURE>.yml`
- `components/headers/<FEATURE>.yml`
- `components/requestBodies/<FEATURE>.yml`
- `components/responses/<FEATURE>.yml`

**If `<FEATURE>.yml does not exist** in any of the above locations, this is considered a new feature. Before creating any files:

1. Search `example.com/docs` for documentation that matches the feature name. If a page is found, note the URL for use in the tag description. If no page is found, omit the link from the tag description entirely, and do not use a placeholder URL. Add a note in the completion checklist advising the user to find the relevant page on the Docs Site and add the link to the tag description in `index.yml` manually.
2. Prompt the user to confirm:
   - The tag `name` (for example, `"User Accounts"`).
   - The tag `description`, following the established pattern: `"The **<TAG NAME>** endpoints enable you to <description>."` with the documentation link appended only if found.
   - The list of new `<FEATURE>.yml` files that will be created across `paths/` and applicable `components/` subdirectories.

Once confirmed, create the files and add the new tag entry to the `tags` list in `index.yml` in alphabetical order.

Also read `index.yml` to identify existing tags and registered paths, and scan `components/parameters/<FEATURE>.yml` for reusable parameters that match path or query parameters in the new endpoint.

## Step 3 — Determine response codes

Infer the appropriate response codes from the HTTP method and path:

**GET**
- `200` — Success
- `401` — Unauthorized
- `403` — Forbidden
- `404` — Not Found (always include if the path contains a resource ID parameter, for example `{userId}`)
- `500` — Internal Server Error

**POST**
- `200` — Success
- `201` — Created
- `400` — Bad Request
- `401` — Unauthorized
- `403` — Forbidden
- `404` — Not Found (include if the path contains a resource ID parameter)
- `500` — Internal Server Error

**PUT / PATCH**
- `200` — Success
- `400` — Bad Request
- `401` — Unauthorized
- `403` — Forbidden
- `404` — Not Found (always include if the path contains a resource ID parameter, for example `{userId}`)
- `500` — Internal Server Error

**DELETE**
- `200` or `204` — Success (use `204` if there is no response body)
- `401` — Unauthorized
- `403` — Forbidden
- `404` — Not Found (always include if the path contains a resource ID parameter, for example `{userId}`)
- `500` — Internal Server Error

## Step 4 — Resolve cross-feature ID parameters

For every path and query parameter that matches the `<resourceName>Id` pattern (for example, `userId` or `accountId`), scan all files in `components/parameters/` to find an existing definition for that parameter. ID parameters are defined in the file that owns the resource — for example, `userId` lives in `components/parameters/users.yml`, not `components/parameters/common.yml`.

- If a matching parameter exists in another feature's parameter file, `$ref` it from there rather than defining it inline or duplicating it in `components/parameters/<FEATURE>.yml`.
- If no matching parameter exists anywhere in `components/parameters/`, define it in `components/parameters/<FEATURE>.yml` if it belongs to the current feature, or prompt the user to confirm where it should live if it belongs to another feature.

This check applies regardless of whether context is provided.

## Step 5 — Detect reusable error components (context only)

Only perform this step when the user has provided a definition inline or with `--from`. Skip this step and proceed directly to Step 6 when no context is provided.

Evaluate the property types of each error schema in the user's definition and compare them against the modern variants in `components/schemas/common.yml`. Do not consider example values — only evaluate whether the property names and types match exactly.

| Properties present | Use |
| --- | --- |
| `type`, `title`, `detail` | `errorTypeTitleDetail` |
| `type`, `title`, `detail`, `status` | `errorTypeTitleDetailStatus` |
| `type`, `title`, `detail`, `status`, `instance` | `errorTypeTitleDetailStatusInstance` |
| `error.name`, `error.message` | `errorNameMessageObj` |
| `name`, `message` | `errorNameMessage` |

**If the property types match exactly**, use the canonical schema.

**If there is a structural discrepancy** (missing, extra, or differently-typed properties), stop and prompt the user:

> "Your error schema closely matches `<canonicalVariant>` but doesn't match exactly. The differences are: `<list discrepancies>`. How do you want to proceed?
> - **Use canonical variant** — Use `<canonicalVarian>` and note the discrepancy in the completion checklist.
> - **Feature-specific** — Create a new schema in `components/schemas/<FEATURE>.yml` and reference it from `components/responses/<FEATURE>.yml`.
> - **Shared/reusable** — I'll propose additions to `components/schemas/common.yml` and `components/responses/common.yml` for your review before making any changes."

Do not modify `common.yml` files without explicit user confirmation.

Also scan `components/schemas/<FEATURE>.yml` and `components/schemas/common.yml` for structural matches against the user's success response and request body schemas. If a match exists, `$ref` it rather than create a duplicate.

## Step 6 — Scaffold the operation

Generate a fully-compliant operation block:

- `summary` — A short description of the action. Derive this from context if provided, otherwise use a placeholder.
- `description` — A longer description of what the operation does. Derive this from context if provided, otherwise use a placeholder.
- `operationId` — Use camelCase, and infer from the method+path (for example, POST `/useer/{userId}/account → `createUserAccount`).
- `tags` — Reuse existing tags from `index.yml` where applicable. For new features, use the tag name confirmed in Step 2.
- `parameters` — Include all path and relevant query parameters, each with:
  - `description`
  - `example`
  - `$ref` to the owning feature's parameter file where a reusable match exists (see Steps 2 and 4).

**Schema property examples:**
- Scalar properties (string, number, boolean, enum) → include `example` inline at the property level.
- Object properties → do NOT add `example` on the object itself; ad `example` only on its scalar children.
- Derive property names, types, and example values from provided context; otherwise, use stubs.

**When context is missing or incomplete** (for example, the provided schema lacks descriptions), infer a compliant content by reading analogous existing entries in the repo's `components/schemas/`, `components/responses/`, and `paths/` files to match established conventions. Flag any inferred content in the completion checklist (Step 8) with a note to review it against `docs/style-guide.md` and `docs/documenting-apis.md`.

**Request body:**
- Reference or create an entry in `components/requestBodies/<FEATURE>.yml` using a `$ref`.
- In the request body component, use `examples` (plural, named) that `$ref` entries in `components/examples/<FEATURE>.yml`.
- Do not use inline `example` at the request body level.

**Responses:**
- One entry per code determined in Step 3.
- Success responses: reference or create an entry in `components/responses/<FEATURE>.yml` using a `$ref`.
- In the response component, use `examples` (plural, named) that `$ref` entries in `components/examples/<FEATURE>.yml`.
- Error responses: always `$ref` the canonical error entries from `components/responses/common.yml`:
  - `$ref: ../responses/common.yml#/error400`.
  - `$ref: ../responses/common.yml#/error401`.
  - `$ref: ../responses/common.yml#/error403`.
  - `$ref: ../responses/common.yml#/error404`.
  - `$ref: ../responses/common.yml#/error500`.

## Step 7 — Insert into the spec

- Add the operation to `paths/<FEATURE>.yml`.
- If the path is new to `index.yml`, register it under the appropriate `paths` entry.
- Add new request body entries to `components/requestBodies/<FEATURE>.yml`.
- Add new response entries to `components/responses/<FEATURE>.yml`.
- Add new schema entries to `components/schemas/<FEATURE>.yml`.
- Add example stubs to `components/examples/<FEATURE>.yml`.

## Step 8 — Output a completion checklist

List every placeholder the user still needs to fill in:

- Summaries and descriptions that need real content.
- Schema property names, types, and descriptions that are stubs.
- Example values in `components/examples/<FEATURE>.yml` that need real data.
- Any content inferred from existing specification patterns that should be reviewed against `docs/style-guide.md` and `docs/documenting-apis.md`.
- Tag description documentation links, if no matching page was found — visit example.com/docs to find the feature page and add the link to the tag description in `index.yml`.
- Any error schemas approximated to a canonical variant that need verification.
- Any cross-feature ID parameters that couldn't be resolve and require placement decision.
- Any schemas that should be further extract to `components/schemas/` if they grow.

Do not run the linter automatically. Remind the user to run `/lint` when ready to validate.
