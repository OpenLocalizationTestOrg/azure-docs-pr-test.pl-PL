---
title: "Obliczeń platformy Azure — rozszerzenie Diagnostyka systemu Linux | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować Azure Linux diagnostycznych rozszerzenia (LAD) do zbierania metryk i rejestrowania zdarzeń z maszyn wirtualnych systemu Linux działających na platformie Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 525d706bd709ae72f2dca1c21e06db533ccf32b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-linux-diagnostic-extension-to-monitor-metrics-and-logs"></a><span data-ttu-id="12a4f-103">Rozszerzenie diagnostycznych Linux służy do monitorowania, metryki i dzienniki</span><span class="sxs-lookup"><span data-stu-id="12a4f-103">Use Linux Diagnostic Extension to monitor metrics and logs</span></span>

<span data-ttu-id="12a4f-104">W tym dokumencie opisano w wersji 3.0 oraz nowszych rozszerzenia diagnostyczne systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="12a4f-104">This document describes version 3.0 and newer of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12a4f-105">Informacje o wersji 2.3 i starsze, zobacz [tego dokumentu](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="12a4f-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="12a4f-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="12a4f-106">Introduction</span></span>

<span data-ttu-id="12a4f-107">Rozszerzenie diagnostycznych Linux pomaga użytkownika monitora kondycji maszyny Wirtualnej systemu Linux uruchomiony w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-107">The Linux Diagnostic Extension helps a user monitor the health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="12a4f-108">Ma ona następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="12a4f-108">It has the following capabilities:</span></span>

* <span data-ttu-id="12a4f-109">Zbiera metryki wydajności systemu z maszyny Wirtualnej i zapisuje je w określonej tabeli w ramach konta magazynu wyznaczonego.</span><span class="sxs-lookup"><span data-stu-id="12a4f-109">Collects system performance metrics from the VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="12a4f-110">Pobiera zdarzenia dziennika z syslog i przechowuje je w określonej tabeli w ramach konta magazynu wyznaczonego.</span><span class="sxs-lookup"><span data-stu-id="12a4f-110">Retrieves log events from syslog and stores them in a specific table in the designated storage account.</span></span>
* <span data-ttu-id="12a4f-111">Umożliwia dostosowanie metryk dane są zbierane i przekazać.</span><span class="sxs-lookup"><span data-stu-id="12a4f-111">Enables users to customize the data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="12a4f-112">Umożliwia dostosowanie urządzeń syslog i poziomy ważności zdarzeń, które są zbierane i przekazać.</span><span class="sxs-lookup"><span data-stu-id="12a4f-112">Enables users to customize the syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="12a4f-113">Umożliwia użytkownikom na przekazywanie do tabeli magazynu wyznaczonego określone pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="12a4f-113">Enables users to upload specified log files to a designated storage table.</span></span>
* <span data-ttu-id="12a4f-114">Obsługuje wysyłanie metryki i dziennik zdarzeń do dowolnego EventHub punktów końcowych i formacie JSON obiekty BLOB na koncie magazynu wyznaczonego.</span><span class="sxs-lookup"><span data-stu-id="12a4f-114">Supports sending metrics and log events to arbitrary EventHub endpoints and JSON-formatted blobs in the designated storage account.</span></span>

<span data-ttu-id="12a4f-115">To rozszerzenie współpracuje z obu modeli wdrażania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-the-extension-in-your-vm"></a><span data-ttu-id="12a4f-116">Instalowanie rozszerzenia w maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="12a4f-116">Installing the extension in your VM</span></span>

<span data-ttu-id="12a4f-117">To rozszerzenie można włączyć za pomocą poleceń cmdlet programu Azure PowerShell, skryptów wiersza polecenia platformy Azure lub szablony wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-117">You can enable this extension by using the Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="12a4f-118">Aby uzyskać więcej informacji, zobacz [funkcji rozszerzenia](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="12a4f-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="12a4f-119">Azure portal nie można włączyć lub skonfigurować LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="12a4f-119">The Azure portal cannot be used to enable or configure LAD 3.0.</span></span> <span data-ttu-id="12a4f-120">Zamiast tego instaluje i konfiguruje wersji 2.3.</span><span class="sxs-lookup"><span data-stu-id="12a4f-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="12a4f-121">Wykresy portalu Azure i alerty pracować z danymi obie wersje rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="12a4f-121">Azure portal graphs and alerts work with data from both versions of the extension.</span></span>

<span data-ttu-id="12a4f-122">Te instrukcje instalacji i [do pobrania Przykładowa konfiguracja](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) LAD 3.0 można skonfigurować:</span><span class="sxs-lookup"><span data-stu-id="12a4f-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="12a4f-123">przechwycenie i zapisanie te same metryki, ponieważ dostarczonych przez LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="12a4f-123">capture and store the same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="12a4f-124">Przechwyć zbiór przydatne metryki systemu plików, nowe 3.0 LAD;</span><span class="sxs-lookup"><span data-stu-id="12a4f-124">capture a useful set of file system metrics, new to LAD 3.0;</span></span>
* <span data-ttu-id="12a4f-125">Przechwytywanie domyślnej kolekcji syslog włączane przez LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="12a4f-125">capture the default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="12a4f-126">Włącz portalu Azure obsługi wykresów i alerty na metryki maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12a4f-126">enable the Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="12a4f-127">Do pobrania konfiguracji jest tylko przykładowe; Zmodyfikuj go do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="12a4f-127">The downloadable configuration is just an example; modify it to suit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="12a4f-128">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="12a4f-128">Prerequisites</span></span>

