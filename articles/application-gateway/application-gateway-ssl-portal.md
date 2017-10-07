---
title: "aaaConfigure SSL odciążania — brama aplikacji w usłudze Azure - Portal Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu portalu hello"
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
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="de6f9-103">Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="de6f9-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="de6f9-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="de6f9-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="de6f9-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="de6f9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="de6f9-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="de6f9-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="de6f9-107">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="de6f9-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="de6f9-108">Brama aplikacji w Azure może być sesji protokołu Secure Sockets Layer (SSL) hello tooterminate skonfigurowanych na powitania bramy tooavoid kosztowne SSL odszyfrowywania zadania toohappen na powitania kolektywu serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="de6f9-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="de6f9-109">Odciążanie protokołu SSL także upraszcza powitania serwera frontonu Konfiguracja i zarządzanie hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="de6f9-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="de6f9-110">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="de6f9-110">Scenario</span></span>

<span data-ttu-id="de6f9-111">powitania po scenariusz przechodzi przez konfigurowanie SSL odciążenia na istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de6f9-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="de6f9-112">Witaj scenariuszu przyjęto założenie, że już zostały wykonane kroki hello zbyt[Utwórz bramę aplikacji](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="de6f9-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="de6f9-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="de6f9-113">Before you begin</span></span>

<span data-ttu-id="de6f9-114">tooconfigure odciążanie protokołu SSL z bramy aplikacji, wymagany jest certyfikat.</span><span class="sxs-lookup"><span data-stu-id="de6f9-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="de6f9-115">Ten certyfikat jest ładowany w bramie aplikacji hello i używany tooencrypt i odszyfrowywania ruchu hello wysyłane za pośrednictwem protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="de6f9-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="de6f9-116">certyfikat Hello musi toobe Format Wymiana informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="de6f9-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="de6f9-117">Tego formatu pliku umożliwia dla hello prywatnego klucza toobe wyeksportowane wymaganych przez hello aplikacji bramy tooperform hello szyfrowania i odszyfrowywania ruchu.</span><span class="sxs-lookup"><span data-stu-id="de6f9-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="de6f9-118">Dodaj odbiornika protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="de6f9-118">Add an HTTPS listener</span></span>

<span data-ttu-id="de6f9-119">odbiornik HTTPS Hello szuka ruchu na podstawie konfiguracji i pomaga pul zaplecza toohello ruchu hello trasy.</span><span class="sxs-lookup"><span data-stu-id="de6f9-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="de6f9-120">Krok 1</span><span class="sxs-lookup"><span data-stu-id="de6f9-120">Step 1</span></span>

<span data-ttu-id="de6f9-121">Przejdź toohello portalu Azure i wybierz istniejącą bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="de6f9-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="de6f9-122">Krok 2</span><span class="sxs-lookup"><span data-stu-id="de6f9-122">Step 2</span></span>

<span data-ttu-id="de6f9-123">Obiekty nasłuchujące i kliknij tooadd przycisku Dodaj hello odbiornik.</span><span class="sxs-lookup"><span data-stu-id="de6f9-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![Blok omówienie bramy aplikacji][1]

### <a name="step-3"></a><span data-ttu-id="de6f9-125">Krok 3</span><span class="sxs-lookup"><span data-stu-id="de6f9-125">Step 3</span></span>

<span data-ttu-id="de6f9-126">Wprowadź wymagane informacje dla odbiornika hello hello i przekazywania hello PFX certyfikatu, po zakończeniu kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="de6f9-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="de6f9-127">**Nazwa** — ta wartość jest przyjazna nazwa odbiorników hello.</span><span class="sxs-lookup"><span data-stu-id="de6f9-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="de6f9-128">**Konfiguracja adresu IP frontonu** — ta wartość jest hello konfiguracji adresu IP frontonu, służący do hello odbiornika.</span><span class="sxs-lookup"><span data-stu-id="de6f9-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="de6f9-129">**Portu frontonu (nazwa/Port)** -przyjazną nazwę dla hello port używany na powitania frontonu bramy aplikacji hello i port rzeczywiste hello używany.</span><span class="sxs-lookup"><span data-stu-id="de6f9-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="de6f9-130">**Protokół** — toodetermine przełącznika, jeśli frontonu hello jest używany http lub https.</span><span class="sxs-lookup"><span data-stu-id="de6f9-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="de6f9-131">**Certyfikat (nazwa/hasło)** — odciążania Jeśli protokół SSL jest używany, certyfikatu PFX jest wymagane dla tego ustawienia i przyjazną nazwę i hasło są wymagane.</span><span class="sxs-lookup"><span data-stu-id="de6f9-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![Dodawanie bloku odbiornika][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="de6f9-133">Utwórz regułę i powiązać ją odbiornika toohello</span><span class="sxs-lookup"><span data-stu-id="de6f9-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="de6f9-134">odbiornik Hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="de6f9-134">hello listener has now been created.</span></span> <span data-ttu-id="de6f9-135">Jest toocreate czasu reguły toohandle hello ruch z hello odbiornika.</span><span class="sxs-lookup"><span data-stu-id="de6f9-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="de6f9-136">Zasady definiują sposób ruch jest kierowany toohello pul zaplecza na podstawie wielu ustawień konfiguracji, w tym, czy koligacji na podstawie plików cookie sesji jest używana, protokół, port i sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="de6f9-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="de6f9-137">Krok 1</span><span class="sxs-lookup"><span data-stu-id="de6f9-137">Step 1</span></span>

<span data-ttu-id="de6f9-138">Kliknij przycisk hello **reguły** bramy aplikacji hello, a następnie kliknij przycisk Dodaj.</span><span class="sxs-lookup"><span data-stu-id="de6f9-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![Blok zasady bramy aplikacji][3]

### <a name="step-2"></a><span data-ttu-id="de6f9-140">Krok 2</span><span class="sxs-lookup"><span data-stu-id="de6f9-140">Step 2</span></span>

<span data-ttu-id="de6f9-141">Na powitania **Dodaj podstawowe reguły** bloku, wpisz przyjazną nazwę reguły hello hello i wybierz utworzony w poprzednim kroku hello odbiornika hello.</span><span class="sxs-lookup"><span data-stu-id="de6f9-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="de6f9-142">Wybierz pulę zaplecza odpowiednie hello i ustawienia protokołu http, a następnie kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="de6f9-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![Okno ustawień protokołu HTTPS][4]

<span data-ttu-id="de6f9-144">Ustawienia Hello są teraz zapisywane toohello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de6f9-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="de6f9-145">Hello Zapisz proces dla tych ustawień może trochę potrwać, zanim staną się dostępne tooview za pośrednictwem portalu hello lub za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de6f9-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="de6f9-146">Brama aplikacji hello raz zapisane obsługuje hello szyfrowania i odszyfrowywania ruchu.</span><span class="sxs-lookup"><span data-stu-id="de6f9-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="de6f9-147">Cały ruch między bramą aplikacji hello i serwerów sieci web zaplecza hello będą obsługiwane za pośrednictwem protokołu http.</span><span class="sxs-lookup"><span data-stu-id="de6f9-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="de6f9-148">Dowolnego klienta do tyłu toohello komunikacji Jeśli inicjowane przy użyciu protokołu https, zostanie zwrócony klienta toohello szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="de6f9-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de6f9-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de6f9-149">Next steps</span></span>

<span data-ttu-id="de6f9-150">toolearn tooconfigure niestandardowych kondycji sondowania z bramy aplikacji Azure, zobacz [utworzyć sondy kondycji niestandardowych](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="de6f9-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
