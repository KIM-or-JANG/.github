# Calendar-project

캘린더로 일정을 관리하며 특정그룹과 일정을 공유할수있는 어플리케이션, 특정 그룹마나 방을 나눌수 있고 쪽지, 댓글 등으로 간단한 커뮤니케이션이 가능한 어플리케이션

> 프로젝트 노션 페이지
- [https://www.notion.so/5-9e3042ff4b354ce7b20e3a8095b29e98](https://www.notion.so/KIM-or-JANG-4f9f4e850c3d40c487511c444ab9eb4d)
<br/>

> **서비스 소개**
#
- Kim-or-JANG의 Calendar는 다양한 사람들이 모여 함께 사용 할 수있는 `공유 캘린더` 입니다
- 사용자는 다양한 모임의 `방을 만들어 일정을 공유하고 관리`할 수 있습니다.
- 사용자는 본인의 메인 페이지에서 `각 모임의 일정과 개인 일정을 한눈에` 모아 볼 수 있습니다.
<br/>
<br/>
<br/>

> **서비스 이용해보기**
#
- https://
<br/>
<br/>
<br/>

> **서비스 주요기능**
#
- 일정관리, 공유기능, 커뮤니티 어플리케이션
- 캘린더
- TodoList
- 친구 기능 
<br/>
<br/>
<br/>

>**기술스택**
#
<br/> <img src="https://img.shields.io/badge/aws-232F3E?style=for-the-badge&logo=aws&logoColor=white"> <img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=Java&logoColor=white"/> <img src="https://img.shields.io/badge/gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white"/>  <img src="https://img.shields.io/badge/SpringSecurity-6DB33F?style=for-the-badge&logo=SpringSecurity&logoColor=white"/> <img src="https://img.shields.io/badge/SpringBoot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white"/> <img src="https://img.shields.io/badge/JsonWebTokens-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white"> <img src="https://img.shields.io/badge/AmazonRDS-527FFF?style=for-the-badge&logo=AmazonRDS&logoColor=white"/> <img src="https://img.shields.io/badge/redis-DC382D?style=for-the-badge&logo=redis&logoColor=white"/> <img src="https://img.shields.io/badge/AWS Route 53-FF6C37?style=for-the-badge&logoColor=white"> <img src="https://img.shields.io/badge/https-527FFF?style=for-the-badge"> <img src="https://img.shields.io/badge/AmazonEC2-FF9900?style=for-the-badge&logo=AmazonEC2&logoColor=white"/> <img src="https://img.shields.io/badge/AmazonS3-569A31?style=for-the-badge&logo=AmazonS3&logoColor=white"/> <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white"/> 
<br/>
<br/>
<br/>

> **아키텍처**
#
<img width="1181" alt="스크린샷 2023-06-26 오전 7 50 15" src="https://github.com/Jangkiwoong/Node.js.login/assets/110136582/214105f8-2bd6-4706-b605-8275e3244601">
<br/>

> **기술적 의사결정**
#
|사용기술|의사결정|
|:---:|:---|
|Amazon Route53|도메인을 등록하고 관리하기 위해 채택|
|Amazon Load Balancer|https로 리다이렉션을 위해 채택|
|Amazon S3|개인 프로필 사진이나 방 프로필 사진에 대한 이미지 파일을 업로드하고 CI/CD 코드 저장을 위해 채택|
|AWS CodeDeploy|CI/CD를 위해 S3에 저장된 코드를 재배포 하기위해 채택|
|QueryDsl|공휴일 데이터, 개인 일정을 편집해서 내려주기 위해 채택|
<br/>
<br/>
<br/>

> **트러블 슈팅**
#
<details>
<summary>불필요한 데이터 응답</summary>
<div markdown="1">
    
|진행  순서|내용|
|:---:|:---|
|문제|데이터 요청시 불필요한 내용들이 같이 응답됨 (예 : roomManager, userPassword, userRole)|
|시도|필요한 데이터를 List로 내려받아 for문을 통해 ResponseDto로 편집해서 내려주지만 데이터량이 많을 경우 시간이 너무 소요될 가능성이 있음|
|해결|관련 글을 찾아보던 도중 QueryDSL에서 Projections.bean()을 통해 ㅁㄴ이ㅏㅓ미ㅏ임ㅇ(다시 적어야함)|

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "iam:PassRole",
                "ec2:CreateTags",
                "ec2:RunInstances"
            ],
            "Resource": "*"
        }
    ]
}
</div>
</details>


<details>
<summary>이미지 로딩시간 지연</summary>
<div markdown="1">
    
|진행  순서|내용|
|:---:|:---|
|문제|S3에 저장되어 있는 이미지 용량이 너무 커 페이지에서 이미지 로딩 시간이 지연됨|
|시도|S3에 저장되어 있는 이미지 용량이 너무 커 페이지에서 이미지 로딩 시간이 지연됨 AWS Lamda를 사용하여 이미지 리사이징을 하려 했으나 S3의 용량이 커진다는 문제와 원본 사진을 저장할 필요가 없어 라이브러리를 사용|
|해결|marvin 라이브러리를 사용하여 2MB에서 976KB 로 이미지 용량 축소|
</div>
</details>
<br/>
<br/>
<br/>

> **ERD**
#
![ERD](https://github.com/KIM-or-JANG/Calendar-BE/assets/110136582/e5cae9e5-d9ca-4365-b6f7-2ab2a43ad614)
<br/>
<br/>
<br/>

> **시기**
> 
- 프로젝트 진행 기간
    - 2023.12 ~ 2023.1 (8주)
