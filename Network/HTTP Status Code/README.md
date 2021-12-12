# HTTP Status Code

## 1xx

- 100 Continue
    
    임시적인 응답.
    지금까지의 상태가 괜찮으며, Client가 계속 요청해도 되고, 요청 완료 시 무시해도 됨.
    
- 101 Switching Protocol
    
    Client의 Upgrade 요청 헤더에 대한 응답에 들어가며, Server에서 Protocol을 변경하겠다.
    → Upgrade:
    HTTP 1.1 ↔  HTTP 2.0
    HTTP/HTTPS ↔ WebSocket
    
- 102 Processing
    
    Server가 요청 수신했고, 이를 처리 중.
    
- 103 Early Hints
    
    Link 헤더와 함께 사용되며, 서버가 응답 준비하는 동안 사용자(user agent) 사전 로딩을 시작할 수 있게 한다.
    

## 2xx

- 200 OK
    
    성공.
    
    - GET: 리소스가 메시지 바디에 전송되었다.
    - HEAD: 개체 헤더가 메시지 바디에 있다.
    - PUT/POST: 수행 결과에 대한 리소스가 메시지 바디에 전송되었다.
    - TRACE: 메시지 바디에 서버에서 수신한 요청 메시지를 포함하고 있다.
- 201 Created
    
    PUT/POST 요청처럼 새로운 리소스가 생성되었음을 알림.
    
- 202 Accepted
    
    Request는 수락되었는데, 결과는 아직 모름.
    
- 204 No Content
    
    Request에 대한 content가 없지만, 헤더는 의미있을 수 있다.
    

## 3xx

- 300 Multiple Choice
    
    Request에 대해 여러 응답이 가능하다.
    사용자는 그 중 반드시 하나를 선택해야함.
    
- 301 Moved Permanently
    
    요청한 resource URI가 변경되었음.
    
- 302 Found
    
    요청은 잘했는데, URI가 일시적으로 변경되었음. Redirect
    
- 304 Not Modified
    
    캐시와 관련. 캐시 만료.
    

## 4xx

- 400 Bad Request
    
    요청이 잘못됨.
    
- 401 Unauthorized
    
    표준: 미승인
    디팩토: 비인증
    
- 403 Forbidden
    
    권한 문제. 단, Server가 Client가 누군지 알고 있는 것이 401과의 차이점.
    
- 404 Not Found
    
    없다. 아니면 403인 것을 숨기기 위해 사용할 수도 있음.
    

## 5xx

- 500 Internal Server Error
    
    서버가 큰일났다.
    
- 501 Not Implemented
- 502 Bad Gateway
- 503 Service Unavailable
- 504 Gateway Timeout