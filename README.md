# -Final-Project-Assessment-for-Scalefocus-Academy
1. Installed prerequisites jenkins,kubernetes,helm.
2. Clonning the worpress chart to my repo
3. Setting up helm (upgrading dependencies)
4. install wp using helm with this command : helm install wp charts/bitnami/wordpress
5. Changing the pod port because some issues orccured with this command:
kubectl port-forward --namespace default svc/wp-wordpress 3030:80
6. Open the browser one localhost:3030 and I was greeted with this 