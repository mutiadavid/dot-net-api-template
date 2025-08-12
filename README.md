# .NET Web API Boilerplate Template
<p align="center">
  <span>English</span> |
  <a href="https://github.com/yanpitangui/dotnet-api-boilerplate/tree/main/translations/pt-br/README.md">Português</a>
</p>

A ``.Net 9.0`` WebApi boilerplate / template project. MediatR, Swagger, ~~AutoMapper~~ Mapster, Serilog and more implemented. 

[![Build](https://github.com/yanpitangui/dotnet-api-boilerplate/actions/workflows/build.yml/badge.svg)](https://github.com/yanpitangui/dotnet-api-boilerplate/actions/workflows/build.yml)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=yanpitangui_dotnet-api-boilerplate&metric=coverage)](https://sonarcloud.io/dashboard?id=yanpitangui_dotnet-api-boilerplate)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=yanpitangui_dotnet-api-boilerplate&metric=alert_status)](https://sonarcloud.io/dashboard?id=yanpitangui_dotnet-api-boilerplate)

The goal of this project is to be a kickstart to your .Net WebApi, implementing the most common used patterns
and technologies for a restful API in .net, making your work easier.

## 🚀 Using This Template

This project is now configured as a .NET template that you can install and use to create new projects with customizable names and settings.

### Install the Template

1. **From this repository:**
   ```bash
   git clone <this-repo-url>
   cd dot-net-api-template
   dotnet new install .
   ```

2. **Verify installation:**
   ```bash
   dotnet new list
   # Look for ".NET Web API Boilerplate" with short name "webapi-boilerplate"
   ```

### Create a New Project

#### Basic Usage
```bash
# Create a new project with default settings
dotnet new webapi-boilerplate -n "MyAwesomeApi"
cd MyAwesomeApi
```

#### Advanced Usage with Custom Parameters
```bash
# Create with custom configuration
dotnet new webapi-boilerplate \
  -n "MyCompanyApi" \
  --CompanyName "MyCompany" \
  --Port0 8080 \
  --Port1 8081 \
  --EnableDocker true \
  --EnableSwagger true
```

#### Available Template Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `ProjectName` | string | "MyWebApi" | The name of your project (replaces "Boilerplate") |
| `CompanyName` | string | "MyCompany" | Your company/organization name |
| `Port0` | integer | 7122 | HTTP port number for the API |
| `Port1` | integer | 7123 | HTTPS port number for the API |
| `EnableSwagger` | bool | true | Include Swagger/OpenAPI documentation |
| `EnableDocker` | bool | true | Include Docker support files |

### Template Features

When you create a new project using this template:
- ✅ All namespaces will use your `ProjectName`
- ✅ Solution and project files will be properly renamed
- ✅ Docker configurations will use your project name
- ✅ Port numbers will be customized if specified
- ✅ Company references will be updated throughout
- ✅ All "Boilerplate" references will be replaced

### Uninstall Template
```bash
dotnet new uninstall .
```

# How to run your generated project
- Download the latest .Net SDK and Visual Studio/Code/Rider.

## Standalone
1. You may need a running instance of Postgres, with appropriate migrations initialized.
	- You can run just the DB on docker. For that, run the following command: ``docker-compose up -d db-server``. Doing that, the application will be able to reach the container of the db server.
2. Go to the src/YourProjectName.Api folder and run ``dotnet run``, or, in visual studio set the api project as startup and run as console/docker/IIS.
3. Visit the URLs shown in your terminal or the ports you configured to access the application's swagger.

## Docker
1. Run ``docker-compose up -d`` in the root directory, or, in visual studio, set the docker-compose project as startup and run. This should start the application and DB.
 - 1. For docker-compose, you should run this command on the root folder: ``dotnet dev-certs https -ep https/aspnetapp.pfx -p yourpassword``
		Replace "yourpassword" with something else in this command and the docker-compose.override.yml file.
This creates the https certificate.
2. Visit the URLs shown in your terminal or the ports you configured to access the application's swagger.

## Running tests
**Important**: You need to have docker up and running. The integration tests will launch a Postgres container and use it to test the API.

In the root folder, run ``dotnet test``. This command will try to find all test projects associated with the sln file.
If you are using Visual Studio, you can also access the Test Menu and open the Test Explorer, where you can see all tests and run all of them or one specifically. 

## Authentication
In this project, some routes requires authentication/authorization. For that, you will have to use the ``api/identity/register`` route to create an account.
After that, you can login using the ``/api/identity/login`` without using cookies and then use received accessToken on the lock (if using swagger) or via the Authorization header on a http request.
For more information, please take a look on swagger documentation.

# This project contains:
- SwaggerUI
- EntityFramework
- Postgres
- Minimal apis
- Strongly Typed Ids
- Test coverage collection
- ~~AutoMapper~~ Mapster
- MediatR
- Feature slicing
- Serilog with request logging and easily configurable sinks
- .Net Dependency Injection
- Resource filtering
- Response compression
- Response pagination
- CI (Github Actions)
- Authentication
- Authorization
- Unit tests
- Integration tests with testcontainers
- Container support with [docker](src/Boilerplate.Api/dockerfile) and [docker-compose](docker-compose.yml)
- OpenTelemetry support (with OLTP as default exporter)
- NuGet Central package management (CPM)

# Project Structure
1. Services
	- This folder stores your apis and any project that sends data to your users.
	1. Boilerplate.Api
		- This is the main api project. Here are all the controllers and initialization for the api that will be used.
	2. docker-compose
		- This project exists to allow you to run docker-compose with Visual Studio. It contains a reference to the docker-compose file and will build all the projects dependencies and run it.
2. Application
	-  This folder stores all data transformations between your api and your domain layer. It also contains your business logic.
	1. Auth
		- This folder contains the login Session implementation.
3. Domain
	- This folder contains your business models, enums and common interfaces.
	1. Boilerplate.Domain
		- Contains business models and enums.
		1. Auth
			- This folder contains the login Session Interface.
4. Infra
	- This folder contains all data access configuration, database contexts, anything that reaches for outside data.
	1. Boilerplate.Infrastructure
		- This project contains the dbcontext, entities configuration and migrations.


# Customizing your generated project
1. Remove/Rename all hero related stuff to your needs.
2. Update business logic, entities, and API endpoints for your domain.
3. Configure your database connection strings and environment variables.
4. Customize Docker settings if needed.
5. Give this repo a star!

# Migrations
To run migrations on your generated project, you need the dotnet-ef tool.
- Run ``dotnet tool install --global dotnet-ef``
- Now, depending on your OS, you have different commands (replace "YourProjectName" with your actual project name):
    1. For windows: ``dotnet ef migrations add InitialCreate --startup-project .\src\YourProjectName.Api\ --project .\src\YourProjectName.Infrastructure\``
    2. For linux/mac: ``dotnet ef migrations add InitialCreate --startup-project ./src/YourProjectName.Api/ --project ./src/YourProjectName.Infrastructure/``
# If you like it, give it a Star
If this template was useful for you, or if you learned something, please give it a Star! :star:

# Thanks
This project has great influence of https://github.com/lkurzyniec/netcore-boilerplate and https://github.com/EduardoPires/EquinoxProject. If you have time, please visit these repos, and give them a star, too!

# About
This boilerplate/template was developed by Yan Pitangui under [MIT license](LICENSE).
