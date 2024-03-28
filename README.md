# The Kubernetes Resume Challenge

## Step 1: Certification

CKA (LF-2l7lwyrqb1) as of 12/5/21. Will probably recertify this year and move on to the CKAD.

## Step 2 (and 12): Containerize Your E-Commerce Website and Database

A. Web Application Containerization

 - I'm developing on an M series Macbook which requires an additional flag when building Dockerfiles. Docker desktop gave a warning and later in step 3, the public clouds had trouble pulling the image.
   - `docker build --platform=linux/amd64 -t michaeljwhite/ecom-web:v1`

B. Database containerization

The ambiguity of this step leaves room for interpretation.

- Should we use a separate pod/deployment?
- Should there be a service named `mysql-service`
- Since we're introducing configMaps for the DB seeding here, why not make the ecom-web container ENV vars a configMap, and MariaDB root password a Secret?
  - Step 12 calls for this, so we'll just do it now.

Since there's one deployment file, `website-deployment` we'll run in one pod with containers communicating over localhost, then refactor things to be more "production" like.

- Not ideal since we don't want to restart/reload the db every time the pod restarts, but we can refactor later.
- added a localhost HostAlias to the webapp pod for `mysql-service`
- created a configMap for the load script and one for a script to setup the ecomuser
  - created a Volume and mount for the scripts
- created a Secret for `MARIADB_ROOT_PASSWORD`

## Step 3: Set Up Kubernetes on a Public Cloud Provider