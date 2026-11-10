---
name: opendoc
description: "Generate or update complete OpenAPI documentation for changed REST resources, using separate contract interfaces and realistic examples derived from the implementation. Invoke explicitly with `opendoc`."
---

# OpenAPI REST documentation

Use this skill when documenting or regenerating REST API contracts from source code. The explicit trigger is `opendoc`; do not process unrelated endpoints.

## Scope and change detection

1. Inspect repository instructions first, especially language, generated-file, and documentation rules.
2. Determine the work set from Git changes before opening every REST class. Include tracked staged and unstaged changes, and relevant untracked files. Prefer `git diff --name-only HEAD` plus `git status --short` to identify changed REST resources and their contract interfaces.
3. Process only changed REST files and the interfaces/classes directly required by them. Do not reprocess an API that is clean in Git merely because it is nearby.
4. A clean class may be changed only when the user explicitly names it or explicitly asks for a complete repository-wide audit/regeneration. Otherwise report it as out of scope.
5. Locate and modify the source class or interface that actually owns the endpoint description/contract. Do not put documentation on an unrelated facade, generated artifact, or static HTML file unless requested.

## Source analysis before writing documentation

For every changed endpoint, derive the contract from the code rather than inventing it:

- inspect the route, HTTP method, path, path/query/header/body parameters, validation, and media types;
- follow the return type, return statements, builders, DTOs/models, serializers, wrappers, and exception/error paths;
- inspect inherited or delegated methods when they determine the serialized response;
- use fixtures or existing tests when they reveal actual values, but never copy secrets or production personal data.

Document every parameter with its name, location, type/schema, requiredness, and an accurate description. Document successful and meaningful error responses, including their actual media type and schema. Every response that returns an object or array of objects must have a complete, realistic example matching the code: correct field names, types, nesting, enums, nullability, and wrapper structure. Arrays and nested collections must contain at least one representative element; object fields that are part of the actual response must be populated with plausible values. Never use an empty list as the only example for a list endpoint and never invent fields or a response shape. If the source is insufficient to establish the response shape, inspect the serializer/model or stop and report the missing source instead of fabricating an example.

All OpenAPI prose and example descriptions must be in Italian when repository instructions require Italian. Keep existing identifiers and API field names unchanged; any new code comments must be in English.

## Contract interface pattern

Prefer a separate interface for the OpenAPI contract:

- keep the REST implementation focused on runtime behavior;
- create or update the corresponding `*Api` interface in the appropriate package;
- put OpenAPI operation, parameter, response, tag, schema, and example annotations on the interface method;
- make the REST class implement that interface and preserve the framework route annotations according to the project convention;
- ensure the interface method signature exactly matches the implementation, including generic types, checked exceptions, and parameter order.

Do not duplicate conflicting annotations across implementation and interface. Follow the target framework's annotation inheritance behavior and the repository's established pattern. Use the correct OpenAPI imports for the project version.

## Language-neutral rules and language-specific notes

The workflow is language-agnostic: identify the runtime resource, its serialized contract, and the contract interface/trait/type supported by the framework. Use the project's native OpenAPI annotation or attribute syntax rather than assuming Java syntax.

For Java/JAX-RS, typically use a separate `*Api.java` interface with `@Operation`, `@Parameter`, `@ApiResponses`/`@ApiResponse`, `@Content`, `@Schema`, and `@ExampleObject` as appropriate. Verify imports against the installed Swagger/OpenAPI version; in Swagger v3 `Parameter` is `io.swagger.v3.oas.annotations.Parameter`. Keep JAX-RS annotations where the application discovers them, unless the project convention proves interface annotations are inherited safely.

For PHP, use the framework's supported OpenAPI attributes or docblocks on the contract interface when interface metadata is supported. Preserve PHP namespace/import conventions and validate the generated document with the project's generator.

Do not create contract interfaces when the generator ignores them, as with Scribe (Laravel): Scribe reads attributes and docblocks only from the controller method, so put all documentation metadata directly on the controller. Create an interface only if the project already uses it for something else (container binding, test doubles, multiple implementations).

## Verification and handoff

After editing:

- inspect the diff and confirm no clean, unrelated API was modified;
- check every changed operation for descriptions, parameter documentation, response schemas, and populated examples;
- validate the generated OpenAPI document and run the narrowest relevant compile/test/generation command;
- check that examples contain no accidental empty arrays or placeholder fields and that they match serialized names and types;
- report files changed, validation performed, and any endpoint that could not be documented without additional source evidence.

Do not commit, push, or alter Git history. Do not place generated resources in the production artifact unless the user explicitly requests that packaging behavior.
