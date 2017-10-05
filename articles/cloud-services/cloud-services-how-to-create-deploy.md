---
title: "Jak utworzyć i wdrożyć usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia i wdrażania usługi w chmurze przy użyciu metody szybkie tworzenie w systemie Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 2a2172a78bfd3ac923edbc9de366b035629dd27b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="446a6-103">Jak utworzyć i wdrożyć usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="446a6-103">How to Create and Deploy a Cloud Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="446a6-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="446a6-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="446a6-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="446a6-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
> 
> 

<span data-ttu-id="446a6-106">Klasyczny portal Azure udostępnia dwa sposoby tworzenia i wdrażania usługi w chmurze: **szybkie tworzenie** i **Utwórz niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="446a6-106">The Azure classic portal provides two ways for you to create and deploy a cloud service: **Quick Create** and **Custom Create**.</span></span>

<span data-ttu-id="446a6-107">W tym temacie wyjaśniono, jak utworzyć nową usługę w chmurze, a następnie użyj przy użyciu metody szybkie tworzenie **przekazać** Aby przekazać i wdrożyć pakiet usługi chmury na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="446a6-107">This topic explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="446a6-108">Korzystając z tej metody, klasycznym portalu Azure sprawia, że dostępne wygodne łącza ukończenia wszystkich wymagań w trakcie pracy.</span><span class="sxs-lookup"><span data-stu-id="446a6-108">When you use this method, the Azure classic portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="446a6-109">Jeśli wszystko jest gotowe do wdrożenia usługi w chmurze podczas jego tworzenia, można wykonać jednocześnie na tym samym czasie przy użyciu **Utwórz niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="446a6-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using **Custom Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="446a6-110">Jeśli planujesz opublikować usługi w chmurze z programu Visual Studio Team Services (VSTS), użyj **szybkie tworzenie**, a następnie skonfigurować publikowanie programu VSTS z **Szybki Start** lub do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="446a6-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use **Quick Create**, and then set up VSTS publishing from **Quick Start** or the dashboard.</span></span>
> 
> 

