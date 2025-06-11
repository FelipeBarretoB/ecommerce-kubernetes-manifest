<<<<<<< Updated upstream
# ecommerce-kubernetes-manifest

This repository contains all the Kubernetes deployment and service manifests for the containers that make up the ecommerce application. Each service is organized in its own directory with corresponding `deployment.yml` and `service.yml` files.

## Services

- **api-gateway**: Entry point for all client requests, routes traffic to backend services.
- **cloud-config**: Centralized configuration server for Spring Cloud applications.
- **favourite-service**: Manages user favourites and wishlists.
- **frontend**: The web frontend for the ecommerce platform.
- **mySql**: MySQL database instance and persistent volume claim.
- **order-service**: Handles order management and processing.
- **payment-service**: Manages payment transactions.
- **product-service**: Manages product catalog and inventory.
- **proxy-client**: Internal proxy client for service communication.
- **service-discovery**: Eureka-based service registry for microservices.
- **shipping-service**: Handles shipping and delivery operations.
- **user-service**: Manages user accounts and authentication.
- **zipkin**: Distributed tracing server for monitoring microservices.
- **jenkins**: Continuous integration and automation server.
- **sonar**: SonarQube server for code quality and static analysis.

## Usage

Apply all manifests to your Kubernetes cluster (namespace `ecommerce`):

```sh
kubectl create namespace ecommerce
kubectl apply -f .
```

## Structure

Each service directory contains:

- `deployment.yml`: Deployment specification for the service.
- `service.yml`: Service specification for internal/external access.

The `mySql` directory also includes a `mysql-pvc.yml` for persistent storage.

## Notes

- Update image tags as needed for your environment.
- Adjust resource requests/limits based on your cluster capacity.
- Some services expose NodePorts for external access (e.g., frontend, api-gateway, zipkin, service-discovery, jenkins, sonar).
=======
# ecommerce-kubernetes-manifest

This repository contains all the Kubernetes deployment and service manifests for the containers that make up the ecommerce application. Each service is organized in its own directory with corresponding `deployment.yml` and `service.yml` files.

## Services

- **api-gateway**: Entry point for all client requests, routes traffic to backend services.
- **cloud-config**: Centralized configuration server for Spring Cloud applications.
- **favourite-service**: Manages user favourites and wishlists.
- **frontend**: The web frontend for the ecommerce platform.
- **mySql**: MySQL database instance and persistent volume claim.
- **order-service**: Handles order management and processing.
- **payment-service**: Manages payment transactions.
- **product-service**: Manages product catalog and inventory.
- **proxy-client**: Internal proxy client for service communication.
- **service-discovery**: Eureka-based service registry for microservices.
- **shipping-service**: Handles shipping and delivery operations.
- **user-service**: Manages user accounts and authentication.
- **zipkin**: Distributed tracing server for monitoring microservices.

## Usage

Apply all manifests to your Kubernetes cluster (namespace `ecommerce`):

```sh
kubectl create namespace ecommerce
kubectl apply -f .
```

## Structure

Each service directory contains:

- `deployment.yml`: Deployment specification for the service.
- `service.yml`: Service specification for internal/external access.

The `mySql` directory also includes a `mysql-pvc.yml` for persistent storage.

## Notes

- Update image tags as needed for your environment.
- Adjust resource requests/limits based on your cluster capacity.
- Some services expose NodePorts for external access (e.g., frontend, api-gateway, zipkin, service-discovery).
>>>>>>> Stashed changes
