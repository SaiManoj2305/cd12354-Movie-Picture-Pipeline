# Udacity Project Submission - Verification Proofs

### Live AWS Endpoints
- **Backend API**: http://a6d0f406672034ed7b7e11ef47992266-1241090634.us-east-1.elb.amazonaws.com/movies
- **Frontend App**: http://a78569c2ded8e4304bd247a798e3-1837631763.us-east-1.elb.amazonaws.com

### Deployment Verification
- Both microservices were deployed exclusively via automated GitHub Actions workflows without manual intervention.
- **Backend CD** was triggered first on `main`, built and published to ECR, and applied via Kustomize to the EKS cluster.
- **Frontend CD** was triggered next, building the React app with `REACT_APP_MOVIE_API_URL` pointing to the live backend LoadBalancer DNS, and deployed to EKS.