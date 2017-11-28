---
title: "Uwierzytelniania za pomocą rejestru kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak zalogować się do rejestru kontenera platformy Azure przy użyciu nazwy głównej usługi Azure Active Directory lub konto administratora"
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
ms.openlocfilehash: aa2a6bf3d7d9ec22020036851fc0f2bca37e31bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="82f54-103">Uwierzytelniania za pomocą prywatnego rejestru kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="82f54-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="82f54-104">Aby pracować z kontenera obrazów w rejestrze kontenera platformy Azure, możesz Zaloguj się za pomocą `docker login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="82f54-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span></span> <span data-ttu-id="82f54-105">Możesz zalogować się przy użyciu  **[nazwy głównej usługi Azure Active Directory](../active-directory/active-directory-application-objects.md)**  specyficznych rejestru lub **konto administratora**.</span><span class="sxs-lookup"><span data-stu-id="82f54-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="82f54-106">Ten artykuł zawiera szczegółowe informacje o tych tożsamości.</span><span class="sxs-lookup"><span data-stu-id="82f54-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="82f54-107">Nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="82f54-107">Service principal</span></span>

<span data-ttu-id="82f54-108">Możesz [przypisać nazwy głównej usługi](container-registry-get-started-azure-cli.md#assign-a-service-principal) do rejestru i użyć jej do uwierzytelniania podstawowego Docker.</span><span class="sxs-lookup"><span data-stu-id="82f54-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="82f54-109">Przy użyciu nazwy głównej usługi jest zalecane w przypadku większości scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="82f54-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="82f54-110">Podaj identyfikator aplikacji i hasło do głównej usługi `docker login` polecenia, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="82f54-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="82f54-111">Po zalogowaniu, Docker buforuje poświadczeń, więc nie trzeba pamiętać identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="82f54-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

> [!TIP]
> <span data-ttu-id="82f54-112">Jeśli chcesz, możesz ponownie wygenerować hasła nazwy głównej usługi, uruchamiając `az ad sp reset-credentials` polecenia.</span><span class="sxs-lookup"><span data-stu-id="82f54-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="82f54-113">Zezwalaj na nazwy główne usług [dostępu opartej na rolach](../active-directory/role-based-access-control-configure.md) rejestru.</span><span class="sxs-lookup"><span data-stu-id="82f54-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span></span> <span data-ttu-id="82f54-114">Dostępne role są:</span><span class="sxs-lookup"><span data-stu-id="82f54-114">Available roles are:</span></span>
  * <span data-ttu-id="82f54-115">Czytnik (dostęp tylko ściągania).</span><span class="sxs-lookup"><span data-stu-id="82f54-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="82f54-116">Współautor (ściągania i wypychania).</span><span class="sxs-lookup"><span data-stu-id="82f54-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="82f54-117">Właściciel (ściągania, wypychania i przypisz role do innych użytkowników).</span><span class="sxs-lookup"><span data-stu-id="82f54-117">Owner (pull, push, and assign roles to other users).</span></span>

<span data-ttu-id="82f54-118">Dostęp anonimowy nie jest dostępna w rejestrach kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="82f54-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="82f54-119">Obrazy publiczne można użyć [Centrum Docker](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="82f54-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="82f54-120">Wiele podmiotów usługi można przypisać do rejestru, w którym można zdefiniować dostęp dla różnych użytkowników lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="82f54-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span></span> <span data-ttu-id="82f54-121">Nazwy główne usług również umożliwić "bezobsługowe" łączność z rejestru developer lub DevOps scenariuszy, takich jak następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="82f54-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span></span>

  * <span data-ttu-id="82f54-122">Kontener wdrożenia z rejestru systemy orchestration, w tym DC/OS, Docker Swarm i Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="82f54-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="82f54-123">Można również pobierać kontenera rejestrów powiązane usługi Azure takich jak [usługi kontenera](../container-service/index.yml), [usługi aplikacji](../app-service/index.md), [partii](../batch/index.md), [sieci szkieletowej usług](/azure/service-fabric/)i inne.</span><span class="sxs-lookup"><span data-stu-id="82f54-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="82f54-124">Ciągłej integracji i wdrażania rozwiązań (np. programu Visual Studio Team Services lub Wpięć) tworzące kontener obrazów i wypychanie ich do rejestru.</span><span class="sxs-lookup"><span data-stu-id="82f54-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="82f54-125">Konto administratora</span><span class="sxs-lookup"><span data-stu-id="82f54-125">Admin account</span></span>
<span data-ttu-id="82f54-126">Z każdym rejestru utworzone konto administratora pobiera tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="82f54-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="82f54-127">Domyślnie konto jest wyłączone, ale można ją włączyć i zarządzać poświadczenia, na przykład za pomocą [portal](container-registry-get-started-portal.md#manage-registry-settings) lub przy użyciu [poleceń Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="82f54-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="82f54-128">Każde konto administratora jest udostępniane z dwóch haseł, które może być generowany ponownie.</span><span class="sxs-lookup"><span data-stu-id="82f54-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="82f54-129">Dwa hasła umożliwiają zachowanie połączenia w rejestrze za pomocą jednego hasła podczas ponownego generowania inne hasło.</span><span class="sxs-lookup"><span data-stu-id="82f54-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="82f54-130">Jeśli konto jest włączone, można przekazać nazwę użytkownika i hasło albo `docker login` polecenia dla uwierzytelniania podstawowego w rejestrze.</span><span class="sxs-lookup"><span data-stu-id="82f54-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="82f54-131">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="82f54-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="82f54-132">Konto administratora jest przeznaczony dla jednego użytkownika do dostępu do rejestru, głównie do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="82f54-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span></span> <span data-ttu-id="82f54-133">Nie zaleca się udostępniania poświadczeń konta administratora wśród innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="82f54-133">It is not recommended to share the admin account credentials among other users.</span></span> <span data-ttu-id="82f54-134">Wszyscy użytkownicy są wyświetlane jako pojedynczego użytkownika w rejestrze.</span><span class="sxs-lookup"><span data-stu-id="82f54-134">All users appear as a single user to the registry.</span></span> <span data-ttu-id="82f54-135">Zmiana lub wyłączenie tego konta spowoduje wyłączenie dostępu do rejestru dla wszystkich użytkowników, którzy korzystają z poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="82f54-135">Changing or disabling this account disables registry access for all users who use the credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="82f54-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82f54-136">Next steps</span></span>
* <span data-ttu-id="82f54-137">[Wypychanie pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="82f54-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="82f54-138">Aby uzyskać więcej informacji o uwierzytelnianiu w wersji zapoznawczej rejestru kontenera, zobacz [wpis w blogu](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="82f54-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
