# CORS

## 정의
교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)는 웹 페이지 상의 제한된 리소스를 최초 자원이 서비스된 도메인 밖의 다른 도메인으로부터 요청할 수 있게 허용하는 구조

## Origin
URL에서 프로토콜, 도메인, 포트 번호를 합친 부분을 의미한다.

ex) https://github.com:80/123456?datas=567#abc <br>
위와 같은 URL이 있다고 가정했을 때, <b>https://</b>은 프로토콜(또는 Scheme)에 해당하는 부분이고, **github.com**은 도메인에 해당하는 부분이며, **:80**은 포트번호에 해당하는 부분이다.
따라서 https://github.com:80 까지가 Origin에 해당하는 부분이다.
<br>
<br>
## SOP와 CORS의 관계
SOP(Same Origin Policy, 동일 출처 정책)는 다른 Origin으로 요청을 보낼 수 없도록 금지하는 브라우저의 기본적인 보안 정책이다. 즉, 동일한 Origin으로만 요청을 보낼 수 있게 하는 것이다. 
이전에는 절대적인 규칙이었기 때문에, 다른 Origin으로 요청을 보내는 건 애초에 불가능하였다. 하지만 기술이 발달하면서 서로 다른 Origin끼리 데이터를 주고받아야 하는 일이 많아졌고, 이로 인해 SOP는 별도의 예외 사항을 두게 되었다. 
즉, 몇 가지 예외 상황에 대해서는 다른 Origin으로도 요청을 보낼 수 있게 하는 것이다.

CORS는 다른 Origin으로 요청을 보내기 위해 지켜야 하는 정책으로, 원래대로라면 SOP에 의해 막히게 될 요청의 제한을 해제해 주는 '브라우저' 정책이다.
즉, 서버는 평소처럼 요청이 오면 응답을 해줄 뿐이고, 브라우저가 자신이 보낸 요청 및 서버로부터 받은 응답의 데이터가 CORS 정책을 지키는지 검사하여 안전한 요청을 보낸 건지 검사하는 것이다. 
따라서 서버가 정상적으로 응답을 해줬더라도, 알고 보니 안전한 요청이 아니라고 판단되면 해당 응답을 버린다. 그렇기 때문에 서버 간 통신에서는 이러한 정책이 전혀 적용되지 않는다는 것을 알 수 있다.
<br>
<br>
## CORS 동작 원리
브라우저는 다른 Origin으로 요청을 보낼 때 Origin 헤더에 자신의 Origin을 설정하고, 서버로부터 응답을 받으면 응답의 Allow-Control-Allow-Origin 헤더(브라우저는 Access-Control-Allow-Origin 헤더를 확인하여 CORS 동작을 수행할지 판단)에 설정된 Origin의 목록에 요청의 Origin 헤더 값이 포함되는지 검사를 진행한다. 
즉, CORS 요청을 위해서는 서버에서 응답의 Allow-Control-Allow-Origin 헤더에 허용되는 Origin의 목록 혹은 와일드카드(*, 모든 Origin을 허용한다는 것을 의미하는 특수 기호)를 설정해주면 된다.
 
CORS 요청은 다음과 같이 세 가지 유형으로 나눠서 생각해볼 수 있다.
 
**1. 단순 요청 (Simple Request)**

단순 요청(Simple Request)이 되기 위한 조건은 아래와 같다. 

- 메소드가 GET, HEAD, POST 중 하나여야 한다.
- User Agent가 자동으로 설정한 헤더를 제외하면, 아래와 같은 헤더들만 사용할 수 있다.
Accept
Accept-Language
Content-Language
Content-Type
DPR
Downlink (en-US)
Save-Data
Viewport-Width
Width
Content-Type 헤더에는 아래와 같은 값들만 설정할 수 있다.
application/x-www-form-urlencode
multipart/form-data
text/plain
. . .
 

위와 같은 조건을 만족하는 단순 요청은 안전한 요청으로 취급되어, (뒤에서 설명할) 프리플라이트 요청이 필요 없이 단 한 번의 요청만을 전송한다. 즉, 위에서 언급한 CORS의 기본적인 동작 원리를 그대로 따른다. 다른 Origin으로 요청을 보낼 때 Origin 헤더에 자신의 Origin을 설정하고, 서버로부터 응답을 받으면 응답의 Allow-Control-Allow-Origin 헤더에 설정된 Origin의 목록에 요청의 Origin 헤더 값이 포함되는지 검사하는 것이다. 이를 그림으로 나타내면 다음과 같다.

 


