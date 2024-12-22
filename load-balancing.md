# Load Balancing

Load balancing is all about divide work among multiple processes so as to not overwork a process and get fast results

> I'm not sure when I'll need this but if there is ever a situation where I want requests to be load balanced across multiple servers but I want all requests from the same user to be handled by the same server because of some data being stored Nginx can handle this.

> In a previous part I wondered what the difference between Nginx Open Source and Nginx Plus is. For one Nginx Open Source supports passive health checking of the servers being proxied while Nginx Plus also supports active health checks.

To set up load balancing you first need to define the servers that you want to be receiving requests. This is done in the **upstream** block. The upstream block takes server declarations that define where the server is (IP, hostname, socket or a mix) and can contain additional parameters such as if it's a backup server that should only be used when the active servers are down and the weight a server should be given when deciding what server to route a request to. The upstream block looks like this:

```conf
upstream <name> {
    server location [parameter];
}
```

An example is:

```conf
upstream api {
    server algorand.com:3000 weight=1;
    server vank.com:443 weight=2;
    server localhost:3000 backup;
}
```

To then define what requests will be balanced use the proxy_pass directive in the location block e.g

```conf
location / {
    proxy_pass http://api
}
```

## TCP Load Balancing
