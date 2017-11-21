#include <curl/curl.h>
#include <iostream>
#include <fstream>

int main()
{
	ofstream outputFile;
	outputFile.open("data.txt");

	CURL *hnd = curl_easy_init();

	curl_easy_setopt(hnd, CURLOPT_CUSTOMREQUEST, "GET");
	curl_easy_setopt(hnd, CURLOPT_URL, "http://192.168.0.10/get_imglist.cgi?DIR=%2FDCIM%2F100OLYMP");

	struct curl_slist *headers = NULL;
	headers = curl_slist_append(headers, "postman-token: 3f2ae586-3eec-1a12-a065-e1f00626c9ee");
	headers = curl_slist_append(headers, "cache-control: no-cache");
	headers = curl_slist_append(headers, "content-length: 4096");
	headers = curl_slist_append(headers, "user-agent: OlympusCameraKit");
	curl_easy_setopt(hnd, CURLOPT_HTTPHEADER, headers);

	CURLcode ret = curl_easy_perform(hnd);
	outputFile << ret;
    return 0;
}