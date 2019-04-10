Is it possible to generate a collection binding for an element with `maxOccurs="1"`?

Here is a schema excerpt resembling some real use case:
```
<xs:sequence>
	<xs:element name="sectionA" type="xs:string" minOccurs="1" maxOccurs="1" />
	<xs:element name="sectionB" type="xs:string" minOccurs="2" maxOccurs="2" />
	<xs:element name="sectionC" type="xs:string" minOccurs="3" maxOccurs="3" />
</xs:sequence>
```


What is being generated:
```
@XmlElement(required = true)
protected String sectionA;
@XmlElement(required = true)
protected List<String> sectionB;
@XmlElement(required = true)
protected List<String> sectionC;
```

What I would like to see:
```
@XmlElement(required = true)
protected List<String> sectionA;
@XmlElement(required = true)
protected List<String> sectionB;
@XmlElement(required = true)
protected List<String> sectionC;
```

I know and understand that the default mapping for an element `element` of type `Element` having `maxOccurs="1"` is just `Element element`. Nevertheless I would like to be able to force collection binding because of consistency and aesthetic reasons (the real use case is slightly more complicated and involves some recursive data structures).

I tried several customizations with .xjb, nothing works.

Here's how one could request such customization using already existing options:
```
<jaxb:bindings node="//xs:element[@name='sectionA']">
	<jaxb:property collectionType="java.util.ArrayList" />
</jaxb:bindings>
```
