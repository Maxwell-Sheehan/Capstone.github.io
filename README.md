# Capstone.github.io

  Throughout my computer science journey I have used multiple products, and softwares to demonstrate a range of ideas, and abilities that allow me to work with modern industry quality code and coding practices. The wide range of course work has given me many strengths and abilities I’m now able to leverage, of these skills certain mindsets have developed which apply to various projects outside of the artifacts highlighted here. Cyber security has grown to be increasingly important, with more media attention, as well as higher stakes then ever as more things go cloud based. The skills developed within these courses has enabled me to have a better critical lens of which I can evaluate cyber security incidents, and prevent them. This comes in the form of code reviews, as well as understanding how various systems interact to prevent potential attack surfaces. 
  
Computer science is about a lot of skills interacting with each other, to none technical users it can almost sound like speaking a foreign language. One of the most important skills you’ll see from my artifacts and code review is the ability to collaborate within a team, and communicate with stakeholders technical information in an easily digestible way. This is similar to how it works in a working organization, you’ll have to work with team members who may not be as technical, and break down crucial concepts to them in ways they can understand. This obviously applies to stakeholders as well, conveying the benefits and drawbacks of certain options, not a bunch of technical jargon that means nothing to them. We see this take place within the three artifacts I enhanced and display below, each of these artifacts touches upon core principles of computer science engrained through my courses. Data structures and algorithms has to do with the speed and efficiency of code, I’m able to take a less efficient artifact and bring it to industry standard of the highest efficiency attainable using better coding practices. I display data in a real measurable way with my software engineering and database artifact, instead of the initial purpose of just meeting course outcomes. Information is important, and should be easily read at a glance, we talked abot the important of conveying ideas earlier, and this is an extension of that. Good data, and good displayed data, should be understood to none technical users quickly so they can work off of it. Finally, talking about security, I take an artifact that is very unsecure, and bring it up to modern secure practices. While a security mindset is important to develop, the ability to utilize the skill like you would any craft is equally important, and is displayed below. 

In summary, all of these artifacts exist and demonstrated understanding I had prior to the new experience I’ve gained. Computer science is constantly involving, and for individuals that is equally true, we are constantly improving and picking up new skills on which we improve ourselves. Each of these artifacts are things I could clearly see multiple problems with, while being in a wide range of subject matters, and I was able to enhance now with my increased understanding and experience. 


If you would like to see an indepth code review, please follow this link to see me discuss the proposed changes, and inevitable revisions of each individual artifact.
    Placeholder

Enhancment One: Software Design and Engineering

  Looking at the first artifact we are refurbishing, we have an old java class that was designed to create and validate a contact being created for an application. The original artifact had some basic error handling, and general input validation. This was created almost a year ago, and I think it’s a good candidate for showcasing the expanded knowledge of what data should be editable, as well as how we can better secure data. For one, this artifact is relatively recent, so it showcases how overall sound code can be improved with more knowledge, and just better understanding of more modern secure coding principles. The artifact has improved by having more robust handling, it no longer is just a generic error but more targeted. All fields are also now final, so they can’t be modified after creation. We have improved data validation, we now trim to remove white space, and have more through validation within the name objects to only accept alphabetic chars, as well as apostrophes and hyphens. This is both more secure code, and more encapsulated maintainable code. It has improved error handling, while also validating data better, so that future development and troubleshooting can be more through.
  
I think this artifacts improvements meet the desired outcome, of the assessment ‘Develop a security mindset that anticipates adversarial exploits in software architecture and designs to expose potential vulnerabilities, mitigate design flaws, and ensure privacy and enhanced security of data and resources’ This both uses a security mindset to expand on an initial design, creates more scalable architecture. And patches potential vulnerabilities and design flaws, bad error handling is a design flaw, and the fact that white space as char was valid before is an error. While I was improving and working on this enhancement, I struggled a bit in trying to make this as secure as possible. So there was a lot of theory on what is acceptable for names, string is a very open ended type in programming, so setting up only alphabetic characters, and common name characters like hyphens took some research. It was certainly challenging to work through, all of the invalid outcomes, and expected outcomes manually, leetcode is nice as it has sturdy test cases. However solo testing edge cases, and fixing bad logic can be quite time consuming. 


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
	
Enhancement Two: Algorithms and Data Structure

