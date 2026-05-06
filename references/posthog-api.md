# Posthog Analytics

## Project Details

**Project Token:** `[YOUR_POSTHOG_PROJECT_TOKEN]`

**Organization:** FL4LL

**Environment:** Production

## Dashboard

[Posthog Dashboard](https://[YOUR_POSTHOG_DOMAIN]/projects/[PROJECT_ID])

## Integration (Next.js)

### 1. Install SDK

```bash
npm install posthog-js
```

### 2. Initialize in `app/layout.tsx`

```typescript
import posthog from 'posthog-js'

if (typeof window !== 'undefined') {
  posthog.init(
    process.env.NEXT_PUBLIC_POSTHOG_KEY,
    { api_host: process.env.NEXT_PUBLIC_POSTHOG_HOST }
  )
}
```

### 3. Environment variables

In `.env.local`:
```
NEXT_PUBLIC_POSTHOG_KEY=[YOUR_PROJECT_TOKEN]
NEXT_PUBLIC_POSTHOG_HOST=https://[YOUR_POSTHOG_DOMAIN]
```

## Key Events to Track

- `user_signup` — new user registration
- `app_launch` — app opened
- `purchase_initiated` — payment flow started
- `purchase_completed` — payment successful
- `feature_used` — feature interaction

## Capturing Events

```typescript
import { usePostHog } from 'posthog-js/react'

const MyComponent = () => {
  const posthog = usePostHog()
  
  const handleClick = () => {
    posthog.capture('button_clicked', {
      button_name: 'signup',
      user_id: userId
    })
  }
}
```

## Links

- [Posthog Docs](https://posthog.com/docs)
- [React Integration](https://posthog.com/docs/libraries/react)
