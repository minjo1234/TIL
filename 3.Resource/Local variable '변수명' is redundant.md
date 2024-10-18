 불필요한 코드기 때문에 바꾸라는 내용

```
String imageData = webClient.get()  
        .uri("/iaas/api/images")  
        .header("Authorization", "Bearer " + accessToken)  
        .retrieve()  
        .bodyToMono(String.class)  
        .block();  
  
return imageData;
```

```
return webClient.get()  
        .uri("/iaas/api/images")  
        .header("Authorization", "Bearer " + accessToken)  
        .retrieve()  
        .bodyToMono(String.class)  
        .block();
```

imageData라는 변수가 불필요하게 사용돼서 삭제하였음

find 찾는 과정
converter 1.imageNames까지를 얻는과정  converImageData 
imageNames를 가공하는 메서드 makeInsertData 

json -> converter -> db 
json -> imageinfo -> Aria_Resources -> db (얘를 써야하는 이유가 명백하면 써도됌..)
json -> Aria_Resources -> db 

AriaFetchService에서는 ariaResources밖에 호출하지못함

JsonNode vs JsonParser 를 사용하는 방법의 차이..

JsonNode 

JsonParser를 사용하면 JSON 문자열을 간단하게 JsonElement 객체로 변환이 가능하다.
이를 통해 JSON 데이터를 처리할 수 있다.
JsonNode 를 사용하면 복잡한 JSON 파일에서 간단하게 접근할 수 있다는 장점이 존재한다.

Set을 사용하면 중복되는값 없이 정보를 저장할 수 있다.

----


settings.gradle

rootProject.name = 'clovirone-base'  
include 'clovircm-domain'  
include 'clovircm-web'  
include 'clovirone-vmware'  
include 'clovirone-vmware-infra'  
include 'license-generator'  
include 'clovirone-data-sample'  
include 'plugin-sdk'  
include 'plugin-example'  
include 'plugin-mobis'  
include 'clovirone-jenkins'  
include 'plugin-khnp'  
include 'plugin-khnp'

build.gradle
에서 사용하는 모듈들 다시 명시