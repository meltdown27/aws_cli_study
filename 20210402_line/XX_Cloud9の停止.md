# Cloud9の停止

## 前提
- CloudShellでやる

## 1.1 リージョンの指定
    export AWS_DEFAULT_REGION='ap-northeast-1'

## 1.2 EC2インスタンスタグ名取得
    EC2_INSTANCE_TAG_PREFIX='aws-cloud9-handson-cloud9-linebot'

## 1.3 EC2インスタンスID取得
    ARRAY_EC2_INSTANCE_IDS=$( \
    aws ec2 describe-instances \
        --filters Name=tag-key,Values=Name \
                Name=tag-value,Values=${EC2_INSTANCE_TAG_PREFIX}* \
        --query Reservations[].Instances[].InstanceId \
        --output text \
    ) \
    && echo ${ARRAY_EC2_INSTANCE_IDS}

## 2.1 インスタンスの停止
    aws ec2 stop-instances \
        --instance-ids ${ARRAY_EC2_INSTANCE_IDS}

## 3.1 インスタンスの停止確認
    aws ec2 describe-instances \
        --instance-ids ${ARRAY_EC2_INSTANCE_IDS} \
        --query 'Reservations[].Instances[].State.Name' \
        --output text