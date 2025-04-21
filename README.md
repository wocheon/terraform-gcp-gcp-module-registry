# Terraform GCP 모듈 메뉴얼

## GCP 모듈 기본 구조
```
├── 리소스 별 Root 모듈
│   ├── main.tf
│   ├── terraform_command.sh
│   ├── terraform.tfvars
│   └── variables.tf
└── modules
│   ├── GCP 모듈 #1
│   │   ├── main.tf
│   │   ├── output.tf
│   │   └── variables.tf
│   └── GCP 모듈 #2
│       ├── main.tf
│       ├── output.tf
│       └── variables.tf
├── README.md
└── tfstate_delete.sh
```

- 리소스 별 Root 모듈
    - Terraform을 실행하는 entry point 역할
    - 각 파일 용도
        - `main.tf` :  modules 안에 정의된 하위 모듈들을 호출
        - `varialbes.tf` : Root 모듈에서 사용하는 변수들을 정의하는 파일
        - `terraform.tfvars` : variables.tf에서 정의한 변수들에 대해 실제 값을 할당하는 파일
        - `terraform_command.sh` : terraform 커맨드 실행시 --var_file 옵션을 자동할당하여 사용할 수 있는 스크립트             
            - plan/apply/destroy 시 사용 가능
            - `terraform init` 별도 실행 필요

- modules 디렉터리
    - root 모듈에서 재사용 가능한 GCP 하위 모듈들
    - 각 파일 용도
        - `main.tf` : 모듈 안에서 실제 리소스를 생성하거나 구성하는 파일
        - `variables.tf` : 모듈이 외부로부터 받아야 할 입력 변수들을 정의
        - `output.tf` : 모듈이 생성한 리소스의 값 을 출력시에 사용 
            - 출력한 값은 Root 모듈이나 다른 모듈에서 참고 가능

## GCP 리소스 모듈 목록

- 현재 모듈 목록
```
modules
 ┣ gce_disk
 ┣ gce_image
 ┣ gce_instance
 ┣ gce_instance_template
 ┣ gce_snapshot
 ┣ gcp_firewall
 ┣ gcp_iam_role
 ┣ gcp_iam_role_binding
 ┣ gcp_iam_service_account
 ┣ gcp_iam_service_account_key
 ┣ gcp_subnetworks
 ┣ gcp_vpc_network
 ┣ gcs_storage_bucket
 ┣ gke_container_cluster
 ┗ gke_container_node_pool
```