# nextjs 메타데이터 설정방법

## 정적 메타데이터 설정방법

페이지 배포 시 이미 메타데이터가 결정되어있는 경우.
page 또는 layout 파일에서 metadata 변수를 export한다.

### metadata 객체

title : 페이지 제목을 결정하는 속성 (탭에 표기되며, 검색엔진 노출되는 title),
description : 검색엔진 노출되는 설명
그 외 속성은 [metadata](https://nextjs.org/docs/app/building-your-application/optimizing/metadata) 참고

## 동적 메타데이터 설정방법

페이지내 동적 데이터에 따라 메타데이터가 달라지는 경우.
generateMetadata 함수를 export한다.(비동기함수)

### generateMetadata 함수

페이지 로드 시 nextjs에 의해 자동으로 실행되는 함수이다.
동적경로, 매개변수를 담은 config 객체를 인수로 전달받으며, metadata 객체를 반환한다.
인수 객체 { { params, searchParams}}
반환 객체 : {title : … , description : ….}

## layout 메타데이터 설정

page 파일 외에 layout 파일에서도 메타데이터 설정이 가능하다.
layout에 설정되어 반환되는 metadata 객체는 자체 메타데이터를 설정하지 않은 모든 페이지에 사용된다. (= default metadata)

_metadata 적용 우선순위는 하위에서 적용될수록 우선순위가 높다. (page> layout)_
