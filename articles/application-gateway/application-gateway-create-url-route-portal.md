---
title: "aaaCreate na podstawie ścieżki reguły — brama aplikacji w usłudze Azure - Portal Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate reguły na podstawie ścieżki dla bramy aplikacji przy użyciu hello portalu"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="3d92f-103">Tworzenie reguły na podstawie ścieżki dla bramy aplikacji przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="3d92f-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d92f-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3d92f-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="3d92f-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d92f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="3d92f-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="3d92f-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="3d92f-107">Na podstawie ścieżki routingu adresów URL umożliwia możesz tooassociate tras na podstawie hello ścieżki adresu URL żądania Http.</span><span class="sxs-lookup"><span data-stu-id="3d92f-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="3d92f-108">Sprawdza, czy jest skonfigurowane dla adresu URL hello na liście hello brama aplikacji w puli zaplecza tooa trasy, a wysyła toohello ruchu sieciowego hello zdefiniowanymi w puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="3d92f-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="3d92f-109">Użycia routingu opartego na adres URL jest tooload równoważenie żądań dla pul serwerów zaplecza toodifferent różne typy zawartości.</span><span class="sxs-lookup"><span data-stu-id="3d92f-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="3d92f-110">Na podstawie adresu URL routingu wprowadza nową bramę tooapplication typ reguły.</span><span class="sxs-lookup"><span data-stu-id="3d92f-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="3d92f-111">Brama aplikacji ma dwa typy zasad: zasady podstawowe i na podstawie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="3d92f-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="3d92f-112">Witaj typu podstawowe reguły, zapewnia usługi okrężnego dla zaplecza hello pul podczas reguły ścieżki dodatkowo dystrybucji działania okrężnego tooround, uwzględnia również wzorzec ścieżki adresu URL żądania hello podczas wybierania puli zaplecza odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="3d92f-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="3d92f-113">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="3d92f-113">Scenario</span></span>

<span data-ttu-id="3d92f-114">Witaj następujący scenariusz przechodzi przez utworzenie w istniejącą bramę aplikacji na podstawie ścieżki reguły.</span><span class="sxs-lookup"><span data-stu-id="3d92f-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="3d92f-115">Witaj scenariuszu przyjęto założenie, że już zostały wykonane kroki hello zbyt[Utwórz bramę aplikacji](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3d92f-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![trasy adresu URL][scenario]

## <span data-ttu-id="3d92f-117"><a name="createrule"></a>Tworzenie reguły na podstawie ścieżki hello</span><span class="sxs-lookup"><span data-stu-id="3d92f-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="3d92f-118">Reguły na podstawie ścieżki wymaga własnego odbiornika, przed utworzeniem reguły hello można tooverify się, że masz toouse dostępne odbiornika.</span><span class="sxs-lookup"><span data-stu-id="3d92f-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="3d92f-119">Krok 1</span><span class="sxs-lookup"><span data-stu-id="3d92f-119">Step 1</span></span>

