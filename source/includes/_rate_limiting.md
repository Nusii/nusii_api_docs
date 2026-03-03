# Rate Limiting

There is a rate limit of 100 API calls every 30 seconds.

With every request to the API we add a couple of headers to the request. 

If the rate limit is exceeded you will receive a response `HTTP 429 (Too Many Requests)`. 

Header | Description
---------- | -------
X-Ratelimit-Limit | The amount of API calls you can make every 30 seconds (always 100)
X-Ratelimit-Remaining | The amount of API calls that are still remaining.
Retry-After | The amount of seconds untill it is allowed again to make API calls
X-RateLimit-Reset | The timestamp when it is allowed again to make API calls.