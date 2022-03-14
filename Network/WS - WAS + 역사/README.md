[notion](https://www.notion.so/WebServer-WAS-81f4940e87bc4d51bd38eaa6a26dfd1f#a10808cecef04ae781d793c4e818bfbd)

# WebServer / WAS

# Web Server

- SW: HTTP를 통해 요청하는 HTML, Object등을 전송해주는 서비스 프로그램
- HW: 위에 언급한 기능을 제공하는 컴퓨터 프로그램을 실행하는 컴퓨터

⇒ 웹 페이지를 클라이언트에 전달하자

![Untitled](WebServer%20%20a366a/Untitled.png)

# Web Application Server

- 다양한 로직 처리를 요구하는 동적인 컨텐츠를 제공하기 위해 만들어진 Application Server
- 요청을 받으면 내부의 프로그램을 통해 결과를 만들어냄
    
    JSP, Servlet : dynamic processing
    or DB Connection
    
- 필요한 기능을 수행하고 그 결과를 웹서버에 전달
- WAS = Web Server + Web Container

# WAS가 아니라 WebServer도 있는 이유

## 1. WAS가 해야 할 일을 줄일 수 있음.

Web Client — Web Server — Web Application Server

- 단순 리소스 제공은 Web Server로 안정적이게
- WAS를 뒤에 여러개 둠으로써 load balancing도 가능

## 2. WAS의 환경설정 파일을 외부에 노출시키지 않을 수 있음.

클라이언트 - WAS  간 port가 직접 연결되어 있다면 중요한 설정 파일들이 노출 될 수 있다.

Web Server & WAS에 접근하는 포트를 다르게 두어서 방화벽같이 보안을 강화할 수 있다.

## 3. Health Check

뒤에 서버가 정상적인 상태인지 확인.

무중단 운영을 위한 장애 극복에 쉽게 대응 가능.

# 동적 기능을 하게 되는 역사

## 1. CGI

Common Gateway Interface

WebServer에서 프로그래밍 기능을 넣자. 그 결과를 클라이언트로 줄 인터페이스

![Untitled](WebServer%20%20a366a/Untitled%201.png)

1. **WebServer에서 매 요청마다 Process를 만든다.**
2. CGI 구현체와 통신한다.

프로세스 단위로 실행되니 부하가 크다.

## 2. Java Servlet

CGI의 문제 개선

프로세스 1개 → 내부에 스레드 풀 공간을 만들어 멀티스레드로 처리.

CGI 통신 규약은 지켰음.

---

각각 Java File 형태로 작성, 요청 받을 URL을 매핑하는 방식.

### 생명주기

1. init()
    
    메모리에 올릴 때, 초기화
    
2. service()
    
    request/response 처리, GET/POST → doGet()/doPost() 분기
    
3. destroy()
    
    종료 요청시 실행
    

### 싱글턴

서블릿 컨테이너에서 서블릿 객체는 싱글턴으로 관리된다.

재사용 및 여러개 HTTP 요청을 동시에 처리하므로 Thread-Safe 하지 않다.

### HttpServletRequest / HttpServletResponse 객체

를 통해 서블릿 컨테이너 → 쓰레드 생성 → req, res 인자로 service() 메소드 호출 → 요청 처리 후 → 객체 소멸

### IoC (Inversion of Control)

서블릿 객체 생성, 소멸 등 프로그램 흐름을 개발자가 주도하지 않고, Servlet Container가 주도해서 제어권이 반전.

## 2. 1. Apache Tomcat

Servelt이 실행 될 수 있는 Web Container환경을 제공하는 Web Application Server

WebServer + Web Container의 조합

하나의 톰캣에는 하나의 JVM을 가지고 있음.

![Untitled](WebServer%20%20a366a/Untitled%202.png)

### Servlet Context

서블릿 컨테이너와 통신하기 위해 사용되는 인터페이스

Servlet Container가 생성/종료되면 Application 별 **web.xm**l을 이용해 컨텍스트를 초기화 및 생성, 종료, 소멸

즉, Servlet Container끼리 통신을 한다는 것은 하나의 톰캣에 여러 애플리케이션을 띄울 수 있다.

## 3. JSP

Servlet은 HTML 코드를 print 해서 출력하는 형태.

JSP는 HTML + Java Code 삽입.

JSP도 .jsp → .java → .class 를 거쳐 Servlet을 통해 처리됨.

## 4. Spring MVC

![Untitled](WebServer%20%20a366a/Untitled%203.png)

1. Request가 들어오면 Dispatcher Servlet(web.xml에 등록)으로 간다.
2. HandlerMapping에서 Handler(적절한 Controller)를 찾는다.
3. HandlerAdapter → Controller의 메서드를 호출한다.
4. ModelAndView 형태 (Model: Data, View: Page논리적이름)
5. ViewResolver가 View를 찾는다.
6. Model을 View에 심어준다.
7. Client로 간다.

### Servlet에 대한 DispatcherServlet의 개선점

URL마다 Servlet이 하나씩 필요했다.

Servlet 하나마다 web.xml에 mapping을 해줘야했다.

⇒ Dispatcher Servlet이 분리해준다.
