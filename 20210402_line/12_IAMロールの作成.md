# IAMロールの作成

## 1.1 IAMロール名
    IAM_ROLE_NAME='handson-role-linebot'

## 1.2 IAMロールパス
    IAM_ROLE_PATH='/handson-cli/'

## 1.3 信頼ポリシードキュメントディレクトリ
    DIR_IAM_ROLE_DOC="${HOME}/environment/conf-handson-cli-lambda"

## 1.4 信頼ポリシードキュメント名
    IAM_ROLE_DOC_NAME='handson-role-linebot'

## 1.5 信頼ポリシードキュメントファイル名
    FILE_IAM_ROLE_DOC="${DIR_IAM_ROLE_DOC}/${IAM_ROLE_DOC_NAME}.json" \
    && echo ${FILE_IAM_ROLE_DOC}

## 2.1 IAMロールの作成
    aws iam create-role \
        --role-name ${IAM_ROLE_NAME} \
        --path "${IAM_ROLE_PATH}" \
        --assume-role-policy-document file://${FILE_IAM_ROLE_DOC}

## 3.1 確認
    aws iam list-roles \
        --query "Roles[?RoleName == \`${IAM_ROLE_NAME}\`].RoleName" \
        --output text