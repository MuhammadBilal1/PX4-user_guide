# 모듈 참조: 시스템

## battery_simulator
소스: [modules/simulator/battery_simulator](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/simulator/battery_simulator)


### 설명

<a id="battery_simulator_usage"></a>

### 사용법
```
battery_simulator <command> [arguments...]
 Commands:
   start

   stop

   status        print status info
```
## battery_status
소스: [modules/battery_status](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/battery_status)


### 설명

제공 기능은 다음과 같습니다:
- ADC 드라이버의 출력을 읽고(ioctl 인터페이스를 통해) `battery_status`를 게시합니다.


### 구현
자체 스레드에서 실행되고, 현재 선택된 자이로 주제를 폴링합니다.

<a id="battery_status_usage"></a>

### 사용법
```
battery_status <command> [arguments...]
 Commands:
   start

   stop

   status        print status info
```
## camera_feedback
소스: [modules/camera_feedback](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/camera_feedback)


### 설명

<a id="camera_feedback_usage"></a>

### 사용법
```
camera_feedback <command> [arguments...]
 Commands:
   start

   stop

   status        print status info
```
## commander
소스: [modules/commander](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/commander)


### 설명
커맨더 모듈에는 모드 전환 및 안전 장치 동작을 위한 상태 머신이 포함되어 있습니다.

<a id="commander_usage"></a>

### 사용법
```
commander <command> [arguments...]
 Commands:
   start
     [-h]        Enable HIL mode

   calibrate     Run sensor calibration
     mag|accel|gyro|level|esc|airspeed Calibration type
     quick       Quick calibration (accel only, not recommended)

   check         Run preflight checks

   arm
     [-f]        Force arming (do not run preflight checks)

   disarm

   takeoff

   land

   transition    VTOL transition

   mode          Change flight mode
     manual|acro|offboard|stabilized|altctl|posctl|auto:mission|auto:loiter|auto
                 :rtl|auto:takeoff|auto:land|auto:precland Flight mode

   pair

   lockdown
     [off]       Turn lockdown off

   set_ekf_origin
     lat, lon, alt Origin Latitude, Longitude, Altitude

   lat|lon|alt   Origin latitude longitude altitude

   stop

   status        print status info
```
## dataman
소스: [modules/dataman](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/dataman)


### 설명
C API를 통해 간단한 데이터베이스 형태로 시스템에 영구 저장소를 제공하는 모듈입니다. 다중 백엔드가 지원됩니다.
- 파일(예: SD 카드)
- RAM (영구적이지 않음)

임무 웨이포인트, 임무 상태 및 지오펜스 다각형과 같은 다양한 유형의 구조화된 데이터를 저장합니다. 각 유형은 특정 유형과 고정된 최대 저장 항목 수를 가지고 있어, 빠른 랜덤 액세스가 가능합니다.

### 구현
단일 항목을 읽고 쓰는 것은 항상 원자적입니다. 여러 항목을 원자적으로 읽고 수정해야 하는 경우에는, `dm_lock`을 사용하여 항목 유형별로 추가 잠금이 있습니다.

**DM_KEY_FENCE_POINTS** 및 **DM_KEY_SAFE_POINTS** 항목: 첫 번째 데이터 요소는 이러한 유형의 항목 수를 저장하는 `mission_stats_entry_s` 구조체입니다. 이러한 항목은 항상 하나의 트랜잭션에서 원자적으로 업데이트됩니다(mavlink Mission Manager에서). 그 시간 동안 내비게이터는 지오펜스 항목 잠금을 획득하려고 시도하지만, 실패하며 지오펜스 위반을 확인하지 않습니다.

<a id="dataman_usage"></a>

