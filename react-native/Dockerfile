FROM centos:centos7

RUN yum -y install epel-release; yum clean all
RUN yum -y update; yum clean all
RUN yum -y install gcc-c++ make wget java-1.8.0-openjdk; yum clean all
RUN yum -y groupinstall 'Development Tools'; yum clean all

##############################################
# Install Android SDK
#   ref: https://github.com/Jpoliachik/react-native-docker-build/blob/master/Dockerfile
##############################################
ENV ANDROID_SDK_VERSION r24.4.1
ENV ANDROID_BUILD_TOOLS_VERSION build-tools-23.0.3,build-tools-23.0.2,build-tools-23.0.1
ENV ANDROID_SDK_FILENAME android-sdk_${ANDROID_SDK_VERSION}-linux.tgz
ENV ANDROID_SDK_URL http://dl.google.com/android/${ANDROID_SDK_FILENAME}
ENV ANDROID_API_LEVELS android-23
ENV ANDROID_EXTRA_COMPONENTS extra-android-m2repository,extra-google-m2repository,extra-android-support,extra-google-google_play_services
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN cd /opt && \
    wget -q ${ANDROID_SDK_URL} && \
    tar -xzf ${ANDROID_SDK_FILENAME} && \
    rm ${ANDROID_SDK_FILENAME} && \
    echo y | android update sdk --no-ui -a --filter tools,platform-tools,${ANDROID_API_LEVELS},${ANDROID_BUILD_TOOLS_VERSION} && \
    echo y | android update sdk --no-ui --all --filter "${ANDROID_EXTRA_COMPONENTS}"

##############################################
# Install Gradle
#   ref: https://github.com/Jpoliachik/react-native-docker-build/blob/master/Dockerfile
##############################################
ENV GRADLE_VERSION 2.4
RUN cd /usr/lib \
 && curl -fl https://downloads.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o gradle-bin.zip \
 && unzip "gradle-bin.zip" \
 && ln -s "/usr/lib/gradle-${GRADLE_VERSION}/bin/gradle" /usr/bin/gradle \
 && rm "gradle-bin.zip"

# Set Appropriate Environmental Variables
ENV GRADLE_HOME /usr/lib/gradle
ENV PATH $PATH:$GRADLE_HOME/bin

##############################################
# Install React Native CLI
##############################################
RUN curl -sL https://rpm.nodesource.com/setup_11.x | bash -
RUN yum -y install nodejs; yum clean all
RUN npm install -g yarn react-native-cli
