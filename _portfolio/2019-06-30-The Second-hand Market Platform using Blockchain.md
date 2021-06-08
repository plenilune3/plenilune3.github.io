---
title: "The Second-hand Market Platform using Blockchain"
excerpt: "Capston Design Project"
date: 2019-06-30

header:
  overlay_image: /assets/images/The_Second-hand_Market_Platform_using_Blockchain/identity.jpg
  overlay_filter: 0.5
  teaser: /assets/images/The_Second-hand_Market_Platform_using_Blockchain/identity.jpg

sidebar:
  - title: "Role"
    image: /assets/images/The_Second-hand_Market_Platform_using_Blockchain/profile.jpg
    image_alt: "logo"
    text: "Team Leader, Developer"
  - title: "Responsibilities"
    text: "Configuring Block-Chain network and Developing API to communicate with the server"

gallery:
  - url: /assets/images/The_Second-hand_Market_Platform_using_Blockchain/image-1.jpg
    image_path: assets/images/The_Second-hand_Market_Platform_using_Blockchain/image-1.jpg
    alt: "placeholder image 1"
  - url: /assets/images/The_Second-hand_Market_Platform_using_Blockchain/image-2.jpg
    image_path: assets/images/The_Second-hand_Market_Platform_using_Blockchain/image-2.jpg
    alt: "placeholder image 2"
  - url: /assets/images/The_Second-hand_Market_Platform_using_Blockchain/identity.jpg
    image_path: assets/images/The_Second-hand_Market_Platform_using_Blockchain/identity.jpg
    alt: "placeholder image 3"
---

## 🎯Summary

캡스톤 디자인 프로젝트로 블록체인을 활용한 중고거래 플랫폼을 만들었습니다.
블록체인 이라는 새로운 기술을 배우면서 개발하는게 쉽지 않았습니다.

블록체인은 이더리움을 사용했고, 웹은 장고로 구현했습니다.
저는 블록체인 네트워크를 구성하고, 중고거래를 위한 스마트 컨트랙트를 작성하는 일을 담당했습니다.
그리고 블록체인 네트워크와 웹 서버가 통신하는 부분을 개발했습니다.

이런저런 어려움이 있었지만 팀원들과 프로젝트를 완성하여 결과발표회에서 최우수상(2위)을 받았습니다.
좋은 결과를 얻어서 그 동안의 노력을 보상 받았다고 생각합니다.

## 📚Introduction

처음 팀원들과 함께 제안한 프로젝트는 블록체인과 전혀 상관없었습니다. 
평범한 웹 프로젝트를 기획해서 제안했고 다른 팀들도 비슷했습니다.
아이디어라도 독특했으면 좋겠다는 평가를 받고, 프로젝트를  다시 기획했습니다.

여러가지 의견을 나누다가 나온 주제가 블록체인이었습니다.
한창 머신러닝을 비롯한 새로운 기술에 관심이 많을 시기라서 도전해보기로 했습니다.
새로운 기술에 대한 도전은 어려운 일이지만, 좋은 팀원들과 함께 색다른 경험을 할 수 있었습니다.

이더리움의 스마트 컨트랙트를 활용하여 사용자가 낮은 수수료로 안전하게 거래하는 것이 목표였습니다.
기존의 안전거래 서비스인 "에스크로"서비스와 다르게 중개자 없이 안전하게 거래하는 플랫폼을 구현하고 싶었습니다.
그래서 중고거래를 할 수 있는 웹 사이트를 만들고, 블록체인 네트워크와 스마트 컨트랙트를 작성하여 원하는 기능을 수행하도록 했습니다.

프로젝트에 대한 자세한 설명은 그때 당시 발표에 사용했던 슬라이드를 첨부하겠습니다.

[프로젝트 발표 내용](/assets/files/The_Second-hand_Market_Platform_using_Blockchain/The Second-hand Market Platform using Blockchain.pdf)

## 🙏What have you expected?

첫 번째, 새로운 기술에 대한 호기심을 채우고 싶었습니다.
당시 머신러닝 수업과 같이 떠오르는 학문을 배우고 있었고, 프로젝트도 진행하면서 흥미가 높았었습니다.
자신감도 높은 상태였고, 좋은 팀원들을 만나서 어려운 주제를 고를 수 있었던 것 같습니다.
그래서, 아직 경험해본적이 없는 블록체인에 도전했습니다.

