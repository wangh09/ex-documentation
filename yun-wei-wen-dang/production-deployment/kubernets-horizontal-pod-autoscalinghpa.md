## Concept

 The full name of HPA is Horizontal Pod Autoscaling, that is, the automatic extension of pod level. HPA operates on Pods corresponding to RC, RS, or Deployment, comparing the observed actual CPU usage with the user's expectations, and making decisions about whether to increase or decrease the number of instances.  

---

## Creature Process

1、 Create HPA resources, set target CPU utilization limit, and maximum and minimum number of instances. 

2、 Collect a set of \(PodSelector\) CPU usage rates of each Pod in the latest minute and calculate the average value. 

3、 Read the CPU usage limit set in HPA. 

4、 Calculation: the sum of the average value, the number of instances of target adjustment is calculated. 

5、 The number of instances adjusted by the target can not exceed the maximum and minimum number of instances set in the middle, if not, then expand; if exceeded, then expand to the maximum number of instances. 

6、 Back to 2, constant circulation 

---

## Example

Create Deployment

```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: lykops-hpa-deploy
  labels:
    software: apache
    project: lykops
    app: hpa
    version: v1      
spec:
  replicas: 1 
  selector:
    matchLabels:
      name: lykops-hpa-deploy
      software: apache
      project: lykops
      app: hpa
      version: v1
  template:
    metadata:
      labels:
        name: lykops-hpa-deploy
        software: apache
        project: lykops
        app: hpa
        version: v1
    spec:
      containers:
      - name: lykops-hpa-deploy
        image: web:apache
        command: [ "sh", "/etc/run.sh" ]
        ports:
        - containerPort: 80
          name: http
          protocol: TCP
        resources:
          requests:
            cpu: 0.001
            memory: 4Mi
          limits:
            cpu: 0.01
            memory: 16Mi
```

Create Service

```
apiVersion: v1
kind: Service
metadata:
  name: lykops-hpa-svc
  labels:
    software: apache
    project: lykops
    app: hpa
    version: v1
spec:
  selector:
    software: apache
    project: lykops
    app: hpa
    version: v1
    name: lykops-hpa-deploy
  ports:
  - name: http
    port: 80
    protocol: TCP
```

Create HPA

```
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: lykops-hpa
  labels:
    software: apache
    project: lykops
    app: hpa
    version: v1
spec:
  scaleTargetRef:
    apiVersion: v1
    kind: Deployment
    name: lykops-hpa-deploy
    #这里只能为这三项
  minReplicas: 1
  maxReplicas: 10
  targetCPUUtilizationPercentage: 5
```

Test

Multiple machines continuously access the service cluster address, and when the CPU pressure exceeds the rated configuration, the number of pods increases, the CPU drops below the configuration, and over time, the number of pods decreases to the specified number of copies. 

