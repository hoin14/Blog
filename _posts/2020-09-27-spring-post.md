---
layout: post
title:  "[Spring] Spring FrameWork"
date:   2020-09-27 02:59:13 +0800
categories: Spring
tags: spring
---

<h5>Spring FrameWork란</h5>

<p>
자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크로서 엔터프라이즈급 애플리케이션을 개발하기 위한 모든 기능을 종합적으로 제공하는 경량화된 솔루션.

엔터프라이즈급 개발이란 뜻대로만 풀이하면 기업을 대상으로 하는 개발이라는 말이며 대규모 데이터 처리와 트랜잭션이 동시에 여러 사용자로 부터 행해지는 매우 큰 규모의 환경을 엔터프라이즈 환경이라 일컫음.

<span style="color:red">Spirng Framework는 경량 컨테이너로 자바 객체를 담고 직접 관리함.</span> 객체의 생성 및 소멸 그리고 라이프 사이클을관리하며 언제든 Spring 컨테이너로 부터 필요한 객체를 가져와 사용할 수 있음. 

이는 Spirng이 IOC 기반의 Framework임을 의미함.
</p>

<h5>Spring Framework는 IOC기반</h5>

<p>IOC는 Inversion of Control의 약자로 말 그대로 제어의 역전<br>

일반적으로 지금까지 프로그램은
객체 결정 및 생성 -> 의존성 객체 생성 -> 객채 내의 메소드 호출 하는 작업을 반복함.
이는 각 객체들이 프로그램의 흐름을 결정하고 각 객체를 구성하는 작업에 직접적으로 참여한 것이며
<span style="color:red">모든 작업을 사용자가 제어하는 구조.</span>
하지만 IOC에서는 이 흐름의 구조를 바꿈.<br>
IOC에서의 객체는 자기가 사용할 객체를 선택하거나 생성하지 않음. 또한 자신이 어디서 만들어지고 어떻게 사용되는지 또한 모름. 자신의 모든 권한을 다른 대상에 위임함으로 써 제어권한을 위임받은 특별한 객체에 의해 결정되고 만들어짐.
<span style="color:red">즉, 제어의 흐름을 사용자가 컨트롤 하지 않고 위임한 특별한 객체에 모든 것을 맡김.
IOC란 기존 사용자가 모든 작업을 제어하던 것을 특별한 객체에 모든 것을 위임하여 객체의 생성부터 생명주기 등 모든 객체에 대한 제어권이 넘어 간 것을 IOC, 제어의 역전 이라고 함.</span</p>

<h5>IOC의 구성요소 DL와 DI</h5>

<p>
DL(Dependency Lookup) - 의존성 검색<br>
컨테이너에서는 객체들을 관리하기 위해 별도의 저장소에 빈을 저장하는데 저장소에 저장되어 있는 개발자들이 컨테이너에서 제공하는 API 를 이용하여 사용하고자 하는 빈 을 검색하는 방법.<br>

DI(Dependency Injection) - 의존성 주입<br>
의존성 주입이란 객체가 서로 의존하는 관계가 되게 의존성을 주입하는 것입니다. 객체지향 프로그램에서 의존성 이란 하나의 객체가 어떠한 다른 객체를 사용하고 있음을 의미함.<span style="color:red">각 클래스 사이에 필요로 하는 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해 주는 것.</span>
</p>

<h5>Spring Framework POJO</h5>

<p>
POJO(Plain Old Java Object) 란 말 그대로 평범한 자바 오브젝트.<br> 
이전 EJB(Enterprise JavaBeans)는 확장 가능한 재사용이 가능한 로직을 개발하기 위해 사용 되었었는데 EJB는 한가지 기능을 위해 불필요한 복잡한 로직이 과도하게 들어가는 단점. 그래서 다시 조명을 받은게 POJO. POJO는 gettet/setter를 가진 단순 자바 오브젝트로 정의를 하고 있음. 이러한 단순 오브젝트는 의존성이 없고 추후 테스트 및 유지보수가 편리한 유연성의 장점을 가짐. 이러한 장점들로 인해 객체지향적인 다양한 설계와 구현이 가능해지고 POJO의 기반의 Framework가 조명을 받고 있음.
</p>

