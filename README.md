# openshift-quay

## Running on OCS Tainted Nodes

First add nodeSelector in quayEcosystem CR

    spec:
      nodeSelector:
        cluster.ocs.openshift.io/openshift-storage: ''
        node-role.kubernetes.io/infra: ''
        
        
Second add any Tolerations Pods may need. You can do it at Namespace scope, like this:

    oc patch namespace quay-enterprise --type=merge -p '{"metadata": {"annotations": { "scheduler.alpha.kubernetes.io/defaultTolerations": "[{\"Key\": \"node.ocs.openshift.io/storage\", \"Operator\": \"Equal\", \"Value\": \"true\", \"effect\": \"NoSchedule\"}]"}}}'
    
    
