---
title: "aaaCreate bramę aplikacji Azure — 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate bramę aplikacji przy użyciu hello Azure CLI 1.0 w Menedżerze zasobów"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="84f6c-103">Tworzenie bramy aplikacji przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="84f6c-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="84f6c-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="84f6c-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="84f6c-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="84f6c-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="84f6c-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="84f6c-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="84f6c-107">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="84f6c-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="84f6c-108">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="84f6c-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="84f6c-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="84f6c-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="84f6c-110">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="84f6c-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="84f6c-111">Zapewnia on trybu failover, wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="84f6c-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="84f6c-112">Brama aplikacji ma następujące funkcje dostarczania aplikacji hello: HTTP załadować sondy kondycji niestandardowych równoważenia koligacji na podstawie plików cookie sesji i odciążanie protokołu Secure Sockets Layer (SSL) i obsługę wielu lokacji.</span><span class="sxs-lookup"><span data-stu-id="84f6c-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="84f6c-113">Wymagania wstępne: Instalacja hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="84f6c-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="84f6c-114">Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](../xplat-cli-install.md) i potrzebna jest zbyt[logowania tooAzure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="84f6c-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="84f6c-115">Jeśli nie masz konta platformy Azure, można je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="84f6c-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="84f6c-116">Zarejestruj się, aby skorzystać z [bezpłatnego demo](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="84f6c-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="84f6c-117">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="84f6c-117">Scenario</span></span>

<span data-ttu-id="84f6c-118">W tym scenariuszu możesz dowiedzieć się, jak bramy aplikacji przy użyciu toocreate hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="84f6c-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="84f6c-119">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="84f6c-119">This scenario will:</span></span>

* <span data-ttu-id="84f6c-120">Utwórz bramę aplikacji średnia z dwóch wystąpień.</span><span class="sxs-lookup"><span data-stu-id="84f6c-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="84f6c-121">Tworzenie sieci wirtualnej o nazwie ContosoVNET z zarezerwowanym blokiem CIDR 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="84f6c-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="84f6c-122">Utwórz podsieć o nazwie subnet01, która używa 10.0.0.0/28 bloku CIDR.</span><span class="sxs-lookup"><span data-stu-id="84f6c-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="84f6c-123">Dodatkowa konfiguracja bramy aplikacji hello, w tym kondycji niestandardowych sondy, adresy w puli zaplecza i dodatkowe reguły są konfigurowane po skonfigurowaniu bramy aplikacji hello i nie podczas pierwszego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="84f6c-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="84f6c-124">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="84f6c-124">Before you begin</span></span>

<span data-ttu-id="84f6c-125">Brama aplikacji w Azure wymaga jego własnej podsieci.</span><span class="sxs-lookup"><span data-stu-id="84f6c-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="84f6c-126">Podczas tworzenia sieci wirtualnej, upewnij się, pozostaw toohave miejsce za mało adresów wielu podsieci.</span><span class="sxs-lookup"><span data-stu-id="84f6c-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="84f6c-127">Po wdrożeniu tooa podsieci bramy aplikacji jedynymi dodatkowymi aplikacji bramy są toobe można dodać podsieci toohello.</span><span class="sxs-lookup"><span data-stu-id="84f6c-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="84f6c-128">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="84f6c-128">Log in tooAzure</span></span>

<span data-ttu-id="84f6c-129">Otwórz hello **wiersza polecenia usługi Microsoft Azure**i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="84f6c-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="84f6c-130">Po wpisaniu hello poprzedzających przykład znajduje się kod.</span><span class="sxs-lookup"><span data-stu-id="84f6c-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="84f6c-131">Przejdź toohttps://aka.ms/devicelogin w procesie logowania hello toocontinue przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="84f6c-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd przedstawiający urządzenia logowania][1]

<span data-ttu-id="84f6c-133">W przeglądarce hello wprowadź otrzymany kod hello.</span><span class="sxs-lookup"><span data-stu-id="84f6c-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="84f6c-134">Jesteś tooa przekierowanego strony logowania.</span><span class="sxs-lookup"><span data-stu-id="84f6c-134">You are redirected tooa sign-in page.</span></span>

