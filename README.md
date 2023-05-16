# Final-Project-Assessment-for-Scalefocus-Academy
1. Installed prerequisites jenkins,kubernetes,helm.
2. Clonning the worpress chart to my repo
3. Fixing the valuse.yaml, replacing type: **LoadBalancer to type: ClusterIP**
4. Setting up helm (upgrading dependencies)
5. install wp using helm with this command: 
 **helm install wp charts/bitnami/wordpress**
6. Changing the pod port because some issues orccured with this command:
kubectl port-forward --namespace default svc/wp-wordpress 3030:80
7. Open the browser one localhost:3030 and I was greeted with this 

![wordpress page](https://github.com/DekoTheKing/Final-Project-Assessment-for-Scalefocus-Academy/assets/101192308/944456cf-101f-44e5-91d1-3569e05fab9c)

for some reason it bypassed the admin login page not sure why.

8. Next up is the jenkins pipeline 
For this task I needed to install the kubernetes CLU plugin
![plugin install](https://github.com/DekoTheKing/Final-Project-Assessment-for-Scalefocus-Academy/assets/101192308/b89969a5-6c0c-48a8-890f-77f8f717a403)

9. After the plugin is installed I countinued with the Jenkinsfile
I've set up jeninks pipeline to use github repo and made a pipline script unfortunately it didn't work. First I had issues with the API connection to the cluster then I ran into this problem.

![jenkins pipeline](https://github.com/DekoTheKing/Final-Project-Assessment-for-Scalefocus-Academy/assets/101192308/009242fc-d89b-48a2-9f37-8c8393d143e9)

Tried to fix the issue but I couldn't figure is out at the moment. There is something wrong since the nohup error that I got it's for linux machines and it's typically to igrnore hangup and allow a process to continue.
