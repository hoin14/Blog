---
layout: post
title:  "[FrameWork] Struts FrameWork"
date:   2020-09-15 02:59:13 +0800
categories: FrameWork
tags: framework
---

스트럿츠 프레임워크의 구조와 사용하는 이유에 대해 알아보자.<br>

<p>
Struts는 MVC 패턴에서 Controller 역할을 하는 웹 어플리케이션 프레임워크이며 기존에 서블릿마다 가닥 가닥 나누어 보내던 것을 Struts는 우선 모든 서블릿 요청을 하나로 모으고, 그 후에 기능에 맞는 액션으로 보내준다.(서블릿 수 감소)
</p>
<h5>스트럿츠의 구조</h5>
<img src="/images/web/struts1.jpg" width="50%" height="50%" alt="">
<p>우선 스트럿츠 컨트롤러는 ActionServlet, RequestProcessor, Action, ActionForm 클래스가 있다.</p>
<p>
웹 어플리케이션의 배포 파일(web.xml)에 스트럿츠 ActionServlet 클래스를 등록해 놓은 후 웹 컨테이너가 구동되면 ActionServlet 클래스가 초기화 된다. ActionServlet 클래스는 초기화되면서 스트럿츠에 등록한 각종 설정 파일들을 로드하고 Config 클래스들과 RequestProcessor 클래스를 초기화 한다.
</p>
<p>
ActionServlet 클래스는 사용자의 요청이 있으면, 요청을 처리해 줄 RequestProcessor 를 찾아 사용자의 요청을 전달하고, RequestProcessor 는 사용자의 요청 URL에 따라 필요하다면 ActionForm 객체를 생성하고 요청 파라미터를 ActionForm에 저장한다. ActionForm에 저장된 값은 필요에 따라 값이 올바른지 검증을 실시한다.
</p>
<p>
요청을 받은 RequestProcessor 객체는 Action을 선택하여 execute() 메소드를 호출하며, 이 때 앞서 생성한 ActionForm 객체를 전달한다. Action 객체는 사용자의 요청을 수행할 비즈니스 로직을 호출하여 수행한 후 수행 결과 값을 ActionForm이나 Request, 세션에 저장한다. 비즈니스 로직이 다 수행된 후 Action 은 RequestProcessor에 ActionForward를 리턴한다.RequestProcessor는 Action에서 리턴한 ActionForward에 따라 뷰 영역의 JSP 페이지를 호출한다.
</p>

<h5>Model 1</h5>
<p>Model 1 방식의 웹 어플리케이션이란, 한 개의 JSP에서 모든 비지니스 로직(데이터베이스 쿼리, 업데이트 등 실제 업무 작업)을 수행하고, 그 결과를 바로 출력하는 방식이다. 현재 가장 쉽게 많이 사용되는 방식의 웹 프로그래밍 모델이다.
 이 방식은 아주 단순한 웹 어플리케이션에서는 빠르고 단순하게 프로그램을 짤 수 있어 편하지만 어플리케이션이 커지게 되면 그 복잡도가 크게 증가하여 디버깅이 어렵고, 한 번 수정할 것이 생기면 수정할 위치를 찾기도 어려울 뿐만 아니라, 단순히 비지니스 로직이 바뀌는 것임에도 화면 출력 부분의 수정이 필요하게 된다(그 반대로 디자인 변경을 위해 프로그램 로직을 바꿔야 하는 경우도 많다). 이로 인해 유지보수 비용과 시간이 증가하게 되고, 자바 웹 프로그래머의 밤샘의 원흉이 된다.</p>
<h5>Model 2</h5>
<p>실제 프로그램 수행 부분과 화면에 결과를 뿌려주는 부분을 서로분리 하는 것이다(MVC). 간단하게 모든 요청을 서블릿이 받고, 비지니스 로직을 서블릿에서 수행하고, 결과 출력을 위해 JSP로 포워딩하도록 해도 어플리케이션 복잡도가 많이 감소하게 된다.</p>
