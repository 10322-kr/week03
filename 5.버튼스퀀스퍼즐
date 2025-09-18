# week03_5
// 핀 설정
const int button1Pin = 2; // 버튼 1
const int button2Pin = 3; // 버튼 2
const int button3Pin = 4; // 버튼 3

const int led1Pin = 10; // LED 1
const int led2Pin = 11; // LED 2
const int led3Pin = 12; // LED 3

// 정답 시퀀스 (1, 3, 2)
const int correctSequence[] = {1, 3, 2};
const int sequenceLength = 3;

// 입력 버퍼
int inputBuffer[sequenceLength];
int bufferIndex = 0;

// 이전 버튼 상태 저장
int lastButton1State = HIGH;
int lastButton2State = HIGH;
int lastButton3State = HIGH;

void setup() {
  // 핀 모드 설정
  pinMode(button1Pin, INPUT_PULLUP);
  pinMode(button2Pin, INPUT_PULLUP);
  pinMode(button3Pin, INPUT_PULLUP);
  
  pinMode(led1Pin, OUTPUT);
  pinMode(led2Pin, OUTPUT);
  pinMode(led3Pin, OUTPUT);
  
  Serial.begin(9600);
}

void loop() {
  // 현재 버튼 상태 읽기
  int button1State = digitalRead(button1Pin);
  int button2State = digitalRead(button2Pin);
  int button3State = digitalRead(button3Pin);
  
  // 버튼이 눌렸을 때 (상태가 HIGH에서 LOW로 변경)
  if (button1State == LOW && lastButton1State == HIGH) {
    handleButtonPress(1);
  }
  if (button2State == LOW && lastButton2State == HIGH) {
    handleButtonPress(2);
  }
  if (button3State == LOW && lastButton3State == HIGH) {
    handleButtonPress(3);
  }
  
  // 이전 버튼 상태 업데이트
  lastButton1State = button1State;
  lastButton2State = button2State;
  lastButton3State = button3State;
}

void handleButtonPress(int buttonNumber) {
  // 입력 버퍼에 버튼 번호 추가
  inputBuffer[bufferIndex] = buttonNumber;
  bufferIndex++;
  
  // 버퍼가 가득 찼는지 확인 (3번 입력)
  if (bufferIndex == sequenceLength) {
    checkSequence();
  }
}

void checkSequence() {
  bool isCorrect = true;
  for (int i = 0; i < sequenceLength; i++) {
    if (inputBuffer[i] != correctSequence[i]) {
      isCorrect = false;
      break;
    }
  }
  
  if (isCorrect) {
    // 정답 피드백: 3개 LED 2초간 동시 점등
    Serial.println("Correct!");
    digitalWrite(led1Pin, HIGH);
    digitalWrite(led2Pin, HIGH);
    digitalWrite(led3Pin, HIGH);
    delay(2000); // 2초 대기
    digitalWrite(led1Pin, LOW);
    digitalWrite(led2Pin, LOW);
    digitalWrite(led3Pin, LOW);
  } else {
    // 오답 피드백: 모든 LED 200ms 간격으로 2회 점멸
    Serial.println("Incorrect!");
    for (int i = 0; i < 2; i++) {
      digitalWrite(led1Pin, HIGH);
      digitalWrite(led2Pin, HIGH);
      digitalWrite(led3Pin, HIGH);
      delay(200);
      digitalWrite(led1Pin, LOW);
      digitalWrite(led2Pin, LOW);
      digitalWrite(led3Pin, LOW);
      delay(200);
    }
  }
  
  // 버퍼 초기화
  bufferIndex = 0;
}
