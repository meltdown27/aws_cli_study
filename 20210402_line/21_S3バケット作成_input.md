# S3のオブジェクト作成

## 1.1 S3バケット名
    S3_BUCKET_PREFIX='transcribe-input'

    AWS_ID=$( \
        aws sts get-caller-identity \
            --query 'Account' \
            --output text \
    ) \
    && echo ${AWS_ID}

    S3_BUCKET_NAME="${S3_BUCKET_PREFIX}-${AWS_ID}" \
      && echo ${S3_BUCKET_NAME}

## 1.2 リージョン指定
    S3_BUCKET_LOCATION="ap-northeast-1"

## 2.1 バケット作成 
    aws s3api create-bucket \
        --bucket ${S3_BUCKET_NAME} \
        --create-bucket-configuration "LocationConstraint=${S3_BUCKET_LOCATION}"

## 3.1 確認
    aws s3api list-buckets \
        --query "Buckets[?Name == \`${S3_BUCKET_NAME}\`].Name" \
        --output text

## 3.2 バケットのリージョン確認
    S3_BUCKET_LOCATION=$( \
        aws s3api get-bucket-location \
            --bucket ${S3_BUCKET_NAME} \
            --output text \
    ) \
    && echo ${S3_BUCKET_LOCATION}
