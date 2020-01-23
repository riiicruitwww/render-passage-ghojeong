# Riiid! 인터뷰

## 절차
Riiid는 지원자분의 역량과 fit을 효율적으로 파악하기 위하여, github을 통해 기술면접을 진행하고자 합니다
전달드린 시간까지 1차 작업을 하고, 필요시 현 Riiid 개발자들의 feedback을 반영하여 최종적으로 작업을 하는 방식입니다.
면접과정을 통하여 지원자분 또한 Riiid 웹개발팀의 협업 과정에 대하여 알아가실수 있기 바랍니다.

1. 해당 Repo를 clone 한다.
```
$ git clone https://github.com/GITHUB_ID/REPOSITORY_NAME-GITHUB_ID.git
$ cd REPOSITORY_NAME-GITHUB_ID
```

2. 별도의 branch를 생성하여 작업한다.
```
$ git checkout -b BRANCH_NAME
$ git add/commit/push 
```

3. 1차 제출시 작업중인 branch를 master branch로 [Pull Request(PR)](https://help.github.com/articles/about-pull-requests/)생성를 한다. 

# render-passage

## 문제

산타 토익에서 예시로 주어진 RC파트 지문 데이터를 렌더하고, 문제를 푸는 UI를 구현하세요.

## 예제

문제풀이 UX의 경우 자유로운 스타일로 구현하시면 됩니다.

토익 RC파트에서 나오는 문단중 한가지 입니다. 
1. 평문(e-mail, notificaiton, mail, memo) <br />
  <img width="350" alt="exmaple_normal_passage" src="./images/normal_passage.png">

## FAQ
### Q1. 데이터 명세가 어떻게 되나요?
### A1. 아래 정도의 명세를 공유드립니다.
```
/*
  package의 경우, 학습 컨텐츠(하나의 학습단위)의 명칭으로, 토익에서는 "문제풀이"와 "강의보기"의 두가지 컨텐츠가 존재합니다.
  예시로 주어진 package의 경우 "문제풀이"이며, 문제에 해당되는 지문(passage)과 문제(question)로 이루어져 있습니다.  
*/
package: {
  name: String, // 문제? 강의?
  type: String, // 토익 파트
  human_id: String, // 고유값
  preview: String, // Package의 간소화된 형태의 string
  questions: Array.of(Question), // "문제풀이" 중 문제
  chunk_map: Object, // Package를 그리는데 사용하는 단위 "Chunk"가 모두 id로 맵핑된 Map
  passag_box: Object // "문제풀이" 중 지문
}

/*
  question, passage, passage_translation의 경우, 각자 필요한 고유값을 가지고 있으며 기본적으로 chunk의 구성으로 그려지며, chunk의 구성의 경우 view_tree로 이루어져 있습니다. (고로 세가지 데이터중, question의 대한 명세만 우선적으로 공유 드립니다.)
*/
question: {
  id: Number, // 고유값
  pack_type: String, // 토익 파트
  passage_box_id: Number, // 해당 문제가 귀속된 pasage_box의 고유값
  raw_fbid: String, // 고유값
  correct_answer: String,  // 정답
  order: Number, // 문제의 순서(문제가 속한 pasasge_box기준)
  pack_id: Number, // 해당 문제가 귀속된 pack의 고유값
  view_tree: Object, // 문제를 구성하는 chunk의 구조(트리 형태)
  labels: Array.of(label_ids: Number) // 문제가 포함하는 토익에서의 분류 label의 교유값
}
```
### Q2. 문제풀이 구현이 막막한데,,,
### A2. 문단의 구현에서 데이터를 이해하고, 실무에 사용되는 데이터 구조를 시각화하는 구현력을 보고자 한다면, 문제풀이의 구현의 경우 UX와 디자인 적인 요소에 대한 역량을 보기 위함입니다. 디자인적인 색감 혹은 센스는 배제하고, 객관식 문제를 컴퓨터로 푸는 유저의 경험에 집중하여 구현해주시면 좋습니다. 하지만, 문단의 구현이 조금 더 해당 기술면접에 핵심적인 요소이라는 점을 인지하여 주시기 바랍니다.
