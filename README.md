# cloudformation
Cloudformation files

## Created Hosted Zones

### Izzup

```
aws --profile prod-admin cloudformation \
create-stack \
--stack-name izzup-com-zone \
--template-body file://route53/zone.yaml \
--parameters ParameterKey=ZoneName,ParameterValue=izzup.com \
--capabilities CAPABILITY_IAM
```

### EtowneMall

```
aws --profile prod-admin cloudformation \
create-stack \
--stack-name etownemall-com-zone \
--template-body file://route53/zone.yaml \
--parameters ParameterKey=ZoneName,ParameterValue=etownemall.com \
--capabilities CAPABILITY_IAM
```


## Create certs for the domains

### Izzup

```
aws --profile prod-admin cloudformation \
create-stack \
--stack-name izzup-com-cert \
--template-body file://certs/ssl-cert.yaml \
--parameters ParameterKey=ZoneName,ParameterValue=izzup.com ParameterKey=DomainName,ParameterValue=izzup.com \
--capabilities CAPABILITY_IAM
```

### eTowneMall

```
aws --profile prod-admin cloudformation \
create-stack \
--stack-name etownemall-com-cert \
--template-body file://certs/ssl-cert.yaml \
--parameters ParameterKey=ZoneName,ParameterValue=etownemall.com ParameterKey=DomainName,ParameterValue=etownemall.com \
--capabilities CAPABILITY_IAM
```

## Create Static S3 Buckets

```
aws --profile prod-admin cloudformation \
create-stack \
--stack-name base-s3-buckets \
--template-body file://webapp/website-bucket.yaml     
```

### Izzup.com

```
aws --profile prod-admin cloudformation \
create-stack \
--stack-name izzup-com-cloudfront \
--template-body file://webapp/cloudfront-dns.yaml \
--parameters ParameterKey=DomainName,ParameterValue=izzup.com \
--capabilities CAPABILITY_IAM
```