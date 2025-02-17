## **💡 Azure에서 동작하는 Web 시스템 개발 정보**

---

## **1. 시스템 개요**
**📌 목표:**
- **Vue 프론트엔드**에서 사용자가 CSV 파일을 업로드
- **C# ASP.NET 백엔드**에서 파일을 처리 (변환, 수정 등)
- 수정된 CSV 파일을 다시 프론트엔드에서 다운로드할 수 있도록 구현
- **Azure 환경에서 동작하는 웹 시스템**으로 개발

---

## **2. 사용 기술 개요**

### **🔹 프론트엔드 (Vue + TypeScript + Vite)**

💡 **프론트엔드는 사용자 인터페이스(UI)를 담당하는 웹 애플리케이션 부분**

- **Vue:** 화면을 구성하고 사용자 입력을 처리하는 JavaScript 프레임워크
- **TypeScript:** JavaScript의 확장판으로, 정적 타입을 지원하여 코드 안정성 증가
- **Vite:** Vue 프로젝트의 개발 및 빌드 속도를 빠르게 해주는 빌드 도구

📌 **프론트엔드 주요 기능:**  
✅ CSV 파일 업로드 UI  
✅ 파일을 백엔드로 전송하는 API 요청  
✅ 백엔드에서 처리된 CSV 다운로드

---

### **🔹 백엔드 (C# ASP.NET MVC + REST API + CSVHelper)**

💡 **백엔드는 프론트엔드에서 받은 데이터를 처리하고, 변환된 데이터를 반환하는 역할**

- **ASP.NET MVC:** Microsoft의 웹 애플리케이션 프레임워크
- **REST API:** 프론트엔드와 백엔드 간의 데이터 통신을 담당
- **CSVHelper:** C#에서 CSV 파일을 쉽게 읽고 쓸 수 있도록 도와주는 라이브러리

📌 **백업데드 주요 기능:**  
✅ 프론트엔드에서 받은 CSV 파일을 서버에 저장  
✅ CSVHelper를 이용해 데이터 변환 및 처리  
✅ 변환된 파일을 다시 프론트엔드로 전송

---

### **🔹 Azure App Service**

💡 **Azure에서 웹 애플리케이션을 실행하는 클라우드 서비스**

- 백엔드 API 및 웹 시스템을 Azure 클라우드에서 배포 및 운영 가능
- 확장성 및 보안 기능을 제공
- CI/CD를 활용하여 자동 배포 가능

📌 **Azure에서의 역할:**  
✅ 웹 API 및 파일 처리를 위한 서버 운영  
✅ API 호출 및 데이터 처리 수행  
✅ 클라우드 환경에서 서비스 관리

---

## **💡 Vite로 Vue 프로젝트 시작**

## 📌 **명령프롬프트**

**Vite 설치 및 프로젝트 생성**   
npm create vite@latest my-vue-app --template vue-ts

**my-vue-app** → 원하는 프로젝트 폴더 이름으로 변경 가능  
**--template vue-ts** → Vue + TypeScript 템플릿 사용

**의존성(Dependencies) 설치**  
cd my-vue-app  
npm install

**개발 서버 실행**  
npm run dev

**HTTP 요청 라이브러리 선택사항**  
npm install axios  
👉 서버와 통신할 때 fetch보다 더 많은 기능을 제공하는 라이브러리입니다.  
👉 예제:  
import axios from 'axios';  

axios.get('https://api.example.com/data')  
.then(response => console.log(response.data))  
.catch(error => console.error(error));  