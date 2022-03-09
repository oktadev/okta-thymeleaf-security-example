# Tutorial: Securing your application when using Thymeleaf templates with Spring Webflux

This repository contains all the code for the Thymeleaf Spring Boot tutorial, illustrating how to protect functionality based on the user authorities and authentication status, and how to prevent CSRF attacks with Spring Security.

**Prerequisites**:
- [Java OpenJDK 11](https://jdk.java.net/java-se-ri/11)
- [Okta CLI 0.9.0](https://cli.okta.com)

## Getting started

To install this example, first clone this repository:

```bash
git clone https://github.com/indiepopart/thymeleaf-security.git
```

## Configure Okta authentication

```shell
cd thymeleaf-security
```

With OktaCLI, register for a free developer account:

```shell
okta register
```
Provide the required information. Once you complete the registration, create a client application with the following command:

```shell
okta apps create
```
You will be prompted to select the following options:

- Application name: thymeleaf-security
- Type of Application: Web
- Type of Application: Okta Spring Boot Starter
- Redirect URI: Default
- Post Logout Redirect URI: Default

The OktaCLI will create the client application and configure the issuer, clientId and clientSecret in `src/main/resources/application.properties`. Update the `issuer`, `client-id` and `client-secret` in `application.yml`. Delete `application.properties`.

```yml
okta:
  oauth2:
    issuer: https://{yourOktaDomain}/oauth2/default
    client-id: {clientId}
    client-secret: {clientSecret}
```

## Enable the scope `quiz` in your Okta authorization server

Sign in to the Okta dashboard, and in the left menu, go to **Security > API**, the choose the **default** authorization server. In the **Scopes** tab, click **Add Scope**. Set the scope name as `quiz` and add a description, leave all the remaining fields with default values and click on **Create**.

## Run with Maven

In the project root, generate the application container image with the following Maven command:

```shell
./mvnw spring-boot:run
```

Once the application is up, go to http://localhost:8080/ and sign in with your Okta credentials.
