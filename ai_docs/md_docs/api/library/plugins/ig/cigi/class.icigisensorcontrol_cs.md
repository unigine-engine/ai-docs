# CigiSensorControl Class (CS)

**Inherits from:** CigiHostPacket


## CigiSensorControl Class

### Properties

## 🔒︎ int ViewID

The view ID specified in the packet.
## 🔒︎ int SensorID

The sensor ID specified in the packet.
## 🔒︎ int SensorEnabled

The value of the **Sensor On/Off** parameter specified in the packet.
## 🔒︎ int Polarity

The value of the **Polarity** parameter specified in the packet. Determines whether the sensor shows white hot or black hot.
## 🔒︎ int DropoutEnabled

The value of the **Line-by-Line Dropout Enable** parameter specified in the packet. This effect is meant to simulate the horizontal stripes caused by a transient loss of video information.
## 🔒︎ int AutomaticGain

The value of the **Automatic Gain** parameter specified in the packet.
## 🔒︎ int TrackColor

The value of the **Track White/Black** parameter specified in the packet.
## 🔒︎ int TrackMode

The value of the **Track Mode** parameter specified in the packet. Determines which track mode the sensor will use.
## 🔒︎ int Response

The value of the **Response Type** parameter specified in the packet.
## 🔒︎ float Gain

The value of the **Gain** parameter specified in the packet. Determines the contrast of the sensor display.
## 🔒︎ float Level

The value of the **Level** parameter specified in the packet. Determines the brightness of the sensor display.
## 🔒︎ float Coupling

The value of the **AC Coupling** parameter specified in the packet. Determines the AC coupling decay constant for the sensor display.
## 🔒︎ float Noise

The value of the **Noise** parameter specified in the packet. Determines the amount of detector noise for the sensor.
### Members

---
