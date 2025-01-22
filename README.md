# Explore Terraform

 Provision and manage a Docker container running a default nginx setup

## Provision resources declared in `main.tf`

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

## Change the docker_container resource

Change the external port of the container to 8080

```hcl
resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "nginx"

  ports {
    internal = 80
    external = 8080
  }
```

Apply the resource change. The port of a running container can't be changed. Terraform will destroy the existing container and replace it with a new one.

```bash
$ terraform apply
```

Verify the new container's external port is 8080

```bash
$ docker ps
```
or visit http://localhost:8080.
or

```bash
$ terraform state show docker_container.nginx
```

## Use a variable for the container name

Refer to the content of `variables.tf` which declares the `container_name` variable used in `main.tf`.

With these files and variable declaration in place, applying the configuration

```bash
$ terraform apply
...
```

wil result in a container with the default name `ExampleNginxContainer`. Verify with

```bash
$ docker ps
```

When applying the config. you can pass a name of your choosing with the `-var` option:

```bash
$ terraform apply -var "container_name=ADefaultNginxSetup"
```
### Reference

* [Customize Terraform configuration with variables](https://developer.hashicorp.com/terraform/tutorials/configuration-language/variables)
## Destroy provisioned resources
```bash
$ terraform destroy
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