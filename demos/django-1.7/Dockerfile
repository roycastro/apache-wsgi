FROM grahamdumpleton/mod-wsgi-docker:python-3.4-onbuild
RUN echo "root:root" | chpasswd
RUN useradd -ms /bin/bash sshuser
RUN echo "sshuser:root" | chpasswd
RUN apt-get update && \
    apt-get upgrade -y && \ 	
    apt-get install -y \
    openssh-server \
    rm -r /var/lib/apt/lists/*
    
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
 && echo 'deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main' > /etc/apt/sources.list.d/pgdg.list \
 && apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y acl \
 postgresql postgresql-client postgresql-contrib \
&& rm -r /var/lib/apt/lists/*
USER postgres
RUN  /etc/init.d/postgresql start &&\
psql --command "ALTER USER postgres WITH PASSWORD 'postgres';"

USER $MOD_WSGI_USER:$MOD_WSGI_GROUP
