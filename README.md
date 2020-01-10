# db-study
> [NoSQL 철저 입문](https://book.naver.com/bookdb/book_detail.nhn?bid=9956311)  

* 관계형 데이터베이스  
    관계형 데이터베이스는 데이터와 데이터 간의 관계를 묘사하기 위해 관계형 대수학을 사용하는 형식 수학 모델에 기반을 두고 있으며 데이터 구조의 논리 구성을 물리적인 저장 구조와 분리했다.  
* 관계형 데이터베이스 관리 시스템(RDBMS)  
    데이터를 관리하고 애플리케이션 사용자들이 데이터를 읽고 추가/갱신/삭제하는 것을 허용하는 다수의 프로그램으로 구성된 애플리케이션이다. 이전 데이터베이스 모델에서는 데이터를 사용하기 위해 매번 프로그램을 개발해야했던 것과는 달리 RDBMS에서는 SQL이라는 공통 언어를 사용한다.    

    * 관계형 데이터베이스 관리 시스템의 구조  
        RDBMS를 구현하기 위한 최소 요구 사항 4가지가 합쳐져 RDBMS의 핵심 데이터 관리와 데이터 조회 서비스를 제공한다.   

        1. 스토리지 관리 프로그램  
            데이터베이스 시스템은 장기기억 저장 장치로 디스크와 플래시 드라이브에 데이터를 저장한다. 어떤 유형의 저장 시스템이 사용되든 RDBMS는 데이터 조각이 저장된 위치 하나하나를 모두 추척해야한다. 테이프 기반 스토리지에서는 데이터를 검색할 때 순차적으로 찾아야했지만 디스크와 플래시 드라이브는 그런 제약이 없기 때문에 RDBMS 설계자들은 인덱스를 생성하여 데이터 조회 방식을 개선했다. **인덱스**란 데이터베이스에 저장된 데이터 블록의 위치 정보를 포함하는 데이터 집합을 말한다.  
            데이터 위치를 추적하는 것 외에도 데이터 위치를 최적화하고, 데이터를 압축하여 저장 공간을 절약하고, 데이터 블록을 복사해서 디스크 결함으로 데이터 블록이 소실되지 않도록 예방한다.  

        2. 메모리 관리 프로그램  
            RDBMS는 메모리에서 데이터를 관리하는 책임도 있다. 메모리 관리 요소는 필요한 경우에 데이터를 메모리로 가져와 유지하고, 더는 필요하지 않을 때 메모리에서 삭제하거나 추가 데이터가 저장될 공간을 마련하는 일을 수행한다. 메모리에서 데이터를 읽어 들이는 것이 디스크에서 읽어 들어것 보다 횔씬 빠르고, 메모리를 효율적이고 효과적으로 사용하느냐에 따라 RDBMS의 전체 성능이 크게 좌우된다.  

        3. 데이터 사전  
            데이터 사전은 데이터베이스에 저장된 데이터 구조 정보를 추적하는 RDBMS의 한 부분이다. 데이터 사전은 데이터베이스를 구성하는 스키마, 테이블, 컬럼, 인덱스, 제약조건, 뷰에 대한 정보를 포함한다.  

            * `스키마` : 테이블, 뷰, 인덱스, 데이터 집합에 대한 구조이며 독립된 애플리케이션의 주요 유형에 따라 스키마를 분리하는 것이 일반적이다.     
            * `테이블` : 엔티티 데이터를 담고 있는 데이버베이스 구조이다. 엔티티는 RDBMS가 지원하는 작업이나 비지니스와 연관된 물리적, 혹은 논리적인 실체를 묘사한다.  
            테이블은 컬럼으로 구성된다. 컬럼에는 한 단위의 정보가 포함되어 있으며 저장된 데이터가 어떤 유형인지 파악하기 위해 데이터 타입 정보를 갖고 있다.  
            * `인덱스` : 데이터베이스에 저장된 데이터 블록의 위치 정보를 포함하는 데이터 집합으로 데이터 조회 속도를 향상시킨다.  
            * `제약 조건` : 컬럼에 들어가는 데이터값을 제한하는 규칙을 말한다. 제약 조건은 데이터 표현 방식과 엔티티에 대한 비지니스 규칙을 기준으로 만드는 것이 일반적이다.  
            * `뷰` : 하나 이상의 테이블에서 관련된 컬럼이나 컬럼에 있는 데이터에 대한 계산한 값들을 모아놓은 것이다. 뷰는 사용자가 볼 수 있는 데이터에 제한을 두는 용도나 여러 테이블의 데이터를 결합해 하나의 뷰로 만들어 보여주는 용도로 사용될 수 있다.   

        4. 질의 언어  
            RDBMS의 질의 언어는 두 가지 유형의 동작을 수행하는데, 하나는 데이터 구조를 정의하는 것이고(CREATE, ALTER, DROP, ...), 다른 하나는 데이터를 조작하는 것(SELECT, UPDATE, DELETE, INSERT)이다.  
* RDBMS를 사용하는 애플리케이션의 구조  
    * 사용자 인터페이스 : 사용자의 작업 처리를 지원한다.  
    * 비지니스 로직 : 계산을 수행하고 비지니스 규칙을 확인하는 프로그램의 한 부분이다.  
    * 데이터베이스 코드 : SQL을 말하며 사용자가 사용자 인터페이스로 수행하는 작업에 따라 사용하는 문장이 달라진다.  

* 관계형 데이터베이스의 한계  
    웹의 출현으로 관계형 데이터베이스의 한계가 문제로 드러나게 되었다. 상당히 큰 규모의 데이터와 극도로 많은 수의 사용자를 대상으로 작업하는 웹 애플리케이션 개발자는 대용량 데이터의 읽기와 쓰기 작업, 빠른 응답 시간, 높은 가용성을 지원해야하는데 이런 것들을 관계형 데이터베이스로 실현하기가 어려웠다.  
