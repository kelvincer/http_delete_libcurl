# Code
```c
#include "curl/curl.h"

int main(void)
{
    int movieId = 142064;
    char *fullURL;
    char *URL = "https://api.themoviedb.org/3/movie/%d/rating";
    sprintf(fullURL, URL, movieId);

    curl_global_init(CURL_GLOBAL_ALL);
    CURL *curl = curl_easy_init();

    if (curl)
    {
        curl_easy_setopt(curl, CURLOPT_CUSTOMREQUEST, "DELETE");
        curl_easy_setopt(curl, CURLOPT_WRITEDATA, stdout);
        curl_easy_setopt(curl, CURLOPT_URL, fullURL);

        struct curl_slist *headers = NULL;
        headers = curl_slist_append(headers, "accept: application/json");
        headers = curl_slist_append(headers, "Content-Type: application/json;charset=utf-8");
        headers = curl_slist_append(headers, "Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI2NDM1MTgzZmM4ZTgyOTQ3OGNiNWY4NTM5ZWZkMWU3MSIsIm5iZiI6MTcyNzAyODk1My45NTM4NzUsInN1YiI6IjVjNjA0NjE1OTI1MTQxMzM3NmMwMWQ3OCIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.ojN56CsCIKIhTfNlXob_o48Npl3xBiznLJls-jrNMRY");
        curl_easy_setopt(curl, CURLOPT_HTTPHEADER, headers);

        CURLcode ret = curl_easy_perform(curl);

        curl_slist_free_all(headers);
        curl_easy_cleanup(curl);
    }

    curl_global_cleanup();

    return 0;
}
```
