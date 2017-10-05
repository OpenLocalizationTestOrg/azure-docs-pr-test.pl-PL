---
title: "Utwórz bramę aplikacji Azure — Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć bramę aplikacji przy użyciu 1.0 interfejsu wiersza polecenia Azure Resource Manager"
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
ms.openlocfilehash: e7b16e789e0f241aa8ca2292aacb2bccde8777ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli"></a><span data-ttu-id="1b9aa-103">Tworzenie bramy aplikacji przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1b9aa-103">Create an application gateway by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b9aa-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1b9aa-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="1b9aa-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b9aa-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="1b9aa-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b9aa-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="1b9aa-107">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b9aa-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="1b9aa-108">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1b9aa-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="1b9aa-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1b9aa-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="1b9aa-110">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="1b9aa-111">Udostępnia tryb failover, oparty na wydajności routing żądań HTTP między różnymi serwerami — w chmurze i lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="1b9aa-112">Brama aplikacji w zawiera następujące funkcje dostarczania aplikacji: HTTP załadować sondy kondycji niestandardowych równoważenia koligacji na podstawie plików cookie sesji i odciążanie protokołu Secure Sockets Layer (SSL) i obsługę wielu lokacji.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-the-azure-cli"></a><span data-ttu-id="1b9aa-113">Wymaganie wstępne: Instalowanie interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1b9aa-113">Prerequisite: Install the Azure CLI</span></span>