This was the enhancement I was most looking forward too, I have spent a lot of effort recently doing leet code problems to enhance my data structure and algorithm skills. If you look at the activity on my github, most of my submissions come from a LeetCode Python repository. So for this reason, I was able to sort out this enhancement fairly quickly, as well as implement it. This artifact was actually for an embedded system using a raspberry pi, it was made with a lot of restrictions around the initial code, as I was told I can’t modify the skeleton code and could only change the specific functions listed. This project initially was more focused on just combining physical hardware to showcase embedded systems as a thermostat, however now about a year later, I can modify the code of what would be on the pi to be a lot more industry standardized. I think these reasons highlight why this is a great artifact to enhance, it is something I now have no restrictions on, and can focus more on software optimizations vs hardware pieces. For instance, when you look at the LCD display, we are now caching the previous display, and checking for if it is different. This will make the LCD display smoother, and reduce the overall processing requirement of the code as it’s now just listening for a different result instead of constantly cycling a new display. We also now use a dictionary for the LED State update, this is an 0(1) time complexity, which is just a better more efficient algorithm compared to the if/elif chain that was used before to update the LED’s that would blink. 
  
I think these changes, and the general approach I had to this artifact do a good job to meet the required course outcomes;
Design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution while managing the trade-offs involved in design choices.  

The new design of the file is both more efficient, and utilizes more normalized industry techniques to improve it’s overall function and user experience. The trade offs of something like this is normally the time and effort it would  take to refactor the class. Tech dept, is generally pretty revenue / time inefficient, as you take something that already works, and improve on it, but don’t create something new that generates value directly. This is a very real industry trade off, however it was not effecting the scope of these improvements. This did cause an update to the outcome coverage plan, and was promptly updated in the journal submission for this week. I always find rebuilding something to be a rewarding experience, it’s not quite reverse engineering, but making something a second time you’ve already worked on really opens the door to innovation. Combined with my enthusiasm for algorithms lately, I think I was well prepared for this weeks improvements. The biggest challenges were largely just not having the pi in working order anymore, as this removed some of the practical, physical trouble shooting I had initially visually seeing the LEDs update.