![Kod tooenter przeglądarki][2]

<span data-ttu-id="84f6c-136">Po wprowadzeniu kodu hello użytkownik jest zalogowany, zamknij hello toocontinue przeglądarki ze scenariuszem hello.</span><span class="sxs-lookup"><span data-stu-id="84f6c-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![pomyślnie zalogował się][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="84f6c-138">Przełącz tryb Manager tooResource</span><span class="sxs-lookup"><span data-stu-id="84f6c-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="84f6c-139">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="84f6c-139">Create hello resource group</span></span>

<span data-ttu-id="84f6c-140">Przed utworzeniem bramy aplikacji hello, grupy zasobów jest utworzyć bramę aplikacji hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="84f6c-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="84f6c-141">Oto Hello hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="84f6c-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="84f6c-142">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="84f6c-142">Create a virtual network</span></span>

<span data-ttu-id="84f6c-143">Po utworzeniu grupy zasobów hello sieci wirtualnej jest tworzona dla bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="84f6c-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="84f6c-144">W hello poniższy przykład przestrzeni adresowej hello było jako 10.0.0.0/16 zgodnie z definicją w hello poprzedzających uwagi scenariusza.</span><span class="sxs-lookup"><span data-stu-id="84f6c-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="84f6c-145">Tworzenie podsieci</span><span class="sxs-lookup"><span data-stu-id="84f6c-145">Create a subnet</span></span>

<span data-ttu-id="84f6c-146">Po utworzeniu sieci wirtualnej hello podsieci jest dodawany do bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="84f6c-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="84f6c-147">Jeśli planujesz toouse brama aplikacji w aplikacji sieci web hostowanych w hello sam wirtualnych sieci jako bramę aplikacji hello, za mało miejsca w innej podsieci, czy tooleave.</span><span class="sxs-lookup"><span data-stu-id="84f6c-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="84f6c-148">Utwórz bramę aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="84f6c-148">Create hello application gateway</span></span>

<span data-ttu-id="84f6c-149">Po utworzeniu sieci wirtualnej hello i podsieć hello wymagania wstępne dla bramy aplikacji hello są spełnione.</span><span class="sxs-lookup"><span data-stu-id="84f6c-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="84f6c-150">Ponadto hasło certyfikatu i hello wcześniej eksportowanego pliku PFX certyfikatu hello są wymagane dla powitania po kroku: hello adresy IP używane dla zaplecza hello są hello adresów IP dla serwera wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="84f6c-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="84f6c-151">Te wartości można albo prywatnych adresów IP w sieci wirtualnej hello, publiczne adresy IP lub nazwy FQDN dla serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="84f6c-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="84f6c-152">Lista parametrów, które można podać podczas tworzenia, uruchom następujące polecenie hello: **brama aplikacji w sieci azure, Utwórz — Pomoc**.</span><span class="sxs-lookup"><span data-stu-id="84f6c-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="84f6c-153">W tym przykładzie tworzy bramę aplikacji w warstwie podstawowa z domyślnych ustawień odbiornika hello, puli zaplecza, ustawienia http zaplecza i zasady.</span><span class="sxs-lookup"><span data-stu-id="84f6c-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="84f6c-154">Możesz zmodyfikować toosuit te ustawienia wdrożenia po aprowizacji hello zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="84f6c-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="84f6c-155">Jeśli masz już aplikację sieci web zdefiniowane z puli zaplecza hello w hello w poprzednich krokach utworzono raz, równoważenie obciążenia sieciowego rozpoczyna się.</span><span class="sxs-lookup"><span data-stu-id="84f6c-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84f6c-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84f6c-156">Next steps</span></span>

<span data-ttu-id="84f6c-157">Dowiedz się, jak sondy kondycji niestandardowych toocreate odwiedzając [utworzyć sondy kondycji niestandardowych](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="84f6c-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="84f6c-158">Dowiedz się, jak tooconfigure odciążanie protokołu SSL i kosztowne odszyfrowywania SSL podjęcia hello wyłączone serwerów sieci web, odwiedzając [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="84f6c-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
