---
title: "niestandardowych skryptów aaaRun na maszynach wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Automatyzowanie zadań konfiguracji maszyny Wirtualnej systemu Linux przy użyciu hello niestandardowe rozszerzenie skryptu"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="2d9aa-103">Przy użyciu hello Azure niestandardowe rozszerzenie skryptu z maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="2d9aa-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="2d9aa-104">Witaj niestandardowe rozszerzenie skryptu pobiera i uruchamia skrypty na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="2d9aa-105">To rozszerzenie jest przydatne w przypadku konfiguracji wdrożenia post, instalacja oprogramowania lub dowolnej innej konfiguracji / zadanie zarządzania.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="2d9aa-106">Skrypty można pobrać z magazynu Azure lub inne dostępne miejsce w Internecie lub podane rozszerzenie toohello czas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="2d9aa-107">Hello rozszerzenia niestandardowego skryptu integruje się z szablonów usługi Azure Resource Manager i można również uruchomić przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, portalu Azure lub hello interfejsu API REST maszyny wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="2d9aa-108">Szczegóły tego dokumentu, jak toouse hello niestandardowe rozszerzenie skryptu z hello Azure CLI i szablonu usługi Azure Resource Manager, a także szczegółowe informacje, kroki w systemach Linux rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="2d9aa-109">Konfiguracja rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="2d9aa-109">Extension Configuration</span></span>
<span data-ttu-id="2d9aa-110">Hello niestandardowe rozszerzenie skryptu konfiguracji określa lokalizację i hello toobe polecenie Uruchom.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="2d9aa-111">Tej konfiguracji mogą być przechowywane w plikach konfiguracji określone w wierszu polecenia hello lub w szablonie usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="2d9aa-112">Poufne dane mogą być przechowywane w chronionej konfigurację, która zostaje zaszyfrowany i odszyfrowane tylko wewnątrz maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="2d9aa-113">Konfiguracja chronionych Hello jest użyteczna, gdy hello wykonanie polecenia zawiera klucze tajne, takie jak hasła.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="2d9aa-114">Publiczna Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="2d9aa-114">Public Configuration</span></span>
<span data-ttu-id="2d9aa-115">Schemat:</span><span class="sxs-lookup"><span data-stu-id="2d9aa-115">Schema:</span></span>

<span data-ttu-id="2d9aa-116">**Uwaga** — te nazwy właściwości jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="2d9aa-117">Użyj nazwy hello, jak pokazano poniżej tooavoid problemy z wdrażaniem.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="2d9aa-118">**commandToExecute**: (wymagane, string) hello tooexecute skryptu punktu wejścia</span><span class="sxs-lookup"><span data-stu-id="2d9aa-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="2d9aa-119">**fileUris**: pobrać adresy URL hello toobe plików (opcjonalne, tablicy ciągów).</span><span class="sxs-lookup"><span data-stu-id="2d9aa-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="2d9aa-120">**Sygnatura czasowa** (opcjonalne, liczba całkowita) Użyj tego pola tootrigger tylko Uruchom ponownie skrypt hello, zmieniając wartość tego pola.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="2d9aa-121">Konfiguracja chronionych</span><span class="sxs-lookup"><span data-stu-id="2d9aa-121">Protected Configuration</span></span>
<span data-ttu-id="2d9aa-122">Schemat:</span><span class="sxs-lookup"><span data-stu-id="2d9aa-122">Schema:</span></span>

<span data-ttu-id="2d9aa-123">**Uwaga** — te nazwy właściwości jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="2d9aa-124">Użyj nazwy hello, jak pokazano poniżej tooavoid problemy z wdrażaniem.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="2d9aa-125">**commandToExecute**: (opcjonalne, ciąg) hello tooexecute skryptu punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="2d9aa-126">Zamiast tego użyj tego pola, jeśli polecenie zawiera klucze tajne, takie jak hasła.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="2d9aa-127">**storageAccountName**: (opcjonalne, ciąg) hello nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="2d9aa-128">Jeśli określisz poświadczeń magazynu fileUris wszystkie muszą być adresami URL dla obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="2d9aa-129">**storageAccountKey**: (opcjonalne, ciąg) hello klucz dostępu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="2d9aa-130">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2d9aa-130">Azure CLI</span></span>
<span data-ttu-id="2d9aa-131">Używając hello Azure CLI toorun hello niestandardowe rozszerzenie skryptu, Utwórz plik konfiguracji lub pliki zawierające uri pliku hello minimalna i hello skryptu wykonywania polecenia.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="2d9aa-132">Opcjonalnie hello ustawienia można określić w poleceniu hello jako ciąg w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="2d9aa-133">Dzięki temu toobe konfiguracji hello określony podczas wykonywania i bez pliku osobną konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="2d9aa-134">Przykłady Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2d9aa-134">Azure CLI Examples</span></span>

<span data-ttu-id="2d9aa-135">**Przykład 1** -publicznej konfiguracji z pliku skryptu.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="2d9aa-136">Polecenia interfejsu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="2d9aa-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="2d9aa-137">**Przykład 2** -publicznej konfiguracji z żadnego pliku skryptu.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="2d9aa-138">Polecenia interfejsu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="2d9aa-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="2d9aa-139">**Przykład 3** — plik konfiguracji publicznego jest plik skryptu używany toospecify hello identyfikatora URI, a plik chroniony konfiguracji jest toobe polecenia hello używane toospecify wykonywane.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="2d9aa-140">Plik konfiguracji publicznego:</span><span class="sxs-lookup"><span data-stu-id="2d9aa-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="2d9aa-141">Plik chroniony konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="2d9aa-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="2d9aa-142">Polecenia interfejsu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="2d9aa-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="2d9aa-143">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d9aa-143">Resource Manager Template</span></span>
<span data-ttu-id="2d9aa-144">Hello Azure niestandardowe rozszerzenie skryptu można uruchomić w czasie wdrażania maszyny wirtualnej przy użyciu szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="2d9aa-145">toodo tak, Dodaj prawidłowo sformatowane JSON toohello wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="2d9aa-146">Przykłady usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d9aa-146">Resource Manager Examples</span></span>
<span data-ttu-id="2d9aa-147">**Przykład 1** -publicznej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-147">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="2d9aa-148">**Przykład 2** — wykonanie polecenia w chronionym konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-148">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="2d9aa-149">Zobacz hello .net Core utworów muzycznych magazynu pokaz pełny przykład - [pokaz magazynu utworów muzycznych](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="2d9aa-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2d9aa-150">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="2d9aa-150">Troubleshooting</span></span>
<span data-ttu-id="2d9aa-151">Po uruchomieniu hello niestandardowe rozszerzenie skryptu skryptu hello jest tworzony lub pobrany do katalogu toohello podobne, poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="2d9aa-152">dane wyjściowe polecenia Hello jest także zapisane w tym katalogu w `stdout` i `stderr` pliku.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="2d9aa-153">Witaj rozszerzenie skryptu Azure tworzy dziennika, który można znaleźć tutaj.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="2d9aa-154">Stan wykonywania Hello hello niestandardowe rozszerzenie skryptu można również pobrać z hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9aa-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="2d9aa-155">dane wyjściowe Hello wygląda hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="2d9aa-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="2d9aa-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2d9aa-156">Next Steps</span></span>
<span data-ttu-id="2d9aa-157">Aby uzyskać informacje na inne rozszerzenia skryptu maszyny Wirtualnej, zobacz [omówienie rozszerzenie skryptu Azure dla systemu Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2d9aa-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

