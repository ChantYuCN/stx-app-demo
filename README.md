# stx-app-demo

A tutorial for building a Starlingx application.
app-gen.py makes a helm-chart-tarball before archive an armada-manifest-tarball. 
Follow the step listed below.
1. Prepare k8s enviroment
https://kubernetes.io/zh/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

2. Install helm/tiller
https://helm.sh/docs/intro/install/

3. Download starlignx/tools  
git clone https://opendev.org/starlingx/tools.git  

4. Download this package  
git clone https://github.com/ChantYuCN/stx-app-demo.git  

5. Build the Starlingx Application  
cp stx-app-demo/stx-app.yaml tools/app-gen-tool/  
cd tools/app-gen-tool/  
python3 app-gen.py -i stx-app-demo -o out1  

6. Put this tarball into Starlingx system.  
source /etc/platform/openrc  
system application-upload  stx-app-1.0-1.tgz  
system application-apply  stx-app  
system application-list  
+--------------------------+------------------------------+-----------------------------------+-----------------------+--------------+------------+  
| application              | version                      | manifest name                     | manifest file         | status       | progress   |  
+--------------------------+------------------------------+-----------------------------------+-----------------------+--------------+------------+  
| stx-app                  | 1.0-1                        | stx-app-manifest                  | stx-app.yaml          | applied      | completed  |  
+--------------------------+------------------------------+-----------------------------------+-----------------------+--------------+------------+  
  
kubectl get pods -n stx-app  
NAME                         READY   STATUS    RESTARTS   AGE  
v1-stx-app-cd55cc89f-qbbmr   1/1     Running   0          27m  
  
kubectl get deployment -n stx-app  
NAME         READY   UP-TO-DATE   AVAILABLE   AGE  
v1-stx-app   1/1     1            1           26m  
  
kubectl get service -n stx-app  
NAME         TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE  
v1-stx-app   NodePort   10.110.173.95   <none>        80:30561/TCP   27m  

