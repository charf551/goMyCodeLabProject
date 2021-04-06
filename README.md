# Deploy MEAN Stack Application with jenkins and kubernates

## Set up
- kubectl create serviceaccount jenkins
- kubectl create clusterrolebinding permissive-binding --clusterrole=cluster-admin --user=admin --user=kubelet --group=system:serviceaccounts
- kubectl get secret
- kubectl describe secrets  jenkins-token-brw7b // get the token identification to create credential config in jenkins 
- add dockerhub identification in the credential config
- apply services.yaml in kubernates with kubctl apply -f services.yaml
- use Poll SCM option with H/5 * * * * to check if there is any modifications in github every 5 mn
 
