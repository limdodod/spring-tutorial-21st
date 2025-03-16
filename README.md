### Spring이 지원하는 기술
---
#### IoC/DI
 1. IOC (Inversion of Control) : 제어의 역전
    - 객체의 생성과 관리를 개발자가 아닌 Spring 프레임워크가 담당한다!!
      
    IoC 컨테이너의 작동 방식
      - 객체를 Class로 정의
      - 객체 간의 연관성 지정: Spring 설정파일 (Config) 또는 어노테이션을 통해 객체가 어떻게 연결될지 (의존성 주입) 지정
      - IoC 컨테이너가 이 정보를 바탕으로 객체 생성, 주입


 2. DI (Dependency Injection) : 의존성 주입
   - 객체가 직접 코드에서 생성한 것이 아니라, 이미 설정된 속성을 통해 필요한 객체(종속성)를 주입받는 방식
     
   1️⃣ 생성자 주입 (권장)

     @Service
     @RequiredArgsConstructor
     public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
       } 
      }
   
   2️⃣ Setter 주입
   
   3️⃣ 필드 주입
   
      ( 2️⃣,3️⃣은 의존성이 없어도 객체가 생성될 수 있어 권장하지 않음!)


#### AOP (Aspect Oriented Programming)
  - 핵심 기능과 부가 기능을 분리하는 방식
  - 객체지향프로그래밍(OOP)는 공통적인 부가 기능의 중복 코드 발생 --> 이를 해결하기 위함

    
#### PSA (Portable Service Abstraction)
  > Service Abstraction (서비스 추상화)
  >> 추상화 계층을 이용해서 특정 기술의 구현부를 숨기고 개발자에게 편의성을 제공해 주는 것

  - PSA란 환경의 변화와 관계없이 일관된 방식의 기술로의 접근 환경을 제공하는 추상화 구조
  - Spring Web MVC, Spring Transaction, Spring Cache 등


### **Spring Bean이란?**
  - Spring 컨테이너가 관리하는 자바의 객체
  - 객체가 의존관계를 등록할 때 Spring 컨테이너에서 빈을 찾고, 그 빈과 의존성을 만든다.

  - 스프링에서 bean 생성시 별다른 설정이 없으면 싱글톤 적용
  - 스프링은 컨테이너를 통해 직접 싱글톤 객체를 생성하고 관리하는데,요청이 들어올 때마다 매번 객체를 생성하지 않고, 이미 만들어진 객체를 공유함
  ---
  ## Bean을 등록하는 방법
  
  1️⃣ @Component -> @Autowired 
  
     : Spring이 자동으로 클래스를 스캔하고 Bean 등록
     : 다른 클래스에서는 @Autowired 어노테이션을 통해 주입받아 사용
     
  2️⃣ @Configuration -> @Bean
  
     : Spring 설정 파일에 @Configuration 어노테이션 추가 -> @Bean으로 지정
  ---  
  ## Spring Bean의 생명주기
  
   스프링 IoC 컨테이너 생성 → 스프링 빈 생성 → 의존관계 주입 → 초기화 콜백 메소드 호출 → 사용 → 소멸 전 콜백 메소드 호출 → 스프링 종료


  
### **스프링 어노테이션**
  - 코드 사이에 특별한 의미, 기능을 수행하도록 하는 기술 (@)

    
  - @SpringBootApplication
    : Spring Boot을 자동으로 실행시켜주는 어노테이션

    
  - @ComponentScan
    : @Component, @Service, @Repository, @Controller, @Configuration이 붙은 빈들을 찾아서
Context에 빈을 등록해 주는 어노테이션 (@SpringBootApplication에 포함)


   - @RequestMapping
     : 어떤 URL을 어떤 메소드가 처리할지 매핑
     : GET/POST/PUT/PATCH/DELETE 정의


   - @Transactional
     : 메서드 실행이 정상적으로 완료되면 자동 커밋, 하나라도 실패히면 자동 롤백

   - @RestController: @Controller + @ResponseBody
                    : JSON 형식의 데이터나 문자열 등을 반환할 때, 더 간단하게 사용

     @Repository: DAO 역할을 하는 클래스에 사용
     
     @Service: 비즈니스 로직을 담당하는 클래스에 사용  


### **단위 테스트와 통합 테스트**

  1. 단위테스트 (Unit Test)
     - 개별 메서드나 함수, 클래스 등 작은 기능 단위를 대상으로 함
     - 코드의 특정 부분이 정확하게 동작하는지 확인
     - JUnit 사용
       
  2. 통합테스트 (Integration Test)
     - 전체 시스템이나 주요 컴포넌트들이 함께 어떻게 작동하는지를 검증하는데 초점을 둠
     - 실제 환경과 가까운 조건에서 여러 컴포넌트의 상호작용 검증
