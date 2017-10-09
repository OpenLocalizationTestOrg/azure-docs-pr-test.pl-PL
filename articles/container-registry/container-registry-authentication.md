---
title: aaaAuthenticate z rejestru kontenera platformy Azure | Dokumentacja firmy Microsoft
description: "Jak toolog tooan rejestru kontenera platformy Azure przy użyciu usługi Azure Active Directory usługi podmiot zabezpieczeń lub konto administratora"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="19c85-103">Uwierzytelniania za pomocą prywatnego rejestru kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="19c85-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="19c85-104">toowork z obrazami kontenera w rejestrze kontenera platformy Azure, możesz Zaloguj się za pomocą hello `docker login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="19c85-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="19c85-105">Możesz zalogować się przy użyciu  **[nazwy głównej usługi Azure Active Directory](../active-directory/active-directory-application-objects.md)**  specyficznych rejestru lub **konto administratora**.</span><span class="sxs-lookup"><span data-stu-id="19c85-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="19c85-106">Ten artykuł zawiera szczegółowe informacje o tych tożsamości.</span><span class="sxs-lookup"><span data-stu-id="19c85-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="19c85-107">Nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="19c85-107">Service principal</span></span>

<span data-ttu-id="19c85-108">Możesz [przypisać nazwy głównej usługi](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour rejestru i użyć jej do uwierzytelniania podstawowego Docker.</span><span class="sxs-lookup"><span data-stu-id="19c85-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="19c85-109">Przy użyciu nazwy głównej usługi jest zalecane w przypadku większości scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="19c85-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="19c85-110">Podaj identyfikator aplikacji hello i hasło toohello główna usługi hello `docker login` polecenia, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="19c85-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="19c85-111">Po zalogowaniu, Docker buforuje poświadczeń hello, więc nie trzeba identyfikator tooremember hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="19c85-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="19c85-112">Jeśli chcesz, można ponownie wygenerować hasła hello nazwy głównej usługi uruchamiając hello `az ad sp reset-credentials` polecenia.</span><span class="sxs-lookup"><span data-stu-id="19c85-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="19c85-113">Zezwalaj na nazwy główne usług [dostępu opartej na rolach](../active-directory/role-based-access-control-configure.md) tooa rejestru.</span><span class="sxs-lookup"><span data-stu-id="19c85-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="19c85-114">Dostępne role są:</span><span class="sxs-lookup"><span data-stu-id="19c85-114">Available roles are:</span></span>
  * <span data-ttu-id="19c85-115">Czytnik (dostęp tylko ściągania).</span><span class="sxs-lookup"><span data-stu-id="19c85-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="19c85-116">Współautor (ściągania i wypychania).</span><span class="sxs-lookup"><span data-stu-id="19c85-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="19c85-117">Właściciel (ściągania, wypychania i przypisz role tooother użytkowników).</span><span class="sxs-lookup"><span data-stu-id="19c85-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="19c85-118">Dostęp anonimowy nie jest dostępna w rejestrach kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="19c85-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="19c85-119">Obrazy publiczne można użyć [Centrum Docker](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="19c85-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="19c85-120">Można przypisać wiele podmiotów usługi rejestru tooa, dzięki czemu można toodefine dostępu dla różnych użytkowników lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="19c85-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="19c85-121">Nazwy główne usług również włączyć łączność "bezobsługowe" klucza rejestru tooa deweloperem lub DevOps scenariuszy, takich jak hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="19c85-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="19c85-122">Kontener wdrożenia z systemów tooorchestration rejestru, w tym DC/OS, Docker Swarm i Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="19c85-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="19c85-123">Można również umieścić toorelated rejestrów kontenera usług Azure takich jak [usługi kontenera](../container-service/index.yml), [usługi aplikacji](../app-service/index.md), [partii](../batch/index.md), [sieci szkieletowej usług](/azure/service-fabric/)i inne.</span><span class="sxs-lookup"><span data-stu-id="19c85-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="19c85-124">Ciągłej integracji i wdrażania rozwiązań (np. programu Visual Studio Team Services lub Wpięć) tworzące kontener obrazów i wypychanie ich tooa rejestru.</span><span class="sxs-lookup"><span data-stu-id="19c85-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="19c85-125">Konto administratora</span><span class="sxs-lookup"><span data-stu-id="19c85-125">Admin account</span></span>
<span data-ttu-id="19c85-126">Z każdym rejestru utworzone konto administratora pobiera tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="19c85-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="19c85-127">Domyślnie konto hello jest wyłączone, ale można ją włączyć i zarządzać nimi poświadczeń hello, na przykład za pomocą hello [portal](container-registry-get-started-portal.md#manage-registry-settings) lub przy użyciu hello [poleceń Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="19c85-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="19c85-128">Każde konto administratora jest udostępniane z dwóch haseł, które może być generowany ponownie.</span><span class="sxs-lookup"><span data-stu-id="19c85-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="19c85-129">dwa hasła Hello pozwalają toomaintain połączeń toohello rejestru za pomocą jednego hasła podczas ponownego generowania hello inne hasło.</span><span class="sxs-lookup"><span data-stu-id="19c85-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="19c85-130">Jeśli konto hello jest włączone, można przekazać hello nazwy użytkownika i toohello albo hasło `docker login` polecenia dla uwierzytelniania podstawowego toohello rejestru.</span><span class="sxs-lookup"><span data-stu-id="19c85-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="19c85-131">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="19c85-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="19c85-132">konto administratora Hello jest przeznaczony do rejestru hello tooaccess pojedynczego użytkownika, głównie do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="19c85-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="19c85-133">Nie jest zalecane poświadczeń konta administratora hello tooshare wśród innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="19c85-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="19c85-134">Wszyscy użytkownicy są wyświetlane jako rejestru toohello jednego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="19c85-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="19c85-135">Zmiana lub wyłączenie tego konta spowoduje wyłączenie dostępu do rejestru dla wszystkich użytkowników, którzy używają hello poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="19c85-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="19c85-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19c85-136">Next steps</span></span>
* <span data-ttu-id="19c85-137">[Wypychanie pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="19c85-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="19c85-138">Aby uzyskać więcej informacji na temat uwierzytelniania w wersji zapoznawczej rejestru kontenera hello Zobacz hello [wpis w blogu](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="19c85-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
