# Rate Limiting

There is a rate limit of 100 API calls every 30 seconds.

If the rate limit is exceeded you will receive a response `HTTP 429 (Too Many Requests)`, with the following headers:

Header | Description
---------- | -------
X-RateLimit-Limit | The amount of API calls you can make every 30 seconds (always 100)
X-RateLimit-Remaining | The amount of API calls that are still remaining (`0` on a 429 response)
Retry-After | The amount of seconds until it is allowed again to make API calls
X-RateLimit-Reset | The time when it is allowed again to make API calls.