# Additional servicces

## IPStack.com

!!! note
    Experimental, since v1.9.

https://ipstack.com/

Service is used for country/city detection by IP address (landing page -> sign-up form). 
Free 10,000 queries per month. 
YouDate uses caching to minimize queries count.
To enable this service:

1. Get free API key: https://ipstack.com/product 
2. Add API key to your `.env` config:

```
IPSTACK_API_KEY = yourKeyHere
```
