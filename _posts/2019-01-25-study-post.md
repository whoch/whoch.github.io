---
title: "19-01-25 오늘의 배운것"
date: 2019-01-25 22:45:28 -0400
categories: jekyll
---

오늘 팀 프로젝트에서 한 것
첫 번째 한 것
* SeminarInfo 테이블의 `위치` 컬럼 명을 Address에서 Locale로 변경후 팀원들에게 내용 공유
  * 이유 : GroupStudyLog에서도 주소를 사용하는데 컬럼명이 서로 달라서 통일하기 위해

두번째 한 것
* Calendar 세미나 hover 할 때 강사 ID값을 NickName으로 표시되게 변경
* nickname을 쓰려면 기존엔 한번의 JOIN으로 사용하던 쿼리를 3개의 테이블 JOIN을 해야돼서 검색해서 쿼리 수정

<pre><code>
Select * From A left JOIN B ON A.name = B.name
left JOIN C ON A.name = C.name
</code></pre>

* 공부를 제대로 안하고 join을 썼더니 오늘에서야 WHERE가 아닌 ON이 맞다는걸 알게 됐다
* 그래서 쿼리 실행 순서가 다른가?도 궁금해졌고 3개의 테이블을 JOIN 해야하니 조금이라도 양이 적어지게 걸러지는? 쿼리가 먼저 실행되길 원했다
* 쿼리 실행 순서 
  * 링크 : https://delirussum.tistory.com/142

<pre><code>
FROM
ON
JOIN
WHERE
GROUP BY
CUBE | ROLLUP
HAVING
SELECT
DISTINCT
ORDER BY
TOP
</code></pre>
* ON이 WHERE보다 빠르고 JOIN보다도 빨리 실행된다
* 그리고 테스트 해보니 1개의 JOIN일 땐 WHERE를 써도 에러가 안났지만 2개부턴 에러가 나서 ON을 쓸 수 밖에 없는 운명이었다
* mySql JOIN의 종류에 대해 알게됐다
  * 링크 : http://rapapa.net/?p=311
  
세번째 한 것
* 세미나 테이블이 StartDate 컬럼은 시간이 있고(TimeStamp) EndDate엔 날짜만 있어서(date) 캘린더에서 endDate에서 시간 설정 해줘야했음
* 종료일에도 수업이 진행돼서 종료일에도 시간이 있는거라고 하고 그럼 종료일에도 시간을 지정해줘야 fullCalendar에서 일정이 올바르게 뜨게 된다
* 날짜와 시간을 공부를 안해봐서 힘들었다 처음엔 "2019-01-25 13:00:00"에서 date인 "2019-01-25"만 빼면 되지 않나?하고 쉽게 생각했는데 잘 안됐다
* 검색해보니 요즘엔 localDateTime을 많이 쓴다고 했다

<pre><code>
int lectureTime = info.getSeminarStartDate().toLocalDateTime().getHour();
schedule.put("end", info.getSeminarEndDate().toLocalDateTime().plusHours(lectureTime));
</code></pre>

* 우선 시작일에서 시간만 빼내서 EndDate에 더하는 방법으로 해결했다 날짜/시간은 공부가 더 필요할 듯 하다 찝찝

네번째 한 것
* 취업 지원 특강을 들었다

다섯번째 한 것
* 팀 프로젝트에 Calendar 페이지를 합쳤다
* FullCalendar 구현을 내 프로젝트에서 연습삼아 따로 하고있었는데 프로젝트가 더 커지기전에 합치는 연습을 해봐야 할 것 같아서 git연습 겸 프로젝트에 Calendar를 추가했다
* 하면서 git 용어를 자꾸 까먹는 것 같아 내 수준에 맞게 용어를 정리했다
* 좀 더 멋있게 vim으로 사용하고 싶었지만 나에겐 시간이 얼마 남지 않아서 sts에 연동하는 쉬운 방법을 택했다
  * 링크 : https://jwgye.tistory.com/38
  
  
 내일 할 것
 * 팀 프로젝트 Planner의 메인 페이지를 만들어보려고 한다
 * 캘린더는 60%정도 구현된 것 같은데 여기서 잠시 스탑하는 이유는 캘린더에 연동될 다른 페이지가 아직 구현이 안됐기 때문이다
 * 이번 주말은 ajax랑 layout 그리고 jquery,script,git등을 공부를 많이  될 것같다
