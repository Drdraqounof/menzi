# Troubleshooting: Next.js `legacyBehavior` Console Error in Link Component

## Error Type
Console Error

## Error Message
```
`legacyBehavior` is deprecated and will be removed in a future release. A codemod is available to upgrade your components:

npx @next/codemod@latest new-link .

Learn more: https://nextjs.org/docs/app/building-your-application/upgrading/codemods#remove-a-tags-from-link-components

    at FeedPage (app/feed/page.tsx:189:13)
```

## Code Frame
```
  187 |               <Home className="w-5 h-5" />
  188 |             </button>
> 189 |             <Link href="/trending" passHref legacyBehavior>
      |             ^
  190 |               <button className="w-full flex items-center justify-start gap-3 hover:bg-secondary rounded px-3 py-2" aria-label="Trending">
  191 |                 <TrendingUp className="w-5 h-5" />
  192 |               </button>
```

## Cause
- The `legacyBehavior` prop on the Next.js `<Link>` component is deprecated and will be removed in future releases.
- Using `legacyBehavior` is not needed in modern Next.js (v13+ with the app directory).
- Wrapping a `<button>` inside a `<Link>` with `legacyBehavior` is not recommended and causes warnings/errors.

## Solution
- Remove `legacyBehavior` and `passHref` from the `<Link>` component.
- Instead, use `<Link>` directly with your button styles, or use a `<button>` with a router push for navigation.
- For icon-only sidebar navigation, use `<Link>` as a wrapper and apply button styles to the `<Link>` itself.

### Before (Deprecated)
```tsx
<Link href="/trending" passHref legacyBehavior>
  <button className="...">...</button>
</Link>
```

### After (Fixed)
```tsx
<Link href="/trending" className="w-full flex items-center justify-start gap-3 hover:bg-secondary rounded px-3 py-2" aria-label="Trending">
  <TrendingUp className="w-5 h-5" />
</Link>
```

## How It Was Fixed
- The sidebar Trending button was refactored to use `<Link>` directly with all button styles and accessibility props.
- This removes the deprecated `legacyBehavior` and prevents future errors or warnings.

## References
- [Next.js Link Component Upgrade Guide](https://nextjs.org/docs/app/building-your-application/upgrading/codemods#remove-a-tags-from-link-components)
- [Next.js Link Documentation](https://nextjs.org/docs/app/api-reference/components/link)
