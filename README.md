## ✍️ Writing Robot

### RzRz 2축 글자 작성 로봇 설계 및 구현

## 1. Project Overview

본 프로젝트는 **2개의 회전 관절(Rz-Rz)을 갖는 로봇을 직접 설계·제작하고, 역기구학(Inverse Kinematics)을 활용하여 글자를 작성하는 로봇을 구현한 프로젝트**입니다.

SolidWorks를 활용하여 로봇의 기구 구조를 설계하고, MATLAB에서 작업공간(Workspace) 분석과 글자 작성을 위한 역기구학 기반 궤적 설계를 수행했습니다.

이후 RoboDK에서 로봇의 동작을 시뮬레이션하고, 3D 프린팅으로 제작한 실제 로봇에서 글자 작성 동작을 구현했습니다.

### Project Information

| 항목 | 내용 |
|---|---|
| Robot | 2-DOF Rz-Rz Robot |
| Mechanical Design | SolidWorks |
| Kinematics & Trajectory | MATLAB |
| Simulation | RoboDK |
| Manufacturing | 3D Printing |
| Key Concepts | Inverse Kinematics, Workspace, Trajectory Planning |

### Final Result

<div align="center">
  <video
    src="https://github.com/user-attachments/assets/de6aa549-04de-4e60-93e6-d1ae50b5c384"
    width="480"
    controls>
  </video>
</div>

## 2. Mechanical Design

### 2.1 로봇 기구 설계

SolidWorks를 활용하여 2개의 회전 관절을 갖는 로봇의 기구 구조를 설계했습니다.

각 관절의 회전운동을 통해 로봇 말단에 장착된 펜을 이동시키는 구조로, 로봇의 안정적인 동작을 위해 중심부를 크고 무겁게 설계하여 무게중심을 고려했습니다.

또한 글자를 작성하기 위해서는 펜의 평면 이동뿐만 아니라 종이와의 접촉을 제어해야 하므로, **Rack & Pinion 기어를 활용한 펜의 상하운동 구조**를 설계했습니다.

- **2축 회전 관절:** 로봇 말단의 평면 위치 제어
- **Rack & Pinion:** 펜의 상하운동 제어
- **Base:** 로봇의 무게중심과 안정성을 고려한 구조

#### SolidWorks Modeling

<p align="center">
  <img src="https://github.com/user-attachments/assets/18667e1d-1415-4539-965c-c39e603307d6" height="230" alt="CAD Detail 1"/>
  &nbsp;
  <img src="https://github.com/user-attachments/assets/12d3f4a6-e238-4a68-a3b1-2798ec275b40" height="230" alt="CAD Detail 2"/>
  &nbsp;
  <img src="https://github.com/user-attachments/assets/050c2809-2a36-4590-8859-ba98583e8661" height="230" alt="CAD Detail 3"/>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/ec6d4570-bd1e-4143-a2ed-7f4c7712615b" width="480" alt="Robot CAD Model"/>
</p>


#### Rack & Pinion Mechanism

<p align="center">
  <img src="https://github.com/user-attachments/assets/3ee0d9c6-3cb6-4e87-8b20-35ed3df082c5" height="260" alt="Rack and Pinion 1"/>
  &nbsp;&nbsp;
  <img src="https://github.com/user-attachments/assets/be797fae-9e6b-4e6e-a37c-c3f776a47336" height="260" alt="Rack and Pinion 2"/>
</p>


### 2.2 하드웨어 제작

SolidWorks에서 설계한 부품을 3D 프린터로 출력하여 실제 로봇을 제작했습니다.

출력된 링크와 관절 부품을 조립하고, 펜 구동부를 결합하여 글자 작성이 가능한 로봇 하드웨어를 구성했습니다.

#### 3D Printing & Assembly

<p align="center">
  <img src="https://github.com/user-attachments/assets/37a99dcc-c566-4295-bdca-493325de25b2" height="220" alt="3D Printing"/>
  <img src="https://github.com/user-attachments/assets/113d481f-7b15-4498-8551-bcf7a20ed4d8" height="220" alt="Robot Assembly1"/>
  <img src="https://github.com/user-attachments/assets/2ce24139-670a-462a-89b9-2a05a3d2d984" height="220" alt="Robot Assembly2"/>

  &nbsp;&nbsp;
  
