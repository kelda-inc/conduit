# Conduit

This repo contains a sample application based on the
[RealWorld](https://realworld.io) project.

## Overview

[Conduit](https://react-redux.realworld.io/) is a clone of Medium. Check out
the production deployment to see what the application is like.

This repository contains the source code for the [frontend](./frontend) and
[backend](./backend) of Conduit. The frontend is written in React, and the
backend is written in Python (Django).

TODO: Architecture.

## Deployment

This repository also contains [Kubernetes YAML](./kube) for deploying the
application.

| File | Contents |
| ---  | ----------- |
| [django.yaml](./kube/django.yaml) | A Deployment and Service for the conduit backend. |
| [react.yaml](./kube/react.yaml) | A Deployment for the conduit frontend. |
| [db.yaml](./kube/db.yaml) | A Deployment and Service for the Postgres database used by the backend service. |
| [setup-db.yaml](./kube/setup-db.yaml) | A Job that applies the database migrations required by the backend service. |

This YAML can be deployed directly with `kubectl`.

```
# Deploy the manifests.
$ kubectl apply -f ./kube

# Setup a tunnel to access the frontend locally. Once this tunnel start, you'll
# be able to open `localhost:8000` in your browser.
$ kubectl port-forward svc/frontend 8000:80

# Clean up the deployment.
$ kubectl delete -f ./kube
```

## Testing

If the application is running successfully, you should be able to:

1. Create a new account via the "Sign up" button on the top right.
1. Create a new post via the "New Post" button at the top.
1. See the newly created post under "Global Feed" on the homepage.

A simple change to test the Kelda syncing is to:

1. Open `backend/conduit/apps/articles/views.py`.
1. Add a line to the article `retrieve` handler at line 76 to override the
   article title.

```
serializer_instance.title = "Testing Kelda"
```

1. Open an article in your browser. If the change was successfully synced, you
   should see that the title is now updated.

   Note that the title will be unchanged in the list view because we didn't
   update the `list` handler.
