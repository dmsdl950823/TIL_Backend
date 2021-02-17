- [1. AWS](#1-aws)
  - [1.1. 클라우드 서비스란?](#11-클라우드-서비스란)
  - [1.2. EC2 - Elastic computer cloud](#12-ec2---elastic-computer-cloud)
    - [1.2.1. 특징](#121-특징)
  - [1.3. EC2 소스 생성 단계](#13-ec2-소스-생성-단계)
  - [1.4. Application distribute](#14-application-distribute)
  - [1.5. EC2 Server 제거](#15-ec2-server-제거)
    - [1.5.1. security group remove](#151-security-group-remove)
    - [1.5.2. key pair remove](#152-key-pair-remove)
    - [1.5.3. double check if it is removed](#153-double-check-if-it-is-removed)
  - [1.6. Concerned images](#16-concerned-images)
# 1. AWS

## 1.1. 클라우드 서비스란?
 물리적 자원/논리적 자원을 Amazon에서 대여해주는 서비스.
 
 물리적 자원 관리를 할 필요 없이 자동으로 관리해줌.


## 1.2. EC2 - Elastic computer cloud
물리적인 자원을 대여해주는 AWS의 대표적인 서비스

### 1.2.1. 특징

```
  - 크기(CPU, Memory, DISC)을 설정한 자원(소스)을 하나 생성하고 여러 서버를 생성할 수 있도록 함
  - 필요한 만큼 자원을 대여하여 사용
  - OS 선택 가능 (UBUNTU, CentOS 등)
```


## 1.3. EC2 소스 생성 단계

1. ```콘솔에 로그인``` 또는 ```내 계정``` - ```Amazon Management Console``` 클릭하여 콘솔 접근
2. 내가 사용하고있는 지역과 가장 가까운 location으로 설정 - 응답 속도 빠름
3. ```AWS 서비스 찾기``` - 키워드 ```EC2``` 입력 - 클릭 ```클라우드의 가상 서버```
4. ```인스턴스``` 클릭
5. ``` 인스턴스 시작 ``` 클릭
6. Amazon Linux (제일 기본) - 선택
7. 인스턴스 유형 선택(기본) - 다음
8. 인스턴스 세부정보 구성 - ```인스턴스 개수``` : 1 - 스토리지 추가 선택
9. 디스크가 있어야 서버를 구축할 수 있음  -  스토리지 추가
10. 태그 추가 (사용할 경우 추가 [선택사항])
11. 보안 그룹 구성 (생성한 인스턴스에 어떤포트를 열지 지정, ip 접근 허용 지정)< br/>
```그룹이름```, ```설명```, ```포트범위```, ```소스``` 입력
12. 인스턴스 시작 검토 (설정한 값 확인)
13. 기존 키 페어/새 키 페어 생성(ssh접근을 위한 키 생성) - ```키 페어이름``` 설정 - ```키 페어 다운로드```
14. ```인스턴스 시작``` 클릭
15. 생성 완료


## 1.4. Application distribute

1. 다운로드한 키젠 파일의 권한을 열어준다

``` sh
    $ cd <keyPair directory>
    $ chmod 400 keyPair.pem
```   

2. key를 사용하여 ssh 연결

``` sh
    $ ssh -i keyPair.pem ec2-user@ < asssigned ip address >
```

1. 외부에 포트 열기
   > ```작업``` - ```네트워킹``` - ```보안그룹 변경``` 의 포트 등록 여부 확인<br />
```보안그룹``` - ```인바운드``` 탭 - ```편집``` - ```규칙 추가``` - 포트범위 입력(ex 30000)


## 1.5. EC2 Server 제거

1. ```keyPair.pem``` 파일 삭제
2. ```작업``` - ```인스턴스상태``` - ```종료```

### 1.5.1. security group remove

> ```[네트워크 및 보안]``` - ```보안그룹``` - ```작업``` - ```보안그룹 삭제``` - ``예``` 클릭

### 1.5.2. key pair remove

> ```[네트워크 및 보안]``` - 삭제할 키 체크 ✔ - ```Delete``` 클릭

### 1.5.3. double check if it is removed

> ```[EC2 대시보드]``` - 상태 체크



## 1.6. Concerned images

...








