# Testing Parallel Routes for Breadcrumbs

With the Release of [Next 15 RC](https://nextjs.org/blog/next-15-rc) this issue has been resolved

## Updated to fix static + dynamic routes

[Provide non-dynamic segments to catch-all parallel routes](https://github.com/vercel/next.js/pull/65233)

Now when I visit `http://localhost:3000/blog/test` I get `blog` in the path params

```
rendering in @breadcrumbs / BreadcrumbSlot { params: { catchAll: [ 'blog', 'hello-world' ] }, searchParams: {} }
GET /blog/test 200 in 615ms
```

## Original PR and issue

[support breadcrumb style catch-all parallel routes #65063](https://github.com/vercel/next.js/pull/65063)

This PR that landed in the canary helps to support Breadcrumbs through parallel routes. It appears
to work for dynamic routes only. The setup of this project is to test that.

The structure of this project has `@breadcrumbs/[...catchAll]/page.tsx` to capture the path for the breadcrumbs.

Then we have two sets of nested paths
* `[name]/[last]/page.tsx`
* `blog/[slug]/page.tsx`

When I visit `http://localhost:3000/jeremy/kreutzbender` I receive both params

```
rendering in @breadcrumbs / BreadcrumbSlot {
  params: { catchAll: [ 'jeremy', 'kreutzbender' ] },
  searchParams: {}
}
GET /jeremy/kreutzbender 200 in 937ms
```

Then when I visit `http://localhost:3000/blog/test` I do not get `blog` in the path params

```
rendering in @breadcrumbs / BreadcrumbSlot { params: { catchAll: [ 'test' ] }, searchParams: {} }
GET /blog/test 200 in 34ms
```

My question is whether this is in the intended behavior. If so, how would I build my breadcrumbs component
to incorporate `Blog` into it?
