# Human-Level Control through Deep Reinforcement Learning

원본 저장소의 README를 읽고싶으시다면 다음을 참고하세요.

https://github.com/devsisters/DQN-tensorflow/blob/master/README.md

  

## 결과

![Break_out](https://user-images.githubusercontent.com/57663398/84415607-f6206980-ac4d-11ea-8577-1385f4919b83.gif) 

  

공을 튀기는 바가 왼쪽에 계속 있으려는 모습을 볼수 있는데, 깨야할 벽의 모서리 부분을 공략하여 뒤 벽에 넘기가 위해서 인것 같다.

 



## 프로젝트 목적

Deep Q-Network를 사용하여 아타리 게임을 학습하여 클리어합니다.

  

  

## 프로젝트 Github 구조도

![img](https://lh5.googleusercontent.com/cAo4RbDPU6JbwPbB_BX-emKyNpS9MSN2VAMsFFbacyK8HebHZM8eD_ttXW9GK8lTujscg8_6n35rw1Mxew7p-p9y6sYDPRXe0fG3i3_TY8JXLfStnOeMNAFdmLHci-pDr5P9hIjM)

  국내 repository 40위인 Devsisters Corp의 DQN-tensorflow를 사용하여 아타리 게임을 학습하여 강화학습이 이루어지는지 확인합니다. 또한, 해당 repository를 개선하여 commit합니다.

  해당 devsisters/DQN-tensorflow repository는Playing Atari with Deep Reinforcement Learning (Mnih et al, 2013) 논문을 파이썬과 tensorflow를 사용하여 구현한 것입니다. Agent, Environment, History를 포함하여 replay_memory 등 논문을 최대한 반영하여 사용하였으며, tensorboard를 통하여 학습의 결과를 확인할 수 있습니다.

   

  

## 변경내용

* python2.7 --> python3.7 코드로 변경( 호환되는건 변경하지 않음)
* linux version --> window 10 version
* 디테일적인 부분들은 아래의 변경기록을 참고하시기 바랍니다.
* tensorflow 1.15.0 사용







##  변경 기록

### 1주차

5.11 - fork, clone하고, window 10, Pyhon 3.6 환경으로 바꾸어서 실행되는지 확인
Linux에 맞게 작성된 파이썬 코드로써, Windows 10버전에 맞게 수정하였습니다. 또한, Python 2.7 버전에 작성된 코드를 Python 3.6으로 맞추었습니다.

xrange -> range수정

self._saver = tf.train.Saver(list(self.w.values()) + [self.step_op], max_to_keep=30) (line 336 in agent.py)
![img](https://lh3.googleusercontent.com/EItnKIN4HmfC5-pEravydtSWgy2fU-J81XBave047psUa2R8qisVE4mQtOlAIjd43CJ0DDDYCbvlc1Fm74io5Mx1Qs0ATp1dr22bpk4rcHufFc9nIbSi3m3ldEXAu4IjkIVVIL8O)

정상적으로 학습되며 loss도 줄고 average_q 값도 조금씩 상승하는 것을 볼 수 있습니다.
\# step을 진행하기전에는 반드시 reset()함수가 먼저 실행되어야 합니다.

self.env.env.reset()도 집어 넣음
5.12 - agent.py, history.py 분석 및 이해
코드마다 주석을 달면서 이해하고, 코드 구성을 파악하였습니다.그리고 계속 학습을 진행하였습니다.
5.13 - 학습 중
24시간 이상 한것 같지만 0.0499, 0.083015, 5.032928, 3.5873, 20.0000 에 멈춰있음avg_q 가 5를 겨우 넘었다![img](https://lh6.googleusercontent.com/dHQ3lPEmMpIfk_OZiKxPajoB5IPuuN8PlxTGWtM2yySaYcqFiSCHnf6rwCXSOQhlJQd5kGb3CTlJCAN4xBjIsVsW9OhPWfd0rxYba3xFYyQbPu-gM8htWAbAePkA7JLy0z-r8byp)

해당 학습에 문제가 발생한것 같아 수정하여 다시 처음부터 학습하였습니다.

5.14 -학습 중
optimizer 수정커널 xvier로 초기화dueling truedouble_q true
5.16아무리 학습해도 max_ep_r이 최대 30에서 증가하지 않음 - 오류로 판단하고 원인 찾기
5.17환경 이상 수정--env_name=BreakoutNoFrameskip-v0 으로 바꿈, gym 라이브러리에서 자체적으로 Breakout-v0은 framskip=4를 해줌. 그래서 프레임 skip을 중복 적용시 16 frame마다 하나의 이미지를 가져오게 되어 상황 판단에 많은 정보를 주지 못하였습니다. 

### 2주차
5.20정상적으로 학습중에 있습니다.![img](https://lh3.googleusercontent.com/UJcMJlyEs1IXaR7jbW0vdlS1TH9hkVWZbG9ZxXy_4E2wswb8A4nu9lw5vXv-35_Z_InEDEdkQvImh5xLT_th39TTjOtKcaaJuMveVGW6KtHexJwDrR0IO8J2-054ArQ09DJjQlvt)
실행 환경
Windows 10

### 3주차

5.26
![img](https://lh4.googleusercontent.com/qm4IX9vhbwuT84e3mT0WboQOmg4zhViKdtqzX1RYyVD3KRXNQ_bbXaFL5Rnc-FPGX8SA0EvqfNV36bfEUwTWL0YD_nuEgEdTJozhj_xISUPEdxv1cxPYSo5mQ8-623N--0tmI0Vm)
Python 3.6Tensorflow-gpu 1.15.0
5.27
![img](https://lh3.googleusercontent.com/M48irYk-ejlHeY3CVmK5K-bYHHTrU_JqlSCdsc_SYWD2ctY4r8tmmpcvUToiU5I4Wt8RiAr1tugOkwRHNZ0xaUrsd55JrZXsXKOZN8UuNIXWyKOTLfr3xv5Wz6-Q4vq3foK9h3ei)

70% 이상 학습하면서 성능이 떨어지는 현상이 보입니다. q 값은 증가하지만 avg_loss는 증가하며 optimizer에 대한 성능때문에 이러한 상황이 발생한것으로 생각됩니다.현재 devsisters/DQN-tensorflow는 RMSProp optimizer를 기본으로 사용하고 있습니다. 그래서 adam, Radam optimizer를 사용하여 앞으로 성능을 끌어올릴 예정입니다.

![img](https://lh5.googleusercontent.com/adiJ4c1BIp082csdCHdxDwSLABJbaiV3wBOItAYRfy9uBKw-6Yew--saneOsFhR8FDka9sR6Q9fXVFuT0ClPuYFMyBCx8SStwcbi5LZF8TiNW8jNlMJi0jlpS1XyECCYZQAoBmR0)

위의 중간 결과를 참고하여 base line 실험 중단합니다. 그리고 optimizer, double DQN, dueling을 적용합니다. 개선 후 빠르게 실험결과를 볼 수 있게 학습 시간을 단축시키고 학습 효율을 증가시킵니다.