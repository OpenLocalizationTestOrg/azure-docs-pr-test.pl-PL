---
title: "aaaAzure obliczeniowe — rozszerzenie diagnostyczne systemu Linux | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure hello metryki toocollect rozszerzenia diagnostycznych Linux Azure (LAD) i rejestrowanie zdarzeń z maszyn wirtualnych systemu Linux działających na platformie Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="641b4-103">Użyj rozszerzenia diagnostycznych Linux toomonitor metryki i dzienniki</span><span class="sxs-lookup"><span data-stu-id="641b4-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="641b4-104">W tym dokumencie opisano w wersji 3.0 oraz nowszych z hello rozszerzenia diagnostyczne systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="641b4-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="641b4-105">Informacje o wersji 2.3 i starsze, zobacz [tego dokumentu](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="641b4-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="641b4-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="641b4-106">Introduction</span></span>

<span data-ttu-id="641b4-107">Hello rozszerzenia diagnostycznych Linux pomaga użytkownika monitorowanie hello kondycja maszyny wirtualnej systemu Linux uruchomiony w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="641b4-108">Ma hello następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="641b4-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="641b4-109">Zbiera metryki wydajności systemu z hello maszyny Wirtualnej i zapisuje je w określonej tabeli w ramach konta magazynu wyznaczonego.</span><span class="sxs-lookup"><span data-stu-id="641b4-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="641b4-110">Pobiera zdarzenia dziennika z syslog i przechowuje je w określonej tabeli w Witaj wyznaczone konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="641b4-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="641b4-111">Umożliwia użytkownikom toocustomize hello danych metryki, które są zbierane i przekazać.</span><span class="sxs-lookup"><span data-stu-id="641b4-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="641b4-112">Umożliwia użytkownikom toocustomize hello syslog urządzeń i poziomy ważności zdarzeń, które są zbierane i przekazać.</span><span class="sxs-lookup"><span data-stu-id="641b4-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="641b4-113">Umożliwia użytkownikom tooupload określony dziennik pliki tooa magazynu wyznaczonego tabeli.</span><span class="sxs-lookup"><span data-stu-id="641b4-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="641b4-114">Obsługuje wysyłanie metryki i dziennik zdarzeń tooarbitrary EventHub punktów końcowych i formacie JSON obiekty BLOB w Witaj wyznaczone konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="641b4-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="641b4-115">To rozszerzenie współpracuje z obu modeli wdrażania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="641b4-116">Instalowanie hello rozszerzenia w maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="641b4-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="641b4-117">To rozszerzenie można włączyć za pomocą poleceń cmdlet programu Azure PowerShell hello skryptów wiersza polecenia platformy Azure i szablony wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="641b4-118">Aby uzyskać więcej informacji, zobacz [funkcji rozszerzenia](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="641b4-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="641b4-119">Witaj portalu Azure nie może być używane tooenable ani skonfigurować LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="641b4-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="641b4-120">Zamiast tego instaluje i konfiguruje wersji 2.3.</span><span class="sxs-lookup"><span data-stu-id="641b4-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="641b4-121">Wykresy portalu Azure i alerty pracować z danymi obie wersje hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="641b4-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="641b4-122">Te instrukcje instalacji i [do pobrania Przykładowa konfiguracja](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) LAD 3.0 można skonfigurować:</span><span class="sxs-lookup"><span data-stu-id="641b4-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="641b4-123">Przechwytywanie i magazynu hello same metryki dostarczonych przez LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="641b4-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="641b4-124">Przechwyć zbiór przydatne metryki systemu plików, nowe tooLAD 3.0;</span><span class="sxs-lookup"><span data-stu-id="641b4-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="641b4-125">Przechwyć hello domyślnej syslog kolekcji włączane przez LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="641b4-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="641b4-126">Włącz hello Azure portalu obsługi wykresów i alerty na metryki maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="641b4-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="641b4-127">do pobrania konfiguracji Hello jest tylko przykładowe; Zmodyfikuj go toosuit własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="641b4-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="641b4-128">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="641b4-128">Prerequisites</span></span>

* <span data-ttu-id="641b4-129">**Agenta systemu Linux platformy Azure w wersji 2.2.0 lub nowszym**.</span><span class="sxs-lookup"><span data-stu-id="641b4-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="641b4-130">Większość obrazów Galeria Linux maszyny Wirtualnej Azure zawierają wersję 2.2.7 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="641b4-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="641b4-131">Uruchom `/usr/sbin/waagent -version` tooconfirm hello wersji zainstalowanej na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="641b4-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="641b4-132">Jeśli hello maszyna wirtualna jest uruchomiona starszą wersję agenta gościa hello, wykonaj [tych instrukcji](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate go.</span><span class="sxs-lookup"><span data-stu-id="641b4-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="641b4-133">**Interfejs wiersza polecenia platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="641b4-133">**Azure CLI**.</span></span> <span data-ttu-id="641b4-134">[Konfigurowanie hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) środowiska na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="641b4-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="641b4-135">Witaj wget polecenia, jeśli nie masz jeszcze go: Uruchom `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="641b4-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="641b4-136">Istniejącą subskrypcję platformy Azure i istniejącego magazynu konta w niej toostore hello danych.</span><span class="sxs-lookup"><span data-stu-id="641b4-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="641b4-137">Przykładowe instalacji</span><span class="sxs-lookup"><span data-stu-id="641b4-137">Sample installation</span></span>

<span data-ttu-id="641b4-138">Wprowadź poprawne parametry hello na powitania pierwsze trzy wiersze, a następnie wykonaj ten skrypt jako katalogu głównego:</span><span class="sxs-lookup"><span data-stu-id="641b4-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="641b4-139">adres URL Hello hello Przykładowa konfiguracja i jego zawartość są toochange podmiotu.</span><span class="sxs-lookup"><span data-stu-id="641b4-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="641b4-140">Pobierz kopię pliku JSON hello ustawienia portalu i dostosować go do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="641b4-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="641b4-141">Wszystkie szablony lub automatyzacji, który można skonstruować należy używać własną kopię zamiast pobierania zawsze tego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="641b4-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="641b4-142">Aktualizowanie ustawień rozszerzenia hello</span><span class="sxs-lookup"><span data-stu-id="641b4-142">Updating hello extension settings</span></span>

<span data-ttu-id="641b4-143">Po zmianie ustawienia publiczne lub chronione, na których je wdrożyć toohello maszyny Wirtualnej, uruchamiając hello tego samego polecenia.</span><span class="sxs-lookup"><span data-stu-id="641b4-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="641b4-144">Zmiana niczego w ustawieniach hello hello zaktualizowane ustawienia są wysyłane toohello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="641b4-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="641b4-145">LAD ponowne załadowanie konfiguracji hello i uruchamia się ponownie.</span><span class="sxs-lookup"><span data-stu-id="641b4-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="641b4-146">Migracja z poprzednich wersji rozszerzenia hello</span><span class="sxs-lookup"><span data-stu-id="641b4-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="641b4-147">Najnowsza wersja rozszerzenia hello Hello jest **3.0**.</span><span class="sxs-lookup"><span data-stu-id="641b4-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="641b4-148">**Wszystkie starsze wersje (2.x) są przestarzałe i mogą być publikowane na wcześniejsze niż 31 lipca 2018**.</span><span class="sxs-lookup"><span data-stu-id="641b4-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="641b4-149">To rozszerzenie wprowadzono istotne zmiany toohello konfiguracji hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="641b4-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="641b4-150">Taka zmiana nastąpiła zabezpieczeń hello tooimprove rozszerzenia hello; w związku z tym zapewnienia zgodności z 2.x nie można wykonać konserwacji.</span><span class="sxs-lookup"><span data-stu-id="641b4-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="641b4-151">Ponadto hello wydawcy rozszerzenia dla tego rozszerzenia jest inny niż hello wydawcy dla wersji 2.x hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="641b4-152">toomigrate z 2.x toothis nowa wersja rozszerzenia hello, należy odinstalować rozszerzenia starego hello (w obszarze hello starej nazwy wydawcy), a następnie zainstaluj w wersji 3 hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="641b4-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="641b4-153">Zalecenia:</span><span class="sxs-lookup"><span data-stu-id="641b4-153">Recommendations:</span></span>

* <span data-ttu-id="641b4-154">Uaktualnianie wersji pomocniczej automatyczne włączone, należy zainstalować rozszerzenie hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="641b4-155">W klasycznym modelu wdrażania maszyn wirtualnych należy określić "3.*" jako wersja hello instalowania rozszerzenia hello za pośrednictwem interfejsu wiersza polecenia XPLAT platformy Azure lub programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="641b4-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="641b4-156">We wdrożeniu usługi Azure Resource Manager modelu maszyn wirtualnych, obejmują ""autoUpgradeMinorVersion": true" w szablonie wdrożenia maszyny Wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="641b4-157">Użyj nowego/innego konta magazynu dla LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="641b4-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="641b4-158">Istnieje kilka małych niezgodności między LAD 2.3 i LAD 3.0 powodujących, że udostępnianie powodującymi konta:</span><span class="sxs-lookup"><span data-stu-id="641b4-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="641b4-159">LAD 3.0 przechowuje zdarzenia dziennika systemowego w tabeli z inną nazwą.</span><span class="sxs-lookup"><span data-stu-id="641b4-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="641b4-160">Witaj counterSpecifier ciągów dla `builtin` metryki różnią się w LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="641b4-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="641b4-161">Ustawienia chronionego</span><span class="sxs-lookup"><span data-stu-id="641b4-161">Protected settings</span></span>

<span data-ttu-id="641b4-162">Ten zestaw informacji o konfiguracji zawiera poufne informacje, które powinny być chronione w widoku publicznych, na przykład poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="641b4-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="641b4-163">Te ustawienia są przesyłane tooand przechowywane przez rozszerzenie hello w postaci zaszyfrowanej.</span><span class="sxs-lookup"><span data-stu-id="641b4-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="641b4-164">Nazwa</span><span class="sxs-lookup"><span data-stu-id="641b4-164">Name</span></span> | <span data-ttu-id="641b4-165">Wartość</span><span class="sxs-lookup"><span data-stu-id="641b4-165">Value</span></span>
---- | -----
<span data-ttu-id="641b4-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="641b4-166">storageAccountName</span></span> | <span data-ttu-id="641b4-167">Nazwa Hello hello konta magazynu, w którym dane są zapisywane przez rozszerzenie hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="641b4-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="641b4-168">storageAccountEndPoint</span></span> | <span data-ttu-id="641b4-169">identyfikowanie hello chmury, w których hello konto magazynu istnieje punkt końcowy hello (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="641b4-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="641b4-170">Jeśli to ustawienie jest nieobecne, LAD domyślnie toohello chmurze publicznej Azure `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="641b4-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="641b4-171">toouse konto magazynu platformy Azure w Niemczech, Azure dla instytucji rządowych lub chińskiej wersji platformy Azure, w związku z tym Ustaw tę wartość.</span><span class="sxs-lookup"><span data-stu-id="641b4-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="641b4-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="641b4-172">storageAccountSasToken</span></span> | <span data-ttu-id="641b4-173">[Tokenu sygnatury dostępu Współdzielonego konta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) usług obiektów Blob i tabeli (`ss='bt'`), odpowiednich toocontainers i obiektów (`srt='co'`), która przyznaje dodać, tworzenie listy, aktualizacji i uprawnienia do zapisu (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="641b4-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="641b4-174">Czy *nie* obejmują hello wiodące znak zapytania (?).</span><span class="sxs-lookup"><span data-stu-id="641b4-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="641b4-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="641b4-175">mdsdHttpProxy</span></span> | <span data-ttu-id="641b4-176">(opcjonalnie) Informacje potrzebne serwera proxy HTTP tooenable toohello tooconnect rozszerzenia hello określone konto magazynu i punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="641b4-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="641b4-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="641b4-177">sinksConfig</span></span> | <span data-ttu-id="641b4-178">(opcjonalnie) Szczegółowe informacje o alternatywnych miejsc docelowych toowhich metryki i zdarzenia mogą być dostarczane.</span><span class="sxs-lookup"><span data-stu-id="641b4-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="641b4-179">Witaj szczegółowe informacje dotyczące każdego ujścia danych obsługiwane przez rozszerzenie hello zostały omówione w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="641b4-180">Można łatwo utworzyć hello wymagane tokenu sygnatury dostępu Współdzielonego za pośrednictwem portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="641b4-181">Wybierz toowhich konta magazynu ogólnego przeznaczenia hello ma hello toowrite rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="641b4-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="641b4-182">Wybierz opcję "Udostępniania sygnatury dostępu" z menu po lewej stronie powitania części ustawień hello</span><span class="sxs-lookup"><span data-stu-id="641b4-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="641b4-183">Wprowadź odpowiednie części hello, jak opisano wcześniej</span><span class="sxs-lookup"><span data-stu-id="641b4-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="641b4-184">Kliknij przycisk "Generowanie sygnatury dostępu Współdzielonego" hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-184">Click hello "Generate SAS" button.</span></span>

![Obraz](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="641b4-186">Kopiuj hello wygenerowany SAS do pola storageAccountSasToken hello; Usuń znaku zapytania wiodące hello ("?").</span><span class="sxs-lookup"><span data-stu-id="641b4-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="641b4-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="641b4-187">sinksConfig</span></span>

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

<span data-ttu-id="641b4-188">Ta sekcja opcjonalna definiuje dodatkowe rozszerzenia hello toowhich wysyła informacje hello zebrane miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="641b4-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="641b4-189">Tablica "sink" Hello zawiera obiekt dla każdego obiektu sink dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="641b4-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="641b4-190">Określa atrybut "typ" hello innych atrybutów w obiekcie hello Hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="641b4-191">Element</span><span class="sxs-lookup"><span data-stu-id="641b4-191">Element</span></span> | <span data-ttu-id="641b4-192">Wartość</span><span class="sxs-lookup"><span data-stu-id="641b4-192">Value</span></span>
------- | -----
<span data-ttu-id="641b4-193">name</span><span class="sxs-lookup"><span data-stu-id="641b4-193">name</span></span> | <span data-ttu-id="641b4-194">Ciąg używany toorefer toothis ujścia innym miejscu w konfiguracji rozszerzenia hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="641b4-195">type</span><span class="sxs-lookup"><span data-stu-id="641b4-195">type</span></span> | <span data-ttu-id="641b4-196">Typ Hello definiowanego obiektu sink.</span><span class="sxs-lookup"><span data-stu-id="641b4-196">hello type of sink being defined.</span></span> <span data-ttu-id="641b4-197">Określa hello inne wartości (jeśli istnieją) w wystąpień tego typu.</span><span class="sxs-lookup"><span data-stu-id="641b4-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="641b4-198">Wersja 3.0 hello rozszerzenia diagnostycznych Linux obsługuje dwa typy zbiornika: EventHub i JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="641b4-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="641b4-199">obiekt sink EventHub Hello</span><span class="sxs-lookup"><span data-stu-id="641b4-199">hello EventHub sink</span></span>

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

<span data-ttu-id="641b4-200">wpis "sasURL" Hello zawiera hello, który powinien zostać opublikowany, pełny adres URL, w tym tokenu sygnatury dostępu Współdzielonego dla hello danych toowhich Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="641b4-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="641b4-201">LAD wymaga sygnatury dostępu Współdzielonego nazewnictwa zasadę, która umożliwia hello wysyłania oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="641b4-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="641b4-202">Przykład:</span><span class="sxs-lookup"><span data-stu-id="641b4-202">An example:</span></span>

* <span data-ttu-id="641b4-203">Tworzenie przestrzeni nazw usługi Event Hubs, o nazwie`contosohub`</span><span class="sxs-lookup"><span data-stu-id="641b4-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="641b4-204">Tworzenie Centrum zdarzeń w przestrzeni nazw hello o nazwie`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="641b4-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="641b4-205">Tworzenie zasad dostępu współużytkowanego na powitania Centrum zdarzeń o nazwie `writer` czy umożliwia hello wysyłania oświadczeń</span><span class="sxs-lookup"><span data-stu-id="641b4-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="641b4-206">Jeśli utworzono sygnatury dostępu Współdzielonego dobra do północy czasu UTC 1 stycznia 2018 hello sasURL wartość może być:</span><span class="sxs-lookup"><span data-stu-id="641b4-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="641b4-207">Aby uzyskać więcej informacji na temat generowania tokeny sygnatury dostępu Współdzielonego usługi Event hubs, zobacz [tej strony sieci web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="641b4-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="641b4-208">obiekt sink JsonBlob Hello</span><span class="sxs-lookup"><span data-stu-id="641b4-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="641b4-209">Dane skierowane tooa JsonBlob ujście są przechowywane w obiekty BLOB w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="641b4-210">Każde wystąpienie LAD tworzy obiektu blob co godzinę dla każdej nazwy obiektu sink.</span><span class="sxs-lookup"><span data-stu-id="641b4-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="641b4-211">Każdy obiekt blob jest zawsze zawiera nieprawidłową składnię tablicy JSON obiektu.</span><span class="sxs-lookup"><span data-stu-id="641b4-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="641b4-212">Nowe wpisy są automatycznie dodawane toohello tablicy.</span><span class="sxs-lookup"><span data-stu-id="641b4-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="641b4-213">Obiekty BLOB są przechowywane w kontenerze z hello takie same nazwy jako hello ujścia.</span><span class="sxs-lookup"><span data-stu-id="641b4-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="641b4-214">Witaj zasady usługi Azure storage dla nazwy kontenera obiektów blob zastosować toohello nazwy wychwytywanie JsonBlob: od 3 do 63 małe znaki alfanumeryczne ASCII lub łączniki.</span><span class="sxs-lookup"><span data-stu-id="641b4-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="641b4-215">Ustawienia publicznego</span><span class="sxs-lookup"><span data-stu-id="641b4-215">Public settings</span></span>

<span data-ttu-id="641b4-216">Ta struktura zawiera bloki różnych ustawień kontrolujących hello informacje zebrane przez rozszerzenie hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="641b4-217">Każde ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="641b4-217">Each setting is optional.</span></span> <span data-ttu-id="641b4-218">Jeśli określisz `ladCfg`, należy także określić `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="641b4-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="641b4-219">Element</span><span class="sxs-lookup"><span data-stu-id="641b4-219">Element</span></span> | <span data-ttu-id="641b4-220">Wartość</span><span class="sxs-lookup"><span data-stu-id="641b4-220">Value</span></span>
------- | -----
<span data-ttu-id="641b4-221">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="641b4-221">StorageAccount</span></span> | <span data-ttu-id="641b4-222">Nazwa Hello hello konta magazynu, w którym dane są zapisywane przez rozszerzenie hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="641b4-223">Muszą być takie same nazwy, jak określono w hello hello [chronionych ustawień](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="641b4-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="641b4-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="641b4-224">mdsdHttpProxy</span></span> | <span data-ttu-id="641b4-225">(opcjonalnie) Sam jak hello [chronionych ustawień](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="641b4-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="641b4-226">wartość publicznego Hello jest zastępowany przez wartość prywatnego hello, jeśli ustawiona.</span><span class="sxs-lookup"><span data-stu-id="641b4-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="641b4-227">Umieść ustawienia serwera proxy, które zawierają klucz tajny, takie jak hasła, w hello [chronionych ustawień](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="641b4-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="641b4-228">pozostałe elementy Hello są szczegółowo opisane w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="641b4-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="641b4-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="641b4-229">ladCfg</span></span>

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

<span data-ttu-id="641b4-230">Wychwytywanie tego opcjonalne struktury formanty hello zbierania metryk i dziennikach toohello dostarczania danych do usługi i tooother metryk usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="641b4-231">Należy określić `performanceCounters` lub `syslogEvents` lub oba.</span><span class="sxs-lookup"><span data-stu-id="641b4-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="641b4-232">Należy określić hello `metrics` struktury.</span><span class="sxs-lookup"><span data-stu-id="641b4-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="641b4-233">Element</span><span class="sxs-lookup"><span data-stu-id="641b4-233">Element</span></span> | <span data-ttu-id="641b4-234">Wartość</span><span class="sxs-lookup"><span data-stu-id="641b4-234">Value</span></span>
------- | -----
<span data-ttu-id="641b4-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="641b4-235">eventVolume</span></span> | <span data-ttu-id="641b4-236">(opcjonalnie) Formanty hello liczby partycji w tabeli magazynu hello utworzone.</span><span class="sxs-lookup"><span data-stu-id="641b4-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="641b4-237">Musi mieć jedną z `"Large"`, `"Medium"`, lub `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="641b4-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="641b4-238">Jeśli nie zostanie określony, wartością domyślną hello jest `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="641b4-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="641b4-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="641b4-239">sampleRateInSeconds</span></span> | <span data-ttu-id="641b4-240">(opcjonalnie) hello domyślny interwał między kolekcję pierwotnych metryki (unaggregated).</span><span class="sxs-lookup"><span data-stu-id="641b4-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="641b4-241">częstotliwość próbkowania Hello najmniejsza obsługiwana jest 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="641b4-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="641b4-242">Jeśli nie zostanie określony, wartością domyślną hello jest `15`.</span><span class="sxs-lookup"><span data-stu-id="641b4-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="641b4-243">metrics</span><span class="sxs-lookup"><span data-stu-id="641b4-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="641b4-244">Element</span><span class="sxs-lookup"><span data-stu-id="641b4-244">Element</span></span> | <span data-ttu-id="641b4-245">Wartość</span><span class="sxs-lookup"><span data-stu-id="641b4-245">Value</span></span>
------- | -----
<span data-ttu-id="641b4-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="641b4-246">resourceId</span></span> | <span data-ttu-id="641b4-247">Identyfikator zasobu usługi Azure Resource Manager Hello hello maszyny Wirtualnej lub hello skalowania maszyny wirtualnej ustawić hello toowhich, do której należy maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="641b4-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="641b4-248">To ustawienie musi być także określona, jeśli wszystkie zbiornika JsonBlob jest używane w konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="641b4-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="641b4-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="641b4-250">częstotliwość Hello są agregacji metryki toobe obliczana i przekazywane tooAzure metryki, wyrażona jako czas jest 8601.</span><span class="sxs-lookup"><span data-stu-id="641b4-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="641b4-251">okres transfer z najmniejszą Hello jest 60 sekund, czyli PT1M.</span><span class="sxs-lookup"><span data-stu-id="641b4-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="641b4-252">Należy określić co najmniej jeden scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="641b4-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="641b4-253">Przykłady powitalne metryk określone w sekcji liczniki wydajności hello są gromadzone co 15 sekund lub częstotliwość próbkowania hello jawnie zdefiniowany dla licznika hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="641b4-254">Jeśli występuje wiele częstotliwości scheduledTransferPeriod (co w przykładzie hello), każdy agregacji jest obliczana niezależnie.</span><span class="sxs-lookup"><span data-stu-id="641b4-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="641b4-255">liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="641b4-255">performanceCounters</span></span>

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

<span data-ttu-id="641b4-256">Ta sekcja opcjonalna steruje hello zbiór metryki.</span><span class="sxs-lookup"><span data-stu-id="641b4-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="641b4-257">Przykłady pierwotnych są agregowane dla wszystkich [scheduledTransferPeriod](#metrics) tooproduce te wartości:</span><span class="sxs-lookup"><span data-stu-id="641b4-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="641b4-258">Średnia</span><span class="sxs-lookup"><span data-stu-id="641b4-258">mean</span></span>
* <span data-ttu-id="641b4-259">Minimalna</span><span class="sxs-lookup"><span data-stu-id="641b4-259">minimum</span></span>
* <span data-ttu-id="641b4-260">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="641b4-260">maximum</span></span>
* <span data-ttu-id="641b4-261">wartości zbierane przez ostatnie</span><span class="sxs-lookup"><span data-stu-id="641b4-261">last-collected value</span></span>
* <span data-ttu-id="641b4-262">Liczba próbek pierwotnych używane toocompute hello agregacji</span><span class="sxs-lookup"><span data-stu-id="641b4-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="641b4-263">Element</span><span class="sxs-lookup"><span data-stu-id="641b4-263">Element</span></span> | <span data-ttu-id="641b4-264">Wartość</span><span class="sxs-lookup"><span data-stu-id="641b4-264">Value</span></span>
------- | -----
<span data-ttu-id="641b4-265">sink — obiekty</span><span class="sxs-lookup"><span data-stu-id="641b4-265">sinks</span></span> | <span data-ttu-id="641b4-266">(opcjonalnie) Rozdzielana przecinkami lista nazw wychwytywanie toowhich wysyłanych LAD w zagregowanych wynikach metryki.</span><span class="sxs-lookup"><span data-stu-id="641b4-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="641b4-267">Wszystkie metryki zagregowane są zbiornika tooeach opublikowane na liście.</span><span class="sxs-lookup"><span data-stu-id="641b4-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="641b4-268">Zobacz [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="641b4-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="641b4-269">Przykład: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="641b4-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="641b4-270">type</span><span class="sxs-lookup"><span data-stu-id="641b4-270">type</span></span> | <span data-ttu-id="641b4-271">Określa dostawcę rzeczywiste hello hello metryki.</span><span class="sxs-lookup"><span data-stu-id="641b4-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="641b4-272">Klasy</span><span class="sxs-lookup"><span data-stu-id="641b4-272">class</span></span> | <span data-ttu-id="641b4-273">Wraz z "licznika" identyfikuje hello określonej metryki w obszarze nazw hello dostawcy.</span><span class="sxs-lookup"><span data-stu-id="641b4-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="641b4-274">Licznik</span><span class="sxs-lookup"><span data-stu-id="641b4-274">counter</span></span> | <span data-ttu-id="641b4-275">Wraz z "class" identyfikuje hello określonej metryki w obszarze nazw hello dostawcy.</span><span class="sxs-lookup"><span data-stu-id="641b4-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="641b4-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="641b4-276">counterSpecifier</span></span> | <span data-ttu-id="641b4-277">Identyfikuje hello określonej metryki w hello Azure metryki w obszarze nazw.</span><span class="sxs-lookup"><span data-stu-id="641b4-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="641b4-278">Warunek</span><span class="sxs-lookup"><span data-stu-id="641b4-278">condition</span></span> | <span data-ttu-id="641b4-279">(opcjonalnie) Stosuje określone wystąpienie hello obiektu toowhich hello metryki wybiera lub wybiera hello agregacji we wszystkich wystąpieniach tego obiektu.</span><span class="sxs-lookup"><span data-stu-id="641b4-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="641b4-280">Aby uzyskać więcej informacji, zobacz hello [ `builtin` definicji metryk](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="641b4-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="641b4-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="641b4-281">sampleRate</span></span> | <span data-ttu-id="641b4-282">JEST interwałem 8601, która ustawia współczynnik hello pobierane pierwotnych próbek ta metryka.</span><span class="sxs-lookup"><span data-stu-id="641b4-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="641b4-283">Jeśli nie jest ustawiona, hello kolekcji interwał jest ustawiany przez wartość hello [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="641b4-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="641b4-284">częstotliwość próbkowania obsługiwanych z najkrótszego Hello wynosi 15 sekund (PT15S).</span><span class="sxs-lookup"><span data-stu-id="641b4-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="641b4-285">jednostki</span><span class="sxs-lookup"><span data-stu-id="641b4-285">unit</span></span> | <span data-ttu-id="641b4-286">Powinien być jednym z tych ciągów: "Count", "B", "Seconds", "%", "CountPerSecond", "BytesPerSecond", "Milisekund".</span><span class="sxs-lookup"><span data-stu-id="641b4-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="641b4-287">Definiuje jednostkę hello hello metryki.</span><span class="sxs-lookup"><span data-stu-id="641b4-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="641b4-288">Konsumenci danych zebranych hello oczekiwać hello zbierane dane wartości toomatch tej jednostki.</span><span class="sxs-lookup"><span data-stu-id="641b4-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="641b4-289">LAD są ignorowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="641b4-289">LAD ignores this field.</span></span>
<span data-ttu-id="641b4-290">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="641b4-290">displayName</span></span> | <span data-ttu-id="641b4-291">toobe etykiety (w języku hello określonego przez skojarzony ustawień regionalnych hello ustawienie) Hello dołączony toothis danych metryk usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="641b4-292">LAD są ignorowane w tym polu.</span><span class="sxs-lookup"><span data-stu-id="641b4-292">LAD ignores this field.</span></span>

<span data-ttu-id="641b4-293">Hello counterSpecifier jest umownym identyfikatorem.</span><span class="sxs-lookup"><span data-stu-id="641b4-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="641b4-294">Konsumenci metryk, takich jak hello wykresów portalu Azure i alerty funkcji, użyj counterSpecifier jako hello "klucza", który identyfikuje metrykę lub wystąpienia metryki.</span><span class="sxs-lookup"><span data-stu-id="641b4-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="641b4-295">Aby uzyskać `builtin` metryki, zalecane jest użycie counterSpecifier wartości, które zaczynają się od `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="641b4-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="641b4-296">Jeśli są zbierane konkretne wystąpienie metrykę, zaleca się Dołącz identyfikator hello hello wystąpienia toohello counterSpecifier wartości.</span><span class="sxs-lookup"><span data-stu-id="641b4-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="641b4-297">Kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="641b4-297">Some examples:</span></span>

* <span data-ttu-id="641b4-298">`/builtin/Processor/PercentIdleTime`-Bezczynności uśredniona wszystkich rdzeni</span><span class="sxs-lookup"><span data-stu-id="641b4-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="641b4-299">`/builtin/Disk/FreeSpace(/mnt)`-Wolnego miejsca dla systemu plików z katalogu/mnt hello</span><span class="sxs-lookup"><span data-stu-id="641b4-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="641b4-300">`/builtin/Disk/FreeSpace`— Wolne miejsce uśredniona wszystkie zainstalowane systemy plików</span><span class="sxs-lookup"><span data-stu-id="641b4-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="641b4-301">LAD ani hello portalu Azure oczekuje hello counterSpecifier wartość toomatch żadnych wzorca.</span><span class="sxs-lookup"><span data-stu-id="641b4-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="641b4-302">Być zgodne w konstrukcji counterSpecifier wartości.</span><span class="sxs-lookup"><span data-stu-id="641b4-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="641b4-303">Po określeniu `performanceCounters`, LAD zawsze zapisuje tabeli tooa danych w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="641b4-304">Możesz można mieć hello takie same dane zapisane tooJSON obiekty BLOB i/lub centra zdarzeń, ale nie można wyłączyć zapisywanie tabeli tooa danych.</span><span class="sxs-lookup"><span data-stu-id="641b4-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="641b4-305">Wszystkie wystąpienia toouse skonfigurowanego diagnostycznych rozszerzenia hello hello tego samego konta magazynu, nazwę i punktu końcowego, dodaj ich toohello metryki i dzienniki tej samej tabeli.</span><span class="sxs-lookup"><span data-stu-id="641b4-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="641b4-306">Jeśli pisania zbyt wiele maszyn wirtualnych toohello, który można ograniczyć tej samej partycji tabeli, Azure zapisuje toothat partycji.</span><span class="sxs-lookup"><span data-stu-id="641b4-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="641b4-307">ustawienie powoduje, że wpisy toobe eventVolume Hello rozmieszczenie do 1 (mała liczba godzin), 10 (średnia liczba godzin) lub 100 (duży) różnych partycji.</span><span class="sxs-lookup"><span data-stu-id="641b4-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="641b4-308">Zwykle, "Medium" wystarcza nie jest ograniczany ruch sieciowy tooensure.</span><span class="sxs-lookup"><span data-stu-id="641b4-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="641b4-309">Funkcja Azure metryki Hello hello portalu Azure wykorzystuje hello danych w tej tabeli tooproduce wykresy lub tootrigger alertów.</span><span class="sxs-lookup"><span data-stu-id="641b4-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="641b4-310">Nazwa tabeli Hello jest złączeniem hello te ciągi:</span><span class="sxs-lookup"><span data-stu-id="641b4-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="641b4-311">Witaj "scheduledTransferPeriod" dla hello zagregowane wartościami przechowywanymi w tabeli hello</span><span class="sxs-lookup"><span data-stu-id="641b4-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="641b4-312">Data, w postaci hello "RRRRMMDD", która zmienia co 10 dni</span><span class="sxs-lookup"><span data-stu-id="641b4-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="641b4-313">Przykłady obejmują `WADMetricsPT1HP10DV2S20170410` i `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="641b4-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="641b4-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="641b4-314">syslogEvents</span></span>

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

<span data-ttu-id="641b4-315">Ta sekcja opcjonalna steruje kolekcji hello dziennika zdarzeń z dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="641b4-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="641b4-316">W przypadku pominięcia sekcji hello zdarzenia dziennika systemowego nie są przechwytywane w ogóle.</span><span class="sxs-lookup"><span data-stu-id="641b4-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="641b4-317">Kolekcja syslogEventConfiguration Hello ma jeden wpis dla każdego obiektu syslog zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="641b4-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="641b4-318">W przypadku minSeverity "NONE" dla określonego obiektu lub tego obiektu nie ma w elemencie hello w ogóle, żadne zdarzenia z tym zakładzie są przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="641b4-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="641b4-319">Element</span><span class="sxs-lookup"><span data-stu-id="641b4-319">Element</span></span> | <span data-ttu-id="641b4-320">Wartość</span><span class="sxs-lookup"><span data-stu-id="641b4-320">Value</span></span>
------- | -----
<span data-ttu-id="641b4-321">sink — obiekty</span><span class="sxs-lookup"><span data-stu-id="641b4-321">sinks</span></span> | <span data-ttu-id="641b4-322">Rozdzielana przecinkami lista nazw wychwytywanie toowhich osobny dziennik zdarzeń są publikowane.</span><span class="sxs-lookup"><span data-stu-id="641b4-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="641b4-323">Wszystkie zdarzenia dziennika spełniające hello ograniczenia syslogEventConfiguration są zbiornika tooeach opublikowane na liście.</span><span class="sxs-lookup"><span data-stu-id="641b4-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="641b4-324">Przykład: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="641b4-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="641b4-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="641b4-325">facilityName</span></span> | <span data-ttu-id="641b4-326">Nazwę obiektu syslog (takich jak "dziennika\_użytkownika" lub "dziennika\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="641b4-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="641b4-327">Zobacz sekcję "funkcje" hello hello [strony man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) hello pełnej listy.</span><span class="sxs-lookup"><span data-stu-id="641b4-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="641b4-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="641b4-328">minSeverity</span></span> | <span data-ttu-id="641b4-329">Poziom ważności syslog (takich jak "dziennika\_błąd" lub "dziennika\_informacje").</span><span class="sxs-lookup"><span data-stu-id="641b4-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="641b4-330">Zobacz sekcję "poziomu" hello hello [strony man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) hello pełnej listy.</span><span class="sxs-lookup"><span data-stu-id="641b4-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="641b4-331">rozszerzenie Hello przechwytuje urządzenie toohello zdarzeń wysłanych w lub powyżej hello określony poziom.</span><span class="sxs-lookup"><span data-stu-id="641b4-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="641b4-332">Po określeniu `syslogEvents`, LAD zawsze zapisuje tabeli tooa danych w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="641b4-333">Możesz można mieć hello takie same dane zapisane tooJSON obiekty BLOB i/lub centra zdarzeń, ale nie można wyłączyć zapisywanie tabeli tooa danych.</span><span class="sxs-lookup"><span data-stu-id="641b4-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="641b4-334">Hello partycjonowania zachowanie dla tej tabeli jest taki sam, jak opisano dla hello `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="641b4-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="641b4-335">Nazwa tabeli Hello jest złączeniem hello te ciągi:</span><span class="sxs-lookup"><span data-stu-id="641b4-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="641b4-336">Data, w postaci hello "RRRRMMDD", która zmienia co 10 dni</span><span class="sxs-lookup"><span data-stu-id="641b4-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="641b4-337">Przykłady obejmują `LinuxSyslog20170410` i `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="641b4-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="641b4-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="641b4-338">perfCfg</span></span>

<span data-ttu-id="641b4-339">Określa tę sekcję, wykonanie dowolnego [OMI](https://github.com/Microsoft/omi) zapytania.</span><span class="sxs-lookup"><span data-stu-id="641b4-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

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

<span data-ttu-id="641b4-340">Element</span><span class="sxs-lookup"><span data-stu-id="641b4-340">Element</span></span> | <span data-ttu-id="641b4-341">Wartość</span><span class="sxs-lookup"><span data-stu-id="641b4-341">Value</span></span>
------- | -----
<span data-ttu-id="641b4-342">przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="641b4-342">namespace</span></span> | <span data-ttu-id="641b4-343">(opcjonalnie) hello OMI przestrzeń nazw, w ramach których hello można wykonać zapytania.</span><span class="sxs-lookup"><span data-stu-id="641b4-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="641b4-344">Jeśli nie zostanie podany, hello wartość domyślna to "główny/scx", implementowane przez hello [programu System Center i platform dostawców](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="641b4-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="641b4-345">query</span><span class="sxs-lookup"><span data-stu-id="641b4-345">query</span></span> | <span data-ttu-id="641b4-346">Wykonano toobe zapytania OMI Hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="641b4-347">Tabela</span><span class="sxs-lookup"><span data-stu-id="641b4-347">table</span></span> | <span data-ttu-id="641b4-348">tabeli magazynu systemu Azure hello (opcjonalnie), Witaj wyznaczone konta magazynu (zobacz [chronionych ustawień](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="641b4-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="641b4-349">frequency</span><span class="sxs-lookup"><span data-stu-id="641b4-349">frequency</span></span> | <span data-ttu-id="641b4-350">(opcjonalnie) hello liczbę sekund między wykonanie hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="641b4-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="641b4-351">Wartość domyślna to 300 (5 minut); wartość minimalna wynosi 15 sekund.</span><span class="sxs-lookup"><span data-stu-id="641b4-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="641b4-352">sink — obiekty</span><span class="sxs-lookup"><span data-stu-id="641b4-352">sinks</span></span> | <span data-ttu-id="641b4-353">(opcjonalnie) Powinien zostać opublikowany przecinkami lista nazw dodatkowe wychwytywanie toowhich raw Przykładowe metryki wyników.</span><span class="sxs-lookup"><span data-stu-id="641b4-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="641b4-354">Bez agregacji te przykłady pierwotnych jest obliczana przez rozszerzenie hello lub metryk usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="641b4-355">Należy określić albo "Tabela" lub "sink" i/lub.</span><span class="sxs-lookup"><span data-stu-id="641b4-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="641b4-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="641b4-356">fileLogs</span></span>

<span data-ttu-id="641b4-357">Formanty hello przechwytywania plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="641b4-357">Controls hello capture of log files.</span></span> <span data-ttu-id="641b4-358">LAD przechwytuje nowych wierszy tekstu, ponieważ są one zapisywane toohello plików i zapisuje je w tootable wierszy i/lub dowolnej określonej wychwytywanie (JsonBlob lub EventHub).</span><span class="sxs-lookup"><span data-stu-id="641b4-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="641b4-359">Element</span><span class="sxs-lookup"><span data-stu-id="641b4-359">Element</span></span> | <span data-ttu-id="641b4-360">Wartość</span><span class="sxs-lookup"><span data-stu-id="641b4-360">Value</span></span>
------- | -----
<span data-ttu-id="641b4-361">Plik</span><span class="sxs-lookup"><span data-stu-id="641b4-361">file</span></span> | <span data-ttu-id="641b4-362">Witaj pełną nazwę ścieżki toobe pliku dziennika hello obserwowane i przechwyceniu.</span><span class="sxs-lookup"><span data-stu-id="641b4-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="641b4-363">Hello pathname nazwę jednego pliku; Nie można jej nazwę katalogu lub zawierać symbole wieloznaczne.</span><span class="sxs-lookup"><span data-stu-id="641b4-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="641b4-364">Tabela</span><span class="sxs-lookup"><span data-stu-id="641b4-364">table</span></span> | <span data-ttu-id="641b4-365">tabeli magazynu systemu Azure hello (opcjonalnie), w magazynie Witaj wyznaczone konta (określone w konfiguracji hello chroniony), do nowych wierszy z powitalne "tail" hello pliku są zapisywane.</span><span class="sxs-lookup"><span data-stu-id="641b4-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="641b4-366">sink — obiekty</span><span class="sxs-lookup"><span data-stu-id="641b4-366">sinks</span></span> | <span data-ttu-id="641b4-367">(opcjonalnie) Wysyłane przecinkami lista nazw dodatkowe wychwytywanie toowhich dziennika wierszy.</span><span class="sxs-lookup"><span data-stu-id="641b4-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="641b4-368">Należy określić albo "Tabela" lub "sink" i/lub.</span><span class="sxs-lookup"><span data-stu-id="641b4-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="641b4-369">Obsługiwane przez dostawcę wbudowane hello metryk</span><span class="sxs-lookup"><span data-stu-id="641b4-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="641b4-370">Dostawca metryki wbudowane Hello jest źródłem metryki najbardziej interesujące tooa szeroką gamę użytkowników.</span><span class="sxs-lookup"><span data-stu-id="641b4-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="641b4-371">Te metryki można podzielić na pięć szerokie klasy:</span><span class="sxs-lookup"><span data-stu-id="641b4-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="641b4-372">Procesor</span><span class="sxs-lookup"><span data-stu-id="641b4-372">Processor</span></span>
* <span data-ttu-id="641b4-373">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="641b4-373">Memory</span></span>
* <span data-ttu-id="641b4-374">Sieć</span><span class="sxs-lookup"><span data-stu-id="641b4-374">Network</span></span>
* <span data-ttu-id="641b4-375">System plików</span><span class="sxs-lookup"><span data-stu-id="641b4-375">Filesystem</span></span>
* <span data-ttu-id="641b4-376">Dysk</span><span class="sxs-lookup"><span data-stu-id="641b4-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="641b4-377">wbudowane metryki hello procesora — klasa</span><span class="sxs-lookup"><span data-stu-id="641b4-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="641b4-378">Hello klasy procesora metryk udostępnia informacje na temat użycia procesora w hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="641b4-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="641b4-379">Podczas agregowania wartości procentowych, wynik hello jest średnią hello przez wszystkie procesory.</span><span class="sxs-lookup"><span data-stu-id="641b4-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="641b4-380">W dwa podstawowe maszyny Wirtualnej Jeśli jeden rdzeń był zajęty 100% i hello innych był bezczynny, 100% hello zgłosił, że PercentIdleTime będzie równa 50.</span><span class="sxs-lookup"><span data-stu-id="641b4-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="641b4-381">Jeśli 50% zajęty dla każdego rdzenia hello takie same, hello zgłosił wynik będzie również wartość równa 50.</span><span class="sxs-lookup"><span data-stu-id="641b4-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="641b4-382">Cztery podstawowe maszyny Wirtualnej z jednego rdzenia 100% jest zajęty i hello innym bezczynny, hello zgłosił, że PercentIdleTime jest 75.</span><span class="sxs-lookup"><span data-stu-id="641b4-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="641b4-383">Licznik</span><span class="sxs-lookup"><span data-stu-id="641b4-383">counter</span></span> | <span data-ttu-id="641b4-384">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="641b4-384">Meaning</span></span>
------- | -------
<span data-ttu-id="641b4-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="641b4-385">PercentIdleTime</span></span> | <span data-ttu-id="641b4-386">Procent czasu, w oknie agregacji hello czy procesory zostały wykonywania pętli bezczynności hello jądra</span><span class="sxs-lookup"><span data-stu-id="641b4-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="641b4-387">percentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="641b4-387">PercentProcessorTime</span></span> | <span data-ttu-id="641b4-388">Procent czasu wykonania wątku czynnego</span><span class="sxs-lookup"><span data-stu-id="641b4-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="641b4-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="641b4-389">PercentIOWaitTime</span></span> | <span data-ttu-id="641b4-390">Procent czasu oczekiwania na toocomplete operacji We/Wy</span><span class="sxs-lookup"><span data-stu-id="641b4-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="641b4-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="641b4-391">PercentInterruptTime</span></span> | <span data-ttu-id="641b4-392">Procent czasu wykonywania sprzęt i oprogramowanie przerwań i wywołań DPC (opóźnione wywołania procedur)</span><span class="sxs-lookup"><span data-stu-id="641b4-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="641b4-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="641b4-393">PercentUserTime</span></span> | <span data-ttu-id="641b4-394">Czynnego czasu w oknie agregacji hello hello procent czasu spędzony w użytkownika więcej przy normalnym priorytecie</span><span class="sxs-lookup"><span data-stu-id="641b4-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="641b4-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="641b4-395">PercentNiceTime</span></span> | <span data-ttu-id="641b4-396">Czynnego czasu hello procentowym priorytetem obniżona (nieuprzywilejowany)</span><span class="sxs-lookup"><span data-stu-id="641b4-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="641b4-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="641b4-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="641b4-398">Czynnego czasu hello procentowym w trybie uprzywilejowanym (jądra)</span><span class="sxs-lookup"><span data-stu-id="641b4-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="641b4-399">Witaj pierwsze cztery liczniki powinien Suma too100%.</span><span class="sxs-lookup"><span data-stu-id="641b4-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="641b4-400">Hello ostatnie trzy liczniki również Suma too100%; Suma hello PercentProcessorTime, PercentIOWaitTime i PercentInterruptTime ich podziału.</span><span class="sxs-lookup"><span data-stu-id="641b4-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="641b4-401">Ustaw tooobtain pojedynczego Metryka zagregowane wszystkich procesorów `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="641b4-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="641b4-402">tooobtain metryki dla konkretny procesor, takie jak drugi procesor logiczny hello z czterech podstawowych maszyny Wirtualnej, należy ustawić `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="641b4-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="641b4-403">Numery procesorów logicznych znajdują się w zakresie hello `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="641b4-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="641b4-404">wbudowane metryki hello pamięci — klasa</span><span class="sxs-lookup"><span data-stu-id="641b4-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="641b4-405">Hello klasy pamięci metryk zawiera informacje o wykorzystanie pamięci, stronicowania i wymiany.</span><span class="sxs-lookup"><span data-stu-id="641b4-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="641b4-406">Licznik</span><span class="sxs-lookup"><span data-stu-id="641b4-406">counter</span></span> | <span data-ttu-id="641b4-407">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="641b4-407">Meaning</span></span>
------- | -------
<span data-ttu-id="641b4-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="641b4-408">AvailableMemory</span></span> | <span data-ttu-id="641b4-409">Dostępnej pamięci fizycznej w MiB</span><span class="sxs-lookup"><span data-stu-id="641b4-409">Available physical memory in MiB</span></span>
<span data-ttu-id="641b4-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="641b4-410">PercentAvailableMemory</span></span> | <span data-ttu-id="641b4-411">Dostępna pamięć fizyczna jako procent całkowitej ilości pamięci</span><span class="sxs-lookup"><span data-stu-id="641b4-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="641b4-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="641b4-412">UsedMemory</span></span> | <span data-ttu-id="641b4-413">W użyciu pamięć fizyczna (MiB)</span><span class="sxs-lookup"><span data-stu-id="641b4-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="641b4-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="641b4-414">PercentUsedMemory</span></span> | <span data-ttu-id="641b4-415">W użyciu pamięć fizyczna jako procent całkowitej ilości pamięci</span><span class="sxs-lookup"><span data-stu-id="641b4-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="641b4-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="641b4-416">PagesPerSec</span></span> | <span data-ttu-id="641b4-417">Całkowita liczba stronicowania (odczyt/zapis)</span><span class="sxs-lookup"><span data-stu-id="641b4-417">Total paging (read/write)</span></span>
<span data-ttu-id="641b4-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="641b4-418">PagesReadPerSec</span></span> | <span data-ttu-id="641b4-419">Strony odczytywać kopii magazynu (pliku wymiany, pliku programu, pliku mapowanego itp.)</span><span class="sxs-lookup"><span data-stu-id="641b4-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="641b4-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="641b4-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="641b4-421">Przechowywanie stron zapisanych toobacking (pliku wymiany, pliku mapowanego itp.)</span><span class="sxs-lookup"><span data-stu-id="641b4-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="641b4-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="641b4-422">AvailableSwap</span></span> | <span data-ttu-id="641b4-423">Obszar wymiany nieużywane (MiB)</span><span class="sxs-lookup"><span data-stu-id="641b4-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="641b4-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="641b4-424">PercentAvailableSwap</span></span> | <span data-ttu-id="641b4-425">Obszar wymiany nieużywane jako procent całkowitego obszaru wymiany</span><span class="sxs-lookup"><span data-stu-id="641b4-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="641b4-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="641b4-426">UsedSwap</span></span> | <span data-ttu-id="641b4-427">W użyciu obszar wymiany (MiB)</span><span class="sxs-lookup"><span data-stu-id="641b4-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="641b4-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="641b4-428">PercentUsedSwap</span></span> | <span data-ttu-id="641b4-429">W obsłudze obszaru wymiany w procentach całkowitego obszaru wymiany</span><span class="sxs-lookup"><span data-stu-id="641b4-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="641b4-430">Ta klasa metryki ma tylko jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="641b4-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="641b4-431">atrybut "warunku" Hello nie zawiera przydatne ustawień i powinny być pominięte.</span><span class="sxs-lookup"><span data-stu-id="641b4-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="641b4-432">wbudowane metryki hello sieci — klasa</span><span class="sxs-lookup"><span data-stu-id="641b4-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="641b4-433">Hello klasy metryki sieci zawiera informacje dotyczące aktywności sieci dla poszczególnych interfejsów od uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="641b4-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="641b4-434">LAD nie ujawnia przepustowości metryk, które mogą być pobierane z hosta metryki.</span><span class="sxs-lookup"><span data-stu-id="641b4-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="641b4-435">Licznik</span><span class="sxs-lookup"><span data-stu-id="641b4-435">counter</span></span> | <span data-ttu-id="641b4-436">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="641b4-436">Meaning</span></span>
------- | -------
<span data-ttu-id="641b4-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="641b4-437">BytesTransmitted</span></span> | <span data-ttu-id="641b4-438">Całkowita liczba bajtów wysłanych od momentu rozruchu</span><span class="sxs-lookup"><span data-stu-id="641b4-438">Total bytes sent since boot</span></span>
<span data-ttu-id="641b4-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="641b4-439">BytesReceived</span></span> | <span data-ttu-id="641b4-440">Całkowita liczba bajtów odebranych od rozruchu</span><span class="sxs-lookup"><span data-stu-id="641b4-440">Total bytes received since boot</span></span>
<span data-ttu-id="641b4-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="641b4-441">BytesTotal</span></span> | <span data-ttu-id="641b4-442">Całkowita liczba bajtów wysyłane lub odbierane od rozruchu</span><span class="sxs-lookup"><span data-stu-id="641b4-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="641b4-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="641b4-443">PacketsTransmitted</span></span> | <span data-ttu-id="641b4-444">Łączna liczba pakietów wysłanych od momentu rozruchu</span><span class="sxs-lookup"><span data-stu-id="641b4-444">Total packets sent since boot</span></span>
<span data-ttu-id="641b4-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="641b4-445">PacketsReceived</span></span> | <span data-ttu-id="641b4-446">Całkowita liczba pakietów otrzymanych od rozruchu</span><span class="sxs-lookup"><span data-stu-id="641b4-446">Total packets received since boot</span></span>
<span data-ttu-id="641b4-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="641b4-447">TotalRxErrors</span></span> | <span data-ttu-id="641b4-448">Liczba błędów od rozruchu</span><span class="sxs-lookup"><span data-stu-id="641b4-448">Number of receive errors since boot</span></span>
<span data-ttu-id="641b4-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="641b4-449">TotalTxErrors</span></span> | <span data-ttu-id="641b4-450">Liczba transmisji błędów od rozruchu</span><span class="sxs-lookup"><span data-stu-id="641b4-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="641b4-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="641b4-451">TotalCollisions</span></span> | <span data-ttu-id="641b4-452">Liczba kolizji zgłoszone przez porty sieciowe powitania od rozruchu</span><span class="sxs-lookup"><span data-stu-id="641b4-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="641b4-453">Mimo że ta klasa jest instancji, LAD nie obsługuje przechwytywania metryki sieci zagregowane we wszystkich urządzeń sieciowych.</span><span class="sxs-lookup"><span data-stu-id="641b4-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="641b4-454">Ustaw tooobtain hello metryki dla określonego interfejsu, takich jak eth0, `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="641b4-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="641b4-455">wbudowane metryki hello klasy systemu plików</span><span class="sxs-lookup"><span data-stu-id="641b4-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="641b4-456">Witaj klasy Filesystem metryk udostępnia informacje na temat użycia systemu plików.</span><span class="sxs-lookup"><span data-stu-id="641b4-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="641b4-457">Wartości bezwzględne i procent ma być zgłaszane będą wyświetlane tooan zwykłego użytkownika (a nie głównego).</span><span class="sxs-lookup"><span data-stu-id="641b4-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="641b4-458">Licznik</span><span class="sxs-lookup"><span data-stu-id="641b4-458">counter</span></span> | <span data-ttu-id="641b4-459">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="641b4-459">Meaning</span></span>
------- | -------
<span data-ttu-id="641b4-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="641b4-460">FreeSpace</span></span> | <span data-ttu-id="641b4-461">Dostępnego miejsca na dysku w bajtach</span><span class="sxs-lookup"><span data-stu-id="641b4-461">Available disk space in bytes</span></span>
<span data-ttu-id="641b4-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="641b4-462">UsedSpace</span></span> | <span data-ttu-id="641b4-463">Używane miejsce na dysku w bajtach</span><span class="sxs-lookup"><span data-stu-id="641b4-463">Used disk space in bytes</span></span>
<span data-ttu-id="641b4-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="641b4-464">PercentFreeSpace</span></span> | <span data-ttu-id="641b4-465">Wartość procentowa wolnego miejsca</span><span class="sxs-lookup"><span data-stu-id="641b4-465">Percentage free space</span></span>
<span data-ttu-id="641b4-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="641b4-466">PercentUsedSpace</span></span> | <span data-ttu-id="641b4-467">Procent wykorzystania miejsca</span><span class="sxs-lookup"><span data-stu-id="641b4-467">Percentage used space</span></span>
<span data-ttu-id="641b4-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="641b4-468">PercentFreeInodes</span></span> | <span data-ttu-id="641b4-469">Wartość procentowa węzłów i nieużywanych</span><span class="sxs-lookup"><span data-stu-id="641b4-469">Percentage of unused inodes</span></span>
<span data-ttu-id="641b4-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="641b4-470">PercentUsedInodes</span></span> | <span data-ttu-id="641b4-471">Wartość procentowa przydzielonych (w użyciu) węzły i sumowane przez wszystkie systemy plików</span><span class="sxs-lookup"><span data-stu-id="641b4-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="641b4-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-472">BytesReadPerSecond</span></span> | <span data-ttu-id="641b4-473">Bajtów odczytanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-473">Bytes read per second</span></span>
<span data-ttu-id="641b4-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="641b4-475">Bajtów zapisanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-475">Bytes written per second</span></span>
<span data-ttu-id="641b4-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-476">BytesPerSecond</span></span> | <span data-ttu-id="641b4-477">Bajty odczytu lub zapisu na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-477">Bytes read or written per second</span></span>
<span data-ttu-id="641b4-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-478">ReadsPerSecond</span></span> | <span data-ttu-id="641b4-479">Operacje odczytu na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-479">Read operations per second</span></span>
<span data-ttu-id="641b4-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-480">WritesPerSecond</span></span> | <span data-ttu-id="641b4-481">Zapis operacji na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-481">Write operations per second</span></span>
<span data-ttu-id="641b4-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-482">TransfersPerSecond</span></span> | <span data-ttu-id="641b4-483">Operacje odczytu lub zapisu na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-483">Read or write operations per second</span></span>

<span data-ttu-id="641b4-484">Wartości zagregowane we wszystkich systemach plików można uzyskać przez ustawienie `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="641b4-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="641b4-485">Wartości dla określonego zainstalowany system plików, takich jak "/ mnt", można uzyskać przez ustawienie `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="641b4-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="641b4-486">wbudowane metryki hello klasy dysku</span><span class="sxs-lookup"><span data-stu-id="641b4-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="641b4-487">Witaj klasy dysku metryk zawiera informacje na temat użycia urządzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="641b4-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="641b4-488">Te statystyki mają zastosowanie toohello cały dysk.</span><span class="sxs-lookup"><span data-stu-id="641b4-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="641b4-489">Jeśli istnieje wiele systemów plików na urządzeniu, hello liczników dla tego urządzenia to w rzeczywistości zagregowane we wszystkich z nich.</span><span class="sxs-lookup"><span data-stu-id="641b4-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="641b4-490">Licznik</span><span class="sxs-lookup"><span data-stu-id="641b4-490">counter</span></span> | <span data-ttu-id="641b4-491">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="641b4-491">Meaning</span></span>
------- | -------
<span data-ttu-id="641b4-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-492">ReadsPerSecond</span></span> | <span data-ttu-id="641b4-493">Operacje odczytu na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-493">Read operations per second</span></span>
<span data-ttu-id="641b4-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-494">WritesPerSecond</span></span> | <span data-ttu-id="641b4-495">Zapis operacji na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-495">Write operations per second</span></span>
<span data-ttu-id="641b4-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-496">TransfersPerSecond</span></span> | <span data-ttu-id="641b4-497">Całkowita liczba operacji na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-497">Total operations per second</span></span>
<span data-ttu-id="641b4-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="641b4-498">AverageReadTime</span></span> | <span data-ttu-id="641b4-499">Średnia liczba sekund na operacja odczytu</span><span class="sxs-lookup"><span data-stu-id="641b4-499">Average seconds per read operation</span></span>
<span data-ttu-id="641b4-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="641b4-500">AverageWriteTime</span></span> | <span data-ttu-id="641b4-501">Średnia liczba sekund na operację zapisu</span><span class="sxs-lookup"><span data-stu-id="641b4-501">Average seconds per write operation</span></span>
<span data-ttu-id="641b4-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="641b4-502">AverageTransferTime</span></span> | <span data-ttu-id="641b4-503">Średnia liczba sekund na operację</span><span class="sxs-lookup"><span data-stu-id="641b4-503">Average seconds per operation</span></span>
<span data-ttu-id="641b4-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="641b4-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="641b4-505">Średnia liczba operacji w kolejce dysku</span><span class="sxs-lookup"><span data-stu-id="641b4-505">Average number of queued disk operations</span></span>
<span data-ttu-id="641b4-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="641b4-507">Liczba bajtów odczytanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-507">Number of bytes read per second</span></span>
<span data-ttu-id="641b4-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="641b4-509">Liczba bajtów zapisanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-509">Number of bytes written per second</span></span>
<span data-ttu-id="641b4-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="641b4-510">BytesPerSecond</span></span> | <span data-ttu-id="641b4-511">Liczba bajtów odczytywanych lub zapisywanych na sekundę</span><span class="sxs-lookup"><span data-stu-id="641b4-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="641b4-512">Zagregowane wartości na wszystkich dyskach można uzyskać przez ustawienie `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="641b4-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="641b4-513">Ustaw tooget informacje dotyczące określonego urządzenia (na przykład/dev/sdf1), `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="641b4-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="641b4-514">Instalowanie i konfigurowanie LAD 3.0 za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="641b4-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="641b4-515">Zakładając, że są chronione ustawienia w pliku hello PrivateConfig.json oraz informacje o konfiguracji publicznego jest PublicConfig.json, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="641b4-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="641b4-516">polecenie Hello przyjęto założenie, że używasz tryb zarządzania zasobami Azure hello (arm) hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="641b4-517">tooconfigure LAD wdrożenia klasycznego modelu (ASM), maszynach wirtualnych, Przełącz zbyt trybu "asm" (`azure config mode asm`) i pominąć hello Nazwa grupy zasobów w poleceniu hello.</span><span class="sxs-lookup"><span data-stu-id="641b4-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="641b4-518">Aby uzyskać więcej informacji, zobacz hello [dokumentacji interfejsu wiersza polecenia i platform](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="641b4-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="641b4-519">Przykład LAD 3.0 konfiguracji</span><span class="sxs-lookup"><span data-stu-id="641b4-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="641b4-520">Oparte na powitania poprzedzających definicje, tutaj jego Przykładowa konfiguracja rozszerzenia LAD 3.0 wyjaśnienie niektórych.</span><span class="sxs-lookup"><span data-stu-id="641b4-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="641b4-521">tooapply przykładowym scenariuszu tooyour powinien korzystać z własnej nazwy konta magazynu, uwzględniając tokenu sygnatury dostępu Współdzielonego i tokeny EventHubs sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="641b4-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="641b4-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="641b4-522">PrivateConfig.json</span></span>

<span data-ttu-id="641b4-523">Skonfiguruj te ustawienia prywatnych:</span><span class="sxs-lookup"><span data-stu-id="641b4-523">These private settings configure:</span></span>

* <span data-ttu-id="641b4-524">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="641b4-524">a storage account</span></span>
* <span data-ttu-id="641b4-525">zgodnego tokenu sygnatury dostępu Współdzielonego konta</span><span class="sxs-lookup"><span data-stu-id="641b4-525">a matching account SAS token</span></span>
* <span data-ttu-id="641b4-526">wychwytywanie kilka (JsonBlob lub EventHubs z tokenami SAS)</span><span class="sxs-lookup"><span data-stu-id="641b4-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

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

### <a name="publicconfigjson"></a><span data-ttu-id="641b4-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="641b4-527">PublicConfig.json</span></span>

<span data-ttu-id="641b4-528">Te ustawienia publicznego spowodować LAD do:</span><span class="sxs-lookup"><span data-stu-id="641b4-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="641b4-529">Przekaż procent procesora czasu i używać miejsca na dysku metryki toohello `WADMetrics*` tabeli</span><span class="sxs-lookup"><span data-stu-id="641b4-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="641b4-530">Przekazywanie komunikatów z toohello zakładzie "użytkownika" i ważność "informacje" syslog `LinuxSyslog*` tabeli</span><span class="sxs-lookup"><span data-stu-id="641b4-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="641b4-531">Przekaż raw OMI zapytania wyników (PercentProcessorTime i PercentIdleTime) toohello o nazwie `LinuxCPU` tabeli</span><span class="sxs-lookup"><span data-stu-id="641b4-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="641b4-532">Przekaż dołączany wiersze w pliku `/var/log/myladtestlog` toohello `MyLadTestLog` tabeli</span><span class="sxs-lookup"><span data-stu-id="641b4-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="641b4-533">W każdym przypadku również przekazywania danych do:</span><span class="sxs-lookup"><span data-stu-id="641b4-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="641b4-534">Magazyn obiektów Blob Azure (nazwa kontenera jest zdefiniowany w ujściu JsonBlob hello)</span><span class="sxs-lookup"><span data-stu-id="641b4-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="641b4-535">Punkt końcowy EventHubs (jak określono w ujściu EventHubs hello)</span><span class="sxs-lookup"><span data-stu-id="641b4-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

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

<span data-ttu-id="641b4-536">Witaj `resourceId` hello konfiguracji musi odpowiadać czy skali maszyny wirtualnej maszyny Wirtualnej lub hello hello ustawiony.</span><span class="sxs-lookup"><span data-stu-id="641b4-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="641b4-537">Metryki platformy Azure, wykresów i alerty wie resourceId hello z hello pracy maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="641b4-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="641b4-538">Oczekuje toofind hello danych dla maszyny Wirtualnej przy użyciu hello resourceId hello wyszukiwania klucza.</span><span class="sxs-lookup"><span data-stu-id="641b4-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="641b4-539">Jeśli używasz platformy Azure skalowania automatycznego resourceId hello w konfiguracji automatycznego skalowania hello musi być zgodna z resourceId hello używane przez LAD.</span><span class="sxs-lookup"><span data-stu-id="641b4-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="641b4-540">Hello resourceId jest wbudowana w hello nazwy JsonBlobs napisane przez LAD.</span><span class="sxs-lookup"><span data-stu-id="641b4-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="641b4-541">Wyświetlanie danych</span><span class="sxs-lookup"><span data-stu-id="641b4-541">View your data</span></span>

<span data-ttu-id="641b4-542">Dane dotyczące wydajności hello tooview portalu Azure lub Ustaw alerty:</span><span class="sxs-lookup"><span data-stu-id="641b4-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![Obraz](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="641b4-544">Witaj `performanceCounters` danych zawsze są przechowywane w tabeli magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="641b4-545">Interfejsy API usługi Azure Storage są dostępne dla wielu języków i platform.</span><span class="sxs-lookup"><span data-stu-id="641b4-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="641b4-546">Dane wysyłane wychwytywanie tooJsonBlob są przechowywane w obiekty BLOB na koncie magazynu hello o nazwie w hello [chronionych ustawień](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="641b4-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="641b4-547">Będzie można korzystać z danych obiektu blob hello przy użyciu dowolnego interfejsów API magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="641b4-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="641b4-548">Ponadto można użyć tych danych hello tooaccess narzędzi interfejsu użytkownika w usłudze Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="641b4-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="641b4-549">Eksplorator serwera programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="641b4-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="641b4-550">[Eksplorator usługi Storage platformy Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Eksploratora usługi Azure Storage").</span><span class="sxs-lookup"><span data-stu-id="641b4-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="641b4-551">Ta migawka sesji Eksploratora usługi Microsoft Azure Storage pokazuje hello wygenerowane tabele usługi Azure Storage i kontenery z rozszerzeniem LAD 3.0 poprawnie skonfigurowana na testowej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="641b4-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="641b4-552">Obraz powitania nie jest zgodna z hello [Przykładowa konfiguracja LAD 3.0](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="641b4-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![Obraz](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="641b4-554">Zobacz hello odpowiednich [dokumentacji EventHubs](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn jak tooconsume komunikaty opublikowane tooan EventHubs endpoint.</span><span class="sxs-lookup"><span data-stu-id="641b4-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="641b4-555">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="641b4-555">Next steps</span></span>

* <span data-ttu-id="641b4-556">Tworzenie metryk alertów w [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) dla metryki hello zbierania.</span><span class="sxs-lookup"><span data-stu-id="641b4-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="641b4-557">Utwórz [monitorowania wykresy](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) dla Twojego metryki.</span><span class="sxs-lookup"><span data-stu-id="641b4-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="641b4-558">Dowiedz się, jak za[utworzyć zestaw skali maszyny wirtualnej](/azure/virtual-machines/linux/tutorial-create-vmss) przy użyciu programu Skalowanie automatyczne toocontrol metryki.</span><span class="sxs-lookup"><span data-stu-id="641b4-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
