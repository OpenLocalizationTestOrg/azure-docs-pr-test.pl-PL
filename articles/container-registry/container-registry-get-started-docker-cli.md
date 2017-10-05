---
title: Wypychanie obrazu platformy Docker do prywatnego rejestru platformy Azure | Microsoft Docs
description: "Wypychanie i ściąganie obrazów platformy Docker do prywatnego rejestru kontenerów na platformie Azure za pomocą interfejsu wiersza polecenia platformy Docker"
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
ms.openlocfilehash: 07d4d72e94eda02e8594dfddb0e911eb0e63012d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="push-your-first-image-to-a-private-docker-container-registry-using-the-docker-cli"></a><span data-ttu-id="5fb05-103">Wypchnij swój pierwszy obraz do prywatnego rejestru kontenerów platformy Docker za pomocą interfejsu wiersza polecenia platformy Docker</span><span class="sxs-lookup"><span data-stu-id="5fb05-103">Push your first image to a private Docker container registry using the Docker CLI</span></span>
<span data-ttu-id="5fb05-104">Rejestr kontenera platformy Azure przechowuje prywatne obrazy kontenerów platformy [Docker](http://hub.docker.com) i zarządza nimi podobnie, jak [koncentrator platformy Docker](https://hub.docker.com/) przechowuje publiczne obrazy platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="5fb05-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="5fb05-105">[Interfejsu wiersza polecenia platformy Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) możesz użyć do [logowania](https://docs.docker.com/engine/reference/commandline/login/), [wypychania](https://docs.docker.com/engine/reference/commandline/push/), [ściągania](https://docs.docker.com/engine/reference/commandline/pull/) oraz innych operacji na rejestrze kontenera.</span><span class="sxs-lookup"><span data-stu-id="5fb05-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="5fb05-106">Dalsze podstawy oraz pojęcia zostały przedstawione w części [ — omówienie](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="5fb05-106">For more background and concepts, see [the overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="5fb05-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5fb05-107">Prerequisites</span></span>
* <span data-ttu-id="5fb05-108">**Usługa Azure Container Registry** — Tworzy rejestr kontenera w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb05-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="5fb05-109">Na przykład użyj witryny [Azure Portal](container-registry-get-started-portal.md) lub [interfejsu wiersza polecenia platformy Azure w wersji 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5fb05-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="5fb05-110">**Interfejs wiersza polecenia platformy Docker** — Aby skonfigurować lokalny komputer jako hosta platformy Docker i uzyskać dostęp do poleceń interfejsu wiersza polecenia platformy Docker, zainstaluj [aparat platformy Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="5fb05-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-to-a-registry"></a><span data-ttu-id="5fb05-111">Zaloguj się do rejestru</span><span class="sxs-lookup"><span data-stu-id="5fb05-111">Log in to a registry</span></span>
<span data-ttu-id="5fb05-112">Uruchom `docker login`, aby zalogować się do rejestru kontenera za pomocą Twoich [poświadczeń rejestru](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5fb05-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="5fb05-113">Poniższy przykład przekazuje identyfikator i hasło [nazwy głównej usługi](../active-directory/active-directory-application-objects.md) Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5fb05-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="5fb05-114">Na przykład nazwę główną usługi można było przypisać do rejestru dla scenariusza automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="5fb05-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="5fb05-115">Pamiętaj o określeniu w pełni kwalifikowanej nazwy rejestru (wszystkie małe litery).</span><span class="sxs-lookup"><span data-stu-id="5fb05-115">Make sure to specify the fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="5fb05-116">W tym przykładzie jest to `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="5fb05-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-to-pull-and-push-an-image"></a><span data-ttu-id="5fb05-117">Kroki, aby ściągnąć i wypchnąć obraz</span><span class="sxs-lookup"><span data-stu-id="5fb05-117">Steps to pull and push an image</span></span>
<span data-ttu-id="5fb05-118">W poniższym przykładzie obraz Nginx jest pobierany z publicznego rejestru koncentratora platformy Docker, oznaczany dla prywatnego rejestru kontenera platformy Azure, wypychany do rejestru użytkownika, a następnie ściągany ponownie.</span><span class="sxs-lookup"><span data-stu-id="5fb05-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span></span>

<span data-ttu-id="5fb05-119">**1. Ściągnij oficjalny obraz platformy Docker dla kontenera Nginx**</span><span class="sxs-lookup"><span data-stu-id="5fb05-119">**1. Pull the Docker official image for Nginx**</span></span>

<span data-ttu-id="5fb05-120">Najpierw ściągnij publiczny obraz kontenera Nginx na swój komputer lokalny.</span><span class="sxs-lookup"><span data-stu-id="5fb05-120">First pull the public Nginx image to your local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="5fb05-121">**2. Uruchamianie kontenera Nginx**</span><span class="sxs-lookup"><span data-stu-id="5fb05-121">**2. Start the Nginx container**</span></span>

<span data-ttu-id="5fb05-122">Następujące polecenie interaktywnie uruchamia lokalny kontener Nginx na porcie 8080, umożliwiając wyświetlenie danych wyjściowych kontenera Nginx.</span><span class="sxs-lookup"><span data-stu-id="5fb05-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span></span> <span data-ttu-id="5fb05-123">Usuwa to działający kontener po zatrzymaniu.</span><span class="sxs-lookup"><span data-stu-id="5fb05-123">It removes the running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="5fb05-124">Przejdź do adresu [http://localhost:8080](http://localhost:8080), aby wyświetlić działający kontener.</span><span class="sxs-lookup"><span data-stu-id="5fb05-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span> <span data-ttu-id="5fb05-125">Zobaczysz ekran podobny do poniższego.</span><span class="sxs-lookup"><span data-stu-id="5fb05-125">You see a screen similar to the following one.</span></span>

![Kontener Nginx na komputerze lokalnym](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="5fb05-127">Aby zatrzymać działający kontener, naciśnij klawisze [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="5fb05-127">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="5fb05-128">**3. Tworzenie aliasu obrazu w rejestrze**</span><span class="sxs-lookup"><span data-stu-id="5fb05-128">**3. Create an alias of the image in your registry**</span></span>

<span data-ttu-id="5fb05-129">Następujące polecenie tworzy alias obrazu z w pełni kwalifikowaną ścieżką do Twojego rejestru.</span><span class="sxs-lookup"><span data-stu-id="5fb05-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="5fb05-130">W tym przykładzie jest określana przestrzeń nazw `samples`, aby uniknąć zaśmiecania katalogu głównego rejestru.</span><span class="sxs-lookup"><span data-stu-id="5fb05-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="5fb05-131">**4. Wypchnięcie obrazu do rejestru**</span><span class="sxs-lookup"><span data-stu-id="5fb05-131">**4. Push the image to your registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="5fb05-132">**5. Ściągnięcie obrazu z rejestru**</span><span class="sxs-lookup"><span data-stu-id="5fb05-132">**5. Pull the image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="5fb05-133">**6. Uruchamianie kontenera Nginx z rejestru**</span><span class="sxs-lookup"><span data-stu-id="5fb05-133">**6. Start the Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="5fb05-134">Przejdź do adresu [http://localhost:8080](http://localhost:8080), aby wyświetlić działający kontener.</span><span class="sxs-lookup"><span data-stu-id="5fb05-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span>

<span data-ttu-id="5fb05-135">Aby zatrzymać działający kontener, naciśnij klawisze [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="5fb05-135">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="5fb05-136">**7. (Opcjonalnie) Usuwanie obrazu**</span><span class="sxs-lookup"><span data-stu-id="5fb05-136">**7. (Optional) Remove the image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="5fb05-137">Limit procesów współbieżnych</span><span class="sxs-lookup"><span data-stu-id="5fb05-137">Concurrent Limits</span></span>
<span data-ttu-id="5fb05-138">W niektórych scenariuszach współbieżne wykonywanie wywołań może powodować błędy.</span><span class="sxs-lookup"><span data-stu-id="5fb05-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="5fb05-139">Poniższa tabela zawiera limity współbieżnych wywołań korzystających z operacji „wypychania” i „ściągania” na rejestrze kontenera platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="5fb05-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="5fb05-140">Operacja</span><span class="sxs-lookup"><span data-stu-id="5fb05-140">Operation</span></span>  | <span data-ttu-id="5fb05-141">Limit</span><span class="sxs-lookup"><span data-stu-id="5fb05-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="5fb05-142">ŚCIĄGANIE</span><span class="sxs-lookup"><span data-stu-id="5fb05-142">PULL</span></span>       | <span data-ttu-id="5fb05-143">Maksymalnie 10 współbieżnych operacji ściągania na rejestr</span><span class="sxs-lookup"><span data-stu-id="5fb05-143">Up to 10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="5fb05-144">WYPYCHANIE</span><span class="sxs-lookup"><span data-stu-id="5fb05-144">PUSH</span></span>       | <span data-ttu-id="5fb05-145">Maksymalnie 5 współbieżnych operacji wypychania na rejestr</span><span class="sxs-lookup"><span data-stu-id="5fb05-145">Up to 5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5fb05-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5fb05-146">Next steps</span></span>
<span data-ttu-id="5fb05-147">Teraz, kiedy znasz już podstawy, możesz zacząć korzystać z rejestru!</span><span class="sxs-lookup"><span data-stu-id="5fb05-147">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="5fb05-148">Na przykład rozpocznij wdrażanie obrazów kontenera do klastra usługi [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="5fb05-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
