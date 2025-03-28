---
description: >-
  Tag et al. / Continuous Alertness Assessments; Using EOG Glasses to
  Unobtrusively Monitor Fatigue Levels In-The-Wild / CHI-2019 conference-year
---

# CAA

[소개할 연구](https://doi.org/10.1145/3290605.3300694)는 2019년에 CHI (Conference on Human Factors in Computing Systems)에서 발표되었으며,\
하루 동안의 눈 깜빡임 빈도를 EOG (Electrooculography)로 측정함으로써 간편하게 대상자의 피로도 수준인 **`Continuous Alertness Assessments`** 를 모니터링하는 기술을 소개하고자 합니다.\
_keyword: Cognition-Aware Systems, Circadian Computing, Fatigue, Eye Blink, Electrooculography_

\


## **1. Problem Definition**

> 피로 수준 모니터링 시스템의 필요성

사람의 집중력과 업무 능력은 24시간 일주기와 관련이 깊기 때문에, 일주기 리듬이 생물학적 사이클에서 벗어날 경우 심각한 건강 문제를 초래할 수 있습니다.\
예를 들어 오랫동안 쉬지 않고 업무를 지속할 경우 실수와 사고를 일으킬 가능성이 증가하며, 이는 교대근무와 장기간 근무가 필요한 조종사, 의료인들에게서 흔히 나타납니다.

수면부족 및 피로감은 업무 효율에 악영향을 미치며, 추론능력, 작업기억 등의 정신기능에도 영향을 줍니다.\
피로감을 스스로 인지하기 어렵기 때문에 **피로 수준을 감지하고 예측할 수 있는 자동화된 시스템** 개발이 필요합니다.

본 리뷰에서는 상용화된 안경을 활용하여 피로 수준을 모니터링하는, EOG 센서 기반의 **`Continuous Alertness Assessments`** 시스템을 소개하려 합니다.

![J!NS MEME glasses](https://github.com/bananaorangel/awesome-reviews-kaist/blob/2022-Spring/.gitbook/2022-spring-assets/Haehyunlee\_2/J!NS%20MEME.png?raw=true)

**`Continuous Alertness Assessments`** 시스템은 아래의 장점을 갖고 있습니다:

* 피로 수준에 따른 업무 순서 배치로 효율성 증대 가능
* 사용자에게 휴식이나 수면이 필요한 경우 알림 생성

\


## **2. Motivation**

> 불편하지 않고 정확한, EOG 안경 기반의 피로 수준 모니터링 시스템 개발

### **2.1 피로 수준을 측정하는 기존 연구들 및 한계점**

\


\[1] 전통적인 방식의 피로 수준 측정 방법

* [Kleitman](https://doi.org/10.1152/ajplegacy.1923.66.1.67)는 항문체온계를 사용하여 신체 내부의 온도를 측정하여 의식의 변화를 측정하였습니다.
* [Hofstra and Weerd](https://doi.org/10.1016/j.yebeh.2008.06.002)는 수면 중인 사람을 대상으로 뇌파, 심전도 등을 측정하여 피로 수준을 파악하는 수면다원검사를 소개하였습니다.

![traditional](https://github.com/bananaorangel/awesome-reviews-kaist/blob/2022-Spring/.gitbook/2022-spring-assets/Haehyunlee\_2/traditional.png?raw=true)

\


\[2] 스마트폰을 활용한 피로 수준 측정 방법

* [Abdullah et al.](https://doi.org/10.1145/2971648.2971712)은 스마트폰을 사용하여 사용자의 Continuous Alertness를 모니터링하는 시스템을 개발하였습니다.
* [Dingler et al.](https://doi.org/10.1145/2968219.2968565)은 스마트폰 기반의 집중력 수준 감시 시스템을 개발하여 생산 효율성을 증대하였습니다.

![smart-fatigue](https://github.com/bananaorangel/awesome-reviews-kaist/blob/2022-Spring/.gitbook/2022-spring-assets/Haehyunlee\_2/smartphone-fatigue.png?raw=true)

\


피로 수준을 측정한 기존 연구들은 대부분 한계점을 갖고 있었습니다.

* 전통적인 방식의 피로 수준 측정 방법은 사용자에게 불쾌감을 주거나 번거로운 장치를 착용해야 했습니다.
* 스마트폰을 활용한 방법도 스마트폰을 사용할 때만 데이터를 측정할 수 있다는 단점이 있거나, 주의가 스마트폰에 집중되어 실제 하고 있는 업무에 대한 집중도가 떨어지게 됩니다.

이러한 단점을 보완하고 실제 측정값의 정확도를 높이기 위해, 안구 움직임을 측정 함으로서 불필요하게 관심을 끌지 않으면서 지속적으로 모니터링을 할 수 있는 시스템의 개발이 필요합니다.

\


### **2.2 기존 한계점을 보완한 EOG 안경 기반의 피로 수준 측정 시스템**

이러한 Research Gap을 줄이기 위해 본 연구에서는 EOG 센서가 달린 안경을 활용하여 피로 수준을 측정하는 **`Continuous Alertness Assessments`** 를 개발하였습니다.

EOG를 통해 얻을 수 있는 안구 운동, 눈깜박임 데이터를 활용하여 피로 수준에 대한 모니터링을 가능하게 해줍니다.

> 개발된 피로 수준 측정 시스템은 아래의 이점을 갖고 있습니다:

* 센서를 번거로운 방법으로 부착해야 하는 전통적인 방식과 달리, EOG 센서를 안경에 부착함으로써 편안한 방식으로 피로 수준을 측정하는 것이 가능합니다.
* 주간/야간, 실내/실외 등 빛의 변화에 관계 없이 피로 수준을 측정할 수 있습니다

> 본 연구는 아래의 3가지 contribution 요소를 갖고 있습니다:

* 2주 간의 실증 실험을 통해 피로 수준과 눈깜박임 횟수 사이에 관련성이 있음을 제시함
* EOG 센서 데이터와 그에 따른 눈깜박임 빈도를 활용하여 피로도 수준 변화를 예측하는 모델을 제시함
* 16명의 피실험자가 시행한 EOG 데이터의 dataset을 제시함

\


## **3. Method**

이 연구의 목적은, 하루 동안의 EOG 데이터를 지속적으로 측정함으로서 의식 수준의 변화와 눈깜빡임 빈도 사이의 관계를 밝히는 것입니다.\
따라서, 먼저 일상생활에서의 피로도 변화를 자유롭게 측정 및 기록하는 방식을 dataset에 사용하였습니다.

이 연구에서는 피로의 개념을 [Van Dongen and Dinges](https://doi.org/10.1002/ppul.1065)가 정의한, ’실행을 지속할 수 있는 욕구나 능력을 잃어버리는 것’으로 정의하였습니다.\
피로 수준의 증가는 각성 수준과 인지 기능의 감소와 같은 의미이며, 반응속도(Reaction Time)의 변화를 측정하는 것으로도 알 수 있습니다.

피로 수준을 측정하기 위해 본 연구에서는 모바일 Tookit을 만들었으며, 이를 통해 피실험자들의 반응속도와 각성 수준을 동시에 측정하였습니다.\
더불어, Toolkit은 피실험자들의 수면 패턴, 자가보고한 졸림 수준, 낮잠과 카페인 사용량에 대한 정보도 수집하였습니다.

### **3.1 EOG 안경 기반의 피로 수준 모니터링 시스템**

피로 수준을 모니터링하기 위한 EOG 안경 기반의 시스템을 개발하였습니다.

* 안경은 [J!NS MEME glasses](https://jinsmeme.com/en/)를 사용하였습니다.
  * 코 주변에 EOG 센서를 장착하여 안구 움직임, 눈깜박임을 측정하였습니다.
  * 안경테에 Accelerator, Gyroscope을 장착하여 머리의 움직임과 자세를 측정하였습니다.
* 데이터 전송은 Bluetooth LE 모듈을 통해 수행되었습니다.

![figure1](https://github.com/bananaorangel/awesome-reviews-kaist/blob/2022-Spring/.gitbook/2022-spring-assets/Haehyunlee\_2/figure1.png?raw=true)

### **3.2 피로 수준 측정 Toolkit**

본 연구에서는 데이터 수집을 위해 [Dinger et al.](https://doi.org/10.1145)이 도입한 모바일 도구 Toolkit을 사용하여 App을 만들었습니다.\
App은 Android 기반으로 각성 수준 및 피로 수준을 아래와 같이 3가지 방법으로 측정할 수 있습니다.

![toolkit](https://github.com/bananaorangel/awesome-reviews-kaist/blob/2022-Spring/.gitbook/2022-spring-assets/Haehyunlee\_2/toolkit.png?raw=true)

3가지 방법은 순서대로 Psychomotor Vigilance Task (PVT), Go/No-Go task, Multiple Object Tracking task입니다.

PVT가 피로 수준을 측정하는데 가장 정확하고 데이터의 양도 많으므로, 본 연구에서는 PVT 방법을 피로 수준을 모니터링하는데 활용하였습니다.

\


## **4. Experiment**

### **4.1 Experiment setup**

#### 4.1.1 **Dataset**

> 사람을 대상으로 한 실험에서 수집된 PVT 수행 결과 및 EOG센서 데이터

본 연구에서는 피로 수준을 평가하기 위한 실증실험을 16명의 피실험자를 대상으로 14일동안 수행하였습니다.

16명의 피실험자(남성 9명, 여성 7명)을 대상으로 하였으며 평균 나이는 28세(SD=5.03)이었습니다.\
모든 피실험자들은 (교정)시력이 정상이었으며, 임상적으로 특별한 질환을 갖고 있지 않았으며, 연구 도중 피로를 유발하는 약물은 복용하고 있지 않았습니다.

각 피실험자들은 14일간 하루에 평균 4개의 설문에 응답하였으며, 1인당 평균 65개의 PVT 평가를 수행하였으며(최소 24개-115개), 총 1,047개의 PVT 수행 결과로 반응 속도가 dataset으로 수집되었습니다.

또한 피실험자들이 안경을 착용한 동안 EOG데이터가 수집되었으며, 총 2,860시간의 EOG raw data가 수집되었습니다. 하루에 한 사람이 16시간 깨어 있는다고 가정하였을 때, 이 결과는 한 사람당 하루 평균 약 8.5시간 동안 EOG를 녹화한 것과 같습니다.

반응 시간과 눈 깜빡임 사이의 관계를 측정하기 위해, 각각의 평가가 수행되기 바로 10분 전 기간 동안의 EOG data를 이용하였습니다.\
이 시간대를 사용한 이유는, PVT를 수행 함으로서 발생할 수 있는 영향을 피하기 위해서였습니다.

#### 4.1.2 **Experiment procedure**

실험은 16명의 피실험자를 대상으로 14일동안 진행되었습니다.

피실험자들은 깨어 있는 동안 하루 종일 J!NS Meme을 착용하였으며, 아침에 안경을 착용하여 App에 접속하고, 매일 저녁에 연결을 해제하였습니다.\
App에는 총 3가지 다른 종류의 설문조사가 제공되었다.

![figure2](https://github.com/bananaorangel/awesome-reviews-kaist/blob/2022-Spring/.gitbook/2022-spring-assets/Haehyunlee\_2/figure2.png?raw=true)

안경을 착용하는 동안 피실험자들은 2시간(±20분)마다 PVT를 수행하였습니다.\
시각 자극이 시작됨과 동시에 2-8초 지연 간격을 두고 반응 속도를 측정하였으며, 20-120초로 이루어진 task를 수행하였습니다.

반응 속도가 짧거나 길어지면 피로도 수준이 높은 것으로 분류되었으며, 이 기준은 너무 빠르거나(100ms보다 빠름) 너무 느린(3000ms) 반응으로 정의되었습니다.

이를 통해 하루 종일의 피로도를 지속적으로 측정하였습니다.

매일 아침마다 첫 번째 설문으로 참가자들은 일어난 시간, 지난 밤의 총 수면시간, 수면의 질(나쁨 1\~매우 좋음 5)을 응답하였습니다.\
그 이후 참가자가 앱에 접속할 때마다 지난 번 설문 이후로 낮잠을 잤는지, 또는 카페인 음료를 마셨는지를 질문하였습니다.\
또한, 참가자들에게 지금 어느 정도 수준으로 졸린지를 1 (극도로 각성)에서 9 (극도로 졸림) 범위로 대답하도록 하였습니다.

또한 수면에 방해가 되지 않도록 하기 위해서, 사용자가 지정한 시간 동안은 알림을 보내지 않는 일시정지 기능을 도입하였습니다.

#### 4.1.3 **Evaluation Metric**

EOG안경을 통한 눈깜박임 측정 알고리즘과 그 타당성 검증, 그리고 데이터의 evaluation에 대하여 서술합니다.

\[1] Blink Detection\
본 연구에서는 한 사람의 EOG 데이터를 두 가지 방식으로 측정하였습니다. 먼저 J!NS Meme 프레임에 두 개의 [Pupil Labs eyetracker](https://doi.org/10.1145/2638728.2641695) cameras 를 설치하였는데, 한 쪽 다리에 하나씩을 설치해서 카메라가 착용자의 눈을 조준하도록 하였습니다.\
이를 통해 착용자가 복잡한 장비나 센서를 몸에 착용하지 않고도 안경에 있는 센서를 통해 EOG 신호와 안구의 운동을 동시에 측정할 수 있었습니다.\
단, 눈 깜빡임은 자연적인 상태에서도 변화가 큰 편이므로 최소 5분 이상 눈깜빡임 횟수를 측정하였습니다.

눈깜박임 횟수를 추정하기 위해서, J!NS Meme으로 수집한 EOG 데이터의 수직 성분 vertical components 을 peak detection algorithm에 적용시켰습니다. 장치의 전송 속도 transmission rate는 50 Hz로, EOG sampling rate인 100 Hz의 절반 수준이었으므로, original vertical value인 EOGV를 EOGV 1 와 EOGV 2 패키지로 나누었습니다.

\[2] Validation\
눈깜박임 감지 알고리즘을 입증하고 눈 깜빡임 감지의 역치 값을 확인하기 위해서, 측정된 눈깜빡임 횟수 및 EOG data sets를 비디오 녹화를 통해 직접 카운트한 눈 깜빡임 횟수와 비교하여 **오차 범위**로 evaluate 하였습니다.

eye tracking cameras의 비디오로 녹화한 눈 깜빡임은 양쪽 눈이 자연스레 감긴 뒤 1초 이상 지속되지 않는 경우로 정의하였습니다.

\[3] Correlation Analysis\
눈깜박임 감지 알고리즘을 입증된 역치값과 window size settings로 실행한 다음, 원자료값 raw data에 선형혼합모형 linear mixed model을 적용하였습니다.

이 때 PVT를 시행함에 따라 얻은 RT 값과 BF를 종속변인 dependent variable으로 사용하였습니다.\
참가자들은 무선요인 random factor로 간주하였습니다.

본 연구에서는 PVT 평가가 시행된 시간을 기록하고, 각 평가가 시행되기 전 선행된 10분 동안의 EOG data를 추출하였습니다.

**`Holm-Bonferroni method`** 를 이용해 다중분석 multiple comparisons를 시행하였습니다.

참고로, 본 연구에서는 시스템의 성능 평가 시 다른 baseline과의 비교를 수행하지 않았습니다.

### **4.2 Result**

\[1] Blink Detection\
vertical EOG 값인 EOGV 1과 EOGV 2 값을 묶은 다음 데이터의 노이즈 값을 제거하기 위해 저역 필터low pass filter (Butterworth filter)를 사용하였습니다. 눈깜빡임이 a peak followed by a dip (한번 튀었다가 한번 빠지는 것: -^--∨- 모양)으로 특징지어지는 만큼, 알고리즘은 눈깜빡임을 측정하기 위해 두 개의 변수인 th\_right 과 th\_up\_to\_down 을 사용하였습니다.

th\_right 는 양의 피크의 높이 the height of the positive peak를 묘사하며, th\_up\_to\_down 는 두 피크 사이의 수직 거리 vertical distance를 묘사합니다(즉 첫 번째 피크의 가장 높은 점과 두 번째 피크의 가장 낮은 점 사이의 거리).

눈깜박임을 완전히 묘사하기 위해서는 세 가지 조건이 충족되어야 합니다.

* 첫 번째로, 첫 번째 피크의 높이가 th\_r보다 커야 한다.
* 두 번째로, 수직 거리 the vertical distance (두 피크 사이의 y-values 차이)가 th\_u\_d보다 커야 한다.
* 세 번째로, 아래 그림에서처럼 더 큰 크기의 peak가 먼저 발생한 뒤 더 작은 lower peak가 뒤따라야 한다.

![figure5](https://github.com/bananaorangel/awesome-reviews-kaist/blob/2022-Spring/.gitbook/2022-spring-assets/Haehyunlee\_2/figure5.png?raw=true)

\[2] Validation\
직접 카운트한 5분간 눈 깜빡임 횟수는 휴식시 54회, 보행시 84회였습니다.\
가장 정확한 눈깜빡임 감지의 th\_r 은 0.8, th\_u\_d는 2.0. 이었으며, 가장 정확한 sliding window size는 0.34초로 측정되었습니다.

저자들의 알고리즘은 휴식 시 61 blinks/5min (12.2 blinks/min), 보행시 81 blinks/5min (16.2 blinks/min)으로 깜빡임 횟수를 감지하였고, 오차범위는 휴식시 +12.5% (+7 blinks), 보행시 -3.7% (3 blinks less)였습니다.

\[3] Correlation Analysis\
분석된 623개의 EOG 데이터에서 평균 눈깜빡임 횟수는 11.4 blinks/min (SD = 12.7)였습니다.

분석 결과 BF와 RT값의 변화는 (χ2(1) = 4.32,p = 0.001) 로서, RT는 약 1.64 milliseconds ±0.38 (standard error), BF는 약 +1 blink/min 증가하는 것으로 나타났습니다.

Holm-Bonferroni method를 이용한 다중분석 multiple comparisons를 시행 결과, 반응 속도의 증가로 표현되는 피로도를 측정하는 데 눈깜박임을 indicator로 사용할 수 있었습니다.

![figure6](https://github.com/bananaorangel/awesome-reviews-kaist/blob/2022-Spring/.gitbook/2022-spring-assets/Haehyunlee\_2/figure6.png?raw=true)

\


## **5. Conclusion**

> Summarize the Papaer

* 본 연구에서는 상용화된 안경인 `J!NS MEME glasses`에 EOG센서를 부착하여 피로 수준을 모니터링하는, 착용하기 쉬운 시스템을 개발하였습니다.
* 개발된 시스템은 일상 생활 도중의 눈 깜박임 빈도를 측정함으로써 하루 동안의 피로 수준을 확인할 수 있습니다.
* 본 연구의 의의는, 더 이상 복잡한 장비를 착용할 필요 없이 상용화된 안경을 착용하는 것만으로 일상생활에서의 피로 수준을 측정하는 시스템을 개발하였다는 것에 있습니다.

> My opinion, Take home message

* Human-Computer Interaction (HCI) 분야에서 **안경을 사용하여 신체 및 인지 데이터를 수집하는 연구**들이 활발하게 이뤄지고 있습니다. 기존에 리뷰했던 [FaceSight](https://dsail.gitbook.io/isyse-review/paper-review/2022-spring-paper-review/chi-2021-facesight) 연구도 안경을 활용하여 사용자들의 제스처 데이터를 수집한 바 있습니다. ![FaceSight](https://github.com/bananaorangel/awesome-reviews-kaist/raw/2022-Spring/.gitbook/2022-spring-assets/Haehyunlee\_1/fig1\_facesight.PNG?raw=true)
* 안경을 활용하여 데이터를 수집하는 경우, 센서들을 신체에 직접 부착해야 하는 불편함이나 번거로움이 적으며 **일상생활에서 사용하기 편리**합니다.\
  이러한 장점들을 기반으로 앞으로도 HCI 분야에서 안경을 사용한 연구들이 활발히 이뤄질 것으로 보입니다.
* 다만 안경 기반의 연구들의 공통적인 문제점인, **착용 위치에 따른 데이터 노이즈 문제**가 고려되어야 할 것입니다. 사용자가 안경을 평소와 다른 위치에 착용할 경우 안경에서 수집된 데이터에 노이즈가 발생하여 잘못된 알람을 피드백하게될 수 있습니다.\
  따라서 안경 착용 위치가 바뀌더라도 일관적인 결과를 도출할 수 있도록 하는 normalize방법이 중요할 것입니다.
* 여러 기술들이 개발되고 있지만, **신기술에 취약한 계층들(예, 노인, 장애인 등)** 도 쉽고 편리하게 사용할 수 있도록 이들을 대상으로 한 연구도 활발하게 이뤄져야 할 것으로 보입니다. 대부분의 실험들이 젊은 사람을 대상으로 이뤄지지만, 추후에는 취약계층을 대상으로 한 실험도 증가한다면 다양한 사람들에게 신기술을 적용할 수 있을 것입니다.

\


***

## **Author Information**

* Haehyun Lee
  * Affiliation : PhD course in KAIST KSE program
  * Research Topic : Human-Computer Interaction, Human Factors in Nuclear Power Plant
  * Contact email : haehyun\_lee@naver.com

\


## **6. Reference & Additional materials**

* 논문 원문 : [Continuous Alertness Assessments](https://doi.org/10.1145/3290605.3300694)
* Github Implementation
  * [Fatigue\_EOG\_Raw](https://github.com/tagbenja/Fatigue\_EOG\_Raw)
* Reference
  * 본 연구에서 활용한 안경 : [J!NS MEME glasses](https://jinsmeme.com/en/), 모바일 toolkit : [Dingler](https://doi.org/10.1145), 카메라 : [Pupil Labs eyetracker](https://doi.org/10.1145/2638728.2641695)
  * 피로 수준 정의 : [Van Dongen and Dinges](https://doi.org/10.1002/ppul.1065)
  * 피로 수준 측정 시스템 : [Kleitman](https://doi.org/10.1152/ajplegacy.1923.66.1.67), [Hofstra and Weerd](https://doi.org/10.1016/j.yebeh.2008.06.002), [Abdullah et al.](https://doi.org/10.1145/2971648.2971712)
