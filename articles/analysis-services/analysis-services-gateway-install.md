---
title: Brama danych lokalnych aaaInstall | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall i skonfiguruj bramę danych lokalnego."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="04f0e-103">Zainstaluj i skonfiguruj bramę danych lokalnych</span><span class="sxs-lookup"><span data-stu-id="04f0e-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="04f0e-104">Brama danych lokalnych jest wymagany, jeśli co najmniej jeden serwer usług Azure Analysis Services w hello sam region połączenia tooon lokalnych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="04f0e-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="04f0e-105">Zobacz toolearn więcej informacji na temat bramy hello [bramy danych lokalnych](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="04f0e-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04f0e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="04f0e-106">Prerequisites</span></span>
<span data-ttu-id="04f0e-107">**Minimalne wymagania:**</span><span class="sxs-lookup"><span data-stu-id="04f0e-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="04f0e-108">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="04f0e-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="04f0e-109">64-bitowej wersji systemu Windows 7 / Windows Server 2008 R2 (lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="04f0e-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="04f0e-110">**Zalecane:**</span><span class="sxs-lookup"><span data-stu-id="04f0e-110">**Recommended:**</span></span>

* <span data-ttu-id="04f0e-111">8 rdzeni procesora CPU</span><span class="sxs-lookup"><span data-stu-id="04f0e-111">8 Core CPU</span></span>
* <span data-ttu-id="04f0e-112">8 GB pamięci</span><span class="sxs-lookup"><span data-stu-id="04f0e-112">8 GB Memory</span></span>
* <span data-ttu-id="04f0e-113">64-bitowej wersji systemu Windows 2012 R2 (lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="04f0e-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="04f0e-114">**Ważne kwestie:**</span><span class="sxs-lookup"><span data-stu-id="04f0e-114">**Important considerations:**</span></span>

* <span data-ttu-id="04f0e-115">Podczas instalacji przy rejestracji bramy w usłudze Azure wybrano hello domyślnego regionu dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="04f0e-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="04f0e-116">Można wybrać inny region.</span><span class="sxs-lookup"><span data-stu-id="04f0e-116">You can choose a different region.</span></span> <span data-ttu-id="04f0e-117">Jeśli masz serwery w więcej niż jeden region, należy zainstalować bramy dla każdego regionu.</span><span class="sxs-lookup"><span data-stu-id="04f0e-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="04f0e-118">Witaj bramy nie można zainstalować na kontrolerze domeny.</span><span class="sxs-lookup"><span data-stu-id="04f0e-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="04f0e-119">Na jednym komputerze można zainstalować tylko jedną bramę.</span><span class="sxs-lookup"><span data-stu-id="04f0e-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="04f0e-120">Zainstaluj bramę hello na komputerze, który pozostaje na, a nie przechodzi toosleep.</span><span class="sxs-lookup"><span data-stu-id="04f0e-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="04f0e-121">Nie należy instalować bramy hello sieci tooyour bezprzewodowo podłączonego komputera.</span><span class="sxs-lookup"><span data-stu-id="04f0e-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="04f0e-122">Wydajność może być mniejsza.</span><span class="sxs-lookup"><span data-stu-id="04f0e-122">Performance can be diminished.</span></span>


## <span data-ttu-id="04f0e-123"><a name="download"></a>Pobierz</span><span class="sxs-lookup"><span data-stu-id="04f0e-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="04f0e-124">Pobierz hello bramy</span><span class="sxs-lookup"><span data-stu-id="04f0e-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="04f0e-125"><a name="install"></a>Zainstaluj</span><span class="sxs-lookup"><span data-stu-id="04f0e-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="04f0e-126">Uruchom Instalatora.</span><span class="sxs-lookup"><span data-stu-id="04f0e-126">Run setup.</span></span>

2. <span data-ttu-id="04f0e-127">Wybierz lokalizację, zaakceptuj postanowienia hello, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="04f0e-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![Zainstaluj lokalizacji oraz postanowienia licencyjne](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="04f0e-129">Wybierz **lokalnych danych bramy (zalecane)**.</span><span class="sxs-lookup"><span data-stu-id="04f0e-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="04f0e-130">Azure Analysis Services nie obsługuje trybu osobistych.</span><span class="sxs-lookup"><span data-stu-id="04f0e-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Wybierz typ bramy](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="04f0e-132">Wprowadź konto toosign tooAzure.</span><span class="sxs-lookup"><span data-stu-id="04f0e-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="04f0e-133">Witaj, konto musi być w Twojej dzierżawy usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="04f0e-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="04f0e-134">To konto jest używane dla hello administratora bramy.</span><span class="sxs-lookup"><span data-stu-id="04f0e-134">This account is used for hello gateway administrator.</span></span> 

   ![Wprowadź konto toosign w tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="04f0e-136">Jeśli możesz zalogować się przy użyciu konta domeny, będzie on zamapowany tooyour konto organizacyjne w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04f0e-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="04f0e-137">Konta organizacyjnego będzie służyć jako administrator bramy hello hello.</span><span class="sxs-lookup"><span data-stu-id="04f0e-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="04f0e-138"><a name="register"></a>Rejestr</span><span class="sxs-lookup"><span data-stu-id="04f0e-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="04f0e-139">W kolejności toocreate zasobu bramy na platformie Azure możesz zarejestrować hello lokalne wystąpienie instalowania z hello usługi bramy w chmurze.</span><span class="sxs-lookup"><span data-stu-id="04f0e-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="04f0e-140">Wybierz **zarejestrować nową bramę na tym komputerze**.</span><span class="sxs-lookup"><span data-stu-id="04f0e-140">Select **Register a new gateway on this computer**.</span></span>

    ![Zarejestruj subskrypcję](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="04f0e-142">Wpisz nazwę i odzyskiwanie klucza bramy.</span><span class="sxs-lookup"><span data-stu-id="04f0e-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="04f0e-143">Domyślnie brama hello używa Twojej subskrypcji domyślnego regionu.</span><span class="sxs-lookup"><span data-stu-id="04f0e-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="04f0e-144">Jeśli potrzebujesz tooselect inny region, wybierz **Region zmiany**.</span><span class="sxs-lookup"><span data-stu-id="04f0e-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![Zarejestruj subskrypcję](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="04f0e-146"><a name="create-resource"></a>Utwórz zasób Azure bramy</span><span class="sxs-lookup"><span data-stu-id="04f0e-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="04f0e-147">Po zainstalowaniu i zarejestrować bramę, należy toocreate zasobów bramy w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="04f0e-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="04f0e-148">Zaloguj tooAzure z hello samo konto używane podczas rejestrowania hello bramy.</span><span class="sxs-lookup"><span data-stu-id="04f0e-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="04f0e-149">W portalu Azure kliknij **Utwórz nową usługę** > **integracji przedsiębiorstwa** > **bramy danych lokalnych** > **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="04f0e-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Utwórz zasób bramy](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="04f0e-151">W **Utwórz bramę połączenia**, wprowadź następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="04f0e-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="04f0e-152">**Nazwa**: Wprowadź nazwę dla zasobu bramy.</span><span class="sxs-lookup"><span data-stu-id="04f0e-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="04f0e-153">**Subskrypcja**: Wybierz hello tooassociate subskrypcji platformy Azure z zasobu bramy.</span><span class="sxs-lookup"><span data-stu-id="04f0e-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="04f0e-154">Ta subskrypcja powinna być hello tej samej subskrypcji, serwery są w.</span><span class="sxs-lookup"><span data-stu-id="04f0e-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="04f0e-155">Hello Domyślna subskrypcja jest oparta na powitania konto platformy Azure, który został użyty toosign w.</span><span class="sxs-lookup"><span data-stu-id="04f0e-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="04f0e-156">**Grupa zasobów**: utwórz grupę zasobów lub wybierz istniejącą.</span><span class="sxs-lookup"><span data-stu-id="04f0e-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="04f0e-157">**Lokalizacja**: hello wybierz region zarejestrować bramy w.</span><span class="sxs-lookup"><span data-stu-id="04f0e-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="04f0e-158">**Nazwa instalacji**: Jeśli instalacji bramy nie została jeszcze wybrana, wybierz hello brama zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="04f0e-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="04f0e-159">Gdy wszystko będzie gotowe, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="04f0e-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="04f0e-160"><a name="connect-servers"></a>Połącz zasób bramy toohello serwerów</span><span class="sxs-lookup"><span data-stu-id="04f0e-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="04f0e-161">W sieci — Omówienie serwera usług Azure Analysis Services kliknij **bramy danych lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="04f0e-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Połącz toogateway serwera](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="04f0e-163">W **wybierz tooconnect bramy danych lokalnego**wybierz zasób bramy, a następnie kliknij przycisk **wybranej bramy Połącz**.</span><span class="sxs-lookup"><span data-stu-id="04f0e-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Połącz zasób toogateway serwera](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="04f0e-165">Jeśli brama nie ma na liście hello, serwer może nie jest w tym samym regionie co określony podczas rejestrowania bramy hello region hello hello.</span><span class="sxs-lookup"><span data-stu-id="04f0e-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="04f0e-166">To już wszystko.</span><span class="sxs-lookup"><span data-stu-id="04f0e-166">That's it.</span></span> <span data-ttu-id="04f0e-167">Jeśli potrzebne porty tooopen lub wykonaj wszelkie rozwiązywania problemów, można się toocheck limit [bramy danych lokalnych](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="04f0e-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04f0e-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04f0e-168">Next steps</span></span>
* [<span data-ttu-id="04f0e-169">Zarządzanie usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="04f0e-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="04f0e-170">Pobieranie danych z usług Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="04f0e-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
