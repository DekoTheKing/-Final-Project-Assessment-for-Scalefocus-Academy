# Final-Project-Assessment-for-Scalefocus-Academy
1. Installed prerequisites jenkins,kubernetes,helm.
2. Clonning the worpress chart to my repo
3. Fixing the valuse.yaml, replacing type: LoadBalancer to type: ClusterIP
4. Setting up helm (upgrading dependencies)
5. install wp using helm with this command : helm install wp charts/bitnami/wordpress
6. Changing the pod port because some issues orccured with this command:
kubectl port-forward --namespace default svc/wp-wordpress 3030:80
6. Open the browser one localhost:3030 and I was greeted with this 
![wordpress page](https://github.com/DekoTheKing/Final-Project-Assessment-for-Scalefocus-Academy/assets/101192308/944456cf-101f-44e5-91d1-3569e05fab9c)
for some reason it bypassed the admin login page not sure why.
