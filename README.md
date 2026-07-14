# AWS 3-Tier Multi-Region Infrastructure (Terraform)

AWS 상에 3-tier 웹 서비스 인프라를 Terraform 코드로 구축한 프로젝트입니다.
멀티 리전 구성과 Pilot Light 방식의 DR(재해복구), 보안 서비스 연동, OIDC 기반 CI/CD까지 포함합니다.

> 3인 팀 프로젝트 | 담당 역할: 아키텍처 설계 및 인프라 구성 (자세한 역할 분담은 아래 참고)

## 아키텍처

<!-- TODO: 아키텍처 다이어그램 이미지 추가 -->
[Architecture](./docs/architecture.png)

## 주요 구성

| 영역 | 사용 서비스 / 구성 |
|---|---|
| 네트워크 | VPC (멀티 리전), 서브넷 분리 (Public / Private / DB) |
| 로드밸런싱 | ALB (HTTPS, ACM 인증서) |
| 컴퓨팅 | EC2 Auto Scaling Group |
| 데이터베이스 | RDS MariaDB Multi-AZ |
| 캐시 | ElastiCache (Redis) |
| CDN / 보안 | CloudFront, WAF (AWS Managed Rules), GuardDuty |
| CI/CD | GitHub Actions + OIDC (액세스 키 없이 AWS 인증) |
| DR | Pilot Light 방식 멀티 리전 재해복구 |
| 운영 | SSM Session Manager (SSH 미사용), IMDSv2 강제 |

## 디렉토리 구조

```
<!-- TODO: 실제 폴더 구조에 맞게 수정 -->
.
├── modules/
├── environments/
└── ...
```

## 배포 방법

```bash
# 사전 준비: AWS CLI 인증 설정, terraform.tfvars 작성 (terraform.tfvars.example 참고)
terraform init
terraform plan
terraform apply
```

## 트러블슈팅

실제 구축 과정에서 겪은 문제와 해결 과정입니다.

### 1. ALB 설정 오류
<!-- TODO: 증상 → 원인 → 해결 순서로 작성 -->

### 2. RDS 엔드포인트 불일치 문제
<!-- TODO: 재생성 후 stale endpoint 참조 이슈 정리 -->

### 3. S3 버킷 이름 충돌
<!-- TODO: 글로벌 유니크 제약으로 인한 충돌과 네이밍 규칙 해결 정리 -->

### 4. 보안 그룹 크로스 폴더 참조
<!-- TODO: 폴더(스택) 간 SG 참조 방식 정리 -->

## 팀 구성 및 역할

| 이름 | 역할 |
|---|---|
| <!-- 이름 --> | <!-- 담당 영역 --> |

> 본 프로젝트의 Terraform 코드 작성에는 AI 도구를 활용했으며,
> 아키텍처 설계·구성 결정·디버깅은 팀에서 직접 수행했습니다.