</p>

## 3. Kinematics & Trajectory Planning

### 3.1 Workspace Analysis

로봇이 글자를 작성하기 위해서는 글자의 좌표가 로봇이 도달할 수 있는 작업공간(Workspace) 내에 존재해야 합니다.

MATLAB을 활용하여 **로봇의 관절 구조와 링크 길이에 따른 작업공간을 분석**하고, 글자 작성이 가능한 영역을 확인했습니다.

이를 바탕으로 로봇의 작업공간 내에서 글자 궤적을 설계했습니다.

#### Workspace Analysis (MATLAB)

<p align="center">
  <img src="https://github.com/user-attachments/assets/cbb6b797-2aa0-4f6a-9926-5e0eeb756fe8" width="520" alt="Workspace Analysis"/>
</p>

### 3.2 Inverse Kinematics

글자 작성에 필요한 목표 좌표를 실제 로봇의 관절 운동으로 변환하기 위해 역기구학(Inverse Kinematics)을 활용했습니다.

역기구학은 로봇 말단의 목표 위치가 주어졌을 때, 해당 위치에 도달하기 위한 관절 각도를 계산하는 방법입니다.

본 프로젝트에서는 MATLAB을 활용하여 글자의 형상을 좌표 기반 궤적으로 설계하고, 각 목표 좌표에 대응하는 관절 각도를 계산했습니다.

**Trajectory Planning Process**

1. **Character Design:** 작성할 글자의 형상을 좌표로 표현
2. **Workspace Check:** 목표 좌표가 로봇의 작업공간에 포함되는지 확인
3. **Inverse Kinematics:** 각 목표 좌표에 대응하는 관절 각도 계산
4. **Trajectory Generation:** 계산된 관절 각도를 기반으로 로봇 동작 궤적 구성

이 과정을 통해 글자의 형상을 로봇이 수행할 수 있는 관절 운동으로 변환했습니다.

#### Character Trajectory & Inverse Kinematics (MATLAB)

<p align="center">
  <img src="https://github.com/user-attachments/assets/13d34706-c5b2-4d53-937e-251b9db4c645" width="520" alt="Character Trajectory"/>
</p>

## 4. Robot Simulation

### 4.1 RoboDK Simulation

MATLAB에서 설계한 로봇의 동작을 검증하기 위해 RoboDK를 활용했습니다.

RoboDK 환경에서 로봇의 기구 구조를 구성하고, 역기구학을 기반으로 설계한 궤적에 따른 로봇의 움직임을 시뮬레이션했습니다.

이를 통해 실제 하드웨어에서 동작을 구현하기 전에 로봇의 이동 궤적과 동작을 확인했습니다.

#### RoboDK Simulation

<p align="center">
  <img src="https://github.com/user-attachments/assets/545e1f76-0f4e-4cb4-8184-03e762074cb9" width="500" alt="RoboDK Simulation"/>
</p>

## 5. Results

SolidWorks를 활용한 기구 설계부터 MATLAB 기반 운동학 해석, RoboDK 시뮬레이션 및 실제 로봇 제작까지 수행했습니다.

### 주요 결과

- **Mechanical Design:** Rz-Rz 2축 로봇 및 Rack & Pinion 기반 펜 구동부 설계
- **Hardware Implementation:** 3D 프린팅을 활용한 로봇 제작 및 조립
- **Kinematics:** MATLAB 기반 작업공간 분석 및 역기구학 계산
- **Trajectory Planning:** 글자 작성을 위한 관절 운동 궤적 설계
- **Simulation:** RoboDK를 활용한 로봇 동작 검증
- **Implementation:** 실제 로봇의 글자 작성 동작 구현

#### 실제 글자 작성 결과

<p align="center">
  <img src="https://github.com/user-attachments/assets/cda856ce-a6ae-459c-89b9-35974026aa13" width="520" alt="Writing Result"/>
</p>
