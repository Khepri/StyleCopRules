StyleCopRules
=============

StyleCop settings intended to help rather than harm your project.

# Introduction

Used correctly, [StyleCop](http://stylecop.codeplex.com/) is a useful tool for enforcing healthy code hygiene in your C# project. Used incorrectly, it can cause considerable harm by prompting developers to resort to bad practices like autogenerating documentation or wasting the developers' time by forcing them to manually keep their code elements sorted. 

StyleCop should be gentle and almost invisible rather than intrusive. It should get out of the developers' way, yet keep them from writing sloppy code by accident. Therefore, there is little room for rules that generate false positives. In general, a candidate rule needs to provide benefits that significantly offset the cost for developers in order to be included in the analysis. When in doubt, it is better to leave a rule out.

This project contains my subjective assessment of the available StyleCop rules, as well as a settings file that corresponds to the assessment.


# Assessment of rules


## Documentation Rules (SA1600-)

I think it's a very bad idea to use a static analysis tool to mandate documentation of all code elements. It inevitably leads to very low-quality documentation. The only reason I can think for doing so is that it leads to high documentation coverage. However, measuring documentation coverage is a completely meaningless exercise because it is easy - trivial - to autogenerate documentation (using ReSharper, GhostDoc or what have you). Autogenerated documentation is worthless. In fact, it's even worse than that: it has negative value. Autogenerated documentation is a source of noise that leads to code that is less readable and makes it harder to find genuine documentation in the code base. 

See http://www.stylecop.com/docs/Documentation%20Rules.html

### Sane

* [SA1603: DocumentationMustContainValidXml](http://www.stylecop.com/docs/SA1603.html)

  There is no reason to ever accept invalid XML.

* [SA1604: ElementDocumentationMustHaveSummary](http://www.stylecop.com/docs/SA1604.html)

  I can't think of any meaningful exceptions to this rule - provided you have a documentation element, it should have a summary.

* [SA1608: ElementDocumentationMustNotHaveDefaultSummary](http://www.stylecop.com/docs/SA1604.html)

  Obvious and admirable! A shame that so many of the other StyleCop rules for documentation invite developers to commit the exact same sin by turning to autogenerated documentation to fulfill a meaningless demand.

* [SA1610: PropertyDocumentationMustHaveValueText](http://www.stylecop.com/docs/SA1610.html)

  Empty documentation is always nonsensical.
  
* [SA1613: ElementParameterDocumentationMustDeclareParameterName](http://www.stylecop.com/docs/SA1613.html)

  This is meaningful granted that you're documenting a parameter.
  
* [SA1614: ElementParameterDocumentationMustHaveText](http://www.stylecop.com/docs/SA1614.html)

  Empty documentation is always nonsensical.
  
* [SA1616: ElementReturnValueDocumentationMustHaveValue](http://www.stylecop.com/docs/SA1616.html)

  This is fine, an empty return tag makes no sense.

* [SA1617: VoidReturnValueMustNotBeDocumented](http://www.stylecop.com/docs/SA1617.html)

  Sure, this is flagging an error.

* [SA1620: GenericTypeParameterDocumentationMustMatchTypeParameters](http://www.stylecop.com/docs/SA1620.html)

  I suppose this makes sense given that the developer has come up with meaningful documentation for the type parameters (but ref SA1618 in the Insane category).

* [SA1621: GenericTypeParameterDocumentationMustDeclareParameterName](http://www.stylecop.com/docs/SA1621.html)

  Ref SA1620.

* [SA1622: GenericTypeParameterDocumentationMustHaveText](http://www.stylecop.com/docs/SA1622.html)

  Ref SA1620.
  
* [SA1625: ElementDocumentationMustNotBeCopiedAndPasted](http://www.stylecop.com/docs/SA1625.html)

  Under serious doubt. Silly to check for, yet hard to envision meaningful duplicate comments. I suppose duplicate comments (due to copy-and-paste) will only happen if the project runs a static analysis tool that requires all code elements to be documented.

* [SA1626: SingleLineCommentsMustNotUseDocumentationStyleSlashes](http://www.stylecop.com/docs/SA1626.html)

  This is OK, no need to use triple-slash for regular code comments.
  
* [SA1627: DocumentationTextMustNotBeEmpty](http://www.stylecop.com/docs/SA1627.html)

  It makes no sense for the documentation text to be empty - in that case the entire documentation of the element should be deleted.

* [SA1644: DocumentationHeadersMustNotContainBlankLines](http://www.stylecop.com/docs/SA1644.html)

  Ambivalent. A bit silly, but fair enough.

* [SA1645: IncludedDocumentationFileDoesNotExist](http://www.stylecop.com/docs/SA1645.html)

  In case _include_ is used the file should clearly exist.

* [SA1646: IncludedDocumentationXPathDoesNotExist](http://www.stylecop.com/docs/SA1646.html)

  Similar to SA1645.

* [SA1647: IncludeNodeDoesNotContainValidFileAndPath](http://www.stylecop.com/docs/SA1647.html)

  Similar to SA1645.
  
* [SA1648: InheritDocMustBeUsedWithInheritingClass](http://www.stylecop.com/docs/SA1648.html)

  I've never seen this tag used, but I suppose it's fine.


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
  
  `<param name="profileName">The profile name</param>`
  
  How does this aid code comprehension in any way?

* [SA1612: ElementParameterDocumentationMustMatchElementParameters](http://www.stylecop.com/docs/SA1612.html)

  This is a silly rule that means you must either document all the parameters or not at all. The developer should be free to document exactly the parameters that need documentation.
  
* [SA1615: ElementReturnValueMustBeDocumented](http://www.stylecop.com/docs/SA1615.html)

  While you may sometimes wish to document the return value, it is often not not necessary.
  If made mandatory, developers will tend to autogenerate documentation of the return value, yielding documentation like the following, which is thoroughly unhelpful:
  
  `<returns>The <see cref="Foo">.</returns>`
  
  How does this aid code comprehension in any way?
  
* [SA1618: GenericTypeParametersMustBeDocumented](http://www.stylecop.com/docs/SA1618.html)

  I'm struggling to come up with a scenario where you may say something about the generic type parameter besides the obvious fact that it is a generic type parameter (which is the example given in the StyleCop documentation). And of course that's completely redundant and silly.

* [SA1619: GenericTypeParametersMustBeDocumentedPartialClass](http://www.stylecop.com/docs/SA1619.html)

  Ref SA1618.

* [SA1623: PropertySummaryDocumentationMustMatchAccessors](http://www.stylecop.com/docs/SA1623.html)

  Completely absurd. We know what properties are and what they do. If we need documentation for a property, we would like to know why it is there - what the purpose is.
  
* [SA1624: PropertySummaryDocumentationMustOmitSetAccessorWithRestricedAccess](http://www.stylecop.com/docs/SA1624.html)

  Huh? If you want to document a property setter of course you should be able to, regardless of access modifier. It would be equally meaningful to prohibit the documentation of private methods.
  
* [SA1628: DocumentationTextMustBeginWithACapitalLetter](http://www.stylecop.com/docs/SA1628.html)
  
  My experience is that this leads to more false than real positives.
  
* [SA1629: DocumentationTextMustEndWithAPeriod](http://www.stylecop.com/docs/SA1629.html)

  My experience is that this leads to more false than real positives.

* [SA1630: DocumentationTextMustContainWhitespace](http://www.stylecop.com/docs/SA1630.html)

  I see no reason to check for this.
  
* [SA1631: DocumentationTextMustMeetCharacterPercentage](http://www.stylecop.com/docs/SA1631.html)
 
  How do you even come up with rules like this?
  
* [SA1632: DocumentationTextMustMeetMinimumCharacterLength](http://www.stylecop.com/docs/SA1632.html)

  This is meaningless. Encourage your developers to write meaningful documentation.

* [SA1633: FileMustHaveHeader](http://www.stylecop.com/docs/SA1633.html)
  
  WAT?
  
* [SA1634: FileHeaderMustShowCopyright](http://www.stylecop.com/docs/SA1634.html)

  HAHAHAHAH!

* [SA1635: FileHeaderMustHaveCopyrightText](http://www.stylecop.com/docs/SA1635.html)

  Stop it.
  
* [SA1636: FileHeaderCopyrightTextMustMatch](http://www.stylecop.com/docs/SA1636.html)

  This is pure trolling.
  
* [SA1637: FileHeaderMustContainFileName](http://www.stylecop.com/docs/SA1637.html)

  Meaningless.

* [SA1638: FileHeaderFileNameDocumentationMustMatchFileName](http://www.stylecop.com/docs/SA1638.html)

  If SA1637 is enabled, yes, but it's not.

* [SA1639: FileHeaderMustHaveSummary](http://www.stylecop.com/docs/SA1639.html)

  But there is no file header. There shouldn't be one.

* [SA1640: FileHeaderMustHaveValidCompanyText](http://www.stylecop.com/docs/SA1640.html)

  Meaningless.

* [SA1641: FileHeaderCompanyNameTextMustMatch](http://www.stylecop.com/docs/SA1641.html)

  Meaningless.

* [SA1642: ConstructorSummaryDocumentationMustBeginWithStandardText](http://www.stylecop.com/docs/SA1642.html)

  This may be the most stupid rule of them all. Standard documentation stating that a constructor creates a new instance of a class? Thank you.

* [SA1643: DestructorSummaryDocumentationMustBeginWithStandardText](http://www.stylecop.com/docs/SA1643.html)

  As stupid as SA1642, but less impact since destructors are scarce.

* [SA1649: FileHeaderFileNameDocumentationMustMatchTypeName](http://www.stylecop.com/docs/SA1649.html)

  But there is still no file header.

* [SA1650: ElementDocumentationMustBeSpelledCorrectly](http://www.stylecop.com/docs/SA1650.html)

  A factory for producing false positives. It's not worth the effort to have developers spend their time maintaining a dictionary to have StyleCop close down that factory. 


## Layout Rules (SA1500-)

I think it's OK to follow some layout rules, to the extent they help the project avoiding code that is simply sloppily written.

See http://www.stylecop.com/docs/Layout%20Rules.html

### Sane

* [SA1500: CurlyBracketsForMultiLineStatementsMustNotShareLine](http://www.stylecop.com/docs/SA1500.html)

  Ambivalent, on occasion it makes sense to have empty curly brackets on a single line.

* [SA1503: CurlyBracketsMustNotBeOmitted](http://www.stylecop.com/docs/SA1503.html)

  Optional curly brackets should not be optional.

* [SA1505: OpeningCurlyBracketsMustNotBeFollowedByBlankLine](http://www.stylecop.com/docs/SA1505.html)

  This is just proper code hygiene.

* [SA1506: ElementDocumentationHeadersMustNotBeFollowedByBlankLine](http://www.stylecop.com/docs/SA1506.html)

  This is just proper code hygiene.

* [SA1507: CodeMustNotContainMultipleBlankLinesInARow](http://www.stylecop.com/docs/SA1507.html)

  This is just proper code hygiene.

* [SA1508: ClosingCurlyBracketsMustNotBePrecededByBlankLine](http://www.stylecop.com/docs/SA1508.html)

  This is just proper code hygiene.

* [SA1509: OpeningCurlyBracketsMustNotBePrecedededByBlankLine](http://www.stylecop.com/docs/SA1509.html)

  This is just proper code hygiene.

* [SA1510: ChainedStatementBlocksMustNotBePrecededByBlankLine](http://www.stylecop.com/docs/SA1510.html)

  This is just proper code hygiene.

* [SA1511: WhileDoFooterMustNotBePrecededByBlankLine](http://www.stylecop.com/docs/SA1511.html)

  This is just proper code hygiene (although I've never seen this violated).
  
* [SA1513: ClosingCurlyBracketMustBeFollowedByBlankLine](http://www.stylecop.com/docs/SA1513.html)

  This is just proper code hygiene.

* [SA1514: ElementDocumentationHeaderMustBePrecededByBlankLine](http://www.stylecop.com/docs/SA1514.html)

  This is just proper code hygiene (and may actually occur in practice).

* [SA1516: ElementsMustBeSeparatedByBlankLine](http://www.stylecop.com/docs/SA1516.html)

  This is just proper code hygiene.

* [SA1517: CodeMustNotContainBlankLinesAtStartOfFile](http://www.stylecop.com/docs/SA1517.html)

  This is just proper code hygiene.

* [SA1518: CodeMustNotContainBlankLinesAtEndOfFile](http://www.stylecop.com/docs/SA1518.html)

  This is just proper code hygiene.


### Insane

* [SA1501: StatementMustNotBeOnSingleLine](http://www.stylecop.com/docs/SA1501.html)

  IMHO the code is sometimes more readable on a single line. YMMV.

* [SA1502: ElementMustNotBeOnSingleLine](http://www.stylecop.com/docs/SA1502.html)

  Sometimes being concise helps readability.

* [SA1504: AllAccessorMustBeMultiLineOrSingleLine](http://www.stylecop.com/docs/SA1504.html)

  Only makes sense if you only ever have trivial property implementation (in which case - heresy! - you might as well have used fields instead, even though .NET lore indicates that this is very bad, m'kay?). It may well be that one accessor (e.g. `get`) is very simple whereas the other one is more complex.

* [SA1512: SingleLineCommentsMustNotBeFollowedByBlankLine](http://www.stylecop.com/docs/SA1512.html)

  I don't quite see the problem and would rather be a bit too permissive than needlessly strict - I wouldn't want to break the build over this.

* [SA1515: SingleLineCommentMustBePrecededByBlankLine](http://www.stylecop.com/docs/SA1515.html)

  Ref SA1512.


## Maintainability Rules (SA1400-)

To claim that these rules vastly improves maintainability is probably stretching it, but they don't put any heavy burdens on the developer either. The false positive ratio will probably be very low.

See http://www.stylecop.com/docs/Maintainability%20Rules.html

### Sane

* [SA1119: StatementMustNotUseUnnecessaryParenthesis](http://www.stylecop.com/docs/SA1119.html)

  Probably just proper code hygiene.

* [SA1400: AccessModifierMustBeDeclared](http://www.stylecop.com/docs/SA1400.html)

  It's probably a good idea to be explicit, but I don't feel strongly about this.

* [SA1401: FieldsMustBePrivate](http://www.stylecop.com/docs/SA1401.html)

  Under severe doubt. This is an etablished "best practice" in the .NET world, but how many developers can provide coherent rationale for this best practice?

* [SA1402: FileMayOnlyContainASingleClass](http://www.stylecop.com/docs/SA1402.html)

  This is the norm, a reader would be very surprised otherwise.

* [SA1403: FileMayOnlyContainASingleNamespace](http://www.stylecop.com/docs/SA1403.html)

  This is the norm, a reader would be very surprised otherwise.

* [SA1404: CodeAnalysisSuppressionMustHaveJustification](http://www.stylecop.com/docs/SA1404.html)

  It's probably always a good idea to provide a reason for suppressing a rule. (If the reason is "the rule is stupid", obviously the rule should be switched off.)
  
* [SA1405: DebugAssertMustProvideMessageText](http://www.stylecop.com/docs/SA1405.html)

  It's probably always a good idea to provide a message; one can only hope that the developer will bother to write a meaningful one. Luckily I think ReSharper is not yet autogenerating such messages!

* [SA1406: DebugFailMustProvideMessageText](http://www.stylecop.com/docs/SA1406.html)

  Ref SA1405.

* [SA1407: ArithmeticExpressionsMustDeclarePrecedence](http://www.stylecop.com/docs/SA1407.html)

  This improves readability.

* [SA1408: ConditionalExpressionsMustDeclarePrecendence](http://www.stylecop.com/docs/SA1408.html)

  This improves readability.

* [SA1409: RemoveUnnecessaryCode](http://www.stylecop.com/docs/SA1409.html)

  Can't think of a reason to allow "empty" code like this.

* [SA1410: RemoveDelegateParenthesisWhenPossible](http://www.stylecop.com/docs/SA1410.html)

  Uncertain. This is not important.

* [SA1411: AttributeConstructorMustNotUseUnnecessaryParenthesis](http://www.stylecop.com/docs/SA1411.html)

  Uncertain. This is not important.


## Naming Rules (SA1300-)

It pretty limited what a purely syntactic analysis tell us about the quality of names.

See http://www.stylecop.com/docs/Naming%20Rules.html

### Sane

* [SA1300: ElementMustBeginWithUpperCaseLetter](http://www.stylecop.com/docs/SA1300.html)

  Fair enough, it's the convention.

* [SA1302: InterfaceNamesMustBeginWithI](http://www.stylecop.com/docs/SA1302.html)

  It's actually a terribly silly rule, but unfortunately it's always been the convention in .NET code that all interfaces should begin with an I. This is the official recommendation from Microsoft. The [naming guidelines](http://msdn.microsoft.com/en-us/library/ms229040%28v=vs.110%29.aspx) tells us to "DO prefix interface names with the letter I, to indicate that the type is an interface.". At the same time, we are told that we should avoid Hungarian notation. It makes no sense. The recommendation probably stems from the misunderstanding that interfaces and classes always go in pairs: one implementing class per interface. Then there's an assumed conflict between the interface and the class as to which one gets the "real" name and which one gets a derivation. According to such a warped view, the choice is between `IFoo` (interface) and `Foo` (class) and `Foo` (interface) and `CFoo` or `FooImpl` (class). A much better solution is to solve this contention by having the class name reflect some concrete aspect of the implementation. An example would be to have a `List` interface with classes `LinkedList` and `ArrayList`. But alas, this battle is lost and there is no point in fighting wind-mills.

* [SA1304: NonPrivateReadonlyFieldsMustBeginWithUpperCaseLetter](http://www.stylecop.com/docs/SA1304.html)

  Uncertain. I suppose the rationale is that non-private fields should have the same syntactic form as properties.

* [SA1307: AccessibleFieldsMustBeginWithUpperCaseLetter](http://www.stylecop.com/docs/SA1307.html)

  Ref SA1304.


### Insane

* [SA1301: ElementMustBeginWithLowerCaseLetter](http://www.stylecop.com/docs/SA1301.html)

  The StyleCop documentation states that this rule is currently never triggered.

* [SA1303: ConstFieldNamesMustBeginWithUpperCaseLetter](http://www.stylecop.com/docs/SA1303.html)

  I can't think of any good reasons for distinguishing syntactically between constants and non-constants - it feels like a watered-down form of Hungarian notation.

* [SA1305: FieldNamesMustNotUseHungarianNotation](http://www.stylecop.com/docs/SA1305.html)

  In my experience this rule only ever leads to false positives: StyleCop will wrongly assume that some field name is written using Hungarian notation. Even though it is possible to whitelist words to prevent StyleCop from flagging false positives on a per-case basis, I think it's a waste of time to teach the analysis tool to avoid false positives when you never experience genuine violations of this rule.

* [SA1306: FieldNamesMustBeginWithLowerCaseLetter](http://www.stylecop.com/docs/SA1306.html)

  I prefer the convention that field names begin with an underscore (ref SA1309). This makes it easy to distinguish between fields (which constitute object state) and variables (which are transient).

* [SA1308: VariableNamesMustNotBePrefixed](http://www.stylecop.com/docs/SA1308.html)

  This is a silly rule preventing a convention I've never seen used in practice. There is no reason to apply rules that have no practical effect. (Of course, if you ever come across developers using this convention, enable this rule at once.)

* [SA1309: FieldNamesMustNotBeginWithUnderscore](http://www.stylecop.com/docs/SA1309.html)

  I feel the exact opposite way: field names should begin with underscore.

* [SA1310: FieldNamesMustNotContainUnderscore](http://www.stylecop.com/docs/SA1310.html)

  I suppose a violation of SA1309 is also a violation of SA1310? Otherwise this rule would be fine.

* [SA1311: StaticReadonlyFieldsMustBeginWithUpperCaseLetter](http://www.stylecop.com/docs/SA1311.html)

  I can't think of any good reasons for distinguishing syntactically between static readonly fields and other fields. It feels like a watered-down form of Hungarian notation.


## Ordering Rules (SA1200-)

In general, I don't think it makes sense to spend the developers' time sorting code elements according to arbitrary criteria like access modifiers or the alphabet. It creates unnecessary work without improving code navigation. 

See http://www.stylecop.com/docs/Ordering%20Rules.html

### Sane

* [SA1203: ConstantsMustAppearBeforeFields](http://www.stylecop.com/docs/SA1203.html)

  Barely.

* [SA1206: DeclarationKeywordsMustFollowOrder](http://www.stylecop.com/docs/SA1206.html)

  Barely.

* [SA1207: ProtectedMustComeBeforeInternal](http://www.stylecop.com/docs/SA1207.html)

  This rule is so specific I suppose it practically never applies, but fine. It does no harm.

* [SA1208: SystemUsingDirectivesMustBePlacedBeforeOtherUsingDirectives](http://www.stylecop.com/docs/SA1208.html)

  Under serious doubt.

* [SA1209: UsingAliasDirectivesMustBePlacedAfterOtherUsingDirectives](http://www.stylecop.com/docs/SA1209.html)

  This makes things more readable.

* [SA1212: PropertyAccessorsMustFollowOrder](http://www.stylecop.com/docs/SA1212.html)

  I've never seen this rule violated, but fine.

* [SA1213: EventAccessorsMustFollowOrder](http://www.stylecop.com/docs/SA1213.html)

  This is fine too.

* [SA1214: StaticReadonlyElementsMustAppearBeforeStaticNonReadonlyElements](http://www.stylecop.com/docs/SA1214.html)

  Not sure it's terribly useful, but perhaps clean to distinguish between readonly and mutable.

* [SA1215: InstanceReadonlyElementsMustAppearBeforeInstanceNonReadonlyElements](http://www.stylecop.com/docs/SA1215.html)

  Not sure it's terribly useful, but perhaps clean to distinguish between readonly and mutable.


### Insane

* [SA1200: UsingDirectivesMustBePlacedWithinNamespace](http://www.stylecop.com/docs/SA1200.html)

  No!

* [SA1201: ElementsMustAppearInTheCorrectOrder](http://www.stylecop.com/docs/SA1201.html)

  No. I am not spending my time memorizing the exact sequence of code elements required to please StyleCop. 

* [SA1202: ElementsMustBeOrderedByAccess](http://www.stylecop.com/docs/SA1202.html)

  No. This is actually harmful, it is much better to group code elements cohesively with respect to functionality (i.e. place private helper functions next to the public functions they help).

* [SA1204: StaticElementsMustAppearBeforeInstanceElements](http://www.stylecop.com/docs/SA1204.html)

  No, I see no advantages gained by this rule that would offset the disadvantages: if I change from static to instance or the other way around I should have to manually move the code around? Insane.

* [SA1205: PartialElementsMustDeclareAccess](http://www.stylecop.com/docs/SA1205.html)

  Ha ha! The rationale is that "StyleCop may not be able to determine the correct placement of the elements in the file". In other words, this insane rule is a prerequisite for other insane rules?

* [SA1210: UsingDirectivesMustBeOrderedAlphabeticallyByNamespace](http://www.stylecop.com/docs/SA1210.html)

  This is quite common, but I find it pretty silly. Let ReSharper organize your using directives.

* [SA1211: UsingAliasDirectivesMustBeOrderedAlphabeticallyByAliasName](http://www.stylecop.com/docs/SA1211.html)

  This is also pretty silly.


## Readability Rules (SA1100-)

As always, StyleCop is mainly helpful when assisting in maintaining elementary code hygiene and consistency of formatting. As corrective-aggressive monkey (ref SA1122), StyleCop is annoying and outright damaging.

See http://www.stylecop.com/docs/Readability%20Rules.html

### Sane

* [SA1100: DoNotPrefixCallsWithBaseUnlessLocalImplementationExists](http://www.stylecop.com/docs/SA1100.html)

  I don't know if this is a problem warranting a rule but OK. 

* [SA1102: QueryClauseMustFollowPreviousClause](http://www.stylecop.com/docs/SA1102.html)

  Seems reasonable.

* [SA1103: QueryClausesMustBeOnSeparateLinesOrAllOnOneLine](http://www.stylecop.com/docs/SA1103.html)

  This rule is fine.

* [SA1104: QueryClauseMustBeginOnNewLineWhenPreviousClauseSpansMultipleLines](http://www.stylecop.com/docs/SA1104.html)

  This rule is fine.

* [SA1105: QueryClausesSpanningMultipleLinesMustBeginOnOwnLine](http://www.stylecop.com/docs/SA1105.html)

  This rule is fine.

* [SA1106: CodeMustNotContainEmptyStatements](http://www.stylecop.com/docs/SA1106.html)

  Hygiene.

* [SA1107: CodeMustNotContainMultipleStatementsOnOneLine](http://www.stylecop.com/docs/SA1107.html)

  I think enforcing this rule is always a good idea, even inside lambda expressions.

* [SA1108: BlockStatementsMustNotContainEmbeddedComments](http://www.stylecop.com/docs/SA1108.html)

  I have never seen anyone violate this rule, but it's a horrible practice.

* [SA1109: BlockStatementsMustNotContainEmbeddedRegions](http://www.stylecop.com/docs/SA1109.html)

  I have never seen anyone violate this rule, but it's a horrible practice.

* [SA1110: OpeningParenthesisMustBeOnDeclarationLine](http://www.stylecop.com/docs/SA1110.html)

  This rule is fine.

* [SA1111: ClosingParenthesisMustBeOnLineOfOpeningParenthesis](http://www.stylecop.com/docs/SA1111.html)

  This rule is fine.

* [SA1112: ClosingParenthesisMustBeOnLineOfOpeningParenthesis](http://www.stylecop.com/docs/SA1112.html)

  No controversy here.

* [SA1113: CommaMustBeOnSameLineAsPreviousParameter](http://www.stylecop.com/docs/SA1113.html)

  Hygiene.

* [SA1114: ParameterListMustFollowDeclaration](http://www.stylecop.com/docs/SA1114.html)

  Hygiene.

* [SA1115: ParameterMustFollowComma](http://www.stylecop.com/docs/SA1115.html)

  I think this rule is fine.

* [SA1116: SplitParametersMustStartOnLineAfterDeclaration](http://www.stylecop.com/docs/SA1116.html)

  I think this rule is fine.

* [SA1117: ParametersMustBeOnSameLineOrSeparateLines](http://www.stylecop.com/docs/SA1117.html)
 
  I think this rule is fine.

* [SA1118: ParameterMustNotSpanMultipleLines](http://www.stylecop.com/docs/SA1118.html)

  I think this rule is fine.

* [SA1120: CommentsMustContainText](http://www.stylecop.com/docs/SA1120.html)

  This rule is fine.

* [SA1123: DoNotPlaceRegionsWithinElements](http://www.stylecop.com/docs/SA1123.html)

  Using regions at all is a bad idea, and this is a horrible idea.

* [SA1124: DoNotUseRegions](http://www.stylecop.com/docs/SA1124.html)

  Just don't do it.

* [SA1125: UseShorthandForNullableTypes](http://www.stylecop.com/docs/SA1125.html)

  I can't think of any code samples where it makes sense to write `Nullable<Foo>` instead of `Foo?`.


### Insane

* [SA1101: PrefixLocalCallsWithThis](http://www.stylecop.com/docs/SA1101.html)

  No chance.

* [SA1121: UseBuiltInTypeAlias](http://www.stylecop.com/docs/SA1121.html)

  I'm inclined to think that it is better to use the real type names when referring to static methods defined by those types, e.g. `String.Compare("foo", "bar")` is better than `string.Compare("foo", "bar")`. 

* [SA1122: UseStringEmptyForEmptyStrings](http://www.stylecop.com/docs/SA1122.html)

  There is an established best practice in the .NET world that you are supposed to use `string.Empty` rather than `""`, but I think it's ridiculous. IMHO `""` is preferable, since it is both more concise and more readable. There is also some superstition out there that `string.Empty` is supposed to be more _performant_ than `""`, but that's pure hogwash. Since .NET 2.0, there has been no difference in performance between the two alternatives (and besides: talk about micro optimization!). Developers who let this myth dictate how they write code today should google "the monkey and the ladder". For a more thorough discussion, see http://stackoverflow.com/a/263257.

* [SA1126: PrefixCallsCorrectly](http://www.stylecop.com/docs/SA1126.html)

  WTF? No.


## Spacing Rules (SA1000-)

This is primarily about simple code hygiene. This is what StyleCop does best.

See http://www.stylecop.com/docs/Spacing%20Rules.html

### Sane

* [SA1000: KeywordsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1000.html)

  OK. Violations of this rule is just sloppy typing.

* [SA1001: CommasMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1001.html)

  OK. Violations of this rule is just sloppy typing.

* [SA1002: SemicolonsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1002.html)

  OK. Violations of this rule is just sloppy typing.

* [SA1003: SymbolsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1003.html)

  Can't think of any code samples where it is acceptable to violate this rule.

* [SA1004: DocumentationLinesMustBeginWithSingleSpace](http://www.stylecop.com/docs/SA1004.html)

  A bit of pedant rule, but probably makes the code a little tidier without causing problems.

* [SA1005: SingleLineCommentsMustBeginWithSingleSpace](http://www.stylecop.com/docs/SA1005.html)

  Even more of a pedant rule, but the practice of adding the one spacing can probably be interned by muscle memory, and I suppose it makes things a little tidier.

* [SA1006: PreprocessorKeywordsMustNotBePrecededBySpace](http://www.stylecop.com/docs/SA1006.html)

  This is the convention. I rarely see preprocessor keywords in the wild, so the rule rarely applies.

* [SA1007: OperatorKeywordMustBeFollowedBySpace](http://www.stylecop.com/docs/SA1007.html)

  This is neat and clean.

* [SA1008: OpeningParenthesisMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1008.html)

  With some doubts. I'm not sure if there might be code samples where it would be preferable to deviate from this rule.

* [SA1009: ClosingParenthesisMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1009.html)

  Ref SA1008.
  
* [SA1010: OpeningSquareBracketsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1010.html)

  Ref SA1008.
    
* [SA1011: ClosingSquareBracketsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1011.html)

  Ref SA1008.
  
* [SA1012: OpeningCurlyBracketsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1012.html)

  Ref SA1008.

* [SA1013: ClosingCurlyBracketsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1013.html)

  Ref SA1008.

* [SA1014: OpeningGenericBracketsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1014.html)

  I think adhering to this rule is problem-free.

* [SA1015: ClosingGenericBracketsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1015.html)

  Ref SA1014.

* [SA1016: OpeningAttributeBracketsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1016.html)

  I think adhering to this rule is problem-free.

* [SA1017: ClosingAttributeBracketsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1017.html)

  Ref SA1016.

* [SA1018: NullableTypeSymbolsMustNotBePrecededBySpace](http://www.stylecop.com/docs/SA1018.html)

  This is the convention.

* [SA1019: MemberAccessSymbolsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1019.html)

  No controversy here.

* [SA1020: IncrementDecrementSymbolsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1020.html)

  This is the convention.

* [SA1021: NegativeSignsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1021.html)

  I see no controversy here.

* [SA1022: PositiveSignsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1022.html)

  I see no controversy here.

* [SA1023: DereferenceAndAccessOfSymbolsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1023.html)

  I suppose this is the convention. Few practical implications, since the rule rarely applies.

* [SA1024: ColonsMustBeSpacedCorrectly](http://www.stylecop.com/docs/SA1024.html)

  This is the convention.

* [SA1025: CodeMustNotContainMultipleWhitespaceInARow](http://www.stylecop.com/docs/SA1025.html)

  No controversy here. Violations are due to sloppy typing.

* [SA1027: TabsMustNotBeUsed](http://www.stylecop.com/docs/SA1027.html)

  No controversy here.


### Insane

* [SA1026: CodeMustNotContainSpaceAfterNewKeywordInImplicitlyTypedArrayAllocation](http://www.stylecop.com/docs/SA1026.html)

  Calling this rule "insane" is a bit harsh, but I don't think I concur. I prefer a whitespace.

