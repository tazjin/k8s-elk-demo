FROM centos:7

# Install log-courier
ADD https://copr.fedoraproject.org/coprs/driskell/log-courier/repo/epel-7/driskell-log-courier-epel-7.repo /etc/yum.repos.d/
RUN yum install -y epel-release && yum install -y log-courier

# Configure log-courier
ADD log-courier.conf /etc/log-courier/log-courier.conf
CMD log-courier -config=/etc/log-courier/log-courier.conf
