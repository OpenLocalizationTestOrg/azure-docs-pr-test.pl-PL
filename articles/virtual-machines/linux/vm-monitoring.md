---
title: "aaaEnable lub wyłączenie monitorowania maszyny Wirtualnej Azure"
description: "Opisuje sposób tooEnable lub Wyłącz monitorowanie maszyny Wirtualnej Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="72806-103">Włącz lub Wyłącz monitorowanie maszyna wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="72806-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="72806-104">W tej sekcji opisano, jak tooenable lub wyłączania monitorowania na wirtualnej maszyny działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="72806-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="72806-105">Można włączyć lub wyłączyć monitorowanie za pomocą portalu hello lub interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (hello Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="72806-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72806-106">Ten dokument zawiera opis wersji 2.3 hello diagnostycznych rozszerzenia systemu Linux, która została wycofana.</span><span class="sxs-lookup"><span data-stu-id="72806-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="72806-107">Wersja 2.3 będzie obsługiwana do 30 czerwca 2018.</span><span class="sxs-lookup"><span data-stu-id="72806-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="72806-108">Zamiast tego można włączyć w wersji 3.0 hello rozszerzenia diagnostyczne systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="72806-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="72806-109">Aby uzyskać więcej informacji, zobacz [hello dokumentacji](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="72806-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="72806-110">Włącz / Wyłącz monitorowanie za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="72806-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="72806-111">Umożliwia monitorowanie maszyny Wirtualnej Azure, która zapewnia dane dotyczące wystąpienia w okresach 1 minutę.</span><span class="sxs-lookup"><span data-stu-id="72806-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="72806-112">(dotyczy zmiany magazynu).</span><span class="sxs-lookup"><span data-stu-id="72806-112">(storage changes apply).</span></span> <span data-ttu-id="72806-113">Dane diagnostyczne szczegółowe jest dostępna dla hello maszyny Wirtualnej w portalu wykresy hello lub za pośrednictwem hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="72806-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="72806-114">Domyślnie portalu Azure umożliwia oparta na hoście monitorowanie określonych metryk.</span><span class="sxs-lookup"><span data-stu-id="72806-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="72806-115">Umożliwia monitorowanie pomiarów w maszynie Wirtualnej podczas powitalne maszyna wirtualna jest uruchomiona lub zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="72806-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="72806-116">Otwórz hello Azure w portalu [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72806-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="72806-117">Lewy pasek nawigacyjny hello kliknij maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="72806-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="72806-118">W przypadku hello listy maszyn wirtualnych należy wybrać wystąpienie uruchamiania i zatrzymywana.</span><span class="sxs-lookup"><span data-stu-id="72806-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="72806-119">zostanie otwarty blok "Maszyny wirtualnej" Hello.</span><span class="sxs-lookup"><span data-stu-id="72806-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="72806-120">Kliknij pozycję wszystkie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="72806-120">Click All settings.</span></span>
* <span data-ttu-id="72806-121">Kliknij pozycję Diagnostyka.</span><span class="sxs-lookup"><span data-stu-id="72806-121">Click Diagnostics.</span></span>
* <span data-ttu-id="72806-122">Zmień stan tooOn lub wyłączona.</span><span class="sxs-lookup"><span data-stu-id="72806-122">Change status tooOn or Off.</span></span> <span data-ttu-id="72806-123">Możesz również wybrać na tym poziomie hello bloku monitorowania szczegóły chcesz tooenable dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72806-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Włącz / Wyłącz monitorowanie za pomocą hello portalu Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="72806-125">Włącz / Wyłącz monitorowanie za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="72806-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="72806-126">tooenable monitorowanie dla maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="72806-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="72806-127">Utwórz plik (nazwanych takich jak PrivateConfig.json):</span><span class="sxs-lookup"><span data-stu-id="72806-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="72806-128">Włącz rozszerzenia hello za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="72806-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="72806-129">Aby uzyskać więcej informacji, zobacz [przy użyciu rozszerzenia diagnostycznych Linux tooMonitor maszyny Wirtualnej systemu Linux na wydajność i danych diagnostycznych](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72806-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
