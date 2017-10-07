---
title: aaaInstall i konfigurowanie maszyn wirtualnych tooprovision Terraform oraz innych infrastruktury na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall i skonfigurować Terraform toocreate Azure zasobów"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: b6706f53b21347442def05a592c30a2d22718984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>Instalowanie i konfigurowanie maszyn wirtualnych tooprovision Terraform oraz innych infrastruktury na platformie Azure 
W tym artykule opisano tooinstall niezbędne kroki hello i skonfiguruj Terraform tooprovision zasobów, takich jak maszyny wirtualne na platformie Azure. Dowiesz się, jak toocreate i używanie usługi Azure poświadczenia zasobów w chmurze tooprovision Terraform tooenable w bezpieczny sposób.

HashiCorp Terraform zapewnia prosty sposób toodefine i wdrażania infrastruktury chmurowej przy użyciu języka tworzenia szablonów niestandardowych o nazwie HashiCorp konfiguracji języka (HCL). Ten język niestandardowy jest [toowrite łatwe i łatwe toounderstand](terraform-create-complete-vm.md). Ponadto, za pomocą hello `terraform plan` polecenia, można zwizualizować hello zmiany tooyour infrastruktury przed ich zatwierdzeniu. Wykonaj te kroki toostart, przy użyciu Terraform w usłudze Azure.

## <a name="install-terraform"></a>Zainstaluj Terraform
tooinstall Terraform, [Pobierz](https://www.terraform.io/downloads.html) odpowiednie dla systemu operacyjnego w katalogu instalacji oddzielny pakiet hello. Pobieranie Hello zawiera pojedynczy plik wykonywalny, dla którego należy także zdefiniować globalnego ścieżki. Aby uzyskać instrukcje dotyczące sposobu tooset hello ścieżka w systemie Linux i komputerów Mac przejdź za[tej strony sieci Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux). Aby uzyskać instrukcje dotyczące sposobu tooset hello ścieżka w systemie Windows, przejdź zbyt[tej strony sieci Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows). tooverify instalację, uruchom hello `terraform` polecenia. Należy wyświetlić listę dostępnych opcji Terraform jako dane wyjściowe.

Następnie należy tooallow Terraform dostępu tooyour Azure tooperform infrastruktury obsługi administracyjnej subskrypcji.

## <a name="set-up-terraform-access-tooazure"></a>Konfigurowanie tooAzure dostępu Terraform
tooenable Terraform tooprovision zasobów na platformie Azure, należy toocreate dwie jednostki w usłudze Azure Active Directory (Azure AD): aplikacji usługi Azure AD i nazwę główną usługi Azure AD. Następnie należy użyć tych jednostek identyfikatorów w skryptach Terraform. Nazwy głównej usługi jest lokalne wystąpienie programu globalny usługi Azure AD aplikacji. Nazwy głównej usługi umożliwia szczegółowe dostępu lokalnego kontroli tooglobal zasobów.

Istnieje kilka sposobów toocreate aplikacji usługi Azure AD i nazwę główną usługi Azure AD. Witaj, łatwiejsze i szybsze sposób obecnie jest toouse 2.0 interfejsu wiersza polecenia Azure, która [można pobrać i zainstalować w systemie Windows, Linux lub Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Można też użyć programu PowerShell lub interfejsu wiersza polecenia platformy Azure w wersji 1.0 infrastruktury zabezpieczeń wymaganymi hello toocreate. Postępuj zgodnie z instrukcjami Hello przedstawia sposób tooconfigure Terraform na platformie Azure przy użyciu wszystkich tych metod.

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>Użyj 2.0 interfejsu wiersza polecenia platformy Azure (dla użytkowników systemu Windows, Linux lub Mac.) 
Po pobraniu i zainstalowaniu hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), zaloguj się tooadminister subskrypcji platformy Azure przez wystawienie hello następujące polecenie:

```
az login
```

>[!NOTE]
>Jeśli używasz Chin hello platformy Azure w Niemczech i chmury Azure dla instytucji rządowych, należy toofirst Konfigurowanie hello toowork wiersza polecenia platformy Azure przy użyciu tej chmury. Można to zrobić, uruchamiając następujące hello:

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

Jeśli masz wiele subskrypcji Azure, ich szczegóły są zwracane przez hello `az login` polecenia. Zestaw hello `SUBSCRIPTION_ID` zwracana wartość hello toohold zmiennej środowiskowej hello `id` pola hello subskrypcji ma toouse. 

Ustaw subskrypcji hello mają toouse dla tej sesji.

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

Kwerenda subskrypcji hello Identyfikatora tooget hello i wartości Identyfikatora dzierżawy.

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

Następnie należy utworzyć osobne funkcje poświadczeń dla Terraform.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

Identyfikator aplikacji, hasło i sp_name oraz dzierżawy są zwracane. Zanotuj identyfikator aplikacji hello i hasło.

tooconfirm poświadczeń (nazwy głównej usługi), Otwórz nowe powłokę i uruchom następujące polecenia hello. SUBSTITUTE hello zwracane wartości sp_name, hasło i dzierżawy:

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>Przy użyciu programu PowerShell (w przypadku użytkowników systemu Windows) 
toouse systemu Windows maszyny toowrite i wykonywanie programu Terraform skryptów i toouse programu PowerShell dla zadań konfiguracji, należy skonfigurować komputer z hello odpowiednich narzędzi programu PowerShell. 

1. Zainstaluj narzędzia programu PowerShell, wykonując kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). 