Artifact:

	# Revised Thermostat Code – All TODOs Completed to Meet Requirements
	# ---------------------------------------------------------------
	from time import sleep
	from datetime import datetime
	from statemachine import StateMachine, State
	import board
	import adafruit_ahtx0
	import digitalio
	import adafruit_character_lcd.character_lcd as characterlcd
	import serial
	from gpiozero import Button, PWMLED
	from threading import Thread
	from math import floor
	
	DEBUG = True
	
	# I2C + Sensor
	i2c = board.I2C()
	thSensor = adafruit_ahtx0.AHTx0(i2c)
	
	# UART
	ser = serial.Serial(
	    port='/dev/ttyS0',
	    baudrate=115200,
	    parity=serial.PARITY_NONE,
	    stopbits=serial.STOPBITS_ONE,
	    bytesize=serial.EIGHTBITS,
	    timeout=1
	)
	
	# LEDs
	redLight = PWMLED(18)
	blueLight = PWMLED(23)
	
	
	class ManagedDisplay():

    ## manages the 16x2 LED display using GPIO pins, handles cleaned up / initilization / update
    def __init__(self):
        self.lcd_rs = digitalio.DigitalInOut(board.D17)
        self.lcd_en = digitalio.DigitalInOut(board.D27)
        self.lcd_d4 = digitalio.DigitalInOut(board.D5)
        self.lcd_d5 = digitalio.DigitalInOut(board.D6)
        self.lcd_d6 = digitalio.DigitalInOut(board.D13)
        self.lcd_d7 = digitalio.DigitalInOut(board.D26)
        self.lcd_columns = 16
        self.lcd_rows = 2
        self.lcd = characterlcd.Character_LCD_Mono(
            self.lcd_rs, self.lcd_en,
            self.lcd_d4, self.lcd_d5,
            self.lcd_d6, self.lcd_d7,
            self.lcd_columns, self.lcd_rows
        )
        self.lcd.clear()

    def cleanupDisplay(self):
        #clear the dispplay and release GPIO Resources
        self.lcd.clear()
        self.lcd_rs.deinit()
        self.lcd_en.deinit()
        self.lcd_d4.deinit()
        self.lcd_d5.deinit()
        self.lcd_d6.deinit()
        self.lcd_d7.deinit()

    def updateScreen(self, line1, line2):
        #add text two the screen
        self.lcd.home()
        self.lcd.message = f"{line1[:16]:<16}\n{line2[:16]:<16}"


	screen = ManagedDisplay() #create LCD instacnce
	
	
	class TemperatureMachine(StateMachine):
	    #stat machine controlling off / heat / cool
	
	    #define states
	    off = State(initial=True)
	    heat = State()
	    cool = State()
	
	    #default setpoint value
	    setPoint = 72
	
	    cycle = off.to(heat) | heat.to(cool) | cool.to(off)
	
	    def on_enter_heat(self):
	        self.updateLights()
	        if DEBUG:
	            print('* Changing state to heat')
	
	    def on_exit_heat(self):
	        redLight.off()
	
	    def on_enter_cool(self):
	        self.updateLights()
	        if DEBUG:
	            print('* Changing state to cool')
	
	    def on_exit_cool(self):
	        blueLight.off()
	
	    def on_enter_off(self):
	        redLight.off()
	        blueLight.off()
	        if DEBUG:
	            print('* Changing state to off')
	
	    def processTempStateButton(self):
	        if DEBUG:
	            print('Cycling Temperature State')
	        self.cycle()
	        self.updateLights()
	
	    def processTempIncButton(self):
	        self.setPoint += 1
	        if DEBUG:
	            print(f'Increasing Set Point -> {self.setPoint}')
	        self.updateLights()
	
	    def processTempDecButton(self):
	        self.setPoint -= 1
	        if DEBUG:
	            print(f'Decreasing Set Point -> {self.setPoint}')
	        self.updateLights()
	
	    #updated LED behavior based on state and temp
	    def updateLights(self):
	        temp = floor(self.getFahrenheit())
	        redLight.off()
	        blueLight.off()
	
	        if self.current_state == self.heat:
	            if temp < self.setPoint:
	                redLight.pulse()
	            else:
	                redLight.on()
	
	        elif self.current_state == self.cool:
	            if temp > self.setPoint:
	                blueLight.pulse()
	            else:
	                blueLight.on()
	
	    def run(self):
	        Thread(target=self.manageMyDisplay).start()
	
	    def getFahrenheit(self):
	        return ((9 / 5) * thSensor.temperature) + 32
	
	    def setupSerialOutput(self):
	        state = self.current_state.id
	        temp = round(self.getFahrenheit(), 1)
	        output = f"{state},{temp},{self.setPoint}\n"
	        return output
	
	    endDisplay = False
	
	    def manageMyDisplay(self):
	        counter = 1
	        altCounter = 1
	        while not self.endDisplay:
	            now = datetime.now()
	            lcd_line_1 = now.strftime('%m/%d %H:%M') + '\n'
	
	            if altCounter < 6:
	                temp = round(self.getFahrenheit(), 1)
	                lcd_line_2 = f"Temp: {temp}F"
	                altCounter += 1
	            else:
	                lcd_line_2 = f"{self.current_state.id.upper()} {self.setPoint}F"
	                altCounter += 1
	                if altCounter >= 11:
	                    self.updateLights()
	                    altCounter = 1
	
	            screen.updateScreen(lcd_line_1, lcd_line_2)
	
	
	            if counter % 30 == 0:
	                ser.write(self.setupSerialOutput().encode())
	                counter = 1
	            else:
	                counter += 1
	
	            sleep(1)
	
	        screen.cleanupDisplay()
	
	
	# State machine
	tsm = TemperatureMachine()
	tsm.run()
	
	# Buttons
	greenButton = Button(24)
	greenButton.when_pressed = tsm.processTempStateButton
	
	redButton = Button(25)
	redButton.when_pressed = tsm.processTempIncButton
	
	blueButton = Button(12)
	blueButton.when_pressed = tsm.processTempDecButton
	
	
	repeat = True
	while repeat:
	    try:
	        sleep(30)
	    except KeyboardInterrupt:
	        print('Cleaning up. Exiting...')
	        repeat = False
	        tsm.endDisplay = True
	        sleep(1)
	

