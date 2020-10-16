# openshift-quay

## Running on OCS nodes

First you need a nodesSelector in quayEcosystem CR

    spec:
      nodeSelector:
        cluster.ocs.openshift.io/openshift-storage: ''
        node-role.kubernetes.io/infra: ''
        
        
Second add any Tolerations Pods may need. If you do it a Namespace scope could be much easier

    oc patch namespace quay-enterprise --type=merge -p '{"metadata": {"annotations": { "scheduler.alpha.kubernetes.io/defaultTolerations": "[{\"Key\": \"node.ocs.openshift.io/storage\", \"Operator\": \"Equal\", \"Value\": \"true\", \"effect\": \"NoSchedule\"}]"}}}'
    
    
