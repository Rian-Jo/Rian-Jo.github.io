---
layout: post
title:  "[System] RBDL 설치 및 실행"
subtitle:   "C++, robotics package, RBDL, visual studio, Windows"
categories: devlog
tags: system devlog
---

로봇 라이브러리 중 손쉽게 사용 가능한 라이브러리를 소개하고자 합니다.
Rigid Body Dynamics Library(RBDL)은 Recursive Newton Euler Algorithm (RNEA),
Composite Rigid Body Algorithm (CRBA), Articulated Body Algorithm (ABA) 을 이용하여 kinematics와 dynamics를 계산 합니다.

여기서는, 윈도우에서 RBDL을 이용하여 visual studio 2019에서 예제를 실행시켜 보는 것까지 해보고자 합니다.

---
## [RBDL 다운로드](https://github.com/rbdl/rbdl)

### RBDL 다운로드
[*RBDL*](https://github.com/rbdl/rbdl)은 깃헙에서 다운 가능합니다. [*문서*](https://rbdl.github.io/)를 통해 코드 및 설명을 확인할 수도 있습니다.


### Cmake 으로 라이브러리 얻기
[*윈도우에서 CMake*](http://www.cmake.org) 하기 위해 윈도우즈용 Cmake을 다운받아 설치합니다. 설치하면 Cmake-gui가 설치된 것을 볼 수 있습니다. 실행하면 gui를 통해 cmake을 간단히 실행 가능합니다. 

cmake list 파일이 있는 경로를 설정하고, 빌드 결과를 얻기 위한 폴더를 별도로 설정한 후, 사진과 같이 실행하면 간단히 소스를 빌드할 수 있습니다.

![](/assets/img/docs/2021-09/2021-09-07-RBDL-Cmake.PNG)



### static library 얻기
Cmake을 한 후, 빌드된 폴더를 보면 vs solution이 생성된 것을 확인할 수 있으며, 개발환경에 맞춰서 솔루션을 실행합니다. RBDL-static 프로젝트를 시작 프로젝트로 설정하고 솔루션 구성(release) 및 플랫폼 설정(x64) 후 빌드 합니다. 빌드에 성공하면 솔루션 폴더에 Release 폴더가 생성된 것을 확인할 수 있으며 폴더 안에 static library들이 생성된 것을 확인할 수 있습니다.

![](/assets/img/docs/2021-09/2021-09-07-RBDL-library.PNG)


### Implementation to visual studio
0. Win32 Console Application 로 새 프로젝트 생성 후, 

1. Property에 C/C++->additional include directories에 (PATH_TO_RBDL)/include 헤더 추가
2. Property에 Linker->additional Library directories에 additional dependency (librbdl.lib) 추가

3. Main 함수에 example code 추가

```
#include "stdafx.h"
#include <iostream>
#include "./rbdl/rbdl.h"

using namespace RigidBodyDynamics;
using namespace RigidBodyDynamics::Math;

int main(int argc, char* argv[]) {

	rbdl_check_api_version(RBDL_API_VERSION);

	Model* model = NULL;

	unsigned int body_a_id, body_b_id, body_c_id;
	Body body_a, body_b, body_c;
	Joint joint_a, joint_b, joint_c;

	model = new Model();

	model->gravity = Vector3d(0., -9.81, 0.);
	body_a = Body(1., Vector3d(0.5, 0., 0.0), Vector3d(1., 1., 1.));
	joint_a = Joint(
		JointTypeRevolute,
		Vector3d(0., 0., 1.)
		);

	body_a_id = model->AddBody(0, Xtrans(Vector3d(0., 0., 0.)), joint_a, body_a);

	body_b = Body(1., Vector3d(0., 0.5, 0.), Vector3d(1., 1., 1.));
	joint_b = Joint(
		JointTypeRevolute,
		Vector3d(0., 0., 1.)
		);

	body_b_id = model->AddBody(body_a_id, Xtrans(Vector3d(1., 0., 0.)), joint_b, body_b);

	body_c = Body(0., Vector3d(0.5, 0., 0.), Vector3d(1., 1., 1.));
	joint_c = Joint(
		JointTypeRevolute,
		Vector3d(0., 0., 1.)
		);

	body_c_id = model->AddBody(body_b_id, Xtrans(Vector3d(0., 1., 0.)), joint_c, body_c);

	VectorNd Q = VectorNd::Zero(model->dof_count);
	VectorNd QDot = VectorNd::Zero(model->dof_count);
	VectorNd Tau = VectorNd::Zero(model->dof_count);
	VectorNd QDDot = VectorNd::Zero(model->dof_count);

	ForwardDynamics(*model, Q, QDot, Tau, QDDot);

	std::cout << QDDot.transpose() << std::endl;

	delete model;


	return 0;
}


```
예제를 실행하면 다음의 결과를 확인할 수 있다.

![](/assets/img/docs/2021-09/2021-09-07-RBDL-example1.PNG)

