# Local Storage

## Configuring Local Machine for Data Storage

{% hint style="warning" %}
**Local Storage Drawbacks**  
  
If you store the data on your local machine, you will not be able leverage any of the collaboration features of the RedBrick AI platform. Configuring local storage is recommended for small single person projects or individual experimentation.
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