<h5>Spring Framework AOP</h5>

<p>
AOP(Aspect Oriented Programming)란 말 그대로 관점 지향 프로그래밍.<br>
대부분 소프트웨어 개발 프로세스에서 사용하는 방법은 OOP(Object Oriented Programming) . 
OOP는 객체지향 원칙에 따라 관심사가 같은 데이터를 한곳에 모아 분리하고 낮은 결합도를 갖게하여 독립적이고 유연한 모듈로 캡슐화를 하는 것. 하지만 이러한 과정 중 중복된 코드들이 많아지고 가독성, 확장성, 유지보수성이 낮음. 이러한 문제를 보완하기 위해 나온 것이 AOP.<br>
AOP에서는 핵심기능과 공통기능을 분리시켜 핵심 로직에 영향을 끼치지 않게 공통기능을 끼워 넣는 개발 형태 이며 이렇게 개발함에 따라 <span style="color:red">무분별하게 중복되는 코드를 한 곳에 모아 중복 되는 코드를 제거 할 수 있어지고 공통기능을 한 곳에 보관함으로써 공통 기능 하나의 수정으로 모든 핵심기능들의 공통기능을 수정 할 수 있어 효율적인 유지보수가 가능하며 재활용성이 극대화됨.</span><br>
물론 AOP로 만들 수 있는 기능은 OOP로 구현 할 수 있는 기능이지만 Spring에서는 AOP를 편리하게 사용 할 수 있도록 이를 지원하고 있음.
</p>

<h5>Spring Framework MVC(model2)</h5>

<img src="/images/web/spring-mvc.png" width="50%" height="50%" alt="">
<p>
MVC란 (Model View Controller) 구조로 사용자 인터페이스와 비지니스 로직을 분리하여 개발 하는 것. MVC에서는 Model1과 Model2로 나누어져 있으며 일반적인 MVC는 Model2를 지칭. </p>

<h5>Model</h5>

<p>Model에서는 데이터처리를 담당하는 부분. Model부분은 Serivce영역과 DAO영역으로 나누어지게 되고 여기서 중요한 것은 Service 부분은 불필요하게 HTTP통신을 하지 않아야하고 request나 response와 같은 객체를 매개변수로 받아선 안됨. 또한 Model 부분의 Service는 view에 종속적인 코드가 없어야 하고 View 부분이 변경되더라도 Service 부분은 그대로 재사용 할 수 있어야 함.Model에서는 View와 Controller 어떠한 정보도 가지고 있어서는 안됨.
</p>

<h5>View</h5>

<p>View는 사용자 Interface를 담당하며 사용자에게 보여지는 부분. View는 Controller를 통해 모델에 데이터에 대한 시각화를 담당하며 View는 자신이 요청을 보낼 Controller의 정보만 알고 있어야 하는 것이 핵심.
Model이 가지고 있는 정보를 저장해서는 안되며 Model, Controller에 구성 요소를 알아서는 안됨.
</p>

<h5>Controller</h5>

<p>Controller에서는 View에 받은 요청을 가공하여 Model(Service 영역)에 이를 전달함. 또한 Model로 부터 받은 결과를 View로 넘겨주는 역할. Controller에서는 모든 요청 에러와 모델 에러를 처리하며 View와 Controller에 정보를 알고 있어야 함.Model과 View의 정보에 대해 알고 있어야함.
</p>

<p>
Model, View, Controller를 나누는 이유는 소스를 분리함으로서 각 소스의 목적이 명확해 지고 유지보수하는데 있어서 용이하기 때문. Model의 Service영역은 자신을 어떠한 Controller가 호출하든 상관없이 정해진 매개변수만 받는다면 자신의 비즈니스 로직을 처리할 수 있어야함. 즉, 모듈화를 통해 어디서든 재사용이 가능하여야 한다는 뜻. 
이말은 View의 정보가 달라지더라도 Controller에서 Service에 넘겨줄 매개변수 데이터 가공만 처리하면 되기 때문에 유지보수 비용을 절감 할 수 있는 효과가 있음. 또한 Service영역의 재사용이 용이하기 때문에 확장성 부분에서도 큰 효과를 볼 수 있는 장점이있음.
</p>