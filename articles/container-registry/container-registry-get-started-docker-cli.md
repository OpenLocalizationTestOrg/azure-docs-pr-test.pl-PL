---
title: aaaPush Docker obrazu tooprivate rejestru Azure | Dokumentacja firmy Microsoft
description: "I wypychania Docker rejestru kontener prywatnego tooa obrazów na platformie Azure przy użyciu interfejsu wiersza polecenia Docker hello"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="c4167-103">Pierwszy obraz tooa prywatnej Docker kontenera rejestr przy użyciu interfejsu wiersza polecenia Docker hello push</span><span class="sxs-lookup"><span data-stu-id="c4167-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="c4167-104">Rejestru kontenera platformy Azure przechowywanych i zarządzanych prywatnej [Docker](http://hub.docker.com) kontener obrazów, podobne toohello sposób [Centrum Docker](https://hub.docker.com/) przechowuje publiczny obrazy usługi Docker.</span><span class="sxs-lookup"><span data-stu-id="c4167-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="c4167-105">Użyj hello [interfejsu wiersza polecenia Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) dla [logowania](https://docs.docker.com/engine/reference/commandline/login/), [wypychania](https://docs.docker.com/engine/reference/commandline/push/), [ściągania](https://docs.docker.com/engine/reference/commandline/pull/)i inne operacje dotyczące Twojej kontenera rejestr.</span><span class="sxs-lookup"><span data-stu-id="c4167-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="c4167-106">Więcej tła i pojęć, zobacz [hello — omówienie](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c4167-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="c4167-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c4167-107">Prerequisites</span></span>
* <span data-ttu-id="c4167-108">**Usługa Azure Container Registry** — Tworzy rejestr kontenera w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c4167-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="c4167-109">Na przykład użyć hello [portalu Azure](container-registry-get-started-portal.md) lub hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c4167-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="c4167-110">**Interfejs wiersza polecenia docker** -tooset komputera lokalnego jako Docker dostępu i host hello Docker polecenia interfejsu wiersza polecenia, zainstaluj [aparatem platformy Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="c4167-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="c4167-111">Zaloguj się w rejestrze tooa</span><span class="sxs-lookup"><span data-stu-id="c4167-111">Log in tooa registry</span></span>
<span data-ttu-id="c4167-112">Uruchom `docker login` toolog w rejestrze kontenera tooyour z Twojej [poświadczenia rejestru](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c4167-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="c4167-113">Witaj w poniższym przykładzie przekazuje hello Identyfikatora i hasła usługi Azure Active Directory [nazwy głównej usługi](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="c4167-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="c4167-114">Na przykład może przypisano rejestr tooyour główna usługi scenariusz automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="c4167-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="c4167-115">Upewnij się, że toospecify hello rejestru w pełni kwalifikowaną nazwę (tylko małe litery).</span><span class="sxs-lookup"><span data-stu-id="c4167-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="c4167-116">W tym przykładzie jest to `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="c4167-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="c4167-117">Kroki toopull i wypychania obrazu</span><span class="sxs-lookup"><span data-stu-id="c4167-117">Steps toopull and push an image</span></span>
<span data-ttu-id="c4167-118">Witaj wykonaj przykładowe, pliki do pobrania hello Nginx obrazu z publicznego rejestru Centrum Docker hello tagi go do rejestru prywatnej kontenera platformy Azure, wypchnięcia jej tooyour rejestru, a następnie pobiera go ponownie.</span><span class="sxs-lookup"><span data-stu-id="c4167-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="c4167-119">**1. Ściąganie hello Docker oficjalnego obrazu dla Nginx**</span><span class="sxs-lookup"><span data-stu-id="c4167-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="c4167-120">Pierwszy ściągania hello publicznego Nginx obrazu tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c4167-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="c4167-121">**2. Kontener Nginx hello Start**</span><span class="sxs-lookup"><span data-stu-id="c4167-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="c4167-122">Witaj następujące polecenie uruchamia kontener Nginx lokalne powitania interaktywnie portu 8080, dzięki czemu dane wyjściowe toosee Nginx.</span><span class="sxs-lookup"><span data-stu-id="c4167-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="c4167-123">Usuwa hello systemem kontenera raz zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="c4167-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="c4167-124">Przeglądaj zbyt[adresem http://localhost: 8080](http://localhost:8080) hello tooview systemem kontenera.</span><span class="sxs-lookup"><span data-stu-id="c4167-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="c4167-125">Zostanie wyświetlony ekran toohello podobne, po jednym.</span><span class="sxs-lookup"><span data-stu-id="c4167-125">You see a screen similar toohello following one.</span></span>

![Kontener Nginx na komputerze lokalnym](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="c4167-127">toostop hello uruchomionych kontenera, naciśnij klawisz [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="c4167-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="c4167-128">**3. Utwórz alias obraz powitania w rejestrze**</span><span class="sxs-lookup"><span data-stu-id="c4167-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="c4167-129">Witaj następujące polecenie tworzy alias obrazu hello z rejestru tooyour pełną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="c4167-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="c4167-130">W tym przykładzie określa hello `samples` bałaganu tooavoid przestrzeni nazw w głównym hello hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="c4167-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="c4167-131">**4. Wypychanie hello obrazu tooyour rejestru**</span><span class="sxs-lookup"><span data-stu-id="c4167-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="c4167-132">**5. Obraz powitania ściągnięcia z rejestru**</span><span class="sxs-lookup"><span data-stu-id="c4167-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="c4167-133">**6. Uruchom kontener Nginx hello z rejestru**</span><span class="sxs-lookup"><span data-stu-id="c4167-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="c4167-134">Przeglądaj zbyt[adresem http://localhost: 8080](http://localhost:8080) hello tooview systemem kontenera.</span><span class="sxs-lookup"><span data-stu-id="c4167-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="c4167-135">toostop hello uruchomionych kontenera, naciśnij klawisz [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="c4167-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="c4167-136">**7. (Opcjonalnie) Usuń obraz powitania**</span><span class="sxs-lookup"><span data-stu-id="c4167-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="c4167-137">Limit procesów współbieżnych</span><span class="sxs-lookup"><span data-stu-id="c4167-137">Concurrent Limits</span></span>
<span data-ttu-id="c4167-138">W niektórych scenariuszach współbieżne wykonywanie wywołań może powodować błędy.</span><span class="sxs-lookup"><span data-stu-id="c4167-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="c4167-139">w poniższej tabeli Hello zawiera hello limity jednoczesnych połączeń z operacji "Push" i "Pull" na rejestru kontenera platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="c4167-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="c4167-140">Operacja</span><span class="sxs-lookup"><span data-stu-id="c4167-140">Operation</span></span>  | <span data-ttu-id="c4167-141">Limit</span><span class="sxs-lookup"><span data-stu-id="c4167-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="c4167-142">ŚCIĄGANIE</span><span class="sxs-lookup"><span data-stu-id="c4167-142">PULL</span></span>       | <span data-ttu-id="c4167-143">Zapasowej too10 równoczesnych ściąga na rejestru</span><span class="sxs-lookup"><span data-stu-id="c4167-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="c4167-144">WYPYCHANIE</span><span class="sxs-lookup"><span data-stu-id="c4167-144">PUSH</span></span>       | <span data-ttu-id="c4167-145">Zapasowej too5 równoczesnych wypchnięcia na rejestru</span><span class="sxs-lookup"><span data-stu-id="c4167-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c4167-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4167-146">Next steps</span></span>
<span data-ttu-id="c4167-147">Teraz znasz podstawy hello, wszystko jest gotowe toostart za pomocą rejestru!</span><span class="sxs-lookup"><span data-stu-id="c4167-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="c4167-148">Na przykład rozpocząć wdrażanie kontenera obrazy tooan [usługi kontenera platformy Azure](https://azure.microsoft.com/documentation/services/container-service/) klastra.</span><span class="sxs-lookup"><span data-stu-id="c4167-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
