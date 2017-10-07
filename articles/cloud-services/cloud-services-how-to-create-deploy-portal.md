---
title: "aaaHow toocreate i wdrażania usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrażania usługi w chmurze przy użyciu hello portalu Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="4011a-103">Jak toocreate i wdrażania usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="4011a-103">How toocreate and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4011a-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4011a-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="4011a-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4011a-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="4011a-106">Witaj Azure portal udostępnia dwa sposoby dla Ciebie toocreate i wdrażania usługi w chmurze: *szybkie tworzenie* i *Utwórz niestandardowy*.</span><span class="sxs-lookup"><span data-stu-id="4011a-106">hello Azure portal provides two ways for you toocreate and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="4011a-107">W tym artykule opisano sposób toouse hello toocreate metody szybkie tworzenie nowej usługi w chmurze, a następnie użyj **przekazać** tooupload i wdrażanie pakietu usług chmury na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4011a-107">This article explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="4011a-108">Korzystając z tej metody, hello portalu Azure sprawia, że dostępne wygodne łącza ukończenia wszystkich wymagań w trakcie pracy.</span><span class="sxs-lookup"><span data-stu-id="4011a-108">When you use this method, hello Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="4011a-109">Jeśli wszystko jest gotowe toodeploy chmury usługi podczas jego tworzenia, możesz to zrobić zarówno na powitania tym samym czasie przy użyciu Utwórz niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="4011a-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="4011a-110">Jeśli planujesz toopublish usługi w chmurze z programu Visual Studio Team Services (VSTS), użyj szybkie tworzenie, a następnie skonfigurować publikowanie programu VSTS z hello Szybki Start Azure lub hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="4011a-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from hello Azure Quickstart or hello dashboard.</span></span> <span data-ttu-id="4011a-111">Aby uzyskać więcej informacji, zobacz [tooAzure ciągłego dostarczania przy użyciu programu Visual Studio Team Services][TFSTutorialForCloudService], lub można znaleźć w pomocy hello **Szybki Start** strony.</span><span class="sxs-lookup"><span data-stu-id="4011a-111">For more information, see [Continuous Delivery tooAzure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for hello **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="4011a-112">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="4011a-112">Concepts</span></span>
<span data-ttu-id="4011a-113">Trzy składniki są wymagane toodeploy aplikacji jako usługa w chmurze na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="4011a-113">Three components are required toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="4011a-114">**Definicja usługi**</span><span class="sxs-lookup"><span data-stu-id="4011a-114">**Service Definition**</span></span>  
  <span data-ttu-id="4011a-115">Witaj chmury pliku definicji usługi (csdef) definiuje hello usługi modelu, w tym hello liczba ról.</span><span class="sxs-lookup"><span data-stu-id="4011a-115">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="4011a-116">**Konfiguracja usługi**</span><span class="sxs-lookup"><span data-stu-id="4011a-116">**Service Configuration**</span></span>  
  <span data-ttu-id="4011a-117">plik konfiguracji usługi chmury Hello (cscfg) zawiera ustawienia konfiguracji dla usługi w chmurze hello i poszczególne role, w tym hello liczby wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="4011a-117">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="4011a-118">**Pakiet usługi**</span><span class="sxs-lookup"><span data-stu-id="4011a-118">**Service Package**</span></span>  
  <span data-ttu-id="4011a-119">pakiet usługi Hello (cspkg) zawiera kod aplikacji hello i konfiguracji i pliku definicji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="4011a-119">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="4011a-120">Dowiedz się więcej na temat tych i w jaki sposób toocreate pakietu [tutaj](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="4011a-120">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="4011a-121">Przygotowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="4011a-121">Prepare your app</span></span>
<span data-ttu-id="4011a-122">Przed wdrożeniem usługi w chmurze, należy utworzyć pakiet usługi chmury hello (cspkg) w kodzie aplikacji i pliku konfiguracji usługi chmury (cscfg).</span><span class="sxs-lookup"><span data-stu-id="4011a-122">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="4011a-123">Hello Azure SDK zawiera narzędzia do przygotowania te pliki wymagane wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="4011a-123">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="4011a-124">Witaj zestawu SDK można zainstalować z hello [Azure pobiera](https://azure.microsoft.com/downloads/) strony w języku hello, w którym chcesz toodevelop kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4011a-124">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="4011a-125">Trzy funkcje usługi chmury wymagają specjalnych konfiguracji przed wyeksportowaniem pakietu usług:</span><span class="sxs-lookup"><span data-stu-id="4011a-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="4011a-126">Jeśli chcesz, aby usługa w chmurze, która używa protokołu Secure Sockets Layer (SSL) do szyfrowania danych toodeploy [konfigurowania aplikacji](cloud-services-configure-ssl-certificate-portal.md#modify) dla protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="4011a-126">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="4011a-127">Jeśli chcesz, aby tooconfigure wystąpień toorole połączeń usług pulpitu zdalnego, [konfigurowania ról hello](cloud-services-role-enable-remote-desktop-new-portal.md) dla pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="4011a-127">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="4011a-128">Tooconfigure pełne, monitorowanie dla usługi w chmurze, należy włączyć diagnostyki Azure dla usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="4011a-128">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="4011a-129">*Monitorowanie minimalnego* (domyślnie hello monitorowania poziomu) używa liczniki wydajności zebrane z hello systemy operacyjne hosta dla wystąpień roli (maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="4011a-129">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="4011a-130">*Monitorowanie pełne* zbiera dodatkowe metryki na podstawie danych wydajności w ramach hello roli wystąpień tooenable bliżej analizy problemy występujące podczas przetwarzania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4011a-130">*Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="4011a-131">toofind się, jak tooenable diagnostyki Azure, zobacz [Włączanie diagnostyki na platformie Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="4011a-131">toofind out how tooenable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="4011a-132">toocreate usługi w chmurze z wdrożeniami role sieci web lub roli proces roboczy musi [Utwórz pakiet usługi hello](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="4011a-132">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4011a-133">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="4011a-133">Before you begin</span></span>
* <span data-ttu-id="4011a-134">Nie zainstalowano hello Azure SDK, kliknij przycisk **Zainstaluj zestaw Azure SDK** tooopen hello [Azure pobiera strony](https://azure.microsoft.com/downloads/), a następnie pobrać hello zestawu SDK dla języka hello, w którym chcesz toodevelop kodu.</span><span class="sxs-lookup"><span data-stu-id="4011a-134">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="4011a-135">(Należy toodo możliwości to później.)</span><span class="sxs-lookup"><span data-stu-id="4011a-135">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="4011a-136">Jeśli wszystkie wystąpienia roli jest wymagany certyfikat, należy utworzyć hello certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="4011a-136">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="4011a-137">Usługi w chmurze wymagają pliku pfx z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="4011a-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="4011a-138">Podczas tworzenia i wdrażania usługi w chmurze hello możesz przekazać hello tooAzure certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="4011a-138">You can upload hello certificates tooAzure as you create and deploy hello cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="4011a-139">Tworzenie i wdrażanie</span><span class="sxs-lookup"><span data-stu-id="4011a-139">Create and deploy</span></span>
1. <span data-ttu-id="4011a-140">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4011a-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4011a-141">Kliknij przycisk **nowy > obliczeniowe**, a następnie przewiń w dół kliknij tooand **usługi w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="4011a-141">Click **New > Compute**, and then scroll down tooand click **Cloud Service**.</span></span>

    ![Publikowanie usługi w chmurze](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="4011a-143">W nowych hello **usługi w chmurze** bloku, wprowadź wartość dla hello **nazwy DNS**.</span><span class="sxs-lookup"><span data-stu-id="4011a-143">In hello new **Cloud Service** blade, enter a value for hello **DNS name**.</span></span>
4. <span data-ttu-id="4011a-144">Utwórz nową **grupy zasobów** lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="4011a-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="4011a-145">Wybierz **lokalizację**.</span><span class="sxs-lookup"><span data-stu-id="4011a-145">Select a **Location**.</span></span>
6. <span data-ttu-id="4011a-146">Kliknij przycisk **pakietu**.</span><span class="sxs-lookup"><span data-stu-id="4011a-146">Click **Package**.</span></span> <span data-ttu-id="4011a-147">Spowoduje to otwarcie hello **przekazania pakietu** bloku.</span><span class="sxs-lookup"><span data-stu-id="4011a-147">This will open hello **Upload a package** blade.</span></span> <span data-ttu-id="4011a-148">Wypełnij pola hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="4011a-148">Fill in hello required fields.</span></span> <span data-ttu-id="4011a-149">Jeśli jakieś role zawierają pojedynczego wystąpienia, upewnij się, **Wdróż, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="4011a-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="4011a-150">Upewnij się, że **rozpocząć wdrażanie** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="4011a-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="4011a-151">Kliknij przycisk **OK** którego zostanie zamknięte hello **przekazania pakietu** bloku.</span><span class="sxs-lookup"><span data-stu-id="4011a-151">Click **OK** which will close hello **Upload a package** blade.</span></span>
9. <span data-ttu-id="4011a-152">Jeśli nie masz żadnych tooadd certyfikatów, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4011a-152">If you do not have any certificates tooadd, click **Create**.</span></span>

    ![Publikowanie usługi w chmurze](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="4011a-154">Przekaż certyfikat</span><span class="sxs-lookup"><span data-stu-id="4011a-154">Upload a certificate</span></span>
<span data-ttu-id="4011a-155">Jeśli pakiet wdrażania [skonfigurowanych certyfikatów toouse](cloud-services-configure-ssl-certificate-portal.md#modify), możesz teraz przekazać hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="4011a-155">If your deployment package was [configured toouse certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload hello certificate now.</span></span>

1. <span data-ttu-id="4011a-156">Wybierz **certyfikaty**, a na powitania **Dodaj certyfikaty** bloku, wybierz plik .pfx certyfikatu SSL hello, a następnie podaj hello **hasło** certyfikatu hello</span><span class="sxs-lookup"><span data-stu-id="4011a-156">Select **Certificates**, and on hello **Add certificates** blade, select hello SSL certificate .pfx file, and then provide hello **Password** for hello certificate,</span></span>
2. <span data-ttu-id="4011a-157">Kliknij przycisk **certyfikatu Attach**, a następnie kliknij przycisk **OK** na powitania **Dodaj certyfikaty** bloku.</span><span class="sxs-lookup"><span data-stu-id="4011a-157">Click **Attach certificate**, and then click **OK** on hello **Add certificates** blade.</span></span>
3. <span data-ttu-id="4011a-158">Kliknij przycisk **Utwórz** na powitania **usługi w chmurze** bloku.</span><span class="sxs-lookup"><span data-stu-id="4011a-158">Click **Create** on hello **Cloud Service** blade.</span></span> <span data-ttu-id="4011a-159">Podczas wdrażania hello osiągnęła hello **gotowe** stanu, możesz przejść toohello następne kroki.</span><span class="sxs-lookup"><span data-stu-id="4011a-159">When hello deployment has reached hello **Ready** status, you can proceed toohello next steps.</span></span>

    ![Publikowanie usługi w chmurze](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="4011a-161">Sprawdź wdrożenia ukończone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="4011a-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="4011a-162">Kliknij przycisk wystąpienie usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="4011a-162">Click hello cloud service instance.</span></span>

    <span data-ttu-id="4011a-163">Witaj stan powinien pokazują, że usługa hello jest **systemem**.</span><span class="sxs-lookup"><span data-stu-id="4011a-163">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="4011a-164">W obszarze **Essentials**, kliknij przycisk hello **adres URL witryny** tooopen usługi chmury w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="4011a-164">Under **Essentials**, click hello **Site URL** tooopen your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="4011a-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4011a-166">Next steps</span></span>
* <span data-ttu-id="4011a-167">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4011a-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="4011a-168">Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4011a-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="4011a-169">[Usługi w chmurze zarządzanie](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4011a-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="4011a-170">Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4011a-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
