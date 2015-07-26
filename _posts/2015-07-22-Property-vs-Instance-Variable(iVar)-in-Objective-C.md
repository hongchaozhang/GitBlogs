---
layout: default
comments: true
category: code
tags: [ios]
title: Property vs Instance Variable (iVar) in objective-c
---
---

## Description

To declare a variable in a objective-c class, we have the following two ways:

* Property

		@interface Photo : NSObject
		@property (nonatomic, strong) NSString *photographer;
		@end

* Instance Variable (iVar)

		@interface Photo : NSObject {
		    NSString *photographer;
		}
		@end
		
Then, what's the difference?

## Differences

### private vs public

For a private/protected variable, use iVar; for a public variable, use property. If you want to use the benifit of property attributes, like retain, nonatomic etc., declare the property in the implementation file as a private property.

### usage

Directly use an iVar inside the class, for example, `photographer`. But use `self.` for a property, for example, `self.photographer`.

### performance

iVar is faster than property, as property will call the `getter` or `setter` functions. When you declare a property, the compiler will add `getter` and `setter` functions for the property.

### @synthesize for property

If you add `@synthesize photographer` in the implementation, compiler will automatically add an iVar `photographer` and `_photographer` to the class. You can directly use `photographer` or `_photographer` instead of `self.photographer` to get or set the value. The iVar method is faster, but keep in mind that it will not call the `getter` or `setter` method.

If you declare the class like:

	@interface Photo : NSObject {
		NSString *photographer;
	}
	@property (nonatomic, strong) NSString *photographer;
	@end

There are actually two `photographer` variables in the class: when you use `photographer` directly, you are using the iVar, and when you use `self.photographer`, you are using the property.

However, when you use `@synthesize photographer` in the implementation file, the compoler will add `photographer` variable for the property. That is to say, `photographer` will be the property, and the iVar will not be usable.

## References

A more detailed description is [here](http://stackoverflow.com/questions/9086736/why-would-you-use-an-ivar).

[reference](http://stackoverflow.com/questions/2032826/property-synthesize), answer by *Rachel Henderson*

<del>*Property* session of the </del>[<del>reference</del>](http://www.cocoadevcentral.com/d/learn_objectivec/). <del>This post is old fashioned</del>.

[Here](http://blog.csdn.net/likendsl/article/details/7345485) has a good explaination.
