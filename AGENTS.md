## Configuration Format
Templates are defined by `NucleiTemplateConfig` instances persisted through `NucleiConfigManager`. Keep field names stable so existing JSON configuration files remain valid.

## Montoya API Access
Because direct MCP access is unavailable, fetch Montoya API documentation via HTTP GET requests to Context7 when you need clarification.

**Endpoint template**
```
https://context7.com/api/v1/portswigger/burp-extensions-montoya-api?type=json&tokens=100000&topic=<TOPIC>
```

**Usage guidelines**
- Form topics with 2–4 technical keywords (e.g., `ui%20suite%20tab`, `http%20request%20builder`).
- Query before changing Montoya-dependent logic or when encountering compilation errors tied to Montoya classes.
- Parse the JSON response and extract method signatures or examples relevant to the task at hand.
- Retry with refined terms if the response lacks the needed details.

## Logging & Diagnostics
- Use `api.logging().logToOutput()` for informational messages and `logToError()` for failures.
- Prefer structured log prefixes (e.g., `[AutoChecker]`) so Burp users can filter messages.
- Async errors should be routed through the logging API within completion handlers.

## Compatibility & Dependencies
- Kotlin JVM toolchain pinned to 21—keep it aligned with the Burp Suite runtime.
- Montoya API dependency is `net.portswigger.burp.extensions:montoya-api:2025.4`; update in lockstep with Burp releases and test against the latest Montoya SDK.
- Avoid adding extra dependencies unless absolutely necessary; bundle everything through the shadow JAR to prevent classpath issues for users.
