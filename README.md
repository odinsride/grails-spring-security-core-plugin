# grails-spring-security-core-plugin
Example repo to replicate issue using Spring Security Core plugin > 4.0.0 in a Grails plugin which is created using the 'plugin' profile

Link to issue: https://github.com/grails-plugins/grails-spring-security-core/issues/627

### Task List

- [x] Steps to reproduce provided
- [x] Stacktrace (if present) provided
- [x] Example that reproduces the problem uploaded to Github
- [x] Full description of the issue provided (see below)

### Steps to Reproduce

1. Create new Grails plugin using the "plugin" profile:
`$ grails create-plugin com.odinsride.grails-spring-security-core-plugin --profile=plugin`
2. Add spring-security-core >= v4.0.0 to `build.gradle`:
`compile "org.grails.plugins:spring-security-core:4.0.3"`
3. Compile the plugin:
`$ grails compile`

### Expected Behaviour

The Grails plugin compiles successfully.

### Actual Behaviour

Compilation fails on the `compileGroovy` task with the following message:

```CONFIGURE SUCCESSFUL in 10s
> Task :compileGroovy FAILED
2 actionable tasks: 1 executed, 1 up-to-date
<-------------> 0% WAITING
> IDLE

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':compileGroovy'.
> BUG! exception in phase 'canonicalization' in source unit 'C:\dev\grails\upgrade-4.0\grails-spring-security-core-plugin\grails-app\init\com\odinsride\Application.groovy' org.springframework.web.servlet.config.annotation.EnableWebMvc

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org
| Error Gradle build terminated with error: org.springframework.web.servlet.config.annotation.EnableWebMvc (Use --stacktrace to see the full trace)
```

I will also note that performing the exact same steps but omitting the `--profile=plugin` flag (which uses the web-plugin profile) does not exhibit this error message.

Further, I found that in a plugin generated with the `plugin` profile, if the following dependency is defined in `build.gradle`, the plugin will compile without the above error:

```
compile "org.grails:grails-web-boot"
```

### Environment Information

- **Operating System**: Windows 10
- **GORM Version:** 7.0.8.RELEASE
- **Grails Version (if using Grails):** 4.0.6
- **JDK Version:** 1.8 (Adopt OpenJDK)

### Example Application

- https://github.com/odinsride/grails-spring-security-core-plugin
