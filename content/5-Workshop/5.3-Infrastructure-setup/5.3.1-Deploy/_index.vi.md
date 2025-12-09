---
title: "Triển khai Hạ tầng"
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

Nguồn: [https://github.com/Aohk22/fcj-1-file-analyzer/tree/main](https://github.com/Aohk22/fcj-1-file-analyzer/tree/main)

## Các bước triển khai

Chạy quy trình Terraform và Image Builder theo thứ tự:

```bash
terraform init
terraform fmt
terraform validate
```

Tạo tài nguyên Image Builder:

```
./plan_imagebuilder.sh
terraform apply plan.tfplan
```

Mã nguồn script:

```
#!/usr/bin/env sh

terraform plan -out=img_builder.tfplan \
  -target=aws_imagebuilder_infrastructure_configuration.imgbuilder_infra_config \
  -target=module.image_builder_pipeline_fhandle \
  -target=module.image_builder_pipeline_fquery \
  -target=module.instance_profile_imgbuilder \
  -target=aws_internet_gateway.igw_main \
  -target=aws_route_table.route_table_public \
  -target=aws_route_table_association.rt_associate_sn_pub_1 \
  -target=aws_iam_role_policy_attachment.imgbuilder_ec2_profile \
  -target=aws_iam_role_policy_attachment.imgbuilder_ec2_ecr_profile \
  -target=aws_iam_role_policy_attachment.imgbuilder_ssm_core
```

Build AMI:

```
./start_image_pipeline.sh
# wait until AMI build completes
```

![](/images/5-Workshop/5.3-Infrastructure-setup/5.3.1-Deploy/screen1.jpg)

Mã nguồn script, script này kiểm tra trạng thái qua AWS API:

```
#!/usr/bin/env bash

arn_build_versions=()
arn_pipelines=(
  "arn:aws:imagebuilder:ap-southeast-2:005716755011:image-pipeline/fhandle-img-pipeline"
  "arn:aws:imagebuilder:ap-southeast-2:005716755011:image-pipeline/fquery-img-pipeline"
)

echo "Sending pipeline requests."
for arn in "${arn_pipelines[@]}"; do
  result=$(
    aws imagebuilder start-image-pipeline-execution \
      --image-pipeline-arn "${arn}"
  )
  arn_build_versions+=("$(echo "${result}" | jq -r '.imageBuildVersionArn')")
done

for arn in "${arn_build_versions[@]}"; do
  echo "$arn"
done

# wait for image.
for build_version in "${arn_build_versions[@]}"; do
  echo "Polling ${build_version}..."
  prev_status="_none"
  while
    status="$(aws imagebuilder get-image --image-build-version-arn "$build_version" | jq -r '.image.state.status')"
    if [[ "$prev_status" != "${status}" ]]; then
      echo "Status: ${status}"
      prev_status="${status}"
    fi
    sleep 5
    [[ "$status" != "AVAILABLE" ]]
  do true; done
done
echo "Image build complete."
```

Triển khai toàn bộ hạ tầng:

```
terraform plan -out=plan.tfplan
terraform apply plan.tfplan
```
