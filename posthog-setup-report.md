<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the DevEvents Next.js App Router project. The following changes were made:

- **`instrumentation-client.ts`** (new file): Initializes PostHog client-side using the Next.js 15.3+ instrumentation API. Configured with a reverse proxy path (`/ingest`), error tracking (`capture_exceptions`), and debug mode in development.
- **`next.config.ts`**: Added PostHog reverse proxy rewrites so analytics requests route through `/ingest` (improves ad-blocker resistance and data accuracy). Also set `skipTrailingSlashRedirect: true` as required by PostHog.
- **`components/ExploreBtn.tsx`**: Added `posthog.capture('explore_events_clicked')` on button click — captures the top of the event discovery funnel.
- **`components/EventCard.tsx`**: Added `posthog.capture('event_card_clicked', { ... })` on link click — captures which specific events users are interested in, with rich properties (title, slug, location, date, time). Also added `'use client'` directive since it now uses an event handler.
- **`.env.local`** (new file): Contains `NEXT_PUBLIC_POSTHOG_KEY` and `NEXT_PUBLIC_POSTHOG_HOST` environment variables (never hardcoded in source).
- **Packages installed**: `posthog-js` (client-side SDK) and `posthog-node` (server-side SDK, ready for future API routes).

| Event Name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicked the "Explore Events" CTA button — top of the event discovery funnel | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicked on an event card to view details — indicates interest in a specific event. Properties: `event_title`, `event_slug`, `event_location`, `event_date`, `event_time` | `components/EventCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard — Analytics basics**: https://us.posthog.com/project/320416/dashboard/1298817
- **Event discovery funnel: Explore → Event click**: https://us.posthog.com/project/320416/insights/UXIgsD9L
- **User engagement trend: Explore & Event Card clicks**: https://us.posthog.com/project/320416/insights/ojdqLbdB
- **Most popular events by clicks**: https://us.posthog.com/project/320416/insights/ZtClL09L
- **Unique users exploring events**: https://us.posthog.com/project/320416/insights/xAqARJSv
- **Event clicks by location**: https://us.posthog.com/project/320416/insights/ZANBxp1Q

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
