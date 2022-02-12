## Sample-Explain

# Program 01 Serial-Monitor

Code :

	#include <Arduino.h>

	int cnt = 0;

	void setup()
	{
		Serial.begin(115200);
	}

	void loop()
	{
		cnt++;
		Serial.printf("PATTANI :%d\n",cnt);
		int s = cnt % 5 + 1;
		int d = s * 1000;
		delay(d);
	}	

#include เป็นคำสั่งที่ใช้อ้างอิงไฟล์ภายนอก เพื่อเรียกใช้ฟังก์ชั่น ==> int cnt คือ เริ่มนับแบบจำนวนเต็มโดยให้ count = 0 ==> void setup() คือ ฟังก์ชั่นใช้ในการประกาศค่าเริ่มต้น เป็นฟังก์ชั่นที run ครั้งเดียว ==> Serial.begin() ใช้ตั้งค่าความเร็วในการสื่อสารเป็นบิตต่อวินาที ==> void loop() คือ ฟังก์ชั่นโค้ดให้โปรแกรม run วนลูปไปเรื่อย ๆ ==> จากนั้นให้ Count บวกเพิ่มที่ละ 1 ==> serial.printf("PATTANI" :%d\n",cnt) คือ แสดง count ในรูปจำนวนเต็ม แล้วขึ้นบรรทัดใหม่ ==> delay(1000) คือ หน่วงเวลา 1000 ms หรือ 1 s

## Program 02 Scan-Wifi

Code :

	#include <Arduino.h>
	#include <ESP8266WiFi.h>

	int cnt = 0;

	void setup()
	{
		Serial.begin(115200);
		WiFi.mode(WIFI_STA);
		WiFi.disconnect();
		delay(100);
		Serial.println("\n\n\n");
	}

	void loop()
	{
		Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");
		int n = WiFi.scanNetworks();
		if(n == 0) {
			Serial.println("NO NETWORK FOUND");
		} else {
			for(int i=0; i<n; i++) {
				Serial.print(i + 1);
				Serial.print(": ");
				Serial.print(WiFi.SSID(i));
				Serial.print(" (");
				Serial.print(WiFi.RSSI(i));
				Serial.println(")");
				Serial.print(WiFi.channel(i));
				delay(10);
			}
		}
		Serial.println("\n\n");
		delay(10 * 1000);
	}	

#include เป็นคำสั่งที่ใช้อ้างอิงไฟล์ภายนอก เพื่อเรียกใช้ฟังก์ชั่น  ==> int cnt คือ เริ่มนับแบบจำนวนเต็มโดยให้ count = 0 

void setup() คือ ฟังก์ชั่นใช้ในการประกาศค่าเริ่มต้น เป็นฟังก์ชั่นที run ครั้งเดียว ==> Serial.begin() ใช้ตั้งค่าความเร็วในการสื่อสารเป็นบิตต่อวินาที ==> WiFi.mode(WIFI_STA); คือ การตั้งค่า WiFi เป็นโหมดสถานี ==> WiFi.disconnect(); คือ ตัดการเชื่อมต่อจากเครื่อข่ายหากเชื่อมต่อไว้ก่อนหน้านี้ ==> delay(100) หน่วงเวลา100 ms

void loop() คือ ฟังก์ชั่นโค้ดให้โปรแกรม run วนลูปไปเรื่อย ๆ ==> serial.println() คือ แสดงข้อมูล แล้วขึ้นบรรทัดใหม่ ==> WiFi.scanNetworks() คือ สแกนเครื่อยข่าย wifi ถ้า n=0 ให้ปริ้นไม่พบเครือค่าย ถ้าไม่เท่ากับ 0 ก็จะเข้าลูป ==> WiFi.SSID() ปริ้นชื่อ wifi บวกกับบอกความแรงสัญญาณ WiFi.RSSI() คือ ความแรงของสัญญาณ delay 10 ms

## Program 03 Output-port

