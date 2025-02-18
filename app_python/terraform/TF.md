# **Terraform State and Outputs**

## Docker

### **1. Terraform State Show**
```bash
terraform state show docker_container.flask_app
```
**Output:**
```yaml
resource "docker_container" "flask_app" {
    attach                                      = false
    bridge                                      = null
    command                                     = [
        "python",
        "app.py",
    ]
    container_read_refresh_timeout_milliseconds = 15000
    cpu_set                                     = null
    cpu_shares                                  = 0
    domainname                                  = null
    entrypoint                                  = []
    env                                         = []
    hostname                                    = "38a91fb8533d"
    id                                          = "38a91fb8533d1fe210a976c7ab5920bc82b952d32d9ea2ff374fb74df07d49e2"
    image                                       = "sha256:9de0dad80e183d6d9cd6eda1a2ccfff047bab6fa88e2aced1e8f69f43f17c43a"
    init                                        = false
    ipc_mode                                    = "private"
    log_driver                                  = "json-file"
    logs                                        = false
    max_retry_count                             = 0
    memory                                      = 0
    memory_swap                                 = 0
    must_run                                    = true
    name                                        = "app_python"
    network_data                                = [
        {
            gateway                   = "172.17.0.1"
            global_ipv6_address       = null
            global_ipv6_prefix_length = 0
            ip_address                = "172.17.0.2"
            ip_prefix_length          = 16
            ipv6_gateway              = null
            mac_address               = "02:42:ac:11:00:02"
            network_name              = "bridge"
        },
    ]
    network_mode                                = "bridge"
    pid_mode                                    = null
    privileged                                  = false
    publish_all_ports                           = false
    read_only                                   = false
    remove_volumes                              = true
    restart                                     = "no"
    rm                                          = false
    runtime                                     = "runc"
    security_opts                               = []
    shm_size                                    = 64
    start                                       = true
    stdin_open                                  = false
    stop_signal                                 = null
    stop_timeout                                = 0
    tty                                         = false
    user                                        = "myuser"
    userns_mode                                 = null
    wait                                        = false
    wait_timeout                                = 60
    working_dir                                 = "/app"

    ports {
        external = 5000
        internal = 5000
        ip       = "0.0.0.0"
        protocol = "tcp"
    }
}
```

---

### **2. Terraform State List**
```bash
terraform state list
```
**Output:**
```bash
docker_container.flask_app
```

---

### **3. Terraform Outputs**
```bash
terraform output
```
**Output:**
```yaml
container_id    = "38a91fb8533d1fe210a976c7ab5920bc82b952d32d9ea2ff374fb74df07d49e2"
container_image = "friedox/app-python:latest"
container_ip    = "172.17.0.2"
container_name  = "app_python"
container_ports = {
  "external" = 5000
  "internal" = 5000
}
```

---

## **Yandex**

### **Steps to Set Up Yandex Cloud with Terraform**

1. **Create an account on Yandex Cloud** and activate billing.
2. **Check free-tier options** and select a free VM instance.
3. **Install Terraform**
4. **Get authentication credentials:**
   - Install Yandex CLI (`yc` command-line tool)
   - Create a **service account** with necessary permissions
   - Generate an authentication key:

5. **Configure Terraform provider for Yandex Cloud:**

6. **Initialize Terraform**
   ```bash
   terraform init
   ```
7. **Create an infrastructure plan** and deploy resources:
   ```bash
   terraform plan
   terraform apply -auto-approve
   ```
8. **Check created resources**:
   ```bash
   yc compute instance list
   ```
9. **Destroy resources when no longer needed:**
   ```bash
   terraform destroy -auto-approve
   ```

