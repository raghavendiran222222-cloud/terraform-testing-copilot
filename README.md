# Terraform Azure Module: ACR and Container Apps

## Summary
This module provisions an **Azure Container Registry (ACR)** and an **Azure Container Apps Environment with Container Apps** following enterprise standards for security, tagging, and naming conventions.

---

## Requirements
- **Terraform**: >= 1.5.0
- **Provider**: azurerm >= 3.85.0

---

## Features
- Creates Azure Container Registry with admin disabled.
- Creates Container App Environment and one or more Container Apps.
- Enforces HTTPS-only and minimal TLS 1.2.
- Applies mandatory tagging policy.

---

## Usage
```hcl
module "container_apps" {
  source  = "git::https://github.com/raghavendiran222222-cloud/terraform-testing-copilot.git?ref=v1.0.0"

  resource_group_name = "rg-eng-app-dev-eus-001"
  location            = "East US"
  acr_name            = "engacrdeveus001"

  container_apps = {
    app1 = {
      image = "nginx:latest"
      cpu   = 0.5
      memory = "1Gi"
    }
  }

  tags = {
    Application          = "MyApp"
    CreationDate         = "04/22/2026"
    DevOwner             = "raghavendirann@presidio.com"
    BusinessOwner        = "business.owner@company.com"
    Environment          = "dev"
    CostCenter           = "CC123"
    DataClassification   = "Unrestricted"
    BusinessCriticality  = "Medium"
    Compliance           = "CIS"
  }
}
```

---

## Resources Created
- `azurerm_container_registry`
- `azurerm_container_app_environment`
- `azurerm_container_app`

---

## Inputs
| Name | Type | Default | Description |
|------|------|---------|-------------|
| `resource_group_name` | string | n/a | Target Azure Resource Group |
| `location` | string | n/a | Azure region |
| `acr_name` | string | n/a | Name for the Azure Container Registry |
| `container_apps` | map(object) | n/a | Map of container apps config |
| `tags` | map(string) | n/a | Mandatory tags |

---

## Outputs
| Name | Description |
|------|-------------|
| `acr_id` | ID of Azure Container Registry |
| `acr_login_server` | Login server name for ACR |
| `container_apps_map` | Map of deployed Container Apps IDs and names |

---

## Example
See [examples/basic](examples/basic) for a fully working configuration.

---

## Maintained By
**Presidio Terraform IaC Team**
