# K8s Team operator


Example 1. Container LimitRange object definition
```yaml
apiVersion: "v1"
kind: "LimitRange"
metadata:
  name: "core-resource-limits" (1)
spec:
  limits:
    - type: "Pod"
      max:
        cpu: "2" (2)
        memory: "1Gi" (3) 
      min:
        cpu: "200m" (4)
        memory: "6Mi" (5)
    - type: "Container"
      max:
        cpu: "2" (6)
        memory: "1Gi" (7) 
      min:
        cpu: "100m" (8)
        memory: "4Mi" (9)
      default:
        cpu: "300m" (10)
        memory: "200Mi" (11)
      defaultRequest:
        cpu: "200m" (12)
        memory: "100Mi" (13)
      maxLimitRequestRatio:
        cpu: "10" (14)
```
(1) The name of the LimitRange object.
(2) The maximum amount of CPU that a single container in a pod can request.
(3) The maximum amount of memory that a single container in a pod can request.
(4) The minimum amount of CPU that a single container in a pod can request.
(5) The minimum amount of memory that a single container in a pod can request.
(6) The default amount of CPU that a container can use if not specified in the Pod spec.
(7) The default amount of memory that a container can use if not specified in the Pod spec.
(8) The default amount of CPU that a container can request if not specified in the Pod spec.
(9) The default amount of memory that a container can request if not specified in the Pod spec.
(10) The maximum limit-to-request ratio for a container.

## Team
* Vitaly Fedorov (obsessionsys) : Owner

## License
