
kubernetes storage manager(쿠버네티스 스토리지 관리자) 이다.

- **개발자:** "나 10GB짜리 저장 공간이 필요해! (PVC 요청)"
- **Trident:** "알았어, 내가 넷앱 스토리지에 가서 10GB 공간 만들어서 바로 연결해줄게! (PV 생성 및 바인딩)"


스냅샷, CSI(Container Storage Interface - 쿠버네티스 표준 규격),
동적 프로비저닝 - 사용자가 요청하는 즉시 스토리지를 생성하고 할당한다.

