---
title: Instalowanie bramy danych lokalnych | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zainstalować i skonfigurować bramę danych lokalnego."
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
ms.openlocfilehash: 6ef296fb98478be9240f0231c8ad39cd2a0af995
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="8dc29-103">Zainstaluj i skonfiguruj bramę danych lokalnych</span><span class="sxs-lookup"><span data-stu-id="8dc29-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="8dc29-104">Bramę danych lokalnych jest wymagany, gdy łączą się lokalnych źródeł danych z co najmniej jeden serwer usług Azure Analysis Services, w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="8dc29-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in the same region connect to on-premises data sources.</span></span> <span data-ttu-id="8dc29-105">Aby dowiedzieć się więcej o bramie, zobacz [bramy danych lokalnych](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="8dc29-105">To learn more about the gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8dc29-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8dc29-106">Prerequisites</span></span>
<span data-ttu-id="8dc29-107">**Minimalne wymagania:**</span><span class="sxs-lookup"><span data-stu-id="8dc29-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="8dc29-108">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="8dc29-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="8dc29-109">64-bitowej wersji systemu Windows 7 / Windows Server 2008 R2 (lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="8dc29-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="8dc29-110">**Zalecane:**</span><span class="sxs-lookup"><span data-stu-id="8dc29-110">**Recommended:**</span></span>

* <span data-ttu-id="8dc29-111">8 rdzeni procesora CPU</span><span class="sxs-lookup"><span data-stu-id="8dc29-111">8 Core CPU</span></span>
* <span data-ttu-id="8dc29-112">8 GB pamięci</span><span class="sxs-lookup"><span data-stu-id="8dc29-112">8 GB Memory</span></span>
* <span data-ttu-id="8dc29-113">64-bitowej wersji systemu Windows 2012 R2 (lub nowszy)</span><span class="sxs-lookup"><span data-stu-id="8dc29-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="8dc29-114">**Ważne kwestie:**</span><span class="sxs-lookup"><span data-stu-id="8dc29-114">**Important considerations:**</span></span>

* <span data-ttu-id="8dc29-115">Podczas instalacji przy rejestracji bramy w usłudze Azure wybrano domyślnego regionu dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8dc29-115">During setup, when registering your gateway with Azure, the default region for your subscription is selected.</span></span> <span data-ttu-id="8dc29-116">Można wybrać inny region.</span><span class="sxs-lookup"><span data-stu-id="8dc29-116">You can choose a different region.</span></span> <span data-ttu-id="8dc29-117">Jeśli masz serwery w więcej niż jeden region, należy zainstalować bramy dla każdego regionu.</span><span class="sxs-lookup"><span data-stu-id="8dc29-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="8dc29-118">Brama nie można zainstalować na kontrolerze domeny.</span><span class="sxs-lookup"><span data-stu-id="8dc29-118">The gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="8dc29-119">Na jednym komputerze można zainstalować tylko jedną bramę.</span><span class="sxs-lookup"><span data-stu-id="8dc29-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="8dc29-120">Zainstalować bramę na komputerze, który pozostaje na, a nie przechodzi w stan uśpienia.</span><span class="sxs-lookup"><span data-stu-id="8dc29-120">Install the gateway on a computer that remains on and does not go to sleep.</span></span>
* <span data-ttu-id="8dc29-121">Nie należy instalować bramy na komputerze bezprzewodowo podłączony do sieci.</span><span class="sxs-lookup"><span data-stu-id="8dc29-121">Do not install the gateway on a computer wirelessly connected to your network.</span></span> <span data-ttu-id="8dc29-122">Wydajność może być mniejsza.</span><span class="sxs-lookup"><span data-stu-id="8dc29-122">Performance can be diminished.</span></span>


## <span data-ttu-id="8dc29-123"><a name="download"></a>Pobierz</span><span class="sxs-lookup"><span data-stu-id="8dc29-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="8dc29-124">Pobierz bramę</span><span class="sxs-lookup"><span data-stu-id="8dc29-124">Download the gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="8dc29-125"><a name="install"></a>Zainstaluj</span><span class="sxs-lookup"><span data-stu-id="8dc29-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="8dc29-126">Uruchom Instalatora.</span><span class="sxs-lookup"><span data-stu-id="8dc29-126">Run setup.</span></span>

2. <span data-ttu-id="8dc29-127">Wybierz lokalizację, zaakceptuj warunki, a następnie kliknij **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="8dc29-127">Select a location, accept the terms, and then click **Install**.</span></span>

   ![Zainstaluj lokalizacji oraz postanowienia licencyjne](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="8dc29-129">Wybierz **lokalnych danych bramy (zalecane)**.</span><span class="sxs-lookup"><span data-stu-id="8dc29-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="8dc29-130">Azure Analysis Services nie obsługuje trybu osobistych.</span><span class="sxs-lookup"><span data-stu-id="8dc29-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Wybierz typ bramy](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="8dc29-132">Wprowadź konto, aby logowanie do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc29-132">Enter an account to sign in to Azure.</span></span> <span data-ttu-id="8dc29-133">Konto musi znajdować się w Twojej dzierżawy usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8dc29-133">The account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="8dc29-134">To konto jest używane dla administratora bramy.</span><span class="sxs-lookup"><span data-stu-id="8dc29-134">This account is used for the gateway administrator.</span></span> 

   ![Wprowadź konto, aby logowanie do platformy Azure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="8dc29-136">Jeśli możesz zalogować się przy użyciu konta domeny, zostanie zamapowane na konto organizacyjne w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dc29-136">If you sign in with a domain account, it will be mapped to your organizational account in Azure AD.</span></span> <span data-ttu-id="8dc29-137">Konta organizacyjnego będzie służyć jako administratora bramy.</span><span class="sxs-lookup"><span data-stu-id="8dc29-137">Your organizational account will be used as the the gateway administrator.</span></span>

## <span data-ttu-id="8dc29-138"><a name="register"></a>Rejestr</span><span class="sxs-lookup"><span data-stu-id="8dc29-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="8dc29-139">Aby utworzyć zasób bramy na platformie Azure, możesz zarejestrować lokalne wystąpienie instalowania z usługi bramy w chmurze.</span><span class="sxs-lookup"><span data-stu-id="8dc29-139">In order to create a gateway resource in Azure, you must register the local instance you installed with the Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="8dc29-140">Wybierz **zarejestrować nową bramę na tym komputerze**.</span><span class="sxs-lookup"><span data-stu-id="8dc29-140">Select **Register a new gateway on this computer**.</span></span>

    ![Zarejestruj subskrypcję](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="8dc29-142">Wpisz nazwę i odzyskiwanie klucza bramy.</span><span class="sxs-lookup"><span data-stu-id="8dc29-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="8dc29-143">Domyślnie przy użyciu brama swoją subskrypcję domyślnego regionu.</span><span class="sxs-lookup"><span data-stu-id="8dc29-143">By default, the gateway uses your subscription's default region.</span></span> <span data-ttu-id="8dc29-144">Jeśli chcesz wybrać inny region, wybierz **Region zmiany**.</span><span class="sxs-lookup"><span data-stu-id="8dc29-144">If you need to select a different region, select **Change Region**.</span></span>

   ![Zarejestruj subskrypcję](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="8dc29-146"><a name="create-resource"></a>Utwórz zasób Azure bramy</span><span class="sxs-lookup"><span data-stu-id="8dc29-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="8dc29-147">Po zainstalowaniu i zarejestrować bramę, należy utworzyć zasób bramy w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc29-147">After you've installed and registered your gateway, you need to create a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="8dc29-148">Zaloguj się do platformy Azure z tego samego konta używanego podczas rejestrowania bramy.</span><span class="sxs-lookup"><span data-stu-id="8dc29-148">Sign in to Azure with the same account you used when registering the gateway.</span></span>

1. <span data-ttu-id="8dc29-149">W portalu Azure kliknij **Utwórz nową usługę** > **integracji przedsiębiorstwa** > **bramy danych lokalnych** > **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8dc29-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Utwórz zasób bramy](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="8dc29-151">W **Utwórz bramę połączenia**, wprowadź następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="8dc29-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="8dc29-152">**Nazwa**: Wprowadź nazwę dla zasobu bramy.</span><span class="sxs-lookup"><span data-stu-id="8dc29-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="8dc29-153">**Subskrypcja**: Wybierz subskrypcję platformy Azure do skojarzenia z zasobu bramy.</span><span class="sxs-lookup"><span data-stu-id="8dc29-153">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="8dc29-154">Ta subskrypcja powinna być tej samej subskrypcji, które serwery są w.</span><span class="sxs-lookup"><span data-stu-id="8dc29-154">This subscription should be the same subscription your servers are in.</span></span>
   
      <span data-ttu-id="8dc29-155">Domyślna subskrypcja opiera się na konto platformy Azure, używany do logowania.</span><span class="sxs-lookup"><span data-stu-id="8dc29-155">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="8dc29-156">**Grupa zasobów**: utwórz grupę zasobów lub wybierz istniejącą.</span><span class="sxs-lookup"><span data-stu-id="8dc29-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="8dc29-157">**Lokalizacja**: Wybierz region, w zarejestrowany bramy w.</span><span class="sxs-lookup"><span data-stu-id="8dc29-157">**Location**: Select the region you registered your gateway in.</span></span>

    * <span data-ttu-id="8dc29-158">**Nazwa instalacji**: Jeśli instalacji bramy nie została jeszcze wybrana, wybierz bramę, w zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="8dc29-158">**Installation Name**: If your gateway installation isn't already selected, select the gateway registered.</span></span> 

    <span data-ttu-id="8dc29-159">Gdy wszystko będzie gotowe, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8dc29-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="8dc29-160"><a name="connect-servers"></a>Połącz serwery do zasobu bramy</span><span class="sxs-lookup"><span data-stu-id="8dc29-160"><a name="connect-servers"></a>Connect servers to the gateway resource</span></span>

1. <span data-ttu-id="8dc29-161">W sieci — Omówienie serwera usług Azure Analysis Services kliknij **bramy danych lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="8dc29-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Połącz serwer bramy](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="8dc29-163">W **wybierz bramę danych lokalnego, aby połączyć**wybierz zasób bramy, a następnie kliknij przycisk **wybranej bramy Połącz**.</span><span class="sxs-lookup"><span data-stu-id="8dc29-163">In **Pick an On-Premises Data Gateway to connect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Połącz serwer bramy zasobów](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="8dc29-165">Jeśli na liście nie ma bramy, serwer, prawdopodobnie nie w tym samym regionie co region określone podczas rejestrowania bramy.</span><span class="sxs-lookup"><span data-stu-id="8dc29-165">If your gateway does not appear in the list, your server is likely not in the same region as the region you specified when registering the gateway.</span></span> 

<span data-ttu-id="8dc29-166">To już wszystko.</span><span class="sxs-lookup"><span data-stu-id="8dc29-166">That's it.</span></span> <span data-ttu-id="8dc29-167">Jeśli trzeba otworzyć porty lub czy rozwiązywania wszelkich problemów, koniecznie zapoznaj się z [bramy danych lokalnych](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="8dc29-167">If you need to open ports or do any troubleshooting, be sure to check out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dc29-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8dc29-168">Next steps</span></span>
* [<span data-ttu-id="8dc29-169">Zarządzanie usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8dc29-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="8dc29-170">Pobieranie danych z usług Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8dc29-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
