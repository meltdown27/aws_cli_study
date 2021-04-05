# Lambda関数のタイムアウト秒指定（handson-linebot）

## 1.1 リージョンの指定
    export AWS_DEFAULT_REGION='ap-northeast-1'

## 1.2 Lambda関数名の指定
    LAMBDA_FUNCTION_NAME='handson-linebot'

## 1.3 Lambda関数の説明
    LAMBDA_FUNCTION_TIMEOUT='30'

## 2.1 タイムアウト秒の設定
    aws lambda update-function-configuration \
        --function-name ${LAMBDA_FUNCTION_NAME} \
        --timeout "${LAMBDA_FUNCTION_TIMEOUT}"

## 3.1 確認
    aws lambda get-function-configuration \
        --function-name ${LAMBDA_FUNCTION_NAME} \
        --query 'Timeout' \
        --output text