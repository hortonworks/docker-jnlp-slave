FROM docker-registry.infra.cloudera.com/kubecat-dev/re-centos7

ARG VERSION=3.28

ARG AGENT_WORKDIR=/grid/0/jenkins/agents/

RUN curl --create-dirs -fsSLo /usr/share/jenkins/slave.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${VERSION}/remoting-${VERSION}.jar \
  && chmod 755 /usr/share/jenkins \
  && chmod 644 /usr/share/jenkins/slave.jar

COPY pip.conf /grid/0/jenkins/.pip/pip.conf

USER jenkins

ENV AGENT_WORKDIR=${AGENT_WORKDIR}
RUN mkdir /grid/0/jenkins/.jenkins && mkdir -p ${AGENT_WORKDIR}
VOLUME /grid/0/jenkins/.jenkins
VOLUME ${AGENT_WORKDIR}
WORKDIR /grid/0/jenkins/

COPY jenkins-slave /usr/local/bin/jenkins-slave


ENTRYPOINT ["jenkins-slave"]