Enhancment

	from time import sleep
	from datetime import datetime
	from statemachine import StateMachine, State
	import board
	import adafruit_ahtx0
	import digitalio
	import adafruit_character_lcd.character_lcd as characterlcd
	import serial
	from gpiozero import Button, PWMLED
	from threading import Thread
	from math import floor
	
	DEBUG = True
	
	# -----------------------------
	# Hardware Setup
	# -----------------------------
	i2c = board.I2C()
	thSensor = adafruit_ahtx0.AHTx0(i2c)
	
	ser = serial.Serial(
	    port='/dev/ttyS0',
	    baudrate=115200,
	    parity=serial.PARITY_NONE,
	    stopbits=serial.STOPBITS_ONE,
	    bytesize=serial.EIGHTBITS,
	    timeout=1
	)
	
	redLight = PWMLED(18)
	blueLight = PWMLED(23)
	
	
	# -----------------------------
	# LCD Display Manager
	# -----------------------------
	class ManagedDisplay:
	
	    def __init__(self):
	        self.lcd_rs = digitalio.DigitalInOut(board.D17)
	        self.lcd_en = digitalio.DigitalInOut(board.D27)
	        self.lcd_d4 = digitalio.DigitalInOut(board.D5)
	        self.lcd_d5 = digitalio.DigitalInOut(board.D6)
	        self.lcd_d6 = digitalio.DigitalInOut(board.D13)
	        self.lcd_d7 = digitalio.DigitalInOut(board.D26)
	
	        self.lcd = characterlcd.Character_LCD_Mono(
	            self.lcd_rs,
	            self.lcd_en,
	            self.lcd_d4,
	            self.lcd_d5,
	            self.lcd_d6,
	            self.lcd_d7,
	            16,
	            2
	        )
	
	        self.lcd.clear()
	
	        # cache previous display output
	        self.prev_line1 = ""
	        self.prev_line2 = ""
	
	    def updateScreen(self, line1, line2):
	
	        # only update LCD if text changed
	        if line1 != self.prev_line1 or line2 != self.prev_line2:
	            self.lcd.home()
	            self.lcd.message = f"{line1[:16]:<16}\n{line2[:16]:<16}"
	
	            self.prev_line1 = line1
	            self.prev_line2 = line2
	
	    def cleanupDisplay(self):
	        self.lcd.clear()
	
	        self.lcd_rs.deinit()
	        self.lcd_en.deinit()
	        self.lcd_d4.deinit()
	        self.lcd_d5.deinit()
	        self.lcd_d6.deinit()
	        self.lcd_d7.deinit()
	
	
	screen = ManagedDisplay()
	
	
	# -----------------------------
	# Thermostat State Machine
	# -----------------------------
	class TemperatureMachine(StateMachine):
	
	    off = State(initial=True)
	    heat = State()
	    cool = State()
	
	    setPoint = 72
	
	    cycle = off.to(heat) | heat.to(cool) | cool.to(off)
	
	    endDisplay = False
	
	    def __init__(self):
	        super().__init__()
	
	        # cached temp value
	        self.currentTemp = 0
	
	        # dictionary state lookup (O(1))
	        self.stateHandlers = {
	            "heat": self.handleHeat,
	            "cool": self.handleCool,
	            "off": self.handleOff
	        }
	
	    # -----------------------------
	    # Temperature Reading
	    # -----------------------------
	    def updateTemperature(self):
	        self.currentTemp = ((9 / 5) * thSensor.temperature) + 32
	
	    # -----------------------------
	    # State Handlers
	    # -----------------------------
	    def handleHeat(self):
	
	        redLight.off()
	        blueLight.off()
	
	        if self.currentTemp < self.setPoint:
	            redLight.pulse()
	        else:
	            redLight.on()
	
	    def handleCool(self):
	
	        redLight.off()
	        blueLight.off()
	
	        if self.currentTemp > self.setPoint:
	            blueLight.pulse()
	        else:
	            blueLight.on()
	
	    def handleOff(self):
	        redLight.off()
	        blueLight.off()
	
	    # -----------------------------
	    # LED State Update
	    # -----------------------------
	    def updateLights(self):
	
	        # dictionary lookup instead of if/elif chain
	        handler = self.stateHandlers[self.current_state.id]
	        handler()
	
	    # -----------------------------
	    # State Transitions
	    # -----------------------------
	    def on_enter_heat(self):
	        self.updateLights()
	
	        if DEBUG:
	            print("* Changed state to HEAT")
	
	    def on_enter_cool(self):
	        self.updateLights()
	
	        if DEBUG:
	            print("* Changed state to COOL")
	
	    def on_enter_off(self):
	        self.updateLights()
	
	        if DEBUG:
	            print("* Changed state to OFF")
	
	    # -----------------------------
	    # Button Actions
	    # -----------------------------
	    def processTempStateButton(self):
	
	        self.cycle()
	        self.updateLights()
	
	        if DEBUG:
	            print("Cycling thermostat mode")
	
	    def processTempIncButton(self):
	
	        self.setPoint += 1
	        self.updateLights()
	
	        if DEBUG:
	            print(f"Setpoint increased -> {self.setPoint}")
	
	    def processTempDecButton(self):
	
	        self.setPoint -= 1
	        self.updateLights()
	
	        if DEBUG:
	            print(f"Setpoint decreased -> {self.setPoint}")
	
	    # -----------------------------
	    # Serial Output
	    # -----------------------------
	    def setupSerialOutput(self):
	
	        state = self.current_state.id
	        temp = round(self.currentTemp, 1)
	
	        return f"{state},{temp},{self.setPoint}\n"
	
	    # -----------------------------
	    # Main Display Thread
	    # -----------------------------
	    def manageMyDisplay(self):
	
	        counter = 0
	        altCounter = 0
	
	        while not self.endDisplay:
	
	            # ONE sensor read per loop
	            self.updateTemperature()
	
	            now = datetime.now()
	
	            line1 = now.strftime("%m/%d %H:%M")
	
	            # alternate display content
	            if altCounter < 5:
	                line2 = f"Temp: {round(self.currentTemp,1)}F"
	            else:
	                line2 = f"{self.current_state.id.upper()} {self.setPoint}F"
	
	            altCounter += 1
	
	            if altCounter >= 10:
	                altCounter = 0
	
	            # only updates LCD if changed
	            screen.updateScreen(line1, line2)
	
	            # serial output every 30 seconds
	            counter += 1
	
	            if counter >= 30:
	                ser.write(self.setupSerialOutput().encode())
	                counter = 0
	
	            sleep(1)
	
	        screen.cleanupDisplay()
	
	    # -----------------------------
	    # Start Background Thread
	    # -----------------------------
	    def run(self):
	        Thread(target=self.manageMyDisplay).start()
	
	
	# -----------------------------
	# Start Thermostat
	# -----------------------------
	tsm = TemperatureMachine()
	tsm.run()
	
	# -----------------------------
	# Button Setup
	# -----------------------------
	greenButton = Button(24)
	greenButton.when_pressed = tsm.processTempStateButton
	
	redButton = Button(25)
	redButton.when_pressed = tsm.processTempIncButton
	
	blueButton = Button(12)
	blueButton.when_pressed = tsm.processTempDecButton
	
	
	# -----------------------------
	# Main Program Loop
	# -----------------------------
	running = True
	
	while running:
	
	    try:
	        sleep(30)
	
	    except KeyboardInterrupt:
	
	        print("Cleaning up and exiting...")
	
	        running = False
	        tsm.endDisplay = True
	
	        sleep(1)


