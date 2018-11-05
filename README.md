# Springboot-language-support.
technical document for language support


(*) in configuration file..
//	language support
	@Bean
	public LocaleResolver localeResolver() {
		SessionLocaleResolver slr = new SessionLocaleResolver();
		slr.setDefaultLocale(Locale.US);
		return slr;
	}
	
	
//	language support	
	@Bean
	public ResourceBundleMessageSource messageSource() {
		ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();
		messageSource.setBasename("i18n/messages");
		messageSource.setUseCodeAsDefaultMessage(true);
		return messageSource;
	}


(*) in controller
// language support
	@Autowired
	private ResourceBundleMessageSource resource;
// language support
	@Autowired
	private HttpServletRequest request;


(*) Controller implementation....
	String deviceId = request.getHeader("DeviceId");
// language support
	String lang = request.getHeader("Accept-Language") + "";
	
	resource.getMessage(x.getDefaultMessage(), null, new Locale(lang))
	
	result.setMessage(errors.getAllErrors().stream()
					.map(x -> resource.getMessage(x.getDefaultMessage(), null, new Locale(lang)))
					.collect(Collectors.joining(",")));
	
	result.setMessage(resource.getMessage("customer.error.invalid", null, new Locale(lang)));


