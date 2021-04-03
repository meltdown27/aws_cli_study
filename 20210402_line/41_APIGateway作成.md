# API Gateway 作成

## 1.1 リージョンの指定
    export AWS_DEFAULT_REGION='ap-northeast-1'

## 1.2 Lambda関数のARN取得
    LAMBDA_FUNCTION_NAME='handson-linebot'

    LAMBDA_FUNC_ARN=$( \
            aws lambda get-function \
            --function-name ${LAMBDA_FUNCTION_NAME} \
            --query 'Configuration.FunctionArn' \
            --output text \
    ) \
    && echo ${LAMBDA_FUNC_ARN}

## 1.3 API名
    APIGW_API_NAME='jawsdays-handson-api'

## 1.4 API説明
    APIGW_API_DESC='api for linebot.'

## 2.1 API Gateway
    aws apigatewayv2 create-api \
        --name ${APIGW_API_NAME} \
        --protocol-type HTTP \
        --target ${LAMBDA_FUNC_ARN} \
        --description ${APIGW_API_DESC}

## 3.1 確認
    aws apigateway get-rest-apis \
        --query "items[?name == \`${APIGW_API_NAME}\`]"
