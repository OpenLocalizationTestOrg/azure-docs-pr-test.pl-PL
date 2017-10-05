---
title: Repozytoria rejestru kontenera platformy Azure | Dokumentacja firmy Microsoft
description: "Jak używać repozytoria rejestru kontenera Azure obrazy usługi Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="e4f88-103">Repozytoria rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4f88-103">Azure container registry repositories</span></span>

<span data-ttu-id="e4f88-104">Rejestru kontenera platformy Azure umożliwia przechowywanie kontener obrazów w repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="e4f88-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="e4f88-105">Dzięki przechowywaniu obrazów w repozytoriów, może mieć grup obrazów (lub wersji obrazów) w izolowanym środowisku.</span><span class="sxs-lookup"><span data-stu-id="e4f88-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="e4f88-106">Można określić te repozytoria po naciśnięciu obrazów do rejestru.</span><span class="sxs-lookup"><span data-stu-id="e4f88-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e4f88-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e4f88-107">Prerequisites</span></span>
* <span data-ttu-id="e4f88-108">**Usługa Azure Container Registry** — Tworzy rejestr kontenera w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f88-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="e4f88-109">Na przykład użyj witryny [Azure Portal](container-registry-get-started-portal.md) lub [interfejsu wiersza polecenia platformy Azure w wersji 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e4f88-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="e4f88-110">**Interfejs wiersza polecenia platformy Docker** — Aby skonfigurować lokalny komputer jako hosta platformy Docker i uzyskać dostęp do poleceń interfejsu wiersza polecenia platformy Docker, zainstaluj [aparat platformy Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="e4f88-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="e4f88-111">**Ściąganie obrazu** — ściąganie obrazu z publicznego rejestru Centrum Docker tagu go i wypchnąć go do rejestru.</span><span class="sxs-lookup"><span data-stu-id="e4f88-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="e4f88-112">Aby uzyskać wskazówki dotyczące wypychania i ściągania obrazów, zobacz [obraz Docker wypychania do rejestru prywatnej Azure](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e4f88-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="e4f88-113">Wyświetlanie repozytoria w portalu</span><span class="sxs-lookup"><span data-stu-id="e4f88-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="e4f88-114">Gdy obrazy zostały przekazane do rejestru kontenera, można wyświetlić listę repozytoria hosting obrazów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f88-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="e4f88-115">Po wykonaniu kroków w [Push Docker obrazu do rejestru prywatnej Azure](container-registry-get-started-docker-cli.md) artykułu, po wykonaniu obrazu Nginx w rejestrze kontenera.</span><span class="sxs-lookup"><span data-stu-id="e4f88-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="e4f88-116">W ramach instrukcji należy określić przestrzeń nazw dla obrazu.</span><span class="sxs-lookup"><span data-stu-id="e4f88-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="e4f88-117">W poniższym przykładzie polecenie wypchnięcia obrazu NGinx w repozytorium "Przykłady":</span><span class="sxs-lookup"><span data-stu-id="e4f88-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="e4f88-118">Usługa Azure Container Registry obsługuje wielopoziomowe przestrzenie nazw repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="e4f88-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="e4f88-119">Ta funkcja pozwala na grupowanie kolekcji obrazów związanych z określoną aplikacją lub kolekcji aplikacji związanych z określonymi zespołami programistycznymi lub operacyjnymi.</span><span class="sxs-lookup"><span data-stu-id="e4f88-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="e4f88-120">Aby uzyskać więcej informacji na temat repozytoria w rejestrach kontenera, zobacz [rejestrów kontenera prywatnego Docker na platformie Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="e4f88-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="e4f88-121">Aby wyświetlić repozytoria rejestru kontenera:</span><span class="sxs-lookup"><span data-stu-id="e4f88-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="e4f88-122">Logowanie do witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e4f88-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="e4f88-123">Na **rejestru kontenera Azure** bloku, wybierz rejestru chcesz sprawdzić</span><span class="sxs-lookup"><span data-stu-id="e4f88-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="e4f88-124">W bloku rejestru kliknij **repozytoria** umożliwia wyświetlenie listy wszystkich repozytoria i obrazów</span><span class="sxs-lookup"><span data-stu-id="e4f88-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="e4f88-125">(Opcjonalnie) Wybierz określony obraz, aby zobaczyć tagów</span><span class="sxs-lookup"><span data-stu-id="e4f88-125">(Optional) Select a specific image to see tags</span></span>

![Repozytoria w portalu](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="e4f88-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4f88-127">Next steps</span></span>
<span data-ttu-id="e4f88-128">Teraz, kiedy znasz już podstawy, możesz zacząć korzystać z rejestru!</span><span class="sxs-lookup"><span data-stu-id="e4f88-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="e4f88-129">Na przykład rozpocznij wdrażanie obrazów kontenera do klastra usługi [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="e4f88-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
