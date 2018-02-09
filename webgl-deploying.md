#Deploying compressed builds

When you build a WebGL project in release mode (see [Publishing builds](PublishingBuilds)), Unity compresses your build output files to reduce the download size of your build. You can choose the type of compression it uses from the Compression Format options in Publishing Settings (menu: __Edit__ > __Project Settings__ > __Player__ > __Publishing Settings__):

* **gzip**: This is the default option. gzip files are bigger than Brotli files, but faster to build, and natively supported by all browsers over both http and https. File names get an additional .gzip suffix appended.

* **Brotli**: Brotli compression offers the best compression ratios. Brotli compressed files are significantly smaller than gzip, but take a long time to compress, increasing your iteration times on release builds. Brotli compression is natively supported by Chrome and Firefox over https (see [WebGL browser compatibility](webgl-browsercompatibility) for more information). Brotli-compressed file names get an additional .br suffix appended.

* **Disabled**: This disables compression. Use this if you want to implement your own compression in post-processing scripts.

Compression-built Unity builds work on any browser. Unity contains a software decompressor written in JavaScript, which it falls back to when compression on the http transfer level is not enabled by the server. The data is downloaded from the server by the browser, and then decompressed by Unity’s loader code. When this is done, this message appears in your browser’s JavaScript console (containing your file name instead of our example):

`Decompressed <Example/MyProject.jsgz> in 82ms. You can remove this delay if you configure your web server to host files using compression.`

Here, `82ms` is just an example; the number of milliseconds depends on the size of the content and on the speed of the computer. Bigger builds take longer to decompress, and faster computers take less time. The decompression time is printed to give you an idea of how much start up time you could potentially save by having the browser handle the decompression instead.

##Advanced: Native browser decompression

The browser can handle decompression of Unity builds natively while it downloads the build data. This has the advantage of avoiding the additional delay caused by decompressing your files in JavaScript, therefore reducing your startup time. To let the browser handle decompression natively, you need to configure your web server to serve the compressed files with the appropriate http headers: These tell the browser that the data is compressed with gzip or Brotli so it decompresses the data while it is being transferred. Brotli compression is supported by Firefox and Chrome on https only, while gzip compression is supported by all browsers. See [WebGL browser compatibility](webgl-browsercompatibility) for more information.

##Setting up web servers

The setup process for native browser decompression depends on your web server. The instructions on this page apply to the two most common web servers, **Apache** and **IIS**. Note that these are designed to work on a default setup, but may need adjustments to match your specific configuration. In particular, there may be issues if you already have other server-side configuration to compress hosted files, which may interfere with this setup.

###Apache

Apache uses invisible .htaccess files for server configuration. This example code below shows an example of a .htaccess file you can put into your _Release_ folder to configure Apache for hosting your compressed files.

````
<IfModule mod_rewrite.c>

  <IfModule mod_mime.c>

    Options +SymLinksIfOwnerMatch

    RewriteEngine on

    RewriteCond %{HTTP:Accept-encoding} br

    RewriteCond %{REQUEST_FILENAME}br -f

    RewriteRule ^(.*)\.(js|data|mem|unity3d)$ $1.$2br [L]

    AddEncoding br .jsbr

    AddEncoding br .databr

    AddEncoding br .membr

    AddEncoding br .unity3dbr

    

    RewriteCond %{HTTP:Accept-encoding} gzip

    RewriteCond %{REQUEST_FILENAME}gz -f

    RewriteRule ^(.*)\.(js|data|mem|unity3d)$ $1.$2gz [L]

    AddEncoding gzip .jsgz

    AddEncoding gzip .datagz

    AddEncoding gzip .memgz

    AddEncoding gzip .unity3dgz

    

  </IfModule>

</IfModule>
````