두 번째, 아주 당연하게 수업에서 좋은 성적을 받고 싶었습니다.
평범한 주제로는 어필을 제대로 못할 것 같아서, 톡톡튀는 주제를 골랐습니다.
이 부분에 대해서는 팀원 간 의견충돌이 조금 있었습니다.
"평범한 주제라도 잘 만들어가면 문제없다."라는 의견이 있었습니다.
하지만 "저희보다 훨씬 잘하는 팀이 많을거다."라는 의견으로 설득했습니다.

## ⚡What have you learned?

웹 프레임워크로 Django를 사용하여 중고거래를 할 수 있는 웹 사이트를 제작했습니다. 
그리고 저는 서버가 블록체인 네트워크와 통신하면서 스마트 컨트랙트를 생성하고 완료할 수 있도록 API를 작성했습니다.

블록체인 네트워크와 비동기 통신을 구현하면서 많은 어려움을 만났습니다.
처음에는 동기로 통신하는 방법을 생각했습니다.
하지만, 블록체인 네트워크에서 트랜잭션이 만들어지는 시간과 웹 서버가 통신하는 시간은 큰 차이가 있었습니다.
그래서 요청을 보내놓고 다른 작업을 수행할 수 있도록 비통기로 통신할 수 있도록 구현하고 싶었습니다.

무언가를 비동기로 만드는 것은 어려운 일이라는 것을 배웠습니다.
결론적으로 반쪽짜리 비동기 통신을 구현했습니다.
프로젝트가 끝나고 난 후, 개인적으로 공부하면서 메시징 큐에 대해 배웠습니다.
"요구사항을 구현하는데 메시징 큐를 사용하면 어땠을까?"라는 의문점이 남았습니다.

매 주 수업시간마다 무엇을 만들고, 현재까지 얼마나 진행했는지 발표했습니다.
피드백을 받으면서 문제가 무엇인지 빠르게 파악할 수 있었습니다.
그래서 이와 같은 리뷰 시간이 정말 중요하다고 느꼈습니다.
그 동안 중요하지 않은 문제에 대해서 고민하고 있는 경우가 많았습니다.
하지만 중요한 부분과 중요하지 않은 부분을 정확히 나눌 수 있어서 빠르게 개발 할 수 있었습니다.

직접 구현하는 일보다, 누군가 구현한 라이브러리를 잘 사용하는 방법을 찾아 공부했습니다.
대표적인 라이브러리가 블록체인 네트워크와 통신할 때 사용하는 web3 였습니다.
인터넷에 정보가 많이 없었기 때문에, 원하는 기능을 구현하기 위해서 공식문서를 많이 참고했습니다.
공식문서에 나와있는데로 정확히 사용하는 것이 중요하다고 느꼈습니다.

## ⭐What is Next?

운 좋게도, 결과발표회에서 최우수상(2위)를 수상할 수 있었습니다.
프로젝트를 진행하는 동안 너무 힌들었지만, 좋은 결과를 얻어서 매우 기뻤습니다.

프로젝트를 진행하면서 여러가지 의문점과 해결해야할 문제들이 남았지만 일단 묻어두려고 합니다.
중요하다고 생각하면, 따로 공부하여 게시글로 따로 올리도록 하겠습니다.

블록체인이 흥미로운 기술이라는 것을 배웠습니다.
하지만 동시에 어려운 기술이라서 공부가 정말 많이 필요하다고 느꼈습니다.
기회가 된다면 인턴십이나 연구실에서 더 깊게 배워보고 싶습니다.

팀원들과 함께 체계적으로 처음부터 끝까지 진행한 프로젝트라서 애정이 많이 갔습니다.
개선하여 다른 경연대회를 나가고 싶었으나, 팀원 중 한 명이 조기졸업 후 취업을 하여 아쉽게 나가지 못했습니다.
그래도 프로젝트 기간 동안 열심히 했기 때문에 후회는 없었습니다.

또다시 새로운 기술 또는 흥미로운 주제와 같은 기회가 주어지면, 주저없이 도전하겠습니다.

## 🌏Reference

 - 

{% include gallery %}
