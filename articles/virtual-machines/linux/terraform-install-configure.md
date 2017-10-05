---
title: "Instalowanie i konfigurowanie Terraform do obsługi administracyjnej maszyn wirtualnych i innych infrastruktury na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować i skonfigurować Terraform tworzenie zasobów Azure"
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
ms.openlocfilehash: da567097be38ac649c6bf1de1508de24d21cb877
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-terraform-to-provision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="4ea28-103">Instalowanie i konfigurowanie Terraform do obsługi administracyjnej maszyn wirtualnych i innych infrastruktury na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4ea28-103">Install and configure Terraform to provision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="4ea28-104">W tym artykule opisano kroki niezbędne do zainstalowania i skonfigurowania Terraform do udostępniania zasobów, takich jak maszyny wirtualne na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea28-104">This article describes the necessary steps to install and configure Terraform to provision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="4ea28-105">Zostanie sposób tworzenia i używania Azure poświadczenia umożliwiające Terraform do udostępniania zasobów w chmurze w bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="4ea28-105">You will learn how to create and use Azure credentials to enable Terraform to provision cloud resources in a secure manner.</span></span>

<span data-ttu-id="4ea28-106">HashiCorp Terraform zapewnia prosty sposób definiowania i wdrażania infrastruktury chmurowej przy użyciu języka tworzenia szablonów niestandardowych o nazwie HashiCorp konfiguracji języka (HCL).</span><span class="sxs-lookup"><span data-stu-id="4ea28-106">HashiCorp Terraform provides an easy way to define and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="4ea28-107">Ten język niestandardowy jest [ułatwia pisanie i łatwy do zrozumienia](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="4ea28-107">This custom language is [easy to write and easy to understand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="4ea28-108">Ponadto przy użyciu `terraform plan` polecenia, można zwizualizować zmian w infrastrukturze przed je zatwierdzić.</span><span class="sxs-lookup"><span data-stu-id="4ea28-108">Additionally, by using the `terraform plan` command, you can visualize the changes to your infrastructure before you commit them.</span></span> <span data-ttu-id="4ea28-109">Wykonaj następujące kroki, aby rozpocząć korzystanie z platformy Azure, Terraform.</span><span class="sxs-lookup"><span data-stu-id="4ea28-109">Follow these steps to start using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="4ea28-110">Zainstaluj Terraform</span><span class="sxs-lookup"><span data-stu-id="4ea28-110">Install Terraform</span></span>
<span data-ttu-id="4ea28-111">Aby zainstalować Terraform, [Pobierz](https://www.terraform.io/downloads.html) katalog instalacji odpowiedni dla systemu operacyjnego do oddzielnego pakietu.</span><span class="sxs-lookup"><span data-stu-id="4ea28-111">To install Terraform, [download](https://www.terraform.io/downloads.html) the package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="4ea28-112">Pobieranie zawiera pojedynczy plik wykonywalny, dla którego należy także zdefiniować globalnego ścieżki.</span><span class="sxs-lookup"><span data-stu-id="4ea28-112">The download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="4ea28-113">Aby uzyskać instrukcje dotyczące ustawiania ścieżka w systemie Linux i komputerów Mac, przejdź do [tej strony sieci Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="4ea28-113">For instructions on how to set the path on Linux and Mac, go to [this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="4ea28-114">Aby uzyskać instrukcje dotyczące ustawiania ścieżka w systemie Windows, przejdź do [tej strony sieci Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="4ea28-114">For instructions on how to set the path on Windows, go to [this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="4ea28-115">Aby zweryfikować instalację, uruchom `terraform` polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ea28-115">To verify your installation, run the `terraform` command.</span></span> <span data-ttu-id="4ea28-116">Należy wyświetlić listę dostępnych opcji Terraform jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4ea28-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="4ea28-117">Następnie należy Terraform dostęp do Twojej subskrypcji platformy Azure w celu obsługi infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="4ea28-117">Next, you need to allow Terraform access to your Azure subscription to perform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-to-azure"></a><span data-ttu-id="4ea28-118">Konfigurowanie Terraform dostępu do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4ea28-118">Set up Terraform access to Azure</span></span>
<span data-ttu-id="4ea28-119">Aby włączyć Terraform do udostępniania zasobów na platformie Azure, musisz utworzyć dwie jednostki w usłudze Azure Active Directory (Azure AD): aplikacji usługi Azure AD i nazwę główną usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ea28-119">To enable Terraform to provision resources into Azure, you need to create two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="4ea28-120">Następnie należy użyć tych jednostek identyfikatorów w skryptach Terraform.</span><span class="sxs-lookup"><span data-stu-id="4ea28-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="4ea28-121">Nazwy głównej usługi jest lokalne wystąpienie programu globalny usługi Azure AD aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4ea28-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="4ea28-122">Nazwy głównej usługi umożliwia kontrolę szczegółowego lokalnego dostępu do zasobów globalnych.</span><span class="sxs-lookup"><span data-stu-id="4ea28-122">A service principal allows granular local access control to global resources.</span></span>

<span data-ttu-id="4ea28-123">Istnieje kilka sposobów, aby utworzyć aplikację usługi Azure AD i usługi Azure AD podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4ea28-123">There are several ways to create an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="4ea28-124">Łatwiejsze i szybsze sposób dzisiaj jest użycie interfejsu wiersza polecenia Azure 2.0, którego [można pobrać i zainstalować w systemie Windows, Linux lub Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4ea28-124">The easiest and fastest way today is to use Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="4ea28-125">Możesz również służy programu PowerShell lub interfejsu wiersza polecenia platformy Azure w wersji 1.0 do tworzenia infrastruktury zabezpieczeń wymaganymi.</span><span class="sxs-lookup"><span data-stu-id="4ea28-125">You also can use PowerShell or Azure CLI 1.0 to create the necessary security infrastructure.</span></span> <span data-ttu-id="4ea28-126">Postępuj zgodnie z instrukcjami pokazują, jak skonfigurować Terraform na platformie Azure przy użyciu wszystkich tych metod.</span><span class="sxs-lookup"><span data-stu-id="4ea28-126">The instructions that follow show you how to configure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="4ea28-127">Użyj 2.0 interfejsu wiersza polecenia platformy Azure (dla użytkowników systemu Windows, Linux lub Mac.)</span><span class="sxs-lookup"><span data-stu-id="4ea28-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="4ea28-128">Po pobraniu i zainstalowaniu [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), zaloguj się do administrowania subskrypcji platformy Azure, wydając polecenie:</span><span class="sxs-lookup"><span data-stu-id="4ea28-128">After you download and install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in to administer your Azure subscription by issuing the following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="4ea28-129">Jeśli używasz Chin platformy Azure w Niemczech i chmury Azure dla instytucji rządowych, należy najpierw skonfigurować wiersza polecenia platformy Azure, aby pracować z tej chmury.</span><span class="sxs-lookup"><span data-stu-id="4ea28-129">If you use the China, Azure Germany, or Azure Government clouds, you need to first configure the Azure CLI to work with that cloud.</span></span> <span data-ttu-id="4ea28-130">Można to zrobić, uruchamiając następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4ea28-130">You can do this by running the following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="4ea28-131">Jeśli masz wiele subskrypcji Azure, ich szczegóły są zwracane przez `az login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ea28-131">If you have multiple Azure subscriptions, their details are returned by the `az login` command.</span></span> <span data-ttu-id="4ea28-132">Ustaw `SUBSCRIPTION_ID` zmiennej środowiskowej, aby pomieścić wartość zwracana `id` pole z subskrypcji, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="4ea28-132">Set the `SUBSCRIPTION_ID` environment variable to hold the value of the returned `id` field from the subscription you want to use.</span></span> 

<span data-ttu-id="4ea28-133">Ustaw subskrypcji, która ma być używana dla tej sesji.</span><span class="sxs-lookup"><span data-stu-id="4ea28-133">Set the subscription that you want to use for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="4ea28-134">Zapytania względem konta można uzyskać Identyfikatora i dzierżawcy wartości Identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4ea28-134">Query the account to get the subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="4ea28-135">Następnie należy utworzyć osobne funkcje poświadczeń dla Terraform.</span><span class="sxs-lookup"><span data-stu-id="4ea28-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="4ea28-136">Identyfikator aplikacji, hasło i sp_name oraz dzierżawy są zwracane.</span><span class="sxs-lookup"><span data-stu-id="4ea28-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="4ea28-137">Zanotuj identyfikator appId i hasło.</span><span class="sxs-lookup"><span data-stu-id="4ea28-137">Make a note of the appId and password.</span></span>

<span data-ttu-id="4ea28-138">Aby potwierdzić poświadczeń (nazwy głównej usługi), Otwórz nowe powłokę i uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ea28-138">To confirm your credentials (service principal), open a new shell and run the following commands.</span></span> <span data-ttu-id="4ea28-139">Zastąp wartości zwracane sp_name, hasło i dzierżawy:</span><span class="sxs-lookup"><span data-stu-id="4ea28-139">Substitute the returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="4ea28-140">Przy użyciu programu PowerShell (w przypadku użytkowników systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="4ea28-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="4ea28-141">Aby użyć komputera z systemem Windows do zapisu i wykonywania skryptów Terraform i przy użyciu programu PowerShell dla zadań konfiguracji, należy skonfigurować komputer z odpowiednich narzędzi programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ea28-141">To use a Windows machine to write and execute your Terraform scripts and to use PowerShell for configuration tasks, configure your machine with the right PowerShell tools.</span></span> 

1. <span data-ttu-id="4ea28-142">Zainstaluj narzędzia programu PowerShell, wykonując kroki opisane w [Instalowanie i konfigurowanie programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="4ea28-142">Install PowerShell tools by following the steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="4ea28-143">Pobieranie i uruchamianie [azure setup.ps1 skryptu](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) z konsoli programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ea28-143">Download and execute the [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from the PowerShell console.</span></span>

3. <span data-ttu-id="4ea28-144">Aby uruchomić skrypt azure setup.ps1, pobierz go i wykonaj `./azure-setup.ps1 setup` polecenie z poziomu konsoli programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ea28-144">To run the azure-setup.ps1 script, download it and execute the `./azure-setup.ps1 setup` command from the PowerShell console.</span></span> <span data-ttu-id="4ea28-145">Następnie zaloguj się do subskrypcji platformy Azure z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="4ea28-145">Then sign in to your Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="4ea28-146">Podaj nazwę aplikacji (dowolny ciąg, wymagane) po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="4ea28-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="4ea28-147">Opcjonalnie wpisz silne hasło po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="4ea28-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="4ea28-148">Jeśli nie podasz hasła, silne hasło zostanie wygenerowany przy użyciu bibliotek .NET zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4ea28-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="4ea28-149">Użyj interfejsu wiersza polecenia platformy Azure w wersji 1.0 (dla systemu Linux lub Mac. użytkowników)</span><span class="sxs-lookup"><span data-stu-id="4ea28-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="4ea28-150">Aby rozpocząć pracę z Terraform na maszynach z systemem Linux lub Mac z interfejsu wiersza polecenia platformy Azure w wersji 1.0, należy zainstalować właściwego bibliotek na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4ea28-150">To get started with Terraform on Linux machines or Macs with Azure CLI 1.0, install the proper libraries on your machine.</span></span>  

1. <span data-ttu-id="4ea28-151">Instalowanie narzędzi interfejsu wiersza polecenia xPlat platformy Azure, wykonując kroki opisane w [zainstalować Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4ea28-151">Install Azure xPlat CLI tools by following the steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="4ea28-152">Pobierz i zainstaluj procesor JSON zgodnie z instrukcjami w [Pobierz jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="4ea28-152">Download and install a JSON processor by following the instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="4ea28-153">Pobieranie i uruchamianie [azure setup.sh skryptu](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash skryptów z poziomu konsoli.</span><span class="sxs-lookup"><span data-stu-id="4ea28-153">Download and execute the [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from the console.</span></span>

4. <span data-ttu-id="4ea28-154">Aby uruchomić skrypt azure setup.sh, pobierz go i wykonaj `./azure-setup setup` polecenie z poziomu konsoli.</span><span class="sxs-lookup"><span data-stu-id="4ea28-154">To run the azure-setup.sh script, download it and execute the `./azure-setup setup` command from the console.</span></span> <span data-ttu-id="4ea28-155">Następnie zaloguj się do subskrypcji platformy Azure z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="4ea28-155">Then sign in to your Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="4ea28-156">Podaj nazwę aplikacji (dowolny ciąg, wymagane) po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="4ea28-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="4ea28-157">Opcjonalnie wpisz silne hasło po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="4ea28-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="4ea28-158">Jeśli nie podasz hasła, silne hasło zostanie wygenerowany przy użyciu bibliotek .NET zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4ea28-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="4ea28-159">Wcześniejsze skrypty Utwórz aplikację usługi Azure AD i usługi podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4ea28-159">All the previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="4ea28-160">Nazwy głównej usługi pobiera współautora lub dostęp na poziomie właściciela subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4ea28-160">The service principal gets a contributor or owner-level access on the subscription.</span></span> <span data-ttu-id="4ea28-161">Z powodu wysokiego poziomu udzielono dostępu zawsze należy chronić informacje zabezpieczeń wygenerowane przez tych skryptów.</span><span class="sxs-lookup"><span data-stu-id="4ea28-161">Because of the high level of access granted, you should always protect the security information generated by those scripts.</span></span> <span data-ttu-id="4ea28-162">Zanotuj wszystkie cztery części zabezpieczeń informacji dostarczonych przez tych skryptów: appId, hasła, IDENTYFIKATOR_SUBSKRYPCJI i tenant_id.</span><span class="sxs-lookup"><span data-stu-id="4ea28-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="4ea28-163">Ustaw zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="4ea28-163">Set environment variables</span></span>
<span data-ttu-id="4ea28-164">Po utworzeniu i skonfigurowaniu nazwy głównej usługi Azure AD, należy umożliwić Terraform wiedzieć dzierżawcy ID, identyfikator subskrypcji identyfikator klienta i klucz tajny klienta do użycia.</span><span class="sxs-lookup"><span data-stu-id="4ea28-164">After you create and configure an Azure AD service principal, you need to let Terraform know the tenant ID, subscription ID, client ID, and client secret to use.</span></span> <span data-ttu-id="4ea28-165">Możesz zrobić to poprzez zastosowanie tych wartości w skryptach Terraform, zgodnie z opisem w [tworzenia podstawowej infrastruktury przy użyciu Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="4ea28-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="4ea28-166">Alternatywnie można ustawić następujące zmienne środowiskowe (i w związku z tym uniknąć przypadkowego ewidencjonowanie lub udostępniania poświadczeń):</span><span class="sxs-lookup"><span data-stu-id="4ea28-166">Alternately, you can set the following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="4ea28-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="4ea28-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="4ea28-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="4ea28-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="4ea28-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="4ea28-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="4ea28-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="4ea28-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="4ea28-171">Ten przykładowy skrypt powłoki umożliwia ustawienie tych zmiennych:</span><span class="sxs-lookup"><span data-stu-id="4ea28-171">You can use this sample shell script to set those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="4ea28-172">Ponadto jeśli używasz Terraform Azure w Chinach, lub opcję Azure dla instytucji rządowych lub platformy Azure w Niemczech, należy ustawić zmienną ŚRODOWISKOWĄ odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="4ea28-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need to set the ENVIRONMENT variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ea28-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ea28-173">Next steps</span></span>
<span data-ttu-id="4ea28-174">Teraz zainstalowaniu Terraform i skonfigurować poświadczenia platformy Azure, dzięki czemu możesz przystąpić do wdrażania infrastruktury do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ea28-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="4ea28-175">Następnie Dowiedz się, jak [tworzenie infrastruktury z Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="4ea28-175">Next, learn how to [create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
