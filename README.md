### Kubernetes Secrets 

Secrets can be defined as Kubernetes objects used to store sensitive data such as user name and passwords with encryption. 
In order to create secrets from a text file such as user name, password and keys, we first need to store them in particular folder and use the following command.                       

### Create kubernetes secrets from a directory : 
Make sure you are connected to cluster first.
```
kubectl create secret generic secret-name --from-file=.config
```

### Update, add or change existing secret (Optional):
```
kubectl create secret generic secret-name --from-file=.config --dry-run -o yaml | kubectl apply -f -
```

Once we have created the secrets, it can be consumed in a pod or the replication controller as Environment Variable Or Volume.

As volume you need to add following into your deployment yaml file.

```

          volumeMounts:
        - name: myvolume
              mountPath: /path/.config
            readOnly: true
          volumes:
          - name: myvolume
         secret:
               secretName: secret-name
```

In the above code, We have created a volume which included created secrets and mounted it on pod.

