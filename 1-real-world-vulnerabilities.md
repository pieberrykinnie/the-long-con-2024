# Real-world Vulnerabilities (and how to demonstrate impact while exploiting them)

Presented by Jade Null - Founder/Hacker of GlitchSecure

Something they've learned - Developers and PMs don't always understand impact, causing findings to remain unfixed for extend periods of time.

## Examples Of Real-World Vulnerabilities

- Cross-site Scripting (XSS)
    - `alert(1)`: boring - don't demonstrate (much) impact and don't account for protections
    - Slightly better XSS: steal cookies by sending a `fetch()` request - cool but not too exciting
    - Tool: [ezXSS](https://github.com/ssl/ezXSS) much more exciting, can take much more data
- Chaining low Severity Vulns: some issues aren't that serious, find ways to chain findings to increase severity and show further impact
    1. Insecure Pre-signed URL Gen
    2. Information Disclosure
    3. Combining #1 and #2: allowed getting their driver license
- Lack of Rate-limiting on Password Reset => Lack of Rate-limiting on Email Triggering Forms
- Open Redirect => Email Parameter Injection => Phishing

## Exploitation paths that show impact

- Demonstrate XSS Impact: show real impact (steal information? perform actions?), use tooling to help (ezXSS)
- Don't be afraid to be a lil scary: Show real impact (if info can be stolen, show it), review past findings (often more impact to be shown)
- Think Like a Spammer: Spammers abuse Rate-Limits and Create Phishing Pages, you should too!
    - Don't be afraid to send yourself a few hundred emails (with permission/scope)
    - Create quick-and-dirty non-functional phishing pages when showing off open redirect

## Q&A

- Are there any tools for developers to train themselves?
    - Deal with error reports
- Most commonly misunderstood vulnerability?
    - CSRF, basically try to demonstrate impact for any of them
