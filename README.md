
# redis-cache_example
An Example showing redis cache and its response time.
This project will allow us to query the Wikipedia API from our endpoint by specifying the keyword we want to query.


**We will use the following npm packages in this project** :

- **Axios** to make HTTP requests.
- **Express** for routing.
- **Redis** as Node.js redis client.
- **Response-time** Nodejs package to record response time in the response header.

**Installing the Node's dependencies**

    npm install
 

**How to test**
1. On your Google Chrome browser, enable Developer Tools
2. Go to  `localhost:3000/api/search?query=Malaysia`.  
You can replace the  `Malaysia`  with any word of your choice.
3. Load the site/URL above.

**To verify Performance/Speed**  
On Chrome's Developer Tools >  Network > /api/search?query=Malaysia
Take note of the **X-Response-Time** fields in the first request.
then refresh/run the request again, and take note of the improved response time of the second request.

**What actually happen - The Workflow**
So, what goes into the  `/api/search`  route hander:

1. Sent a requests for article
2. Our code look inside the Redis store to see if the articles that have been cached previously
    -   If true, the cached version will be served to the client.
    -   Otherwise, we will get/fetch the article from the Wikipedia API
        -   We cache the response from the API in Redis for a specific duration (5 minutes).
        -   We send a response to the user.
3. With the lifespan of 5 minutes (or what we have defined), the cache will expires after. A request made after the cache expired will render the request to make a get/fetch again to the actual API to retrieve the current/new data to be put into the cache.