<span data-ttu-id="3d92f-120">Przejdź toohello [portalu Azure](http://portal.azure.com) i wybierz istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3d92f-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="3d92f-121">Kliknij przycisk **reguły**</span><span class="sxs-lookup"><span data-stu-id="3d92f-121">Click **Rules**</span></span>

![Application Gateway — omówienie][1]

### <a name="step-2"></a><span data-ttu-id="3d92f-123">Krok 2</span><span class="sxs-lookup"><span data-stu-id="3d92f-123">Step 2</span></span>

<span data-ttu-id="3d92f-124">Kliknij przycisk **na podstawie ścieżki** tooadd przycisk nowej reguły na podstawie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="3d92f-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="3d92f-125">Krok 3</span><span class="sxs-lookup"><span data-stu-id="3d92f-125">Step 3</span></span>

<span data-ttu-id="3d92f-126">Witaj **reguły na podstawie ścieżki Dodaj** bloku ma dwie sekcje.</span><span class="sxs-lookup"><span data-stu-id="3d92f-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="3d92f-127">Pierwsza sekcja Hello jest, gdzie są zdefiniowane hello odbiornika, nazwa hello hello reguły i ustawienia ścieżki domyślnej hello.</span><span class="sxs-lookup"><span data-stu-id="3d92f-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="3d92f-128">ustawienia ścieżki domyślna Hello są dla tras, które nie są objęte hello niestandardowej ścieżki na podstawie trasy.</span><span class="sxs-lookup"><span data-stu-id="3d92f-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="3d92f-129">Witaj drugiej sekcji hello **reguły na podstawie ścieżki Dodaj** bloku jest, gdzie został zdefiniowany hello ścieżki reguły oparte na siebie.</span><span class="sxs-lookup"><span data-stu-id="3d92f-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="3d92f-130">**Ustawienia podstawowe**</span><span class="sxs-lookup"><span data-stu-id="3d92f-130">**Basic Settings**</span></span>

* <span data-ttu-id="3d92f-131">**Nazwa** — ta wartość jest regułą toohello przyjazną nazwę dostępnej w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="3d92f-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="3d92f-132">**Odbiornik** — ta wartość jest hello odbiornik, który jest używany dla hello reguły.</span><span class="sxs-lookup"><span data-stu-id="3d92f-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="3d92f-133">**Domyślna pula zaplecza** — to ustawienie jest ustawieniem hello, definiujący toobe zaplecza hello używany dla reguły domyślnej hello</span><span class="sxs-lookup"><span data-stu-id="3d92f-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="3d92f-134">**Domyślne ustawienia HTTP** — to ustawienie jest ustawienie hello, który definiuje toobe ustawienia HTTP hello używany dla reguły domyślnej hello.</span><span class="sxs-lookup"><span data-stu-id="3d92f-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="3d92f-135">**Reguły ścieżki**</span><span class="sxs-lookup"><span data-stu-id="3d92f-135">**Path-based rules**</span></span>

* <span data-ttu-id="3d92f-136">**Nazwa** — ta wartość jest przyjazną nazwę reguły na podstawie toopath.</span><span class="sxs-lookup"><span data-stu-id="3d92f-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="3d92f-137">**Ścieżki** — to ustawienie określa hello ścieżki hello reguły szuka podczas przesyłania ruchu</span><span class="sxs-lookup"><span data-stu-id="3d92f-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="3d92f-138">**Puli zaplecza** — to ustawienie jest ustawieniem hello, definiujący hello toobe zaplecza dla reguły hello używane</span><span class="sxs-lookup"><span data-stu-id="3d92f-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="3d92f-139">**Ustawienie HTTP** — to ustawienie jest ustawieniem hello, definiujący toobe ustawienia HTTP hello używany dla reguły hello.</span><span class="sxs-lookup"><span data-stu-id="3d92f-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d92f-140">Ścieżki: Lista hello ścieżka toomatch wzorców.</span><span class="sxs-lookup"><span data-stu-id="3d92f-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="3d92f-141">Każdy musi rozpoczynać się od / i miejsce tylko hello "\*" jest dozwolona znajduje się na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="3d92f-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="3d92f-142">Nieprawidłowa przykładów /xyz, /xyz* lub/xyz / *.</span><span class="sxs-lookup"><span data-stu-id="3d92f-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Dodawanie bloku reguły na podstawie ścieżki z informacjami o wypełnione][2]

<span data-ttu-id="3d92f-144">Dodawanie tooan reguły na podstawie ścieżki istniejącą bramę aplikacji jest łatwy za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="3d92f-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="3d92f-145">Po utworzeniu reguły na podstawie ścieżki, może być edytowany tooadd dodatkowe reguły.</span><span class="sxs-lookup"><span data-stu-id="3d92f-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![Dodawanie dodatkowych reguły ścieżki][3]

<span data-ttu-id="3d92f-147">Ten krok obejmuje skonfigurowanie trasę na podstawie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="3d92f-147">This step configures a path-based route.</span></span> <span data-ttu-id="3d92f-148">Jest ważne toounderstand, że żądania są nie ulegną, jak żądania są dostępne w bramy aplikacji sprawdza żądania hello oraz basic na powitania adresu url wzorca Wysyła hello żądania toohello odpowiednie zaplecza.</span><span class="sxs-lookup"><span data-stu-id="3d92f-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d92f-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d92f-149">Next steps</span></span>

<span data-ttu-id="3d92f-150">toolearn tooconfigure odciążanie protokołu SSL z bramy aplikacji Azure, zobacz temat [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3d92f-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
