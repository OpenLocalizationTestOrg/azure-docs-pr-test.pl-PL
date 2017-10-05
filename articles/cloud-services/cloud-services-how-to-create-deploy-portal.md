---
title: "Jak utworzyć i wdrożyć usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia i wdrażania usługi w chmurze przy użyciu portalu Azure."
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
ms.openlocfilehash: e5ce666f1d826c7901c9fd5e7fafe6171139c3ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="d4f3e-103">Jak utworzyć i wdrożyć usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="d4f3e-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4f3e-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d4f3e-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="d4f3e-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d4f3e-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="d4f3e-106">Azure portal udostępnia dwa sposoby tworzenia i wdrażania usługi w chmurze: *szybkie tworzenie* i *Utwórz niestandardowy*.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="d4f3e-107">W tym artykule wyjaśniono, jak utworzyć nową usługę w chmurze, a następnie użyj przy użyciu metody szybkie tworzenie **przekazać** Aby przekazać i wdrożyć pakiet usługi chmury na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="d4f3e-108">Korzystając z tej metody, portalu Azure sprawia, że dostępne wygodne łącza ukończenia wszystkich wymagań w trakcie pracy.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="d4f3e-109">Jeśli wszystko jest gotowe do wdrożenia usługi w chmurze podczas jego tworzenia, możesz to zrobić zarówno w tym samym czasie przy użyciu Utwórz niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="d4f3e-110">Jeśli planujesz opublikować usługi w chmurze z programu Visual Studio Team Services (VSTS), użyj szybkiego tworzenia, a następnie skonfiguruj publikowanie programu VSTS z Szybki Start Azure lub do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard.</span></span> <span data-ttu-id="d4f3e-111">Aby uzyskać więcej informacji, zobacz [ciągłego dostarczania danych do platformy Azure przy użyciu programu Visual Studio Team Services][TFSTutorialForCloudService], lub można znaleźć w Pomocy **Szybki Start** strony.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="d4f3e-112">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="d4f3e-112">Concepts</span></span>
<span data-ttu-id="d4f3e-113">Trzy składniki są wymagane do wdrażania aplikacji jako usługa w chmurze na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="d4f3e-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="d4f3e-114">**Definicja usługi**</span><span class="sxs-lookup"><span data-stu-id="d4f3e-114">**Service Definition**</span></span>  
  <span data-ttu-id="d4f3e-115">Chmura pliku definicji usługi (csdef) definiuje modelu usługi, w tym liczba ról.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="d4f3e-116">**Konfiguracja usługi**</span><span class="sxs-lookup"><span data-stu-id="d4f3e-116">**Service Configuration**</span></span>  
  <span data-ttu-id="d4f3e-117">Plik konfiguracji usługi chmury (cscfg) zawiera ustawienia konfiguracji dla chmury usługi i poszczególne role, w tym liczbę wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="d4f3e-118">**Pakiet usługi**</span><span class="sxs-lookup"><span data-stu-id="d4f3e-118">**Service Package**</span></span>  
  <span data-ttu-id="d4f3e-119">Pakiet usługi (cspkg) zawiera kod aplikacji i konfiguracji i pliku definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="d4f3e-120">Dowiedz się więcej na temat tych i tworzenie pakietu [tutaj](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="d4f3e-121">Przygotowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="d4f3e-121">Prepare your app</span></span>
<span data-ttu-id="d4f3e-122">Przed wdrożeniem usługi w chmurze, należy utworzyć pakiet usługi chmury (cspkg) w kodzie aplikacji i pliku konfiguracji usługi chmury (cscfg).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="d4f3e-123">Zestaw Azure SDK oferuje narzędzia przygotowania te pliki wymagane wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="d4f3e-124">Można zainstalować zestawu SDK [Azure pobiera](https://azure.microsoft.com/downloads/) strony w języku wolisz do opracowywania kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="d4f3e-125">Trzy funkcje usługi chmury wymagają specjalnych konfiguracji przed wyeksportowaniem pakietu usług:</span><span class="sxs-lookup"><span data-stu-id="d4f3e-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="d4f3e-126">Jeśli ma zostać wdrożona usługa w chmurze, która używa protokołu Secure Sockets Layer (SSL) do szyfrowania danych [konfigurowania aplikacji](cloud-services-configure-ssl-certificate-portal.md#modify) dla protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="d4f3e-127">Jeśli chcesz skonfigurować połączenia pulpitu zdalnego z wystąpień roli [konfigurowania ról](cloud-services-role-enable-remote-desktop-new-portal.md) dla pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="d4f3e-128">Jeśli chcesz skonfigurować pełne, monitorowanie dla usługi w chmurze, należy włączyć diagnostyki Azure dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="d4f3e-129">*Monitorowanie minimalnego* (domyślne monitorowania poziomu) używa liczniki wydajności zebrane z hosta systemów operacyjnych dla wystąpień roli (maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="d4f3e-130">*Monitorowanie pełne* zbiera dodatkowe metryki na podstawie danych wydajności w ramach wystąpienia roli, aby umożliwić analizę bliżej problemów występujących podczas przetwarzania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-130">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="d4f3e-131">Aby dowiedzieć się, jak włączyć diagnostyki Azure, zobacz [Włączanie diagnostyki na platformie Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-131">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="d4f3e-132">Aby utworzyć usługi w chmurze z wdrożeniami ról sieć web i proces roboczy ról, należy [Utwórz pakiet usługi](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d4f3e-133">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="d4f3e-133">Before you begin</span></span>
* <span data-ttu-id="d4f3e-134">Jeśli nie zainstalowano zestaw SDK usługi Azure, kliknij przycisk **Zainstaluj zestaw Azure SDK** otworzyć [strona plików do pobrania usługi Azure](https://azure.microsoft.com/downloads/), a następnie pobrać zestaw SDK dla języka wolisz tworzenia kodu.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="d4f3e-135">(Będziesz mieć możliwość zrobić to później).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="d4f3e-136">Jeśli wszystkie wystąpienia roli jest wymagany certyfikat, należy utworzyć certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="d4f3e-137">Usługi w chmurze wymagają pliku pfx z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="d4f3e-138">Jak utworzyć i wdrożyć usługę w chmurze, możesz przekazać certyfikaty na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-138">You can upload the certificates to Azure as you create and deploy the cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="d4f3e-139">Tworzenie i wdrażanie</span><span class="sxs-lookup"><span data-stu-id="d4f3e-139">Create and deploy</span></span>
1. <span data-ttu-id="d4f3e-140">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d4f3e-141">Kliknij przycisk **nowy > obliczeniowe**, następnie przewiń w dół i kliknij przycisk **usługi w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-141">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![Publikowanie usługi w chmurze](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="d4f3e-143">W nowym **usługi w chmurze** bloku, wprowadź wartość dla **nazwy DNS**.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-143">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
4. <span data-ttu-id="d4f3e-144">Utwórz nową **grupy zasobów** lub wybierz istniejący.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="d4f3e-145">Wybierz **lokalizację**.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-145">Select a **Location**.</span></span>
6. <span data-ttu-id="d4f3e-146">Kliknij przycisk **pakietu**.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-146">Click **Package**.</span></span> <span data-ttu-id="d4f3e-147">Spowoduje to otwarcie **przekazania pakietu** bloku.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-147">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="d4f3e-148">Wypełnij wymagane pola.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-148">Fill in the required fields.</span></span> <span data-ttu-id="d4f3e-149">Jeśli jakieś role zawierają pojedynczego wystąpienia, upewnij się, **Wdróż, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="d4f3e-150">Upewnij się, że **rozpocząć wdrażanie** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="d4f3e-151">Kliknij przycisk **OK** którego zostanie zamknięte **przekazania pakietu** bloku.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-151">Click **OK** which will close the **Upload a package** blade.</span></span>
9. <span data-ttu-id="d4f3e-152">Jeśli nie masz żadnych certyfikatów, aby dodać, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-152">If you do not have any certificates to add, click **Create**.</span></span>

    ![Publikowanie usługi w chmurze](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="d4f3e-154">Przekaż certyfikat</span><span class="sxs-lookup"><span data-stu-id="d4f3e-154">Upload a certificate</span></span>
<span data-ttu-id="d4f3e-155">Jeśli pakiet wdrażania [skonfigurowana do używania certyfikatów](cloud-services-configure-ssl-certificate-portal.md#modify), możesz teraz przekazać certyfikat.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-155">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="d4f3e-156">Wybierz **certyfikaty**i na **Dodaj certyfikaty** bloku, wybierz plik .pfx certyfikatu SSL, a następnie podaj **hasło** dla certyfikatu</span><span class="sxs-lookup"><span data-stu-id="d4f3e-156">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="d4f3e-157">Kliknij przycisk **certyfikatu Attach**, a następnie kliknij przycisk **OK** na **Dodaj certyfikaty** bloku.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-157">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="d4f3e-158">Kliknij przycisk **Utwórz** na **usługi w chmurze** bloku.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-158">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="d4f3e-159">Po wdrożeniu został osiągnięty **gotowe** stanu, możesz przejść do następnych kroków.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-159">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![Publikowanie usługi w chmurze](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="d4f3e-161">Sprawdź wdrożenia ukończone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="d4f3e-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="d4f3e-162">Kliknij przycisk wystąpienie usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-162">Click the cloud service instance.</span></span>

    <span data-ttu-id="d4f3e-163">Stan powinny wskazywać, że usługa jest **systemem**.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-163">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="d4f3e-164">W obszarze **Essentials**, kliknij przycisk **adres URL witryny** można otworzyć usługi w chmurze w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="d4f3e-164">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="d4f3e-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4f3e-166">Next steps</span></span>
* <span data-ttu-id="d4f3e-167">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="d4f3e-168">Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="d4f3e-169">[Usługi w chmurze zarządzanie](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="d4f3e-170">Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4f3e-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
