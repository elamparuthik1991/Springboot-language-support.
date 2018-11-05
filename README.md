# Spring boot- multiple language support

This code will support multiple languages.
1. we need to create folder in "src/main/resources".
2. folder name may be "i18n".
3. inside "i18n" we need to create properties file.
4. messages.properties is the default file.
5. messages_ta.properties is the tamil language property file, key word is "ta".(*) "ta" need to be passed in "Accept-Language" header.
6. all the APIs need to send "Accept-Language" header for getting language support, else it will take messages.properties.

## Step-1  Configuration

### Inside @Configuration we need to include @Bean the general concept.

```java
@Bean
public LocaleResolver localeResolver() {
    SessionLocaleResolver slr = new SessionLocaleResolver();
    slr.setDefaultLocale(Locale.US);
    return slr;
}
```
```java
@Bean
public ResourceBundleMessageSource messageSource() {
    ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();
    messageSource.setBasename("i18n/messages");
    messageSource.setUseCodeAsDefaultMessage(true);
    return messageSource;
}
```

## Step-2  Controller implementation.
### For including bean we need to use @Autowired and use @Bean Model name.

```java
@Autowired
private ResourceBundleMessageSource resource;
```
### For getting all request we need HttpServletRequest to be @Autowired.
```java
@Autowired
private HttpServletRequest request;
```
### Inside the @GetRequest("\") or @PostRequest("\") method we need to include following code. 
### response.getMessage() will have code "uesrId.error.exist" and it will get from language properties file.

```java
String lang = "" + request.getHeader("Accept-Language");
String errorMessage = resource.getMessage("userId.error.exist", null, new Locale(lang));
```
## Conclution
   End of this code implemevtation you will able to find language supported..
any clarification you may contact me at "elamparuthik1991@gmail.com".