Enhancement Three: Enhancement Three: Databases

Looking at the purpose of this artifacts initial creation, we have an artifact that was intended to just demonstrate basic CRUD function within a database. The only expectation at the initial time of it’s creation was the basic functions of a database, as well as one form of visualization within the data. Now we include this within the ePortfolio as something that feels more like an industry standard piece of software with a clear intention behind it’s data. The software has been improved to show key KPI’s, has evolved to show better more informative graphs, moving away from just a pie chart. And the functions of the map and pinning animals has changed, now instead of only being able to select one dog, or piece of data at a time, you can select multiple and have them post on the map. This will be a useful piece of software for real databases that want to visualize their information, so that they could more easily find trends and clusters within the data sets. 

I would say these changes align with the following course outcome; Demonstrate an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals. The software uses modern innovative techniques to properly display data, as you would expect a business piece of software would. And the value that the theoretical animal rescue facility could gain from the improved database visualization is apparent. I definitely faced the most challenges surrounding these artifacts as the initial artifact existed is codio, and the database was initially hosted only in codio. This made testing the enhancements rather challenging as I was effectively locked out of the artifacts initial data set. The ability to creat mock data, and test the enhancements seemed the simplest solution, and enabled me to be confident in the solutions proposed. 


Artifact:

	from jupyter_dash import JupyterDash
	from dash import dcc, html, dash_table
	from dash.dependencies import Input, Output
	import dash_leaflet as dl
	import plotly.express as px
	import pandas as pd
	import base64
	from CRUD_Python_Module import AnimalShelter
	import os
	
	# -------------------------------
	# Configure JupyterDash for Codio
	# -------------------------------
	JupyterDash.infer_jupyter_proxy_config()
	
	# -------------------------------
	# Build App Layout
	# -------------------------------
	app = JupyterDash(__name__)
	
	# -------------------------------
	# Database Connection
	# -------------------------------
	username = 'aacuser' 
	password = 'password123' 
	db = AnimalShelter(username, password)
	
	# Read all data initially
	df = pd.DataFrame.from_records(db.read({}))
	if '_id' in df.columns:
	    df.drop(columns=['_id'], inplace=True)
	
	# -------------------------------
	# Load and encode logo image
	# -------------------------------
	
	image_filename = "code_files/Grazioso Salvare Logo.png"
	if os.path.exists(image_filename):
	    encoded_image = base64.b64encode(open(image_filename, 'rb').read())
	    logo_component = html.Img(
	        src='data:image/png;base64,{}'.format(encoded_image.decode()),
	        style={'height': '100px'}
	    )
	else:
	    logo_component = html.Div(
	        "Logo not found. Place the logo in code_files folder.",
	        style={'color': 'red', 'fontWeight':'bold'}
	    )
	
	# -------------------------------
	# Build App Layout
	# -------------------------------
	app = JupyterDash(__name__)
	
	app.layout = html.Div([
	    html.Center([
	        logo_component,
	        html.H1('Grazioso Salvare Dashboard - Max Sheehan')
	    ]),
	    html.Hr(),
	
	    # Filter buttons
	    html.Div([
	        dcc.RadioItems(
	            id='filter-type',
	            options=[
	                {'label': 'Water Rescue', 'value': 'water'},
	                {'label': 'Mountain or Wilderness Rescue', 'value': 'mountain'},
	                {'label': 'Disaster or Individual Tracking', 'value': 'disaster'},
	                {'label': 'Reset', 'value': 'reset'}
	            ],
	            value='reset',
	            inline=True
	        )
	    ]),
	    html.Hr(),
	
	    # Data Table
	    dash_table.DataTable(
	        id='datatable-id',
	        columns=[{"name": i, "id": i} for i in df.columns],
	        data=df.to_dict('records'),
	        page_size=12,
	        filter_action='native',
	        sort_action='native',
	        row_selectable='single',
	        selected_rows=[0],
	        style_table={'overflowX': 'auto', 'maxHeight': '500px'}
	    ),
	    html.Br(),
	    html.Hr(),
	
	    # Graph + Map display
	    html.Div(className='row', style={'display': 'flex'}, children=[
	        html.Div(id='graph-id', className='col s12 m6'),
	        html.Div(id='map-id', className='col s12 m6')
	    ])
	])
	
	# -------------------------------
	# Filter Callback
	# -------------------------------
	@app.callback(
	    Output('datatable-id', 'data'),
	    [Input('filter-type', 'value')]
	)
	def update_dashboard(filter_type):
	    if filter_type == 'water':
	        data = db.read({
	            "animal_type": "Dog",
	            "breed": {"$in": ["Labrador Retriever Mix", "Chesapeake Bay Retriever", "Newfoundland"]}
	        })
	    elif filter_type == 'mountain':
	        data = db.read({
	            "animal_type": "Dog",
	            "breed": {"$in": ["German Shepherd", "Alaskan Malamute", "Old English Sheepdog", "Siberian Husky", "Rottweiler"]}
	        })
	    elif filter_type == 'disaster':
	        data = db.read({
	            "animal_type": "Dog",
	            "breed": {"$in": ["Doberman Pinscher", "German Shepherd", "Golden Retriever", "Bloodhound", "Rottweiler"]}
	        })
	    else:
	        data = db.read({})
	
	    df = pd.DataFrame.from_records(data)
	    if '_id' in df.columns:
	        df.drop(columns=['_id'], inplace=True)
	    return df.to_dict('records')
	
	# -------------------------------
	# Map Callback
	# -------------------------------
	@app.callback(
	    Output('map-id', 'children'),
	    [Input('datatable-id', 'derived_virtual_data'),
	     Input('datatable-id', 'derived_virtual_selected_rows')]
	)
	def update_map(viewData, selectedRows):
	    if not viewData or not selectedRows:
	        return [dl.Map(style={'width': '100%', 'height': '500px'}, center=[30.27, -97.74], zoom=10, children=[dl.TileLayer()])]
	
	    dff = pd.DataFrame.from_dict(viewData)
	    if dff.empty:
	        return [dl.Map(style={'width': '100%', 'height': '500px'}, center=[30.27, -97.74], zoom=10, children=[dl.TileLayer()])]
	
	    selected_row = selectedRows[0]
	    selected_animal = dff.iloc[selected_row]
	
	    lat = selected_animal.get("location_lat", 30.27)
	    lon = selected_animal.get("location_long", -97.74)
	
	    return [
	        dl.Map(style={'width': '100%', 'height': '500px'}, center=[lat, lon], zoom=10, children=[
	            dl.TileLayer(),
	            dl.Marker(position=[lat, lon], children=[
	                dl.Tooltip(selected_animal.get("name", "Unknown")),
	                dl.Popup([
	                    html.H4(selected_animal.get("name", "Unknown")),
	                    html.P(f"Breed: {selected_animal.get('breed', 'Unknown')}"),
	                    html.P(f"Type: {selected_animal.get('animal_type', 'Unknown')}"),
	                    html.P(f"Age: {selected_animal.get('age_upon_outcome', 'Unknown')}"),
	                ])
	            ])
	        ])
	    ]
	
	# -------------------------------
	# Graph Callback
	# -------------------------------
	@app.callback(
	    Output('graph-id', 'children'),
	    [Input('datatable-id', 'derived_virtual_data')]
	)
	def update_graphs(viewData):
	    dff = pd.DataFrame.from_dict(viewData)
	    if dff.empty or 'breed' not in dff.columns:
	        return html.Div("No data to display.")
	    fig = px.pie(dff, names='breed', title='Animal Breed Distribution')
	    return [dcc.Graph(figure=fig)]
	
	# -------------------------------
	# Run App
	# -------------------------------
	app.run_server()


