# 폰트 최적화

### 폰트의 문제점
폰트도 네트워크를 통해 다운로드를 받기 때문에 네트워크 환경에 따라 다운로드 지연을 받는다.이런 웹폰트의 문제를 FOUT와 FOIT 두가지로 나눌 수 있다.
FOUT는 Flash of unstyeld text로 폰트를 다운로드 하기전에는 기본 텍스트로 보여주다가 폰트가 다운로드 된 시점에 폰트가 적용되는 현상으로 IE, Edge 브라우저에서 기본적으로 발생한다.
FOIT는  Flash of invisible text의 약자로 폰트가 다운로드 되기전에는 해당 폰트가 적용된 텍스트를 보여주지않다가 다운로드 된 시점에 폰트와 텍스트를 보여주는 현상으로 Chrome, Safari  브라우저에서 기본적으로 발생한다.


### 웹폰트 성능 최적화 방법

1. 폰트 적용 시점 컨트롤하기
- FOUT , FOIT를 컨트롤하는 방법으로서  @font-face css에 font-display를 사용하여 해당 폰트를 어떤 방식을 사용하여 노출시킬건지 적용 가능하다.
  
  ```
  Auto : 기본
  Block : FOIT(timeout = 3s)
  Swap : FOUT 처음부터 기본폰트
  Fallback : FOIT(timeout = 0.1s) -3s후에도 불러오지못하면 기본폰트+ 캐시됨
  Optional : FOIT(timeout = 0.1s) - 네트워크 상태에 따라 기본폰트 유지여수 결정 + 캐시됨 (구글 기본 권장 방식)
  ```


2. 폰트 사이즈 줄이기
- 폰트 사이즈를 줄이기 위해서는 웹폰트 포맷 사용,local 폰트 사용, Subset과 Unicode Range를 적용 그리고 data-uri로 변환하는 방식이 있다.

  - 웹폰트 포맷 사용 
	woff : ttf 폰트를 압축하여 웹에서 더 사용하기 쉽게 만든 형식.
	EOT > TTF/OTF > WOFF > WOFF2 순으로 용량이 작음.
 	브라우저 마다 지원되지않는 버전에 대응하기 위해서는  폰트 format을 설정해주고 여러개의 폰트 포맷을 선언하면 됨.  ex ) src : url (….woff2) format(woff2) , url (….woff) format(woff)

  - local 폰트 사용
	local에 폰트가 있다면 별도로 네트워크를 통해 다운로드 받을필요가 없음. 
	local에 폰트 존재 여부는 src : local(폰트명) 으로 체크.

  - Subset 사용
	실제로 사용할 언어  + 글자들만 잘라서 사용하는 방식
	폰트가 적용되지않는 텍스트에도 폰트를 불러오는 문제가 있을 수 있음  > Unicode Range 적용하여 불필요한 로드 제거

  - Unicode Range 적용
	유니코드와 폰트를 함께 지정하므로서 지정된 유니코드에만 폰트가 적용되도록 할 수 있음.

  - data-uri로 변환
	파일을 base64 코드로 변환하여 css와 폰트 데이터를 함께 불러오는 방식으로 사용


### + 폰트 Preload하기
- 폰트가 페이지에서 필요하기전에 폰트가 필요하다는것을 알려서 미리 로드하는 방식
- index파일 내 head 태그안에 link태그로 폰트를 로드함.
- 직접 로드하면 compile시 link url이 맞지않으므로 webpack plugin(preload-webpack-plugin) 사용하여 preload