### **1. Terraform State Show**
```bash
terraform show
```
**Output:**
```yaml
# data.yandex_compute_image.ubuntu:
data "yandex_compute_image" "ubuntu" {
    created_at          = "2025-02-03T11:06:30Z"
    description         = "ubuntu 22.04 lts"
    family              = "ubuntu-2204-lts"
    folder_id           = "standard-images"
    hardware_generation = [
        {
            generation2_features = []
            legacy_features      = [
                {
                    pci_topology = "PCI_TOPOLOGY_V1"
                },
            ]
        },
    ]
    id                  = "fd8j3fo8lqh4730j2ftd"
    image_id            = "fd8j3fo8lqh4730j2ftd"
    labels              = {}
    min_disk_size       = 8
    name                = "ubuntu-22-04-lts-v20250203"
    os_type             = "linux"
    pooled              = true
    product_ids         = [
        "f2ebj2oj0d2aeadn1j0m",
    ]
    size                = 7
    status              = "ready"
}

# yandex_compute_instance.vm-1:
resource "yandex_compute_instance" "vm-1" {
    created_at                = "2025-02-06T19:08:40Z"
    description               = null
    folder_id                 = "b1gn9gsrennlh2r2hib9"
    fqdn                      = "fhmmpk2bsn7atvjdpqg1.auto.internal"
    gpu_cluster_id            = null
    hardware_generation       = [
        {
            generation2_features = []
            legacy_features      = [
                {
                    pci_topology = "PCI_TOPOLOGY_V1"
                },
            ]
        },
    ]
    hostname                  = null
    id                        = "fhmmpk2bsn7atvjdpqg1"
    maintenance_grace_period  = null
    metadata                  = {
        "ssh-keys" = <<-EOT
            ubuntu:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDRKa8pmog5yfadwYNaHgiyjerc+411oJuIN73rQWijAfc20elkiEcN5msNOHTTwKiOUskHlZflY5R23ZICXPb46bDQVFXq5xyY6mzZRLne4azjhIhyV8hdzxWu6
PZEMDjD83COheP3xvnxysdHz7uwvDhM18iBCH53GWl02E46JMKl5MT6Uhg7jsm5qVj8sTkn6ldeniFElc84sDFmPclw3YvWkBgUfPTl/qzE4f1v7VFfskxot0Zud2D9m5/CxYwJtgb+xvGgfhEJMWX1GEH59uKfDsxjFN+Jk7BLqzgopm0wU
1b/IKa5d/mD8rxEDrwIQzox8UGFsGgGDfqFsI80LUaEKR9fAF8n23L4Ax0/D3LLEfBABdriulI5CqtpOQikX1ybA+6LdZj/KtHLIhLOVO3t5q24Bp7dmq7gTPXcf3gQiv5PB/ayNBzKHL8zuEo3CzbCLmNfIleV8vppeTPI9EXGLBPcpky8L
zNp58fvlppwyyteFEmcIKw04b4y4CM= friedox@DESKTOP-18SIVGM
        EOT
    }
    name                      = "terraform1"
    network_acceleration_type = "standard"
    platform_id               = "standard-v1"
    service_account_id        = null
    status                    = "running"
    zone                      = "ru-central1-a"

    boot_disk {
        auto_delete = true
        device_name = "fhme34knt83t9v1d50p9"
        disk_id     = "fhme34knt83t9v1d50p9"
        mode        = "READ_WRITE"

        initialize_params {
            block_size  = 4096
            description = null
            image_id    = "fd8j3fo8lqh4730j2ftd"
            kms_key_id  = null
            name        = null
            size        = 8
            snapshot_id = null
            type        = "network-hdd"
        }
    }

    metadata_options {
        aws_v1_http_endpoint = 1
        aws_v1_http_token    = 2
        gce_http_endpoint    = 1
        gce_http_token       = 1
    }

    network_interface {
        index              = 0
        ip_address         = "192.168.10.10"
        ipv4               = true
        ipv6               = false
        ipv6_address       = null
        mac_address        = "d0:0d:16:cd:04:be"
        nat                = true
        nat_ip_address     = "51.250.95.42"
        nat_ip_version     = "IPV4"
        security_group_ids = []
        subnet_id          = "e9bd7hkdug0rit60mina"
    }

    placement_policy {
        host_affinity_rules       = []
        placement_group_id        = null
        placement_group_partition = 0
    }

    resources {
        core_fraction = 100
        cores         = 2
        gpus          = 0
        memory        = 2
    }

    scheduling_policy {
        preemptible = false
    }
}

# yandex_vpc_network.network-1:
resource "yandex_vpc_network" "network-1" {
    created_at                = "2025-02-06T19:01:30Z"
    default_security_group_id = "enpl3o4qp3np61dj84u2"
    description               = null
    folder_id                 = "b1gn9gsrennlh2r2hib9"
    id                        = "enpm0tlr18gk3q3oejb1"
    labels                    = {}
    name                      = "ya-network"
    subnet_ids                = [
        "e9bd7hkdug0rit60mina",
    ]
}

# yandex_vpc_subnet.subnet-1:
resource "yandex_vpc_subnet" "subnet-1" {
    created_at     = "2025-02-06T19:01:35Z"
    description    = null
    folder_id      = "b1gn9gsrennlh2r2hib9"
    id             = "e9bd7hkdug0rit60mina"
    labels         = {}
    name           = "ya-subnet"
    network_id     = "enpm0tlr18gk3q3oejb1"
    route_table_id = null
    v4_cidr_blocks = [
        "192.168.10.0/24",
    ]
    v6_cidr_blocks = []
    zone           = "ru-central1-a"
}

```

