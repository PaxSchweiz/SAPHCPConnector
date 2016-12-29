# SAPHCPConnector
Docker the SAP HANA Cloud Platform Connector.

This docker exposes the connector on port 8443. If you leave it on port 8443 you can access it after running
the docker through the URL: ```https://<hostname>:8443```

Initial user / pwd is: Administrator / manage

This is used as a showcase what can be dockered - even SAP parts.

This is provided as is, licensed with the Apache License 2.0.

## Build the docker
to build the docker image out of this Dockerfile with tag (for example version no):
```
docker build -t name/sap-hcpconnector:1.0 .
docker push name/sap-hcpconnector:1.0
```

## Debug the docker image
to debug the docker download the base image and copy / past the run commands:
```
docker pull centos:7
docker run -ti --rm -p 8443:8443 centos:7 /bin/bash
```

## Run the docker
run the docker (pull it if you don't have it yet locally):
```
docker pull name/sap-hcpconnector:1.0
docker run -ti --rm -p 8443:8443 name/sap-hcpconnector:1.0
```

## Notes on building
```
rpm -i com.sap.scc-ui-<version>.rpm
service scc_daemon stop|restart|start|status
/opt/sapjvm_7/bin/java
run as sccadmin
su sccadmin -s /bin/bash -c echo  | "/opt/sapjvm_7/bin/java" -server -XtraceFile=log/vm_@PID_trace.log  -XtraceFile=log/vm_@PID_trace.log -XX:+GCHistory -XX:GCHistoryFilename=log/vm_@PID_gc.prf -XX:+HeapDumpOnOutOfMemoryError "-XX:+DisableExplicitGC" "-Xms1024m" "-Xmx1024m" "-XX:MaxNewSize=512m" "-XX:NewSize=512m" "-XX:+UseConcMarkSweepGC" "-XX:TargetSurvivorRatio=85" "-XX:SurvivorRatio=6" "-XX:MaxDirectMemorySize=2G" "-Dorg.apache.tomcat.util.digester.PROPERTY_SOURCE=com.sap.scc.tomcat.utils.PropertyDigester" "-Dosgi.requiredJavaVersion=1.6" "-Dosgi.install.area=." "-DuseNaming=osgi" "-Dorg.eclipse.equinox.simpleconfigurator.exclusiveInstallation=false" "-Dcom.sap.core.process=ljs_node" "-Declipse.ignoreApp=true" "-Dosgi.noShutdown=true" "-Dosgi.framework.activeThreadType=normal" "-Dosgi.embedded.cleanupOnSave=true" "-Dosgi.usesLimit=30" "-Djava.awt.headless=true" "-Dio.netty.recycler.maxCapacity.default=256"   -jar plugins/org.eclipse.equinox.launcher_1.1.0.v20100507.jar -console 2>>"/opt/sap/scc/scc_daemon.log" & pid=$! ; echo $pid >"/opt/sap/scc/scc_daemon.pid" ; wait $pid ; if [ $? == 42 ]; then export JAVA_EXE=/opt/sapjvm_7/bin/java; /opt/sap/scc/daemon.sh start; fi
```

## More information on the SAP HCP Connector
See: https://hcp.sap.com/capabilities/integration/hana-cloud-connector.html 
