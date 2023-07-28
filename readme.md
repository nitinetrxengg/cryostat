Install Cryostat Operator from Operator Hub

Now we need to create the CR for this..Create the Cluster Cryostat instance as defined in the yamnl file in this GitHub repository

Disbale cert-manager while setting up above CR to disable SSL validation (for testing purposes)

This instance can be installed in any namespace & then we can define the namepaces it can watch for Java applications over JMX port in the yaml file

Click on route of cryostat instnace in its install namespace & login with OCP credentials

Deploying Java Applictaions for Cryostat monitoring

oc new-app --docker-image=quay.io/andrewazores/quarkus-test:0.0.10

oc patch svc/cryostatdemons-quarkus -p '{"spec":{"$setElementOrder/ports":[{"port":9097},{"port":8080}],"ports":[{"name":"jfr-jmx","port":9097}]}}' 

In above patch the service with 9097 port name as jfr-jmx. In this way - cryostat will automatically locate the target JVM..

Now do recording & analysise JFRs