2. Pobieranie i uruchamianie hello [azure setup.ps1 skryptu](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) z konsoli programu PowerShell hello.

3. toorun hello azure setup.ps1 skryptu, Pobierz i wykonaj hello `./azure-setup.ps1 setup` polecenie z konsoli programu PowerShell hello. Następnie zaloguj się tooyour subskrypcji platformy Azure z uprawnieniami administracyjnymi.

4. Podaj nazwę aplikacji (dowolny ciąg, wymagane) po wyświetleniu monitu. Opcjonalnie wpisz silne hasło po wyświetleniu monitu. Jeśli nie podasz hasła, silne hasło zostanie wygenerowany przy użyciu bibliotek .NET zabezpieczeń.

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>Użyj interfejsu wiersza polecenia platformy Azure w wersji 1.0 (dla systemu Linux lub Mac. użytkowników)
tooget pracę z Terraform na maszynach z systemem Linux lub Mac z Azure CLI w wersji 1.0, bibliotek prawidłowego hello instalacji na tym komputerze.  

1. Zainstaluj narzędzia interfejsu wiersza polecenia xPlat platformy Azure, wykonując kroki hello w [zainstalować Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). 

2. Pobierz i zainstaluj procesor JSON, wykonując instrukcje hello w [Pobierz jq](https://stedolan.github.io/jq/download/).

3. Pobieranie i uruchamianie hello [azure setup.sh skryptu](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash skryptu z hello konsoli.

4. toorun hello azure setup.sh skryptu, Pobierz i wykonaj hello `./azure-setup setup` polecenie hello konsoli. Następnie zaloguj się tooyour subskrypcji platformy Azure z uprawnieniami administracyjnymi.
 
5. Podaj nazwę aplikacji (dowolny ciąg, wymagane) po wyświetleniu monitu. Opcjonalnie wpisz silne hasło po wyświetleniu monitu. Jeśli nie podasz hasła, silne hasło zostanie wygenerowany przy użyciu bibliotek .NET zabezpieczeń.

Wszystkie wcześniejsze skrypty hello Utwórz aplikację usługi Azure AD i usługi podmiotu zabezpieczeń. nazwy głównej usługi Hello pobiera współautora lub dostęp na poziomie właściciela na powitania subskrypcji. Ze względu na powitania wysokiego poziomu udzielono dostępu zawsze należy chronić informacje o zabezpieczeniach hello wygenerowane przez tych skryptów. Zanotuj wszystkie cztery części zabezpieczeń informacji dostarczonych przez tych skryptów: appId, hasła, IDENTYFIKATOR_SUBSKRYPCJI i tenant_id.

## <a name="set-environment-variables"></a>Ustaw zmienne środowiskowe
Po utworzeniu i skonfigurowaniu nazwy głównej usługi Azure AD, należy toolet Terraform wiedzieć hello Identyfikatora dzierżawy, identyfikator subskrypcji, identyfikator klienta i toouse tajnego klienta. Możesz zrobić to poprzez zastosowanie tych wartości w skryptach Terraform, zgodnie z opisem w [tworzenia podstawowej infrastruktury przy użyciu Terraform](terraform-create-complete-vm.md). Alternatywnie można ustawić hello następujące zmienne środowiskowe (i w związku z tym uniknąć przypadkowego ewidencjonowanie lub udostępniania poświadczeń):

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

Można użyć tego tooset skryptu powłoki próbki tych zmiennych:

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

Ponadto Terraform użytkownik korzysta z platformy Azure w Chinach, lub opcję Azure dla instytucji rządowych lub platformy Azure w Niemczech, należy najpierw zmiennej środowiskowej hello tooset odpowiednio.

## <a name="next-steps"></a>Następne kroki
Teraz zainstalowaniu Terraform i skonfigurować poświadczenia platformy Azure, dzięki czemu możesz przystąpić do wdrażania infrastruktury do Twojej subskrypcji platformy Azure. Następnie Dowiedz się, jak za[tworzenie infrastruktury z Terraform](terraform-create-complete-vm.md).