* <span data-ttu-id="12a4f-129">**Agenta systemu Linux platformy Azure w wersji 2.2.0 lub nowszym**.</span><span class="sxs-lookup"><span data-stu-id="12a4f-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="12a4f-130">Większość obrazów Galeria Linux maszyny Wirtualnej Azure zawierają wersję 2.2.7 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="12a4f-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="12a4f-131">Uruchom `/usr/sbin/waagent -version` o potwierdzenie wersja zainstalowana na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12a4f-131">Run `/usr/sbin/waagent -version` to confirm the version installed on the VM.</span></span> <span data-ttu-id="12a4f-132">Jeśli maszyna wirtualna działa starszą wersję agenta gościa, należy wykonać [tych instrukcji](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) go zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="12a4f-132">If the VM is running an older version of the guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to update it.</span></span>
* <span data-ttu-id="12a4f-133">**Interfejs wiersza polecenia platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="12a4f-133">**Azure CLI**.</span></span> <span data-ttu-id="12a4f-134">[Konfigurowanie programu Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) środowiska na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="12a4f-134">[Set up the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="12a4f-135">Polecenie wget, jeśli nie masz jeszcze go: Uruchom `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-135">The wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="12a4f-136">Istniejącą subskrypcję platformy Azure i istniejące konto magazynu w niej do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="12a4f-136">An existing Azure subscription and an existing storage account within it to store the data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="12a4f-137">Przykładowe instalacji</span><span class="sxs-lookup"><span data-stu-id="12a4f-137">Sample installation</span></span>

<span data-ttu-id="12a4f-138">Podaj prawidłowe parametry w pierwszych trzech wierszy, a następnie wykonaj ten skrypt jako katalogu głównego:</span><span class="sxs-lookup"><span data-stu-id="12a4f-138">Fill in the correct parameters on the first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login to Azure first before anything else
az login

# Select the subscription containing the storage account
az account set --subscription <your_azure_subscription_id>

# Download the sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build the VM resource ID. Replace storage account name and resource ID in the public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build the protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure to install and enable the extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="12a4f-139">Adres URL Przykładowa konfiguracja i jego zawartość, mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-139">The URL for the sample configuration, and its contents, are subject to change.</span></span> <span data-ttu-id="12a4f-140">Pobierz kopię pliku JSON ustawienia portalu i dostosować go do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="12a4f-140">Download a copy of the portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="12a4f-141">Wszystkie szablony lub automatyzacji, który można skonstruować należy używać własną kopię zamiast pobierania zawsze tego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="12a4f-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-the-extension-settings"></a><span data-ttu-id="12a4f-142">Aktualizowanie ustawień rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="12a4f-142">Updating the extension settings</span></span>

<span data-ttu-id="12a4f-143">Po zmianie ustawienia publiczne lub chronione, na których je wdrożyć na maszynie wirtualnej za pomocą tego samego polecenia.</span><span class="sxs-lookup"><span data-stu-id="12a4f-143">After you've changed your Protected or Public settings, deploy them to the VM by running the same command.</span></span> <span data-ttu-id="12a4f-144">Jeśli jakieś zmiany w ustawieniach, zaktualizowano ustawienia są wysyłane do rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="12a4f-144">If anything changed in the settings, the updated settings are sent to the extension.</span></span> <span data-ttu-id="12a4f-145">LAD ponowne załadowanie konfiguracji i uruchamia się ponownie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-145">LAD reloads the configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-the-extension"></a><span data-ttu-id="12a4f-146">Migracja z poprzednich wersji rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="12a4f-146">Migration from previous versions of the extension</span></span>

<span data-ttu-id="12a4f-147">Najnowsza wersja rozszerzenia **3.0**.</span><span class="sxs-lookup"><span data-stu-id="12a4f-147">The latest version of the extension is **3.0**.</span></span> <span data-ttu-id="12a4f-148">**Wszystkie starsze wersje (2.x) są przestarzałe i mogą być publikowane na wcześniejsze niż 31 lipca 2018**.</span><span class="sxs-lookup"><span data-stu-id="12a4f-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12a4f-149">To rozszerzenie wprowadzono istotne zmiany w konfiguracji rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="12a4f-149">This extension introduces breaking changes to the configuration of the extension.</span></span> <span data-ttu-id="12a4f-150">Taka zmiana została wprowadzona w celu zwiększenia bezpieczeństwa rozszerzenia. w związku z tym zapewnienia zgodności z 2.x nie można wykonać konserwacji.</span><span class="sxs-lookup"><span data-stu-id="12a4f-150">One such change was made to improve the security of the extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="12a4f-151">Ponadto wydawcy rozszerzenia dla tego rozszerzenia jest inny niż wydawcy dla wersji 2.x.</span><span class="sxs-lookup"><span data-stu-id="12a4f-151">Also, the Extension Publisher for this extension is different than the publisher for the 2.x versions.</span></span>
>
> <span data-ttu-id="12a4f-152">Aby przeprowadzić migrację z 2.x do nowej wersji rozszerzenia, należy odinstalować stary rozszerzenia (pod starą nazwę wydawcy), a następnie zainstaluj rozszerzenie w wersji 3.</span><span class="sxs-lookup"><span data-stu-id="12a4f-152">To migrate from 2.x to this new version of the extension, you must uninstall the old extension (under the old publisher name), then install version 3 of the extension.</span></span>

<span data-ttu-id="12a4f-153">Zalecenia:</span><span class="sxs-lookup"><span data-stu-id="12a4f-153">Recommendations:</span></span>

* <span data-ttu-id="12a4f-154">Uaktualnianie wersji pomocniczej automatyczne włączone, należy zainstalować rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-154">Install the extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="12a4f-155">W klasycznym modelu wdrażania maszyn wirtualnych należy określić "3.*" jako wersja instalowania rozszerzenia za pomocą interfejsu wiersza polecenia XPLAT platformy Azure lub programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="12a4f-155">On classic deployment model VMs, specify '3.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="12a4f-156">We wdrożeniu usługi Azure Resource Manager modelu maszyn wirtualnych, obejmują ""autoUpgradeMinorVersion": true" w szablonie wdrożenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12a4f-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span>
* <span data-ttu-id="12a4f-157">Użyj nowego/innego konta magazynu dla LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="12a4f-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="12a4f-158">Istnieje kilka małych niezgodności między LAD 2.3 i LAD 3.0 powodujących, że udostępnianie powodującymi konta:</span><span class="sxs-lookup"><span data-stu-id="12a4f-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="12a4f-159">LAD 3.0 przechowuje zdarzenia dziennika systemowego w tabeli z inną nazwą.</span><span class="sxs-lookup"><span data-stu-id="12a4f-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="12a4f-160">CounterSpecifier ciągów dla `builtin` metryki różnią się w LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="12a4f-160">The counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="12a4f-161">Ustawienia chronionego</span><span class="sxs-lookup"><span data-stu-id="12a4f-161">Protected settings</span></span>

<span data-ttu-id="12a4f-162">Ten zestaw informacji o konfiguracji zawiera poufne informacje, które powinny być chronione w widoku publicznych, na przykład poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="12a4f-163">Te ustawienia są przesyłane do i przechowywane przez rozszerzenie w postaci zaszyfrowanej.</span><span class="sxs-lookup"><span data-stu-id="12a4f-163">These settings are transmitted to and stored by the extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "the storage account to receive data",
    "storageAccountEndPoint": "the hostname suffix for the cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="12a4f-164">Nazwa</span><span class="sxs-lookup"><span data-stu-id="12a4f-164">Name</span></span> | <span data-ttu-id="12a4f-165">Wartość</span><span class="sxs-lookup"><span data-stu-id="12a4f-165">Value</span></span>
---- | -----
<span data-ttu-id="12a4f-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="12a4f-166">storageAccountName</span></span> | <span data-ttu-id="12a4f-167">Nazwa konta magazynu, w którym dane są zapisywane przez rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-167">The name of the storage account in which data is written by the extension.</span></span>
<span data-ttu-id="12a4f-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="12a4f-168">storageAccountEndPoint</span></span> | <span data-ttu-id="12a4f-169">(opcjonalnie) Punkt końcowy identyfikowanie chmury, w której istnieje konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-169">(optional) The endpoint identifying the cloud in which the storage account exists.</span></span> <span data-ttu-id="12a4f-170">Jeśli to ustawienie jest nieobecne, LAD domyślnie chmurze publicznej Azure `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-170">If this setting is absent, LAD defaults to the Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="12a4f-171">Aby korzystać z konta magazynu platformy Azure w Niemczech, Azure dla instytucji rządowych lub chińskiej wersji platformy Azure, w związku z tym Ustaw tę wartość.</span><span class="sxs-lookup"><span data-stu-id="12a4f-171">To use a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="12a4f-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="12a4f-172">storageAccountSasToken</span></span> | <span data-ttu-id="12a4f-173">[Tokenu sygnatury dostępu Współdzielonego konta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) usług obiektów Blob i tabeli (`ss='bt'`), mające zastosowanie do kontenerów i obiektów (`srt='co'`), która przyznaje dodać, tworzenie listy, aktualizacji i uprawnienia do zapisu (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="12a4f-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable to containers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="12a4f-174">Czy *nie* zawierać wiodących znak zapytania (?).</span><span class="sxs-lookup"><span data-stu-id="12a4f-174">Do *not* include the leading question-mark (?).</span></span>
<span data-ttu-id="12a4f-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="12a4f-175">mdsdHttpProxy</span></span> | <span data-ttu-id="12a4f-176">(opcjonalnie) Wymagane do włączenia rozszerzenia do nawiązania połączenia z określonego konta magazynu i punktu końcowego informacji serwera proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="12a4f-176">(optional) HTTP proxy information needed to enable the extension to connect to the specified storage account and endpoint.</span></span>
<span data-ttu-id="12a4f-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="12a4f-177">sinksConfig</span></span> | <span data-ttu-id="12a4f-178">(opcjonalnie) Szczegóły dotyczące alternatywnych miejsc docelowych, do których mogą być dostarczane metryk i zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="12a4f-178">(optional) Details of alternative destinations to which metrics and events can be delivered.</span></span> <span data-ttu-id="12a4f-179">W poniższych sekcjach opisano konkretne szczegółowe informacje o każdym ujścia danych obsługiwane przez rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-179">The specific details of each data sink supported by the extension are covered in the sections that follow.</span></span>

<span data-ttu-id="12a4f-180">Można łatwo utworzyć wymagany token sygnatury dostępu Współdzielonego za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-180">You can easily construct the required SAS token through the Azure portal.</span></span>

1. <span data-ttu-id="12a4f-181">Wybierz konto magazynu ogólnego przeznaczenia, do którego mają rozszerzenie do zapisu</span><span class="sxs-lookup"><span data-stu-id="12a4f-181">Select the general-purpose storage account to which you want the extension to write</span></span>
1. <span data-ttu-id="12a4f-182">Wybierz opcję "Udostępniania sygnatury dostępu" z części ustawień menu po lewej stronie</span><span class="sxs-lookup"><span data-stu-id="12a4f-182">Select "Shared access signature" from the Settings part of the left menu</span></span>
1. <span data-ttu-id="12a4f-183">Wprowadź odpowiednie części, jak opisano wcześniej</span><span class="sxs-lookup"><span data-stu-id="12a4f-183">Make the appropriate sections as previously described</span></span>
1. <span data-ttu-id="12a4f-184">Kliknij przycisk "Generowanie sygnatury dostępu Współdzielonego".</span><span class="sxs-lookup"><span data-stu-id="12a4f-184">Click the "Generate SAS" button.</span></span>

![Obraz](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="12a4f-186">Skopiuj wygenerowany SAS do pola storageAccountSasToken; Usuń znak znaku zapytania ("?").</span><span class="sxs-lookup"><span data-stu-id="12a4f-186">Copy the generated SAS into the storageAccountSasToken field; remove the leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="12a4f-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="12a4f-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="12a4f-188">Ta sekcja opcjonalna definiuje dodatkowe miejsc docelowych, do których rozszerzenie wysyła zebrane informacje.</span><span class="sxs-lookup"><span data-stu-id="12a4f-188">This optional section defines additional destinations to which the extension sends the information it collects.</span></span> <span data-ttu-id="12a4f-189">Tablica "sink" zawiera obiekt dla każdego obiektu sink dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="12a4f-189">The "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="12a4f-190">Atrybut "type" Określa inne atrybuty w obiekcie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-190">The "type" attribute determines the other attributes in the object.</span></span>

<span data-ttu-id="12a4f-191">Element</span><span class="sxs-lookup"><span data-stu-id="12a4f-191">Element</span></span> | <span data-ttu-id="12a4f-192">Wartość</span><span class="sxs-lookup"><span data-stu-id="12a4f-192">Value</span></span>
------- | -----
<span data-ttu-id="12a4f-193">name</span><span class="sxs-lookup"><span data-stu-id="12a4f-193">name</span></span> | <span data-ttu-id="12a4f-194">Ciąg używany do odwoływania się do tego obiektu sink występującego w konfiguracji rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="12a4f-194">A string used to refer to this sink elsewhere in the extension configuration.</span></span>
<span data-ttu-id="12a4f-195">type</span><span class="sxs-lookup"><span data-stu-id="12a4f-195">type</span></span> | <span data-ttu-id="12a4f-196">Typ ujścia definiowanego.</span><span class="sxs-lookup"><span data-stu-id="12a4f-196">The type of sink being defined.</span></span> <span data-ttu-id="12a4f-197">Określa (jeśli istnieją) inne wartości w wystąpień tego typu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-197">Determines the other values (if any) in instances of this type.</span></span>

<span data-ttu-id="12a4f-198">Wersja 3.0 rozszerzenia diagnostycznych Linux obsługuje dwa typy zbiornika: EventHub i JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="12a4f-198">Version 3.0 of the Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="the-eventhub-sink"></a><span data-ttu-id="12a4f-199">Obiekt sink EventHub</span><span class="sxs-lookup"><span data-stu-id="12a4f-199">The EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="12a4f-200">Wpis "sasURL" zawiera pełny adres URL tokenu sygnatury dostępu Współdzielonego, w tym Centrum zdarzeń, do którego powinien zostać opublikowany, dane.</span><span class="sxs-lookup"><span data-stu-id="12a4f-200">The "sasURL" entry contains the full URL, including SAS token, for the Event Hub to which data should be published.</span></span> <span data-ttu-id="12a4f-201">LAD wymaga sygnatury dostępu Współdzielonego nazewnictwa zasad, która umożliwia wysyłanie oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="12a4f-201">LAD requires a SAS naming a policy that enables the Send claim.</span></span> <span data-ttu-id="12a4f-202">Przykład:</span><span class="sxs-lookup"><span data-stu-id="12a4f-202">An example:</span></span>

* <span data-ttu-id="12a4f-203">Tworzenie przestrzeni nazw usługi Event Hubs, o nazwie`contosohub`</span><span class="sxs-lookup"><span data-stu-id="12a4f-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="12a4f-204">Tworzenie Centrum zdarzeń w obszarze nazw o nazwie`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="12a4f-204">Create an Event Hub in the namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="12a4f-205">Tworzenie zasad dostępu współużytkowanego w Centrum zdarzeń o nazwie `writer` , który umożliwia wysyłanie oświadczeń</span><span class="sxs-lookup"><span data-stu-id="12a4f-205">Create a Shared access policy on the Event Hub named `writer` that enables the Send claim</span></span>

<span data-ttu-id="12a4f-206">Jeśli utworzono sygnatury dostępu Współdzielonego dobra do północy czasu UTC 1 stycznia 2018 wartość sasURL może być:</span><span class="sxs-lookup"><span data-stu-id="12a4f-206">If you created a SAS good until midnight UTC on January 1, 2018, the sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="12a4f-207">Aby uzyskać więcej informacji na temat generowania tokeny sygnatury dostępu Współdzielonego usługi Event hubs, zobacz [tej strony sieci web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="12a4f-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="the-jsonblob-sink"></a><span data-ttu-id="12a4f-208">Obiekt sink JsonBlob</span><span class="sxs-lookup"><span data-stu-id="12a4f-208">The JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="12a4f-209">Dane, skierowane do ujścia JsonBlob są przechowywane w obiektach BLOB w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-209">Data directed to a JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="12a4f-210">Każde wystąpienie LAD tworzy obiektu blob co godzinę dla każdej nazwy obiektu sink.</span><span class="sxs-lookup"><span data-stu-id="12a4f-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="12a4f-211">Każdy obiekt blob jest zawsze zawiera nieprawidłową składnię tablicy JSON obiektu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="12a4f-212">Nowe wpisy są automatycznie dodawane do tablicy.</span><span class="sxs-lookup"><span data-stu-id="12a4f-212">New entries are atomically added to the array.</span></span> <span data-ttu-id="12a4f-213">Obiekty BLOB są przechowywane w kontenerze o takiej samej nazwie jak obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="12a4f-213">Blobs are stored in a container with the same name as the sink.</span></span> <span data-ttu-id="12a4f-214">Zasady usługi Azure storage dla nazwy kontenera obiektów blob się do nazwy wychwytywanie JsonBlob: od 3 do 63 małe znaki alfanumeryczne ASCII lub łączniki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-214">The Azure storage rules for blob container names apply to the names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="12a4f-215">Ustawienia publicznego</span><span class="sxs-lookup"><span data-stu-id="12a4f-215">Public settings</span></span>

<span data-ttu-id="12a4f-216">Ta struktura zawiera bloki różnych ustawień kontrolujących informacje zebrane przez rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-216">This structure contains various blocks of settings that control the information collected by the extension.</span></span> <span data-ttu-id="12a4f-217">Każde ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="12a4f-217">Each setting is optional.</span></span> <span data-ttu-id="12a4f-218">Jeśli określisz `ladCfg`, należy także określić `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "the storage account to receive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="12a4f-219">Element</span><span class="sxs-lookup"><span data-stu-id="12a4f-219">Element</span></span> | <span data-ttu-id="12a4f-220">Wartość</span><span class="sxs-lookup"><span data-stu-id="12a4f-220">Value</span></span>
------- | -----
<span data-ttu-id="12a4f-221">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="12a4f-221">StorageAccount</span></span> | <span data-ttu-id="12a4f-222">Nazwa konta magazynu, w którym dane są zapisywane przez rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-222">The name of the storage account in which data is written by the extension.</span></span> <span data-ttu-id="12a4f-223">Muszą być tej samej nazwie, jak określono w [chronionych ustawień](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="12a4f-223">Must be the same name as is specified in the [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="12a4f-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="12a4f-224">mdsdHttpProxy</span></span> | <span data-ttu-id="12a4f-225">(opcjonalnie) Sam jak w [chronionych ustawień](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="12a4f-225">(optional) Same as in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="12a4f-226">Wartość publicznego jest zastępowany przez wartość prywatne, jeśli ustawiona.</span><span class="sxs-lookup"><span data-stu-id="12a4f-226">The public value is overridden by the private value, if set.</span></span> <span data-ttu-id="12a4f-227">Umieść ustawienia serwera proxy, które zawierają klucz tajny, takie jak hasła, w [chronionych ustawień](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="12a4f-227">Place proxy settings that contain a secret, such as a password, in the [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="12a4f-228">Wszystkie pozostałe elementy zostały szczegółowo opisane w kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="12a4f-228">The remaining elements are described in detail in the following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="12a4f-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="12a4f-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="12a4f-230">To określa opcjonalne struktury wychwytywanie zbieranie metryk i dzienników w celu dostarczania do usługi Azure metryki i innych danych.</span><span class="sxs-lookup"><span data-stu-id="12a4f-230">This optional structure controls the gathering of metrics and logs for delivery to the Azure Metrics service and to other data sinks.</span></span> <span data-ttu-id="12a4f-231">Należy określić `performanceCounters` lub `syslogEvents` lub oba.</span><span class="sxs-lookup"><span data-stu-id="12a4f-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="12a4f-232">Należy określić `metrics` struktury.</span><span class="sxs-lookup"><span data-stu-id="12a4f-232">You must specify the `metrics` structure.</span></span>

<span data-ttu-id="12a4f-233">Element</span><span class="sxs-lookup"><span data-stu-id="12a4f-233">Element</span></span> | <span data-ttu-id="12a4f-234">Wartość</span><span class="sxs-lookup"><span data-stu-id="12a4f-234">Value</span></span>
------- | -----
<span data-ttu-id="12a4f-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="12a4f-235">eventVolume</span></span> | <span data-ttu-id="12a4f-236">(opcjonalnie) Określa liczbę partycji tworzonych w tabeli magazynu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-236">(optional) Controls the number of partitions created within the storage table.</span></span> <span data-ttu-id="12a4f-237">Musi mieć jedną z `"Large"`, `"Medium"`, lub `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="12a4f-238">Jeśli nie zostanie określony, wartością domyślną jest `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-238">If not specified, the default value is `"Medium"`.</span></span>
<span data-ttu-id="12a4f-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="12a4f-239">sampleRateInSeconds</span></span> | <span data-ttu-id="12a4f-240">(opcjonalnie) Domyślny interwał między kolekcję pierwotnych metryki (unaggregated).</span><span class="sxs-lookup"><span data-stu-id="12a4f-240">(optional) The default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="12a4f-241">Szybkość, z najmniejszą obsługiwanych próbki wynosi 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="12a4f-241">The smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="12a4f-242">Jeśli nie zostanie określony, wartością domyślną jest `15`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-242">If not specified, the default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="12a4f-243">metrics</span><span class="sxs-lookup"><span data-stu-id="12a4f-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="12a4f-244">Element</span><span class="sxs-lookup"><span data-stu-id="12a4f-244">Element</span></span> | <span data-ttu-id="12a4f-245">Wartość</span><span class="sxs-lookup"><span data-stu-id="12a4f-245">Value</span></span>
------- | -----
<span data-ttu-id="12a4f-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="12a4f-246">resourceId</span></span> | <span data-ttu-id="12a4f-247">Ustaw identyfikator zasobu usługi Azure Resource Manager z maszyny Wirtualnej lub skali maszyny wirtualnej do której należy maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="12a4f-247">The Azure Resource Manager resource ID of the VM or of the virtual machine scale set to which the VM belongs.</span></span> <span data-ttu-id="12a4f-248">To ustawienie musi być także określona, jeśli wszystkie zbiornika JsonBlob jest używane w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="12a4f-248">This setting must be also specified if any JsonBlob sink is used in the configuration.</span></span>
<span data-ttu-id="12a4f-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="12a4f-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="12a4f-250">Częstotliwość, z jaką metryki agregacji są obliczane i przeniesione do metryki Azure, wyrażona jako czas 8601 jest.</span><span class="sxs-lookup"><span data-stu-id="12a4f-250">The frequency at which aggregate metrics are to be computed and transferred to Azure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="12a4f-251">Najmniejsza okres transfer jest 60 sekund, czyli PT1M.</span><span class="sxs-lookup"><span data-stu-id="12a4f-251">The smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="12a4f-252">Należy określić co najmniej jeden scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="12a4f-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="12a4f-253">Przykłady metryk określone w sekcji liczniki wydajności są zbierane co 15 sekund lub na przykład ocenić jawnie zdefiniowane dla licznika.</span><span class="sxs-lookup"><span data-stu-id="12a4f-253">Samples of the metrics specified in the performanceCounters section are collected every 15 seconds or at the sample rate explicitly defined for the counter.</span></span> <span data-ttu-id="12a4f-254">Jeśli występuje wiele częstotliwości scheduledTransferPeriod (jak pokazano w przykładzie), każdy agregacji jest obliczana niezależnie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-254">If multiple scheduledTransferPeriod frequencies appear (as in the example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="12a4f-255">liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="12a4f-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="12a4f-256">Ta sekcja opcjonalna kontrolę nad zbieraniem metryki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-256">This optional section controls the collection of metrics.</span></span> <span data-ttu-id="12a4f-257">Przykłady pierwotnych są agregowane dla wszystkich [scheduledTransferPeriod](#metrics) do tworzenia tych wartości:</span><span class="sxs-lookup"><span data-stu-id="12a4f-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) to produce these values:</span></span>

* <span data-ttu-id="12a4f-258">Średnia</span><span class="sxs-lookup"><span data-stu-id="12a4f-258">mean</span></span>
* <span data-ttu-id="12a4f-259">Minimalna</span><span class="sxs-lookup"><span data-stu-id="12a4f-259">minimum</span></span>
* <span data-ttu-id="12a4f-260">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="12a4f-260">maximum</span></span>
* <span data-ttu-id="12a4f-261">wartości zbierane przez ostatnie</span><span class="sxs-lookup"><span data-stu-id="12a4f-261">last-collected value</span></span>
* <span data-ttu-id="12a4f-262">Liczba próbek raw, używany do obliczania wartości zagregowanej</span><span class="sxs-lookup"><span data-stu-id="12a4f-262">count of raw samples used to compute the aggregate</span></span>

<span data-ttu-id="12a4f-263">Element</span><span class="sxs-lookup"><span data-stu-id="12a4f-263">Element</span></span> | <span data-ttu-id="12a4f-264">Wartość</span><span class="sxs-lookup"><span data-stu-id="12a4f-264">Value</span></span>
------- | -----
<span data-ttu-id="12a4f-265">sink — obiekty</span><span class="sxs-lookup"><span data-stu-id="12a4f-265">sinks</span></span> | <span data-ttu-id="12a4f-266">(opcjonalnie) Rozdzielana przecinkami lista nazw wychwytywanie, do których LAD wysyła zagregowane metryki wyników.</span><span class="sxs-lookup"><span data-stu-id="12a4f-266">(optional) A comma-separated list of names of sinks to which LAD sends aggregated metric results.</span></span> <span data-ttu-id="12a4f-267">Wszystkie metryki zagregowane są publikowane do każdej z wymienionych ujścia.</span><span class="sxs-lookup"><span data-stu-id="12a4f-267">All aggregated metrics are published to each listed sink.</span></span> <span data-ttu-id="12a4f-268">Zobacz [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="12a4f-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="12a4f-269">Przykład: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="12a4f-270">type</span><span class="sxs-lookup"><span data-stu-id="12a4f-270">type</span></span> | <span data-ttu-id="12a4f-271">Określa dostawcę rzeczywiste metryki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-271">Identifies the actual provider of the metric.</span></span>
<span data-ttu-id="12a4f-272">Klasy</span><span class="sxs-lookup"><span data-stu-id="12a4f-272">class</span></span> | <span data-ttu-id="12a4f-273">Wraz z "licznika" identyfikuje określonej metryki w obszarze nazw dostawcy.</span><span class="sxs-lookup"><span data-stu-id="12a4f-273">Together with "counter", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="12a4f-274">Licznik</span><span class="sxs-lookup"><span data-stu-id="12a4f-274">counter</span></span> | <span data-ttu-id="12a4f-275">Wraz z "class" identyfikuje określonej metryki w obszarze nazw dostawcy.</span><span class="sxs-lookup"><span data-stu-id="12a4f-275">Together with "class", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="12a4f-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="12a4f-276">counterSpecifier</span></span> | <span data-ttu-id="12a4f-277">Identyfikuje określonej metryki w obszarze nazw metryki Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-277">Identifies the specific metric within the Azure Metrics namespace.</span></span>
<span data-ttu-id="12a4f-278">Warunek</span><span class="sxs-lookup"><span data-stu-id="12a4f-278">condition</span></span> | <span data-ttu-id="12a4f-279">(opcjonalnie) Wybiera konkretne wystąpienie obiektu do którego Metryka stosuje lub wybiera agregacji we wszystkich wystąpieniach tego obiektu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-279">(optional) Selects a specific instance of the object to which the metric applies or selects the aggregation across all instances of that object.</span></span> <span data-ttu-id="12a4f-280">Aby uzyskać więcej informacji, zobacz [ `builtin` definicji metryk](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="12a4f-280">For more information, see the [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="12a4f-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="12a4f-281">sampleRate</span></span> | <span data-ttu-id="12a4f-282">JEST interwałem 8601, która ustawia współczynnik pobierane pierwotnych próbek ta metryka.</span><span class="sxs-lookup"><span data-stu-id="12a4f-282">IS 8601 interval that sets the rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="12a4f-283">Jeśli nie jest ustawiona, kolekcji interwał jest ustawiany przez wartość [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="12a4f-283">If not set, the collection interval is set by the value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="12a4f-284">Najkrótszy częstotliwość próbkowania obsługiwanych wynosi 15 sekund (PT15S).</span><span class="sxs-lookup"><span data-stu-id="12a4f-284">The shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="12a4f-285">jednostki</span><span class="sxs-lookup"><span data-stu-id="12a4f-285">unit</span></span> | <span data-ttu-id="12a4f-286">Powinien być jednym z tych ciągów: "Count", "B", "Seconds", "%", "CountPerSecond", "BytesPerSecond", "Milisekund".</span><span class="sxs-lookup"><span data-stu-id="12a4f-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="12a4f-287">Definiuje jednostkę metryki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-287">Defines the unit for the metric.</span></span> <span data-ttu-id="12a4f-288">Konsumenci danych zebranych oczekuje wartości zebrane dane do tej jednostki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-288">Consumers of the collected data expect the collected data values to match this unit.</span></span> <span data-ttu-id="12a4f-289">LAD są ignorowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-289">LAD ignores this field.</span></span>
<span data-ttu-id="12a4f-290">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="12a4f-290">displayName</span></span> | <span data-ttu-id="12a4f-291">Etykieta (w języku określonym przez ustawienie skojarzone ustawienia regionalne) jest dołączony do tych danych w Azure metryki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-291">The label (in the language specified by the associated locale setting) to be attached to this data in Azure Metrics.</span></span> <span data-ttu-id="12a4f-292">LAD są ignorowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-292">LAD ignores this field.</span></span>

<span data-ttu-id="12a4f-293">CounterSpecifier jest umownym identyfikatorem.</span><span class="sxs-lookup"><span data-stu-id="12a4f-293">The counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="12a4f-294">Konsumenci metryki, Azure portalu wykresów, takich jak i alerty funkcji, użyj counterSpecifier jako "klucza", który identyfikuje metrykę lub wystąpienia metryki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-294">Consumers of metrics, like the Azure portal charting and alerting feature, use counterSpecifier as the "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="12a4f-295">Aby uzyskać `builtin` metryki, zalecane jest użycie counterSpecifier wartości, które zaczynają się od `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="12a4f-296">Określone wystąpienie metryki są zbierane, firma Microsoft zaleca się, że możesz dołączyć do wartości counterSpecifier identyfikator wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="12a4f-296">If you are collecting a specific instance of a metric, we recommend you attach the identifier of the instance to the counterSpecifier value.</span></span> <span data-ttu-id="12a4f-297">Kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="12a4f-297">Some examples:</span></span>

* <span data-ttu-id="12a4f-298">`/builtin/Processor/PercentIdleTime`-Bezczynności uśredniona wszystkich rdzeni</span><span class="sxs-lookup"><span data-stu-id="12a4f-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="12a4f-299">`/builtin/Disk/FreeSpace(/mnt)`-Wolnego miejsca w systemie plików w katalogu/mnt</span><span class="sxs-lookup"><span data-stu-id="12a4f-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for the /mnt filesystem</span></span>
* <span data-ttu-id="12a4f-300">`/builtin/Disk/FreeSpace`— Wolne miejsce uśredniona wszystkie zainstalowane systemy plików</span><span class="sxs-lookup"><span data-stu-id="12a4f-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="12a4f-301">Portalu Azure ani LAD oczekuje, że wartość counterSpecifier na zgodny z żadnym wzorcem.</span><span class="sxs-lookup"><span data-stu-id="12a4f-301">Neither LAD nor the Azure portal expects the counterSpecifier value to match any pattern.</span></span> <span data-ttu-id="12a4f-302">Być zgodne w konstrukcji counterSpecifier wartości.</span><span class="sxs-lookup"><span data-stu-id="12a4f-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="12a4f-303">Po określeniu `performanceCounters`, zawsze LAD zapisuje dane do tabeli w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-303">When you specify `performanceCounters`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="12a4f-304">Może mieć te same dane zapisane obiekty BLOB JSON i/lub centra zdarzeń, ale nie można wyłączyć zapisywanie danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="12a4f-304">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="12a4f-305">Wszystkie wystąpienia rozszerzenia diagnostycznych skonfigurowana do używania tej samej nazwy konta magazynu i punktu końcowego dodać dzienniki i metryk do tej samej tabeli.</span><span class="sxs-lookup"><span data-stu-id="12a4f-305">All instances of the diagnostic extension configured to use the same storage account name and endpoint add their metrics and logs to the same table.</span></span> <span data-ttu-id="12a4f-306">Jeśli pisania zbyt wiele maszyn wirtualnych w tej samej partycji tabeli, Azure można ograniczyć zapisy do tej partycji.</span><span class="sxs-lookup"><span data-stu-id="12a4f-306">If too many VMs are writing to the same table partition, Azure can throttle writes to that partition.</span></span> <span data-ttu-id="12a4f-307">Ustawienie eventVolume powoduje, że wpisy rozpowszechniania przez 10 (małe), 1 (średnia liczba godzin) lub 100 (duży) różnych partycji.</span><span class="sxs-lookup"><span data-stu-id="12a4f-307">The eventVolume setting causes entries to be spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="12a4f-308">Zwykle wystarczające, aby upewnić się, że nie jest ograniczany ruch sieciowy jest "Średnia".</span><span class="sxs-lookup"><span data-stu-id="12a4f-308">Usually, "Medium" is sufficient to ensure traffic is not throttled.</span></span> <span data-ttu-id="12a4f-309">Funkcję metryki Azure w portalu Azure używa danych zawartych w tej tabeli do produkcji wykresy lub wyzwalanie alertów.</span><span class="sxs-lookup"><span data-stu-id="12a4f-309">The Azure Metrics feature of the Azure portal uses the data in this table to produce graphs or to trigger alerts.</span></span> <span data-ttu-id="12a4f-310">Nazwa tabeli jest złączeniem te ciągi:</span><span class="sxs-lookup"><span data-stu-id="12a4f-310">The table name is the concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="12a4f-311">"ScheduledTransferPeriod" zagregowane wartości przechowywane w tabeli</span><span class="sxs-lookup"><span data-stu-id="12a4f-311">The "scheduledTransferPeriod" for the aggregated values stored in the table</span></span>
* `P10DV2S`
* <span data-ttu-id="12a4f-312">Data, w postaci "RRRRMMDD", która zmienia co 10 dni</span><span class="sxs-lookup"><span data-stu-id="12a4f-312">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="12a4f-313">Przykłady obejmują `WADMetricsPT1HP10DV2S20170410` i `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="12a4f-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="12a4f-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="12a4f-315">Ta sekcja opcjonalna kontrolę nad zbieraniem dziennika zdarzeń z dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="12a4f-315">This optional section controls the collection of log events from syslog.</span></span> <span data-ttu-id="12a4f-316">W przypadku pominięcia sekcji zdarzenia dziennika systemowego nie są przechwytywane w ogóle.</span><span class="sxs-lookup"><span data-stu-id="12a4f-316">If the section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="12a4f-317">Kolekcja syslogEventConfiguration ma jeden wpis dla każdego obiektu syslog zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="12a4f-317">The syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="12a4f-318">W przypadku minSeverity "NONE" dla określonego obiektu lub tego obiektu nie ma w elemencie w ogóle, żadne zdarzenia z tym zakładzie są przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="12a4f-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in the element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="12a4f-319">Element</span><span class="sxs-lookup"><span data-stu-id="12a4f-319">Element</span></span> | <span data-ttu-id="12a4f-320">Wartość</span><span class="sxs-lookup"><span data-stu-id="12a4f-320">Value</span></span>
------- | -----
<span data-ttu-id="12a4f-321">sink — obiekty</span><span class="sxs-lookup"><span data-stu-id="12a4f-321">sinks</span></span> | <span data-ttu-id="12a4f-322">Rozdzielana przecinkami lista nazw wychwytywanie, w którym publikowane są zdarzenia dziennika poszczególnych.</span><span class="sxs-lookup"><span data-stu-id="12a4f-322">A comma-separated list of names of sinks to which individual log events are published.</span></span> <span data-ttu-id="12a4f-323">Dopasowywanie ograniczeń w syslogEventConfiguration wszystkie zdarzenia dziennika są publikowane do każdej z wymienionych ujścia.</span><span class="sxs-lookup"><span data-stu-id="12a4f-323">All log events matching the restrictions in syslogEventConfiguration are published to each listed sink.</span></span> <span data-ttu-id="12a4f-324">Przykład: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="12a4f-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="12a4f-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="12a4f-325">facilityName</span></span> | <span data-ttu-id="12a4f-326">Nazwę obiektu syslog (takich jak "dziennika\_użytkownika" lub "dziennika\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="12a4f-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="12a4f-327">Zobacz sekcję "funkcje" [strony man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) dla pełnej listy.</span><span class="sxs-lookup"><span data-stu-id="12a4f-327">See the "facility" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span>
<span data-ttu-id="12a4f-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="12a4f-328">minSeverity</span></span> | <span data-ttu-id="12a4f-329">Poziom ważności syslog (takich jak "dziennika\_błąd" lub "dziennika\_informacje").</span><span class="sxs-lookup"><span data-stu-id="12a4f-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="12a4f-330">Zobacz sekcję "poziomu" [strony man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) dla pełnej listy.</span><span class="sxs-lookup"><span data-stu-id="12a4f-330">See the "level" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span> <span data-ttu-id="12a4f-331">Rozszerzenie przechwytuje zdarzeń wysłanych do funkcji lub wyższym określonego poziomu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-331">The extension captures events sent to the facility at or above the specified level.</span></span>

<span data-ttu-id="12a4f-332">Po określeniu `syslogEvents`, zawsze LAD zapisuje dane do tabeli w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-332">When you specify `syslogEvents`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="12a4f-333">Może mieć te same dane zapisane obiekty BLOB JSON i/lub centra zdarzeń, ale nie można wyłączyć zapisywanie danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="12a4f-333">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="12a4f-334">Zachowanie partycjonowania dla tej tabeli jest taka sama jak `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-334">The partitioning behavior for this table is the same as described for `performanceCounters`.</span></span> <span data-ttu-id="12a4f-335">Nazwa tabeli jest złączeniem te ciągi:</span><span class="sxs-lookup"><span data-stu-id="12a4f-335">The table name is the concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="12a4f-336">Data, w postaci "RRRRMMDD", która zmienia co 10 dni</span><span class="sxs-lookup"><span data-stu-id="12a4f-336">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="12a4f-337">Przykłady obejmują `LinuxSyslog20170410` i `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="12a4f-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="12a4f-338">perfCfg</span></span>

<span data-ttu-id="12a4f-339">Określa tę sekcję, wykonanie dowolnego [OMI](https://github.com/Microsoft/omi) zapytania.</span><span class="sxs-lookup"><span data-stu-id="12a4f-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="12a4f-340">Element</span><span class="sxs-lookup"><span data-stu-id="12a4f-340">Element</span></span> | <span data-ttu-id="12a4f-341">Wartość</span><span class="sxs-lookup"><span data-stu-id="12a4f-341">Value</span></span>
------- | -----
<span data-ttu-id="12a4f-342">przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="12a4f-342">namespace</span></span> | <span data-ttu-id="12a4f-343">(opcjonalnie) Przestrzeń nazw OMI, w którym można wykonać zapytania.</span><span class="sxs-lookup"><span data-stu-id="12a4f-343">(optional) The OMI namespace within which the query should be executed.</span></span> <span data-ttu-id="12a4f-344">Jeśli zostanie określona, wartością domyślną jest "główny/scx", implementowane przez [programu System Center i platform dostawców](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="12a4f-344">If unspecified, the default value is "root/scx", implemented by the [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="12a4f-345">query</span><span class="sxs-lookup"><span data-stu-id="12a4f-345">query</span></span> | <span data-ttu-id="12a4f-346">Zapytanie OMI do wykonania.</span><span class="sxs-lookup"><span data-stu-id="12a4f-346">The OMI query to be executed.</span></span>
<span data-ttu-id="12a4f-347">Tabela</span><span class="sxs-lookup"><span data-stu-id="12a4f-347">table</span></span> | <span data-ttu-id="12a4f-348">(opcjonalnie) W tabeli magazynu systemu Azure w ramach konta magazynu wyznaczonego (zobacz [chronionych ustawień](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="12a4f-348">(optional) The Azure storage table, in the designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="12a4f-349">częstotliwość</span><span class="sxs-lookup"><span data-stu-id="12a4f-349">frequency</span></span> | <span data-ttu-id="12a4f-350">(opcjonalnie) Liczba sekund między wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="12a4f-350">(optional) The number of seconds between execution of the query.</span></span> <span data-ttu-id="12a4f-351">Wartość domyślna to 300 (5 minut); wartość minimalna wynosi 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="12a4f-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="12a4f-352">sink — obiekty</span><span class="sxs-lookup"><span data-stu-id="12a4f-352">sinks</span></span> | <span data-ttu-id="12a4f-353">(opcjonalnie) Rozdzielana przecinkami lista nazw wychwytywanie dodatkowe, do których powinien zostać opublikowany, przykładowe nieprzetworzone wyniki metryki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-353">(optional) A comma-separated list of names of additional sinks to which raw sample metric results should be published.</span></span> <span data-ttu-id="12a4f-354">Bez agregacji te przykłady pierwotnych jest obliczana przez rozszerzenie lub metryk usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-354">No aggregation of these raw samples is computed by the extension or by Azure Metrics.</span></span>

<span data-ttu-id="12a4f-355">Należy określić albo "Tabela" lub "sink" i/lub.</span><span class="sxs-lookup"><span data-stu-id="12a4f-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="12a4f-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="12a4f-356">fileLogs</span></span>

<span data-ttu-id="12a4f-357">Steruje przechwytywania plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="12a4f-357">Controls the capture of log files.</span></span> <span data-ttu-id="12a4f-358">LAD przechwytuje nowych wierszy tekstu, ponieważ są one zapisywane do pliku i zapisuje je w tabeli wiersze i/lub dowolnej określonej wychwytywanie (JsonBlob lub EventHub).</span><span class="sxs-lookup"><span data-stu-id="12a4f-358">LAD captures new text lines as they are written to the file and writes them to table rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="12a4f-359">Element</span><span class="sxs-lookup"><span data-stu-id="12a4f-359">Element</span></span> | <span data-ttu-id="12a4f-360">Wartość</span><span class="sxs-lookup"><span data-stu-id="12a4f-360">Value</span></span>
------- | -----
<span data-ttu-id="12a4f-361">Plik</span><span class="sxs-lookup"><span data-stu-id="12a4f-361">file</span></span> | <span data-ttu-id="12a4f-362">Pełna nazwa ścieżki pliku dziennika, aby być obserwowane i przechwycone.</span><span class="sxs-lookup"><span data-stu-id="12a4f-362">The full pathname of the log file to be watched and captured.</span></span> <span data-ttu-id="12a4f-363">Nazwa ścieżki musi nazwę jednego pliku; Nie można jej nazwę katalogu lub zawierać symbole wieloznaczne.</span><span class="sxs-lookup"><span data-stu-id="12a4f-363">The pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="12a4f-364">Tabela</span><span class="sxs-lookup"><span data-stu-id="12a4f-364">table</span></span> | <span data-ttu-id="12a4f-365">(opcjonalnie) Tabela magazynu Azure w ramach konta magazynu wyznaczonego (określone w konfiguracji chronionym), w którym są zapisywane nowe wiersze z "fragmentu" w pliku.</span><span class="sxs-lookup"><span data-stu-id="12a4f-365">(optional) The Azure storage table, in the designated storage account (as specified in the protected configuration), into which new lines from the "tail" of the file are written.</span></span>
<span data-ttu-id="12a4f-366">sink — obiekty</span><span class="sxs-lookup"><span data-stu-id="12a4f-366">sinks</span></span> | <span data-ttu-id="12a4f-367">(opcjonalnie) Rozdzielana przecinkami lista nazw dodatkowe wychwytywanie do wierszy dziennika, które wysyłane.</span><span class="sxs-lookup"><span data-stu-id="12a4f-367">(optional) A comma-separated list of names of additional sinks to which log lines sent.</span></span>

<span data-ttu-id="12a4f-368">Należy określić albo "Tabela" lub "sink" i/lub.</span><span class="sxs-lookup"><span data-stu-id="12a4f-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-the-builtin-provider"></a><span data-ttu-id="12a4f-369">Metryki obsługiwane przez dostawcę wbudowane</span><span class="sxs-lookup"><span data-stu-id="12a4f-369">Metrics supported by the builtin provider</span></span>

<span data-ttu-id="12a4f-370">Dostawca metryki wbudowane jest źródłem szeroką gamę użytkowników najbardziej interesujące metryki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-370">The builtin metric provider is a source of metrics most interesting to a broad set of users.</span></span> <span data-ttu-id="12a4f-371">Te metryki można podzielić na pięć szerokie klasy:</span><span class="sxs-lookup"><span data-stu-id="12a4f-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="12a4f-372">Procesor</span><span class="sxs-lookup"><span data-stu-id="12a4f-372">Processor</span></span>
* <span data-ttu-id="12a4f-373">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="12a4f-373">Memory</span></span>
* <span data-ttu-id="12a4f-374">Sieć</span><span class="sxs-lookup"><span data-stu-id="12a4f-374">Network</span></span>
* <span data-ttu-id="12a4f-375">System plików</span><span class="sxs-lookup"><span data-stu-id="12a4f-375">Filesystem</span></span>
* <span data-ttu-id="12a4f-376">Dysk</span><span class="sxs-lookup"><span data-stu-id="12a4f-376">Disk</span></span>

### <a name="builtin-metrics-for-the-processor-class"></a><span data-ttu-id="12a4f-377">wbudowane metryki dla klasy procesora</span><span class="sxs-lookup"><span data-stu-id="12a4f-377">builtin metrics for the Processor class</span></span>

<span data-ttu-id="12a4f-378">Klasa procesora metryk udostępnia informacje na temat użycia procesora w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12a4f-378">The Processor class of metrics provides information about processor usage in the VM.</span></span> <span data-ttu-id="12a4f-379">Podczas agregowania wartości procentowych, wynikiem jest średnią przez wszystkie procesory.</span><span class="sxs-lookup"><span data-stu-id="12a4f-379">When aggregating percentages, the result is the average across all CPUs.</span></span> <span data-ttu-id="12a4f-380">W dwa podstawowe maszyny Wirtualnej Jeśli jeden rdzeń był zajęty 100% i innych był bezczynny, 100% zgłoszone PercentIdleTime jest 50.</span><span class="sxs-lookup"><span data-stu-id="12a4f-380">In a two core VM, if one core was 100% busy and the other was 100% idle, the reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="12a4f-381">Jeśli każda core 50% zajęte przez ten sam okres, zgłoszone również będą 50.</span><span class="sxs-lookup"><span data-stu-id="12a4f-381">If each core was 50% busy for the same period, the reported result would also be 50.</span></span> <span data-ttu-id="12a4f-382">W cztery podstawowe maszyny Wirtualnej z jednego rdzenia 100% jest zajęty i innych bezczynny zgłoszone PercentIdleTime jest 75.</span><span class="sxs-lookup"><span data-stu-id="12a4f-382">In a four core VM, with one core 100% busy and the others idle, the reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="12a4f-383">Licznik</span><span class="sxs-lookup"><span data-stu-id="12a4f-383">counter</span></span> | <span data-ttu-id="12a4f-384">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="12a4f-384">Meaning</span></span>
------- | -------
<span data-ttu-id="12a4f-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-385">PercentIdleTime</span></span> | <span data-ttu-id="12a4f-386">Procent czasu, w oknie agregacji, że procesory zostały wykonywania pętli bezczynności jądra</span><span class="sxs-lookup"><span data-stu-id="12a4f-386">Percentage of time during the aggregation window that processors were executing the kernel idle loop</span></span>
<span data-ttu-id="12a4f-387">percentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-387">PercentProcessorTime</span></span> | <span data-ttu-id="12a4f-388">Procent czasu wykonania wątku czynnego</span><span class="sxs-lookup"><span data-stu-id="12a4f-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="12a4f-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-389">PercentIOWaitTime</span></span> | <span data-ttu-id="12a4f-390">Procent czasu oczekiwania na zakończenie operacji We/Wy</span><span class="sxs-lookup"><span data-stu-id="12a4f-390">Percentage of time waiting for IO operations to complete</span></span>
<span data-ttu-id="12a4f-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-391">PercentInterruptTime</span></span> | <span data-ttu-id="12a4f-392">Procent czasu wykonywania sprzęt i oprogramowanie przerwań i wywołań DPC (opóźnione wywołania procedur)</span><span class="sxs-lookup"><span data-stu-id="12a4f-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="12a4f-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-393">PercentUserTime</span></span> | <span data-ttu-id="12a4f-394">Czynnego czasu podczas okna agregacji procent czasu spędzony w użytkownika więcej przy normalnym priorytecie</span><span class="sxs-lookup"><span data-stu-id="12a4f-394">Of non-idle time during the aggregation window, the percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="12a4f-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-395">PercentNiceTime</span></span> | <span data-ttu-id="12a4f-396">Czynnego czasu wartość procentowa działania priorytetem obniżona (nieuprzywilejowany)</span><span class="sxs-lookup"><span data-stu-id="12a4f-396">Of non-idle time, the percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="12a4f-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="12a4f-398">Czas czynnego wartość procentowa działania w trybie uprzywilejowanym (jądra)</span><span class="sxs-lookup"><span data-stu-id="12a4f-398">Of non-idle time, the percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="12a4f-399">Pierwsze cztery liczniki powinien Suma, umożliwiającej 100%.</span><span class="sxs-lookup"><span data-stu-id="12a4f-399">The first four counters should sum to 100%.</span></span> <span data-ttu-id="12a4f-400">Ostatnich trzech również liczniki Suma do 100%; Suma PercentProcessorTime, PercentIOWaitTime i PercentInterruptTime ich podziału.</span><span class="sxs-lookup"><span data-stu-id="12a4f-400">The last three counters also sum to 100%; they subdivide the sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="12a4f-401">Uzyskanie pojedynczego metrykę zagregowane we wszystkich procesorów, wartość `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-401">To obtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="12a4f-402">Aby uzyskać metryki dla określonego procesora, takich jak drugi procesor logiczny z czterech podstawowych maszyny Wirtualnej, należy ustawić `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-402">To obtain a metric for a specific processor, such as the second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="12a4f-403">Numery procesorów logicznych znajdują się w zakresie `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-403">Logical processor numbers are in the range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-the-memory-class"></a><span data-ttu-id="12a4f-404">wbudowane metryki dla klasy pamięci</span><span class="sxs-lookup"><span data-stu-id="12a4f-404">builtin metrics for the Memory class</span></span>

<span data-ttu-id="12a4f-405">Klasa pamięci metryk zawiera informacje o wykorzystanie pamięci, stronicowania i wymiany.</span><span class="sxs-lookup"><span data-stu-id="12a4f-405">The Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="12a4f-406">Licznik</span><span class="sxs-lookup"><span data-stu-id="12a4f-406">counter</span></span> | <span data-ttu-id="12a4f-407">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="12a4f-407">Meaning</span></span>
------- | -------
<span data-ttu-id="12a4f-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="12a4f-408">AvailableMemory</span></span> | <span data-ttu-id="12a4f-409">Dostępnej pamięci fizycznej w MiB</span><span class="sxs-lookup"><span data-stu-id="12a4f-409">Available physical memory in MiB</span></span>
<span data-ttu-id="12a4f-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="12a4f-410">PercentAvailableMemory</span></span> | <span data-ttu-id="12a4f-411">Dostępna pamięć fizyczna jako procent całkowitej ilości pamięci</span><span class="sxs-lookup"><span data-stu-id="12a4f-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="12a4f-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="12a4f-412">UsedMemory</span></span> | <span data-ttu-id="12a4f-413">W użyciu pamięć fizyczna (MiB)</span><span class="sxs-lookup"><span data-stu-id="12a4f-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="12a4f-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="12a4f-414">PercentUsedMemory</span></span> | <span data-ttu-id="12a4f-415">W użyciu pamięć fizyczna jako procent całkowitej ilości pamięci</span><span class="sxs-lookup"><span data-stu-id="12a4f-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="12a4f-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="12a4f-416">PagesPerSec</span></span> | <span data-ttu-id="12a4f-417">Całkowita liczba stronicowania (odczyt/zapis)</span><span class="sxs-lookup"><span data-stu-id="12a4f-417">Total paging (read/write)</span></span>
<span data-ttu-id="12a4f-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="12a4f-418">PagesReadPerSec</span></span> | <span data-ttu-id="12a4f-419">Strony odczytywać kopii magazynu (pliku wymiany, pliku programu, pliku mapowanego itp.)</span><span class="sxs-lookup"><span data-stu-id="12a4f-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="12a4f-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="12a4f-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="12a4f-421">Stron zapisanych do magazynu zapasowego (pliku wymiany, pliku mapowanego itp.)</span><span class="sxs-lookup"><span data-stu-id="12a4f-421">Pages written to backing store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="12a4f-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="12a4f-422">AvailableSwap</span></span> | <span data-ttu-id="12a4f-423">Obszar wymiany nieużywane (MiB)</span><span class="sxs-lookup"><span data-stu-id="12a4f-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="12a4f-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="12a4f-424">PercentAvailableSwap</span></span> | <span data-ttu-id="12a4f-425">Obszar wymiany nieużywane jako procent całkowitego obszaru wymiany</span><span class="sxs-lookup"><span data-stu-id="12a4f-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="12a4f-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="12a4f-426">UsedSwap</span></span> | <span data-ttu-id="12a4f-427">W użyciu obszar wymiany (MiB)</span><span class="sxs-lookup"><span data-stu-id="12a4f-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="12a4f-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="12a4f-428">PercentUsedSwap</span></span> | <span data-ttu-id="12a4f-429">W obsłudze obszaru wymiany w procentach całkowitego obszaru wymiany</span><span class="sxs-lookup"><span data-stu-id="12a4f-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="12a4f-430">Ta klasa metryki ma tylko jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="12a4f-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="12a4f-431">Atrybut "warunku" nie zawiera przydatne ustawień i powinny być pominięte.</span><span class="sxs-lookup"><span data-stu-id="12a4f-431">The "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-the-network-class"></a><span data-ttu-id="12a4f-432">wbudowane metryki dla klasy sieciowe</span><span class="sxs-lookup"><span data-stu-id="12a4f-432">builtin metrics for the Network class</span></span>

<span data-ttu-id="12a4f-433">Klasa sieci metryk zawiera informacje o aktywności sieci dla poszczególnych interfejsów od uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="12a4f-433">The Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="12a4f-434">LAD nie ujawnia przepustowości metryk, które mogą być pobierane z hosta metryki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="12a4f-435">Licznik</span><span class="sxs-lookup"><span data-stu-id="12a4f-435">counter</span></span> | <span data-ttu-id="12a4f-436">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="12a4f-436">Meaning</span></span>
------- | -------
<span data-ttu-id="12a4f-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="12a4f-437">BytesTransmitted</span></span> | <span data-ttu-id="12a4f-438">Całkowita liczba bajtów wysłanych od momentu rozruchu</span><span class="sxs-lookup"><span data-stu-id="12a4f-438">Total bytes sent since boot</span></span>
<span data-ttu-id="12a4f-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="12a4f-439">BytesReceived</span></span> | <span data-ttu-id="12a4f-440">Całkowita liczba bajtów odebranych od rozruchu</span><span class="sxs-lookup"><span data-stu-id="12a4f-440">Total bytes received since boot</span></span>
<span data-ttu-id="12a4f-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="12a4f-441">BytesTotal</span></span> | <span data-ttu-id="12a4f-442">Całkowita liczba bajtów wysyłane lub odbierane od rozruchu</span><span class="sxs-lookup"><span data-stu-id="12a4f-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="12a4f-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="12a4f-443">PacketsTransmitted</span></span> | <span data-ttu-id="12a4f-444">Łączna liczba pakietów wysłanych od momentu rozruchu</span><span class="sxs-lookup"><span data-stu-id="12a4f-444">Total packets sent since boot</span></span>
<span data-ttu-id="12a4f-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="12a4f-445">PacketsReceived</span></span> | <span data-ttu-id="12a4f-446">Całkowita liczba pakietów otrzymanych od rozruchu</span><span class="sxs-lookup"><span data-stu-id="12a4f-446">Total packets received since boot</span></span>
<span data-ttu-id="12a4f-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="12a4f-447">TotalRxErrors</span></span> | <span data-ttu-id="12a4f-448">Liczba błędów od rozruchu</span><span class="sxs-lookup"><span data-stu-id="12a4f-448">Number of receive errors since boot</span></span>
<span data-ttu-id="12a4f-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="12a4f-449">TotalTxErrors</span></span> | <span data-ttu-id="12a4f-450">Liczba transmisji błędów od rozruchu</span><span class="sxs-lookup"><span data-stu-id="12a4f-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="12a4f-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="12a4f-451">TotalCollisions</span></span> | <span data-ttu-id="12a4f-452">Liczba kolizji zgłoszone przez porty od rozruchu</span><span class="sxs-lookup"><span data-stu-id="12a4f-452">Number of collisions reported by the network ports since boot</span></span>

 <span data-ttu-id="12a4f-453">Mimo że ta klasa jest instancji, LAD nie obsługuje przechwytywania metryki sieci zagregowane we wszystkich urządzeń sieciowych.</span><span class="sxs-lookup"><span data-stu-id="12a4f-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="12a4f-454">Aby uzyskać metryki dla określonego interfejsu, takich jak eth0, ustaw `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-454">To obtain the metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-the-filesystem-class"></a><span data-ttu-id="12a4f-455">wbudowane metryki dla klasy systemu plików</span><span class="sxs-lookup"><span data-stu-id="12a4f-455">builtin metrics for the Filesystem class</span></span>

<span data-ttu-id="12a4f-456">Klasa Filesystem metryk udostępnia informacje na temat użycia systemu plików.</span><span class="sxs-lookup"><span data-stu-id="12a4f-456">The Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="12a4f-457">Wartości bezwzględne i procent ma być zgłaszane będzie wyświetlana do zwykłego użytkownika (a nie głównego).</span><span class="sxs-lookup"><span data-stu-id="12a4f-457">Absolute and percentage values are reported as they'd be displayed to an ordinary user (not root).</span></span>

<span data-ttu-id="12a4f-458">Licznik</span><span class="sxs-lookup"><span data-stu-id="12a4f-458">counter</span></span> | <span data-ttu-id="12a4f-459">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="12a4f-459">Meaning</span></span>
------- | -------
<span data-ttu-id="12a4f-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="12a4f-460">FreeSpace</span></span> | <span data-ttu-id="12a4f-461">Dostępnego miejsca na dysku w bajtach</span><span class="sxs-lookup"><span data-stu-id="12a4f-461">Available disk space in bytes</span></span>
<span data-ttu-id="12a4f-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="12a4f-462">UsedSpace</span></span> | <span data-ttu-id="12a4f-463">Używane miejsce na dysku w bajtach</span><span class="sxs-lookup"><span data-stu-id="12a4f-463">Used disk space in bytes</span></span>
<span data-ttu-id="12a4f-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="12a4f-464">PercentFreeSpace</span></span> | <span data-ttu-id="12a4f-465">Wartość procentowa wolnego miejsca</span><span class="sxs-lookup"><span data-stu-id="12a4f-465">Percentage free space</span></span>
<span data-ttu-id="12a4f-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="12a4f-466">PercentUsedSpace</span></span> | <span data-ttu-id="12a4f-467">Procent wykorzystania miejsca</span><span class="sxs-lookup"><span data-stu-id="12a4f-467">Percentage used space</span></span>
<span data-ttu-id="12a4f-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="12a4f-468">PercentFreeInodes</span></span> | <span data-ttu-id="12a4f-469">Wartość procentowa węzłów i nieużywanych</span><span class="sxs-lookup"><span data-stu-id="12a4f-469">Percentage of unused inodes</span></span>
<span data-ttu-id="12a4f-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="12a4f-470">PercentUsedInodes</span></span> | <span data-ttu-id="12a4f-471">Wartość procentowa przydzielonych (w użyciu) węzły i sumowane przez wszystkie systemy plików</span><span class="sxs-lookup"><span data-stu-id="12a4f-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="12a4f-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-472">BytesReadPerSecond</span></span> | <span data-ttu-id="12a4f-473">Bajtów odczytanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-473">Bytes read per second</span></span>
<span data-ttu-id="12a4f-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="12a4f-475">Bajtów zapisanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-475">Bytes written per second</span></span>
<span data-ttu-id="12a4f-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-476">BytesPerSecond</span></span> | <span data-ttu-id="12a4f-477">Bajty odczytu lub zapisu na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-477">Bytes read or written per second</span></span>
<span data-ttu-id="12a4f-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-478">ReadsPerSecond</span></span> | <span data-ttu-id="12a4f-479">Operacje odczytu na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-479">Read operations per second</span></span>
<span data-ttu-id="12a4f-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-480">WritesPerSecond</span></span> | <span data-ttu-id="12a4f-481">Zapis operacji na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-481">Write operations per second</span></span>
<span data-ttu-id="12a4f-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-482">TransfersPerSecond</span></span> | <span data-ttu-id="12a4f-483">Operacje odczytu lub zapisu na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-483">Read or write operations per second</span></span>

<span data-ttu-id="12a4f-484">Wartości zagregowane we wszystkich systemach plików można uzyskać przez ustawienie `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="12a4f-485">Wartości dla określonego zainstalowany system plików, takich jak "/ mnt", można uzyskać przez ustawienie `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-the-disk-class"></a><span data-ttu-id="12a4f-486">wbudowane metryki dla klasy dysku</span><span class="sxs-lookup"><span data-stu-id="12a4f-486">builtin metrics for the Disk class</span></span>

<span data-ttu-id="12a4f-487">Klasa dysku metryk udostępnia informacje na temat użycia urządzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="12a4f-487">The Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="12a4f-488">Te statystyki mają zastosowanie do całego dysku.</span><span class="sxs-lookup"><span data-stu-id="12a4f-488">These statistics apply to the entire drive.</span></span> <span data-ttu-id="12a4f-489">Jeśli istnieje wiele systemów plików na urządzeniu, liczników dla tego urządzenia to w rzeczywistości zagregowane we wszystkich z nich.</span><span class="sxs-lookup"><span data-stu-id="12a4f-489">If there are multiple file systems on a device, the counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="12a4f-490">Licznik</span><span class="sxs-lookup"><span data-stu-id="12a4f-490">counter</span></span> | <span data-ttu-id="12a4f-491">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="12a4f-491">Meaning</span></span>
------- | -------
<span data-ttu-id="12a4f-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-492">ReadsPerSecond</span></span> | <span data-ttu-id="12a4f-493">Operacje odczytu na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-493">Read operations per second</span></span>
<span data-ttu-id="12a4f-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-494">WritesPerSecond</span></span> | <span data-ttu-id="12a4f-495">Zapis operacji na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-495">Write operations per second</span></span>
<span data-ttu-id="12a4f-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-496">TransfersPerSecond</span></span> | <span data-ttu-id="12a4f-497">Całkowita liczba operacji na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-497">Total operations per second</span></span>
<span data-ttu-id="12a4f-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-498">AverageReadTime</span></span> | <span data-ttu-id="12a4f-499">Średnia liczba sekund na operacja odczytu</span><span class="sxs-lookup"><span data-stu-id="12a4f-499">Average seconds per read operation</span></span>
<span data-ttu-id="12a4f-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-500">AverageWriteTime</span></span> | <span data-ttu-id="12a4f-501">Średnia liczba sekund na operację zapisu</span><span class="sxs-lookup"><span data-stu-id="12a4f-501">Average seconds per write operation</span></span>
<span data-ttu-id="12a4f-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="12a4f-502">AverageTransferTime</span></span> | <span data-ttu-id="12a4f-503">Średnia liczba sekund na operację</span><span class="sxs-lookup"><span data-stu-id="12a4f-503">Average seconds per operation</span></span>
<span data-ttu-id="12a4f-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="12a4f-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="12a4f-505">Średnia liczba operacji w kolejce dysku</span><span class="sxs-lookup"><span data-stu-id="12a4f-505">Average number of queued disk operations</span></span>
<span data-ttu-id="12a4f-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="12a4f-507">Liczba bajtów odczytanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-507">Number of bytes read per second</span></span>
<span data-ttu-id="12a4f-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="12a4f-509">Liczba bajtów zapisanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-509">Number of bytes written per second</span></span>
<span data-ttu-id="12a4f-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="12a4f-510">BytesPerSecond</span></span> | <span data-ttu-id="12a4f-511">Liczba bajtów odczytywanych lub zapisywanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="12a4f-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="12a4f-512">Zagregowane wartości na wszystkich dyskach można uzyskać przez ustawienie `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="12a4f-513">Aby uzyskać informacje dotyczące określonego urządzenia (na przykład/dev/sdf1), należy ustawić `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="12a4f-513">To get information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="12a4f-514">Instalowanie i konfigurowanie LAD 3.0 za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="12a4f-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="12a4f-515">Zakładając, że ustawienia chronionego znajdują się w pliku PrivateConfig.json i informacje o konfiguracji publicznego jest PublicConfig.json, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="12a4f-515">Assuming your protected settings are in the file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="12a4f-516">Polecenie przyjęto założenie, że używany jest tryb zarządzania zasobami Azure (arm) z wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-516">The command assumes you are using the Azure Resource Management mode (arm) of the Azure CLI.</span></span> <span data-ttu-id="12a4f-517">Aby skonfigurować LAD wdrożenia klasycznego modelu (ASM), maszynach wirtualnych, Przełącz do trybu "asm" (`azure config mode asm`) i pominąć nazwę grupy zasobów w poleceniu.</span><span class="sxs-lookup"><span data-stu-id="12a4f-517">To configure LAD for classic deployment model (ASM) VMs, switch to "asm" mode (`azure config mode asm`) and omit the resource group name in the command.</span></span> <span data-ttu-id="12a4f-518">Aby uzyskać więcej informacji, zobacz [dokumentacji interfejsu wiersza polecenia i platform](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="12a4f-518">For more information, see the [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="12a4f-519">Przykład LAD 3.0 konfiguracji</span><span class="sxs-lookup"><span data-stu-id="12a4f-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="12a4f-520">Oparte na poprzednim definicje, Oto przykładowa konfiguracja rozszerzenia LAD 3.0 z wyjaśnień.</span><span class="sxs-lookup"><span data-stu-id="12a4f-520">Based on the preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="12a4f-521">Aby zastosować w tym przykładzie do sprawę, należy używać własne nazwy konta magazynu, token sygnatury dostępu Współdzielonego konta i tokeny EventHubs sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="12a4f-521">To apply this sample to your case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="12a4f-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="12a4f-522">PrivateConfig.json</span></span>

<span data-ttu-id="12a4f-523">Skonfiguruj te ustawienia prywatnych:</span><span class="sxs-lookup"><span data-stu-id="12a4f-523">These private settings configure:</span></span>

* <span data-ttu-id="12a4f-524">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="12a4f-524">a storage account</span></span>
* <span data-ttu-id="12a4f-525">zgodnego tokenu sygnatury dostępu Współdzielonego konta</span><span class="sxs-lookup"><span data-stu-id="12a4f-525">a matching account SAS token</span></span>
* <span data-ttu-id="12a4f-526">wychwytywanie kilka (JsonBlob lub EventHubs z tokenami SAS)</span><span class="sxs-lookup"><span data-stu-id="12a4f-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="12a4f-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="12a4f-527">PublicConfig.json</span></span>

<span data-ttu-id="12a4f-528">Te ustawienia publicznego spowodować LAD do:</span><span class="sxs-lookup"><span data-stu-id="12a4f-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="12a4f-529">Przekaż metryki procent procesora czasu i używać miejsca na dysku do `WADMetrics*` tabeli</span><span class="sxs-lookup"><span data-stu-id="12a4f-529">Upload percent-processor-time and used-disk-space metrics to the `WADMetrics*` table</span></span>
* <span data-ttu-id="12a4f-530">Przekazywanie komunikatów z syslog zakładzie "użytkownika" i ważność "informacje" do `LinuxSyslog*` tabeli</span><span class="sxs-lookup"><span data-stu-id="12a4f-530">Upload messages from syslog facility "user" and severity "info" to the `LinuxSyslog*` table</span></span>
* <span data-ttu-id="12a4f-531">Przekaż nieprzetworzone wyniki zapytania OMI (PercentProcessorTime i PercentIdleTime) do nazwanego `LinuxCPU` tabeli</span><span class="sxs-lookup"><span data-stu-id="12a4f-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) to the named `LinuxCPU` table</span></span>
* <span data-ttu-id="12a4f-532">Przekaż dołączany wiersze w pliku `/var/log/myladtestlog` do `MyLadTestLog` tabeli</span><span class="sxs-lookup"><span data-stu-id="12a4f-532">Upload appended lines in file `/var/log/myladtestlog` to the `MyLadTestLog` table</span></span>

<span data-ttu-id="12a4f-533">W każdym przypadku również przekazywania danych do:</span><span class="sxs-lookup"><span data-stu-id="12a4f-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="12a4f-534">Magazyn obiektów Blob Azure (nazwa kontenera jest zdefiniowany w ujściu JsonBlob)</span><span class="sxs-lookup"><span data-stu-id="12a4f-534">Azure Blob storage (container name is as defined in the JsonBlob sink)</span></span>
* <span data-ttu-id="12a4f-535">Punkt końcowy EventHubs (jak określono w ujściu EventHubs)</span><span class="sxs-lookup"><span data-stu-id="12a4f-535">EventHubs endpoint (as specified in the EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="12a4f-536">`resourceId` w konfiguracji muszą być zgodne czy maszyny Wirtualnej lub skalowania maszyny wirtualnej ustawić.</span><span class="sxs-lookup"><span data-stu-id="12a4f-536">The `resourceId` in the configuration must match that of the VM or the virtual machine scale set.</span></span>

* <span data-ttu-id="12a4f-537">Metryki platformy Azure, wykresów i alerty wie resourceId pracy maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12a4f-537">Azure platform metrics charting and alerting knows the resourceId of the VM you're working on.</span></span> <span data-ttu-id="12a4f-538">Oczekuje się znaleźć dane dla maszyny Wirtualnej przy użyciu element resourceId klucz wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="12a4f-538">It expects to find the data for your VM using the resourceId the lookup key.</span></span>
* <span data-ttu-id="12a4f-539">Jeśli używasz platformy Azure skalowania automatycznego resourceId w konfiguracji automatycznego skalowania musi być zgodna z resourceId używane przez LAD.</span><span class="sxs-lookup"><span data-stu-id="12a4f-539">If you use Azure autoscale, the resourceId in the autoscale configuration must match the resourceId used by LAD.</span></span>
* <span data-ttu-id="12a4f-540">Element resourceId jest wbudowana w nazwach JsonBlobs napisane przez LAD.</span><span class="sxs-lookup"><span data-stu-id="12a4f-540">The resourceId is built into the names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="12a4f-541">Wyświetlanie danych</span><span class="sxs-lookup"><span data-stu-id="12a4f-541">View your data</span></span>

<span data-ttu-id="12a4f-542">Użyj portalu Azure, aby wyświetlić dane wydajności lub Ustaw alerty:</span><span class="sxs-lookup"><span data-stu-id="12a4f-542">Use the Azure portal to view performance data or set alerts:</span></span>

![Obraz](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="12a4f-544">`performanceCounters` Danych zawsze są przechowywane w tabeli magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-544">The `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="12a4f-545">Interfejsy API usługi Azure Storage są dostępne dla wielu języków i platform.</span><span class="sxs-lookup"><span data-stu-id="12a4f-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="12a4f-546">Dane wysłane do ujścia JsonBlob są przechowywane w obiektach blob na koncie magazynu o nazwie w [chronionych ustawień](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="12a4f-546">Data sent to JsonBlob sinks is stored in blobs in the storage account named in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="12a4f-547">Będzie można korzystać z danych obiektu blob, przy użyciu dowolnego interfejsów API magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="12a4f-547">You can consume the blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="12a4f-548">Ponadto można tych narzędzi interfejsu użytkownika dostępu do danych w usłudze Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="12a4f-548">In addition, you can use these UI tools to access the data in Azure Storage:</span></span>

* <span data-ttu-id="12a4f-549">Eksplorator serwera programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12a4f-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="12a4f-550">[Eksplorator usługi Storage platformy Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Eksploratora usługi Azure Storage").</span><span class="sxs-lookup"><span data-stu-id="12a4f-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="12a4f-551">Tej migawki sesji Eksploratora usługi Microsoft Azure Storage jest wyświetlana wygenerowanego tabele usługi Azure Storage i kontenery z rozszerzeniem LAD 3.0 poprawnie skonfigurowana na testowej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="12a4f-551">This snapshot of a Microsoft Azure Storage Explorer session shows the generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="12a4f-552">Obraz nie jest zgodna z [Przykładowa konfiguracja LAD 3.0](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="12a4f-552">The image doesn't match exactly with the [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![Obraz](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="12a4f-554">Zobacz odpowiedniego [dokumentacji EventHubs](../../event-hubs/event-hubs-what-is-event-hubs.md) aby nauczyć się korzystać komunikaty opublikowane do punktu końcowego EventHubs.</span><span class="sxs-lookup"><span data-stu-id="12a4f-554">See the relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) to learn how to consume messages published to an EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12a4f-555">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="12a4f-555">Next steps</span></span>

* <span data-ttu-id="12a4f-556">Tworzenie metryki alertów w [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) dla metryki zbierania.</span><span class="sxs-lookup"><span data-stu-id="12a4f-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for the metrics you collect.</span></span>
* <span data-ttu-id="12a4f-557">Utwórz [monitorowania wykresy](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) dla Twojego metryki.</span><span class="sxs-lookup"><span data-stu-id="12a4f-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="12a4f-558">Dowiedz się, jak [utworzyć zestaw skali maszyny wirtualnej](/azure/virtual-machines/linux/tutorial-create-vmss) przy użyciu programu metryk, aby kontrolować skalowanie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="12a4f-558">Learn how to [create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics to control autoscaling.</span></span>
