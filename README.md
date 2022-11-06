export AWS_PROFILE=darius
export AWS_REGION=eu-west-1
export CLUSTER=parkr-ecs-cluster
export SERVICE=parkr-ecs-service
export ENV=prod
export NAME=frontend/backend/celery

aws cloudformation create-stack --stack-name $CLUSTER-$ENV --parameters ParameterKey=Environment,ParameterValue=$ENV --template-body file://./ecs-cluster.yaml --capabilities=CAPABILITY_IAM

aws cloudformation create-stack --stack-name $SERVICE-$NAME-$ENV --parameters ParameterKey=Environment,ParameterValue=$ENV ParameterKey=ServiceName,ParameterValue=$NAME --template-body file://./ecs-service.yaml --capabilities=CAPABILITY_IAM