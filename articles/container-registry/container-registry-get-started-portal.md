---
title: prywatne aaaCreate Docker rejestru - portalu Azure | Dokumentacja firmy Microsoft
description: "Rozpocząć tworzenie i zarządzanie nimi prywatnej rejestrów kontenera Docker z hello portalu Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="99f82-103">Utwórz prywatne rejestru kontenera Docker przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="99f82-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="99f82-104">Użyj hello Azure toocreate portalu rejestru kontenera i zarządzać ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="99f82-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="99f82-105">Można również utworzyć i zarządzać nimi za pomocą hello rejestrów kontenera [poleceń Azure CLI 2.0](container-registry-get-started-azure-cli.md), [programu Azure PowerShell](container-registry-get-started-powershell.md) lub programowo hello rejestru kontenera [interfejsu API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="99f82-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="99f82-106">Tło i pojęcia dla [hello omówienie](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="99f82-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="99f82-107">Tworzenie rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="99f82-107">Create a container registry</span></span>
1. <span data-ttu-id="99f82-108">W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **+ nowy**.</span><span class="sxs-lookup"><span data-stu-id="99f82-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="99f82-109">Marketplace hello wyszukiwania dla **rejestru kontenera platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="99f82-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="99f82-110">Wybierz pozycję **Azure Container Registry**, której wydawcą jest firma **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="99f82-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="99f82-111">![Usługa Container Registry w portalu Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="99f82-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="99f82-112">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="99f82-112">Click **Create**.</span></span> <span data-ttu-id="99f82-113">Witaj **rejestru kontenera Azure** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="99f82-113">hello **Azure Container Registry** blade appears.</span></span>

    ![Ustawienia usługi Container Registry](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="99f82-115">W hello **rejestru kontenera Azure** bloku, wprowadź hello następujących informacji.</span><span class="sxs-lookup"><span data-stu-id="99f82-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="99f82-116">Po zakończeniu kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="99f82-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="99f82-117">a.</span><span class="sxs-lookup"><span data-stu-id="99f82-117">a.</span></span> <span data-ttu-id="99f82-118">**Nazwa rejestru**: globalnie unikatowa nazwa domeny najwyższego poziomu dla określonego rejestru.</span><span class="sxs-lookup"><span data-stu-id="99f82-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="99f82-119">W tym przykładzie nazwa rejestru hello jest *myRegistry01*, ale podstawić własną unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="99f82-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="99f82-120">Nazwa Hello może zawierać tylko litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="99f82-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="99f82-121">b.</span><span class="sxs-lookup"><span data-stu-id="99f82-121">b.</span></span> <span data-ttu-id="99f82-122">**Grupa zasobów**: Wybierz istniejący [grupy zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) lub nazwa typu hello nowej.</span><span class="sxs-lookup"><span data-stu-id="99f82-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="99f82-123">c.</span><span class="sxs-lookup"><span data-stu-id="99f82-123">c.</span></span> <span data-ttu-id="99f82-124">**Lokalizacja**: Wybierz lokalizację centrum danych Azure, gdzie usługa hello jest [dostępne](https://azure.microsoft.com/regions/services/), takich jak **południowo-środkowe stany**.</span><span class="sxs-lookup"><span data-stu-id="99f82-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="99f82-125">d.</span><span class="sxs-lookup"><span data-stu-id="99f82-125">d.</span></span> <span data-ttu-id="99f82-126">**Administrator**: należy włączyć rejestru hello tooaccess użytkownika Administrator.</span><span class="sxs-lookup"><span data-stu-id="99f82-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="99f82-127">Można zmienić to ustawienie po utworzeniu hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="99f82-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="99f82-128">Ponadto tooproviding uzyskiwać dostęp do konta administratora, rejestrów kontenera obsługę uwierzytelniania kopii podmiotów zabezpieczeń usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="99f82-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="99f82-129">Więcej informacji i zagadnień do rozważenia znajduje się w temacie [Authenticate with a container registry](container-registry-authentication.md) (Uwierzytelnianie za pomocą rejestru kontenerów).</span><span class="sxs-lookup"><span data-stu-id="99f82-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="99f82-130">e.</span><span class="sxs-lookup"><span data-stu-id="99f82-130">e.</span></span> <span data-ttu-id="99f82-131">**Konto magazynu**: Użyj hello domyślne ustawienie toocreate [konta magazynu](../storage/common/storage-introduction.md), lub wybierz istniejące konto magazynu w hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="99f82-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="99f82-132">Usługa Premium Storage nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="99f82-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="99f82-133">Zarządzanie ustawieniami rejestru</span><span class="sxs-lookup"><span data-stu-id="99f82-133">Manage registry settings</span></span>
<span data-ttu-id="99f82-134">Po utworzeniu hello rejestru, Znajdź hello ustawień rejestru należy uruchomić na powitania **rejestrów kontenera** bloku w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="99f82-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="99f82-135">Na przykład może być konieczne hello toolog ustawień w rejestrze tooyour lub może być tooenable lub wyłączyć hello administrator.</span><span class="sxs-lookup"><span data-stu-id="99f82-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="99f82-136">Na powitania **rejestrów kontenera** bloku, kliknij nazwę hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="99f82-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![Blok rejestru kontenerów](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="99f82-138">toomanage ustawień dostępu, kliknij przycisk **klucz dostępu**.</span><span class="sxs-lookup"><span data-stu-id="99f82-138">toomanage access settings, click **Access key**.</span></span>

    ![Dostęp do rejestru kontenerów](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="99f82-140">Należy zwrócić uwagę hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="99f82-140">Note hello following settings:</span></span>

   * <span data-ttu-id="99f82-141">**Serwer logowania** -hello w pełni kwalifikowanej nazwy użyj toolog w rejestrze toohello.</span><span class="sxs-lookup"><span data-stu-id="99f82-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="99f82-142">W tym przykładzie jest to `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="99f82-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="99f82-143">**Administrator** — Przełącz tooenable lub wyłączenie konta administratora hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="99f82-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="99f82-144">**Nazwa użytkownika** i **hasło** — Witaj poświadczeń konta administratora hello (jeśli jest włączona) toolog można użyć w rejestrze toohello.</span><span class="sxs-lookup"><span data-stu-id="99f82-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="99f82-145">Opcjonalnie można ponownie wygenerować hello hasła.</span><span class="sxs-lookup"><span data-stu-id="99f82-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="99f82-146">Dwa hasła są tworzone, dzięki czemu można zachować rejestru toohello połączenia za pomocą jednego hasła podczas ponownego generowania hello inne hasło.</span><span class="sxs-lookup"><span data-stu-id="99f82-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="99f82-147">Zamiast tego zobacz tooauthenticate z nazwy głównej usługi [uwierzytelniony przez prywatne rejestru kontenera Docker](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="99f82-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="99f82-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99f82-148">Next steps</span></span>
* [<span data-ttu-id="99f82-149">Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push</span><span class="sxs-lookup"><span data-stu-id="99f82-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
