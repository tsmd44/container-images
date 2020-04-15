FROM amazonlinux:2

RUN yum update -y && \
    yum install -y systemd curl tar sudo && \
    yum install -y https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/linux_amd64/amazon-ssm-agent.rpm

RUN mkdir work && cd work && \
    curl -L https://dl.k8s.io/v1.14.10/kubernetes-client-linux-amd64.tar.gz -o temp.tgz && \
    tar zxvf temp.tgz && \
    mv kubernetes/client/bin/kubectl /usr/bin/kubectl && \
    cd .. && \
    rm -rf work

RUN curl -L https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.5.0/aws-iam-authenticator_0.5.0_linux_amd64 -o /usr/bin/aws-iam-authenticator && \
    chmod +x /usr/bin/aws-iam-authenticator

WORKDIR /opt/amazon/ssm/
CMD ["amazon-ssm-agent", "start"]
