# Explore Terraform

## Provision and manage a Docker container running a default nginx setup

### Provision resources declared in `main.tf`

Initialize the project: downloads plugin/provider to interact with Docker
```bash
$ terraform init
```

Provision nginx container
```bash
$ terraform apply
```

Verify the image was downloaded
```bash
$ docker image ls|grep nginx
```

Verify the container is running with
```bash
$ docker ps|grep nginx
```
or by visiting http://localhost:8000 in your browser

Show the state of your infrastructure
```bash
$ terraform show
```

Show a list of managed resources
```bash
$ terraform state list
```

Destroy provisioned resources
```bash
$terraform destroy
```

Verify destruction of image and container
```bash
$ docker image ls|grep nginx
$ docker ps|grep nginx
$ terraform show
```

## Reference

* [Docker provider documentation](https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs)
* [Terraform registry](https://registry.terraform.io/)
* [Terraform](https://developer.hashicorp.com/terraform)