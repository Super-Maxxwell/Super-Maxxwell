- 👋 Hi, I’m @Super-Maxxwell
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---XML
--->

public class buildXml {
	
	//Doc
	public static Document buildDocument( ) throws ParserConfigurationException {
		return DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument();
	}
	
	//Element
	public static Element createElement(Document doc,String elementname) {
		return doc.createElement(elementname);
	}
	//Attribute
	public static Attr createAttribute(Document doc,String type,String value ) {
		Attr attribute =doc.createAttribute(type);
		attribute.setValue(value);
		return attribute;
	}
	//Attributes for Element
	public static Element setAttributeForElement(Element element,Attr attribute) {
		element.setAttributeNode(attribute);
		return element;
	}
	public static Element setAttributeForElement1(Element element,Attr attribute) {
		element.setAttributeNode(attribute);
		return element;
	}
  
  
  

//Property XML

public class PropXml {

	private static final String NAME = "Kalindu";
	private static final String INSTITUTE = "SLIIT";
	private static final String MODULE = "MTIT";
	private static final String YEAR = "2022";
	private static final String COMMENT = "New file added";
	private static final String PROPERTY_FILENAME = "Property.xml";

	public static void createProperty() {
		try {
			Properties properties =new Properties();
			
			properties.setProperty("NAME", NAME);
			properties.setProperty("INSTITUTE", INSTITUTE);
			properties.setProperty("MODULE", MODULE);
			properties.setProperty("YEAR", YEAR);
			properties.storeToXML(new FileOutputStream(PROPERTY_FILENAME),COMMENT);
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}}
	public static void main(String[] args) {
		createProperty();
	}

}
  
  
  
	
	//Text nodes for elemnt
	public static Element appendTextNode(Document doc,Element element,String textnode) {
		element.appendChild(doc.createTextNode(textnode));
		return element;
	}
	//Transform
	public static void transformToXml(Document doc) throws TransformerFactoryConfigurationError, TransformerException {
		Transformer transformer= TransformerFactory.newInstance().newTransformer();
		DOMSource source = new DOMSource();
		transformer.transform(source, new StreamResult(new File("Students.xml")));
		
		transformer.transform(source, new StreamResult(System.out));
		
	}
	
	
	
	public static void main(String[] args) throws ParserConfigurationException, TransformerFactoryConfigurationError, TransformerException {
		// TODO Auto-generated method stub
		
		Document doc = buildDocument();

		Element Employee = setAttributeForElement(createElement(doc, "Employee"),
				createAttribute(doc, "Gender", "Male"));

		Employee.appendChild((Node) appendTextNode(doc,
				setAttributeForElement(createElement(doc, "Name"), createAttribute(doc, "Initials", "S.A.")),
				"Nalaka Dissanayake"));
		
		doc.appendChild(createElement(doc, "School")).appendChild(createElement(doc, "Students")).appendChild(Employee);
		transformToXml(doc);
	}

}



//XML
public class q2 {

	Document doc= DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument();
	
	//Create Root Elements and child elements
	Element rootElement= doc.createElement("School");
	doc.appendChild(rootElement);
	Element Students= doc.createElement("Students");
	rootElement.appendChild(Students);
	Element Student= doc.createElement("Student");
	Students.appendChild(Student);
	
	//Set attributes to element
	Attr attr= doc.createAttribute("gender");
	attr.setValue("male");
	Student.setAttributeNode(attr);
	
	//Name element
	Element Name= doc.createElement("Name");
	Attr attrType= doc.createAttribute("Initials");
	attrType.setValue("S.A");
	Name.setAttributeNode(attrType);
	Name.appendChild(doc.createTextNode("Nalaka Dissanayake")); 
	Student.appendChild(Name);
	
	//Address element
	Element Address= doc.createElement("Address");
	//1st Attribute
	Attr attrType1= doc.createAttribute("No");
	attrType1.setValue("115/1");
	Address.setAttributeNode(attrType);
	//2nd Attribute
	Attr attrType2= doc.createAttribute("Street");
	attrType2.setValue("Avenue Street");
	Address.setAttributeNode(attrType2);
	//Text node
	Address.appendChild(doc.createTextNode("115/1,Avenue Street,Kandy")); 
	Student.appendChild(Address);
	
	
	//Transform
	Transformer transformer = TransformerFactory.newInstance().newTransformer();
	DOMSource  domsource= new DOMSource(doc);
	transformer.transform(domsource, new StreamResult(new File("student.xml")));
	transformer.transform(domsource, new StreamResult(System.out));
	
	
	}

