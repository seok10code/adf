# ADF - SAP CDC

https://learn.microsoft.com/en-us/azure/data-factory/sap-change-data-capture-introduction-architecture

https://learn.microsoft.com/en-us/azure/data-factory/connector-sap-change-data-capture

### SAP CDC Capabilities / SAP CDC 기능

- The SAP CDC Capabilities in Data Factory use the SAP Operational Data Provisioning framework to replicate the delta in an SAP source dataset.
- Data Factory의 SAP CDC 기능은 SAP ODP(운영 데이터 프로비저닝) 프레임워크를 사용하여 SAP 소스 데이터 세트의 델타를 복제합니다.

### SAP CDC 기능을 사용하는 방법

- SAP CDC 기능의 핵심에는 새로운 SAP CDC 커넥터가 있습니다.
- ODP를 지원하는 모든 SAP 시스템에 연결할 수 있습니다.
- SAP ECC, SAP S/4HANA, SAP BW 및 SAP BW/4HANA가 포함됩니다.
- 애플리케이션 계층에서 직접 작동하거나 프록시로 SAP Landscape Transformation Replication Server(SLT)를 통해 간접적으로 작동합니다.
- 추출하는 데이터에는 물리적 테이블뿐만 아니라 테이블을 사용하여 생성된 논리적 객체도 포함됩니다.
- 테이블 기반 개체의 예로는 SAP ABAP CDS 보기가 있습니다
(SAP Advanced Business Application Programming Core Data Services)

### SAP CDC 아키텍처

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e124162f-2de7-45c2-97a9-97bc665df48d/6af58679-de92-44fc-b286-8024b417d619/Untitled.png)

- SAP CDC 솔루션은 SAP와 Azure 간의 커넥터 입니다.
- SAP 측에는 전체 및 Delta 원시 SAP 데이터를 추출하기 위해 표준 원격 함수 호출 모듈을 통해 ODP API를 호출하는 SAP ODP 커넥터가 포함되어 있습니다.
- Data Factory tumbling window 트리거를 사용하여 대기 시간이 짧고 워터마크를 사용하지 않고 Azure에서 SAP 데이터를 복제함으로써 파이프라인을 실행하고 데이터 흐름을 자주 매핑할 수 있습니다.

### 필요사항

- Data Factory SAP CDC linked service
- SAP CDC source dataset
- pipeline with a mapping data flow activity in which you use the SAP CDC source dataset
- self-hosted integration runtime

### SAP CDC 커넥터는 SAP ODP 프레임워크를 사용하여 다양한 데이터 소스 유형을 추출

- SAP ECC에서 데이터를 추출하여 SAP BW에 로드하도록 구축된 SAP 추출기
- SAP S/4HANA의 새로운 데이터 추출 표준, ABAP CDS 뷰
- SAP BW 및 SAP BW/4HANA의 InfoProviders 및 InfoObjects 데이터 세트
- SAP 애플리케이션 테이블, SAP LT 복제 서버(SLT)를 프록시로 사용하는 경우

- SAP 데이터 소스는 공급자입니다. 공급자는 SAP 시스템에서 실행되어 운영 델타 대기열(ODQ)에서 전체 또는 증분 데이터를 생성합니다.
- Data Factory 매핑 데이터 흐름 원본은 ODQ의 구독자입니다.
