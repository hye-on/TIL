###   OCP: 개방-폐쇄 원칙 (Open/closed principle)


    소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.->다형성 활용

    문제점: 구현 객체를 변경하려면 클라이언트 코드를 변경해야한다. 다형성을 사용했지만 OCP원칙을 지킬수가 없다.

    이 문제를 스프링이 해결해준다.