---
title: "Konfigurowanie SSL odciążania — brama aplikacji w usłudze Azure - Azure Portal | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje, aby utworzyć bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu portalu"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="a6095-103">Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="a6095-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6095-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a6095-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="a6095-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6095-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="a6095-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6095-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="a6095-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a6095-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="a6095-108">Usługę Azure Application Gateway można skonfigurować tak, aby przerywała sesję protokołu SSL (Secure Sockets Layer) na poziomie bramy, co pozwoli na uniknięcie wykonywania kosztownych zadań szyfrowania protokołu SSL w kolektywie serwerów sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a6095-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="a6095-109">Odciążanie protokołu SSL upraszcza również konfigurowanie serwerów frontonu i zarządzanie aplikacją sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a6095-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="a6095-110">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="a6095-110">Scenario</span></span>

<span data-ttu-id="a6095-111">Poniższy scenariusz przechodzi przez konfigurowanie SSL odciążenia na istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6095-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="a6095-112">Scenariusz przyjęto założenie, że już zostały wykonane kroki, aby [Utwórz bramę aplikacji](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a6095-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a6095-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a6095-113">Before you begin</span></span>

<span data-ttu-id="a6095-114">Aby skonfigurować odciążanie protokołu SSL z bramy aplikacji, wymagany jest certyfikat.</span><span class="sxs-lookup"><span data-stu-id="a6095-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="a6095-115">Ten certyfikat jest załadowany na bramie aplikacji i używany do szyfrowania i odszyfrowywania ruchu wysyłane za pośrednictwem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="a6095-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="a6095-116">Ten certyfikat musi mieć format wymiana informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="a6095-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="a6095-117">Ten format pliku umożliwia klucz prywatny można wyeksportować co jest wymagane przez bramę aplikacji do szyfrowania i deszyfrowania ruchu.</span><span class="sxs-lookup"><span data-stu-id="a6095-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="a6095-118">Dodaj odbiornika protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="a6095-118">Add an HTTPS listener</span></span>

<span data-ttu-id="a6095-119">Odbiornik HTTPS jest szuka ruchu na podstawie konfiguracji i pomaga kierowania ruchu do pul zaplecza.</span><span class="sxs-lookup"><span data-stu-id="a6095-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="a6095-120">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a6095-120">Step 1</span></span>

<span data-ttu-id="a6095-121">Przejdź do portalu Azure i wybierz istniejącą bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="a6095-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="a6095-122">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a6095-122">Step 2</span></span>

<span data-ttu-id="a6095-123">Kliknij odbiorników i kliknij przycisk Dodaj, aby dodać odbiornik.</span><span class="sxs-lookup"><span data-stu-id="a6095-123">Click Listeners and click the Add button to add a listener.</span></span>

![Blok omówienie bramy aplikacji][1]

### <a name="step-3"></a><span data-ttu-id="a6095-125">Krok 3</span><span class="sxs-lookup"><span data-stu-id="a6095-125">Step 3</span></span>

<span data-ttu-id="a6095-126">Wprowadź wymagane informacje dla odbiornika i przekazywanie certyfikatu PFX, po zakończeniu kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="a6095-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="a6095-127">**Nazwa** — ta wartość jest przyjazną nazwę odbiornika.</span><span class="sxs-lookup"><span data-stu-id="a6095-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="a6095-128">**Konfiguracja adresu IP frontonu** — ta wartość jest konfiguracja adresu IP frontonu, która jest używana dla odbiornika.</span><span class="sxs-lookup"><span data-stu-id="a6095-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="a6095-129">**Portu frontonu (nazwa/Port)** — użyć przyjazną nazwę dla portu na frontonie bramy aplikacji i rzeczywistym portem.</span><span class="sxs-lookup"><span data-stu-id="a6095-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="a6095-130">**Protokół** — przełącznika do określania, jeśli http lub https jest używane dla frontonu.</span><span class="sxs-lookup"><span data-stu-id="a6095-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="a6095-131">**Certyfikat (nazwa/hasło)** — odciążania Jeśli protokół SSL jest używany, certyfikatu PFX jest wymagane dla tego ustawienia i przyjazną nazwę i hasło są wymagane.</span><span class="sxs-lookup"><span data-stu-id="a6095-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![Dodawanie bloku odbiornika][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="a6095-133">Utwórz regułę i powiązać ją do odbiornika</span><span class="sxs-lookup"><span data-stu-id="a6095-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="a6095-134">Odbiornik został utworzony.</span><span class="sxs-lookup"><span data-stu-id="a6095-134">The listener has now been created.</span></span> <span data-ttu-id="a6095-135">Nadszedł czas, aby utworzyć zasadę, aby obsługiwać ruch z odbiornika.</span><span class="sxs-lookup"><span data-stu-id="a6095-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="a6095-136">Zasady definiują sposób ruch jest kierowany do pul zaplecza, na podstawie wielu ustawień konfiguracji, w tym, czy koligacji na podstawie plików cookie sesji jest używana, protokół, port i sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="a6095-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="a6095-137">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a6095-137">Step 1</span></span>

<span data-ttu-id="a6095-138">Kliknij przycisk **reguły** bramy aplikacji, a następnie kliknij przycisk Dodaj.</span><span class="sxs-lookup"><span data-stu-id="a6095-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![Blok zasady bramy aplikacji][3]

### <a name="step-2"></a><span data-ttu-id="a6095-140">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a6095-140">Step 2</span></span>

<span data-ttu-id="a6095-141">Na **Dodaj podstawowe reguły** bloku, wpisz przyjazną nazwę reguły i wybierz polecenie odbiornika utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="a6095-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="a6095-142">Wybierz pulę zaplecza odpowiednie i ustawienia protokołu http, a następnie kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="a6095-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![Okno ustawień protokołu HTTPS][4]

<span data-ttu-id="a6095-144">Ustawienia są teraz zapisywane na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6095-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="a6095-145">Proces zapisywania dla tych ustawień może potrwać pewien czas, zanim staną się dostępne do wyświetlenia za pośrednictwem portalu lub przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a6095-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="a6095-146">Po zapisaniu bramy aplikacji obsługuje szyfrowania i odszyfrowywania ruchu.</span><span class="sxs-lookup"><span data-stu-id="a6095-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="a6095-147">Cały ruch między bramą aplikacji i serwerów sieci web zaplecza będą obsługiwane za pośrednictwem protokołu http.</span><span class="sxs-lookup"><span data-stu-id="a6095-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="a6095-148">Każdy komunikat do klienta, jeśli inicjowane przy użyciu protokołu https zostaną zwrócone do klienta szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="a6095-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6095-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6095-149">Next steps</span></span>

<span data-ttu-id="a6095-150">Aby dowiedzieć się, jak skonfigurować sondy kondycji niestandardowych z bramy aplikacji Azure, zobacz [utworzyć sondy kondycji niestandardowych](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a6095-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
