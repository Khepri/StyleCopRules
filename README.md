SaneCop
=======

StyleCop settings intended to help rather than harm your project.

# Assessment of rules


## Documentation Rules (SA1600-)

### Sane

* [SA1603: DocumentationMustContainValidXml](http://www.stylecop.com/docs/SA1603.html)

  There is no reason to ever accept invalid XML.

* [SA1604: ElementDocumentationMustHaveSummary](http://www.stylecop.com/docs/SA1604.html)

  I can't think of any meaningful exceptions to this rule - provided you have a documentation element, it should have a summary.

* [SA1608: ElementDocumentationMustNotHaveDefaultSummary](http://www.stylecop.com/docs/SA1604.html)

  Obvious and admirable! A shame that so many of the other StyleCop rules for documentation invite developers to commit the exact same sin by turning to autogenerated documentation to fulfill a meaningless demand.

### Insane

* [SA1600: ElementsMustBeDocumented](http://www.stylecop.com/docs/SA1600.html)

  No, I don't think they must. Mandatory documentation of all code elements inevitably leads to autogeneration of documentation based on the code elements themselves - hence the documentation can obviously not tell you anything not already in the code, obviating the need for the documentation in the first place. The result is "undocumentation" that clutters the code and harms readability.

* [SA1601: PartialElementsMustBeDocumented](http://www.stylecop.com/docs/SA1601.html)
 
  Ref SA1600.

* [SA1602: EnumerationItemsMustBeDocumented](http://www.stylecop.com/docs/SA1602.html)

  The StyleCop documentation for this rule nicely illustrates the type of meaningless undocumentation you incur on your code base when this rule is enabled. "Dog: Represents a dog."

* [SA1605: PartialElementDocumentationMustHaveSummary](http://www.stylecop.com/docs/SA1605.html)

  I see no reason for applying this rule.
  
* [SA1609: PropertyDocumentationMustHaveValue](http://www.stylecop.com/docs/SA1609.html)

  Reading the StyleCop documentation for this rule is sufficient to realize it is nonsense. What you possibly write that is not already covered by the name of the property or the summary description? The documentation of the value is doomed to become a hollow echo of the two.

* [SA1611: ElementParametersMustBeDocumented](http://www.stylecop.com/docs/SA1611.html)
  
  While you may sometimes wish to document parameters, it is often not necessary, in particular if the parameter is given a meaningful name. If made mandatory, developers will tend to autogenerate documentation of parameters, resulting in documentation like the following: 
  
  `<param name="profileName>The profile name</param>"`
  
  How does this aid the developer in any way?

* [SA1612: ElementParameterDocumentationMustMatchElementParameters](http://www.stylecop.com/docs/SA1612.html)

  This is a silly rule that means you must either document all the parameters or not at all. The developer should be free to document exactly the parameters that need documentation.
  
* [SA1615: ElementReturnValueMustBeDocumented](http://www.stylecop.com/docs/SA1615.html)

  While you may sometimes wish to document the return value, it is often not not necessary.
  If made mandatory, developers will tend to autogenerate documentation of the return value, yielding documentation like the following:
  
  `<returns>The <see cref="Foo">.</returns>`
  
  How does this aid the developer in any way?
  
* [SA1618: GenericTypeParametersMustBeDocumented](http://www.stylecop.com/docs/SA1618.html)

  I'm struggling to come up with a scenario where you may say something about the generic type parameter besides the obvious fact that it is a generic type parameter (which is the example given in the StyleCop documentation). And of course that's completely redundant and silly.

* [SA1619: GenericTypeParametersMustBeDocumentedPartialClass](http://www.stylecop.com/docs/SA1619.html)

  Ref SA1618.


## Layout Rules (SA1500-)

### Sane

### Insane


## Maintainability Rules (SA1400-)


## Naming Rules (SA1300-)


## Ordering Rules (SA1200-)


## Readability Rules (SA1100-)


## Spacing Rules (SA1000-)