### 사용법
```
dataman <command> [arguments...]
 Commands:
   start
     [-f <val>]  Storage file
                 values: <file>
     [-r]        Use RAM backend (NOT persistent)

 The options -f and -r are mutually exclusive. If nothing is specified, a file
 'dataman' is used

   poweronrestart Restart dataman (on power on)

   inflightrestart Restart dataman (in flight)

   stop

   status        print status info
```
## dmesg
소스: [systemcmds/dmesg](https://github.com/PX4/PX4-Autopilot/tree/master/src/systemcmds/dmesg)


### 설명

부팅 콘솔 메시지를 출력합니다. NuttX의 작업 대기열 및 syslog의 출력은 캡처되지 않습니다.

### 예

백그라운드에서 모든 메시지를 출력합니다.
```
dmesg -f &
```

<a id="dmesg_usage"></a>

### 사용법
```
dmesg <command> [arguments...]
 Commands:
     [-f]        Follow: wait for new messages
```
## esc_battery
소스: [modules/esc_battery](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/esc_battery)


### 설명
ESC 상태의 정보를 사용하여 구현하고, 배터리 상태를 게시합니다.

<a id="esc_battery_usage"></a>

### 사용법
```
esc_battery <command> [arguments...]
 Commands:
   start

   stop

   status        print status info
```
## gyro_calibration
소스: [modules/gyro_calibration](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/gyro_calibration)


### 설명
간단한 온라인 자이로스코프 교정.

<a id="gyro_calibration_usage"></a>

### 사용법
```
gyro_calibration <command> [arguments...]
 Commands:
   start

   stop

   status        print status info
```
## gyro_fft
소스: [modules/gyro_fft](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/gyro_fft)


### 설명

<a id="gyro_fft_usage"></a>

### 사용법
```
gyro_fft <command> [arguments...]
 Commands:
   start

   stop

   status        print status info
```
## heater
소스: [drivers/heater](https://github.com/PX4/PX4-Autopilot/tree/master/src/drivers/heater)


### 설명
설정점에서 IMU 온도를 조절하기 위하여 LP 작업 대기열에서 주기적으로 실행되는 백그라운드 프로세스입니다.

이 작업은 부팅 시 SENS_EN_THERMAL을 설정하거나, CLI를 통하여 시작 스크립트에서 시작할 수 있습니다.

<a id="heater_usage"></a>

### 사용법
```
heater <command> [arguments...]
 Commands:
   start

   stop

   status        print status info
```
## land_detector
소스: [modules/land_detector](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/land_detector)


### 설명
차량의 자유낙하와 착지상태를 감지하고, `vehicle_land_detected` 주제를 게시하는 모듈입니다. 각 차량 유형(멀티로터, 고정익, vtol, ...)은 명령 추력, 무장 상태 및 차량 모션과 같은 다양한 상태를 고려하여 자체 알고리즘을 제공합니다.

### 구현
모든 유형은 공통 기본 클래스를 사용하여 자체 클래스에서 구현됩니다. 기본 클래스는 상태를 유지합니다(착륙, 아마도_착륙, 지상_접촉). 가능한 각 상태는 파생 클래스에서 구현됩니다. 각 내부 상태의 히스테리시스 및 고정된 우선 순위에 따라 실제 land_detector 상태가 결정됩니다.

#### 멀티콥터 착륙 감지기
**ground_contact**: z 방향의 추력 설정점 및 속도는 GROUND_CONTACT_TRIGGER_TIME_US 시간에 대해 정의된 임계값 미만이어야 합니다. ground_contact가 감지되면, 위치 컨트롤러는 본체 x 및 y의 추력 설정값을 끕니다.

**maybe_landed**: 더 엄격한 추력 설정값 임계값과 함께 ground_contact가 필요하며, 수평 방향으로 속도가 없습니다. 트리거 시간은 MAYBE_LAND_TRIGGER_TIME에 의해 정의됩니다. Maybe_landed가 감지되면 위치 컨트롤러는 추력 설정값을 0으로 설정합니다.

**착륙**: LAND_DETECTOR_TRIGGER_TIME_US 시간 동안 참이 되기 위해서는 may_landed가 필요합니다.

모듈은 HP 작업 대기열에서 주기적으로 실행됩니다.

<a id="land_detector_usage"></a>

### 사용법
```
land_detector <command> [arguments...]
 Commands:
   start         Start the background task
     fixedwing|multicopter|vtol|rover|airship Select vehicle type

   stop

   status        print status info
```
## load_mon
소스: [modules/load_mon](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/load_mon)


### 설명
CPU 로드 및 RAM 사용량을 계산하고, `cpuload` 주제를 게시하기 위하여 낮은 우선순위 작업 대기열에서 주기적으로 실행되는 백그라운드 프로세스입니다.

NuttX에서는 각 프로세스의 스택 사용량도 확인하고, 300바이트 미만으로 떨어지면 경고가 출력되고 로그 파일에도 기록됩니다.

<a id="load_mon_usage"></a>

### 사용법
```
load_mon <command> [arguments...]
 Commands:
   start         Start the background task

   stop

   status        print status info
```
## logger
소스: [modules/logger](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/logger)


### 설명
설정 가능한 uORB 주제 세트와 시스템 printf 메시지(`PX4_WARN` 및 `PX4_ERR`)를 ULog 파일에 기록하는 시스템 로거입니다. 시스템 및 비행 성능 평가, 튜닝, 재생 및 충돌 분석에 사용할 수 있습니다.

2개의 백엔드를 지원합니다.
- 파일: ULog 파일을 파일 시스템(SD 카드)에 기록합니다.
- MAVLink: MAVLink를 통해 ULog 데이터를 클라이언트로 스트리밍합니다(클라이언트가 이를 지원해야 함).

두 백엔드를 동시에 활성화하고 사용할 수 있습니다.

파일 백엔드는 전체(일반 로그)와 미션 로그의 두 가지 유형의 로그 파일을 지원합니다. 임무 로그는 축소된 ulog 파일이며, 지오태깅 또는 차량 관리 등에 사용할 수 있습니다. SDLOG_MISSION 매개변수를 통하여 활성화 및 설정할 수 있습니다. 일반 로그는 항상 미션 로그의 상위 집합입니다.

### 구현
구현은 두 개의 스레드를 사용합니다.
- 고정된 속도로 실행되는 메인 스레드(또는 -p로 시작된 경우 주제에 대한 폴링) 및 데이터 업데이트 확인
- 작성자 스레드, 파일에 데이터 쓰기

그 사이에는 구성 가능한 크기의 쓰기 버퍼가 있습니다(및 미션 로그를 위한 또 다른 고정 크기 버퍼). 드롭아웃을 방지하려면 크기가 커야 합니다.

### 예
즉시 로깅을 시작하는 일반적인 사용법입니다.
```
logger start -e -t
```

또는, 이미 동작중일 경우
```
logger on
```

<a id="logger_usage"></a>

### 사용법
```
logger <command> [arguments...]
 Commands:
   start
     [-m <val>]  Backend mode
                 values: file|mavlink|all, default: all
     [-x]        Enable/disable logging via Aux1 RC channel
     [-e]        Enable logging right after start until disarm (otherwise only
                 when armed)
     [-f]        Log until shutdown (implies -e)
     [-t]        Use date/time for naming log directories and files
     [-r <val>]  Log rate in Hz, 0 means unlimited rate
                 default: 280
     [-b <val>]  Log buffer size in KiB
                 default: 12
     [-p <val>]  Poll on a topic instead of running with fixed rate (Log rate
                 and topic intervals are ignored if this is set)
                 values: <topic_name>

   on            start logging now, override arming (logger must be running)

   off           stop logging now, override arming (logger must be running)

   stop

   status        print status info
```
## netman
소스: [systemcmds/nshterm](https://github.com/PX4/PX4-Autopilot/tree/master/src/systemcmds/netman)


  설명 네트워크 구성 관리자는 네트워크 설정을 비휘발성 메모리에 저장합니다.  부팅시 `업데이트` 옵션이 실행됩니다. 네트워크 구성이 존재하지 않는 경우. 기본 설정은 비휘발성에 저장되고 시스템이 재부팅됩니다. 후속 부팅 시 `업데이트` 옵션은 SD 카드의 루트에 `net.cfg`가 있는 지 확인합니다.  `net.cfg`의 네트워크 설정을 비휘발성 메모리에 저장하고 파일을 삭제하고 시스템을 재부팅합니다.

  `저장` 옵션은 SD 카드에 `net.cfg`됩니다. 이것을 사용하여 설정을 편집합니다. `show` 옵션은 네트워크 설정을 콘솔에 표시합니다.

  예 $ netman save # 매개변수를 SD 카드에 저장합니다. $ netman show # 현재 설정을 표시합니다. $ netman update -i eth0 # 업데이트 수행

<a id="netman_usage"></a>

### 사용법
```
netman <command> [arguments...]
 Commands:
   show          Display the current persistent network settings to the console.

   update        Check SD card for net.cfg and update network persistent network
                 settings.

   save          Save the current network parameters to the SD card.
     [-i <val>]  Set the interface name
                 default: eth0
```
## pwm_input
소스: [drivers/pwm_input](https://github.com/PX4/PX4-Autopilot/tree/master/src/drivers/pwm_input)


### 설명
타이머 캡처 ISR을 통하여 AUX5(또는 MAIN5)의 PWM 입력을 측정하고, uORB 'pwm_input' 메시지를 통하여 게시합니다.

<a id="pwm_input_usage"></a>

### 사용법
```
pwm_input <command> [arguments...]
 Commands:
   start

   test          prints PWM capture info.

   stop

   status        print status info
```
## rc_update
소스: [modules/rc_update](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/rc_update)


### 설명
rc_update 모듈은 RC 채널 매핑을 처리합니다. 원시 입력 채널(`input_rc`)을 읽은 다음 보정을 적용하고 RC 채널을 구성된 채널에 매핑합니다. 모드를 전환한 다음 `rc_channels` 및 `manual_control_setpoint`로 게시합니다.

### 구현
제어 대기 시간을 줄이기 위하여 모듈은 input_rc 게시에 예약됩니다.

<a id="rc_update_usage"></a>

### 사용법
```
rc_update <command> [arguments...]
 Commands:
   start

   stop

   status        print status info
```
## replay
소스: [modules/replay](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/replay)


### 설명
이 모듈은 ULog 파일을 재생하는 데 사용됩니다.

구성에 사용되는 두 가지 환경 변수가 있습니다. `재생`, ULog 파일 이름으로 설정해야 합니다. 재생될 로그 파일입니다. 두 번째는 `replay_mode`를 통해 지정된 모드입니다.
- `replay_mode=ekf2`: 특정 EKF2 재생 모드. ekf2 모듈과 함께만 사용할 수 있지만, 가능한 한 빨리 재생할 수 있습니다.
- 일반 그렇지 않으면 이것은 모든 모듈을 재생하는 데 사용할 수 있지만 재생은 로그가 기록된 것과 동일한 속도로 수행됩니다.

모듈은 일반적으로 uORB 게시자 규칙과 함께 사용되어 재생되어야 하는 메시지를 지정합니다. 재생 모듈은 로그에 있는 모든 메시지를 게시합니다. 또한 로그의 매개변수를 적용합니다.

재생 절차는 [시스템 전체 재생](https://dev.px4.io/master/en/debug/system_wide_replay.html) 페이지에 설명되어 있습니다.

<a id="replay_usage"></a>

### 사용법
```
replay <command> [arguments...]
 Commands:
   start         Start replay, using log file from ENV variable 'replay'

   trystart      Same as 'start', but silently exit if no log file given

   tryapplyparams Try to apply the parameters from the log file

   stop

   status        print status info
```
## send_event
소스: [modules/events](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/events)


### 설명
하우스키핑 작업을 수행하기 위하여 LP 작업 대기열에서 주기적으로 실행되는 백그라운드 프로세스입니다. 현재 RC Loss에 대한 톤 알람만 담당합니다.

작업은 CLI 또는 uORB 주제(MAVLink의 차량 명령 등)를 통하여 시작할 수 있습니다.

<a id="send_event_usage"></a>

### 사용법
```
send_event <command> [arguments...]
 Commands:
   start         Start the background task

   stop

   status        print status info
```
## sensors
소스: [modules/sensors](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/sensors)


### 설명
센서 모듈은 전체 시스템의 중심입니다. 드라이버에서 낮은 수준의 출력을 가져와서, 사용 가능한 형식으로 바꾸고 나머지 시스템에 게시합니다.

제공 기능은 다음과 같습니다:
- 센서 드라이버(`sensor_gyro` 등)의 출력을 읽습니다. 동일한 유형이 여러 개 있는 경우 투표 및 장애 조치 처리를 수행합니다. 그런 다음, 보드 회전 및 온도 보정을 적용합니다(활성화된 경우). 마지막으로 데이터를 게시합니다. 주제 중 하나는 시스템의 많은 부분에서 사용되는 `sensor_combined`입니다.
- 매개변수가 변경되거나 시작될 때 센서 드라이버가 업데이트된 보정 매개변수(스케일 및 오프셋)를 가져오는 지 확인하십시오. 센서 드라이버는 매개변수 업데이트를 위하여 ioctl 인터페이스를 사용합니다. 이것이 제대로 작동하려면, `센서`가 시작될 때 센서 드라이버가 이미 실행되고 있어야 합니다.
- 센서 일관성 검사를 수행하고, `sensors_status_imu` 주제를 게시합니다.

### 구현
자체 스레드에서 실행되고, 현재 선택된 자이로 주제를 폴링합니다.

<a id="sensors_usage"></a>

### 사용법
```
sensors <command> [arguments...]
 Commands:
   start
     [-h]        Start in HIL mode

   stop

   status        print status info
```
## temperature_compensation
소스: [modules/temperature_compensation](https://github.com/PX4/PX4-Autopilot/tree/master/src/modules/temperature_compensation)


### 설명
온도 보상 모듈을 사용하면 시스템의 모든 자이로(들), 가속(들) 및 바로(들)이 온도 보상을 받을 수 있습니다. 모듈은 센서에서 오는 데이터를 모니터링하고, 온도 변화가 감지될 때마다 관련 sensor_correction 주제를 업데이트합니다. 모듈은 또한 다음 부팅 시 계수 계산 루틴을 수행하도록 구성할 수 있으며, 이를 통하여 차량이 온도 주기를 겪는 동안 열 보정 계수를 계산할 수 있습니다.

<a id="temperature_compensation_usage"></a>

### 사용법
```
temperature_compensation <command> [arguments...]
 Commands:
   start         Start the module, which monitors the sensors and updates the
                 sensor_correction topic

   calibrate     Run temperature calibration process
     [-g]        calibrate the gyro
     [-a]        calibrate the accel
     [-b]        calibrate the baro (if none of these is given, all will be
                 calibrated)

   stop

   status        print status info
```
## tune_control
소스: [systemcmds/tune_control](https://github.com/PX4/PX4-Autopilot/tree/master/src/systemcmds/tune_control)


### 설명

(외부) 음향 톤을 제어하고 테스트하기 위한 명령줄 도구입니다.

음향 톤은 가청 알림 및 경고를 제공합니다(예: 시스템이 작동할 때, 위치 잠금을 얻을 때 등). 이 도구를 사용하려면, tune_control uorb 주제를 처리할 수 있는 드라이버가 실행 중이어야 합니다.

음향 톤 형식과 사전 정의된 시스템 조정에 대한 정보는 다음을 참고하십시오. https://github.com/PX4/Firmware/blob/master/src/lib/tunes/tune_definition.desc

### 예

시스템 소리 2번을 재생합니다.
```
tune_control play -t 2
```

<a id="tune_control_usage"></a>

### 사용법
```
tune_control <command> [arguments...]
 Commands:
   play          Play system tune or single note.
     error       Play error tune
     [-t <val>]  Play predefined system tune
                 default: 1
     [-f <val>]  Frequency of note in Hz (0-22kHz)
     [-d <val>]  Duration of note in us
     [-s <val>]  Volume level (loudness) of the note (0-100)
                 default: 40
     [-m <val>]  Melody in string form
                 values: <string> - e.g. "MFT200e8a8a"

   libtest       Test library

   stop          Stop playback (use for repeated tunes)
```
## work_queue
소스: [systemcmds/work_queue](https://github.com/PX4/PX4-Autopilot/tree/master/src/systemcmds/work_queue)


### 설명

작업 대기열 상태를 표시하는 명령줄 도구입니다.

<a id="work_queue_usage"></a>

### 사용법
```
work_queue <command> [arguments...]
 Commands:
   start

   stop

   status        print status info
```
