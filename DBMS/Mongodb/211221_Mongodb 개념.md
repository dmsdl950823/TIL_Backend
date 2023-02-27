# MongoDB 란?

MongoDB 는 최신 소프트웨어 애플리케이션에 자주 사용되는 오픈소스 비관계형(문서기반) 데이터베이스 입니다. MongoDB Inc 에 의해 개발되었고, 많은 버전을 출시해왔습니다.

MongoDB 는 C++, Go, Javascript, Python 등을 개발 언어로 사용하며, 많은 웹 애플리케이션의 언어를 지원합니다. 그중에서 Javascript 를 주로 지원하는데, mongodb 데이터 형식이 JS 로 변경하기 쉽기 때문입니다.

Mongodb 데이터베이스는 높은 퍼포면스, 사용성, 규모 등에서 활용도가 높으며, cross-platform 이므로 개발자가 여러 플랫폼에서 쉽게 개발할 수 있습니다.


## MongoDB 구조

MongoDB 는 주로 우리가 개발할 영역을 선택할 수 있는 데이터베이스의 타입을 가지고있습니다. (머선소리)

### 로컬 개발 (Local Developement)

개발자들은 로컬 개발이나 독립적인 애플리케이션을 위해서 mongodb 를 사용할 수 있습니다. 특정 버전의 mongodb 를 이용해 to-do 리스트와 캘린더 같은 앱들을 ios/android 플랫폼에서 만들 수 있습니다. mongodb local development 환경을 제한없이 저장장치에서 사용 가능합니다.

## 클라우드 개발 (Cloud Development)

클라우드 개발이나 분리된 개발 웹앱/웹기반 모바일/데스크탑 앱 환경을 위해서 cloud database 버전의 mongodb (Mongodb Atals) 를 사용할 수도 있습니다. 클라우드 개발환경을 100개의 연결과 상호작용하고 512MB 분량의 클라우드 데이터 저장공간을 사용할 수 있습니다.

개발한 애플리케이션의 규모가 켜질경우 mongodb atlas 는 요청에 따라 크기를 늘릴 수도 있습니다.

## MongoDB 내부

둘 중 어떤 타입이든 같은 데이터베이스 구조를 갖지만, 차이점은 데이터 저장공간의 방식입니다. 하나는 저장을 위해 OS 를 포함하지만 다른 하나는 클라우드를 위해 API 를 사용합니다.

* 각 mongodb database 는 *컬렉션*을 갖습니다. mysql database 의 테이블과 비슷합니다.
* 각각의 컬렉션은 레코드(문서 형식)를 갖습니다.
* 각 문서는 JSON 오브젝트처럼 키-값(key-value) 쌍으로 이루어져있습니다.
* 키-값 쌍은 레코드를 정의합니다.

``` json
{
  "_id": "5ewr3122rwer12323123",
  "name": "John Doe" , 
  "username": "JohnsDoe123", 
  "email": "johndoe123@abc.xyz"
}
```

각각의 이 문서들은 objectId라고 불리는 id 값으로 특별하게 오브젝트를 식별할 수 있습니다.  (`"_id": "5ewr3122rwer12323123"`)  이 값은 strings, arrays, objects 등 다양한 형식을 포함할 수도 있습니다. 

우리는 기존 원래 데이터 모델을 변경 없이 새로운 버전으로 수정할 수 있습니다. 수정되면 각각의 문서는 이전 버전의 문서와는 다릅니다. 그리고 또한 새로운 모델을 

그러므로 각 문서는 이전 버전의 문서와는 다르며, nodejs 개발 환경의 mongoose 같은 ORM을 사용할 때 새로은 모델을 수정합니다. 이러한 방법으로 필요에 의해 mongodb 의 구조를 변경시킬 수 있습니다.

단일 레코드 작업 및 여러 레코드에 CRUD 작업을 위한 메서드를 사용할 수 있으며, 애플리케이션에서 사용할 수 있는 여러 쿼리 방법을 사용할 수 있습니다.

``` js
find()      // Find documents of a collection.
save()      // Save document to a collection.
updateOne() // Updates a document.
delete()    // Delete method deletes a document.
findByIdAndDelete()  // Finds a document for given ObjectID and deletes it.
findByIdAndUpdate()  // Finds a document for given ObjectID and updates it with given values.
deleteOne() // Deletes the first document from the selected resultset/collection.
```

관계형 데이터베이스와는 반대로 mongodb 의 쿼리는 많은 접근을 필요로 합니다. 그리고 외래키 속성을 사용하지 않습니다. 

Opposed to relational databases the mongodb's querying takes easy approach.
And no foreign keys used for the data delete and updates so collisions handling with on-update and on-delete actions are not needed but can implement a solution by developer's side and it is possible.

## MongoDB 가 제공하는 것들

## 주로 사용하는 곳