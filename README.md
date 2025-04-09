# NAS CPA 연동 메뉴얼

## 1. 랜딩 페이지
귀사에서 제공해주시는 랜딩 페이지 URL 호출 시 ***naskey*** 파라메터 값을 추가로 보내드립니다.

***naskey*** 파라메터 값은 [NAS 서버 호출](#2-nas-서버-호출) 시 사용됩니다.

- 예) 귀사에서 제공해주시는 랜딩 페이지 URL
  ```
  http://test.com/event/123
  ```

- 예) 최종 랜딩페이지 URL
  ```
  http://test.com/event/123?naskey=[임의값]
  ```

## 2. NAS 서버 호출
사용자가 회원가입, 다운로드 등의 요건 완료 시, NAS 서버를 호출합니다.

NAS 서버 호출 방식은 [iframe 태그 삽입 방식](#2-1-iframe-태그-삽입-방식), [img 태그 삽입 방식](#2-2-img-태그-삽입-방식), [서버 to 서버 호출 방식](#2-3-서버-to-서버-호출-방식) 을 지원합니다.

개발 환경에 맞게 선택해서 사용하시기 바랍니다.

### 2-1. iframe 태그 삽입 방식
웹페이지에 iframe 스크립트를 삽입하여, NAS 서버를 호출하는 방식입니다.

적용 방법은 아래 예제를 확인해주시기 바랍니다.

예제 : [`/example`](example)

#### ***예제 설명***
  - [`index.html`](example/index.html) : 랜딩 페이지
    > 랜딩 페이지에서 naskey 값을 확인합니다.
    > 
    > naskey 값이 있으면, 완료 페이지(complete_iframe.html) 에 naskey 값을 같이 보냅니다. 
  
  - [`complete_iframe.html`](example/complete_iframe.html) : 완료 페이지
    > nasCpaComplete() 함수를 호출하여 NAS 서버를 호출합니다. 

### 2-2. img 태그 삽입 방식
웹페이지에 img 스크립트를 삽입하여, NAS 서버를 호출하는 방식입니다.

적용 방법은 아래 예제를 확인해주시기 바랍니다.

예제 : [`/example`](example)

#### ***예제 설명***
- [`index.html`](example/index.html) : 랜딩 페이지
  > 랜딩 페이지에서 naskey 값을 확인합니다.
  >
  > naskey 값이 있으면, 완료 페이지(complete_img.html) 에 naskey 값을 같이 보냅니다.

- [`complete_img.html`](example/complete_img.html) : 완료 페이지
  > nasCpaComplete() 함수를 호출하여 NAS 서버를 호출합니다.

### 2-3. 서버 to 서버 호출 방식
Node, PHP 등의 서버에서 직접 NAS 서버를 호출하는 방식입니다.

사용자의 회원가입/다운로드 등의 요건 완료 시, 아래의 URL을 호출해 주시기 바랍니다.

```
https://api.appang.kr/campaign/complete/cpa?naskey=[랜딩페이지의 naskey 파라메터 값]
```

NAS 서버 호출 후 HTTP200 상태가 리턴되면 정상적으로 호출된것입니다.

결과 데이터는 JSON으로 반환됩니다.

결과 데이터 예시)
```json
{
  "result": 0
}
```

naskey 값이 정상적이지 않을 경우에는, result 값이 -99999 가 반환됩니다.

이 경우, 랜딩페이지에서 받은 naskey 값이 맞는지 확인해주시기 바랍니다.

그 외의 값은 정상 처리된 값입니다.
