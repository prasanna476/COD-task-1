# COD-task-1// Push Button Counter with Debouncing

const int buttonPin = 2;   // Push button pin
int buttonState = 0;       
int lastButtonState = 0;   
unsigned long lastDebounceTime = 0;
unsigned long debounceDelay = 50;  
int counter = 0;

void setup() {
  pinMode(buttonPin, INPUT);
  Serial.begin(9600);  // Start Serial Monitor
}

void loop() {
  int reading = digitalRead(buttonPin);

  if (reading != lastButtonState) {
    lastDebounceTime = millis();  // Reset debounce timer
  }

  if ((millis() - lastDebounceTime) > debounceDelay) {
    if (reading != buttonState) {
      buttonState = reading;
      if (buttonState == HIGH) {
        counter++;
        Serial.print("Button pressed count: ");
        Serial.println(counter);
      }
    }
  }

  lastButtonState = reading;
}
