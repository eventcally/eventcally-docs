---
title: API Rate Limit
lang: de
redirect_from: /goto/dev-api-rate-limit/
---
Für den API-Zugriff gibt es verschiedene Rate-Limits.

Die Rate-Limits können in den Headers der HTTP Response ausgelesen werden. Sie beginnen mit `X-RateLimit-`.

Die Rate-Limits sind dynamisch. Im Vergleich zu API Schlüsseln haben Anfragen per OAuth ein deutlich höheres Limit.

Bitte beachte die Informationen zur [Authorisierung]({% post_url /developer/2023-05-23-api-authorization %}).