Code : 

	#include <Arduino.h>
	#include <ESP8266WiFi.h>

	int cnt = 0;

	void setup()
	{
		Serial.begin(115200);
		pinMode(0, OUTPUT);
		Serial.println("\n\n\n");
	}

	void loop()
	{
		cnt++;
		if(cnt % 2) {
			Serial.println("========== ON ===========");
			digitalWrite(0, HIGH);
		} else {
			Serial.println("========== OFF ===========");
			digitalWrite(0, LOW);
		}
		delay(500);
	}

#include เป็นคำสั่งที่ใช้อ้างอิงไฟล์ภายนอก เพื่อเรียกใช้ฟังก์ชั่น ==> int cnt คือ เริ่มนับแบบจำนวนเต็มโดยให้ count = 0 

void setup() คือ ประกาศค่าเริ่มต้น เป็นฟังก์ชั่นที run ครั้งเดียว ==> Serial.begin() ใช้เพื่อตั้งค่าความเร็วในการสื่อสารเป็นบิตต่อวินาที ==> pinMode() กำหนดการทำงานของ pin

void loop() คือ ฟังก์ชั่นโค้ดให้โปรแกรม run วนลูปไปเรื่อย ๆ ==> ให้ count บวกทีละ 1 ถ้า cnt = 2 print ON นอกนั้น print OFF

digitalWrite() ใช้สำหรับสั่งให้ Arduino เขียนค่า HIGH หรือ LOW ที่ขา digital ของบอร์ด ==> delay(500) ms

## Program 04

Code :

	#include <Arduino.h>
	#include <ESP8266WiFi.h>

	int cnt = 0;

	void setup()
	{
		Serial.begin(115200);
		pinMode(0, INPUT);
		pinMode(2, OUTPUT);
		Serial.println("\n\n\n");
	}

	void loop()
	{
		int val = digitalRead(0);
		Serial.printf("======= read %d\n", val);
		if(val==1) {
			digitalWrite(2, LOW);
		} else {
			digitalWrite(2, HIGH);
		}
		delay(100);
	}

#include เป็นคำสั่งที่ใช้อ้างอิงไฟล์ภายนอก เพื่อเรียกใช้ฟังก์ชั่น ==> int cnt คือ เริ่มนับแบบจำนวนเต็มโดยให้ count = 0 

void setup() คือ ประกาศค่าเริ่มต้น เป็นฟังก์ชั่นที run ครั้งเดียว ==> Serial.begin() ใช้เพื่อตั้งค่าความเร็วในการสื่อสารเป็นบิตต่อวินาที ==> pinMode() กำหนดการทำงานของ pin

void loop() คือ ฟังก์ชั่นโค้ดให้โปรแกรม run วนลูปไปเรื่อย ๆ ==> int val เก็บค่าสัญญาณ digitalRead() ที่อ่านค่าสถานะของขาดิจิตอลเป็นจำนวนเต็ม  ถ้าค่าเป็น 1 digitalWrite(2, LOW) เขียนค่า LOW ที่ขา digital ของบอร์ด แต่ถ้าเป็น 2 digitalWrite(2, HIGH) เขียนค่า HIGH ที่ขา digital ของบอร์ด ==> delay(100) ms

## Program 05

Code :

	#include <ESP8266WiFi.h>
	//#include <WiFiClient.h>
	#include <ESP8266WebServer.h>

	const char* ssid = "HI_BMFWIFI_2.4G";
	const char* password = "0819110933";

	ESP8266WebServer server(80);

	int cnt = 0;

	void setup(void){
		Serial.begin(115200);

		WiFi.mode(WIFI_STA);
		WiFi.begin(ssid, password);
		while (WiFi.status() != WL_CONNECTED) {
			delay(500);
			Serial.print(".");
		}
		Serial.print("\n\nIP address: ");
		Serial.println(WiFi.localIP());

		server.onNotFound([]() {
			server.send(404, "text/plain", "Path Not Found");
		});

		/// http://192.0.0.1/ = Hello cnt: ???
		server.on("/", []() {
			cnt++;
			String msg = "Hello cnt: ";
			msg += cnt;
			server.send(200, "text/plain", msg);
		});
		/// http://192.0.0.1/on = Hello cnt: ???
		server.on("/on", []() {
			cnt++;
			String msg = "Switch on ";
			msg += cnt;
			server.send(200, "text/plain", msg);
		});
		/// http://192.0.0.1/off = Switch off: ???
		server.on("/off", []() {
			cnt++;
			String msg = "Hello cnt: ";
			msg += cnt;
			server.send(200, "text/plain", msg);
		});

		server.begin();
		Serial.println("HTTP server started");
	}

	void loop(void){
  	server.handleClient();
	}

