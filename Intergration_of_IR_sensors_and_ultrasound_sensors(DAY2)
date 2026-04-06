// ===== MOTOR PINS =====
int IN1 = 8;
int IN2 = 9;
int IN3 = 10;
int IN4 = 11;
int ENA = 5;
int ENB = 6;

// ===== IR SENSORS =====
int leftIR  = 12;
int midIR   = 7;
int rightIR = 4;

// ===== ULTRASONIC =====
int trig = 2;
int echo = 3;

void setup() {
  Serial.begin(9600);

  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);

  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);

  pinMode(leftIR, INPUT);
  pinMode(midIR, INPUT);
  pinMode(rightIR, INPUT);

  pinMode(trig, OUTPUT);
  pinMode(echo, INPUT);

  analogWrite(ENA, 180);
  analogWrite(ENB, 180);

  Serial.println("=== SYSTEM STARTED ===");
}

// ===== DISTANCE FUNCTION =====
int getDistance() {
  digitalWrite(trig, LOW);
  delayMicroseconds(2);

  digitalWrite(trig, HIGH);
  delayMicroseconds(10);

  digitalWrite(trig, LOW);

  long duration = pulseIn(echo, HIGH, 30000);
  int distance = duration * 0.034 / 2;

  return distance;
}

void loop() {

  int distance = getDistance();

  int L = digitalRead(leftIR);
  int M = digitalRead(midIR);
  int R = digitalRead(rightIR);

  // DEBUG OUTPUT
  Serial.print("Dist:");
  Serial.print(distance);
  Serial.print(" L:");
  Serial.print(L);
  Serial.print(" M:");
  Serial.print(M);
  Serial.print(" R:");
  Serial.println(R);

  // ===== OBSTACLE =====
  if (distance > 0 && distance < 15) {
    stopMotors();
    Serial.println("STOP - OBSTACLE");
    return;
  }

  // ===== LINE FOLLOW =====
  if (M == 0) {
    forward();
  }
  else if (L == 0) {
    left();
  }
  else if (R == 0) {
    right();
  }
  else {
    stopMotors();
  }

  delay(150);
}

// ===== MOVEMENTS =====

void forward() {
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void left() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void right() {
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
}

void stopMotors() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
}
