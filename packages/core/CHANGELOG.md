# @urql/core

## 5.2.0

### Minor Changes

- export the getOperationName utility function
  Submitted by [@giacomocerquone](https://github.com/giacomocerquone) (See [#3785](https://github.com/urql-graphql/urql/pull/3785))

## 5.1.2

### Patch Changes

- Correct typo in cacheHit debug message of the `debugExchange`
  Submitted by [@jorrit](https://github.com/jorrit) (See [#3773](https://github.com/urql-graphql/urql/pull/3773))
- ⚠️ Fix `fetchSource` not text-decoding response chunks as streams, which could cause UTF-8 decoding to break
  Submitted by [@i110](https://github.com/i110) (See [#3767](https://github.com/urql-graphql/urql/pull/3767))
- ⚠️ Fix compatibility with Typescript >5.5 (See: https://github.com/0no-co/graphql.web/pull/49)
  Submitted by [@andreisergiu98](https://github.com/andreisergiu98) (See [#3730](https://github.com/urql-graphql/urql/pull/3730))
- Change debug log verbosity to `console.debug` rather than `console.log`
  Submitted by [@kitten](https://github.com/kitten) (See [#3770](https://github.com/urql-graphql/urql/pull/3770))

## 5.1.1

### Patch Changes

- Omit minified files and sourcemaps' `sourcesContent` in published packages
  Submitted by [@kitten](https://github.com/kitten) (See [#3755](https://github.com/urql-graphql/urql/pull/3755))

## 5.1.0

### Minor Changes

- Remove `addMetadata` transform where we'd strip out metadata for production environments, this particularly affects `OperationResult.context.metadata.cacheOutcome`
  Submitted by [@alpavlove](https://github.com/alpavlove) (See [#3714](https://github.com/urql-graphql/urql/pull/3714))

## 5.0.8

### Patch Changes

- ⚠️ Fix `deepMerge` regression on array values
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3696](https://github.com/urql-graphql/urql/pull/3696))

## 5.0.7

### Patch Changes

- Remove `for-of` syntax from `@urql/core` helpers for JSC memory reduction
  Submitted by [@kitten](https://github.com/kitten) (See [#3690](https://github.com/urql-graphql/urql/pull/3690))

## 5.0.6

### Patch Changes

- Allow empty error messages when re-hydrating GraphQL errors
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3650](https://github.com/urql-graphql/urql/pull/3650))

## 5.0.5

### Patch Changes

- Removes double serialization of `data` in `ssrExchange`
  Submitted by [@negezor](https://github.com/negezor) (See [#3632](https://github.com/urql-graphql/urql/pull/3632))

## 5.0.4

### Patch Changes

- Change how we calculate the `OperationKey` to take files into account, before we
  would encode them to `null` resulting in every mutation with the same variables
  (excluding the files) to have the same key. This resulted in mutations that upload
  different files at the same time to share a result in GraphCache
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3601](https://github.com/urql-graphql/urql/pull/3601))

## 5.0.3

### Patch Changes

- Use `documentId` from persisted documents for document keys, when it's available
  Submitted by [@kitten](https://github.com/kitten) (See [#3575](https://github.com/urql-graphql/urql/pull/3575))

## 5.0.2

### Patch Changes

- ⚠️ Fix issue where a reexecute on an in-flight operation would lead to multiple network-requests.
  For example, this issue presents itself when Graphcache is concurrently updating multiple, inter-dependent queries with shared entities. One query completing while others are still in-flight may lead to duplicate operations being issued
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3573](https://github.com/urql-graphql/urql/pull/3573))

## 5.0.1

### Patch Changes

- ⚠️ Fix `@ts-ignore` on TypeScript peer dependency import in typings not being applied due to a leading `!` character
  Submitted by [@kitten](https://github.com/kitten) (See [#3567](https://github.com/urql-graphql/urql/pull/3567))

## 5.0.0

### Major Changes

- Remove deprecated `dedupExchange`
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3520](https://github.com/urql-graphql/urql/pull/3520))
- Remove deprecated `maskTypename`
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3520](https://github.com/urql-graphql/urql/pull/3520))

### Patch Changes

- Upgrade `@0no-co/graphql.web` to `1.0.5`
  Submitted by [@kitten](https://github.com/kitten) (See [#3553](https://github.com/urql-graphql/urql/pull/3553))

## 4.3.0

### Minor Changes

- Support [Apollo Federation's format](https://www.apollographql.com/docs/router/executing-operations/subscription-multipart-protocol/) for subscription results in `multipart/mixed` responses (result properties essentially are namespaced on a `payload` key)
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3499](https://github.com/urql-graphql/urql/pull/3499))
- Add support for sending persisted documents. Any `DocumentNode` with no/empty definitions and a `documentId` property is considered a persisted document. When this is detected a `documentId` parameter rather than a `query` string is sent to the GraphQL API, similar to Automatic Persisted Queries (APQs). However, APQs are only supported via `@urql/exchange-persisted`, while support for `documentId` is now built-in
  Submitted by [@kitten](https://github.com/kitten) (See [#3515](https://github.com/urql-graphql/urql/pull/3515))

### Patch Changes

- Allow `url` to be a plain, non-URL pathname (i.e. `/api/graphql`) to be used with `preferGetMethod`
  Submitted by [@akrantz01](https://github.com/akrantz01) (See [#3514](https://github.com/urql-graphql/urql/pull/3514))
- Correctly support the `Headers` class being used in `fetchOptions`
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3505](https://github.com/urql-graphql/urql/pull/3505))

## 4.2.3

### Patch Changes

- Add back our cache-outcome on the document-cache, this was behind a development flag however in our normalized cache we always add it already
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3464](https://github.com/urql-graphql/urql/pull/3464))

## 4.2.2

### Patch Changes

- ⚠️ Fix the default `cacheExchange` crashing on `cache-only` request policies with cache misses due to `undefined` results
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3459](https://github.com/urql-graphql/urql/pull/3459))

## 4.2.1

### Patch Changes

- ⚠️ Fix incorrect JSON stringification of objects from different JS contexts. This could lead to invalid variables being generated in the Vercel Edge runtime specifically
  Submitted by [@SoraKumo001](https://github.com/SoraKumo001) (See [#3453](https://github.com/urql-graphql/urql/pull/3453))

## 4.2.0

### Minor Changes

- Try to parse `text/plain` content-type as JSON before bailing out with an error
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3430](https://github.com/urql-graphql/urql/pull/3430))

## 4.1.4

### Patch Changes

- Implement new `@defer` / `@stream` transport protocol spec changes
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3389](https://github.com/urql-graphql/urql/pull/3389))
- Support non spec-compliant error bodies, i.e. the Shopify API does return `errors` but as an object. Adding
  a check whether we are really dealing with an Array of errors enables this
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3395](https://github.com/urql-graphql/urql/pull/3395))
- ⚠️ Fix `preferGetMethod: 'force' | 'within-url-limit'` not being applied correctly by the `Client`
  Submitted by [@Burbenog](https://github.com/Burbenog) (See [#3403](https://github.com/urql-graphql/urql/pull/3403))

## 4.1.3

### Patch Changes

- ⚠️ Fix missing `teardown` operation handling in the `ssrExchange`. This could lead to duplicate network operations being executed
  Submitted by [@kitten](https://github.com/kitten) (See [#3386](https://github.com/urql-graphql/urql/pull/3386))

## 4.1.2

### Patch Changes

- Explicitly unblock `client.reexecuteOperation` calls to allow stalled operations from continuing and re-executing. Previously, this could cause `@urql/exchange-graphcache` to stall if an optimistic mutation led to a cache miss
  Submitted by [@kitten](https://github.com/kitten) (See [#3363](https://github.com/urql-graphql/urql/pull/3363))

## 4.1.1

### Patch Changes

- Add case for `subscriptionExchange` to handle `GraphQLError[]` received in the `error` observer callback.
  **Note:** This doesn't strictly check for the `GraphQLError` shape and only checks for arrays and receiving errors in the `ExecutionResult` on the `next` observer callback is preferred and recommended for transports
  Submitted by [@kitten](https://github.com/kitten) (See [#3346](https://github.com/urql-graphql/urql/pull/3346))

## 4.1.0

### Minor Changes

- Update `formatDocument` to output `FormattedNode` type mapping. The formatter will now annotate added `__typename` fields with `_generated: true`, place selection nodes' directives onto a `_directives` dictionary, and will filter directives to not include `"_"` underscore prefixed directives in the final query. This prepares us for a feature that allows enhanced client-side directives in Graphcache
  Submitted by [@kitten](https://github.com/kitten) (See [#3317](https://github.com/urql-graphql/urql/pull/3317))

### Patch Changes

- Add `OperationContext.optimistic` flag as an internal indication on whether a mutation triggered an optimistic update in `@urql/exchange-graphcache`'s `cacheExchange`
  Submitted by [@kitten](https://github.com/kitten) (See [#3308](https://github.com/urql-graphql/urql/pull/3308))

## 4.0.11

### Patch Changes

- Re-order `maskTypename` to apply masking earlier in the chain
  Submitted by [@kitten](https://github.com/kitten) (See [#3298](https://github.com/urql-graphql/urql/pull/3298))
- ⚠️ Fix `ssrExchange` not formatting query documents using `formatDocument`. Without this call we'd run the risk of not having `__typename` available on the client-side when rehydrating
  Submitted by [@kitten](https://github.com/kitten) (See [#3288](https://github.com/urql-graphql/urql/pull/3288))
- Add deprecation notice for `maskTypename` option.
  Masking typenames in a result is no longer recommended. It’s only
  useful when multiple pre-conditions are applied and inferior to
  mapping to an input object manually
  Submitted by [@kitten](https://github.com/kitten) (See [#3299](https://github.com/urql-graphql/urql/pull/3299))

## 4.0.10

### Patch Changes

- Add missing `fetchSubscriptions` entry to `OperationContext`. The Client’s `fetchSubscriptions` now works properly and can be used to execute subscriptions as multipart/event-stream requests
  Submitted by [@kitten](https://github.com/kitten) (See [#3244](https://github.com/urql-graphql/urql/pull/3244))
- ⚠️ Fix `fetchSource` not working for subscriptions since `hasNext` isn’t necessarily set
  Submitted by [@kitten](https://github.com/kitten) (See [#3244](https://github.com/urql-graphql/urql/pull/3244))

## 4.0.9

### Patch Changes

- Return `AbortController` invocation to previous behaviour where it used to be more forceful. It will now properly abort outside of when our generator yields results, and hence now also cancels requests again that have already delivered headers but are currently awaiting a response body
  Submitted by [@kitten](https://github.com/kitten) (See [#3239](https://github.com/urql-graphql/urql/pull/3239))

## 4.0.8

### Patch Changes

- Respect `additionalTypenames` on subscriptions and re-execute queries for them as well, as one would intuitively expect
  Submitted by [@kitten](https://github.com/kitten) (See [#3230](https://github.com/urql-graphql/urql/pull/3230))
- Update build process to generate correct source maps
  Submitted by [@kitten](https://github.com/kitten) (See [#3201](https://github.com/urql-graphql/urql/pull/3201))
- Don't allow `isSubscriptionOperation` option in `subscriptionExchange` to include `teardown` operations, to avoid confusion
  Submitted by [@kitten](https://github.com/kitten) (See [#3206](https://github.com/urql-graphql/urql/pull/3206))

## 4.0.7

### Patch Changes

- Publish with npm provenance
  Submitted by [@kitten](https://github.com/kitten) (See [#3180](https://github.com/urql-graphql/urql/pull/3180))

## 4.0.6

### Patch Changes

- Handle `multipart/mixed` variations starting with boundary rather than CRLF and a boundary
  Submitted by [@kitten](https://github.com/kitten) (See [#3172](https://github.com/urql-graphql/urql/pull/3172))
- ⚠️ Fix regression which would disallow `network-only` operations after `cache-and-network` completed
  Submitted by [@kitten](https://github.com/kitten) (See [#3174](https://github.com/urql-graphql/urql/pull/3174))

## 4.0.5

### Patch Changes

- Replace `File` and `Blob` objects with `null` in variables if multipart request will be started
  Submitted by [@kitten](https://github.com/kitten) (See [#3169](https://github.com/urql-graphql/urql/pull/3169))
- Strictly deduplicate `cache-and-network` and `network-only` operations, while a non-stale response is being waited for
  Submitted by [@kitten](https://github.com/kitten) (See [#3157](https://github.com/urql-graphql/urql/pull/3157))
- ⚠️ Fix boundary stopping `multipart/mixed` streams when it randomly occurs in response payloads
  Submitted by [@kitten](https://github.com/kitten) (See [#3155](https://github.com/urql-graphql/urql/pull/3155))
- Improve dispatching of arbitrary operations using `reexecuteOperation`
  Submitted by [@kitten](https://github.com/kitten) (See [#3159](https://github.com/urql-graphql/urql/pull/3159))

## 4.0.4

### Patch Changes

- ⚠️ Fix `hasNext` being defaulted to `false` when a new subscription event is received on the `subscriptionExchange` that doesn't have `hasNext` set
  Submitted by [@kitten](https://github.com/kitten) (See [#3137](https://github.com/urql-graphql/urql/pull/3137))

## 4.0.3

### Patch Changes

- Handle `fetch` rejections in `makeFetchSource` and properly hand them over to `CombinedError`s
  Submitted by [@kitten](https://github.com/kitten) (See [#3131](https://github.com/urql-graphql/urql/pull/3131))

## 4.0.2

### Patch Changes

- ⚠️ Fix incremental delivery payloads not merging data correctly, or not handling patches on root
  results
  Submitted by [@kitten](https://github.com/kitten) (See [#3124](https://github.com/urql-graphql/urql/pull/3124))

## 4.0.1

### Patch Changes

- ⚠️ Fix format of `map` form data field on multipart upload requests. This was erroneously set to a string rather than a string tuple
  Submitted by [@kitten](https://github.com/kitten) (See [#3118](https://github.com/urql-graphql/urql/pull/3118))

## 4.0.0

### Major Changes

- Remove `defaultExchanges` from `@urql/core` and make `exchanges` a required property on `Client` construction.
  In doing so we make the `urql` package more tree-shakeable as the three default exchanges are in no code paths
  meaning they can be removed if not used.
  A migration would look as follows if you are currently creating a client without exchanges

  ```js
  import { createClient, cacheExchange, fetchExchange } from '@urql/core';

  const client = createClient({
    url: '',
    exchanges: [cacheExchange, fetchExchange],
  });
  ```

  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3033](https://github.com/urql-graphql/urql/pull/3033))

- Update `subscriptionExchange` to receive `FetchBody` instead. In the usual usage of `subscriptionExchange` (for instance with `graphql-ws`) you can expect no breaking changes. However, the `key` and `extensions` field has been removed and instead the `forwardSubscription` function receives the full `Operation` as a second argument
  Submitted by [@kitten](https://github.com/kitten) (See [#3054](https://github.com/urql-graphql/urql/pull/3054))
- Remove dependence on `graphql` package and replace it with `@0no-co/graphql.web`, which reduces the default bundlesize impact of `urql` packages to a minimum. All types should remain compatible, even if you use `graphql` elsewhere in your app, and if other dependencies are using `graphql` you may alias it to `graphql-web-lite`
  Submitted by [@kitten](https://github.com/kitten) (See [#3097](https://github.com/urql-graphql/urql/pull/3097))
- Update `OperationResult.hasNext` and `OperationResult.stale` to be required fields. If you have a custom exchange creating results, you'll have to add these fields or use the `makeResult`, `mergeResultPatch`, or `makeErrorResult` helpers
  Submitted by [@kitten](https://github.com/kitten) (See [#3061](https://github.com/urql-graphql/urql/pull/3061))
- Remove `getOperationName` export from `@urql/core`
  Submitted by [@kitten](https://github.com/kitten) (See [#3062](https://github.com/urql-graphql/urql/pull/3062))

### Minor Changes

- Return a new `OperationResultSource` from all `Client` methods (which replaces `PromisifiedSource` on shortcut methods). This allows not only `toPromise()` to be called, but it can also be used as an awaitable `PromiseLike` and has a `.subscribe(onResult)` method aliasing the subscribe utility from `wonka`
  Submitted by [@kitten](https://github.com/kitten) (See [#3060](https://github.com/urql-graphql/urql/pull/3060))
- Update `subscriptionExchange` to support incremental results out of the box. If a subscription proactively completes, results are also now updated with `hasNext: false`
  Submitted by [@kitten](https://github.com/kitten) (See [#3055](https://github.com/urql-graphql/urql/pull/3055))
- Implement `text/event-stream` response support. This generally adheres to the GraphQL SSE protocol and GraphQL Yoga push responses, and is an alternative to `multipart/mixed`
  Submitted by [@kitten](https://github.com/kitten) (See [#3050](https://github.com/urql-graphql/urql/pull/3050))
- Implement GraphQL Multipart Request support in `@urql/core`. This adds the File/Blob upload support to `@urql/core`, which effectively deprecates `@urql/exchange-multipart-fetch`
  Submitted by [@kitten](https://github.com/kitten) (See [#3051](https://github.com/urql-graphql/urql/pull/3051))
- Support `GraphQLRequest.extensions` as spec-extensions input to GraphQL requests
  Submitted by [@kitten](https://github.com/kitten) (See [#3054](https://github.com/urql-graphql/urql/pull/3054))
- Allow subscriptions to be handled by the `fetchExchange` when `fetchSubscriptions` is turned on
  Submitted by [@kitten](https://github.com/kitten) (See [#3106](https://github.com/urql-graphql/urql/pull/3106))
- Deprecate the `dedupExchange`. The functionality of deduplicating queries and subscriptions has now been moved into and absorbed by the `Client`.
  Previously, the `Client` already started doing some work to share results between
  queries, and to avoid dispatching operations as needed. It now only dispatches operations
  strictly when the `dedupExchange` would allow so as well, moving its logic into the
  `Client`
  Submitted by [@kitten](https://github.com/kitten) (See [#3058](https://github.com/urql-graphql/urql/pull/3058))

### Patch Changes

- Deduplicate operations as the `dedupExchange` did; by filtering out duplicate operations until either the original operation has been cancelled (teardown) or a first result (without `hasNext: true`) has come in
  Submitted by [@kitten](https://github.com/kitten) (See [#3101](https://github.com/urql-graphql/urql/pull/3101))
- ⚠️ Fix source maps included with recently published packages, which lost their `sourcesContent`, including additional source files, and had incorrect paths in some of them
  Submitted by [@kitten](https://github.com/kitten) (See [#3053](https://github.com/urql-graphql/urql/pull/3053))
- Allow `makeOperation` to be called with a partial `OperationContext` when it’s called to copy an operation. When it receives an `Operation` as a second argument now, the third argument, the context, will be spread into the prior `operation.context`
  Submitted by [@kitten](https://github.com/kitten) (See [#3081](https://github.com/urql-graphql/urql/pull/3081))
- Move `multipart/mixed` to end of `Accept` header to avoid cauing Yoga to unnecessarily use it
  Submitted by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#3039](https://github.com/urql-graphql/urql/pull/3039))
- Upgrade to `wonka@^6.3.0`
  Submitted by [@kitten](https://github.com/kitten) (See [#3104](https://github.com/urql-graphql/urql/pull/3104))
- Update `Exchange` contract and `composeExchanges` utility to remove the need to manually call `share` on either incoming `Source<Operation>` or `forward()`’s `Source<OperationResult>`. This is now taken care of internally in `composeExchanges` and should make it easier for you to create custom exchanges and for us to explain them
  Submitted by [@kitten](https://github.com/kitten) (See [#3082](https://github.com/urql-graphql/urql/pull/3082))
- Add support for `graphql`’s built-in `TypedQueryDocumentNode` typings for type inference
  Submitted by [@kitten](https://github.com/kitten) (See [#3085](https://github.com/urql-graphql/urql/pull/3085))
- Add missing type exports of SSR-related types (`SerializedResult`, `SSRExchangeParams`, `SSRExchange`, and `SSRData`) to `@urql/core`'s type exports
  Submitted by [@kitten](https://github.com/kitten) (See [#3079](https://github.com/urql-graphql/urql/pull/3079))
- Allow any object fitting the `GraphQLError` shape to rehydrate without passing through a `GraphQLError` constructor in `CombinedError`
  Submitted by [@kitten](https://github.com/kitten) (See [#3087](https://github.com/urql-graphql/urql/pull/3087))
- Add missing `hasNext` and `stale` passthroughs on caching exchanges
  Submitted by [@kitten](https://github.com/kitten) (See [#3059](https://github.com/urql-graphql/urql/pull/3059))
- ⚠️ Fix incremental results not merging `errors` from subsequent non-incremental results
  Submitted by [@kitten](https://github.com/kitten) (See [#3055](https://github.com/urql-graphql/urql/pull/3055))
- Add logic for `request.extensions.persistedQuery` to `@urql/core` to omit sending `query` as needed
  Submitted by [@kitten](https://github.com/kitten) (See [#3057](https://github.com/urql-graphql/urql/pull/3057))
- ⚠️ Fix incorrect operation name being picked from queries that contain multiple operations
  Submitted by [@kitten](https://github.com/kitten) (See [#3062](https://github.com/urql-graphql/urql/pull/3062))
- Replace fetch source implementation with async generator implementation, based on Wonka's `fromAsyncIterable`.
  This also further hardens our support for the "Incremental Delivery" specification and
  refactors its implementation and covers more edge cases
  Submitted by [@kitten](https://github.com/kitten) (See [#3043](https://github.com/urql-graphql/urql/pull/3043))
- Ensure network errors are always issued with `CombinedError`s, while downstream errors are re-thrown
  Submitted by [@kitten](https://github.com/kitten) (See [#3063](https://github.com/urql-graphql/urql/pull/3063))
- Refactor `Client` result source construction code and allow multiple mutation
  results, if `result.hasNext` on a mutation result is set to `true`, indicating
  deferred or streamed results
  Submitted by [@kitten](https://github.com/kitten) (See [#3102](https://github.com/urql-graphql/urql/pull/3102))
- Remove dependence on `import { visit } from 'graphql';` with smaller but functionally equivalent alternative
  Submitted by [@kitten](https://github.com/kitten) (See [#3097](https://github.com/urql-graphql/urql/pull/3097))

## 3.2.2

### Patch Changes

- ⚠️ Fix generated empty `Variables` type as passed to generics, that outputs a type of `{ [var: string]: never; }`.
  A legacy/unsupported version of `typescript-urql`, which wraps `urql`'s React hooks, generates
  empty variables types as the following code snippet, which is not detected:
  ```ts
  type Exact<T extends { [key: string]: unknown }> = { [K in keyof T]: T[K] };
  type Variables = Exact<{ [key: string]: never }>;
  ```
  Submitted by [@kitten](https://github.com/kitten) (See [#3029](https://github.com/urql-graphql/urql/pull/3029))

## 3.2.1

### Patch Changes

- Bump to `@urql/core@3.2.1` due to invalid `3.2.0` release
  Submitted by [@kitten](https://github.com/kitten) (See [`a84268db`](https://github.com/urql-graphql/urql/commit/a84268db98789b2fd23de009c7b5e1c09fca7103))

## 3.2.0

### Minor Changes

- Update support for the "Incremental Delivery" payload specification, accepting the new `incremental` property on execution results, as per the specification. This will expand support for newer APIs implementing the more up-to-date specification
  Submitted by [@kitten](https://github.com/kitten) (See [#3007](https://github.com/urql-graphql/urql/pull/3007))
- Update default `Accept` header to include `multipart/mixed` and `application/graphql-response+json`. The former seems to now be a defactor standard-accepted indication for support of the "Incremental Delivery" GraphQL over HTTP spec addition/RFC, and the latter is an updated form of the older `Content-Type` of GraphQL responses, so both the old and new one should now be included
  Submitted by [@kitten](https://github.com/kitten) (See [#3007](https://github.com/urql-graphql/urql/pull/3007))

### Patch Changes

- Add TSDoc annotations to all external `@urql/core` APIs
  Submitted by [@kitten](https://github.com/kitten) (See [#2962](https://github.com/urql-graphql/urql/pull/2962))
- ⚠️ Fix subscriptions not being duplicated when `hasNext` isn't set. The `hasNext` field is an upcoming "Incremental Delivery" field. When a subscription result doesn't set it we now set it to `true` manually. This indicates to the `dedupExchange` that no duplicate subscription operations should be started
  Submitted by [@kitten](https://github.com/kitten) (See [#3015](https://github.com/urql-graphql/urql/pull/3015))
- Expose consistent `GraphQLRequestParams` utility type from which `GraphQLRequest`s are created in all bindings
  Submitted by [@kitten](https://github.com/kitten) (See [#3022](https://github.com/urql-graphql/urql/pull/3022))

## 3.1.1

### Patch Changes

- Correctly mark cache-hits from the ssr-exchange, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2872](https://github.com/urql-graphql/urql/pull/2872))
- ⚠️ Fix type-generation, with a change in TS/Rollup the type generation took the paths as src and resolved them into the types dir, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2870](https://github.com/urql-graphql/urql/pull/2870))
- ⚠️ Fix regression in `@urql/core`'s `stringifyDocument` that caused some formatted documents to not be reprinted, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2871](https://github.com/urql-graphql/urql/pull/2871))

## 3.1.0

### Minor Changes

- Implement `mapExchange`, which replaces `errorExchange`, allowing `onOperation` and `onResult` to be called to either react to or replace operations and results. For backwards compatibility, this exchange is also exported as `errorExchange` and supports `onError`, by [@kitten](https://github.com/kitten) (See [#2846](https://github.com/urql-graphql/urql/pull/2846))

### Patch Changes

- Move remaining `Variables` generics over from `object` default to `Variables extends AnyVariables = AnyVariables`. This has been introduced previously in [#2607](https://github.com/urql-graphql/urql/pull/2607) but some missing ports have been missed due to TypeScript not catching them previously. Depending on your TypeScript version the `object` default is incompatible with `AnyVariables`, by [@kitten](https://github.com/kitten) (See [#2843](https://github.com/urql-graphql/urql/pull/2843))
- Reuse output of `stringifyDocument` in place of repeated `print`. This will mean that we now prevent calling `print` repeatedly for identical operations and are instead only reusing the result once.
  This change has a subtle consequence of our internals. Operation keys will change due to this
  refactor and we will no longer sanitise strip newlines from queries that `@urql/core` has printed, by [@kitten](https://github.com/kitten) (See [#2847](https://github.com/urql-graphql/urql/pull/2847))
- Update to `wonka@^6.1.2` to fix memory leak in `fetch` caused in Node.js by a lack of clean up after initiating a request, by [@kitten](https://github.com/kitten) (See [#2850](https://github.com/urql-graphql/urql/pull/2850))

## 3.0.5

### Patch Changes

- Update typings of the client to encompass the changes of https://github.com/FormidableLabs/urql/pull/2692, by [@c-schwan](https://github.com/c-schwan) (See [#2758](https://github.com/FormidableLabs/urql/pull/2758))
- ⚠️ Fix case where our transform-debug-target babel plugin would override the root dispatchDebug in `compose.ts` with the latest found exchange, in this case `fetchExchange`, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2762](https://github.com/FormidableLabs/urql/pull/2762))

## 3.0.4

### Patch Changes

- ⚠️ Fix `ssrExchange` bug which prevented `staleWhileRevalidate` from sending off requests as network-only requests, and caused unrelated `network-only` operations to be dropped, by [@kitten](https://github.com/kitten) (See [#2691](https://github.com/FormidableLabs/urql/pull/2691))
- Allow URL limit for GET requests to be bypassed using `preferGetMethod: 'force'` rather than the default `true` or `'within-url-limit'` value, by [@kitten](https://github.com/kitten) (See [#2692](https://github.com/FormidableLabs/urql/pull/2692))
- ⚠️ Fix operation identities preventing users from deeply cloning operation contexts. Instead, we now use a client-wide counter (rolling over as needed).
  While this changes an internal data structure in `@urql/core` only, this change also affects the `offlineExchange` in `@urql/exchange-graphcache` due to it relying on the identity being previously an object rather than an integer, by [@kitten](https://github.com/kitten) (See [#2732](https://github.com/FormidableLabs/urql/pull/2732))

## 3.0.3

### Patch Changes

- ⚠️ Fix variable types in core makeOperation, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2665](https://github.com/FormidableLabs/urql/pull/2665))

## 3.0.2

### Patch Changes

- ⚠️ Fix case where `maskTypename` would not traverse down when the root query-field does not contain a `__typename`, by [@mlecoq](https://github.com/mlecoq) (See [#2643](https://github.com/FormidableLabs/urql/pull/2643))

## 3.0.1

### Patch Changes

- ⚠️ fix setting a client default requestPolicy, we set `context.requestPolicy: undefined`
  from our bindings which makes a spread override the client-set default, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2634](https://github.com/FormidableLabs/urql/pull/2634))

## 3.0.0

### Major Changes

- **Goodbye IE11!** 👋 This major release removes support for IE11. All code that is shipped will be transpiled much less and will _not_ be ES5-compatible anymore, by [@kitten](https://github.com/kitten) (See [#2504](https://github.com/FormidableLabs/urql/pull/2504))
- Remove support for options on the `Client` and `Client.createOperationContext`. We've noticed that there's no real need for `createOperationContext` or the options on the `Client` and that it actually encourages modifying properties on the `Client` that are really meant to be modified dynamically via exchanges, by [@kitten](https://github.com/kitten) (See [#2619](https://github.com/FormidableLabs/urql/pull/2619))
- Implement stricter variables types, which require variables to always be passed and match TypeScript types when the generic is set or inferred. This is a breaking change for TypeScript users potentially, unless all types are adhered to, by [@kitten](https://github.com/kitten) (See [#2607](https://github.com/FormidableLabs/urql/pull/2607))
- Upgrade to [Wonka v6](https://github.com/0no-co/wonka) (`wonka@^6.0.0`), which has no breaking changes but is built to target ES2015 and comes with other minor improvements.
  The library has fully been migrated to TypeScript which will hopefully help with making contributions easier!, by [@kitten](https://github.com/kitten) (See [#2504](https://github.com/FormidableLabs/urql/pull/2504))

### Minor Changes

- Remove the `babel-plugin-modular-graphql` helper, this because the graphql package hasn't converted to ESM yet which gives issues in node environments, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2551](https://github.com/FormidableLabs/urql/pull/2551))

## 2.6.1

### Patch Changes

- ⚠️ Fix missing React updates after an incoming response that schedules a mount. We now prevent dispatched operations from continuing to flush synchronously when the original source that runs the queue has terminated. This is important for the React bindings, because an update (e.g. `setState`) may recursively schedule a mount, which then disabled other `setState` updates from being processed. Previously we assumed that React used a trampoline scheduler for updates, however it appears that `setState` can recursively start more React work, by [@kitten](https://github.com/kitten) (See [#2556](https://github.com/FormidableLabs/urql/pull/2556))

## 2.6.0

### Minor Changes

- Allow providing a custom `isSubscriptionOperation` implementation, by [@n1ru4l](https://github.com/n1ru4l) (See [#2534](https://github.com/FormidableLabs/urql/pull/2534))

## 2.5.0

### Minor Changes

- Add `Accept` header to GraphQL HTTP requests. This complies to the specification but doesn't go as far as sending `Content-Type` which would throw a lot of APIs off. Instead, we'll now be sending an accept header for `application/graphql+json, application/json` to indicate that we comply with the GraphQL over HTTP protocol.
  This also fixes headers merging to allow overriding `Accept` and `Content-Type` regardless of the user options' casing, by [@kitten](https://github.com/kitten) (See [#2457](https://github.com/FormidableLabs/urql/pull/2457))

### Patch Changes

- Support aborting in `withPromise` cases, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2446](https://github.com/FormidableLabs/urql/pull/2446))
- Passthrough responses with content type of `text/*` as error messages, by [@kitten](https://github.com/kitten) (See [#2456](https://github.com/FormidableLabs/urql/pull/2456))

## 2.4.4

### Patch Changes

- cut off `url` when using the GET method at 2048 characters (lowest url-size coming from chromium), by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2384](https://github.com/FormidableLabs/urql/pull/2384))
- ⚠️ Fix issue where a synchronous `toPromise()` return would not result in the stream tearing down, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2386](https://github.com/FormidableLabs/urql/pull/2386))

## 2.4.3

### Patch Changes

- Prevent ignored characters in GraphQL queries from being replaced inside strings and block strings. Previously we accepted sanitizing strings via regular expressions causing duplicate hashes as acceptable, since it'd only be caused when a string wasn't extracted into variables. This is fixed now however, by [@kitten](https://github.com/kitten) (See [#2295](https://github.com/FormidableLabs/urql/pull/2295))

## 2.4.2

### Patch Changes

- Undo logic to catch errors from incremental fetching and forking the response stream, introduce logic
  to detect results, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2287](https://github.com/FormidableLabs/urql/pull/2287))

## 2.4.1

### Patch Changes

- ⚠️ Fix mutation operation being used as compared identity and instead add a stand-in comparison, by [@kitten](https://github.com/kitten) (See [#2228](https://github.com/FormidableLabs/urql/pull/2228))

## 2.4.0

### Minor Changes

- Allow for repeated mutations that have similar inputs which results in the same key, this is for instance the case with file uploads, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2189](https://github.com/FormidableLabs/urql/pull/2189))

### Patch Changes

- Bump `@graphql-typed-document-node/core` to 3.1.1 for `graphql@16` support, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2153](https://github.com/FormidableLabs/urql/pull/2153))
- ⚠️ Fix error bubbling, when an error happened in the exchange-pipeline we would treat it as a GraphQL-error, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2210](https://github.com/FormidableLabs/urql/pull/2210))
- Filter `network-only` requests from the `ssrExchange`, this is to enable `staleWhileRevalidated` queries to successfully dispatch their queries, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2198](https://github.com/FormidableLabs/urql/pull/2198))

## 2.3.6

### Patch Changes

- Extend peer dependency range of `graphql` to include `^16.0.0`.
  As always when upgrading across many packages of `urql`, especially including `@urql/core` we recommend you to deduplicate dependencies after upgrading, using `npm dedupe` or `npx yarn-deduplicate`, by [@kitten](https://github.com/kitten) (See [#2133](https://github.com/FormidableLabs/urql/pull/2133))

## 2.3.5

### Patch Changes

- ⚠️ Fix issue where `maskTypename` would ignore array shapes, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#2074](https://github.com/FormidableLabs/urql/pull/2074))

## 2.3.4

### Patch Changes

- Prevent `Buffer` from being polyfilled by an automatic detection in Webpack. Instead of referencing the `Buffer` global we now simply check the constructor name, by [@kitten](https://github.com/kitten) (See [#2027](https://github.com/FormidableLabs/urql/pull/2027))
- ⚠️ Fix error-type of an `ExecutionResult` to line up with subscription-libs, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#1998](https://github.com/FormidableLabs/urql/pull/1998))

## 2.3.3

### Patch Changes

- Adding option to `ssrExchange` to include the `extensions` field of operation results in the cache, by [@dios-david](https://github.com/dios-david) (See [#1985](https://github.com/FormidableLabs/urql/pull/1985))

## 2.3.2

### Patch Changes

- ⚠️ Fix issue where the ssr-exchange would loop due to checking network-only revalidations, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#1944](https://github.com/FormidableLabs/urql/pull/1944))

## 2.3.1

### Patch Changes

- ⚠️ Fix mark `query.__key` as non-enumerable so `formatDocument` does not restore previous invocations when cloning the gql-ast, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#1870](https://github.com/FormidableLabs/urql/pull/1870))
- ⚠️ Fix: update toPromise to exclude `hasNext` results. This change ensures that
  when we call toPromise() on a query we wont serve an incomplete result, the
  user will expect to receive a non-stale full-result when using toPromise(), by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#1880](https://github.com/FormidableLabs/urql/pull/1880))

## 2.3.0

### Minor Changes

- Add **experimental** support for `@defer` and `@stream` responses for GraphQL. This implements the ["GraphQL Defer and Stream Directives"](https://github.com/graphql/graphql-spec/blob/4fd39e0/rfcs/DeferStream.md) and ["Incremental Delivery over HTTP"](https://github.com/graphql/graphql-over-http/blob/290b0e2/rfcs/IncrementalDelivery.md) specifications. If a GraphQL API supports `multipart/mixed` responses for deferred and streamed delivery of GraphQL results, `@urql/core` (and all its derived fetch implementations) will attempt to stream results. This is _only supported_ on browsers [supporting streamed fetch responses](https://developer.mozilla.org/en-US/docs/Web/API/Response/body), which excludes IE11.
  The implementation of streamed multipart responses is derived from [`meros` by `@maraisr`](https://github.com/maraisr/meros), and is subject to change if the RFCs end up changing, by [@kitten](https://github.com/kitten) (See [#1854](https://github.com/FormidableLabs/urql/pull/1854))

## 2.2.0

### Minor Changes

- Add a `staleWhileRevalidate` option to the `ssrExchange`, which allows the client to immediately refetch a new result on hydration, which may be used for cached / stale SSR or SSG pages. This is different from using `cache-and-network` by default (which isn't recommended) as the `ssrExchange` typically acts like a "replacement fetch request", by [@kitten](https://github.com/kitten) (See [#1852](https://github.com/FormidableLabs/urql/pull/1852))

### Patch Changes

- ⚠️ Fix prevent mangling embedded strings in queries sent using the `GET` method, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#1851](https://github.com/FormidableLabs/urql/pull/1851))
- The [single-source behavior previously](https://github.com/FormidableLabs/urql/pull/1515) wasn't effective for implementations like React,
  where the issue presents itself when the state of an operation is first polled. This led to the operation being torn down erroneously.
  We now ensure that operations started at the same time still use a shared single-source, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#1850](https://github.com/FormidableLabs/urql/pull/1850))

## 2.1.6

### Patch Changes

- Warn for invalid operation passed to query/subscription/mutation, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#1829](https://github.com/FormidableLabs/urql/pull/1829))

## 2.1.5

### Patch Changes

- Prevent `ssrExchange().restoreData()` from adding results to the exchange that have already been invalidated. This may happen when `restoreData()` is called repeatedly, e.g. per page. When a prior run has already invalidated an SSR result then the result is 'migrated' to the user's `cacheExchange`, which means that `restoreData()` should never attempt to re-add it again, by [@kitten](https://github.com/kitten) (See [#1776](https://github.com/FormidableLabs/urql/pull/1776))
- ⚠️ Fix accidental change in passive `stale: true`, where a `cache-first` operation issued by Graphcache wouldn't yield an affected query and update its result to reflect the loading state with `stale: true`. This is a regression from `v2.1.0` and mostly becomes unexpected when `cache.invalidate(...)` is used, by [@kitten](https://github.com/kitten) (See [#1755](https://github.com/FormidableLabs/urql/pull/1755))

## 2.1.4

### Patch Changes

- Prevent stale results from being emitted by promisified query sources, e.g. `client.query(...).toPromise()` yielding a partial result with `stale: true` set. Instead, `.toPromise()` will now filter out stale results, by [@kitten](https://github.com/kitten) (See [#1709](https://github.com/FormidableLabs/urql/pull/1709))

## 2.1.3

### Patch Changes

- Treat empty variables the same as no variables in `@urql/core`'s `createRequest`, by [@kitten](https://github.com/kitten) (See [#1695](https://github.com/FormidableLabs/urql/pull/1695))

## 2.1.2

### Patch Changes

- ⚠️ Fix a condition under which the `Client` would hang when a query is started and consumed with `toPromise()`, by [@kitten](https://github.com/kitten) (See [#1634](https://github.com/FormidableLabs/urql/pull/1634))
- Refactor `Client` to hide some implementation details and to reduce size, by [@kitten](https://github.com/kitten) (See [#1638](https://github.com/FormidableLabs/urql/pull/1638))

## 2.1.1

### Patch Changes

- ⚠️ Fix a regression in `@urql/core@2.1.1` that prevented concurrent operations from being dispatched with differing request policies, which for instance prevented the explicit `executeQuery` calls on bindings to fail, by [@kitten](https://github.com/kitten) (See [#1626](https://github.com/FormidableLabs/urql/pull/1626))

## 2.1.0

### Minor Changes

- With the "single-source behavior" the `Client` will now also avoid executing an operation if it's already active, has a previous result available, and is either run with the `cache-first` or `cache-only` request policies. This is similar to a "short circuiting" behavior, where unnecessary work is avoided by not issuing more operations into the exchange pipeline than expected, by [@kitten](https://github.com/kitten) (See [#1600](https://github.com/FormidableLabs/urql/pull/1600))
- Add consistent "single-source behavior" which makes the `Client` more forgiving when duplicate
  sources are used, which previously made it difficult to use the same operation across an app
  together with `cache-and-network`; This was a rare use-case, and it isn't recommended to overfetch
  data across an app, however, the new `Client` implementation of shared sources ensures that when an
  operation is active that the `Client` distributes the last known result for the active operation to
  any new usages of it (which is called “replaying stale results”) (See [#1515](https://github.com/FormidableLabs/urql/pull/1515))

### Patch Changes

- Remove closure-compiler from the build step (See [#1570](https://github.com/FormidableLabs/urql/pull/1570))
- ⚠️ Fix inconsistency in generating keys for `DocumentNode`s, especially when using GraphQL Code Generator, which could cause SSR serialization to fail, by [@zenflow](https://github.com/zenflow) (See [#1509](https://github.com/FormidableLabs/urql/pull/1509))

## 2.0.0

### Major Changes

- **Breaking**: Remove `pollInterval` feature from `OperationContext`. Instead consider using a source that uses `Wonka.interval` and `Wonka.switchMap` over `client.query()`'s source, by [@kitten](https://github.com/kitten) (See [#1374](https://github.com/FormidableLabs/urql/pull/1374))
- Remove deprecated `operationName` property from `Operation`s. The new `Operation.kind` property is now preferred. If you're creating new operations you may also use the `makeOperation` utility instead.
  When upgrading `@urql/core` please ensure that your package manager didn't install any duplicates of it. You may deduplicate it manually using `npx yarn-deduplicate` (for Yarn) or `npm dedupe` (for npm), by [@kitten](https://github.com/kitten) (See [#1357](https://github.com/FormidableLabs/urql/pull/1357))

### Minor Changes

- Reemit an `OperationResult` as `stale: true` if it's being reexecuted as `network-only` operation to give bindings immediate feedback on background refetches, by [@kitten](https://github.com/kitten) (See [#1375](https://github.com/FormidableLabs/urql/pull/1375))

## 1.16.2

### Patch Changes

- Add a workaround for `graphql-tag/loader`, which provides filtered query documents (where the original document contains multiple operations) without updating or providing a correct `document.loc.source.body` string, by [@kitten](https://github.com/kitten) (See [#1315](https://github.com/FormidableLabs/urql/pull/1315))

## 1.16.1

### Patch Changes

- Add fragment deduplication to `gql` tag. Identical fragments can now be interpolated multiple times without a warning being triggered or them being duplicated in `gql`'s output, by [@kitten](https://github.com/kitten) (See [#1225](https://github.com/FormidableLabs/urql/pull/1225))

## 1.16.0

### Minor Changes

- Add a built-in `gql` tag function helper to `@urql/core`. This behaves similarly to `graphql-tag` but only warns about _locally_ duplicated fragment names rather than globally. It also primes `@urql/core`'s key cache with the parsed `DocumentNode`, by [@kitten](https://github.com/kitten) (See [#1187](https://github.com/FormidableLabs/urql/pull/1187))

### Patch Changes

- ⚠️ Fix edge case in `formatDocument`, which fails to add a `__typename` field if it has been aliased to a different name, by [@kitten](https://github.com/kitten) (See [#1186](https://github.com/FormidableLabs/urql/pull/1186))
- Cache results of `formatDocument` by the input document's key, by [@kitten](https://github.com/kitten) (See [#1186](https://github.com/FormidableLabs/urql/pull/1186))

## 1.15.2

### Patch Changes

- Don't add `undefined` to any property of the `ssrExchange`'s serialized results, as this would crash in Next.js, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#1168](https://github.com/FormidableLabs/urql/pull/1168))

## 1.15.1

### Patch Changes

- Export `getOperationName` from `@urql/core` and use it in `@urql/exchange-execute`, fixing several imports, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#1135](https://github.com/FormidableLabs/urql/pull/1135))

## 1.15.0

### Minor Changes

- Improve the Suspense implementation, which fixes edge-cases when Suspense is used with subscriptions, partially disabled, or _used on the client-side_. It has now been ensured that client-side suspense functions without the deprecated `suspenseExchange` and uncached results are loaded consistently. As part of this work, the `Client` itself does now never throw Suspense promises anymore, which is functionality that either way has no place outside of the React/Preact bindings, by [@kitten](https://github.com/kitten) (See [#1123](https://github.com/FormidableLabs/urql/pull/1123))

### Patch Changes

- Use `Record` over `object` type for subscription operation variables. The `object` type is currently hard to use ([see this issue](https://github.com/microsoft/TypeScript/issues/21732)), by [@enisdenjo](https://github.com/enisdenjo) (See [#1119](https://github.com/FormidableLabs/urql/pull/1119))
- Add support for `TypedDocumentNode` to infer the type of the `OperationResult` and `Operation` for all methods, functions, and hooks that either directly or indirectly accept a `DocumentNode`. See [`graphql-typed-document-node` and the corresponding blog post for more information.](https://github.com/dotansimha/graphql-typed-document-node), by [@kitten](https://github.com/kitten) (See [#1113](https://github.com/FormidableLabs/urql/pull/1113))
- Refactor `useSource` hooks which powers `useQuery` and `useSubscription` to improve various edge case behaviour. This will not change the behaviour of these hooks dramatically but avoid unnecessary state updates when any updates are obviously equivalent and the hook will furthermore improve continuation from mount to effects, which will fix cases where the state between the mounting and effect phase may slightly change, by [@kitten](https://github.com/kitten) (See [#1104](https://github.com/FormidableLabs/urql/pull/1104))

## 1.14.1

### Patch Changes

- ⚠️ Fix the production build overwriting the development build. Specifically in the previous release we mistakenly replaced all development bundles with production bundles. This doesn't have any direct influence on how these packages work, but prevented development warnings from being logged or full errors from being thrown, by [@kitten](https://github.com/kitten) (See [#1097](https://github.com/FormidableLabs/urql/pull/1097))

## 1.14.0

This version of `@urql/core` renames `Operation.operationName` to `Operation.kind`. For now the old
property is merely deprecated and will issue a warning if it's used directly. That said, all
exchanges that are released today also need this new version of `@urql/core@>=1.14.0`, so if you
upgrade to any of the following packages, you will also need to upgrade `@urql/core`. If you upgrade
and see the deprecation warning, check whether all following exchanges have been upgraded:

- `@urql/exchange-auth@0.1.2`
- `@urql/exchange-execute@1.0.2`
- `@urql/exchange-graphcache@3.1.8`
- `@urql/exchange-multipart-fetch@0.1.10`
- `@urql/exchange-persisted-fetch@1.2.2`
- `@urql/exchange-populate@0.2.1`
- `@urql/exchange-refocus@0.2.1`
- `@urql/exchange-retry@0.1.9`
- `@urql/exchange-suspense@1.9.2`

Once you've upgraded `@urql/core` please also ensure that your package manager hasn't accidentally
duplicated the `@urql/core` package. If you're using `npm` you can do so by running `npm dedupe`,
and if you use `yarn` you can do so by running `yarn-deduplicate`.

If you have a custom exchange, you can mute the deprecation warning by using `Operation.kind` rather
than `Operation.operationName`. If these exchanges are copying or altering operations by spreading
them this will also trigger the warning, which you can fix by using [the new `makeOperation` helper
function.](https://formidable.com/open-source/urql/docs/api/core/#makeoperation)

### Minor Changes

- Deprecate the `Operation.operationName` property in favor of `Operation.kind`. This name was
  previously confusing as `operationName` was effectively referring to two different things. You can
  safely upgrade to this new version, however to mute all deprecation warnings you will have to
  **upgrade** all `urql` packages you use. If you have custom exchanges that spread operations, please
  use [the new `makeOperation` helper
  function](https://formidable.com/open-source/urql/docs/api/core/#makeoperation) instead, by [@bkonkle](https://github.com/bkonkle) (See [#1045](https://github.com/FormidableLabs/urql/pull/1045))

### Patch Changes

- Add missing `.mjs` extension to all imports from `graphql` to fix Webpack 5 builds, which require extension-specific import paths for ESM bundles and packages. **This change allows you to safely upgrade to Webpack 5.**, by [@kitten](https://github.com/kitten) (See [#1094](https://github.com/FormidableLabs/urql/pull/1094))

## 1.13.1

### Patch Changes

- Allow `client.reexecuteOperation` to be called with mutations which skip the active operation minimums, by [@kitten](https://github.com/kitten) (See [#1011](https://github.com/FormidableLabs/urql/pull/1011))

## 1.13.0

Please note that this release changes the data structure of the `ssrExchange`'s
output. We don't treat this as a breaking change, since this data is considered
a private structure, but if your tests or other code relies on this, please check
the type changes and update it.

### Minor Changes

- Adds an error exchange to urql-core. This allows tapping into all graphql errors within the urql client. Useful for logging, debugging, handling authentication errors etc, by [@kadikraman](https://github.com/kadikraman) (See [#947](https://github.com/FormidableLabs/urql/pull/947))

### Patch Changes

- ⚠️ Fix condition where mutated result data would be picked up by the `ssrExchange`, for instance as a result of mutations by Graphcache. Instead the `ssrExchange` now serializes data early, by [@kitten](https://github.com/kitten) (See [#962](https://github.com/FormidableLabs/urql/pull/962))
- Omit the `Content-Type: application/json` HTTP header when using GET in the `fetchExchange`, `persistedFetchExchange`, or `multipartFetchExchange`, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#957](https://github.com/FormidableLabs/urql/pull/957))

## 1.12.3

### Patch Changes

- Remove whitespace and comments from string-queries, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#911](https://github.com/FormidableLabs/urql/pull/911))
- Remove redundant whitespaces when using GET for graphql queries, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#908](https://github.com/FormidableLabs/urql/pull/908))

## 1.12.2

### Patch Changes

- ⚠️ Fix `formatDocument` mutating parts of the `DocumentNode` which may be shared by other documents and queries. Also ensure that a formatted document will always generate the same key in `createRequest` as the original document, by [@kitten](https://github.com/kitten) (See [#880](https://github.com/FormidableLabs/urql/pull/880))
- ⚠️ Fix `ssrExchange` invalidating results on the client-side too eagerly, by delaying invalidation by a tick, by [@kitten](https://github.com/kitten) (See [#885](https://github.com/FormidableLabs/urql/pull/885))

## 1.12.1

### Patch Changes

- ⚠️ Fix timing for out-of-band `client.reexecuteOperation` calls. This would surface in asynchronous caching scenarios, where no result would be delivered by the cache synchronously, while it still calls `client.reexecuteOperation` for e.g. a `network-only` request, which happens for `cache-and-network`. This issue becomes especially obvious in highly synchronous frameworks like Svelte, by [@kitten](https://github.com/kitten) (See [#860](https://github.com/FormidableLabs/urql/pull/860))
- Replace unnecessary `scheduleTask` polyfill with inline `Promise.resolve().then(fn)` calls, by [@kitten](https://github.com/kitten) (See [#861](https://github.com/FormidableLabs/urql/pull/861))

## 1.12.0

As always, please ensure that you deduplicate `@urql/core` when upgrading. Additionally
deduplicating the versions of `wonka` that you have installed may also reduce your bundlesize.

### Minor Changes

- Expose a `client.subscription` shortcut method, similar to `client.query` and `client.mutation`, by [@FredyC](https://github.com/FredyC) (See [#838](https://github.com/FormidableLabs/urql/pull/838))

### Patch Changes

- Upgrade to a minimum version of wonka@^4.0.14 to work around issues with React Native's minification builds, which use uglify-es and could lead to broken bundles, by [@kitten](https://github.com/kitten) (See [#842](https://github.com/FormidableLabs/urql/pull/842))

## 1.11.8

### Patch Changes

- Add operationName to GET queries, by [@jakubriedl](https://github.com/jakubriedl) (See [#798](https://github.com/FormidableLabs/urql/pull/798))

## 1.11.7

### Patch Changes

- Add `source` debug name to all `dispatchDebug` calls during build time to identify events by which exchange dispatched them, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#780](https://github.com/FormidableLabs/urql/pull/780))

## 1.11.6

### Patch Changes

- Add a `"./package.json"` entry to the `package.json`'s `"exports"` field for Node 14. This seems to be required by packages like `rollup-plugin-svelte` to function properly, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#771](https://github.com/FormidableLabs/urql/pull/771))

## 1.11.5

### Patch Changes

- Hoist variables in unminified build output for Metro Bundler builds which otherwise fails for `process.env.NODE_ENV` if-clauses, by [@kitten](https://github.com/kitten) (See [#737](https://github.com/FormidableLabs/urql/pull/737))
- Add a babel-plugin that removes empty imports from the final build output, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#735](https://github.com/FormidableLabs/urql/pull/735))

## 1.11.4

### Patch Changes

Sorry for the many updates; Please only upgrade to `>=1.11.4` and don't use the deprecated `1.11.3`
and `1.11.2` release.

- ⚠️ Fix nested package path for @urql/core/internal and @urql/exchange-graphcache/extras, by [@kitten](https://github.com/kitten) (See [#734](https://github.com/FormidableLabs/urql/pull/734))

## 1.11.3

### Patch Changes

- Make the extension of the main export unknown, which fixes a Webpack issue where the resolver won't pick `module` fields in `package.json` files once it's importing from another `.mjs` file, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#733](https://github.com/FormidableLabs/urql/pull/733))

## 1.11.1

### Patch Changes

- ⚠️ Fix missing `@urql/core/internal` entrypoint in the npm-release, which was previously not included, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#731](https://github.com/FormidableLabs/urql/pull/731))

## 1.11.0

### Minor Changes

- Add debugging events to exchanges that add more detailed information on what is happening
  internally, which will be displayed by devtools like the urql [Chrome / Firefox extension](https://github.com/FormidableLabs/urql-devtools), by [@andyrichardson](https://github.com/andyrichardson) (See [#608](https://github.com/FormidableLabs/urql/pull/608))
- Add @urql/core/internal entrypoint for internally shared utilities and start sharing fetchExchange-related code, by [@kitten](https://github.com/kitten) (See [#722](https://github.com/FormidableLabs/urql/pull/722))

### Patch Changes

- ⚠️ Fix stringifyVariables breaking on x.toJSON scalars, by [@kitten](https://github.com/kitten) (See [#718](https://github.com/FormidableLabs/urql/pull/718))

## 1.10.9

### Patch Changes

- Pick modules from graphql package, instead of importing from graphql/index.mjs, by [@kitten](https://github.com/kitten) (See [#700](https://github.com/FormidableLabs/urql/pull/700))

## 1.10.8

### Patch Changes

- Add graphql@^15.0.0 to peer dependency range, by [@kitten](https://github.com/kitten) (See [#688](https://github.com/FormidableLabs/urql/pull/688))
- ⚠️ Fix non-2xx results never being parsed as GraphQL results. This can result in valid GraphQLErrors being hidden, which should take precedence over generic HTTP NetworkErrors, by [@kitten](https://github.com/kitten) (See [#678](https://github.com/FormidableLabs/urql/pull/678))

## 1.10.7

### Patch Changes

- ⚠️ Fix oversight in edge case for #662. The operation queue wasn't marked as being active which caused `stale` results and `cache-and-network` operations from reissuing operations immediately (unqueued essentially) which would then be filtered out by the `dedupExchange`, by [@kitten](https://github.com/kitten) (See [#669](https://github.com/FormidableLabs/urql/pull/669))

## 1.10.6

### Patch Changes

- ⚠️ Fix critical bug in operation queueing that can lead to unexpected teardowns and swallowed operations. This would happen when a teardown operation kicks off the queue, by [@kitten](https://github.com/kitten) (See [#662](https://github.com/FormidableLabs/urql/pull/662))

## 1.10.5

### Patch Changes

- Refactor a couple of core helpers for minor bundlesize savings, by [@kitten](https://github.com/kitten) (See [#658](https://github.com/FormidableLabs/urql/pull/658))
- Add support for variables that contain non-plain objects without any enumerable keys, e.g. `File` or `Blob`. In this case `stringifyVariables` will now use a stable (but random) key, which means that mutations containing `File`s — or other objects like this — will now be distinct, as they should be, by [@kitten](https://github.com/kitten) (See [#650](https://github.com/FormidableLabs/urql/pull/650))

## 1.10.4

### Patch Changes

- ⚠️ Fix node resolution when using Webpack, which experiences a bug where it only resolves
  `package.json:main` instead of `module` when an `.mjs` file imports a package, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#642](https://github.com/FormidableLabs/urql/pull/642))

## 1.10.3

### Patch Changes

- ⚠️ Fix Node.js Module support for v13 (experimental-modules) and v14. If your bundler doesn't support
  `.mjs` files and fails to resolve the new version, please double check your configuration for
  Webpack, or similar tools, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#637](https://github.com/FormidableLabs/urql/pull/637))

## 1.10.2

### Patch Changes

- Add a guard to "maskTypenames" so a null value isn't considered an object, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#621](https://github.com/FormidableLabs/urql/pull/621))

## 1.10.1

### Patch Changes

- ⚠️ Fix Rollup bundle output being written to .es.js instead of .esm.js, by [@kitten](https://github.com/kitten) (See [#609](https://github.com/FormidableLabs/urql/pull/609))

## 1.10.0

### Minor Changes

- Add `additionalTypenames` to the `OperationContext`, which allows the document cache to invalidate efficiently when the `__typename` is unknown at the initial fetch, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#601](https://github.com/FormidableLabs/urql/pull/601)) [You can learn more about this change in our docs.](https://formidable.com/open-source/urql/docs/basics/document-caching/#adding-typenames)

### Patch Changes

- Add missing GraphQLError serialization for extensions and path field to ssrExchange, by [@kitten](https://github.com/kitten) (See [#607](https://github.com/FormidableLabs/urql/pull/607))

## 1.9.2

### Patch Changes

- Prevent active teardowns for queries on subscriptionExchange, by [@kitten](https://github.com/kitten) (See [#577](https://github.com/FormidableLabs/urql/pull/577))

## 1.9.1

### Patch Changes

- ⚠️ Fix `cache-only` operations being forwarded and triggering fetch requests, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#551](https://github.com/FormidableLabs/urql/pull/551))
- Adds a one-tick delay to the subscriptionExchange to prevent unnecessary early tear downs, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#542](https://github.com/FormidableLabs/urql/pull/542))
- Add enableAllOperations option to subscriptionExchange to let it handle queries and mutations as well, by [@kitten](https://github.com/kitten) (See [#544](https://github.com/FormidableLabs/urql/pull/544))

## 1.9.0

### Minor Changes

- Adds the `maskTypename` export to urql-core, this deeply masks typenames from the given payload.
  Masking `__typename` properties is also available as a `maskTypename` option on the `Client`. Setting this to true will
  strip typenames from results, by [@JoviDeCroock](https://github.com/JoviDeCroock) (See [#533](https://github.com/FormidableLabs/urql/pull/533))
- Add support for sending queries using GET instead of POST method (See [#519](https://github.com/FormidableLabs/urql/pull/519))
- Add client.readQuery method (See [#518](https://github.com/FormidableLabs/urql/pull/518))

### Patch Changes

- ⚠️ Fix ssrExchange not serialising networkError on CombinedErrors correctly. (See [#515](https://github.com/FormidableLabs/urql/pull/515))
- Add explicit error when creating Client without a URL in development. (See [#512](https://github.com/FormidableLabs/urql/pull/512))
