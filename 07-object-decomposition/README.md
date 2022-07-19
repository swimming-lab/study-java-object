# 7장. 객체 분해

불필요한ㄴ 정보를 제거하고 현재의 문제 해결에 필요한 핵심만 남기는 작업을 추상화라 한다.

가장 일반적인 추상화 방법은 한 번에 다뤄야 하는 문제의 크기를 줄이는 것이다.

큰 문제를 해결 가능한 작은 문제로 나누는 작업을 분해(decomposition)라고 한다.

### **프로시저 추상화와 데이터 추상화**

- 프로시저 추상화(procedure abstraction)
    - 소프트웨어가 무엇을 해야하는지를 추상화한다.
    - 기능 분해(function decomposition), 알고리즘 분해(algorithmic decomposition)
- 데이터 추상화(data abstraction)
    - 소프트웨어가 무엇을 알아야 하는지를 추상화한다.
    - 둘 중 하나를 선택
        - 데이터를 중심으로 타입을 추상화(type abstraction)
            - 추상 데이터 타입(Abstact Data Type)
        - 데이터를 중심으로 프로시저를 추상화
            - 객체지향(Object-Oriented)
            

프로그래밍 언어적인 관점에서 객체지향을 바라보는 일반적인 관점은 데이터 추상화와 프로시저 추상화를 함께 포함한 클래스를 이용해 시스템을 분해하는 것이다.

### **프로시저 추상화와 기능 분해**

**메인 함수로서의 시스템**

기능 분해 관점에서 추상화의 단위는 프로시저이며 시스템은 프로시저를 단위로 분해된다.

전통적인 기능 분해 방법은 하향식 접근법(Top-Down Approach)을 따른다. 시스템을 구성하는 가장 최상위(topmost) 기능을 정의하고, 이 최상위 기능을 좀 더 작은 단계의 하위 기능으로 분해해 나가는 방법을 말한다.상위 기능보다 하위 기능이 덜 추상적이어야 한다.(구체적이어야 한다)

**급여 관리 시스템**

공식 ‘급여 = 기본급 - (기본급 * 소득세율)’

하양식 접근법을 따르며 최상위의 추상적인 함수 정의에서 출발해서 단계적으로 시스템을 구축한다.

- 직원의 급여를 계산한다.

- 직원의 급여를 계산한다.
    - 사용자로부터 소득세율을 입력받는다.
    - 직원의 급여를 계산한다.
    - 양식에 맞게 결과를 출력한다.

- 직원의 급여를 계산한다.
    - 사용자로부터 소득세율을 입력받는다.
        - “세율을 입력하세요: “라는 문장을 화면에 출력한다.
        - 키도르르 통해 세율을 입력받는다.
    - 직원의 급여를 계산한다.
        - 전역 변수에 저장된 직원의 기본급 정보를 얻는다
        - 급여를 계산한다.
    - 양식에 맞게 결과를 출력한다.
        - “이름: {직원명}, 급여: {계산된 금액}” 형식에 따라 출력 문자열을 생성한다.
    

**급여 관리 시스템 구현**

```ruby
def main(name)
	taxRate = getTaxRate()
	pay = calculatePayFor(name, taxRate)
	puts(describeResult(name, pay))
end

def getTaxRate()
	print("세율을 입력하세요: ")
	return gets().chomp().to_f()
end

$employees = ["직원A", "직원B", "직원C"]
$basePays = [400, 300, 250]

def calculatePayFor(name, taxRate)
	index = $employees.index(name)
	basePay = $basePays(index)
	return basePay - (basePay * taxRate)
end

def descripbeResult(name, pay)
	return "이름: #{name}, 급여: #{pay}"
end

main("직원A")
```

예제에서 알 수 있는것처럼 하향식 기능 분해는 시스템을 최상위의 가장 추상적인 메인 함수로 정의하고, 메인 함수를 구현 가능한 수준까지 세부적인 단계로 분해하는 방법이다.

하향식 기능 분해 방식으로 설계한 시스템은 메인 함수를 투르로 하는 ‘트리(tree)’로 표현할 수 있다.

하향식 기능 분해는 논리적이고 체계적인 시스템 개발 절차를 제시한다.

[그림7-2]

**하향식 기능 분해의 문제점**

- 시스템은 하나의 메인 함수로 구성돼 있지 않다.
- 기능 추가나 요구사항 변경으로 인해 메인 함수를 빈번하게 수정해야 한다.
- 비즈니스 로직이 사용자 인터페이스와 강하게 결합된다.
- 하향식 분해는 너무 이른 시기에 함수들의 실행 순서를 고정시키기 때문에 유연성과 재사용성이 저하된다.
- 데이터 형식이 변경될 경우 파급효과를 예측할 수 없다.

