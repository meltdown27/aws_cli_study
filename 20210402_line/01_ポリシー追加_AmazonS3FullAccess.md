# ポリシー追加（AmazonS3FullAccess）

## 前提
- handson-cloud9-linebot-roleというCloud9用のロールを作る
- ロール：handson-cloud9-linebot-roleをCloud9で作成されたEC2にAttach
- CloudShellでやる

## 1.1 IAMロール名
    IAM_ROLE_NAME='handson-cloud9-linebot-role'

## 1.2 IAMポリシー名
    IAM_POLICY_NAME='AmazonS3FullAccess'

## 1.3 ポリシーARNの取得
    IAM_POLICY_ARN=$( \
    aws iam list-policies \
        --scope AWS \
        --max-items 1000 \
        --query "Policies[?PolicyName==\`${IAM_POLICY_NAME}\`].Arn" \
        --output text \
    ) \
    && echo "${IAM_POLICY_ARN}"

## 2.1 ポリシーのアタッチ
    aws iam attach-role-policy \
        --role-name ${IAM_ROLE_NAME} \
        --policy-arn ${IAM_POLICY_ARN}

## 3.1 確認
    aws iam list-attached-role-policies \
        --role-name ${IAM_ROLE_NAME} \
        --query "AttachedPolicies[?PolicyName == \`${IAM_POLICY_NAME}\`].PolicyName" \
        --output text