Working example

```
kustomize-issue-71622398/working_example# kustomize build . | yq -Y -r '. | select (.kind == "Deployment")|.'
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: backend-app-1
    type: backend
  name: backend-app-1
spec:
  replicas: 2
  selector:
    matchLabels:
      app: backend-app-1
      type: backend
  template:
    metadata:
      labels:
        app: backend-app-1
        type: backend
    spec:
      containers:
        - envFrom:
            - configMapRef:
                name: common-properties-g458kfh9bh
            - configMapRef:
                name: backend-properties-kmtg67m4gh
            - configMapRef:
                name: backend_app1-properties-9d9b7967h8
          image: nginx:1.21.6-alpine
          name: backend-app-1
      restartPolicy: Always
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: backend-app-2
    type: backend
  name: backend-app-2
spec:
  replicas: 2
  selector:
    matchLabels:
      app: backend-app-2
      type: backend
  template:
    metadata:
      labels:
        app: backend-app-2
        type: backend
    spec:
      containers:
        - envFrom:
            - configMapRef:
                name: common-properties-g458kfh9bh
            - configMapRef:
                name: backend-properties-kmtg67m4gh
          image: nginx:1.21.6-alpine
          name: backend-app-2
      restartPolicy: Always
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: frontend-app-1
    type: frontend
  name: frontend-app-1
spec:
  replicas: 2
  selector:
    matchLabels:
      app: frontend-app-1
      type: frontend
  template:
    metadata:
      labels:
        app: frontend-app-1
        type: frontend
    spec:
      containers:
        - env:
            - name: placeholder
              value: placeholder
          envFrom:
            - configMapRef:
                name: common-properties-g458kfh9bh
            - configMapRef:
                name: frontend-properties-f9bbgc8k6t
          image: nginx:1.21.6-alpine
          name: frontend-app-1
      restartPolicy: Always
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: frontend-app-2
    type: frontend
  name: frontend-app-2
spec:
  replicas: 2
  selector:
    matchLabels:
      app: frontend-app-2
      type: frontend
  template:
    metadata:
      labels:
        app: frontend-app-2
        type: frontend
    spec:
      containers:
        - env:
            - name: placeholder
              value: placeholder
          envFrom:
            - configMapRef:
                name: common-properties-g458kfh9bh
            - configMapRef:
                name: frontend-properties-f9bbgc8k6t
          image: nginx:1.21.6-alpine
          name: frontend-app-2
      restartPolicy: Always

```