#include เป็นคำสั่งที่ใช้อ้างอิงไฟล์ภายนอก เพื่อเรียกใช้ฟังก์ชั่น platformio  รูปแบบการใช้งาน

const char* ssid = "Username" คือ การประกาศสร้างตัวแปรเก็บ Username เครื่อข่าย WiFi ชื่อว่า ssid

const char* password = "Password" คือ การประกาศสร้างตัวแปรเก็บ Password ของเครื่อข่าย WiFi ชื่อว่า password

ESP8266WebServer server(80) คือ เปิด WebServer ที่ port 80

void setup() คือ ฟังก์ชั่นใช้ในการประกาศค่าเริ่มต้น เป็นฟังก์ชั่นที run ครั้งเดียว

Serial.begin() ใช้เพื่อตั้งค่าความเร็วในการสื่อสารเป็นบิตต่อวินาที

WiFi.mode(WIFI_STA); คือ เป็นการตั้งค่า WiFi เป็นโหมดสถานี

WiFi.begin(ssid, pass) คือ สำหรับเชื่อมต่อไวไฟ โดยใช้ชื่อไวไฟ และ รหัสผ่านของเครื่อยข่าย

delay() คือ หน่วงเวลา (ms)

## Program 06

	Code :

	#include <ESP8266WiFi.h>
	//#include <WiFiClient.h>
	#include <ESP8266WebServer.h>

	const char* ssid = "MY-ESP8266";
	const char* password = "choompol";

	IPAddress local_ip(192, 168, 1, 1);
	IPAddress gateway(192, 168, 1, 1);
	IPAddress subnet(255, 255, 255, 0);

	ESP8266WebServer server(80);

	int cnt = 0;

	void setup(void){
		Serial.begin(115200);

		WiFi.softAP(ssid, password);
		WiFi.softAPConfig(local_ip, gateway, subnet);
		delay(100);

		server.onNotFound([]() {
			server.send(404, "text/plain", "Path Not Found");
		});

		server.on("/", []() {
			cnt++;
			String msg = "Hello cnt: ";
			msg += cnt;
			server.send(200, "text/plain", msg);
		});

		server.begin();
		Serial.println("HTTP server started");
	}

	void loop(void){
  	server.handleClient();
	}

#include เป็นคำสั่งที่ใช้อ้างอิงไฟล์ภายนอก เพื่อเรียกใช้ฟังก์ชั่น หรือตัวแปรที่มีการสร้างหรือกำหนดไว้ในไฟล์นั้น รูปแบบการใช้งาน

const char* ssid = "Username" คือ การประกาศสร้างตัวแปรเก็บ Username เครื่อข่าย WiFi ชื่อว่า ssid

const char* password = "Password" คือ การประกาศสร้างตัวแปรเก็บ Password ของเครื่อข่าย WiFi ชื่อว่า password

local_ip คือ สำหรับตั้ง IP

gateway คือ สำหรับตั้ง gateway

subnet คือ สำหรับตั้ง subnet

ESP8266WebServer server(80) คือ เปิด WebServer ที่ port 80

WiFi.softAP(ssid,passwaord) คือ ฟังก์ชันสำหรับตั้งค่า Access Point ใช้งานในโหมด AP mode

WiFi.softAPConfig(IPAddress local_ip, IPAddress gateway, IPAddress subnet) คือ ฟังก์ชันสำหรับตั้งค่า IP , gateway , subnet ใน AP mode

delay() คือ หน่วงเวลา (ms)

