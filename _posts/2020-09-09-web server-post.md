---
layout: post
title:  "[Web] Web Server와 WAS"
date:   2020-09-09 02:59:13 +0800
categories: Web
tags: web
---


<strong>Web Server와 WAS 무엇이 다른가?</strong><br>


<h4 id="static-pages와-dynamic-pages">정적페이지와 동적페이지</h4>
<img src="/images/web/static-vs-dynamic.png" width="50%" height="50%" alt="">

<ol>
  <li>정적페이지
    <ul>
      <li>Web Server는 파일 경로 이름을 받아 경로와 일치하는 file contents를 반환한다.</li>
      <li>항상 동일한 페이지를 반환한다.</li>
      <li>Ex) image, html, css, javascript 파일과 같이 컴퓨터에 저장되어 있는 파일들</li>
    </ul> 
  </li>
  <li>동적페이지
    <ul>
      <li>인자의 내용에 맞게 동적인 contents를 반환한다.</li>
    </ul>
    <ul>
      <li>즉, 웹 서버에 의해서 실행되는 프로그램을 통해서 만들어진 결과물 
      * Servlet: WAS 위에서 돌아가는 Java Program</li>
      <li>개발자는 Servlet에 doGet()을 구현한다.</li>
    </ul>
  </li>
</ol>

<h4 id="web-server와-was의-차이">Web Server와 WAS의 차이</h4>
<p><img src="/images/web/webserver-vs-was1.png" width="50%" height="50%" alt="" /></p>
<h3 id="web-server">Web Server</h3>
<ul>
  <li>Web Server의 개념
    <ul>
      <li>소프트웨어와 하드웨어로 구분된다.</li>
      <li>1) 하드웨어
        <ul>
          <li>Web 서버가 설치되어 있는 컴퓨터</li>
        </ul>
      </li>
      <li>2) 소프트웨어
        <ul>
          <li><span style="background-color: #e1e1e1">웹 브라우저 클라이언트로부터 HTTP 요청을 받아 <strong>정적인 컨텐츠(.html .jpeg .css 등)</strong>를 제공하는 컴퓨터 프로그램</span></li>
        </ul>
      </li>
    </ul>
  </li>
  <li>Web Server의 기능
    <ul>
      <li><strong>HTTP 프로토콜을 기반으로 하여 클라이언트(웹 브라우저 또는 웹 크롤러)의 요청을 서비스 하는 기능</strong>을 담당한다.</li>
      <li>요청에 따라 아래의 두 가지 기능 중 적절하게 선택하여 수행한다.</li>
      <li>기능 1)
        <ul>
          <li>정적인 컨텐츠 제공</li>
          <li>WAS를 거치지 않고 바로 자원을 제공한다.</li>
        </ul>
      </li>
      <li>기능 2)
        <ul>
          <li>동적인 컨텐츠 제공을 위한 요청 전달</li>
          <li>클라이언트의 요청(Request)을 WAS에 보내고, WAS가 처리한 결과를 클라이언트에게 전달(응답, Response)한다.</li>
          <li>클라이언트는 일반적으로 웹 브라우저를 의미한다.</li>
        </ul>
      </li>
    </ul>
  </li>
  <li>Web Server의 예
    <ul>
      <li>Ex) Apache Server, Nginx, IIS(Windows 전용 Web 서버) 등</li>
    </ul>
  </li>
</ul>

<h4 id="wasweb-application-server">WAS(Web Application Server)</h4>
<ul>
  <li>WAS의 개념
    <ul>
      <li><span style="background-color: #e1e1e1">DB 조회나 다양한 로직 처리를 요구하는 <strong>동적인 컨텐츠</strong>를 제공하기 위해 만들어진 Application Server</span></li>
      <li>HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)이다.</li>
      <li><strong>“웹 컨테이너(Web Container)” 혹은 “서블릿 컨테이너(Servlet Container)”</strong>라고도 불린다.
        <ul>
          <li>Container란 JSP, Servlet을 실행시킬 수 있는 소프트웨어를 말한다.</li>
          <li>즉, WAS는 JSP, Servlet 구동 환경을 제공한다.</li>
        </ul>
      </li>
    </ul>
  </li>
  <li>WAS의 역할
    <ul>
      <li><strong>WAS = Web Server + Web Container</strong></li>
      <li>Web Server 기능들을 구조적으로 분리하여 처리하고자하는 목적으로 제시되었다.
        <ul>
          <li>분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능을 처리하는 분산 환경에서 사용된다.</li>
          <li>주로 DB 서버와 같이 수행된다.</li>
        </ul>
      </li>
      <li>현재는 WAS가 가지고 있는 Web Server도 정적인 컨텐츠를 처리하는 데 있어서 성능상 큰 차이가 없다.</li>
    </ul>
  </li>
  <li>WAS의 주요 기능
    <ol>
      <li>프로그램 실행 환경과 DB 접속 기능 제공</li>
      <li>여러 개의 트랜잭션(논리적인 작업 단위) 관리 기능</li>
      <li>업무를 처리하는 비즈니스 로직 수행</li>
    </ol>
  </li>
  <li>WAS의 예
    <ul>
      <li>Ex) Tomcat, JBoss, Jeus, Web Sphere 등</li>
    </ul>
  </li>
