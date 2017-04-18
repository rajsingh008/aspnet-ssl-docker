# Supported tags and respective `Dockerfile` links

- [`4.6.2-windowsservercore-10.0.14393.321`, `4.6.2-windowsservercore`, `4.6.2`, `latest` (*4.6.2/Dockerfile*)](https://github.com/rgarita/aspnet-ssl-docker/blob/master/4.6.2/Dockerfile)
- [`3.5` (*3.5/Dockerfile*)](https://github.com/rgarita/aspnet-ssl-docker/blob/master/3.5/Dockerfile)

These images are updated via [pull requests to the `rgarita/aspnet-docker` GitHub repo](https://github.com/rgarita/aspnet-ssl-docker/pulls).

[![Downloads from Docker Hub](https://img.shields.io/docker/pulls/rgarita/aspnet-ssl.svg)](https://hub.docker.com/r/rgarita/aspnet-ssl)
[![Stars on Docker Hub](https://img.shields.io/docker/stars/rgarita/aspnet-ssl.svg)](https://hub.docker.com/r/rgarita/aspnet-ssl)

# What is ASP.NET

ASP.NET is a high productivity framework for building Web Applications using Web Forms, MVC, Web API and SignalR.

This repository contains `Dockerfile` definitions for ASP.NET Docker images. These images use the [ASPNET image](https://hub.docker.com/r/microsoft/aspnet/) as their base.

This image contains:
- Windows Server Core as the base OS
- IIS 10 as Web Server
- .NET Framework 4.6.2 (or 3.5)
- .NET Extensibility for IIS
- Self Signed Cert

# How to use these Images

Copy `4.6.2\sample\Dockerfile` to your app directory. You would then be able to build and run the site from the app directory.

```
$ docker build -t aspnet-site --build-arg site_root=/
$ docker run -d -p 8000:80 --name my-running-site aspnet-site
```

There is no need to specify an `ENTRYPOINT` in your Dockerfile since the `microsoft/aspnet` base image already includes an entrypoint application that monitors the status of the IIS World Wide Web Publishing Service (W3SVC).

### Verify in the browser

> With the current release, you can't use `http://localhost` to browse your site from the container host. This is because of a known behavior in WinNAT, and will be resolved in future. Until that is addressed, you need to use the IP address of the container.

Once the container starts, you'll need to finds its IP address so that you can connect to your running container from a browser. You use the `docker inspect` command to do that:

`docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-running-site`

You will see an output similar to this:

```
172.28.103.186
```

You can connect the running container using the IP address and configured port, `http://172.28.103.186` in the example shown.

For a comprehensive tutorial on running an ASP.NET app in a container, check out [the tutorial on the docs site](https://docs.microsoft.com/en-us/dotnet/articles/framework/docker/aspnetmvc).

## Image variants

The `microsoft/aspnet` images come in different flavors, each designed for a specific use case.

### `4.6.2`

This image is for ASP.NET application built for Framework 4.0 and later version. It is based on the [ASPNET Image](https://hub.docker.com/r/microsoft/aspnet/) and includes the .NET Framework and .NET 4.6.2 Extensibility for IIS.

### `3.5`

This image is for ASP.NET application built for Framework 3.5 and later version. It is based on the [ASPNET Image](https://hub.docker.com/r/microsoft/aspnet/) and includes the .NET Framework and .NET 3.5 Extensibility for IIS.

# Related Repos

See the following related repos for other application types:

- [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) for ASP.NET Core applications.
- [microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/) for .NET Core images.
- [microsoft/dotnet-framework](https://hub.docker.com/r/microsoft/dotnet-framework/) for .NET Framework applications.

# License

View [license information](https://www.microsoft.com/net/dotnet_library_license.htm) for the software contained in this image. 

Windows Container images are licensed per the Windows license:

MICROSOFT SOFTWARE SUPPLEMENTAL LICENSE TERMS

CONTAINER OS IMAGE

Microsoft Corporation (or based on where you live, one of its affiliates) (referenced as “us,” “we,” or “Microsoft”) licenses this Container OS Image supplement to you (“Supplement”). You are licensed to use this Supplement in conjunction with the underlying host operating system software (“Host Software”) solely to assist running the containers feature in the Host Software. The Host Software license terms apply to your use of the Supplement. You may not use it if you do not have a license for the Host Software. You may use this Supplement with each validly licensed copy of the Host Software.

# Supported Docker versions

This image is officially supported on Docker version 1.12.2.

Please see [the Docker installation documentation](https://docs.docker.com/installation/) for details on how to upgrade your Docker daemon.

# User Feedback

## Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/microsoft/aspnet-iis-docker/issues).

## Documentation

You can read [documentation for ASP.NET](https://asp.net/), including Docker usage in the [.NET docs](https://docs.microsoft.com/en-us/dotnet/articles/framework/docker/aspnetmvc). The docs are also [open source on GitHub](https://github.com/dotnet/core-docs). Contributions are welcome!
