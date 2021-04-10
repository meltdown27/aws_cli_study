# IAMポリシードキュメントの作成

## 1.1 リージョンの指定
    export AWS_DEFAULT_REGION='ap-northeast-1'

## 1.2 ポリシードキュメント用ディレクトリの指定
    DIR_IAM_POLICY_DOC="${HOME}/environment/conf-handson-cli-lambda"

## 1.2.1 ディレクトリがあるか確認
    ls -d ${DIR_IAM_ROLE_DOC}

### 1.2.2 ない場合
    mkdir -p ${DIR_IAM_ROLE_DOC}

## 1.3 ポリシードキュメント名
    IAM_POLICY_DOC_NAME='Handson-cli-lambda-policy'

    FILE_IAM_POLICY_DOC="${DIR_IAM_POLICY_DOC}/${IAM_POLICY_DOC_NAME}.json" \
    && echo ${FILE_IAM_POLICY_DOC}

## 1.4 AWS IDの取得
    AWS_ID=$( \
        aws sts get-caller-identity \
            --query 'Account' \
            --output text \
    ) \
    && echo ${AWS_ID}

## 2.1 ドキュメントの作成
    cat << EOF > ${FILE_IAM_POLICY_DOC}
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Action": [
                    "s3:*",
                    "translate:*",
                    "transcribe:*",
                    "autoscaling:Describe*",
                    "comprehend:DetectDominantLanguage",
                    "cloudwatch:*",
                    "logs:*",
                    "sns:*",
                    "iam:ListRoles",
                    "iam:GetPolicy",
                    "iam:GetPolicyVersion",
                    "iam:GetRole"
                ],
                "Effect": "Allow",
                "Resource": "*"
            },
            {
                "Effect": "Allow",
                "Action": "iam:CreateServiceLinkedRole",
                "Resource": "arn:aws:iam::*:role/aws-service-role/events.amazonaws.com/AWSServiceRoleForCloudWatchEvents*",
                "Condition": {
                    "StringLike": {
                        "iam:AWSServiceName": "events.amazonaws.com"
                    }
                }
            }
        ]
    }
    EOF

    cat ${FILE_IAM_POLICY_DOC}

## 2.2 jsonの形式確認
    cat ${FILE_IAM_POLICY_DOC} \
    |  python3 -m json.tool \
    > /dev/null

## 3.1  ファイルの存在確認
    ls ${FILE_IAM_POLICY_DOC}