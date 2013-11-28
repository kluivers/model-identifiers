model-identifiers
=================

Apple model identifiers. Gives you an approximation of the device based on the model identifier.

Each entry provides the following information (if available):

 - **Device** - the device name (eg. MacBook Pro, iPad 2, iPad Air)
 - **Generation** - device generation (eg. Late 2006)
 - **Variant** - variants within the same generation (eg. 17-inch, Retina)

## About

Created by [Joris Kluivers](http://joris.kluivers.nl) ([@kluivers](http://twitter.com/kluivers) on Twitter).

When using this file consider:

 - Bitcoin: `1AKhoHUVfcQ3E5PApytySgDwPgL3PpbyoF`
 - Litecoin: `LZyxW1Czfrrf7hfst6qztMgpWDxpeXDAjp`
 
 
## Find the identifier

To find your Mac model identifier, on the command line try:

    $ sysctl -n hw.model

or in code:

    #include <sys/types.h>
	#include <sys/sysctl.h>
    
    #if TARGET_OS_IPHONE
		char *propertyName = "hw.machine";
	#else
		char *propertyName = "hw.model";
	#endif
    
    size_t size;
    
    // Mac: use 'hw.model'. On iOS use 'hw.machine'
	sysctlbyname(propertyName, NULL, &size, NULL, 0);
	
	char *model = malloc(size);
	sysctlbyname(propertyName, model, &size, NULL, 0);
	
	// model identifier as NSString
	NSString *modelIdentifier = [NSString stringWithCString:model encoding:NSUTF8StringEncoding];
	
	free(model);
	


### Identifier Uniqueness
Be aware that a single identifier may refer to multiple models from different years or with different characteristics. In this case the `Generation` and/or the `Variant` could not be determined exactly and the key may be missing.

Somewhere around 2010 this practice was changed and from that point on most models have their own unique identifier. 

 
## Sources
 
Related Apple support pages:

- [How to identify iMac models](http://support.apple.com/kb/ht1758)
- [How to identify your MacBook Air](http://support.apple.com/kb/HT3255)
- [EFI and SMC firmware updates for Intel-based Macs](http://support.apple.com/kb/ht1237)
