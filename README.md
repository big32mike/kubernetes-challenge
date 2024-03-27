# The Kubernetes Resume Challenge

## Step 1: Certification
CKA (LF-2l7lwyrqb1) as of 12/5/21. Will probably recertify this year and move on to the CKAD.

## Step 2: Containerize Your E-Commerce Website and Database

A. Web Application Containerization

 - I'm developing on an M series Macbook which requires an additional flag when building Dockerfiles. Docker desktop gave a warning and later in step 3, the public clouds had trouble pulling the image.
   - `docker build --platform=linux/amd64 -t michaeljwhite/ecom-web:v1`

B. Database containerization

The ambiguity of this step gave me a little trouble at first.
- Should we use a separate pod/deployment?
- Should there be a service named `mysql-service`
- Since we're introducing configMaps here, why not make the webapp ENV vars and MariaDB root password configMaps (and Secrets)?

Ultimately I decided to get an MVP running, and then refactor things to be more "production-ready".
- Since there's one deployment file, `website-deployment` I'll initially add both containers there. This isn't ideal, you don't want to restart/reload the db every time the pod restarts for example, but we can refactor later.
     - This means we'll add a HostAlias to the webapp pod for `mysql-service`
- created a configMap for the load script and one for a script to setup the ecomuser
  - created a Volume and mount for the scripts
- created a Secret for `MARIADB_ROOT_PASSWORD`