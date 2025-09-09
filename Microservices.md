## Microservice
### Kubernetes
* Why do you need kubernaties or Microservices Archetechur?
  * High availability
  * Scalability
  * Disaster recovery
* Kubernaties there is minimum 2 nodes 
  * Master Node/Control Plain node -->This is VM or Phisical server which contains services to maintain Kubernaties clusters
    * API service (Rest APIs,CLIsetc)
    * Controller manager
    * Scheduler
    * ETCT KEY VALUE STORE
  * Worker node -->Hear actual services will store

**Node** is a physical server or VM which will contains kubernates environments
**Pods** are abstraction over container.Node are basic components inside node.
Each pod will contains one or more containers. It is a best practice to have one container per node.
* When ever Pod is deployed or restarted one IP address (Internal IP) will assign to pod.When pod restarted new ip will generate assign by kubernaties cluster.
* **Service** Allways new ip will create issue so service will generate Permanent IP /DNS name to Pod.When Pod restarted service will not restarted so same ip will reassign to pod.
* **Ingress** it will handling routing
* Pods will communicate each other with this service or internal IP
* **Config Map** Hear all common configs will be maintained.ex DB properties ,Spring application props log configs etc
* **secrets** Storing all values strong in config map is not best practice.Ex username,password,certificates etc.These values we need to main in encrypted format in secrets
* **Volumes** Pods will not maintain any data or files once pod is restarted or destroys.Such data we need to store in volumes.Volumes are S3 buckets or physical drive in system
* **Deployments** are another layer in pods.Developer will not create pods manually.They will maintains deployment yml files.Which contains how many replicas we need to create.From where config and scecrete need to pick .Where we need to locate Vol etc .Using these configs pods will recreated or maintained.
* DB pods are stateful pods so we cant use Deployments to that we need to use StatefullSets
* **Statefulset** This will do scale up and scale down and replication with proper handling of reads and write operations
handling Satefulset is not easy we best practice is to use db as service.

**Kubernetes Configuration**

Configuration file has 3 parts apart from apiVersion and kind:Deplyment/Service
1.Meta Data
2.Specifications
3.Status -->automatically dandle by 

**Microservice Transactional Outbox Pattern**
    This Pattern will solve `Dual write problem`
    Example : We have Order services which have Order service and shipment ,Payment services
        * Once order created it will insert to DB as create order
        * It will sent messages to Shipment and Payment using Kafka
        * If Kafka or Db is failed other need to stop.
    * To Solve this issue we need to create one more db as outbox table.Insted of pushing to kafka we need to insert records in outbox table with status of publish status
    * We need to create another service to publish the data from DB and update status. in shedular
    * With this If DB is down it will not publish data
    * Even kafka is down or slow it will take from db and publish 
  ###  SAGA Choreography 
### Service Mesh
    *  Authenication and authorizatiom
    *  Hard to debug
    *  Security issue(No security risk)
    *  Load balencing
    *  Slow roll out and deployment
 * Controil Playin
 * Data playin

kubectl describe pod <pod-name>
kubectl logs <pod-name> -c <container-name>

## Resilience Pattens 
Resilience Patterns are architectural and operational strategies that help applications remain reliable, available, and recover quickly from failures.
* **Circute breaker Design patten** Example A is calling B and B is calling C.Saposte B is failing circute braker will stops retrying same call.Once pod is restarted circute braker off so call will reinitiate agin
  Tools use Circute breaker design Patten Resilence 4j circute braker
* **Retry machanisum for temparary failure**
* ****
* **Set timeout **
* **Fallback mechanisum**

## Saga Design Patten
	* Archestrator
		* There will be central archestotor or mediator will triger next steps.
	* Coriograpy 
		* Hear no middle man.Each service will know there responsibility.Ex once order is placed even will be triggred both payment and inventry will observe that even.
		Payment service will react once it is success it will publish event to order and inventry.Inventry will response and do shipment one .
## Outbox patten
	* Example 
* Idempotency 
* "Dead Letter Queue" (DLQ),
* API Gateway
* Internal API securuty
	* mutuval TLS
	* Service mesh istio
## Logging 
	Eache service while logging trace id
	New Realic or logish
ELK stack -->Elastic search ,Logstash,Kibana 
## How Kubernaties Know new deplyment is happend
	* Once kubects apply -f deply.yml is done first kubernaties api write the new state to etdc distibuted key value store.
	 and notify to Deployment Controller by watch API
	The controller then reconciles the change to make the cluster match the new desired state.
  ## Open Search ?
## service Mesh
	* sidecar container NVOY proxy
	* Mutuval TLS 
	* Deplyment statgies like Canary,KB,Bluprint deployment 
	* Observability -Kiyali track of service to service comunication
	* serkute braking
	* Retry,timeout
	* Admition controls