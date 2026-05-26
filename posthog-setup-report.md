<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog into the DevEvent Next.js App Router project. The following changes were made:

- **`instrumentation-client.ts`** (new): Initializes PostHog client-side using the `posthog-js` SDK via Next.js 15.3+ instrumentation API. Configured with a reverse proxy (`/ingest`), exception capture for error tracking, and debug mode in development.
- **`next.config.ts`** (updated): Added `/ingest` reverse proxy rewrites for PostHog ingestion and static assets, plus `skipTrailingSlashRedirect: true` to support PostHog trailing-slash API requests.
- **`components/ExploreBtn.tsx`** (updated): Added `posthog.capture('explore_events_clicked')` on button click to track when users express intent to browse events.
- **`components/EventCard.tsx`** (updated): Added `'use client'` directive and `posthog.capture('event_card_clicked', { event_title, event_slug, event_location, event_date })` on card click to track which events users are most interested in.
- **`.env.local`** (updated): Added `NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN` and `NEXT_PUBLIC_POSTHOG_HOST` environment variables.

## Tracked events

| Event name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicks the 'Explore Events' button on the homepage hero section | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicks on an event card to view event details (with title, slug, location, date properties) | `components/EventCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- [Analytics basics dashboard](/dashboard/1626747)
- [Explore Events clicks over time](/insights/33Dtaw89) — Daily trend of the Explore Events button being clicked
- [Event card clicks over time](/insights/lx2153yg) — Daily trend of event card clicks
- [Unique users exploring events](/insights/fmG5TNhb) — Total unique daily users clicking Explore Events (last 30 days)
- [Discovery to event click funnel](/insights/PNoW4mYu) — Conversion funnel from Explore Events → event card click
- [Most clicked events](/insights/VyLz03GW) — Bar chart of which event cards get clicked most, broken down by event title

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
