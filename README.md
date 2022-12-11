# Embedded09

### 아이디어 소개
- 물체의 이동을 감지하는 시스템
- 별도의 장소에 부착하여 통행량을 측정하기 위해서 사용
- 블루투스로 연결된 핸드폰에서 보안모드와 통계모드를 조절할 수 있음
- 보안모드에서는 이동 감지 시 경고음과 LED가 동작하고 스마트폰으로 경고 알람이 전송
- 통계모드에서는 이동 감지 시 프로그램 상에서 count를 파일에 기록
- 이동을 감지할 때마다 측정하는 것이 아니라 일정 시간동안의 동행량이 파일에 기록됨
- 스마트폰에서 파일에 저장된 기록을 불러서 확인 가능
- 보안모드에 이동이 감지된 후 스마트폰에서 경고음과 LED를 조작 가능

### 사용된 센서 및 장치
- 초음파 센서(HC-SR04)
- 블루투스 모듈(HC-06)
- 액티브 스피커
- LED

### 전체 시스템 구조
![image](https://user-images.githubusercontent.com/90839233/206896733-0d123e5a-1c0c-40eb-ad86-51fce4951a3b.png)

### 주요 개발 내용
- 초음파 센서(HC-SR04) / Security.c

1. 최대 거래 측정
2. 측정 유효 범위 = 최대 거리 - margin

(통계모드일 때)

3. 측정 유효 범위 > 측정 값 = 물체 인식
4. 물체 인식 후, 다시 특정 유효 범위로 복귀시 counter 함수 호출
5. counter 함수 갱신 시 파일에 기록

(보안모드일 때)

3. 측정 유효 범위 > 측정값 = 물체 인식
4. 물체 인식시 buzzer 작동((waring) on)
5. UserControl에서 bool값 변화 (bool WARING FALSE) 수신시 부저 작동 종료

- 블루투스(HC-06) 및 액티브 스피커, LED / UserControl.c

1. 사용자 입력 대기
2. 사용자가 값 입력 (user(phone) -> UserControl.c(HC-06))
3. 블루투스로 받은 사용자의 입력에 따른 함수 실행
- 0 : 보안모드로 변경
- 1 : 통계모드로 변경
- 2 : 기록 파일 요청
- 3 : 기록 파일 초기화
- 4 : 초기 설정하기
- 5 : 경보 끄기


### 제한조건 구현 내용
1. 제한조건 구현 내용 (멀티프로세스/쓰레드, IPC/뮤텍스)

### 사용 설명서
1. 장치를 설치 후 블루투스로 스마트폰과 연동시켜준다.
2. 스마트폰에서 '초기 설정' 이라는 메뉴를 눌러 측정할 거리를 계산한다.
3. 기본적으로 통계모드가 실행된다.
4. 보안모드로 변경을 원하면 스마트폰에서 '보안' 메뉴를 선택한다.
5. 통행량의 기록을 확인하고 싶다면 스마트폰에서 '기록 확인' 메뉴를 선택한다.
6. 기록된 통행량을 삭제하고자 한다면 스마트폰에서 '기록 삭제' 메뉴를 선택한다.
7. 보안모드에서 경보 발생 시 울리는 경보음과 LED를 끄고 싶다면 '경보 해제' 메뉴를 선택한다.

### 문제 및 해결방안

### 한계점

### 시연 영상

### 참고자료






