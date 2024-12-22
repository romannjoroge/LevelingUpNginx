# Basics of Nginx

Obviously to use Nginx you need to have installed it on your system. It isn't just magic that works on servers ;)

There is Nginx Open Source and Nginx Plus. I guess the Plus has some more features, I'm not sure if those extra features can be implelmented using Open Source

To check if you've installed Nginx and the version of Nginx installed run the command below:

```bash
nginx -v
```

(IDK what I did but I seem to have an older version of Nginx than the book :( )

To check if nginx is running run the command:

```bash
ps -ef | grep nginx
```

To check if Nginx is returning requests you can curl localhost

```bash
curl localhost
```

## Important files and directories

*/etc/nginx/* - where you can configure Nginx server
*/etc/nginx/nginx.conf* - entrypoint for the configurations. It has global configurations for things like worker processes and references the other configurations
*/etc/nginx/conf.d/* - Contains the default server configuration file. Files ending in .conf are included in the nginx.conf file. That's why I found configurations in this folder. In other configurations this would be sites-enabled which contains links from sites-available (this sites-available, sites-enabled framework is deprecated)
*/var/log/nginx/* - contains an access.log where each request made is logged and errors.log where error events and debug information if the debug module is enabled.

> You can change where the logs go in the default configuration file.

## Some useful commands

This commands need to be run as sudo:

*nginx -s signal* - can send signals such as stop, quit, reload, open to the master process. Stop discontinues Nginx immediately while quit lets Nginx finish the requests its processing before stopping. reload reloads the configuration
*nginx -t* - tests the Nginx configurations

> May never use Nginx enough to need this but assuming I had a configuration that's shared by multiple configurations I could split it to else where then include it (doesn't seem like the included files need to be ending in .conf

If you want Nginx to listen to something define a server block.
The listen directive can specify that it should be default for a certain port
I think every request comes with a header for server name, then when nginx receives a request on a port it looks for what server context has that server_name. This is avoided if a context defines itself as default for a port.
When a request is made it has a URI e.g www.example.com/api/test the /api/test is the URI. When Nginx gets a request it matches the **request to the matching location block context for the URI**. That's why the location block is there.
The root tells Nginx where to look for files when serving **static content**.
Index defines what to get if no path is provided in URI
