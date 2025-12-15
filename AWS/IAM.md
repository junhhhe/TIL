## AWS IAM (Identity and Access Management)

AWS IAM은 AWS 리소스에 대한 접근 권한을 안전하게 관리하며, **최소 권한 원칙**을 구현

---

### 1. IAM 핵심 구성 요소

| 구성 요소 | 역할 | 사용 시점 |
| :--- | :--- | :--- |
| **User** | AWS에 접근하는 개별 사용자 (영구 자격 증명) | 개발자, 관리자 등의 로그인 및 API 접근 |
| **Group** | 동일 권한을 가진 User들의 집합 | 권한 일괄 관리 |
| **Role** | 권한을 위임받는 주체 (임시 자격 증명) | EC2가 S3에 접근, 계정 간 권한 위임 |
| **Policy** | 권한 정의 문서 (JSON) | User, Group, Role에 연결되어 권한을 부여 |

### 2. IAM Policy (권한 정책) 상세 분석

#### 2.1. Policy 핵심 요소

* **Effect:** `Allow` (허용) 또는 `Deny` (거부).
* **Action:** 허용/거부할 AWS 서비스의 특정 작업 (예: `s3:GetObject`).
* **Resource:** 대상이 되는 리소스 (ARN 형식, 예: `arn:aws:s3:::my-bucket/*`).

#### 2.2. 명시적 거부의 우선순위

* IAM은 기본적으로 모든 것을 **암묵적으로 거부(Implicit Deny)**
* **명시적 거부 (`Explicit Deny`)**는 모든 허용 규칙보다 **항상 우선**

### 3. IAM Role (역할)의 중요성

* **임시 자격 증명:** Role은 Access Key 대신 임시 자격 증명을 사용하여 보안을 강화
* **신뢰 정책 (Trust Policy):** 이 Role을 **누가 맡을 수 있는지(Principal)** 정의 (예: `ec2.amazonaws.com` 서비스)

### 4. 보안 모범 사례 (Best Practices)

1.  **루트 계정 사용 금지:** MFA를 설정하고 일상적인 작업에는 사용하지 않음
2.  **최소 권한 원칙:** 필요한 최소한의 권한만 부여
3.  **MFA 필수 적용:** 모든 User에게 다중 인증(MFA)을 적용하여 보안을 강화
4.  **Role 사용:** EC2 인스턴스 등 AWS 서비스에는 Access Key 대신 IAM Role을 할당하여 권한을 부여
