# 20191221

## SSIS, SSAS - 권태돈 강사

* Business Intelligenece
* Data Mart(데이타 통합) - 차원 모델링
* SQL Server Integration Services(SSIS, 데이터 통합 도구) - 제어흐름

* SQL Server Analysis Services(SSAS, 대량의 데이터 신속하게...) - 데이터 형식 모델, 유지관리

 

OLTP(On-Line **Transaction** Processing) : 기간계 시스템

->쪼개놓는다--> DB정규화!



Data Warehouse

Data Mart(쉬움)



처음할일: 기간계, data 원본 파악





## SSMS

* sa 의 password 찾기

1. windows 인증(관리자)
2. 보안탭
3. 로그인탭(비밀번호 변경가능)
4. 데이터베이스->복원->AdventureWorks2016, AdventureWorksDW2016 복원





#### DW란??(대기업, 공공기관)

=> 규모가 방대함...한 회사의 모든 데이터를 통합

##### 정의

* 의사 결정 지원에 사용될 수 있는 응용 프로그램들이  활용하는 정보 기반을 제공하는 하나의 **통합**된 데이터 저장공간

* 다양한 운영 환경의 시스템들로부터 데이터들을 추출(E)/변환(T)/적재(L) 해서 요약한 읽기 전용 데이터베이스

  

  #### Data Mart(중소기업)

  =>  리포트를 만들기 위한 데이터 마트, 리포트에 필요한 요소만 추출하면 됨

##### 특징

* 주제 지향적 ✓
* 통합성 ✓
* 비휘발성
* 시계열성

##### 스키마 디자인

* 테이블 구성
  * 업무사용자가 반드시 인지할 수 있도록
  * 사용자가 접근 가능하도록 
  * 반드시 **단순한** 구조
* 스키마 타입(차이점 : 면접 주된 질문)
  * 성형**(star)**스키마 : 하나의 주제가 하나의 테이블, 가장 권장, 고려할 사항.
  * 사실 성운(Constellation)스키마
  * 눈송이**(Snowflake)**스키마: 차원 테이블이 여러개로 구성, **정규화**(속성의 개수가 가변적일 때)

* 차원 테이블(Dimension)
  - 사용자 관점에서 데이터를 기술
  - 설명하는 내용을 포함하는 폭이 넓은 행
  - 비교적 작은 크기
  - 사실 테이블과 외래키 관계로 **한번만** 조인
  - 심하게 인덱스 설정
  - 대표적인 차원(시간 주기, 권역(도-시-구), 제품, 고객, 사원, 기타)

* 사실 테이블(Fact)
  * 전형적인 사례: 개별 매출 기록
  * 대부분 수치형 데이터
  * 폭이 좁고, 소수의 컬럼만 존재
  * 대량의 데이터 행이 존재(수십억~)
  * 차원을 통해 접근

* star 스키마의 장점
  * 정규화 데이터를 단순화된 형태로 변환
  * 쿼리에 대한 높은 성능(high-performance)의 제공
  * 스타 조인 최적화(Star Join Query Optimization) 지원
  * 많은 BI도구에서 표준처럼 지원
  * 낮은 유지보수 비용(추가/변경 용이)

* Snowflake 스키마의 장점
  * 여러 차원 테이블을 이용한 계층(hierarchies)의 정의
  * 데이터 통합의 프로세스를 단순화
* 시간-날짜 차원
  * 시간 혹은 날짜 정보를 포함하는 차원 테이블
  * 팩트 테이블과 데이터 구체화 정도가 동일해야 함.
  * **날씨, 기온, 명절 여부, 공휴일 여부** 등의 정보를 추가해도 좋다.
    * cf) 마케팅달력이란? 한 주는 무조건 7일 ex) 12월말 1월초 묶음





## SSIS

#### 참고 : informetica, talend, ibm datastage





#### 참고: JOIN

