---
layout: default
built_from_commit: 922313f3b1cc7f14c799bddb4e354e45b29be180
title: 'Resource Type: filebucket'
canonical: "/puppet/latest/types/filebucket.html"
---

> **NOTE:** This page was generated from the Puppet source code on 2019-07-24 15:17:23 -0700

filebucket
-----

* [Attributes](#filebucket-attributes)

<h3 id="filebucket-description">Description</h3>

A repository for storing and retrieving file content by MD5 checksum. Can
be local to each agent node, or centralized on a puppet master server. All
puppet masters provide a filebucket service that agent nodes can access
via HTTP, but you must declare a filebucket resource before any agents
will do so.

Filebuckets are used for the following features:

- **Content backups.** If the `file` type's `backup` attribute is set to
  the name of a filebucket, Puppet will back up the _old_ content whenever
  it rewrites a file; see the documentation for the `file` type for more
  details. These backups can be used for manual recovery of content, but
  are more commonly used to display changes and differences in a tool like
  Puppet Dashboard.

To use a central filebucket for backups, you will usually want to declare
a filebucket resource and a resource default for the `backup` attribute
in site.pp:

    # /etc/puppetlabs/puppet/manifests/site.pp
    filebucket { 'main':
      path   => false,                # This is required for remote filebuckets.
      server => 'puppet.example.com', # Optional; defaults to the configured puppet master.
    }

    File { backup => main, }

Puppet master servers automatically provide the filebucket service, so
this will work in a default configuration. If you have a heavily
restricted `auth.conf` file, you may need to allow access to the
`file_bucket_file` endpoint.

<h3 id="filebucket-attributes">Attributes</h3>

<pre><code>filebucket { 'resource title':
  <a href="#filebucket-attribute-name">name</a>   =&gt; <em># <strong>(namevar)</strong> The name of the...</em>
  <a href="#filebucket-attribute-path">path</a>   =&gt; <em># The path to the _local_ filebucket; defaults to...</em>
  <a href="#filebucket-attribute-port">port</a>   =&gt; <em># The port on which the remote server is...</em>
  <a href="#filebucket-attribute-server">server</a> =&gt; <em># The server providing the remote filebucket...</em>
  # ...plus any applicable <a href="{{puppet}}/metaparameter.html">metaparameters</a>.
}</code></pre>

<h4 id="filebucket-attribute-name">name</h4>

_(**Namevar:** If omitted, this attribute's value defaults to the resource's title.)_

The name of the filebucket.

([↑ Back to filebucket attributes](#filebucket-attributes))

<h4 id="filebucket-attribute-path">path</h4>

The path to the _local_ filebucket; defaults to the value of the
`clientbucketdir` setting.  To use a remote filebucket, you _must_ set
this attribute to `false`.

([↑ Back to filebucket attributes](#filebucket-attributes))

<h4 id="filebucket-attribute-port">port</h4>

The port on which the remote server is listening.

This setting is _only_ consulted if the `path` attribute is set to `false`.

If this attribute is not specified, the first entry in the `server_list`
configuration setting is used, followed by the value of the `masterport`
setting if `server_list` is not set.

([↑ Back to filebucket attributes](#filebucket-attributes))

<h4 id="filebucket-attribute-server">server</h4>

The server providing the remote filebucket service.

This setting is consulted only if the `path` attribute is set to `false`.

If this attribute is not specified, the first entry in the `server_list`
configuration setting is used, followed by the value of the `server` setting
if `server_list` is not set.

([↑ Back to filebucket attributes](#filebucket-attributes))





> **NOTE:** This page was generated from the Puppet source code on 2019-07-24 15:17:23 -0700