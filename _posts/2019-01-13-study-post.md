---
title: "오늘의 에러"
date: 2019-01-13 12:54:28 -0400
categories: jekyll
---

***************************
APPLICATION FAILED TO START


Description:

Field testMapper in com.example.demo.db.service.TestService required a bean of type 'com.example.demo.dao.DbMapper.TestMapper' that could not be found.

The injection point has the following annotations:
	- @org.springframework.beans.factory.annotation.Autowired(required=true)

Action:

Consider defining a bean of type 'com.example.demo.dao.DbMapper.TestMapper' in your configuration.
***************************

- 발생 경위

게시판용을 따로 분리해서 사용하고 싶어서  BoardController, BoardService, BoardMapper, BoardDB.xml을 새로 추가 하던중 에러가 떴다
에러 내용에 있는 TestMapper는 기존에 잘 돌아갔었고 손도 안댔는데 갑자기 정의된 bean을 찾을 수 없다니?,,Board가 아니고?

- 해결 
  - 'resources/mybatis/mapper/BoardDB.xml 파일에서
  
    <mapper namespace="com.example.demo.dao.DbMapper.BoardMapper"> 이부분을
    <mapper namespace="com.example.demo.dao.DbMapper.BoardMApper"> MApper로 오타냄
  
이렇게 A를 대문자로 오타를 내서 발생한 에러였다
근데 왜 BoardMapper가 아니고 TestMapper가 문제 생겼다고 알려준거야?,,

- 해결경로
STS를 하나 더 켜서 수정전 버전을 임포트해서 순서대로 하나씩 바꾸면서 확인해봄

- 깨달은 점
  - TestMapper라고 알려줘도 내가 작업중인 Mapper에 문제가 생긴걸 수도 있다
  - 타이핑을 직접 치지 말고 가능한 복사해서 사용하자 평소에 복붙 하더라도!꼭!
  - 이클립스가 대충 알려준것 같아도 그 포인트가 맞다(Mapper) 괜히 다른곳 의심하지 말자
  - 쉬운거라도 한번에 쭉 다 하고 확인하지 말고 하나 만들때마다 한번씩 확인하자 제발
