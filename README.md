
<div id="rendered" class="markdown-body">
	<h1>Spring boot- multiple language support</h1>
	<p>this code will support multiple languages.</p>
	<h2>Step-1  Configuration</h2>
	<p>
    Inside @Configuration we need to include @Bean is generaral concept. 
	</p>
	<pre>
		<code class="language-bash">
        @Bean
        public LocaleResolver localeResolver() {
          SessionLocaleResolver slr = new SessionLocaleResolver();
          slr.setDefaultLocale(Locale.US);
          return slr;
        }
    </code>
	</pre>
  <pre>
		<code class="language-bash">
        @Bean
        public ResourceBundleMessageSource messageSource() {
          ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();
          messageSource.setBasename("i18n/messages");
          messageSource.setUseCodeAsDefaultMessage(true);
          return messageSource;
        }
    </code>
	</pre>
	<h2>Step-2  Controller implementation.</h2>
	<p>
    For including bean we need to use @Autowired and use @Bean Model name.
	</p>
	<pre>
		<code class="language-bash">
        @Autowired
	      private ResourceBundleMessageSource resource;
    </code>
	</pre>
	<p>
    For getting all request come to api we need HttpServletRequest to be @Autowired.
	</p>
	<pre>
		<code class="language-bash">
        @Autowired
	      private HttpServletRequest request;
    </code>
	</pre>
	<p>
    Inside the @GetRequest("\") or @PostRequest("\") method we need to include following code.<br/>
    response.getMessage() will have code("uesrId.error.exist") and it will get from language properties file.
	</p>
  <pre>
		<code class="language-bash">
      String lang = request.getHeader("Accept-Language") + "";
      String errorMessage = resource.getMessage("userId.error.exist", null, new Locale(lang));
    </code>
	</pre>
	
	<p>
    (*) we need to create folder in "src/main/resources".<br/> 
    (*) folder name must be "i18n".<br/>
    (*) inside "i18n" we need to create properties file.<br/>
    (*) messages.properties is default file.<br/>
    (*) messages_fr.properties is franse language property file, key word is "fr".<br/>
    (*) "fr" need to be passed in "Accept-Language" header.<br/>
    (*) all the APIs need to send "Accept-Language" header for getting language support, else it will take messages.properties.
	</p>
  
  
</div>
