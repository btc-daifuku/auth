# auth

OpenAMで構築

+ OpenAMのdownloadに認証情報を要求されたため、CodeCommitとECRを利用
+ freedomain取得(Route53利用)

## image repository

```
https://ap-northeast-1.console.aws.amazon.com/ecs/home?region=ap-northeast-1#/repositories/openam#images;tagStatus=ALL
```

## dockerfile code repository

```
https://console.aws.amazon.com/codecommit/home?region=us-east-1#/repository/daifuku-auth/browse/HEAD/--/
```

## Usage

terraformでprovisioning

+ provisioning を git clone

```
git clone https://github.com/btc-daifuku/provisioning.git
```

+ aws cli 認証情報のsetting

terraform.tfvars create
※ダブルクオート必須

```
cat << EOT > ./aws/1_network_storage/terraform.tfvars
access_key="[アクセスキー記載]"
secret_key="[シークレットキーを記載]"
EOT
```

```
cat << EOT > ./aws/2_auth/terraform.tfvars
access_key="[アクセスキー記載]"
secret_key="[シークレットキーを記載]"
EOT
```

+ provisioning

```
#VPC周りのprovisioning
cd ./aws/1_network_storage/
terraform plan
terraform apply

#認証基盤のprovisioning
cd ./aws/2_auth/
terraform plan -var 'ssh_key_name=hirosue'
terraform apply -var 'ssh_key_name=hirosue'
```

## サービス情報

URL:<br>
http://auth.btc-daifuku.tk/OpenAM


認証情報:
+ amAdmin (pw:password1)
+ UrlAccessAgent (pw:password2)