![image](https://user-images.githubusercontent.com/64126100/193022261-cee2d594-1daa-468b-8f12-e5503d34a52f.png)
<br>
<br>
**2. 프리플라이트 요청 (Preflight Request)**

위에서 소개한 단순 요청의 조건에 벗어나는(안전하지 않은) 요청의 경우, 서버에 실제 요청을 보내기 전에 예비 요청에 해당하는 프리플라이트 요청(Preflight Request)을 먼저 보내서 실제 요청이 전송하기에 안전한지 확인한다. 
만약 안전한 요청이라고 확인이 된다면, 그때서야 실제 요청을 서버에게 보낸다. 따라서 총 두 번의 요청을 전송한다.

**프리플라이트 요청의 특징**

- 메소드로 OPTIONS를 사용한다.
- Origin 헤더에 자신의 Origin을 설정한다.
- Access-Control-Request-Method 헤더에 실제 요청에 사용할 메소드를 설정한다.
- Access-Control-Request-Headers 헤더에 실제 요청에 사용할 헤더들을 설정한다.
 
 <br>
<b>서버는 이러한 프리플라이트 요청에 대해 다음과 같은 특징을 가진 응답을 제공해야 한다.</b>

- Access-Control-Allow-Origin 헤더에 허용되는 Origin들의 목록 혹은 와일드카드(*)를 설정한다.
- Access-Control-Allow-Methods 헤더에 허용되는 메소드들의 목록 혹은 와일드카드(*)를 설정한다.
- Access-Control-Allow-Headers 헤더에 허용되는 헤더들의 목록 혹은 와일드카드(*)를 설정한다.
- Access-Control-Max-Age 헤더에 해당 프리플라이트 요청이 브라우저에 캐시 될 수 있는 시간을 초 단위로 설정한다.
 

이러한 응답을 받고 나면 브라우저는 이 응답의 정보를 자신이 전송한 요청의 정보와 비교하여 실제 요청의 안전성을 검사한다. 
만약 이 안전성 검사에 통과하게 된다면, 그때서야 실제 요청을 서버에게 보낸다. 단, 이때는 Access-Control-Request-XXX 형태의 헤더는 보내지 않는다.

예를 들어, Content-Type 헤더의 값이 application/json이고 사용자 정의 헤더로 Custom-Header를 사용하는 POST 요청을 서버에게 보내려 한다면 이는 단순 요청의 조건에 벗어나기 때문에 프리플라이트 요청이 필요하다. 
따라서 총 두 번의 요청이 서버에게 전송된다.
 


![image](https://user-images.githubusercontent.com/64126100/193022214-ff1a15e7-dac0-4855-8af8-351095d8c32a.png)
 

<b>3. 인증 정보를 포함한 요청 (Credentialed Request)</b>

위에서 소개한 두 유형의 요청은 인증 정보가 없는 경우였다. 여기서 말하는 인증 정보(Credential)란 쿠키(Cookie) 혹은 인증(Authorization) 헤더에 설정하는 토큰 값 등을 일컫는다. 
만약 이러한 인증 정보를 함께 보내야 하는 요청(Credentialed Request)이라면, 별도로 따라줘야 하는 CORS 정책이 존재한다.


우선, 쿠키 등의 인증 정보를 보내기 위해서는 클라이언트 단에서 요청 시 별도의 설정이 필요하다. 
이는 Ajax 요청을 위해 어떠한 도구를 사용하느냐에 따라 달라진다. 만약 XMLHttpRequest, jQuery의 ajax, 또는 axios를 사용한다면 withCredentials 옵션을 true로 설정해줘야 한다. 반면, fetch API를 사용한다면 credentials 옵션을 include로 설정해줘야 한다. 이러한 별도의 설정을 해주지 않으면 쿠키 등의 인증 정보는 절대로 자동으로 서버에게 전송되지 않는다.

위와 같은 설정을 통해 인증 정보를 요청에 포함시켰다면, 이 요청은 이제 인증 정보를 포함한 요청이 된다. 
그리고 서버는 이러한 요청에 대해 일반적인 CORS 요청과는 다르게 대응해줘야 한다. 
응답의 Allow-Control-Allow-Origin 헤더가 와일드카드(*)가 아닌 분명한 Origin으로 설정되어야 하고, Allow-Control-Allow-Credentials 헤더는 true로 설정되어야 한다. 
그렇지 않으면 브라우저에 의해 응답이 거부된다.

 ![image](https://user-images.githubusercontent.com/64126100/193022154-c5e606c1-38ca-4ec6-8966-e5d98f6c49e5.png)