<span data-ttu-id="1b9aa-114">Aby wykonać kroki opisane w tym artykule, należy [instalowanie interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](../xplat-cli-install.md) i trzeba [Zaloguj się do usługi Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="1b9aa-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="1b9aa-115">Jeśli nie masz konta platformy Azure, można je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="1b9aa-116">Zarejestruj się, aby skorzystać z [bezpłatnego demo](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="1b9aa-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="1b9aa-117">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="1b9aa-117">Scenario</span></span>

<span data-ttu-id="1b9aa-118">W tym scenariuszu Dowiedz się jak utworzyć bramę aplikacji przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="1b9aa-119">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="1b9aa-119">This scenario will:</span></span>

* <span data-ttu-id="1b9aa-120">Utwórz bramę aplikacji średnia z dwóch wystąpień.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="1b9aa-121">Tworzenie sieci wirtualnej o nazwie ContosoVNET z zarezerwowanym blokiem CIDR 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="1b9aa-122">Utwórz podsieć o nazwie subnet01, która używa 10.0.0.0/28 bloku CIDR.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="1b9aa-123">Dodatkowa konfiguracja bramy aplikacji, w tym kondycji niestandardowych sondy, adresy w puli zaplecza i dodatkowe reguły są konfigurowane po skonfigurowaniu bramy aplikacji i nie podczas pierwszego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-123">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1b9aa-124">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1b9aa-124">Before you begin</span></span>

<span data-ttu-id="1b9aa-125">Brama aplikacji w Azure wymaga jego własnej podsieci.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="1b9aa-126">Podczas tworzenia sieci wirtualnej, upewnij się, że pozostanie wystarczająco dużo przestrzeni adresowej do mają wiele podsieci.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-126">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="1b9aa-127">Po wdrożono bramę aplikacji do podsieci bramy aplikacji tylko dodatkowe mogą mają zostać dodane do tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-127">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="1b9aa-128">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-128">Log in to Azure</span></span>

<span data-ttu-id="1b9aa-129">Otwórz **wiersza polecenia usługi Microsoft Azure**i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-129">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="1b9aa-130">Po wpisaniu powyższego przykładu znajduje się kod.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-130">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="1b9aa-131">Przejdź do https://aka.ms/devicelogin w przeglądarce, aby kontynuować proces logowania.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-131">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd przedstawiający urządzenia logowania][1]

<span data-ttu-id="1b9aa-133">W przeglądarce wprowadź otrzymany kod.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-133">In the browser, enter the code you received.</span></span> <span data-ttu-id="1b9aa-134">Nastąpi przekierowanie do strony logowania.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-134">You are redirected to a sign-in page.</span></span>

![przeglądarki, aby wprowadzić kod][2]

<span data-ttu-id="1b9aa-136">Po wprowadzeniu kodu użytkownik jest zalogowany, zamknij przeglądarkę, aby kontynuować na ze scenariuszem.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-136">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![pomyślnie zalogował się][3]

## <a name="switch-to-resource-manager-mode"></a><span data-ttu-id="1b9aa-138">Przełącz tryb Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b9aa-138">Switch to Resource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-the-resource-group"></a><span data-ttu-id="1b9aa-139">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="1b9aa-139">Create the resource group</span></span>

<span data-ttu-id="1b9aa-140">Przed utworzeniem bramy aplikacji, tworzona jest grupa zasobów zawiera bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-140">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="1b9aa-141">Poniżej przedstawiono polecenia.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-141">The following shows the command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="1b9aa-142">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1b9aa-142">Create a virtual network</span></span>

<span data-ttu-id="1b9aa-143">Po utworzeniu grupy zasobów sieci wirtualnej jest tworzona dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-143">Once the resource group is created, a virtual network is created for the application gateway.</span></span>  <span data-ttu-id="1b9aa-144">W poniższym przykładzie przestrzeni adresowej został jako 10.0.0.0/16 zgodnie z definicją w uwagach do poprzedniego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-144">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="1b9aa-145">Tworzenie podsieci</span><span class="sxs-lookup"><span data-stu-id="1b9aa-145">Create a subnet</span></span>

<span data-ttu-id="1b9aa-146">Po utworzeniu sieci wirtualnej podsieci jest dodawany do bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-146">After the virtual network is created, a subnet is added for the application gateway.</span></span>  <span data-ttu-id="1b9aa-147">Jeśli zamierzasz korzystać z bramy aplikacji z aplikacją sieci web hostowanej w tej samej sieci wirtualnej co brama aplikacji, należy pozostawić wystarczająco dużo miejsca w innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-147">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="1b9aa-148">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="1b9aa-148">Create the application gateway</span></span>

<span data-ttu-id="1b9aa-149">Po utworzeniu sieci wirtualnej i podsieci wymagania wstępne dla bramy aplikacji są spełnione.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-149">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="1b9aa-150">Ponadto PFX wcześniej wyeksportowany certyfikat i hasło dla certyfikatu są wymagane dla następujący krok: adresy IP używane do wewnętrznej bazy danych są adresami IP dla serwera wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-150">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="1b9aa-151">Te wartości można prywatnych adresów IP w sieci wirtualnej, publiczne adresy IP lub nazwy FQDN dla serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-151">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

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
> <span data-ttu-id="1b9aa-152">Lista parametrów, które można podać podczas tworzenia, uruchom następujące polecenie: **brama aplikacji w sieci azure, Utwórz — Pomoc**.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-152">For a list of parameters that can be provided during creation run the following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="1b9aa-153">W tym przykładzie tworzy bramę aplikacji w warstwie podstawowa z domyślnych ustawień odbiornika, puli zaplecza, ustawienia http zaplecza i zasady.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-153">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="1b9aa-154">Można zmodyfikować te ustawienia do wdrożenia po udostępnianie zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-154">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="1b9aa-155">Jeśli masz już aplikację sieci web zdefiniowane z puli zaplecza w poprzednich krokach utworzono raz, równoważenie obciążenia sieciowego rozpoczyna się.</span><span class="sxs-lookup"><span data-stu-id="1b9aa-155">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b9aa-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b9aa-156">Next steps</span></span>

<span data-ttu-id="1b9aa-157">Dowiedz się, jak utworzyć sondy kondycji niestandardowych odwiedzając [utworzyć sondy kondycji niestandardowych](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1b9aa-157">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="1b9aa-158">Dowiedz się, jak skonfigurować odciążanie protokołu SSL i podejmij kosztowne odszyfrowywania SSL poza serwerów sieci web, odwiedzając [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="1b9aa-158">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