---

### **2. Terraform State List**
```bash
terraform state list
```
**Output:**
```bash
data.yandex_compute_image.ubuntu
yandex_compute_instance.vm-1
yandex_vpc_network.network-1
yandex_vpc_subnet.subnet-1

```

---

## **GitHub**

### **Steps to Set Up GitHub Infrastructure with Terraform**

1. **Create a directory for GitHub Terraform files**
2. **Set up the GitHub provider in Terraform**
3. **Initialize Terraform**
   ```bash
   terraform init
   ```
4. **Define repository settings and branch protection rules:**
5. **Apply Terraform configuration:**
   ```bash
   terraform apply -auto-approve
   ```
6. **Check repository state:**
   ```bash
   terraform state list
   ```

### **1. Terraform State Show**
```bash
terraform state show github_repository.repo
```
**Output:**
```yaml
# github_repository.repo:
resource "github_repository" "repo" {
    allow_auto_merge            = false
    allow_merge_commit          = true
    allow_rebase_merge          = true
    allow_squash_merge          = true
    allow_update_branch         = false
    archived                    = false
    auto_init                   = true
    default_branch              = "master"
    delete_branch_on_merge      = false
    description                 = "Core course labs repository managed by Terraform"
    etag                        = "W/\"32a1c6095422b96b3873d6ccca24eecd2b0b24d5ac458dda47f7a975a6b09473\""
    full_name                   = "Friedox/S25-core-course-labs"
    git_clone_url               = "git://github.com/Friedox/S25-core-course-labs.git"
    has_discussions             = false
    has_downloads               = false
    has_issues                  = true
    has_projects                = false
    has_wiki                    = false
    homepage_url                = null
    html_url                    = "https://github.com/Friedox/S25-core-course-labs"
    http_clone_url              = "https://github.com/Friedox/S25-core-course-labs.git"
    id                          = "S25-core-course-labs"
    is_template                 = false
    merge_commit_message        = "PR_TITLE"
    merge_commit_title          = "MERGE_MESSAGE"
    name                        = "S25-core-course-labs"
    node_id                     = "R_kgDONxuO6A"
    primary_language            = "HTML"
    private                     = false
    repo_id                     = 924552936
    squash_merge_commit_message = "COMMIT_MESSAGES"
    squash_merge_commit_title   = "COMMIT_OR_PR_TITLE"
    ssh_clone_url               = "git@github.com:Friedox/S25-core-course-labs.git"
    svn_url                     = "https://github.com/Friedox/S25-core-course-labs"
    topics                      = []
    visibility                  = "public"
    vulnerability_alerts        = false
    web_commit_signoff_required = false

    security_and_analysis {
        secret_scanning {
            status = "enabled"
        }
        secret_scanning_push_protection {
            status = "enabled"
        }
    }
}
```

---

### **2. Terraform State List**
```bash
terraform state list
```
**Output:**
```bash
github_branch_protection.main_protection
github_repository.repo
```

---

### **Terraform Best Practices**

#### **Docker**
- Use Terraform variables to configure containers.
- Store Docker images in a remote registry (Docker Hub).

#### **Yandex Cloud**
- Store authentication keys (`key.json`) securely and exclude them from version control.
- Use variable files (`terraform.tfvars`) to manage cloud credentials.
- Define resource names dynamically using input variables.

#### **GitHub**
- Store sensitive GitHub tokens as environment variables.
- Use `terraform import` to manage existing repositories.
