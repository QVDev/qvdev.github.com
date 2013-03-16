---
layout: post
title: "JSON to Object mapping"
description: ""
category: "ios"
tags: [ios,JSON,Object mapping]
---
{% include JB/setup %}
<br>
Recently I needed to create object from a JSON response in IOS. After some researching and fooling around 
with some ios libraries. I could not find something simple and easy to use. Most of the libraries are
doing more then just creating objects from the JSON. So I decided too look into on how much trouble it could
be to create this myself. In this post I will explain in detail what I did to make my own Objects from JSON without
using any libraries that take space for stuff you don't need.
<br><br>
<!-- more start -->
So for example you have the next JSON:
{% highlight objective-c %}
{
  "identifier": "511d5f71ad0234001251e5a5",
  "action": "pass",
  "point": "1500",
  "geolocation": [
    "13.3904",
    "52.506433"]
}
{% endhighlight %}

And want to have an simple object that can refer to this data as easy as testObject.identifier or testObject action. 
All we need to do is create a new class. And do the following in the .h file for every JSON atribute: 

{% highlight objective-c %}
@interface OBTestObject : NSObject
@property(nonatomic, strong) NSString *identifier;
@property(nonatomic, strong) NSString *action;
@property(nonatomic, copy) NSNumber * point;
@property(nonatomic, copy) NSArray *geolocation;
@end
{% endhighlight %}

And do the following in the .m file

{% highlight objective-c %}
@implementation OBTestObject
//This for catching unknown properties
-(void)setValue:(id)value forUndefinedKey:(NSString*)key
{
    NSLog(@"Error: setting unknown key: %@ with data: %@", key, value);
}
-(void)encodeWithCoder:(NSCoder*)encoder
{
    [encoder encodeObject:self. identifier forKey:@"identifier"];
	[encoder encodeObject:self.action forKey:@"action"];
	[encoder encodeObject:self.point forKey:@"point"];
	[encoder encodeObject:self.geolocation forKey:@"geolocation"];
}
-(id)initWithCoder:(NSCoder*)decoder
{
    self = [super init];
    if (self) {
    	self.identifier = [decoder decodeObjectForKey:@"identifier"];
		self.action = [decoder decodeObjectForKey:@"action"];
		self.point = [decoder decodeObjectForKey:@"point"];
		self.geolocation = [decoder decodeObjectForKey:@"geolocation"];
    }
    return self;
}
@end
{% endhighlight %}
Ok so now we have setup the whole model and can be used as follow.
{% highlight objective-c %}
OBTestObject* testObject = [[OBTestObject alloc] 
[testObject setValuesForKeysWithDictionary:JSON];
{% endhighlight %}
and thats it, now all the values from the JSON are mapped to the object you just made and can be used easily.<br>
This can be done even with custom objects in the JSON. I will explain this as a second part.
<!-- more end --> 