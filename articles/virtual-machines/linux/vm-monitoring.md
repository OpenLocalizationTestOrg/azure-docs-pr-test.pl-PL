---
title: "Włączanie lub wyłączanie monitorowania maszyna wirtualna platformy Azure"
description: "Opisuje, jak włączyć lub wyłączyć monitorowanie maszyna wirtualna platformy Azure"
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
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="692ea-103">Włącz lub Wyłącz monitorowanie maszyna wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="692ea-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="692ea-104">W tej sekcji opisano, jak włączyć lub wyłączyć monitorowanie w przypadku maszyn wirtualnych działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="692ea-104">This section describes how to enable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="692ea-105">Można włączyć lub wyłączyć monitorowanie za pomocą portalu lub interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="692ea-105">You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="692ea-106">Ten dokument zawiera opis wersji 2.3 rozszerzenia diagnostyczne systemu Linux, która została wycofana.</span><span class="sxs-lookup"><span data-stu-id="692ea-106">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="692ea-107">Wersja 2.3 będzie obsługiwana do 30 czerwca 2018.</span><span class="sxs-lookup"><span data-stu-id="692ea-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="692ea-108">Zamiast tego można włączyć w wersji 3.0 rozszerzenia diagnostyczne systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="692ea-108">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="692ea-109">Aby uzyskać więcej informacji, zobacz [dokumentacji](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="692ea-109">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-the-azure-portal"></a><span data-ttu-id="692ea-110">Włącz / Wyłącz monitorowanie za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="692ea-110">Enable / Disable Monitoring through the Azure portal</span></span>

<span data-ttu-id="692ea-111">Umożliwia monitorowanie maszyny Wirtualnej Azure, która zapewnia dane dotyczące wystąpienia w okresach 1 minutę.</span><span class="sxs-lookup"><span data-stu-id="692ea-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="692ea-112">(dotyczy zmiany magazynu).</span><span class="sxs-lookup"><span data-stu-id="692ea-112">(storage changes apply).</span></span> <span data-ttu-id="692ea-113">Dane diagnostyczne szczegółowe jest dostępna dla maszyny Wirtualnej w portalu wykresy lub za pośrednictwem interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="692ea-113">Detailed diagnostics data is then available for the VM in the portal graphs or through the API.</span></span> <span data-ttu-id="692ea-114">Domyślnie portalu Azure umożliwia oparta na hoście monitorowanie określonych metryk.</span><span class="sxs-lookup"><span data-stu-id="692ea-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="692ea-115">Umożliwia monitorowanie pomiarów w maszynie Wirtualnej uruchomionej maszyny Wirtualnej lub w stanie zatrzymania.</span><span class="sxs-lookup"><span data-stu-id="692ea-115">You can enable monitoring of metrics from within a VM while the VM is running or in stopped state.</span></span>

* <span data-ttu-id="692ea-116">Otwórz portal Azure w [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="692ea-116">Open the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="692ea-117">Na lewym pasku nawigacyjnym kliknij maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="692ea-117">In the left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="692ea-118">Na maszynach wirtualnych listy wybierz wystąpienie uruchamiania i zatrzymywana.</span><span class="sxs-lookup"><span data-stu-id="692ea-118">In the list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="692ea-119">Zostanie otwarty blok "Maszyny wirtualnej".</span><span class="sxs-lookup"><span data-stu-id="692ea-119">The "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="692ea-120">Kliknij pozycję wszystkie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="692ea-120">Click All settings.</span></span>
* <span data-ttu-id="692ea-121">Kliknij pozycję Diagnostyka.</span><span class="sxs-lookup"><span data-stu-id="692ea-121">Click Diagnostics.</span></span>
* <span data-ttu-id="692ea-122">Zmiana stanu na włączony lub wyłączony.</span><span class="sxs-lookup"><span data-stu-id="692ea-122">Change status to On or Off.</span></span> <span data-ttu-id="692ea-123">Można również wybrać w tym bloku poziom monitorowania szczegóły, które chcesz włączyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="692ea-123">You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.</span></span>

![Włącz / Wyłącz monitorowanie za pomocą portalu Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="692ea-125">Włącz / Wyłącz monitorowanie za pomocą interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="692ea-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="692ea-126">Aby włączyć monitorowanie dla maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="692ea-126">To enable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="692ea-127">Utwórz plik (nazwanych takich jak PrivateConfig.json):</span><span class="sxs-lookup"><span data-stu-id="692ea-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* <span data-ttu-id="692ea-128">Włącz rozszerzenia za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="692ea-128">Enable the extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="692ea-129">Aby uzyskać więcej informacji, zobacz [przy użyciu systemu Linux diagnostycznych rozszerzenia Monitor systemu Linux VM wydajności i danych diagnostycznych](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="692ea-129">For more information, see [Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
