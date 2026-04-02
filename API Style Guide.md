Internal APIs should provide the same level of documentation quality expected for public consumers. Internal consumers are just as important as external consumers. Follow the same standards for both.

## Contents

- [Naming](#naming)
- [Describing an API](#describing-an-api)
- [Dependencies and behaviors](#dependencies-and-behaviors)
- [Parameters and properties](#parameters-and-properties)
- [Request body](#request-body)
- [Empty responses](#empty-responses)
- [Examples](#examples)
- [Tags](#tags)
- [Components](#components)
- [Lexicon and terms](#lexicon-and-terms)
- [Text and formatting](#text-and-formatting)

## Naming

**Use sentence case** Begin the name of the API with the verb related to its action.

✅ Get all users

✅ Create a new user

❌ Get All Users

When possible, keep API names concise.

✅ Get user data

❌ Get information about a user

Do not use punctuation in the `summary` property.

✅ Get all users

❌ Get all users.

## Describing an API

**All APIs must include a description.**

Begin with a present-tense verb and briefly state what action the API performs.

✅ Gets information about the user.
✅ Deletes a user from the database.
❌ This endpoint lets you get information about the user.
❌ Delete operation

Provide further explanation in subsequent sentences. For example, how to use it, prerequisites, behaviors the consumer should be aware of, or related APIs to direct the consumer to.

## Dependencies and behaviors

Document any API dependencies. For example, see [Google's API reference code comments Description entry](https://developers.google.com/style/api-reference-comments).

Document any behaviors consumers should expect from the endpoint.

## Parameters and properties

Use code font for parameter names to make them scannable.

✅ The user's `id` value.
❌ The user's id value.

### Default behavior

Include the `default` value where applicable to note default behavior when describing parameters or properties.

In some cases, behavior may be unclear from the `default` property alone. In such cases, provide context in the property's description.

✅ Whether the user is in the public directory. This value defaults to null.
✅ The user's ID. If you do not provide this value, the system randomly generates a user ID.

## Request body

Use "property" and "properties" to describe a request body JSON object's key value.

✅ The `id` property in the `user` object.

## Empty responses

If an API returns an empty response, such as an HTTP 204 No Content or HTTP 201 Created response, note it in the description. Consumers may expect to see output.

✅ Creates a new response. On success, this returns an HTTP `204 No Content` response.

## Examples

Always include examples in API documentation, including but not limited to:

- Parameters
- Request bodies
- Responses

Examples provide consumers with clarity and context around the API and its expected behavior.

### Example format

Use examples in the same format as what consumers would see or use in their APIs. For example:

- A user ID: `123-456-7890`
- The product's unique ID: `f36a368e-7a4b-444b-8552-dbdcbdc52dfb`

### Sensitive information and data

Avoid using real names. Use generic names. For example:

- Alex Lee
- Taylor Cruz

If additional names are required for multiple users in an example, reference [Example person names](https://developers.google.com/style/examples#example-person-names).

### Proprietary examples

Don't use trademarked or copyrighted examples. This includes brands, characters, devices, or software.

When in doubt, use "Test", "Example", or "Sample" as placeholder values.

✅ Test API
✅ Example, Inc.
✅ https://example.git.com
❌ Dungeons & Dragons API
❌ Dunder Mifflin, Inc.
❌ https://xkcd.com

### Domains and IP addresses

Use the following for all domain examples:

- `https://example.com`, `https://example.net`, `https://example.org` - IANA-hosted URLs for general examples.
- `subdomain.example.com` - For subdomain examples.

Use the following IANA-reserved IP address ranges:

- `192.0.2.0` - `192.0.2.255`
- `198.51.100.0` - `198.51.100.255`
- `203.0.113.0` - `203.0.113.255`
- `233.252.0.0` - `233.252.0.255`
- IPv6: `2001:db8::` - `2001:db8:ffff:ffff:ffff:ffff:ffff:ffff`

### Placeholders

Use angle brackets (`<>`) for placeholder values as needed. For example, `<PlaceholderValue>`.

## Tags

Always use Tags in OpenAPI specifications.

- Include a `tags` property and a tag for each endpoint.
- Include a description with each tag that provides a general overview of what the group of endpoints does.

## Components

Use components in an OpenAPI specifications.

- Components keep documentation concise.
- Components are easier to maintain--you update information in a single place, rather than throughout the entire specification.
- Components help reduce maintenance burden because they are reusable and scalable.

## Lexicon and terms

Use inclusive language. Avoid ableist language.

Refer to [Google's Word list](https://developers.google.com/style/word-list). It's a comprehensive list with justification for using or avoiding specific words and phrases.

## Text and formatting

### Commas

Use serial commas (Oxford commas) to eliminate ambiguity.

✅ This API gets the user's ID, name, and IP address.
❌ This API gets the user's ID, name and IP address.

### Dashes

Use em dashes (—) to separate listed items from their descriptions.

✅ `id` — The user's ID.
❌ `id` - The user's ID.
❌ `id` -- The user's ID.

### Hyphens

Use a hyphen with a space on either side to separate values, such as IP address ranges.

✅ `192.0.2.0` - `192.0.2.255`

### Ampersands

Do not use the ampersand (`&`) character. Use "and" instead.

✅ This API returns a user's basic data and usage information.
❌ This API returns a user's basic data & usage information.

### Important callouts

Use the `### Important` format to warn users about potentially destructive behavior or deprecations.

```
### Important

Use cation when using this endpoint. The system **replaces** existing data with the data passed in the request body.
```

### Notes

Use the `**Note:**` format to share specific, non-destructive details about an endpoint, such as behaviors, constraints, or caveats.

```
**Note:**

The maximum allowed file size is 10 MB.
```

### For example

Use "for example". Don't use abbreviations such as "e.g.", as abbreviations don't always localize.

✅ The user's ID. For example, `123-456-7890`.
❌ The user's ID, e.g. `123-456-7890`.

### Whether

Use "whether" when describing Boolean values. Don't use "whether or not".

✅ Whether the API is public.
❌ Whether or not the API is public.

You can use "if true" form for Boolean values.

✅ If true, sets the API as public.

### Sentences

End all sentences, including descriptions, with a period.

✅ An ID is the unique identifier assigned to a user's account.
❌ The API uses API keys for authentication