* 조인키 : 두 테이블을 연결하는 열(컬럼)
* 조인유형 : 내부(INNER), 왼쪽 외부(LEFT OUTER), 완전 외부(FULL OUTER)
  * 내부조인: 두 테이블 모두에 존재하는 조인키만 조인(합친다)한다.
  * 외부조인: 두 테이블 중 양쪽 한 곳이라도 존재하면 조인 결과에 나옴
  * 왼쪽 외부조인: 두 테이블 중 왼쪽에 존재하는 조인키는 무조건 결과에 나옴
  * 완전 외부조인: 두 테이블 중 양쪽 한 곳이라도 존재하면 조인 결과에 나옴
  
  
  
  ### 1. 파생 열

* null 값의 치환
* A = B + C
* 3항 연산자 : ISNULL( [CurrencyRateID]  )?0: [CurrencyRateID] 

 ###  2. 데이터변환

SSIS 데이터 형식에 매우 민감함

비유니코드------> 유니코드 (X)

### 3. 스크립트 구성 요소

- Visual C#, Visual Basic.Net(나는 못해)

### 4. UNION ALL

* 집합 연산의 합집합, 밑으로 붙인다.(행이 늘어난다) cf) join은 열이 늘어남

### 5. 병합

#### 빠른 로드

- Bulk Insert

#### 그냥 입력

* Insert



테이블 잠금: 





### 제어흐름

1. 결과를 받아올 필요가 없는 SQL
2. 결과를 받아와야하는SQL
3. ssis 변수를 이용해 sql 쿼리를 실행하는 것





# SSAS

일종의 데이타베이스, Data Mart->OLAP->POWER BI

Power BI = SQL Server Analysis Servieces Tabular Model



#### OLAP (<-->OLTP)

* 사용자가 대용량 데이터를 쉽고 다양한 관점에서 추출 및 분석할 수 있도록 지원하는 비즈니스 인텔리전스(BI) 기술
* 다차원 큐브 형태로 저장하고 측정 항목(measure)과 차원(dimensions)이라는 두 가지 기본 형태로 구분

##### SSAS

* OLAP 서비스를 담당하는 제품

* **다차원 모델**, 테이블 형식 모델, 데이터 마이닝 구조를 가짐
* SSDT(SQL Server Data Tools)로 개발 후 SQL Server로 배포하는 형식


## 과제

* 관계만들기, 관계지정해야함 (Table->create Relationship)

* 측정값 정의(분석하려고 하는 대상값)
* 배포-> 솔루션 탐색기->power bi 실행->데이터가져오기->Analysis Service / 엑셀버튼/ 엑셀에서 데이터->데이터가져오기->데이터베이스에서->Analysis Services에서





* #### 관계설정과 측정값 정의가 핵심

* 데이타 변환: table -> table property-> design

mysql 예제에서 가져왔다고???

데이타 마트를 만드는게 목표, 테이브이 궁극적 목표(Cube)

date, film filmactor, film feature ->snowflake 나머지는 star 테이블



작업정의서-원본테이블보고 관계찾아내-->어떤 열로 서로 연결되어있느냐(열이름이 같아)

ex) film, category, film_category

role=> 주연, 조연으로 쪼개

DimFilmFeature ==> 책에 있어

* avgRentalDuration=>datediff이용 빌려간날짜 반납날짜 시간구하기

* return class

ISNULL()? A: B

ISNULL() ? A :ISNULL() ? C : D

* FactRental

날짜키: 20191222 ---->차원테이블과의 연결 용이 날짜에서 연월일뽑아내서 합쳐서 integer로 변환



데이터형식변환이슈 비유니코드-->유니코드

DATEDIFF("Hh",rental_date,return_date)

ActualRentalDuration > rental_duration * 24 ? "렌탈초과" : "정상"

```
int _Film_Id = 0;
    int _row_rank = 1;

public override void 입력0_ProcessInputRow(입력0Buffer Row)
{
    if (Row.FilmId != _Film_Id)
    {
        _row_rank = 1;
        Row.rowrank = _row_rank;

        _Film_Id = Row.FilmId;
    }
    else
    {
        _row_rank++;
        Row.rowrank = _row_rank;
    }
}
```


### AZURE 사용정리 문서파일 : 
http://www.taeyo.net/Notes/Storage/WindowsAzure%EC%82%AC%EC%9A%A9%EA%B8%B0AtoZ_1%EB%B6%80.pdf
