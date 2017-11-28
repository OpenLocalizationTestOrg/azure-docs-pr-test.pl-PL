---
title: "Tworzenie prywatnego rejestru platformy Docker — witryna Azure Portal | Microsoft Doc"
description: "Rozpoczynanie pracy z tworzeniem prywatnych rejestrów kontenerów platformy Docker za pomocą witryny Azure Portal i zarządzaniem nimi"
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
ms.openlocfilehash: 7fbbb56d775ee96c9a44363a4e41d4fc3c630582
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-portal"></a><span data-ttu-id="8aad0-103">Tworzenie prywatnego rejestru kontenerów platformy Docker za pomocą witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8aad0-103">Create a private Docker container registry using the Azure portal</span></span>
<span data-ttu-id="8aad0-104">Użyj witryny Azure Portal, aby utworzyć rejestr kontenerów i zarządzać jego ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="8aad0-104">Use the Azure portal to create a container registry and manage its settings.</span></span> <span data-ttu-id="8aad0-105">Tworzenie rejestrów kontenerów i zarządzanie nimi jest także możliwe przy użyciu [poleceń interfejsu wiersza polecenia platformy Azure w wersji 2.0](container-registry-get-started-azure-cli.md), programu [Azure PowerShell](container-registry-get-started-powershell.md) lub programowo przy użyciu [interfejsu API REST](https://go.microsoft.com/fwlink/p/?linkid=834376) usługi Container Registry.</span><span class="sxs-lookup"><span data-stu-id="8aad0-105">You can also create and manage container registries using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="8aad0-106">Podstawy oraz pojęcia zostały przedstawione w części [omówienie](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8aad0-106">For background and concepts, see [the overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="8aad0-107">Tworzenie rejestru kontenerów</span><span class="sxs-lookup"><span data-stu-id="8aad0-107">Create a container registry</span></span>
1. <span data-ttu-id="8aad0-108">W witrynie [Azure Portal](https://portal.azure.com) kliknij pozycję **+ Nowy**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-108">In the [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="8aad0-109">W portalu Marketplace wyszukaj hasło **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-109">Search the marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="8aad0-110">Wybierz pozycję **Azure Container Registry**, której wydawcą jest firma **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="8aad0-111">![Usługa Container Registry w portalu Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="8aad0-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="8aad0-112">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-112">Click **Create**.</span></span> <span data-ttu-id="8aad0-113">Zostanie wyświetlony blok usługi **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-113">The **Azure Container Registry** blade appears.</span></span>

    ![Ustawienia usługi Container Registry](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="8aad0-115">W bloku usługi **Azure Container Registry** wprowadź następujące informacje.</span><span class="sxs-lookup"><span data-stu-id="8aad0-115">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="8aad0-116">Po zakończeniu kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="8aad0-117">a.</span><span class="sxs-lookup"><span data-stu-id="8aad0-117">a.</span></span> <span data-ttu-id="8aad0-118">**Nazwa rejestru**: globalnie unikatowa nazwa domeny najwyższego poziomu dla określonego rejestru.</span><span class="sxs-lookup"><span data-stu-id="8aad0-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="8aad0-119">W tym przykładzie nazwa rejestru to *myRegistry01*, ale zastąp ją własną unikatową nazwą.</span><span class="sxs-lookup"><span data-stu-id="8aad0-119">In this example, the registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="8aad0-120">Nazwa może zawierać tylko litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="8aad0-120">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="8aad0-121">b.</span><span class="sxs-lookup"><span data-stu-id="8aad0-121">b.</span></span> <span data-ttu-id="8aad0-122">**Grupa zasobów**: wybierz istniejącą [grupę zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) lub wprowadź nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="8aad0-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="8aad0-123">c.</span><span class="sxs-lookup"><span data-stu-id="8aad0-123">c.</span></span> <span data-ttu-id="8aad0-124">**Lokalizacja**: wybierz taką lokalizację centrum danych Azure, gdzie usługa jest [dostępna](https://azure.microsoft.com/regions/services/), na przykład **Południowo-środkowe stany USA**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-124">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="8aad0-125">d.</span><span class="sxs-lookup"><span data-stu-id="8aad0-125">d.</span></span> <span data-ttu-id="8aad0-126">**Administrator**: jeśli chcesz, umożliw administratorowi dostęp do rejestru.</span><span class="sxs-lookup"><span data-stu-id="8aad0-126">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="8aad0-127">Po utworzeniu rejestru można zmienić to ustawienie.</span><span class="sxs-lookup"><span data-stu-id="8aad0-127">You can change this setting after creating the registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="8aad0-128">Oprócz zapewniania dostępu za pośrednictwem konta administratora rejestry kontenerów obsługują uwierzytelnianie wspierane przez nazwy główne usług w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8aad0-128">In addition to providing access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="8aad0-129">Więcej informacji i zagadnień do rozważenia znajduje się w temacie [Authenticate with a container registry](container-registry-authentication.md) (Uwierzytelnianie za pomocą rejestru kontenerów).</span><span class="sxs-lookup"><span data-stu-id="8aad0-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="8aad0-130">e.</span><span class="sxs-lookup"><span data-stu-id="8aad0-130">e.</span></span> <span data-ttu-id="8aad0-131">**Konto magazynu**: użyj ustawienia domyślnego, aby utworzyć [konto magazynu](../storage/common/storage-introduction.md), lub wybierz istniejące konto magazynu w tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="8aad0-131">**Storage account**: Use the default setting to create a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in the same location.</span></span> <span data-ttu-id="8aad0-132">Usługa Premium Storage nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="8aad0-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="8aad0-133">Zarządzanie ustawieniami rejestru</span><span class="sxs-lookup"><span data-stu-id="8aad0-133">Manage registry settings</span></span>
<span data-ttu-id="8aad0-134">Po utworzeniu rejestru znajdź ustawienia rejestru, uruchamiając blok **Rejestry kontenerów** w portalu.</span><span class="sxs-lookup"><span data-stu-id="8aad0-134">After creating the registry, find the registry settings by starting at the **Container Registries** blade in the portal.</span></span> <span data-ttu-id="8aad0-135">Ustawienia mogą być konieczne na przykład w celu zalogowania się do rejestru lub włączenia albo wyłączenia administratora.</span><span class="sxs-lookup"><span data-stu-id="8aad0-135">For example, you might need the settings to log in to your registry, or you might want to enable or disable the admin user.</span></span>

1. <span data-ttu-id="8aad0-136">W bloku **Rejestry kontenerów** kliknij nazwę swojego rejestru.</span><span class="sxs-lookup"><span data-stu-id="8aad0-136">On the **Container Registries** blade, click the name of your registry.</span></span>

    ![Blok rejestru kontenerów](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="8aad0-138">Aby zarządzać ustawieniami dostępu, kliknij pozycję **Klucz dostępu**.</span><span class="sxs-lookup"><span data-stu-id="8aad0-138">To manage access settings, click **Access key**.</span></span>

    ![Dostęp do rejestru kontenerów](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="8aad0-140">Zwróć uwagę na następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="8aad0-140">Note the following settings:</span></span>

   * <span data-ttu-id="8aad0-141">**Serwer logowania** — w pełni kwalifikowana nazwa służąca do logowania do rejestru.</span><span class="sxs-lookup"><span data-stu-id="8aad0-141">**Login server** - The fully qualified name you use to log in to the registry.</span></span> <span data-ttu-id="8aad0-142">W tym przykładzie jest to `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="8aad0-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="8aad0-143">**Administrator** — przełącznik umożliwiający włączenie lub wyłączenie konta administratora w rejestrze.</span><span class="sxs-lookup"><span data-stu-id="8aad0-143">**Admin user** - Toggle to enable or disable the registry's admin user account.</span></span>
   * <span data-ttu-id="8aad0-144">**Nazwa użytkownika** oraz **Hasło** — poświadczenia konta administratora (jeśli włączono) służące do logowania do rejestru.</span><span class="sxs-lookup"><span data-stu-id="8aad0-144">**Username** and **Password** - The credentials of the admin user account (if enabled) you can use to log in to the registry.</span></span> <span data-ttu-id="8aad0-145">Opcjonalnie można ponownie wygenerować hasła.</span><span class="sxs-lookup"><span data-stu-id="8aad0-145">You can optionally regenerate the passwords.</span></span> <span data-ttu-id="8aad0-146">Tworzone są dwa hasła, co umożliwia utrzymanie połączeń z rejestrem za pomocą jednego hasła, gdy ponownie generowane jest drugie hasło.</span><span class="sxs-lookup"><span data-stu-id="8aad0-146">Two passwords are created so that you can maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="8aad0-147">Aby zamiast tego przeprowadzić uwierzytelnianie za pomocą nazwy głównej usługi, zobacz [Authenticate with a private Docker container registry](container-registry-authentication.md) (Uwierzytelnianie przy użyciu prywatnego rejestru kontenerów platformy Docker).</span><span class="sxs-lookup"><span data-stu-id="8aad0-147">To authenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8aad0-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8aad0-148">Next steps</span></span>
* <span data-ttu-id="8aad0-149">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md) (Wypychanie pierwszego obrazu za pomocą interfejsu wiersza polecenia platformy Docker)</span><span class="sxs-lookup"><span data-stu-id="8aad0-149">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md)</span></span>
