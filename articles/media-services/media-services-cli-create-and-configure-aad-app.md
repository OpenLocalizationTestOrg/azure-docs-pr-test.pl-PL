---
title: "toocreate aaaUse 2.0 interfejsu wiersza polecenia aplikacji usługi Azure AD i skonfiguruj ją tooaccess interfejsu API usługi Azure Media Services | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób toocreate toouse 2.0 interfejsu wiersza polecenia aplikacji usługi Azure AD i skonfiguruj ją tooaccess interfejsu API usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a><span data-ttu-id="0d1be-103">Użyj toocreate 2.0 interfejsu wiersza polecenia aplikacji AAD i skonfiguruj go tooaccess interfejsu API usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="0d1be-103">Use CLI 2.0 toocreate an AAD app and configure it tooaccess Azure Media Services API</span></span>

<span data-ttu-id="0d1be-104">W tym temacie pokazano, jak toocreate toouse 2.0 interfejsu wiersza polecenia aplikacji usługi Azure Active Directory (Azure AD) i tooaccess główną usługi Azure Media Services zasobów.</span><span class="sxs-lookup"><span data-stu-id="0d1be-104">This topic shows you how toouse CLI 2.0 toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0d1be-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0d1be-105">Prerequisites</span></span>

- <span data-ttu-id="0d1be-106">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d1be-106">An Azure account.</span></span> <span data-ttu-id="0d1be-107">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d1be-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="0d1be-108">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="0d1be-108">A Media Services account.</span></span> <span data-ttu-id="0d1be-109">Aby uzyskać więcej informacji, zobacz [Tworzenie konta usługi Azure Media Services przy użyciu portalu Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="0d1be-109">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-hello-azure-cloud-shell"></a><span data-ttu-id="0d1be-110">Użyj hello powłoki chmury Azure</span><span class="sxs-lookup"><span data-stu-id="0d1be-110">Use hello Azure Cloud Shell</span></span>

1. <span data-ttu-id="0d1be-111">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0d1be-111">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0d1be-112">Uruchom program hello powłoki chmury z hello górnym okienku nawigacji portalu hello.</span><span class="sxs-lookup"><span data-stu-id="0d1be-112">Launch hello Cloud Shell from hello upper navigation pane of hello portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="0d1be-114">Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Cloud powłoki](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="0d1be-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a><span data-ttu-id="0d1be-115">Utwórz aplikację usługi Azure AD i skonfiguruj dostęp do konta usługi media toohello 2.0 interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="0d1be-115">Create an Azure AD app and configure access toohello media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="0d1be-116">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0d1be-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="0d1be-117">W tym przykładzie hello **zakres** jest ścieżką wszystkich zasobów hello nośnika hello konta usługi.</span><span class="sxs-lookup"><span data-stu-id="0d1be-117">In this example, hello **scope** is hello full resource path for hello media services account.</span></span> <span data-ttu-id="0d1be-118">Jednak hello **zakres** może być dowolnym poziomie.</span><span class="sxs-lookup"><span data-stu-id="0d1be-118">However, hello **scope** can be at any level.</span></span>

<span data-ttu-id="0d1be-119">Może to być na przykład jeden z następujących poziomów hello:</span><span class="sxs-lookup"><span data-stu-id="0d1be-119">For example, it could be one of hello following levels:</span></span>
 
* <span data-ttu-id="0d1be-120">Witaj **subskrypcji** poziom.</span><span class="sxs-lookup"><span data-stu-id="0d1be-120">hello **subscription** level.</span></span>
* <span data-ttu-id="0d1be-121">Witaj **grupy zasobów** poziom.</span><span class="sxs-lookup"><span data-stu-id="0d1be-121">hello **resource group** level.</span></span>
* <span data-ttu-id="0d1be-122">Witaj **zasobów** poziom (na przykład konto nośnika).</span><span class="sxs-lookup"><span data-stu-id="0d1be-122">hello **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="0d1be-123">Aby uzyskać więcej informacji, zobacz [Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="0d1be-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="0d1be-124">Zobacz też [Manage Role-Based kontrola dostępu przy użyciu interfejsu wiersza polecenia platformy Azure hello](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0d1be-124">Also see [Manage Role-Based Access Control with hello Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0d1be-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d1be-125">Next steps</span></span>

<span data-ttu-id="0d1be-126">Rozpoczynanie pracy z [przekazywania plików konta tooyour](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="0d1be-126">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
