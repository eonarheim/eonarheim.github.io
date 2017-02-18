Title: Migrating to Wyam in GH Pages from WordPress
Published: 2/17/2017
Tags: 
 - Static Site
 - Wyam
 - Markdown
 - Razor
 - WordPress
 - GitHub Pages
disqus_identifier: https://erikonarheim.com/posts/using-wyam-blog/
---
Recently I needed to update my WordPress version (yet again), along with patch my server, update my HTTPS certificate, and pay my hosting bill. The amount of admin-istrivia around maintaining your own server and application platform is more than I want to do for a blog. This got me thinking there must be a better way to do this, my friends [@kamranayub](https://twitter.com/kamranayub) in particular have been pushing me to move to static site generation.

## Intro Wyam

This leads me to the Wyam static site generator. It is a great little static site generator built in C#/.NET. If you come from a Markdown/Razor background you'll really find this stuff really familiar and easy to use. Wyam is super configurable, fully customizable, and compatible with GitHub pages. Let's dig into it.

I've had some experience with Jekyll..


## Installing Wyam

Installing Wyam is pretty easy, navigate [here](https://wyam.io/docs/usage/obtaining) and follow one of the many ways to install. I used the Windows installer, unfortunately it does not automatically add itself to the path. Fortunately, it is easy to do with the following command once installed:

```powershell
%LocalAppData%\Wyam\Wyam.Windows add-path
```

In a new command window you can confirm 

```powershell
wyam --help
```


## Building your first blog (post)

[Blog Recipe](https://wyam.io/recipes/blog/overview)


## Testing Wyam locally with IIS (or just use the easy way)

When I started working on this I tried a number of different of local servers to test this, TLDR: just use `wyam preview` in the root directory of our block (above the input folder). 

![preview](images\wyam-preview2.png)

If you want to know the hard way and see how to use IIS in a non-standard directory to run Wyam read on, otherwise skip to the next section :)

I keep a projects directory on my machine where I do most of my development on various projects. Unfortunately IIS does not have the permission to read into directories outside of `C:\inetpub\wwwroot` by default which is a good default for servers. But if you want to test outside of your web root in your development space it is a problem. To fix this you'll need to set some file ACLs so that IIS can read your files. Give `IIS_IUSRS` and `Users` on the local machine Execute, List, and Read.

![Folder ACLs](images\iis-perms.PNG)

Next you'll need to solve the problem of the extension-less `/posts/name-of-my-post` file names that need to be served as if they contained an `index.html` when they don't.

![extensionless](images\url-non-rewrite.PNG)

Versus

![extension](images\url-non-rewrite-html.PNG)

In order to fix this Wyam has some [azure documentation]() referencing the rewrite module in azure. IIS does not come with this pre-installed so you'll need to [install the module](https://www.iis.net/downloads/microsoft/url-rewrite) located at the bottom of the page.

![rewrite-module](images\download-rewrite.PNG)

Once that is complete you can drop in a `web.config` in your `input` directory with the rewrite rule referenced in the Wyam docs and voila! 

```xml
<?xml version="1.0"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="html">
          <match url="(.*)" />
          <conditions>
            <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
            <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
          </conditions>
          <action type="Rewrite" url="{R:1}.html" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
![rewrite](images\url-rewrite.PNG)

## Preserve you old links

If your blog has some good SEO juice, or maybe you just don't want to break older links, you'll want to preserve old links or at least redirect to your new ones. Here is how it is done

Wyam handles these via the Meta-refresh tag on specific pages

## Setting up automatic deployment with TravisCI and GitHub Pages

TravisCI is a super powerful CI/CD tool with free plans for open source. It's super easy to tie it to your GitHub account and add your repository for building.

![addtravis](images\travis.PNG)

Find your GH pages repo and turn it on.

![repo](images\ghrepo.PNG)

I suggest only building on official pushes and not PR's because it is possible for anyone to craft a malicious PR to output secrets from travis. Also I recommend only building when `.travis.yml` files are present to prevent gratuituous error emails in your inbox before repo is ready for prime time.

![settings](images\travis-settings.PNG)


## Using CloudFlare CDN for HTTPS

CloudFlare is super useful (and free) for setting up HTTPS for your GitHub pages, and for the free tier account it is very full featured. If you aren't too squeamish about surrendering your NS (name server) records, it is pretty simple.

First, sign up for a free account on [cloudflare](https://www.cloudflare.com/)

Second, CloudFlare can scan the DNS records in your site and let you know if there will be any problems migrating.

![dnsscan](images\cloudflarescan.PNG)

Third, update your name server records to point to CloudFlare's names servers so the can serve up DNS on your behalf. In my case, I use a service called DNSimple.com but you may use GoDaddy or NameCheap as your registrar.

![name server](images\dnsimplenameservers.PNG)

Last, is to setup your free SSL certificate by switching the SSL drop down to "full", this can take some time so keep that in mind. The CloudFlare site says up to 24 hours (but from experience it seems to finish in about an hour or so).

![crypto](images\cloudflare-crypto.PNG)

Once everything has been provisioned and propagated you'll notice that CloudFlare is serving your domain off of a SAN certificate.

![san1](images\san-cert.PNG)

![san2](images\cloudflarescan2.PNG)


We are done! The new Wyam blog platform is now ready for new posts and is on a more sustainable and secure set of technologies. Hopefully you find this useful, let me know what you think.

-Erik

