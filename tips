A) Hosting environment/ General tips

* Get a dedicated server or a VPS from a poster specialised in Magento.
* Host your site in the country (or at least on the continent) where your customers are. If you have customers worldwide, use a CDN (see tips below on CDN).
* Don't host files on your web server that you do not use, large or small.
* Goto MySQL Admin and select all the tables and repair and then optimize them. Small effect but good to check. Do things in MySQL break often? Get a new hoster.
* IF you have PHP6 or lower: Use a PHP accelerator like APC, ZendOptimizer+ or Xcache. No longer needed with PHP7.    
* APC – http://pecl.php.net/package/APC. Increased the APC.shm.size to something like 128 to allow more data to be cached by apc.
*    Xcache – http://xcache.lighttpd.net/
*    Only install necessary database modules.
*    Swap Apache for NginX or Litespeed.
*    [REPLACED by nginx_pagespeed] Use Apache mod_expires and be sure to set how long files should be cached. You could use the example below for your Apache virtualhost config: # Turn on Expires and set default to 0                ExpiresActive On                ExpiresDefault A0                # Set up caching on media files for 1 year (forever?)                        ExpiresDefault A29030400                        Header append Cache-Control "public"                # Set up caching on media files for 2 weeks                        ExpiresDefault A1209600                        Header append Cache-Control "public"                # Set up 1 week caching on commonly updated files                        ExpiresDefault A604800                        Header append Cache-Control "proxy-revalidate"                # Force no caching for dynamic files                        ExpiresActive Off                        Header set Cache-Control "private, no-cache, no-store, proxy-revalidate, no-transform"                        Header set Pragma "no-cache"
*    [REPLACED by nginx_pagespeed] Enable Gzip Compression in htaccess. > REPLACED by nginx_pagespeed
*    Compress output, use zlib.output_compression or mod_deflate.
*    Use a Content Delivery Network (CDN) for parallel transfer of static content. There is a Magento extension that can help you do this with category and product images: the One Pica Image CDN. But... (see next tip).
*    Don't use too many different external sources (for images, iframes, (twitter/facebook)feeds etc.) because every DNS lookup takes extra time and you create an extra dependancy (on some 3rd party server) for your site to load properly.
*    (If you still use Apache) Enable Apache KeepAlives: Make sure your Apache configuration has KeepAlives enabled. KeepAlives are a trick where multiple HTTP requests can be funneled through a single TCP connection. The setup of each TCP connection incurs additional time, this can significantly reduce the time it takes to download all the files (HTML, JavaScript, images) for a website. More info  at Apache.org. Be carefull though, I've heard from some that this create (a lot of) extra load on the server and might crash the server on high traffic moments!
*    Minimize redirects.
*    Make your output W3C compliant at least do cross-browser testing. Errors slow down the browser.
*    Turn off or at least reduce web server logging (reduces disk writes).    
*    Disable Access Time Logging. For Linux servers, if you have access-time logging enabled on any of your mysql, web server or cache partitions, try turning it off for a performance boost. If you’re using ext3 or reiserfs there may be faster journal write methods you can use. For more info see Linux.com.
*    Compile MySQL from source instead of your OS’s package manager. You can also use Percona or MariaDB.
*    Always upgrade to the latest Magento version. Not only will you get more features and bug- and security fixes, but with every update Magento performs better.
*    Query Cach size: Magento Blog: Modify the configuration for your MySQL server to take better advantage of your server’s RAM. Most Linux distributions provide a conservative MySQL package out of the box to ensure it will run on a wide array of hardware configurations. If you have ample RAM (eg, 1gb or more), then you may want to try tweaking the configuration. An example my.cnf is below, though you will want to consult the MySQL documentation for a complete list of configuration directives and recommended settings. A proper MySQL setup is very important with Magento.
*    set 'php_value memory_limit 512M' in your php configuration or add it to your .htaccess file to ensure you don't run out of memory.
*    Use a memory-based filesystem for dynamic data. If you store dynamic data (var/cache, var/session) on RAMdisk or tmpfs, the disk I/O is decreased. Use Redis / RedisSession
*    Change realpath_cache_size in php.ini. realpath_cache_size=1M (careful, this is per apache process) realpath_cache_ttl=86400 (ok for production site)
*    Memcache (for the hardcore) is documented in http://www.magentocommerce.com/boards/viewthread/9037/ and more tips from http://alexle.net/archives/275 to get you up and running. Or use Redis.
*    Disable the PHP open_basedir directive. Read this.
*    Eliminate directory structure scans for .htaccess files. Or use nginx.
*    Recommended innodb_buffer_pool_size.    
*    Combined web and db server, 6 GB RAM:  2-3 GB
*    Dedicated database server, 6GB RAM: 5 GB
*    Dedicated database server, 12 GB RAM: 10 GB
*    innodb_thread_concurrency.    
*    2 * [numberofCPUs] + 2
*    Query Cach: query_cache_size: 64MB, query_cache_limit: 2MB. Depends on the server though.
*    Usually 1 (fat) server should be able to handle everything. If you do a lot of backend work during peak hours however you could consider using a seperate backend server to handle admin users, process backend activity (cron), pre generate full page caching and to handle media queries.
*    If 1 fat server isn't enough: use multiple web nodes (frontend servers) to handle browsing and checkout.
*    Use Varnish reverse proxy caching. If you use EE, just use FPC since it's easier to tweak compared to Varnish.
*    If you have a popular site that is heavily crawled by searchengines, you can save some resources by tweaking your robots.txt.
*    Try some of these cache extensions:    
 *    https://github.com/GordonLesti/Lesti_Fpc
 *    http://www.artio.net/magento-extensions/m-turbo-accelerator
 *    http://www.aitoc.com/en/magento_booster.html
 *    http://www.tinybrick.com/magento-modules/performance.html/
