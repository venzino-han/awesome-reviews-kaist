---
description : Xiangning Chen et al., / When Vision Transformer Outperform ResNet Without Pre-Training Or Strong Data Augmentation / ICLR-2022  
---

# **When Vision Transformer Outperform ResNet Without Pre-Training Or Strong Data Augmentation** 

## **1. Problem Definition**  


![fig1](https://erratic-tailor-f01.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa054ce54-ccde-4c75-a438-277e63bcc76a%2FUntitled.png?table=block\&id=6b4ec770-3591-48e1-b817-9c3e62dcdea5\&spaceId=ad2a71b5-1b0d-4734-bbc4-60a807442e5d\&width=2000\&userId=\&cache=v2)

* Convolution-free한 ViT와 MLPs만 사용한 모델의 경우 inductive bias의 부재로 인해 매우 많은 데이터를 학습시키거나 강력한 augmentation 전략을 사용해 이를 극복하고자 하였다.
* Transformer가 NLP분야에 소개된 이후 vision에서의 활용이 있었고 hand-wired feature와 inductive bias가 없이 일반화 가능한 모델을 만들기 위해 상당한 양의 데이터를 투입시키는 방법이 활용되었다. 예를들어 pre-train ViT는 google의 private dataset으로 3억장의 labeled image를 학습하였다
* ViT와 Mixer는 ResNet에 비해 기하적으로 아주 sharpe한 loss landsacpe를 가지고 있음을 알 수 있다. 이것은 학습-일반화 성능의 괴리가 생기는 원인으로 지목된다

## **2. Motivation** 
* <2. Motivation>에서는 motivation이 된 아이디어와 그 근거를 객관적으로 제시한 실험들을 살펴보겠습니다.

### **2.0 Motivation**

* 학습된 landscape는 상당히 local minima에 sharpe한 모습을 보였지만 최근 제시된 sharpness-aware optimizer(SAM)을 활용한 결과 ViT와 MLP Mixer는 지도, 비지도, 적대적, 전이 등 다양한 학습 전략에서 상당한 성능 향상이 있음을 확인했다. Scratch부터 학습된다면 비슷한 size의 ViT와 ResNet에서 ViT가 ResNet의 성능을 뛰어넘을 수 있음을 확인했다
* SGD,Adam과같은 first-order optimizer는 training error를 낮추는데에는 좋은 알고리즘이다. 하지만 이것은 더 고차원적인 목표인 주변의 loss도 낮게 만듦에는 신경쓰지 않는다. 따라서 최근의 연구인 SAM에서 이런 문제의 해결을 찾게 되었다. SAM optimizer는 single poing에서의 loss 최저보다 single poing 주변 모두가 loss가 낮아지도록 설계되었다. 이렇게 향상된 일반화 성능은 강력한 augmentation과 pre-training과정없이 ViT, MLPs가 ResNet을 뛰어넘을 수 있게 하였다
* SAM을 사용한 후 model의 (특히 첫 몇 개의 레이어에서) [Hessian 고윳값](https://angeloyeo.github.io/2020/06/17/Hessian.html)이 작아지는 것을 확인했다(=볼록한 정도가 감소했다=sharpeness하지 않아졌다). Weight norm은 이것을 커지게 만들었고 이는 일반화에 자주 쓰이는 weight decay가 regularization에 크게 도움되지 않았을지 모른다는 가정을 가능하게 한다. SAM과 강력한 augmentation과의 비슷한 특성들을 살펴볼 것이다


### **2.1 ViTs and MLP-Mixers converge to extremely sharp local minima**

![fig2](https://erratic-tailor-f01.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff9de0b6f-c4d6-476e-9bd1-17d102d2b668%2FUntitled.png?table=block\&id=cf50b7ae-7730-47e2-a373-4ec7ae48f5bc\&spaceId=ad2a71b5-1b0d-4734-bbc4-60a807442e5d\&width=2000\&userId=\&cache=v2)

* Figure1 (a) vs (b),(c) : ResNet에 비해서 conv-free한 방법은 loss의 landscape가 sharper함을 확인할 수 있다. Table1을 보면 Hessian 행렬에서 얻은 고윳값 중 제일 큰 ![](https://latex.codecogs.com/gif.latex?%5Clambda\_%7Bmax%7D)을 확인할 수 있다. ![](https://latex.codecogs.com/gif.latex?%5Clambda\_%7Bmax%7D)는 landscape의 최대(최악) 곡률이다. ResNet과 비교하면 ViT와 특히, Mixer가 상당히 높다는 것을 알 수 있다


### **2.2 Small training errors**

![fig3](https://erratic-tailor-f01.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F641cd367-d795-449e-851b-301e78ba204e%2FUntitled.png?table=block\&id=32aa79ba-a881-4f93-ae85-5c4fc26c419b\&spaceId=ad2a71b5-1b0d-4734-bbc4-60a807442e5d\&width=2000\&userId=\&cache=v2)

* ViT와 MLP가 극소적인 부분에 수렴한다는 것은 training에 dynamics가 존재한다는 의미이다. Figure2의 좌측과 중앙을 보면 MLP는 ViT보다 낮은 training loss를 가지지만 test에서의 성능은 더 나쁘다. 이는 부분적인 극소에 수렴했다고 분석할 수 있다


### **2.3 ViTs and MLP-Mixers have worse trainability**

* 또한 ViT와 MLP가 poor한 trianability에 노출되어있다는 것을 알 수 있었다. 여기서 trainability란 경사하강법에 의해 네트워크가 최적화되는 현상의 효율성을 말한다. Xiao의 연구에 의하면 Jacobian 행렬(Jacobian 행렬은 1차 미분 행렬) ![](https://latex.codecogs.com/gif.latex?J)에 대하여 neural tangent kernel(NTK) ![](https://latex.codecogs.com/gif.latex?%5CTheta=JJ%5E%5Ctop)로 정의한다. ![](https://latex.codecogs.com/gif.latex?%5CTheta)의 고윳값 ![](https://latex.codecogs.com/gif.latex?%5Clambda\_1%5Cgeq%5Ccdots%5Cgeq%5Clambda\_m)에 대하여 ![](https://latex.codecogs.com/gif.latex?%5Ckappa=%5Clambda\_1/%5Clambda\_m)으로 정의한다. 만약 ![](https://latex.codecogs.com/gif.latex?%5Ckappa)가 지속적으로 변하면 학습이 불안정하다. Table1의 모델에 따른 ![](https://latex.codecogs.com/gif.latex?%5Ckappa)를 비교해 볼 것


## **3. Method**  

* 가장 많이 사용되는 first-order optimizer들은 ![](https://latex.codecogs.com/gif.latex?L\_%7Btrain%7D)만을 낮추게 설계되어 있어서 더 넓은 관점에서의 일반화를 위한 곡률, 상관같은 properties는 고려하지 않는다. 하지만 DNNs는 non-convex하기 때문에 training error는 0에 가깝게 수렴하나 test에서는 그러지 못한다. 심지어 ViT와 MLP는 inductive bias의 부재로 sharp loss landscape를 가지는 현상이 두드러진다


### **3.1 SAM : Overview**

![](https://latex.codecogs.com/gif.latex?\(1\)%5Cspace%5Cmin\_w%5Cmax\_%7B%7C%7C%5Cepsilon%7C%7C\_2%5Cleq%5Crho%7DL\_%7Btrain%7D\(w+%5Cepsilon\))

![](https://latex.codecogs.com/gif.latex?\(2\)%5Cspace%5Cspace%5Chat%7B%5Cepsilon%7D\(w\)=%5Carg%5Cmax\_%7B%7C%7C%5Cepsilon%7C%7C\_2%5Cleq%5Crho%7DL\_%7Btrain%7D\(w\)+%5Cepsilon%5E%7BT%7D%5Cbigtriangledown\_%7Bw%7DL\_%7Btrain%7D\(w\)=%5Crho%5Cbigtriangledown\_%7Bw%7DL\_%7Btrain%7D\(w\)/%7C%7C%5Cbigtriangledown\_%7Bw%7DL\_%7Btrain%7D\(w\)%7C%7C\_2)

* 직관적으로 SAM은 주변의 이웃의 ![](https://latex.codecogs.com/gif.latex?L\_%7Btrain%7D)까지 낮아지게 하는 weight ![](https://latex.codecogs.com/gif.latex?w)를 찾는 알고리즘이다. 여기서 ![](https://latex.codecogs.com/gif.latex?%5Crho)는 얼마나 멀리까지를 고려하는지 고려하는 hyper-parameter이다
* (1)수식은 ![](https://latex.codecogs.com/gif.latex?L\_%7Btrain%7D)을 최소화하는 weight ![](https://latex.codecogs.com/gif.latex?w)를 찾음과 동시에 ![](https://latex.codecogs.com/gif.latex?L\_%7Btrain%7D\(w+%5Cepsilon\))을 최대화하는 ![](https://latex.codecogs.com/gif.latex?%5Cepsilon)을 찾는 것이 목표이다. 이따 ![](https://latex.codecogs.com/gif.latex?%5Cepsilon)은 L-2 norm이 ![](https://latex.codecogs.com/gif.latex?%5Crho)보다 작아야한다. ![](https://latex.codecogs.com/gif.latex?%5Cmin\_w)는 sharp하게 수렴하려하고 ![](https://latex.codecogs.com/gif.latex?%5Cmax\_%7B%7C%7C%5Cepsilon%7C%7C\_2%5Cleq%5Crho%7D)은 ![](https://latex.codecogs.com/gif.latex?w)주변의 Loss를 키워 sharpness를 완화시킨다
* (2)수식을 보면 어떻게 가장 적절한 ![](https://latex.codecogs.com/gif.latex?%5Cepsilon)을 찾는지 알 수 있다. ![](https://latex.codecogs.com/gif.latex?%5Crho%5Cbigtriangledown\_wL\_%7Btrain%7D\(w\)/%7C%7C%5Cbigtriangledown\_wL\_%7Btrain%7D\(w\)%7C%7C\_2)을 보면 ![](https://latex.codecogs.com/gif.latex?%5Cbigtriangledown\_%7Bw%7DL\_%7Btrain%7D\(w\)/%7C%7C%5Cbigtriangledown\_%7Bw%7DL\_%7Btrain%7D\(w\)%7C%5Cmid\_2) 는 L-2 표준화된 ![](https://latex.codecogs.com/gif.latex?w)에 대한 Loss의 gradient다. 즉 Loss의 방향은 그대로 가지고 여기에 ![](https://latex.codecogs.com/gif.latex?%5Crho)를 곱해서 그 방향의 주변만큼 스텝을 옮긴 지점을 ![](https://latex.codecogs.com/gif.latex?%5Chat%5Cepsilon\(w\))로 인정하는 것이다



## **4. Experiment**  

### **Experiment setup**  
* Dataset : ImageNet, Real, V2, ImageNet-R, ImageNet-C (실험마다 제시되어있음)
* baseline : ViT-B, ViT-S, Patch size는 실험 Table에 제시되어있음
* Evaluation Metric : Acc

### **Result**  


### **4.1 Sharpness-Aware Optimization Improves ViTs And MLP-Mizers**

*   ViT의 hyper-parameter의 수정없이 scratch부터 ImageNet을 학습시킴. Inception style processing을 입력단에 추가함. MLP에는 입력단에 강력한 augmentation이 포함되어 있는데 공정한 비교를 위해서 Inception style processing로 대체함. learning에 필요한 hyper-parameter는 greedy search를 통해서 찾았다

    #### Smoother regions around the local minima

    * Figure 1의 (d),(e)처럼 smoother regions에 수렴한 것을 확인할 수 있다. 또한 ![](https://latex.codecogs.com/gif.latex?%5Clambda\_%7Bmax%7D)역시 하락했다

    #### Higher accuracy

    <img src="https://erratic-tailor-f01.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fab1b563b-3024-4bbc-a528-79e2c2237de7%2FUntitled.png?table=block&#x26;id=a100c1a1-b3ac-4ecf-871f-554a8f5a8009&#x26;spaceId=ad2a71b5-1b0d-4734-bbc4-60a807442e5d&#x26;width=2000&#x26;userId=&#x26;cache=v2" alt="fig4" data-size="original">

    #### Better robustness

    * Table2의 ImageNet-R : Train set과 Test set의 class는 같지만 distribution이 다름
    * ImageNet-C : Test set에 강력한 noise가 있음

### **4.2 ViTs Outperform ResNets Without Pre-Training Or Strong Augmentations**

```bash
When trained from scratch on ImageNet with SAM, ViTs outperform ResNets of similar and 
greater sizes (also comparable throughput at inference) regarding both clean accuracy.
```

* 비슷한 #params를 놓고 비교하면 ViT가 ResNet의 성능을 상회했다

### **4.3 Intrinsic Changes After SAM**

#### Smoother loss landscapes for every network component

![fig5](https://erratic-tailor-f01.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcbef3c52-2e74-4e3e-9754-6864ba473e86%2FUntitled.png?table=block\&id=14112506-399f-4de4-9fb7-46c0578c322d\&spaceId=ad2a71b5-1b0d-4734-bbc4-60a807442e5d\&width=2000\&userId=\&cache=v2)

* SAM 이후 곡률의 정도인 ![](https://latex.codecogs.com/gif.latex?%5Clambda\_%7Bmax%7D)가 작아진 것을 모델의 레이어별로 수치화하였다\


![](https://latex.codecogs.com/gif.latex?\(3\)H\_k=\(a\_%7Bk-1%7Da\_%7Bk-1%7D%5ET\)%5Cotimes%5Cmathcal%7BH%7D\_k,%5Cspace%5Cmathcal%7BH%7D\_k=B\_%7Bk%7DW%5E%7BT%7D\_%7Bk+1%7D%5Cmathcal%7BH%7D\_%7Bk+1%7DW\_%7Bk+1%7DB\_%7Bk%7D+D\_%7Bk%7D)

![](https://latex.codecogs.com/gif.latex?\(4\)B\_k=%5Cmathrm%7Bdiag%7D\(f%27\_k\(h\_k\)\),%5Cspace%7B%7DD\_k=%5Cmathrm%7Bdiag%7D\(f%27%27\_k\(h\_k\)%5Cfrac%7B%5Cpartial%7BL%7D%7D%7B%5Cpartial%7Ba\_k%7D%7D\))

![](https://latex.codecogs.com/gif.latex?f\(%5Ccdot\)): activation , GELU

![](https://latex.codecogs.com/gif.latex?W\_k) : k번째 layer의 params

![](https://latex.codecogs.com/gif.latex?h\_k) : ![](https://latex.codecogs.com/gif.latex?W\_%7Bk%7Da\_%7Bk-1%7D), activation을 거치기 전의 k번째 layer의 output

![](https://latex.codecogs.com/gif.latex?a\_k) : ![](https://latex.codecogs.com/gif.latex?f\_k\(h\_k\))

![](https://latex.codecogs.com/gif.latex?%5Cotimes) : Kronecker product

![](https://latex.codecogs.com/gif.latex?%5Cmathcal%7BH%7D\_k) : layer k의 activation을 거치기 전의 Hessian 행렬

![](https://latex.codecogs.com/gif.latex?H\_k) : ![](https://latex.codecogs.com/gif.latex?W\_k)의 Hessian 행렬

* Table 3을 보면 앞단의 레이어가 더 높은 ![](https://latex.codecogs.com/gif.latex?%5Clambda\_%7Bmax%7D)를 가짐을 알 수 있다. 이는 (3) 수식에서 분석가능한데, Hessian norm은 역전파에 의하여 뒤에서 앞으로 누적이 되기 때문이다

#### Greater weight norms

* Table3를 보면 SAM을 사용한 후 ![](https://latex.codecogs.com/gif.latex?%7C%7C%5Ccdot%7C%7C)으로 나타난 norm결과를 보면 오히려 상승한 것을 알 수 있다. 이는 weight decay가 ViT와 MLP를 규제하는데는 그다지 효율적이지 않았음을 뜻한다

#### Sparser active neurons in MLP-Mixers

* 수식 (3)과 (4)를 보면 ![](https://latex.codecogs.com/gif.latex?B\_k)는 ![](https://latex.codecogs.com/gif.latex?f\_k)가 GELU이기 때문에 0보다 큰 값으로 결정된다. GELU의 1차도 함수는 입력 값이 0보다 작다면 급격히 작아진다(사실상0). 따라서 active된 GELU의 수가 Hessian norm으로 직결 되는 것이다
* Figure2의 맨 오른쪽을 보면 SAM을 사용하면 활성화된 뉴런의 수가 더 적어졌음을 알 수 있다. 이것은 image patch가 어떤 반복성을 가지고 있었을지 모른다는 가정을 가능하게 한다(=반복적인 정보가 있으니 sparse해도 감지가 가능했다?)

#### ViT's active neurons are highly sparse

* Transformer의 첫 레이어에서 active neuron(value가 0보다 크다)의 수가 10%정도였고 이는 50%이상이 active한 ResNet과 비교하면 매우 낮은 수치이다
* 따라서 pruning의 여지가 있음을 확인했고 왜 multi modality data가 transformer 구조에 잘 적합되는지도 설명할 수 있다

#### More perceptive attention maps in ViTs

![fig6](https://erratic-tailor-f01.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ffb551857-b152-4011-9f46-976b73ac0f0e%2FUntitled.png?table=block\&id=30a1a98a-9f2e-4a55-95c6-90ab3321b8ca\&spaceId=ad2a71b5-1b0d-4734-bbc4-60a807442e5d\&width=2000\&userId=\&cache=v2)

### **4.4 SAM vs. Strong Augmentations**

![fig7](https://erratic-tailor-f01.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb1af1ee4-ce5a-49c2-b6a4-5f6bf525007e%2FUntitled.png?table=block\&id=15dd004b-fc6b-4fbb-8a01-5313d7cd1722\&spaceId=ad2a71b5-1b0d-4734-bbc4-60a807442e5d\&width=2000\&userId=\&cache=v2)

*   비교를 위해 strong augmentation은 mixup과 RandAugment를 사용하였다

    #### Generalization

    * SAM의 경우 ViT, Mixer에서 augmentation보다 좋은 성능을 내었고 특히 dataset이 작은 경우 이런 현상이 두드러졌다(i1k). 흥미로운 관찰로, Figure2의 중간을 보면 Aug와 SAM이 training error를 오히려 높혔다. 이는 regularization의 효과로 보인다. 둘의 차이가 있다면 Aug쪽이 training loss가 요동치는 모습을 볼 수 있다

    #### Sharpness at convergence

    <img src="https://erratic-tailor-f01.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3092ca24-b721-41e8-a6bb-9b011afa6429%2FUntitled.png?table=block&#x26;id=dca19671-3bf9-4851-8ba3-c9afc748f397&#x26;spaceId=ad2a71b5-1b0d-4734-bbc4-60a807442e5d&#x26;width=2000&#x26;userId=&#x26;cache=v2" alt="fig8" data-size="original">

    * Augmentation이 SAM과같이 기하적으로 loss를 smoothe 할 수 있을까?
    * 우선 시각화하여 확인하였다. AUG가 ![](https://latex.codecogs.com/gif.latex?%5Clambda\_%7Bmax%7D)를 크게했지만 average flatness를 알 수 있는 Gaussian 섭동 loss ![](https://latex.codecogs.com/gif.latex?L%5E%7B%5Cmathcal%7BN%7D%7D\_%7Btrain%7D=%5Cmathbb%7BE%7D\_%7B%5Cepsilon%5Csim%5Cmathcal%7BN%7D%7D%5BL\_%7Btrain%7D\(w+%5Cepsilon\)%5D)를 ViT-B에서보다 작게 만들었다(![](https://latex.codecogs.com/gif.latex?w)주변에서의 로스가 작았다는 것은 최적으로 인정된 ![](https://latex.codecogs.com/gif.latex?w)주변에서의 로스가 작았다는 뜻이고 이는 곧 ![](https://latex.codecogs.com/gif.latex?w)주변으로 flatness하다는 뜻이다)
    * 이것은 SAM과 augmentation모두가 loss landscape를 flat하게 만들었다는 뜻이다
      * 가우시안 섭동이 작은거는 알겠습니다. 하지만 ![](https://latex.codecogs.com/gif.latex?%5Clambda\_%7Bmax%7D)가 1659.3으로 비교적 큰 값이 나왔는데?
      * 이것은 SAM과 Augmentation의 flaten 전략이 다르기 때문이다. SAM은 minmax를 사용해 전체적인 Loss에서의 landscape를 강제하지만 Augmentation같은 경우 최악의 case는 무시해버리고 augmentation으로부터 알 수 있는 inductive bias 방향으로의 landscape flaten을 하기 때문이다




  



## **5. Conclusion**  

* 이 연구는 지금까지 방대한 양의 데이터와 augmentation에 의존한 ViT, MLP의 기하적 loss 특징을 분석했다. 여기서 local minima 문제를 찾고 SAM을 도입해 flatten loss landscape로 일반화 성능의 향상을 끌어냈다. ViT는 어떠한 pre-training이 없다면 ResNet의 성능을 앞지를 수 있었다. 또한 SAM을 도입한 ViT의 attention map이 더욱 해석 가능하게 변화했다
* 개인적 의견으로, ViT가 강력한 구조임은 맞지만 data hungry한 특징이 유난히 강해 연구 이후의 실용 단계에서 어떻게 이용될 수 있을지 회의적이었다. optimizer를 바꾸는 방법으로 보통의 실험실과 PC에서도 구현이 가능한 방법을 제안했다는 것에 큰 의의가 있다고 생각한다.

---  
## **Author Information**  

* 홍성래 SungRae Hong
    * Master's Course, KAIST Knowledge Service Engineering 
    * Interested In : SSL, Vision DL, Audio DL
    * Contact : sun.hong@kaist.ac.kr

## **6. Reference & Additional materials**  

이 논문을 이해하는데 필요한 수학적 지식을 아래에서 확인할 수 있습니다.

* 출처 : 공돌이의 수학노트
    * [헤세 행렬(Hessian Matrix)의 기하학적 의미](https://angeloyeo.github.io/2020/06/17/Hessian.html)
    * [자코비안(Jacobian) 행렬의 기하학적 의미](https://angeloyeo.github.io/2020/07/24/Jacobian.html)



