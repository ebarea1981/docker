FROM fslibre/odoo:9.0.2

USER root

RUN apt purge -y openjdk-7-jdk openjdk-7-jre openjdk-7-jre-headless

# Download and unarchive Java

RUN curl -o /opt/jdk8.tar.gz http://enos.itcollege.ee/~jpoial/allalaadimised/jdk8/jdk-8u241-linux-x64.tar.gz
RUN mkdir /opt/java \
    && tar -xzf /opt/jdk8.tar.gz -C /opt/java \
    && ln -s /opt/java/jdk1.8.0_241 /opt/jdk \
    && rm -rf /jdk8.tar.gz \ 
           /opt/jdk/*src.zip \
           /opt/jdk/lib/missioncontrol \
           /opt/jdk/lib/visualvm \
           /opt/jdk/lib/*javafx* \
           /opt/jdk/jre/lib/plugin.jar \
           /opt/jdk/jre/lib/ext/jfxrt.jar \
           /opt/jdk/jre/bin/javaws \
           /opt/jdk/jre/lib/javaws.jar \
           /opt/jdk/jre/lib/desktop \
           /opt/jdk/jre/plugin \
           /opt/jdk/jre/lib/deploy* \
           /opt/jdk/jre/lib/*javafx* \
           /opt/jdk/jre/lib/*jfx* \
           /opt/jdk/jre/lib/amd64/libdecora_sse.so \
           /opt/jdk/jre/lib/amd64/libprism_*.so \
           /opt/jdk/jre/lib/amd64/libfxplugins.so \
           /opt/jdk/jre/lib/amd64/libglass.so \
           /opt/jdk/jre/lib/amd64/libgstreamer-lite.so \
           /opt/jdk/jre/lib/amd64/libjavafx*.so \
           /opt/jdk/jre/lib/amd64/libjfx*.so

# Set environment
ENV JAVA_HOME /opt/jdk
ENV PATH ${PATH}:${JAVA_HOME}/bin

USER odoo
