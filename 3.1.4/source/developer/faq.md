# Frequently asked questions (for developers)

## Plugin developement

### How many extensions can a plugin advertise?

There is no limit on "how much" functionality a plugin may add. Normally every plugin should consist of a small number of extension points and supporting files all tightly related to the same topic.

### Can several plugins implementing the same authentication method coexist?

Yes (in the sense those plugins can all be started), however only one plugin can be associated to an authentication method at a time. Also, if a plugin bundles several extensions mapping to the same acr, only one of them will take effect. The rest will be skipped.

### Can I use dependency injection in my plugins?

No. You can merely obtain certain managed bean references by using the `org.gluu.casa.misc.Utils` class.

### How do I use an external java library to my plugin?

Simply add it to your project as you normally would. Ensure the jar files needed will be part of the resulting fat jar (aka "jar with dependencies"). Check the runtime libraries already available in casa (see [dependencies](./intro-plugin#dependencies)), if you find something you can use there, just assign a `provided` scope to the dependency you are interested in.

### How do I have access to objects such as the HTTP request?

You don't normally need to, but here is an example on how to obtain references to `javax.servlet.http.HttpServletRequest` and `javax.servlet.http.HttpSession` objects respetively:

```
Execution current = Executions.getCurrent();
request = (HttpServletRequest) current.getNativeRequest();
session = (HttpSession) current.getSession().getNativeSession();
```

## Enrollment APIs

### Are enrollment APIs protected?

Yes. To be able to do any useful interaction, you have to pass in the authorization header of your requests a token.

### How do I obtain a token?

From oxAuth's token endpoint. For this purpose, you have to register a client previously, say, by using oxTrust admin GUI. Ask your administrator for instructions on how to do so and how to pass a token in HTTP headers.


## My problem is not listed here

Feel free to open a [support](https://support.gluu.org/) ticket.