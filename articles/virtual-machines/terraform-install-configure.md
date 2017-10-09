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
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="94ada-103">Instalowanie i konfigurowanie maszyn wirtualnych tooprovision Terraform oraz innych infrastruktury na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="94ada-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="94ada-104">W tym artykule opisano tooinstall niezbędne kroki hello i skonfiguruj Terraform tooprovision zasobów, takich jak maszyny wirtualne na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="94ada-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="94ada-105">Dowiesz się, jak toocreate i używanie usługi Azure poświadczenia zasobów w chmurze tooprovision Terraform tooenable w bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="94ada-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="94ada-106">HashiCorp Terraform zapewnia prosty sposób toodefine i wdrażania infrastruktury chmurowej przy użyciu języka tworzenia szablonów niestandardowych o nazwie HashiCorp konfiguracji języka (HCL).</span><span class="sxs-lookup"><span data-stu-id="94ada-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="94ada-107">Ten język niestandardowy jest [toowrite łatwe i łatwe toounderstand](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="94ada-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="94ada-108">Ponadto, za pomocą hello `terraform plan` polecenia, można zwizualizować hello zmiany tooyour infrastruktury przed ich zatwierdzeniu.</span><span class="sxs-lookup"><span data-stu-id="94ada-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="94ada-109">Wykonaj te kroki toostart, przy użyciu Terraform w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="94ada-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="94ada-110">Zainstaluj Terraform</span><span class="sxs-lookup"><span data-stu-id="94ada-110">Install Terraform</span></span>
<span data-ttu-id="94ada-111">tooinstall Terraform, [Pobierz](https://www.terraform.io/downloads.html) odpowiednie dla systemu operacyjnego w katalogu instalacji oddzielny pakiet hello.</span><span class="sxs-lookup"><span data-stu-id="94ada-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="94ada-112">Pobieranie Hello zawiera pojedynczy plik wykonywalny, dla którego należy także zdefiniować globalnego ścieżki.</span><span class="sxs-lookup"><span data-stu-id="94ada-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="94ada-113">Aby uzyskać instrukcje dotyczące sposobu tooset hello ścieżka w systemie Linux i komputerów Mac przejdź za[tej strony sieci Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="94ada-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="94ada-114">Aby uzyskać instrukcje dotyczące sposobu tooset hello ścieżka w systemie Windows, przejdź zbyt[tej strony sieci Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="94ada-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="94ada-115">tooverify instalację, uruchom hello `terraform` polecenia.</span><span class="sxs-lookup"><span data-stu-id="94ada-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="94ada-116">Należy wyświetlić listę dostępnych opcji Terraform jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="94ada-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="94ada-117">Następnie należy tooallow Terraform dostępu tooyour Azure tooperform infrastruktury obsługi administracyjnej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="94ada-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="94ada-118">Konfigurowanie tooAzure dostępu Terraform</span><span class="sxs-lookup"><span data-stu-id="94ada-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="94ada-119">tooenable Terraform tooprovision zasobów na platformie Azure, należy toocreate dwie jednostki w usłudze Azure Active Directory (Azure AD): aplikacji usługi Azure AD i nazwę główną usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ada-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="94ada-120">Następnie należy użyć tych jednostek identyfikatorów w skryptach Terraform.</span><span class="sxs-lookup"><span data-stu-id="94ada-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="94ada-121">Nazwy głównej usługi jest lokalne wystąpienie programu globalny usługi Azure AD aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94ada-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="94ada-122">Nazwy głównej usługi umożliwia szczegółowe dostępu lokalnego kontroli tooglobal zasobów.</span><span class="sxs-lookup"><span data-stu-id="94ada-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="94ada-123">Istnieje kilka sposobów toocreate aplikacji usługi Azure AD i nazwę główną usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94ada-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="94ada-124">Witaj, łatwiejsze i szybsze sposób obecnie jest toouse 2.0 interfejsu wiersza polecenia Azure, która [można pobrać i zainstalować w systemie Windows, Linux lub Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="94ada-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="94ada-125">Można też użyć programu PowerShell lub interfejsu wiersza polecenia platformy Azure w wersji 1.0 infrastruktury zabezpieczeń wymaganymi hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="94ada-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="94ada-126">Postępuj zgodnie z instrukcjami Hello przedstawia sposób tooconfigure Terraform na platformie Azure przy użyciu wszystkich tych metod.</span><span class="sxs-lookup"><span data-stu-id="94ada-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="94ada-127">Użyj 2.0 interfejsu wiersza polecenia platformy Azure (dla użytkowników systemu Windows, Linux lub Mac.)</span><span class="sxs-lookup"><span data-stu-id="94ada-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="94ada-128">Po pobraniu i zainstalowaniu hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), zaloguj się tooadminister subskrypcji platformy Azure przez wystawienie hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="94ada-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="94ada-129">Jeśli używasz Chin hello platformy Azure w Niemczech i chmury Azure dla instytucji rządowych, należy toofirst Konfigurowanie hello toowork wiersza polecenia platformy Azure przy użyciu tej chmury.</span><span class="sxs-lookup"><span data-stu-id="94ada-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="94ada-130">Można to zrobić, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="94ada-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="94ada-131">Jeśli masz wiele subskrypcji Azure, ich szczegóły są zwracane przez hello `az login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="94ada-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="94ada-132">Zestaw hello `SUBSCRIPTION_ID` zwracana wartość hello toohold zmiennej środowiskowej hello `id` pola hello subskrypcji ma toouse.</span><span class="sxs-lookup"><span data-stu-id="94ada-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="94ada-133">Ustaw subskrypcji hello mają toouse dla tej sesji.</span><span class="sxs-lookup"><span data-stu-id="94ada-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="94ada-134">Kwerenda subskrypcji hello Identyfikatora tooget hello i wartości Identyfikatora dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="94ada-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="94ada-135">Następnie należy utworzyć osobne funkcje poświadczeń dla Terraform.</span><span class="sxs-lookup"><span data-stu-id="94ada-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="94ada-136">Identyfikator aplikacji, hasło i sp_name oraz dzierżawy są zwracane.</span><span class="sxs-lookup"><span data-stu-id="94ada-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="94ada-137">Zanotuj identyfikator aplikacji hello i hasło.</span><span class="sxs-lookup"><span data-stu-id="94ada-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="94ada-138">tooconfirm poświadczeń (nazwy głównej usługi), Otwórz nowe powłokę i uruchom następujące polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="94ada-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="94ada-139">SUBSTITUTE hello zwracane wartości sp_name, hasło i dzierżawy:</span><span class="sxs-lookup"><span data-stu-id="94ada-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="94ada-140">Przy użyciu programu PowerShell (w przypadku użytkowników systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="94ada-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="94ada-141">toouse systemu Windows maszyny toowrite i wykonywanie programu Terraform skryptów i toouse programu PowerShell dla zadań konfiguracji, należy skonfigurować komputer z hello odpowiednich narzędzi programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94ada-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="94ada-142">Zainstaluj narzędzia programu PowerShell, wykonując kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="94ada-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="94ada-143">Pobieranie i uruchamianie hello [azure setup.ps1 skryptu](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) z konsoli programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="94ada-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="94ada-144">toorun hello azure setup.ps1 skryptu, Pobierz i wykonaj hello `./azure-setup.ps1 setup` polecenie z konsoli programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="94ada-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="94ada-145">Następnie zaloguj się tooyour subskrypcji platformy Azure z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="94ada-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="94ada-146">Podaj nazwę aplikacji (dowolny ciąg, wymagane) po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="94ada-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="94ada-147">Opcjonalnie wpisz silne hasło po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="94ada-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="94ada-148">Jeśli nie podasz hasła, silne hasło zostanie wygenerowany przy użyciu bibliotek .NET zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="94ada-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="94ada-149">Użyj interfejsu wiersza polecenia platformy Azure w wersji 1.0 (dla systemu Linux lub Mac. użytkowników)</span><span class="sxs-lookup"><span data-stu-id="94ada-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="94ada-150">tooget pracę z Terraform na maszynach z systemem Linux lub Mac z Azure CLI w wersji 1.0, bibliotek prawidłowego hello instalacji na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="94ada-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="94ada-151">Zainstaluj narzędzia interfejsu wiersza polecenia xPlat platformy Azure, wykonując kroki hello w [zainstalować Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="94ada-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="94ada-152">Pobierz i zainstaluj procesor JSON, wykonując instrukcje hello w [Pobierz jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="94ada-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="94ada-153">Pobieranie i uruchamianie hello [azure setup.sh skryptu](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash skryptu z hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="94ada-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="94ada-154">toorun hello azure setup.sh skryptu, Pobierz i wykonaj hello `./azure-setup setup` polecenie hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="94ada-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="94ada-155">Następnie zaloguj się tooyour subskrypcji platformy Azure z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="94ada-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="94ada-156">Podaj nazwę aplikacji (dowolny ciąg, wymagane) po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="94ada-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="94ada-157">Opcjonalnie wpisz silne hasło po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="94ada-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="94ada-158">Jeśli nie podasz hasła, silne hasło zostanie wygenerowany przy użyciu bibliotek .NET zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="94ada-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="94ada-159">Wszystkie wcześniejsze skrypty hello Utwórz aplikację usługi Azure AD i usługi podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="94ada-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="94ada-160">nazwy głównej usługi Hello pobiera współautora lub dostęp na poziomie właściciela na powitania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="94ada-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="94ada-161">Ze względu na powitania wysokiego poziomu udzielono dostępu zawsze należy chronić informacje o zabezpieczeniach hello wygenerowane przez tych skryptów.</span><span class="sxs-lookup"><span data-stu-id="94ada-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="94ada-162">Zanotuj wszystkie cztery części zabezpieczeń informacji dostarczonych przez tych skryptów: appId, hasła, IDENTYFIKATOR_SUBSKRYPCJI i tenant_id.</span><span class="sxs-lookup"><span data-stu-id="94ada-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="94ada-163">Ustaw zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="94ada-163">Set environment variables</span></span>
<span data-ttu-id="94ada-164">Po utworzeniu i skonfigurowaniu nazwy głównej usługi Azure AD, należy toolet Terraform wiedzieć hello Identyfikatora dzierżawy, identyfikator subskrypcji, identyfikator klienta i toouse tajnego klienta.</span><span class="sxs-lookup"><span data-stu-id="94ada-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="94ada-165">Możesz zrobić to poprzez zastosowanie tych wartości w skryptach Terraform, zgodnie z opisem w [tworzenia podstawowej infrastruktury przy użyciu Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="94ada-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="94ada-166">Alternatywnie można ustawić hello następujące zmienne środowiskowe (i w związku z tym uniknąć przypadkowego ewidencjonowanie lub udostępniania poświadczeń):</span><span class="sxs-lookup"><span data-stu-id="94ada-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="94ada-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="94ada-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="94ada-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="94ada-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="94ada-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="94ada-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="94ada-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="94ada-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="94ada-171">Można użyć tego tooset skryptu powłoki próbki tych zmiennych:</span><span class="sxs-lookup"><span data-stu-id="94ada-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="94ada-172">Ponadto Terraform użytkownik korzysta z platformy Azure w Chinach, lub opcję Azure dla instytucji rządowych lub platformy Azure w Niemczech, należy najpierw zmiennej środowiskowej hello tooset odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="94ada-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94ada-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94ada-173">Next steps</span></span>
<span data-ttu-id="94ada-174">Teraz zainstalowaniu Terraform i skonfigurować poświadczenia platformy Azure, dzięki czemu możesz przystąpić do wdrażania infrastruktury do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94ada-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="94ada-175">Następnie Dowiedz się, jak za[tworzenie infrastruktury z Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="94ada-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
