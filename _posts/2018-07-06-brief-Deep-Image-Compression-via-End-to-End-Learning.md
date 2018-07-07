---
layout: post
title:  "Deep Image Compression via End to End Learning"
date:   2018-07-07 22:03:00 +0900
categories:
  - [Briefs, Machine_Learning]
tags:
  - Machine Learning
  - Image Compression 
comments: true
---
Deep Image Compression via End to End Learning
===
{:no_toc .}

* Table of contents
{:toc}
본 논문은 ariv에 올라온 논문으로 2018년 6월 5일에 올라온 가장 최신의 논문이다. 

## 요약 및 Introduction

해당 논문은 가장 최신의 정지영상 압축을 논한 것으로서 HEVC Intra인 BPG 보다 월등한 성능 (MSSSIM - BDrate로 7.81% ~ 19.1% 성능을 내었다.  with respect to  Kodak and ETH data set)을 보여주었다. 특징은 다음과 같다.

- 3 단계 Downsampling과 Upsampling을 사용하였다.
	- Upsampling은 Super Resolution에 사용된 CNN 구조를 그대로 사용하였다.
- RD Optimization을 반영한 Perceptual Loss Function을 사용하였다.
- ReLu 함수대신 PReLu (Paeametric Rectified Linear Unit) 를 사용하였다. 
- Entropy Coding Tool로 PAQ를 사용하였다.
	- PAQ의 압축 성능이 매우 뛰어나 보인다. 적어도 JPEG의 2배 이상이다.
	- 사실, 여기에서 모든 성능이 나오는 것은 아닌지 의심된다. 
- Adversarial Loss를 고려하여 Wasserstein GAN (WGAN)[1]을 사용하였다. 

## End to End Learning Frame work
- Down sampling
	- Stride-2  $4 \times 4$ Convolution Layer
- Up samling : Super Resolution에서 사용하는 방식 그대로이다.   
	- $3 \times 3$ Kernel을 일반적으로 사용한다.
	- $5 \times 5$ Kernel은 First/Last Layer에서 사용한다.

### Quantization and Entropy Coding
간단한 Scalar Quantization을 사용한다. 
$$
X_Q = Round\left( X_E \cdot (2^Q - 1) \right)
$$
where $X_E \in (0,1)$ 은 Feature Map (fMAP)의 Coefficient이다. (Sigmoid 함수 출력), $Q$는 Qunatization Level 이며 6으로 세팅되어 있다. 
- Binary Coding을 위해 이렇게 만들어진 값에 PAQ를 적용한다.
- De-quantization은 
$$
{X'}_E = \frac{X_Q}{2^Q - 1}
$$
- Back propagation에서는 Round Function을 생략한다.

### Rate Estimation 

##  Reference
[1] M. Arjovsky, S. Chintala, and L. Bottou. Wasserstein gan. arXiv preprint arXiv:1701.07875, 2017.
