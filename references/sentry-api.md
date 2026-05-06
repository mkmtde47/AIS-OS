# Sentry Error Tracking

## Project: Sheahaircare

**DSN:** `https://8d79134658b58b3e92629717e66a30a8@o4511344634298368.ingest.us.sentry.io/4511344635543552`

**Free tier:** 5,000 errors/month per project

## Dashboard

[Sentry Dashboard](https://sentry.io/organizations/mkm/issues/?project=4511344635543552)

## Integration (Next.js)

### 1. Install Sentry SDK

```bash
npm install @sentry/nextjs
```

### 2. Initialize in `app/layout.tsx` or `instrumentation.ts`

```typescript
import * as Sentry from "@sentry/nextjs";

Sentry.init({
  dsn: process.env.NEXT_PUBLIC_SENTRY_DSN,
  environment: process.env.NODE_ENV,
  tracesSampleRate: 1.0,
});
```

### 3. Set environment variable

In `.env.local`:
```
NEXT_PUBLIC_SENTRY_DSN=https://8d79134658b58b3e92629717e66a30a8@o4511344634298368.ingest.us.sentry.io/4511344635543552
```

### 4. Capture errors manually

```typescript
try {
  // your code
} catch (error) {
  Sentry.captureException(error);
}
```

## What gets tracked automatically

- Uncaught exceptions
- Unhandled promise rejections
- Performance monitoring
- Page load metrics
- API errors

## When to check Sentry

1. After deploying to production
2. When users report issues
3. Before each release (check for regressions)

## Links

- [Sentry Docs](https://docs.sentry.io/platforms/javascript/guides/nextjs/)
- [Your Sentry Organization](https://sentry.io/organizations/mkm/)
