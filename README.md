# Capstone.github.io

  Throughout my computer science journey I have used multiple products, and softwares to demonstrate a range of ideas, and abilities that allow me to work with modern industry quality code and coding practices. The wide range of course work has given me many strengths and abilities I’m now able to leverage, of these skills certain mindsets have developed which apply to various projects outside of the artifacts highlighted here. Cyber security has grown to be increasingly important, with more media attention, as well as higher stakes then ever as more things go cloud based. The skills developed within these courses has enabled me to have a better critical lens of which I can evaluate cyber security incidents, and prevent them. This comes in the form of code reviews, as well as understanding how various systems interact to prevent potential attack surfaces. 
  
Computer science is about a lot of skills interacting with each other, to none technical users it can almost sound like speaking a foreign language. One of the most important skills you’ll see from my artifacts and code review is the ability to collaborate within a team, and communicate with stakeholders technical information in an easily digestible way. This is similar to how it works in a working organization, you’ll have to work with team members who may not be as technical, and break down crucial concepts to them in ways they can understand. This obviously applies to stakeholders as well, conveying the benefits and drawbacks of certain options, not a bunch of technical jargon that means nothing to them. We see this take place within the three artifacts I enhanced and display below, each of these artifacts touches upon core principles of computer science engrained through my courses. Data structures and algorithms has to do with the speed and efficiency of code, I’m able to take a less efficient artifact and bring it to industry standard of the highest efficiency attainable using better coding practices. I display data in a real measurable way with my software engineering and database artifact, instead of the initial purpose of just meeting course outcomes. Information is important, and should be easily read at a glance, we talked abot the important of conveying ideas earlier, and this is an extension of that. Good data, and good displayed data, should be understood to none technical users quickly so they can work off of it. Finally, talking about security, I take an artifact that is very unsecure, and bring it up to modern secure practices. While a security mindset is important to develop, the ability to utilize the skill like you would any craft is equally important, and is displayed below. 

In summary, all of these artifacts exist and demonstrated understanding I had prior to the new experience I’ve gained. Computer science is constantly involving, and for individuals that is equally true, we are constantly improving and picking up new skills on which we improve ourselves. Each of these artifacts are things I could clearly see multiple problems with, while being in a wide range of subject matters, and I was able to enhance now with my increased understanding and experience. 


If you would like to see an indepth code review, please follow this link to see me discuss the proposed changes, and inevitable revisions of each individual artifact.
    Placeholder

Enhancment One: Software Design and Engineering
#
    Throughout my computer science journey I have used multiple products, and softwares to demonstrate a range of ideas, and abilities that allow me to work with modern industry quality code and coding practices. The wide range of course work has given me many strengths and abilities I’m now able to leverage, of these skills certain mindsets have developed which apply to various projects outside of the artifacts highlighted here. Cyber security has grown to be increasingly important, with more media attention, as well as higher stakes then ever as more things go cloud based. The skills developed within these courses has enabled me to have a better critical lens of which I can evaluate cyber security incidents, and prevent them. This comes in the form of code reviews, as well as understanding how various systems interact to prevent potential attack surfaces. 
	Computer science is about a lot of skills interacting with each other, to none technical users it can almost sound like speaking a foreign language. One of the most important skills you’ll see from my artifacts and code review is the ability to collaborate within a team, and communicate with stakeholders technical information in an easily digestible way. This is similar to how it works in a working organization, you’ll have to work with team members who may not be as technical, and break down crucial concepts to them in ways they can understand. This obviously applies to stakeholders as well, conveying the benefits and drawbacks of certain options, not a bunch of technical jargon that means nothing to them. We see this take place within the three artifacts I enhanced and display below, each of these artifacts touches upon core principles of computer science engrained through my courses. Data structures and algorithms has to do with the speed and efficiency of code, I’m able to take a less efficient artifact and bring it to industry standard of the highest efficiency attainable using better coding practices. I display data in a real measurable way with my software engineering and database artifact, instead of the initial purpose of just meeting course outcomes. Information is important, and should be easily read at a glance, we talked abot the important of conveying ideas earlier, and this is an extension of that. Good data, and good displayed data, should be understood to none technical users quickly so they can work off of it. Finally, talking about security, I take an artifact that is very unsecure, and bring it up to modern secure practices. While a security mindset is important to develop, the ability to utilize the skill like you would any craft is equally important, and is displayed below. 
	In summary, all of these artifacts exist and demonstrated understanding I had prior to the new experience I’ve gained. Computer science is constantly involving, and for individuals that is equally true, we are constantly improving and picking up new skills on which we improve ourselves. Each of these artifacts are things I could clearly see multiple problems with, while being in a wide range of subject matters, and I was able to enhance now with my increased understanding and experience. 

