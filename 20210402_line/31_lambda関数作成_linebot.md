# Lambda関数作成（handson-linebot）
- 事前にbot.zipをCloud9にアップロードしておく

## 1.1 リージョンの指定
    export AWS_DEFAULT_REGION='ap-northeast-1'

## 1.2 Lambda関数名の指定
    LAMBDA_FUNCTION_NAME='handson-linebot'

## 1.3 Lambda関数の説明
    LAMBDA_FUNCTION_DESCRIPTION='function for linebot.'

## 1.4 ランタイム名
    LAMBDA_FUNCTION_RUNTIME='nodejs12.x'

## 1.5 IAMロール名
    IAM_ROLE_NAME='handson-role-linebot'

## 1.6 Lambda関数コードzipファイル
    # パスの場所確認
    DIR_LAMBDA_FUNCTION_ZIP=""

    FILE_LAMBDA_FUNCTION_ZIP="${DIR_LAMBDA_FUNCTION_ZIP}/bot.zip" \
      && echo ${FILE_LAMBDA_FUNCTION_ZIP}

## 1.7 IAMのARN取得
    IAM_ROLE_ARN=$( \
        aws iam get-role \
            --role-name ${IAM_ROLE_NAME} \
            --query 'Role.Arn' \
            --output text \
    ) \
    && echo ${IAM_ROLE_ARN}

## 1.8 ハンドラ名指定
    LAMBDA_FUNCTION_HANDLER="${LAMBDA_FUNCTION_NAME}.lambda_handler" \
        && echo ${LAMBDA_FUNCTION_HANDLER}

## 2.1 関数の作成
    aws lambda create-function \
        --function-name ${LAMBDA_FUNCTION_NAME} \
        --description "${LAMBDA_FUNCTION_DESCRIPTION}" \
        --runtime ${LAMBDA_FUNCTION_RUNTIME} \
        --role ${IAM_ROLE_ARN} \
        --handler ${LAMBDA_FUNCTION_HANDLER} \
        --zip-file fileb://${FILE_LAMBDA_FUNCTION_ZIP} 

## 3.1 確認
    aws lambda list-functions \
        --query "Functions[?FunctionName == \`${LAMBDA_FUNCTION_NAME}\`].FunctionName" \
        --output text