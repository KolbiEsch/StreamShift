# StreamShift

A service where users input a watchlist of movies that they want to see but don't want to pay rental fees for. StreamShift connects to the TMDB and JustWatch APIs and notifies the user when a movie on their watchlist is on a streaming service they subscribe to.

```mermaid
graph TD
    Client[React TS Frontend] -->|HTTPS / REST API| API[.NET C# Web API]
    
    subgraph Backend Services
    API -->|Read/Write| DB[(PostgreSQL)]
    Worker[Background Worker / Hangfire] -->|Read/Write| DB
    Worker -->|Fetch Data| TMDB[TMDB / JustWatch API]
    Worker -->|Trigger| Email[Email Service - SendGrid]
    end

    API -->|Auth| AuthProvider[Identity/JWT]
```