Enhancment

	from jupyter_dash import JupyterDash
	from dash import dcc, html, dash_table
	from dash.dependencies import Input, Output
	import dash_leaflet as dl
	import plotly.express as px
	import pandas as pd
	import base64
	from CRUD_Python_Module import AnimalShelter
	import os
	
	# -------------------------------
	# Configure JupyterDash for Codio
	# -------------------------------
	JupyterDash.infer_jupyter_proxy_config()
	
	# -------------------------------
	# Build App Layout
	# -------------------------------
	app = JupyterDash(__name__)
	
	# -------------------------------
	# Database Connection
	# -------------------------------
	username = 'aacuser' 
	password = 'password123' 
	db = AnimalShelter(username, password)
	
	# Read all data initially
	df = pd.DataFrame.from_records(db.read({}))
	if '_id' in df.columns:
	    df.drop(columns=['_id'], inplace=True)
	
	# -------------------------------
	# Load and encode logo image
	# -------------------------------
	
	image_filename = "code_files/Grazioso Salvare Logo.png"
	if os.path.exists(image_filename):
	    encoded_image = base64.b64encode(open(image_filename, 'rb').read())
	    logo_component = html.Img(
	        src='data:image/png;base64,{}'.format(encoded_image.decode()),
	        style={'height': '100px'}
	    )
	else:
	    logo_component = html.Div(
	        "Logo not found. Place the logo in code_files folder.",
	        style={'color': 'red', 'fontWeight':'bold'}
	    )
	
	# -------------------------------
	# Build App Layout
	# -------------------------------
	app = JupyterDash(__name__)
	
	app.layout = html.Div([
	    html.Center([
	        logo_component,
	        html.H1('Grazioso Salvare Dashboard - Max Sheehan')
	    ]),
	    html.Hr(),
	
	    # Filter buttons
	    html.Div([
	        dcc.RadioItems(
	            id='filter-type',
	            options=[
	                {'label': 'Water Rescue', 'value': 'water'},
	                {'label': 'Mountain or Wilderness Rescue', 'value': 'mountain'},
	                {'label': 'Disaster or Individual Tracking', 'value': 'disaster'},
	                {'label': 'Reset', 'value': 'reset'}
	            ],
	            value='reset',
	            inline=True
	        )
	    ]),
	    html.Hr(),
	
	    # KPI Summary Cards
	    html.Div(
	        id='summary-cards',
	        style={
	            'display': 'flex',
	            'justifyContent': 'space-around',
	            'marginBottom': '20px',
	            'padding': '15px',
	            'backgroundColor': '#f5f5f5',
	            'borderRadius': '5px'
	        }
	    ),
	
	
	
	    # Data Table
	    dash_table.DataTable(
	        id='datatable-id',
	        columns=[{"name": i, "id": i} for i in df.columns],
	        data=df.to_dict('records'),
	        page_size=12,
	        filter_action='native',
	        sort_action='native',
	        row_selectable='single',
	        selected_rows=[0],
	
	        style_table={ # added better visualizations elemnts to display data
	        'overflowX': 'auto',
	        'height': '500px',
	        'overflowY': 'auto'
	    },
	    style_header={
	        'fontWeight': 'bold'
	    },
	    style_cell={
	        'textAlign': 'left',
	        'padding': '8px'
	    }
	    ),
	    html.Br(),
	    html.Hr(),
	
	    # Graph + Map display
	    html.Div(className='row', style={'display': 'flex'}, children=[
	        html.Div(id='graph-id', className='col s12 m6'),
	        html.Div(id='map-id', className='col s12 m6')
	    ])
	])
	
	# -------------------------------
	# Filter Callback
	# -------------------------------
	@app.callback(
	    Output('datatable-id', 'data'),
	    [Input('filter-type', 'value')]
	)
	def update_dashboard(filter_type):
	    if filter_type == 'water':
	        data = db.read({
	            "animal_type": "Dog",
	            "breed": {"$in": ["Labrador Retriever Mix", "Chesapeake Bay Retriever", "Newfoundland"]}
	        })
	    elif filter_type == 'mountain':
	        data = db.read({
	            "animal_type": "Dog",
	            "breed": {"$in": ["German Shepherd", "Alaskan Malamute", "Old English Sheepdog", "Siberian Husky", "Rottweiler"]}
	        })
	    elif filter_type == 'disaster':
	        data = db.read({
	            "animal_type": "Dog",
	            "breed": {"$in": ["Doberman Pinscher", "German Shepherd", "Golden Retriever", "Bloodhound", "Rottweiler"]}
	        })
	    else:
	        data = db.read({})
	
	    df = pd.DataFrame.from_records(data)
	    if '_id' in df.columns:
	        df.drop(columns=['_id'], inplace=True)
	    return df.to_dict('records')
	
	
	# -------------------------------
	# KPI Summary Cards Callback // This addition adds the ability to see important metrics like totla animals, unique breeds etc, that allows reacts to filtering
	# -------------------------------
	@app.callback(
	    Output('summary-cards', 'children'),
	    [Input('datatable-id', 'derived_virtual_data')]
	)
	def update_summary(viewData):
	
	    if not viewData:
	        return []
	
	    dff = pd.DataFrame(viewData)
	
	    if dff.empty:
	        return []
	
	    total_animals = len(dff)
	
	    unique_breeds = (
	        dff['breed'].nunique()
	        if 'breed' in dff.columns
	        else 0
	    )
	
	    animal_types = (
	        dff['animal_type'].nunique()
	        if 'animal_type' in dff.columns
	        else 0
	    )
	
	    return [
	
	        html.Div([
	            html.H2(total_animals),
	            html.P("Total Animals")
	        ], style={
	            'textAlign': 'center',
	            'padding': '10px'
	        }),
	
	        html.Div([
	            html.H2(unique_breeds),
	            html.P("Unique Breeds")
	        ], style={
	            'textAlign': 'center',
	            'padding': '10px'
	        }),
	
	        html.Div([
	            html.H2(animal_types),
	            html.P("Animal Types")
	        ], style={
	            'textAlign': 'center',
	            'padding': '10px'
	        })
	
	    ]
	
	# -------------------------------
	# Map Callback // Improved map logic to allow multiple animals to be selected, this way can see and visualize clusters and concentrations of data visually on map
	# -------------------------------
	@app.callback(
	    Output('map-id', 'children'),
	    [Input('datatable-id', 'derived_virtual_data')]
	)
	def update_map(viewData):
	
	    if not viewData:
	        return dl.Map(
	            center=[30.27, -97.74],
	            zoom=10,
	            style={'width': '100%', 'height': '500px'},
	            children=[dl.TileLayer()]
	        )
	
	    dff = pd.DataFrame(viewData)
	
	    if dff.empty:
	        return dl.Map(
	            center=[30.27, -97.74],
	            zoom=10,
	            style={'width': '100%', 'height': '500px'},
	            children=[dl.TileLayer()]
	        )
	
	    markers = []
	
	    for _, row in dff.iterrows():
	
	        try:
	
	            lat = float(row['location_lat'])
	            lon = float(row['location_long'])
	
	            markers.append(
	                dl.Marker(
	                    position=[lat, lon],
	                    children=[
	                        dl.Tooltip(
	                            row.get('name', 'Unknown')
	                        )
	                    ]
	                )
	            )
	
	        except:
	            continue
	
	    return dl.Map(
	        center=[30.27, -97.74],
	        zoom=10,
	        style={'width': '100%', 'height': '500px'},
	        children=[
	            dl.TileLayer(),
	            *markers
	        ]
	    )
	
	# -------------------------------
	# Graph Callback // Now this is a bar graph that shows the top 10 breeds
	# ------------------------------- 
	@app.callback(
	    Output('graph-id', 'children'),
	    [Input('datatable-id', 'derived_virtual_data')]
	)
	def update_graphs(viewData):
	
	    if not viewData:
	        return html.Div("No data available.")
	
	    dff = pd.DataFrame(viewData)
	
	    if dff.empty:
	        return html.Div("No data available.")
	
	    graphs = []
	
	    # Top 10 Breeds
	    if 'breed' in dff.columns:
	
	        breed_counts = (
	            dff['breed']
	            .fillna('Unknown')
	            .value_counts()
	            .head(10)
	            .reset_index()
	        )
	
	        breed_counts.columns = ['Breed', 'Count']
	
	        breed_fig = px.bar(
	            breed_counts,
	            x='Breed',
	            y='Count',
	            title='Top 10 Animal Breeds'
	        )
	
	        graphs.append(
	            dcc.Graph(figure=breed_fig)
	        )
	
	    # Animal Type Distribution
	    if 'animal_type' in dff.columns:
	
	        type_fig = px.pie(
	            dff,
	            names='animal_type',
	            title='Animal Type Distribution'
	        )
	
	        graphs.append(
	            dcc.Graph(figure=type_fig)
	        )
	
	    return html.Div(graphs)
	
	# -------------------------------
	# Run App
	# -------------------------------
	app.run_server()