*    Install the Yireo DisableLog addon. It prevents Magento writing tons of stuff to your database which is useless when you're already using something like Google Analytics.
    Use Magento with HHVM (HipHop Virtual Machine). Facebook uses this too and they reported 6x to 9x server performance improvement. See http://www.slideshare.net/MeetMagentoNY2014/jenna-warren-14pm-23-sept.

B) Template

*    Optimize all your (template) images- Most if not all should be at least below 10kb. Use nginx_pagespeed.    
*    Crop the white space using your image editor.
*    Use PNG8 Files or GIF files rather than Jpegs and don't use transparency (depending on how many colors you use and how large the image is, but try for yourself).
*    Scale images: make images in the dimensions you need and not resizing them in the editor.
*    Use image compression (you can use smush.it to do it for you).
*    Use CSS Sprites, there even are CSS Sprite Generators.
*    Minify your Css, remove unused code. Use nginx_pagespeed.
*    Minimize Javascript use. Use nginx_pagespeed.
*    Use a lightweight template as a basis for your template.
*    Specify Image dimensions.
*    Use Block cache and HTML output in your extensions.
*    Apply Javascript Lazy Loader for prototype.
*    Move all JavaScript to the end of the page https://github.com/bobbyshaw/magento-footer-js.

C) Magento configuration

*    Uninstall any extensions that you don't actually use.
*    Disable modules that you don't use: System -> Configuration -> Advanced -> Advanced.
*    This is an example setting[/caption]
*    Enable all Magento Caches: System -> Cache Management.
*    Use an offsite Stats Tracker like Google Analytics and not an onsite one. Most of this will use Javascript, host the Javascript yourself.
*    Combine Javascript and Combine CSS files: System ->Configuration ->Advanced ->Developer -> 'Javascript settings' and 'CSS Settings'. You can also consider using an extensions to do this like the Fooman Speedster extension, whichever works best for you.
*    Try some of the Magento performance extensions. Research the extensions, ask around fir experiences.
*    Enable the Magento Flat Catalog.
*    Don't use layered navigation if you don't really need it, it's resource intensive.
*    Don't use Magento's Compilation feature. Use Aoe_ClassPathCache instead.
*    Use the correct session storage, choose file system or database (during setup). Most installations should use "file system" because it's faster and doesn't cause the database to grow. If you're on a cluster, use RedisSession.
*    If it's good for your conversion, show more products. But be aware that showing more product on a category page will increase page load. But conversion trumps page load so test it.
*    Set only those attribute frontend properties to 'Yes' that you're actually going to use. Set all other to 'No'. Don't use in quick search, advanced search compare, etc etc.: Catalog -> Attributes -> Manage Atributes -> Frontend Properties. 

Enterprise only tip:

*    Disable Enterprise_CatalogEvent. Go to Admin -> System -> Configuration -> Catalog -> Catalog Events. Then you want to turn off the settings for "Enable Catalog Events Functionality" and "Enable Catalog Event Widget".
*    Enable Solr search, it's quicker compared to the default setup, especially when you have lots of products (>10k).
*    Enable Full Page Caching.

D) Speed testing, analysing, monitoring

*    Test your Magento site with Magento Speed Test (by Ashley Schroder) or look for the TTFB in your inspector.
*    Run your site through websiteoptimization.com.
*    Use Google Page Speed Firefox extension or Yahoo Yslow for some tips from Google and Yahoo.
*    Implement Google Speed measurements in Analytics: Measure Page Load Time with Site Speed Analytics Report
*    Speed monitoring and downtime alerts.    
*    Mon.itor.us
*    Pingdom
*    Send logs to a logging service like laggy for useful alerts. See https://github.com/firegento/firegento-logger

Bonus Tips
(because these doesn't actually speed up the frontend but only the backend):

*    Use [K-Meleon](http://kmeleonbrowser.org/) if you are on Windows for your general Admin work. It renders Magento’s heavy JS back-end significantly faster than any other browser.
*    Use the GoogleGears extension from Yireo.com to cache static files locally.
*    Use a local pc/mac application to manage Magento (like mag-manager.com).

So to summarize:

*    Use a big fat server configured by a Magento specialist. Hardware helps, but configuration is key.
*    Use nginx + nginx_pagespeed and use mod_pagespeed to tweak (see https://www.h-o.nl/blog/best-magento-mod_pagespeed-configuration).
*    Use the latest PHP version (currently 7) or HHVM
*    Use a CDN like Cloudflare.
