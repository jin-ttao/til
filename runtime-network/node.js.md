내 로컬 vs code에서 특정 파일에서만 node version을 올릴 수 있어? 다른 파일에서는 node 버전을 유지하고.
.nvmrc 파일 사용 (추천) / 프로젝트별 설정 방법 / VS Code 워크스페이스 설정
nvm

2단계에서 vs code 터미널에서 원하는 Node 버전 설치하면, 이미 있었던 프로젝트들은 node version이 18.16인데 영향을 받는거 아니야? 영향을 받지 않는다면 그 이유도 알려줘.
기존 프로젝트들은 영향을 받지 않습니다. 그 이유를 설명해드리겠습니다:
	1.	nvm의 작동 방식
	•	nvm은 여러 Node.js 버전을 독립적으로 관리합니다
	•	각 버전은 별도의 디렉토리에 설치됩니다
버전 전환 메커니즘
	•	nvm은 심볼릭 링크나 PATH 조정을 통해 Node 버전을 전환합니다
	•	각 프로젝트의 Node 버전은 다음 우선순위로 결정됩니다:
	a.	.nvmrc 파일이 있는 경우 해당 버전
	b.	수동으로 nvm use 명령을 실행한 경우 지정된 버전
	c.	전역으로 설정된 기본 버전

```
nvm list
```
![runtime-nvm-1](/assets/runtime-nvm.png)
![runtime-nvm-2](/assets/runtime-nvm-2.png)
![runtime-nvm-3](/assets/runtime-nvm-3.png)

참고
https://mong-blog.tistory.com/entry/NVM-%EB%B2%84%EC%A0%84-%EC%84%A4%EC%A0%95-%EC%89%BD%EA%B2%8C-%ED%95%98%EA%B8%B0with-nvmrc
