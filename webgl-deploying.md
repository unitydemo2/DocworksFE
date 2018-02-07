# WebGL: Deploying compressed builds

When you build a WebGL project in release mode (see [Publishing builds](PublishingBuilds)), Unity compresses your build output files to reduce the download size of your build. You can choose the type of compression it uses from the Compression Format options in Publishing Settings (menu: __Edit__ > __Project Settings__ > __Player__ > __Publishing Settings__):

* __gzip__: This is the default option. gzip files are bigger than Brotli files, but faster to build, and natively supported by all browsers over both http and https.

* __Brotli__: Brotli compression offers the best compression ratios. Brotli compressed files are significantly smaller than gzip, but take a long time to compress, increasing your iteration times on release builds. Brotli compression is natively supported by Chrome and Firefox over https (see [WebGL browser compatibility](webgl-browsercompatibility) for more information).

* __Disabled__: This disables compression. Use this if you want to implement your own compression in post-processing scripts.

Compression-built Unity builds work on any browser. Unity contains a software decompressor written in JavaScript, which it falls back to when compression on the http transfer level is not enabled by the server.

## Advanced: Native browser decompression

The browser can handle decompression of Unity builds natively while it downloads the build data. This has the advantage of avoiding the additional delay caused by decompressing your files in JavaScript, therefore reducing your startup time. To let the browser handle decompression natively, you need to configure your web server to serve the compressed files with the appropriate http headers: These tell the browser that the data is compressed with gzip or Brotli so it decompresses the data while it is being transferred. Brotli compression is supported by Firefox and Chrome on https only, while gzip compression is supported by all browsers. See [WebGL browser compatibility](webgl-browsercompatibility) for more information.

## Setting up web servers

The setup process for native browser decompression depends on your web server. The instructions on this page apply to the two most common web servers, __Apache__ and __IIS__. Note that these are designed to work on a default setup, but may need adjustments to match your specific configuration. In particular, there may be issues if you already have other server-side configuration to compress hosted files, which may interfere with this setup. The basic idea is to append a *Content-Encoding* header to the server response, corresponding to the type of compression used at build time. This will allow the browser to perform decompression natively and asynchronously during download.

### Apache

Apache server uses invisible *.htaccess* files for server configuration. The code below shows examples of *.htaccess* files which can be used to enforce native browser decompression. Note that Apache server configuration setup is optional.

For gzip-compressed builds put the following *.htaccess* file into your *Build* subfolder:

```
<IfModule mod_mime.c>

  AddEncoding gzip .unityweb

</IfModule>
```


For brotli-compressed builds put the following *.htaccess* file into your *Build* subfolder:

```
<IfModule mod_mime.c>
  AddEncoding br .unityweb
</IfModule>
```

## IIS

__Necessary IIS server configuration steps:__

By default IIS server does not serve static content of unknown MIME type. In order to make Unity build work on IIS, you first need to associate the *.unityweb* extension with the *application/octet-stream* content typ. There are two ways to achieve that:

*Using IIS Manager interface:*
Select your website in the IIS Manager panel, open the *MIME Types* feature and select *Add…* action. Set *.unityweb* as file name extension and *application/octet-stream* as MIME type, click *OK*.

*Using server configuration file:*
IIS uses *web.config* files for server configuration. Those configuration files reflect all the changes made in IIS Manager for a specific folder. In order to associate *application/octet-stream* MIME type with *.unityweb* extension, you can use the following *web.config* file:

```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
	<system.webServer>
    		<staticContent>
        	<remove fileExtension=".unityweb" />
<mimeMap fileExtension=".unityweb" mimeType="application/octet-stream" />
    		</staticContent>
	</system.webServer>
</configuration>
```

Note that configuration file affects all the server subfolders, therefore it is sufficient to set the MIME type for the *.unityweb* extension just once in the server root folder.

Optional IIS server configuration steps:


In order to speed up the build startup times, you may optionally use the following configuration files. Note that in order to use this setup, you need to have Microsoft’s [IIS URL Rewrite IIS module](http://www.iis.net/downloads/microsoft/url-rewrite) installed; otherwise, the browser will throw a 500 Internal Server Error.

For gzip-compressed builds put the following *web.config* file into the *Build* subfolder:

```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
	<system.webServer>
    		<staticContent>
        			<remove fileExtension=".unityweb" />
        			<mimeMap fileExtension=".unityweb" mimeType="application/octet-stream" />
    		</staticContent>
    		<rewrite>
        			<outboundRules>
            			<rule name="Append gzip Content-Encoding header">
                			<match serverVariable="RESPONSE_Content-Encoding" pattern=".*" />
                			<conditions>
                    				<add input="{REQUEST_FILENAME}" pattern="\.unityweb$" />
                			</conditions>
                			<action type="Rewrite" value="gzip" />
            			</rule>
        			</outboundRules>
    		</rewrite>
	</system.webServer>
</configuration>
```

For brotli-compressed builds put the following *web.config* file into the *Build* subfolder:

```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
	<system.webServer>
    		<staticContent>
        			<remove fileExtension=".unityweb" />
        			<mimeMap fileExtension=".unityweb" mimeType="application/octet-stream" />
    		</staticContent>
    		<rewrite>
        			<outboundRules>
            			<rule name="Append br Content-Encoding header">
                			<match serverVariable="RESPONSE_Content-Encoding" pattern=".*" />
                			<conditions>
                    				<add input="{REQUEST_FILENAME}" pattern="\.unityweb$" />
                			</conditions>
                			<action type="Rewrite" value="br" />
            			</rule>
        			</outboundRules>
    		</rewrite>
	</system.webServer>
</configuration>

```

Note that the `<remove fileExtension=".unityweb" />` lines are required to handle a situation when content type is already overridden at a higher level in the server directory’s hierarchy, which could otherwise cause a server exception.

----
*  <span class="page-edit">2017-05-24  <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-history">Updated in 5.6</span>


