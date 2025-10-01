# LAB-4-10125

// C++ code

//

const int trigPin = 9;
const int echoPin = 10;

long duration;
int distance;
bool objectPresent = false;
int count = 0;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  if (distance > 0 && distance < 20) {
    if (!objectPresent) {
      Serial.println("Object Detected & Present");
      objectPresent = true;
    }
  } else {
    if (objectPresent) {
      Serial.println("Detected Object Is Gone");
      count++;
      Serial.print(count);
      Serial.println(" Objects Detected");
      objectPresent = false;
    } else {
      Serial.println("Waiting To Detect An Object");
    }
  }

  delay(300);
}
