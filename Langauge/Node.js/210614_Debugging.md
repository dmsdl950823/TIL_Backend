# Node.js 디버깅

모든 프로그래밍 코드에는 언제나 버그가 있습니다. 쉽게 찾을 수 있는 버그도 있으나, *메모리 누수* 나 *잘못된 변수 참조* 등 찾기 어려운 버그도 있으므로, 디버깅 하는 방법은 반드시 익혀두어야 합니다.

# 노드의 스택 트레이스

노드는 실행 중 에러가 발생하면 **에러에 대한 스택 트레이스를 출력**하고 프로세스를 종료합니다. 에러 스택 트레이스를 확인하면 어디서 무슨 에러가 발생했는지 알 수 있습니다. 또한 에러가 발생한 코드의 호출 관계를 추적해 보여주므로, 에러를 확인하는데 유용합니다. 노드에서 에러가 발생하면 가장 먼저 에러 스택 트레이스를 확인해야합니다.

`clog` 모듈을 사용하는것도 편리하다.

``` bash
    $ npm install clog
```

``` js
    const clog = require('clog')
    clog('example', '...')
    clog.log('로그성 메세지')
    clog.info('정보성 메세지')
    clog.warn('경고성 메세지')
    clog.error('에러 메세지')
    clog.debug('디버깅용 메세지')
```

# 노드 인스펙터를 이용한 디버깅

로직이 복잡하거나 쉽게 추적되지 않는 버그는 찾기 어렵고, 매번 로그를 출력하여 확인하는 방법은 불편합니다.

> GDB :: GNU Project Debugger - 실행 도중에 내부에서 무슨일이 벌어지고있는지 확인할 수 있는 도구입니다

노드는 GDB 를 이용한 디버그 모드를 지원합니다. 노드를 디버그 모드로 실행하면 디버거로 연결해 디버깅 할 수 있습니다.

[노드 인스펙터](https://github.com/nodejs/node-inspect) 는 웹킷 기반 **웹 브라우저(safari, chrome) 에 있는 개발자 도구에 기반을 둔 노드 디버거**입니다. 클라이언트 자바스크립트 개발에서 웹킷의 개발자 도구를 사용해본 경험이 있다면 익숙하게 사용할 수 있습니다.

노드 인스펙터를 이용하면 노드 앱을 수정하지않고도 실행중에 중단점을 지정해 각 객체의 상태를 확인할 수 있어 편리합니다.

``` bash
    # 노드 인스펙터는 커맨드라인에서 사용합니다.
    $ npm install --global node-inspect

    $ node --debug-brk <testfile>  # 디버거 라인에서 진행하지않고 대기
    $ node --debug <testfile>   # 종료하지 않고 계속 진행하면서 디버깅을 하는 방법
    # $ node --inspect <file>   # Chrome inspector protocol 전용

    $ node-inspector &   # 노드 인스펙터 실행
```

디버깅을 위해 코드에 중단점 (breakpoint) 를 설정할 수도 있습니다.

breakpoint 를 지정하고 `Pause the script execution` 버튼(⏸) 을 실행시키면 코드가 이어서 실행되다, 해당 라인에서 중지됩니다.

| 버튼 이름                          | 설명                                                    |
| ---------------------------------- | ------------------------------------------------------- |
| `Pause the script execution` (⏸)   | 스크립트 중단 / 재실행                                  |
| `Step over next function call` (🔂) | 한줄씩 차례대로 실행 - 현재 소스와 같은 계층에서만 이동 |
| `Step into next function call` (⬇) | 함수의 내부까지 이동                                    |
| `Step out current function` (⬆)    | 함수의 내부까지 이동                                    |
| `Deactive all breakpoints`         |                                                         |
|                                    |                                                         |
| `Call Stack` Tab                   | 함수의 호출 스택을 보여줌                               |
| `Scope Variable` Tab               | 현재 멈춰진 부분에서 접근할 수 있는 변수를 보여줌       |
| `Script` Tab                       | 콘솔 확인 - 다양한 테스트 가능                          |
