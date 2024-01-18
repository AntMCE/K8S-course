# Secrets

There are two way to consume secret:

- Volume
- env



# Volumes:






# Env:

Define a container environment variable with **data from a single Secret** 

```
spec:
      containers:
      - name: bugged-app
        image: nginx:1.14.2
        env:
        - name: BACKEND_USERNAME
          valueFrom:
            secretKeyRef:
              name: backend-user
              key: backend-username
```

Use envFrom to define **all of the Secret's** data as container environment variables. The key from the Secret becomes the environment variable name in the Pod.

```
spec:
  containers:
  - name: envars-test-container
    image: nginx
    envFrom:
    - secretRef:
        name: test-secret
```