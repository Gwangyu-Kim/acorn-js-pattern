# 개요 

구조 패턴*Structural patterns* 

- [적응자*Adapter*](##적응자)
- [가교*Bridge*](##가교)
- [복합체*Composite*](##복합체*Composite*)
- 장식자_Decorator_
- 퍼사드_Facade_
- 플라이급_Flyweight_
- 프록시_Proxy_

## 적응자

- 요구되는 인터페이스를 구현한 작은 코드 조각
- 비공개 복사본을 래핑하고 이를 통해 프록시로 호출
- 코드의 추상화 레벨을 변경하는데 사용
- 코드 인터페이스를 단순화 할 수 있는 강력한 패턴 

## 가교 

적응자 패턴을 새로운 수준으로 만든다. 하나의 인터페이스를 가지고 각각이 다른 구현의 중간자 역할을 하는 여러 적응자를 만들 수 있다.<br>

## 복합체*Composite* 

- 상속은 강한 결합(Tight coupling)이다 상속 대신 복합체를 사용해 느슨한 결합(Loose coupling)을 제안
- 복합체 패턴은 복합체를 컴포넌트로 교환하여 처리하는 특별한 경우 
- 복합체를 구축하는 두 가지 방법 
  - 복합체 컴포넌트가 고정된 개수의 컴포넌트를 구축
  - 정해지지 않은 개수의 컴포넌트를 구축 
- 부모 복합체에 포함된 컴포넌트는 복합체와 동일한 타입
- 복합체는 자신과 같은 타입의 인스턴스를 포함할 수 있다.
- 복합체는 트리 구조이기 때문에 자바스크립트 코드에서 자주 사용되는 패턴 jQuery 대표 사례


 ## 플라이급*Flyweight*

- 객체를 생성하는 데는 고가의 비용이 든다.
- 각 인스턴스에 프로토타입의 다른 값들만 관리 함으로써, 데이터를 압축할 수 있는 방법을 제공한다.

```js

var Soldier = (function() {
  function Soldier() {};
  Soldier.prototype.Health = 10;
  Soldier.prototype.FightingAbility = 5;
  Soldier.prototype.Hunger = 0;
  return Soldier;
})();

var soldier = new Solider();
console.log(soldier.Health); // 10
soldier.Health = 7;
console.log(soldier.Health); // 7
delete soldier.Health;
console.log(soldier.Health); // 10

```