</ul>

<h4 id="web-server와-was를-구분하는-이유">Web Server와 WAS를 구분하는 이유</h4>
<ul>
  <li><strong>Web Server가 필요한 이유?</strong>
    <ul>
      <li>클라이언트(웹 브라우저)에 이미지 파일(정적 컨텐츠)을 보내는 과정을 생각해보자.
        <ul>
          <li>이미지 파일과 같은 정적인 파일들은 웹 문서(HTML 문서)가 클라이언트로 보내질 때 함께 가는 것이 아니다.</li>
          <li>클라이언트는 HTML 문서를 먼저 받고 그에 맞게 필요한 이미지 파일들을 다시 서버로 요청하면 그때서야 이미지 파일을 받아온다.</li>
          <li>Web Server를 통해 정적인 파일들을 Application Server까지 가지 않고 앞단에서 빠르게 보내줄 수 있다.</li>
        </ul>
      </li>
      <li>따라서 Web Server에서는 정적 컨텐츠만 처리하도록 기능을 분배하여 서버의 부담을 줄일 수 있다.</li>
    </ul>
  </li>
  <li><strong>WAS가 필요한 이유?</strong>
    <ul>
      <li>웹 페이지는 정적 컨텐츠와 동적 컨텐츠가 모두 존재한다.
        <ul>
          <li>사용자의 요청에 맞게 적절한 동적 컨텐츠를 만들어서 제공해야 한다.</li>
          <li>이때, Web Server만을 이용한다면 사용자가 원하는 요청에 대한 결과값을 모두 미리 만들어 놓고 서비스를 해야 한다.</li>
          <li>하지만 이렇게 수행하기에는 자원이 절대적으로 부족하다.</li>
        </ul>
      </li>
      <li>따라서 WAS를 통해 요청에 맞는 데이터를 DB에서 가져와서 비즈니스 로직에 맞게 그때 그때 결과를 만들어서 제공함으로써 자원을 효율적으로 사용할 수 있다.</li>
    </ul>
  </li>
</ul>

<h4 id="web-service-architecture">Web Service Architecture</h4>
<p>Client -&gt; Web Server -&gt; WAS -&gt; DB</p>
<ol>
  <li>Web Server는 웹 브라우저 클라이언트로부터 HTTP 요청을 받는다.</li>
  <li>Web Server는 클라이언트의 요청(Request)을 WAS에 보낸다.</li>
  <li>WAS는 관련된 Servlet을 메모리에 올린다.</li>
  <li>WAS는 web.xml을 참조하여 해당 Servlet에 대한 Thread를 생성한다. (Thread Pool 이용)</li>
  <li>HttpServletRequest와 HttpServletResponse 객체를 생성하여 Servlet에 전달한다.
    <ul>
      <li>5-1. Thread는 Servlet의 service() 메서드를 호출한다.</li>
      <li>5-2. service() 메서드는 요청에 맞게 doGet() 또는 doPost() 메서드를 호출한다.</li>
      <li><code class="language-plaintext highlighter-rouge">protected doGet(HttpServletRequest request, HttpServletResponse response)</code></li>
    </ul>
  </li>
  <li>doGet() 또는 doPost() 메서드는 인자에 맞게 생성된 적절한 동적 페이지를 Response 객체에 담아 WAS에 전달한다.</li>
  <li>WAS는 Response 객체를 HttpResponse 형태로 바꾸어 Web Server에 전달한다.</li>
  <li>생성된 Thread를 종료하고, HttpServletRequest와 HttpServletResponse 객체를 제거한다.</li>
</ol>