## <a name="concepts"></a><span data-ttu-id="446a6-111">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="446a6-111">Concepts</span></span>
<span data-ttu-id="446a6-112">Aby wdrożyć aplikację jako usługa w chmurze na platformie Azure wymagane są trzy składniki:</span><span class="sxs-lookup"><span data-stu-id="446a6-112">Three components are required in order to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="446a6-113">**Definicja usługi**</span><span class="sxs-lookup"><span data-stu-id="446a6-113">**Service Definition**</span></span>  
  <span data-ttu-id="446a6-114">Chmura pliku definicji usługi (csdef) definiuje modelu usługi, w tym liczba ról.</span><span class="sxs-lookup"><span data-stu-id="446a6-114">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="446a6-115">**Konfiguracja usługi**</span><span class="sxs-lookup"><span data-stu-id="446a6-115">**Service Configuration**</span></span>  
  <span data-ttu-id="446a6-116">Plik konfiguracji usługi chmury (cscfg) zawiera ustawienia konfiguracji dla chmury usługi i poszczególne role, w tym liczbę wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="446a6-116">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="446a6-117">**Pakiet usługi**</span><span class="sxs-lookup"><span data-stu-id="446a6-117">**Service Package**</span></span>  
  <span data-ttu-id="446a6-118">Pakiet usługi (cspkg) zawiera kod aplikacji i konfiguracji i pliku definicji usługi.</span><span class="sxs-lookup"><span data-stu-id="446a6-118">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="446a6-119">Dowiedz się więcej na temat tych i tworzenie pakietu [tutaj](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="446a6-119">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="446a6-120">Przygotowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="446a6-120">Prepare your app</span></span>
<span data-ttu-id="446a6-121">Przed wdrożeniem usługi w chmurze, należy utworzyć pakiet usługi chmury (cspkg) w kodzie aplikacji i pliku konfiguracji usługi chmury (cscfg).</span><span class="sxs-lookup"><span data-stu-id="446a6-121">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="446a6-122">Zestaw Azure SDK oferuje narzędzia przygotowania te pliki wymagane wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="446a6-122">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="446a6-123">Można zainstalować zestawu SDK [Azure pobiera](https://azure.microsoft.com/downloads/) strony w języku wolisz do opracowywania kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="446a6-123">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="446a6-124">Trzy funkcje usługi chmury wymagają specjalnych konfiguracji przed wyeksportowaniem pakietu usług:</span><span class="sxs-lookup"><span data-stu-id="446a6-124">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="446a6-125">Jeśli ma zostać wdrożona usługa w chmurze, która używa protokołu Secure Sockets Layer (SSL) do szyfrowania danych [konfigurowania aplikacji](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) dla protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="446a6-125">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) for SSL.</span></span>
* <span data-ttu-id="446a6-126">Jeśli chcesz skonfigurować połączenia pulpitu zdalnego z wystąpień roli [konfigurowania ról](cloud-services-role-enable-remote-desktop.md) dla pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="446a6-126">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop.md) for Remote Desktop.</span></span>
* <span data-ttu-id="446a6-127">Jeśli chcesz skonfigurować pełne, monitorowanie dla usługi w chmurze, należy włączyć diagnostyki Azure dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="446a6-127">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="446a6-128">*Monitorowanie minimalnego* (domyślne monitorowania poziomu) używa liczniki wydajności zebrane z hosta systemów operacyjnych dla wystąpień roli (maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="446a6-128">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="446a6-129">"Monitorowanie pełne * zbiera dodatkowe metryki na podstawie danych wydajności w ramach wystąpienia roli, aby umożliwić analizę bliżej problemów występujących podczas przetwarzania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="446a6-129">"Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="446a6-130">Aby dowiedzieć się, jak włączyć diagnostyki Azure, zobacz [Włączanie diagnostyki na platformie Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="446a6-130">To find out how to enable Azure Diagnostics, see [Enabling Diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="446a6-131">Aby utworzyć usługi w chmurze z wdrożeniami ról sieć web i proces roboczy ról, należy [Utwórz pakiet usługi](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="446a6-131">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="446a6-132">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="446a6-132">Before you begin</span></span>
* <span data-ttu-id="446a6-133">Jeśli nie zainstalowano zestaw SDK usługi Azure, kliknij przycisk **Zainstaluj zestaw Azure SDK** otworzyć [strona plików do pobrania usługi Azure](https://azure.microsoft.com/downloads/), a następnie pobrać zestaw SDK dla języka wolisz tworzenia kodu.</span><span class="sxs-lookup"><span data-stu-id="446a6-133">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="446a6-134">(Będziesz mieć możliwość zrobić to później).</span><span class="sxs-lookup"><span data-stu-id="446a6-134">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="446a6-135">Jeśli wszystkie wystąpienia roli jest wymagany certyfikat, należy utworzyć certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="446a6-135">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="446a6-136">Usługi w chmurze wymagają pliku pfx z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="446a6-136">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="446a6-137">Możesz [Przekaż certyfikaty Azure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) podczas tworzenia i wdrażania usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="446a6-137">You can [upload the certificates to Azure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) as you create and deploy the cloud service.</span></span>
* <span data-ttu-id="446a6-138">Jeśli planujesz wdrożyć usługę w chmurze do grupy koligacji, należy utworzyć grupy koligacji.</span><span class="sxs-lookup"><span data-stu-id="446a6-138">If you plan to deploy the cloud service to an affinity group, create the affinity group.</span></span> <span data-ttu-id="446a6-139">Grupy koligacji służy do wdrażania usługi w chmurze i innymi usługami Azure w tej samej lokalizacji, w regionie.</span><span class="sxs-lookup"><span data-stu-id="446a6-139">You can use an affinity group to deploy your cloud service and other Azure services to the same location in a region.</span></span> <span data-ttu-id="446a6-140">Można utworzyć grupy koligacji w **sieci** obszaru klasyczny Portal Azure portalu na **grup koligacji** strony.</span><span class="sxs-lookup"><span data-stu-id="446a6-140">You can create the affinity group in the **Networks** area of the Azure classic portal, on the **Affinity Groups** page.</span></span>

## <a name="how-to-create-a-cloud-service-using-quick-create"></a><span data-ttu-id="446a6-141">Porady: Tworzenie usługi w chmurze przy użyciu szybkie tworzenie</span><span class="sxs-lookup"><span data-stu-id="446a6-141">How to: Create a cloud service using Quick Create</span></span>
1. <span data-ttu-id="446a6-142">W [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **nowy**>**obliczeniowe**>**usługi w chmurze** > **Szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="446a6-142">In the [Azure classic portal](http://manage.windowsazure.com/), click **New**>**Compute**>**Cloud Service**>**Quick Create**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. <span data-ttu-id="446a6-144">W **adres URL**, wprowadź nazwę domeny podrzędnej do użycia w publiczny adres URL do uzyskiwania dostępu do usługi w chmurze we wdrożeniach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="446a6-144">In **URL**, enter a subdomain name to use in the public URL for accessing your cloud service in production deployments.</span></span> <span data-ttu-id="446a6-145">Format adresu URL wdrożeń produkcyjnych jest: http://*myURL*. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="446a6-145">The URL format for production deployments is: http://*myURL*.cloudapp.net.</span></span>
3. <span data-ttu-id="446a6-146">W **Region lub grupę koligacji**, wybierz region geograficzny lub grupy koligacji, aby wdrożyć w usłudze chmury.</span><span class="sxs-lookup"><span data-stu-id="446a6-146">In **Region or Affinity Group**, select the geographic region or affinity group to deploy the cloud service to.</span></span> <span data-ttu-id="446a6-147">Wybierz grupy koligacji, jeśli chcesz wdrożyć usługi w chmurze do tej samej lokalizacji co innymi usługami Azure w obrębie regionu.</span><span class="sxs-lookup"><span data-stu-id="446a6-147">Select an affinity group if you want to deploy your cloud service to the same location as other Azure services within a region.</span></span>
4. <span data-ttu-id="446a6-148">Kliknij pozycję **Utwórz usługę w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="446a6-148">Click **Create Cloud Service**.</span></span>
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    <span data-ttu-id="446a6-150">Stan procesu można monitorować w obszarze wiadomości w dolnej części okna.</span><span class="sxs-lookup"><span data-stu-id="446a6-150">You can monitor the status of the process in the message area at the bottom of the window.</span></span>
   
    <span data-ttu-id="446a6-151">**Usługi w chmurze** powoduje otwarcie obszaru z nową usługę w chmurze wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="446a6-151">The **Cloud Services** area opens, with the new cloud service displayed.</span></span> <span data-ttu-id="446a6-152">Stan zmieni się na utworzone, tworzenia usługi w chmurze została zakończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="446a6-152">When the status changes to Created, cloud service creation has completed successfully.</span></span>
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a><span data-ttu-id="446a6-154">Porady: przekazywanie certyfikatu dla usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="446a6-154">How to: Upload a certificate for a cloud service</span></span>
1. <span data-ttu-id="446a6-155">W [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, kliknij nazwę usługi w chmurze, a następnie kliknij przycisk **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="446a6-155">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Certificates**.</span></span>
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. <span data-ttu-id="446a6-157">Kliknij opcję **przekazać certyfikat** lub **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="446a6-157">Click either **Upload a certificate** or **Upload**.</span></span>
3. <span data-ttu-id="446a6-158">W **pliku**, użyj **Przeglądaj** umożliwia wybranie certyfikatu (pfx).</span><span class="sxs-lookup"><span data-stu-id="446a6-158">In **File**, use **Browse** to select the certificate (.pfx file).</span></span>
4. <span data-ttu-id="446a6-159">W **hasło**, wprowadź klucz prywatny dla certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="446a6-159">In **Password**, enter the private key for the certificate.</span></span>
5. <span data-ttu-id="446a6-160">Kliknij przycisk **OK** (znacznikiem wyboru).</span><span class="sxs-lookup"><span data-stu-id="446a6-160">Click **OK** (checkmark).</span></span>
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    <span data-ttu-id="446a6-162">Możesz obserwować postęp przekazywania w obszarze wiadomości pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="446a6-162">You can watch the progress of the upload in the message area, shown below.</span></span> <span data-ttu-id="446a6-163">Po zakończeniu przekazywania, certyfikat zostanie dodany do tabeli.</span><span class="sxs-lookup"><span data-stu-id="446a6-163">When the upload completes, the certificate is added to the table.</span></span> <span data-ttu-id="446a6-164">W obszarze wiadomości kliknij przycisk OK, aby zamknąć komunikat.</span><span class="sxs-lookup"><span data-stu-id="446a6-164">In the message area, click OK to close the message.</span></span>
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a><span data-ttu-id="446a6-166">Porady: Wdrażanie usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="446a6-166">How to: Deploy a cloud service</span></span>
1. <span data-ttu-id="446a6-167">W [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, kliknij nazwę usługi w chmurze, a następnie kliknij przycisk **pulpitu nawigacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="446a6-167">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**, click the name of the cloud service, and then click **Dashboard**.</span></span>
2. <span data-ttu-id="446a6-168">Kliknij opcję **przekazania nowego wdrożenia produkcyjnego** lub **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="446a6-168">Click either **Upload a new production deployment** or **Upload**.</span></span>
3. <span data-ttu-id="446a6-169">W **etykieta wdrożenia**, wprowadź nazwę dla nowego wdrożenia — na przykład MyCloudServicev4.</span><span class="sxs-lookup"><span data-stu-id="446a6-169">In **Deployment label**, enter a name for the new deployment - for example, MyCloudServicev4.</span></span>
4. <span data-ttu-id="446a6-170">W **pakietu**, użyj **Przeglądaj** i wybierz plik pakietu usługi (cspkg) do użycia.</span><span class="sxs-lookup"><span data-stu-id="446a6-170">In **Package**, use **Browse** to select the service package file (.cspkg) to use.</span></span>
5. <span data-ttu-id="446a6-171">W **konfiguracji**, użyj **Przeglądaj** i wybierz plik konfiguracji usługi (cscfg) do użycia.</span><span class="sxs-lookup"><span data-stu-id="446a6-171">In **Configuration**, use **Browse** to select the service configure file (.cscfg) to use.</span></span>
6. <span data-ttu-id="446a6-172">Jeśli usługa w chmurze będzie zawierać żadnych ról z tylko jednym wystąpieniem, zaznacz **Wdróż, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** pole wyboru, aby umożliwić wdrożenie, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="446a6-172">If the cloud service will include any roles with only one instance, select the **Deploy even if one or more roles contain a single instance** check box to enable the deployment to proceed.</span></span>
   
    <span data-ttu-id="446a6-173">Każdy rola ma co najmniej dwa wystąpienia Azure tylko może zagwarantować 99,95% dostępu do usługi w chmurze podczas konserwacji i obsługi aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="446a6-173">Azure can only guarantee 99.95 percent access to the cloud service during maintenance and service updates if every role has at least two instances.</span></span> <span data-ttu-id="446a6-174">W razie potrzeby można dodać wystąpienia dodatkowych ról na **skali** strony po wdrożeniu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="446a6-174">If needed, you can add additional role instances on the **Scale** page after you deploy the cloud service.</span></span> <span data-ttu-id="446a6-175">Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="446a6-175">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>
7. <span data-ttu-id="446a6-176">Kliknij przycisk **OK** (zaznaczone), aby rozpocząć wdrażanie usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="446a6-176">Click **OK** (checkmark) to begin the cloud service deployment.</span></span>
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    <span data-ttu-id="446a6-178">Można monitorować stan wdrożenia w obszarze wiadomości.</span><span class="sxs-lookup"><span data-stu-id="446a6-178">You can monitor the status of the deployment in the message area.</span></span> <span data-ttu-id="446a6-179">Kliknij przycisk OK, aby ukryć wiadomości.</span><span class="sxs-lookup"><span data-stu-id="446a6-179">Click OK to hide the message.</span></span>
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="446a6-181">Sprawdź wdrożenia ukończone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="446a6-181">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="446a6-182">Kliknij przycisk **pulpitu nawigacyjnego**.</span><span class="sxs-lookup"><span data-stu-id="446a6-182">Click **Dashboard**.</span></span>
   
    <span data-ttu-id="446a6-183">Stan powinny wskazywać, że usługa jest **systemem**.</span><span class="sxs-lookup"><span data-stu-id="446a6-183">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="446a6-184">W obszarze **szybkiego dostępu**, kliknij adres URL witryny, aby otworzyć usługi w chmurze w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="446a6-184">Under **quick glance**, click the site URL to open your cloud service in a web browser.</span></span>
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a><span data-ttu-id="446a6-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="446a6-186">Next steps</span></span>
* <span data-ttu-id="446a6-187">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="446a6-187">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="446a6-188">Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="446a6-188">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="446a6-189">[Usługi w chmurze zarządzanie](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="446a6-189">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>
* <span data-ttu-id="446a6-190">Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="446a6-190">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