When Apache receives a request for a file (such as _Release/mygame.js_), this configuration checks to see if the client accepts Brotli-encoded data (`RewriteCond %{HTTP:Accept-encoding} br`), then checks to see if there is a file at _Release/mygame.jsb**r_ (`RewriteCond %{REQUEST_FILENAME}br -f`). If both conditions are met, it rewrites the request to the .jsbr file, and serves it. `AddEncoding br .jsbr` tells Apache to add the headers to tell the client that the file uses Brotli encoding.

The following block of code example does the same setup for gzip, so if a _Release/mygame.jsgz_ file exists but the conditions for Brotli compression are not met, then it will host the file in the .gzip format.

##IIS

IIS uses _web.config_ files for server configuration. This sample code shows an example of a _web.config_ file you can put into your _Release_ folder to configure IIS for hosting your compressed files. 

To use this, you need to have Microsoft’s [IIS URL Rewrite IIS module](http://www.iis.net/downloads/microsoft/url-rewrite) installed; otherwise, the browser throws a 500 Internal Server Error. If you don’t have the module installed, you can still use this file, but without the section of code starting `<rewrite>` and ending `</rewrite>`. This does not enable compressed transfers, but does enable IIS to host the file extensions.

````
<?xml version="1.0" encoding="UTF-8"?>

<configuration>

    <system.webServer>

        <staticContent>

            <remove fileExtension=".mem" />

            <remove fileExtension=".data" />

            <remove fileExtension=".unity3d" />

            <remove fileExtension=".jsbr" />

            <remove fileExtension=".membr" />

            <remove fileExtension=".databr" />

            <remove fileExtension=".unity3dbr" />

            <remove fileExtension=".jsgz" />

            <remove fileExtension=".memgz" />

            <remove fileExtension=".datagz" />

            <remove fileExtension=".unity3dgz" />

            <mimeMap fileExtension=".mem" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".data" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".unity3d" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".jsbr" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".membr" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".databr" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".unity3dbr" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".jsgz" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".memgz" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".datagz" mimeType="application/octet-stream" />

            <mimeMap fileExtension=".unity3dgz" mimeType="application/octet-stream" />

        </staticContent>

        <rewrite>

            <rules>

                <rule name="Append br suffix to WebGL content requests">

                    <match url="(.*)\.(js|data|mem|unity3d)$" />

                    <conditions>

                        <add input="{HTTP_ACCEPT_ENCODING}" pattern="br" />

                        <add input="{REQUEST_FILENAME}br" matchType="IsFile" />

                    </conditions>

                    <action type="Rewrite" url="{R:1}.{R:2}br" />

                </rule>

                <rule name="Append gz suffix to WebGL content requests">

                    <match url="(.*)\.(js|data|mem|unity3d)$" />

                    <conditions>

                        <add input="{HTTP_ACCEPT_ENCODING}" pattern="gzip" />

                        <add input="{REQUEST_FILENAME}gz" matchType="IsFile" />

                    </conditions>

                    <action type="Rewrite" url="{R:1}.{R:2}gz" />

                </rule>

            </rules>

            <outboundRules>

                <rule name="Append br Content-Encoding header to the rewritten responses">

                    <match serverVariable="RESPONSE_Content-Encoding" pattern=".*" />

                    <conditions>

                        <add input="{REQUEST_FILENAME}" pattern="\.(js|data|mem|unity3d)br$" />

                    </conditions>

                    <action type="Rewrite" value="br" />

                </rule>

                <rule name="Append gzip Content-Encoding header to the rewritten responses">

                    <match serverVariable="RESPONSE_Content-Encoding" pattern=".*" />

                    <conditions>

                        <add input="{REQUEST_FILENAME}" pattern="\.(js|data|mem|unity3d)gz$" />

                    </conditions>

                    <action type="Rewrite" value="gzip" />

                </rule>

            </outboundRules>

        </rewrite>

    </system.webServer>

</configuration>
````

You only need the `<remove fileExtension=".*”>` lines if these extensions can be overridden at a higher level in the directory’s hierarchy.

