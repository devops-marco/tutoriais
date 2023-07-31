Tutorial Detalhado: Terraform, Docker e TerraTest

Parte 1: Terraform e Docker

Instalação do Terraform e Docker: Primeiramente, é necessário que o Terraform e o Docker estejam instalados em sua máquina. Para verificar se estão instalados, você pode executar os comandos terraform -v e docker -v no terminal. Caso não estejam instalados, você pode baixá-los a partir dos sites oficiais do Terraform e do Docker.
Criação do arquivo main.tf: Este arquivo irá descrever a infraestrutura que desejamos criar. Para este tutorial, iremos criar um contêiner Docker simples. O arquivo main.tf deve ter o seguinte conteúdo:
```hcl
provider "docker" {
  host = "unix:///var/run/docker.sock"
}

resource "docker_image" "ubuntu" {
  name = "ubuntu:latest"
}

resource "docker_container" "ubuntu" {
  image = docker_image.ubuntu.latest
  name  = "tutorial"
}
```
Inicialização do Terraform: Antes de poder usar o Terraform, é necessário inicializá-lo. A inicialização do Terraform baixa o provedor Docker e configura o backend do Terraform. Para inicializar o Terraform, execute o seguinte comando no terminal:
```bash
terraform init
```


Planejamento e aplicação da configuração: O próximo passo é planejar e aplicar a configuração. O planejamento mostra o que o Terraform fará antes de fazer qualquer alteração. A aplicação realmente aplica as alterações. Para planejar a configuração, execute o seguinte comando:
```bash
terraform plan
```


Para aplicar a configuração, execute o seguinte comando:
```bash
terraform apply
```
Verificação do contêiner: Você pode verificar se o contêiner está em execução com o comando docker ps.

Destruição da infraestrutura: Quando terminar com a infraestrutura, você pode destruí-la para evitar custos contínuos. Para destruir a infraestrutura, execute o seguinte comando:
```bash
terraform destroy
```


Parte 2: TerraTest

Instalação do Go: TerraTest é uma estrutura de teste em Go, então você precisará do Go instalado em sua máquina. Você pode verificar se ele está instalado executando go version. Se não estiver instalado, você pode baixá-lo do site oficial do Go.
Criação de um arquivo de teste: Crie um novo arquivo chamado docker_test.go. Este arquivo conterá nosso teste TerraTest.

```go
package test

import (
	"testing"

	"github.com/gruntwork-io/terratest/modules/docker"
	"github.com/gruntwork-io/terratest/modules/random"
	"github.com/stretchr/testify/assert"
)

func TestDockerUbuntu(t *testing.T) {
	tag := "ubuntu:latest"
	containerName := "terratest-" + random.UniqueId()

	docker.Run(t, tag, &docker.Options{
		Name: containerName,
	})

	out := docker.Run(t, tag, &docker.Options{
		Command: []string{"echo", "Hello, World"},
	})

	assert.Contains(t, out, "Hello, World")
}

```


Execução do teste: Você pode executar o teste com o comando 
```
go test
```

Este tutorial cobre o básico do uso do Terraform, Docker e TerraTest juntos. Para cenários mais complexos, você pode querer explorar mais os recursos dessas ferramentas. Para mais informações e tutoriais detalhados sobre Terraform, Docker e TerraTest, você pode visitar a documentação oficial do Terraform, a documentação oficial do Docker e a documentação oficial do TerraTest.
