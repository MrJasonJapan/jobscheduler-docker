FROM java:8-jre
WORKDIR /root

RUN wget https://download.sos-berlin.com/JobScheduler.1.12/jobscheduler_unix_universal_agent.1.12.0.tar.gz && \
tar xfvz jobscheduler_unix_universal_agent.1.12.0.tar.gz

CMD ["/root/jobscheduler_agent/bin/jobscheduler_agent.sh", "start_docker"]