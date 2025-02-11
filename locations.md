# Locations

Locations are used to tell Nginx what to do when a rotue is hit e.g when we go to <your-domain>/<route> what should Nginx serve?

We can tell Nginx to serve the contents that are in a directory named <route> from a certain root that we specify. For example if you want Nginx to serve content in your-site/about when the about route is reached you can add this configuration:

```conf
html {
    server {
        listens 8080;

        location /about {
            root your-site
        }
    }
}
```

You can also tell Nginx to serve content from a folder that has a different name from the <route> using an alias. The alias points at the directory that Nginx should get what to serve from. For example:

```conf
html {
    server {
        listens 8080;
        
        location /careers {
            alias your-site/about
        }
    }
}
```

You can pass a regex express to location using ~*. For example if we want to define the location of /count/number we can do **location ~* /count/[0-9]**
