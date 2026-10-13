## 16. Performance

- **Measure first:** Lighthouse, WebPageTest, Chrome Performance panel, React Profiler, and Core Web Vitals (LCP, INP, CLS) from real users.
- **Bundle size:** analyze with a visualizer (`rollup-plugin-visualizer` for Vite, `source-map-explorer`, or `@next/bundle-analyzer`). Code-split routes with `React.lazy` and dynamic imports. Replace heavy libraries (moment with dayjs or Intl). Watch for whole-library imports; prefer ES module builds (`lodash-es`).
- **Images and fonts:** modern formats (WebP, AVIF), correct sizes, lazy loading, priority for the LCP image, `font-display: swap`, subset fonts.
- **Lists:** virtualize long lists (TanStack Virtual, react-window); paginate or infinite-scroll server data.
- **Re-renders:** colocate state, split contexts, select narrowly with `useAppSelector` and `selectFromResult`, memoize expensive selectors. Do not memoize everything; profile.
- **Interactions:** debounce and throttle expensive handlers; use `startTransition` or `useDeferredValue` for heavy updates.
- **Network:** cache with RTK Query, prefetch likely navigation, compress (Brotli), use HTTP caching and a CDN, avoid request waterfalls.
- **Budgets in CI:** `size-limit` or Lighthouse CI so regressions are caught in MRs.
