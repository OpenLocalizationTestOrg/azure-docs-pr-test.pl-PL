---
title: repozytoria rejestru kontenera aaaAzure | Dokumentacja firmy Microsoft
description: "Jak toouse magazynach rejestru kontenera Azure obrazy usługi Docker"
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
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="c62ed-103">Repozytoria rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c62ed-103">Azure container registry repositories</span></span>

<span data-ttu-id="c62ed-104">Rejestru kontenera platformy Azure pozwala toostore kontener obrazów w repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="c62ed-104">Azure container registry allows you toostore container images in repositories.</span></span> <span data-ttu-id="c62ed-105">Dzięki przechowywaniu obrazów w repozytoriów, może mieć grup obrazów (lub wersji obrazów) w izolowanym środowisku.</span><span class="sxs-lookup"><span data-stu-id="c62ed-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="c62ed-106">Po naciśnięciu rejestru tooyour obrazów, można określić te repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="c62ed-106">You can specify these repositories when you push images tooyour registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c62ed-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c62ed-107">Prerequisites</span></span>
* <span data-ttu-id="c62ed-108">**Usługa Azure Container Registry** — Tworzy rejestr kontenera w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c62ed-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="c62ed-109">Na przykład użyć hello [portalu Azure](container-registry-get-started-portal.md) lub hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c62ed-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="c62ed-110">**Interfejs wiersza polecenia docker** -tooset komputera lokalnego jako Docker dostępu i host hello Docker polecenia interfejsu wiersza polecenia, zainstaluj [aparatem platformy Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="c62ed-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="c62ed-111">**Ściąganie obrazu** — ściąganie obrazu z publicznego rejestru Centrum Docker hello tagu go i wypchnąć go tooyour rejestru.</span><span class="sxs-lookup"><span data-stu-id="c62ed-111">**Pull an image** - Pull an image from hello public Docker Hub registry, tag it, and push it tooyour registry.</span></span> <span data-ttu-id="c62ed-112">Aby uzyskać wskazówki dotyczące wypychania i ściągania obrazów, zobacz [Docker wypychania obrazu tooAzure prywatnej rejestru](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c62ed-112">For guidance on how push and pull images, see [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="c62ed-113">Wyświetlanie repozytoria w hello portalu</span><span class="sxs-lookup"><span data-stu-id="c62ed-113">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="c62ed-114">Po ma przypisany rejestru kontenera tooyour obrazów, można wyświetlić listę repozytoria hello hosting hello obrazów w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c62ed-114">Once you have pushed images tooyour container registry, you can see a list of hello repositories hosting hello images in hello Azure portal.</span></span>

<span data-ttu-id="c62ed-115">Po wykonaniu kroków hello hello [Push Docker obrazu tooAzure prywatnej rejestru](container-registry-get-started-docker-cli.md) artykułu, po wykonaniu obrazu Nginx w rejestrze kontenera.</span><span class="sxs-lookup"><span data-stu-id="c62ed-115">If you followed hello steps in hello [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="c62ed-116">W ramach instrukcji hello należy określić przestrzeń nazw dla obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="c62ed-116">As part of hello instructions, you should have specified a namespace for hello image.</span></span> <span data-ttu-id="c62ed-117">W poniższym przykładzie hello polecenie hello wypchnięcia hello NGinx obrazu toohello "Przykłady" repozytorium:</span><span class="sxs-lookup"><span data-stu-id="c62ed-117">In hello example below, hello command pushes hello NGinx image toohello "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="c62ed-118">Usługa Azure Container Registry obsługuje wielopoziomowe przestrzenie nazw repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="c62ed-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="c62ed-119">Ta funkcja umożliwia możesz toogroup kolekcje tooa powiązanych obrazy specyficzne dla aplikacji, lub zbiór aplikacji toospecific rozwoju lub zespołów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c62ed-119">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="c62ed-120">Zobacz tooread więcej informacji na temat repozytoria w rejestrach kontenera [rejestrów kontenera prywatnego Docker na platformie Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="c62ed-120">tooread more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="c62ed-121">repozytoria tooview hello kontenera rejestru:</span><span class="sxs-lookup"><span data-stu-id="c62ed-121">tooview hello container registry repositories:</span></span>

1. <span data-ttu-id="c62ed-122">Zaloguj się za toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c62ed-122">Log in toohello Azure portal</span></span>
2. <span data-ttu-id="c62ed-123">Na powitania **rejestru kontenera Azure** bloku, wybierz hello rejestru chcesz tooinspect</span><span class="sxs-lookup"><span data-stu-id="c62ed-123">On hello **Azure Container Registry** blade, select hello registry you wish tooinspect</span></span>
3. <span data-ttu-id="c62ed-124">W bloku rejestru powitania kliknij **repozytoria** toosee listę wszystkich repozytoriów hello i obrazów</span><span class="sxs-lookup"><span data-stu-id="c62ed-124">In hello registry blade, click **Repositories** toosee a list of all hello repositories and their images</span></span>
4. <span data-ttu-id="c62ed-125">(Opcjonalnie) Wybierz tagi toosee określonego obrazu</span><span class="sxs-lookup"><span data-stu-id="c62ed-125">(Optional) Select a specific image toosee tags</span></span>

![Repozytoria w portalu hello](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="c62ed-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c62ed-127">Next steps</span></span>
<span data-ttu-id="c62ed-128">Teraz znasz podstawy hello, wszystko jest gotowe toostart za pomocą rejestru!</span><span class="sxs-lookup"><span data-stu-id="c62ed-128">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="c62ed-129">Na przykład rozpocząć wdrażanie kontenera obrazy tooan [usługi kontenera platformy Azure](https://azure.microsoft.com/documentation/services/container-service/) klastra.</span><span class="sxs-lookup"><span data-stu-id="c62ed-129">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
