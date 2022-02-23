# Public Storage

Public storage method allows you to upload URLs that are accessible by your/your teams browsers. The data doesn't actually have to be **publicly accessible on the internet,** it just has to be accessible to your browser.&#x20;

There are two main use-cases of Public Storage methods:&#x20;

1. Data that is publicly available on the internet.&#x20;
2. Data that is stored on an on-premise server that is accessible in a private network.

## Items Path

For public storage data, you have to upload an [items list](./#items-list) to your projects to import specific datapoints. Please have a look at the [items list](./#items-list) documentation for a overview of the format for the JSON file.&#x20;

The `items` path needs to be formatted as follows:&#x20;

```json
"https://path-to-your-data.png"
```

A good test to see if this will work with Public Storage method, is to paste the link in your browser and see if your browser is able to load the data. If it is, then this URL will work.&#x20;

## Configuring Local Server for Data Storage

{% hint style="warning" %}
**Local Storage Drawbacks**\
****\
****If you store the data on your local machine, you will not be able leverage any of the collaboration features of the RedBrick AI platform. Configuring local storage is recommended for small single person projects or individual experimentation.
{% endhint %}

This section will cover how to configure your local machine to store data for use with the RedBrick AI platform. To allow the RedBrick AI platform to access data from your local machine, you will have to start an http server through which your data will be hosted. There are several packages that enable this:

{% tabs %}
{% tab title="http-server" %}
```bash
$ npm install --global http-server # Mac users can do brew install http-server
$ http-server path/to/data
```
{% endtab %}

{% tab title="SimpleHTTPServer" %}
```bash
$ python -m http.server --directory path/to/data
```
{% endtab %}
{% endtabs %}

Once you start your http server, you will be able to see your data in the browser by using the a path like `http://127.0.0.1:8000/path/to/data/img.png`.
