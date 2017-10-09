---
title: "aaaAzure chmury powłoki (wersja zapoznawcza) — Szybki Start | Dokumentacja firmy Microsoft"
description: "Szybki Start dla hello powłoki chmury Azure"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a><span data-ttu-id="bac12-103">Szybki Start dotyczące używania hello powłoki chmury Azure</span><span class="sxs-lookup"><span data-stu-id="bac12-103">Quickstart for using hello Azure Cloud Shell</span></span>

<span data-ttu-id="bac12-104">Ten dokument zawiera szczegóły jak toouse hello Azure Cloud powłoki w hello [portalu Azure](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bac12-104">This document details how toouse hello Azure Cloud Shell in hello [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="bac12-105">Uruchom powłokę chmury</span><span class="sxs-lookup"><span data-stu-id="bac12-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="bac12-106">Uruchom **powłoki chmury** z hello górnym menu nawigacyjnym hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bac12-106">Launch **Cloud Shell** from hello top navigation of hello Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="bac12-107">Wybierz toocreate subskrypcja konta magazynu i udział plików na platformę Azure</span><span class="sxs-lookup"><span data-stu-id="bac12-107">Select a subscription toocreate a storage account and Azure file share</span></span>
3. <span data-ttu-id="bac12-108">Wybierz opcję "Utwórz magazyn"</span><span class="sxs-lookup"><span data-stu-id="bac12-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="bac12-109">Azure CLI 2.0 są automatycznie uwierzytelniani w każdym sesssion.</span><span class="sxs-lookup"><span data-stu-id="bac12-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="bac12-110">Ustaw swoją subskrypcję</span><span class="sxs-lookup"><span data-stu-id="bac12-110">Set your subscription</span></span>
1. <span data-ttu-id="bac12-111">Subskrypcje listy, do których masz dostęp do:</span><span class="sxs-lookup"><span data-stu-id="bac12-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="bac12-112">Ustaw preferowany subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="bac12-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="bac12-113">Subskrypcja zostanie zapamiętany dla przyszłych sesji przy użyciu `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="bac12-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="bac12-114">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="bac12-114">Create a resource group</span></span>
<span data-ttu-id="bac12-115">Utwórz nową grupę zasobów w WestUS o nazwie "MyRG":</span><span class="sxs-lookup"><span data-stu-id="bac12-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="bac12-116">Tworzenie maszyny wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="bac12-116">Create a Linux VM</span></span>
<span data-ttu-id="bac12-117">Tworzenie maszyny Wirtualnej systemu Ubuntu w nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bac12-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="bac12-118">Hello Azure CLI 2.0 utworzy kluczy SSH i hello konfiguracji maszyny Wirtualnej z nimi.</span><span class="sxs-lookup"><span data-stu-id="bac12-118">hello Azure CLI 2.0 will create SSH keys and setup hello VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="bac12-119">Witaj tooauthenticate klucze publiczne i prywatne używane maszyny Wirtualnej są umieszczane w `/User/.ssh/id_rsa` i `/User/.ssh/id_rsa.pub` przez Azure CLI 2.0 domyślnie.</span><span class="sxs-lookup"><span data-stu-id="bac12-119">hello public and private keys used tooauthenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="bac12-120">Folderu .ssh jest utrwalona w obrazie 5 GB na udział dołączonych plików na platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="bac12-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="bac12-121">Nazwa użytkownika na tej maszynie Wirtualnej zostanie nazwy użytkownika używane w chmurze powłoki ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="bac12-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="bac12-122">SSH do maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="bac12-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="bac12-123">Wyszukaj nazwę maszyny Wirtualnej na pasku wyszukiwania portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="bac12-123">Search for your VM name in hello Azure portal search bar</span></span>
2. <span data-ttu-id="bac12-124">Kliknij przycisk "Połącz", a następnie uruchom:`ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="bac12-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="bac12-125">Podczas ustanawiania połączenia SSH hello, powinna zostać wyświetlona hello Ubuntu powitalnej wiersza.</span><span class="sxs-lookup"><span data-stu-id="bac12-125">Upon establishing hello SSH connection, you should see hello Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="bac12-126">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="bac12-126">Cleaning up</span></span> 
<span data-ttu-id="bac12-127">Usunięcie grupy zasobów i wszystkie zasoby w niej:</span><span class="sxs-lookup"><span data-stu-id="bac12-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="bac12-128">Uruchom polecenie `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="bac12-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="bac12-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bac12-129">Next Steps</span></span>
[<span data-ttu-id="bac12-130">Dowiedz się więcej o trwałych magazynu w chmurze powłoki</span><span class="sxs-lookup"><span data-stu-id="bac12-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="bac12-131">
[Więcej informacji na temat usługi Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="bac12-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="bac12-132">
[Więcej informacji na temat usługi Magazyn plików Azure](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="bac12-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>