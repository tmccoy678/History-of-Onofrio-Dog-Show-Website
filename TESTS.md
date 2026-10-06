# Robustness tests: `execpgm/fndindex` input handling

**Date:** 2026-10-06
**Target:** `http://www.onofrio.com/execpgm/fndindex`
**Method:** Single benign HTTP GET requests with varied `show` parameters.
No fuzzing, no authentication attempts, no write operations.

## Results

| Request | Response | Notes |
|---------|----------|-------|
| `?show=PL2026101411BH` (valid) | **200**, ~32 KB page | Normal show page |
| `?show=TEST` (bogus) | **500** | Generic Apache 500 page; no stack trace, paths, or backend details disclosed |
| `?show=` (empty) | **500** | Same generic 500 page |
| *(no parameters)* | **200** | Index/default page loads fine |
| `?show=PL2026101411BH%27` (valid + encoded `'`) | **200** | Handled without error |

## Interpretation

- Malformed or empty `show` values reach the backend program unvalidated and
  cause an unhandled error (HTTP 500).
- The 500 response body is the stock Apache error page — **no information
  disclosure** observed (no paths, stack traces, or backend identifiers).
- The encoded-quote case returning 200 suggests at least some input handling
  exists for that shape; the failure mode is specifically empty/nonsense
  values, not metacharacters.

## Recommendation (as sent to Onofrio)

Validate the `show` parameter before it reaches the backend: empty or
unexpected values should return a normal 404 or a "show not found" page
rather than propagating to an unhandled backend error.
