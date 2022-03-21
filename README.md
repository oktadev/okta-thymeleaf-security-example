# Secure Thymeleaf with Spring Webflux Example

This repository contains all the code for [Thymeleaf Templates with Spring WebFlux to Secure Your Apps][blog]. This example illustrates how to protect functionality based on the user authorities and authentication status, and how to prevent CSRF attacks with Spring Security.

**Prerequisites**:

- [HTTPie 3.0.2](https://httpie.io/)
- [Java 11](https://jdk.java.net/java-se-ri/11)
- [Okta CLI 0.10.0](https://cli.okta.com)

> [Okta](https://developer.okta.com/) has Authentication and User Management APIs that reduce development time with instant-on, scalable user infrastructure. Okta's intuitive API and expert support make it easy for developers to authenticate, manage and secure users and roles in any application.

* [Getting Started](#getting-started)
* [Links](#links)
* [Help](#help)
* [License](#license)

## Getting started

To install this example, first clone this repository:

```bash
git clone https://github.com/oktadev/okta-thymeleaf-security-example.git thymeleaf-security
```

### Configure Okta authentication

```shell
cd thymeleaf-security
```

With the Okta CLI, register for a free developer account:

```shell
okta register
```

Provide the required information. Once you complete the registration, create a client application with the following command:

```shell
okta apps create
```

You will be prompted to select the following options:

- Application name: **thymeleaf-security**
- Type of Application: **Web**
- Type of Application: **Okta Spring Boot Starter**
- Redirect URI: **Default**
- Post Logout Redirect URI: **Default**

The OktaCLI will create the client application and configure the issuer, clientId and client secret in `src/main/resources/application.properties`. Update the `issuer`, `client-id`, and `client-secret` in `application.yml`. Delete `application.properties`.

```yml
okta:
  oauth2:
    issuer: https://{yourOktaDomain}/oauth2/default
    client-id: {clientId}
    client-secret: {clientSecret}
```

### Enable the scope `quiz` in your Okta authorization server

Sign in to the Okta Admin Console, and in the left menu, go to **Security > API**. Choose the **default** authorization server. In the **Scopes** tab, click **Add Scope**. Set the scope name as `quiz` and add a description, leave all the remaining fields with default values and click on **Create**.

### Run with Maven

In the project root, generate the application container image with the following Maven command:

```shell
./mvnw spring-boot:run
```

Once the application is up, go to `http://localhost:8080/` and sign in with your Okta credentials.

## Links

This example uses the following open source libraries from Okta:

* [Okta CLI](https://cli.okta.com)
* [Okta Spring Boot Starter](https://github.com/okta/okta-spring-boot)

## Help

Please post any questions as comments on the [blog post][blog], or visit our [Okta Developer Forums](https://devforum.okta.com/).

## License

Apache 2.0, see [LICENSE](LICENSE).

[blog]: https://developer.okta.com/blog/2022/03/22/thymeleaf-security