Artifact:

    
    public class Contact {
    private final String contactId; // this is unqiue and can't be updated
    private String firstName;
    private String lastName;
    private String phone;
    private String address;


    //Constructor that creates a contact object, checks inputs for requirements
    public Contact(String contactId, String firstName, String lastName, String phone, String address) {
        if (contactId == null || contactId.length() > 10) //can't be empty or longer then 10 char
            throw new IllegalArgumentException("Invalid contact ID");
        if (firstName == null || firstName.length() > 10)
            throw new IllegalArgumentException("Invalid fisrt name");
        if (lastName == null || lastName.length() > 10)
            throw new IllegalArgumentException("Invalid last name");
        if (phone == null || !phone.matches("\\d{10}")) //phone num must be 10 digits
            throw new IllegalArgumentException("Invalid phone #");
        if (address == null || address.length() > 30) 
            throw new IllegalArgumentException("Invalid address, too long");

        //sets fields for object
        this.contactId = contactId;
        this.firstName = firstName;
        this.lastName = lastName;
        this.phone = phone;
        this.address = address;    
    }
    //Getters
    public String getContactId() { return contactId; }
    public String getFirstName() { return firstName; }
    public String getLastName() { return lastName; }
    public String getPhone() { return phone; }
    public String getAddress() { return address; }

    //Setting with validation
    public void setFirstName(String firstName) {
        if (firstName == null || firstName.length() > 10)
            throw new IllegalArgumentException("Invalid first name");
        this.firstName = firstName;
    }

    public void setLastName(String lastName) {
        if (lastName == null || lastName.length() > 10)
            throw new IllegalArgumentException("Invalid last name");
        this.lastName = lastName;
    }

    public void setPhone(String phone) {
        if (phone == null || !phone.matches("\\d{10}"))
            throw new IllegalArgumentException("Invalid phone");
        this.phone = phone;
    }

    public void setAddress(String address) {
        if (address == null || address.length() > 30)
            throw new IllegalArgumentException("invalid address");
        this.address = address; 
      }

    }

Enhancment:
  
    public final class Contact {

    // Validation constants
    private static final int MAX_ID_LENGTH = 10;
    private static final int MAX_NAME_LENGTH = 10;
    private static final int PHONE_LENGTH = 10;
    private static final int MAX_ADDRESS_LENGTH = 30;

    // Immutable fields
    private final String contactId;
    private final String firstName;
    private final String lastName;
    private final String phone;
    private final String address;

    // Constructor
    public Contact(String contactId,
                   String firstName,
                   String lastName,
                   String phone,
                   String address) {

        this.contactId = validateId(contactId);
        this.firstName = validateName(firstName, "First name");
        this.lastName = validateName(lastName, "Last name");
        this.phone = validatePhone(phone);
        this.address = validateAddress(address);
    }

    // ID validation
    private String validateId(String id) {
        if (id == null)
            throw new IllegalArgumentException("Contact ID cannot be null");

        id = id.trim();

        if (id.isEmpty() || id.length() > MAX_ID_LENGTH)
            throw new IllegalArgumentException("Invalid contact ID");

        return id;
    }

    // Name validation
    private String validateName(String name, String fieldName) {
        if (name == null)
            throw new IllegalArgumentException(fieldName + " cannot be null");

        name = name.trim();

        if (name.isEmpty() || name.length() > MAX_NAME_LENGTH)
            throw new IllegalArgumentException("Invalid " + fieldName);

        // Allows letters, apostrophes, and hyphens
        if (!name.matches("[A-Za-z'-]+"))
            throw new IllegalArgumentException(fieldName + " contains invalid characters");

        return name;
    }

    // Phone validation
    private String validatePhone(String phone) {
        if (phone == null)
            throw new IllegalArgumentException("Phone number cannot be null");

        phone = phone.trim();

        if (!phone.matches("\\d{" + PHONE_LENGTH + "}"))
            throw new IllegalArgumentException("Phone number must be exactly 10 digits");

        return phone;
    }

    // Address validation
    private String validateAddress(String address) {
        if (address == null)
            throw new IllegalArgumentException("Address cannot be null");

        address = address.trim();

        if (address.isEmpty() || address.length() > MAX_ADDRESS_LENGTH)
            throw new IllegalArgumentException("Invalid address");

        return address;
    }

    // Getters
    public String getContactId() {
        return contactId;
    }

    public String getFirstName() {
        return firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public String getPhone() {
        return phone;
    }

    public String getAddress() {
        return address;
    }
}