**언제 하향식 분해가 유용한가?**

프로그래밍 과정에서 이미 해결된 알고리즘을 문서화하고 서술하는 데에 훌륭한 기법이다. 그러나 실제로 동작하는 커다란 소프트웨어를 설계하는 데 적합한 방법은 아니다.

### 모듈

**정보 은닉과 모듈**

정보 은닉은 시스템을 모듈 단위로 분해하기 위한 기본 원리로 시스템에서 자주 변경되는 부분을 상대적으로 덜 변경되는 안정적인 인터페이스 뒤로 감춰야 한다는 것이 핵심이다.

모듈은 변경될 가능성이 있는 비밀을 내부로 감추고, 잘 정의되고 쉽게 변경되지 않을 퍼블릭 인터페이스를 외부에 제공해서 내부의 비밀에 함부로 접근하지 못하게 한다.

모듈은 두 가지 비밀을 감춰야 한다.

- 복잡성
    - 모듈이 너무 복잡한 경우 이해하고 사용하기가 어렵다
    - 외부에 모듈을 추상화할 수 있는 간단한 인터페이스를 제공해서 모듈의 복잡도를 낮춘다.
- 변경 가능성
    - 변경 가능한 설계 결정이 외부에 노출될 경우 실제로 변경이 발생했을 때 파급효과가 커진다.
    - 변경 발생 시 하나의 모듈만 수정하면 되도록 변경 가능한 설게 결정을 모듈 내부로 감추고 외부에는 쉽게 변경되지 않을 인터페이스를 제공한다.

급여 관리 시스템의 전체 직원에 관한 처리를 Employees 모듈로 캡슐화한 결과이다.

```ruby
module Employees
	$employees = ["직원A", "직원B", "직원C", "직원D", "직원E", "직원F"]
	$basePays = [400, 300, 250, 1, 1, 1.5]
	$hourlys = [false, false, false, true, true, true]
	$timeCards = [0, 0, 0, 120, 120, 120]

	def Employees.calculatePay(name, taxRate)
		if (Employees.hourly?(name)) then
			pay = Employees.calculateHourlyPayFor(name, taxRate)
		else
			pay = Employees.calculatePayFor(name, taxRate)
		end
	end

	def Employees.hourly?(name)
		return $hourlys[$employees.index(name)]
	end
	
	def Employees.calculateHourlyPayFor(name, taxRate)
		index = $employees.index(name)
		basePay = $basePays[index] * $timeCards[index]
		return basePay - (basePay * taxRate)
	end

	def Employees.calculatePayFor(name, taxRate)
		return basePay - (basePay * taxRate)
	end

	def Employees.sumOfBasepays()
		return = 0
		for name in $employees
			if (not Employees.hourly?(name)) then
				return += $basePays[$employees.index(name)]
			end
		end
		return result
	end
end

def main(operation, args={})
	case(operation)
	when :pay then calculatePay(args[:name])
	when :basePays then sumOfBasepays()
	end
end

def calculatePay(anem)
	taxRate = getTaxRate()
	pay = Employees.calculatePay(name, taxRate)
	puts(describeResult(name, pay))
end

def getTaxRate()
	print("세율을 입력하세요: ")
	return gets().chomp().to_f()
end

def descripbeResult(name, pay)
	return "이름: #{name}, 급여: #{pay}"
end

def sumOfBasePays()
	puts(Employees.sumOfBasePays())
end
```

**모듈의 장점과 한계**

- 장점
    - 모듈 내부의 변수가 변경되더라도 모듈 내부에만 영향을 미친다.
        - 어떤 데이턱 ㅏ변경됐을 때 영향을 받는 함수를 찾기 위해 해당 데이터를 정의한 모듈만 검색하면 된다.
    - 비즈니스 로직과 사용자 인터페이스에 대한 관심사를 분리한다.
        - 사용자 입력, 출력을 Employees 모듈이 아닌 외부, 비즈니스 로직과 공통 로직을 분리
    - 전역 변수와 전역 함수를 제거함으로써 네임스페이스 오염을 방지한다.
- 단점
    - 인스턴스의 개념을 제공하지 않는다.
    - Employees 모듈은 단지 회사에 속한 모든 직원 정보를 가지고 있는 모듈일 뿐이다.
    - 추상화 메커니즘이 필요, 이를 만족시키기 위한 개념이 추상 데이터 타입이다.