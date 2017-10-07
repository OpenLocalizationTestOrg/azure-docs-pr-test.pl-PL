---
title: "aaaCreate bramę aplikacji Azure — 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate bramę aplikacji przy użyciu hello Azure CLI 2.0 w Menedżerze zasobów"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="47f8e-103">Tworzenie bramy aplikacji przy użyciu hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="47f8e-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="47f8e-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="47f8e-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="47f8e-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="47f8e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="47f8e-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="47f8e-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="47f8e-107">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="47f8e-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="47f8e-108">Interfejs wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="47f8e-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="47f8e-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="47f8e-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="47f8e-110">Brama aplikacji jest dedykowany urządzenie wirtualne, która udostępnia kontroler dostarczania aplikacji (ADC) jako usługa, oferty różnych warstwy 7 załadować równoważenia możliwości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47f8e-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="47f8e-111">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="47f8e-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="47f8e-112">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="47f8e-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="47f8e-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.</span><span class="sxs-lookup"><span data-stu-id="47f8e-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="47f8e-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="47f8e-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="47f8e-115">Wymagania wstępne: Instalacja hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="47f8e-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="47f8e-116">Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="47f8e-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="47f8e-117">Jeśli nie masz konta platformy Azure, można je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="47f8e-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="47f8e-118">Zarejestruj się, aby skorzystać z [bezpłatnego demo](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="47f8e-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="47f8e-119">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="47f8e-119">Scenario</span></span>

<span data-ttu-id="47f8e-120">W tym scenariuszu możesz dowiedzieć się, jak bramy aplikacji przy użyciu toocreate hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47f8e-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="47f8e-121">W tym scenariuszu obejmują:</span><span class="sxs-lookup"><span data-stu-id="47f8e-121">This scenario will:</span></span>

* <span data-ttu-id="47f8e-122">Utwórz bramę aplikacji średnia z dwóch wystąpień.</span><span class="sxs-lookup"><span data-stu-id="47f8e-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="47f8e-123">Tworzenie sieci wirtualnej o nazwie AdatumAppGatewayVNET z zarezerwowanym blokiem CIDR 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="47f8e-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="47f8e-124">Tworzenie podsieci o nazwie Appgatewaysubnet używającej bloku 10.0.0.0/28 jako bloku CIDR.</span><span class="sxs-lookup"><span data-stu-id="47f8e-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="47f8e-125">Dodatkowa konfiguracja bramy aplikacji hello, w tym kondycji niestandardowych sondy, adresy w puli zaplecza i dodatkowe reguły są konfigurowane po skonfigurowaniu bramy aplikacji hello i nie podczas pierwszego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="47f8e-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="47f8e-126">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="47f8e-126">Before you begin</span></span>

<span data-ttu-id="47f8e-127">Brama aplikacji w Azure wymaga jego własnej podsieci.</span><span class="sxs-lookup"><span data-stu-id="47f8e-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="47f8e-128">Podczas tworzenia sieci wirtualnej, upewnij się, pozostaw toohave miejsce za mało adresów wielu podsieci.</span><span class="sxs-lookup"><span data-stu-id="47f8e-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="47f8e-129">Po wdrożeniu tooa podsieci bramy aplikacji bramy tylko dodatkowych aplikacji można dodać podsieci toohello.</span><span class="sxs-lookup"><span data-stu-id="47f8e-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="47f8e-130">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="47f8e-130">Log in tooAzure</span></span>

<span data-ttu-id="47f8e-131">Otwórz hello **wiersza polecenia usługi Microsoft Azure**i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="47f8e-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="47f8e-132">Można również użyć `az login` bez hello przełącznika dla nazwy logowania urządzenia, która wymaga wprowadzenie kodu na aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="47f8e-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="47f8e-133">Po wpisaniu hello poprzedzających przykład znajduje się kod.</span><span class="sxs-lookup"><span data-stu-id="47f8e-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="47f8e-134">Przejdź toohttps://aka.ms/devicelogin w procesie logowania hello toocontinue przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="47f8e-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd przedstawiający urządzenia logowania][1]

<span data-ttu-id="47f8e-136">W przeglądarce hello wprowadź otrzymany kod hello.</span><span class="sxs-lookup"><span data-stu-id="47f8e-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="47f8e-137">Jesteś tooa przekierowanego strony logowania.</span><span class="sxs-lookup"><span data-stu-id="47f8e-137">You are redirected tooa sign-in page.</span></span>

![Kod tooenter przeglądarki][2]

<span data-ttu-id="47f8e-139">Po wprowadzeniu kodu hello użytkownik jest zalogowany, zamknij hello toocontinue przeglądarki ze scenariuszem hello.</span><span class="sxs-lookup"><span data-stu-id="47f8e-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![pomyślnie zalogował się][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="47f8e-141">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="47f8e-141">Create hello resource group</span></span>

<span data-ttu-id="47f8e-142">Przed utworzeniem bramy aplikacji hello, grupy zasobów jest utworzyć bramę aplikacji hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="47f8e-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="47f8e-143">Oto Hello hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="47f8e-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="47f8e-144">Utwórz bramę aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="47f8e-144">Create hello application gateway</span></span>

<span data-ttu-id="47f8e-145">Hello adresy IP używane dla hello wewnętrznej bazy danych są adresami IP powitania serwera wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="47f8e-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="47f8e-146">Te wartości można albo prywatnych adresów IP w sieci wirtualnej hello, publiczne adresy IP lub nazwy FQDN dla serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="47f8e-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="47f8e-147">Witaj poniższy przykład tworzy bramę aplikacji przy użyciu ustawień konfiguracyjnych dodatkowe ustawienia protokołu http, porty i zasady.</span><span class="sxs-lookup"><span data-stu-id="47f8e-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="47f8e-148">Hello poprzednim przykładzie pokazano wiele właściwości, które nie są wymagane podczas tworzenia hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47f8e-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="47f8e-149">Witaj poniższy przykład kodu tworzy bramę aplikacji hello wymagane informacje.</span><span class="sxs-lookup"><span data-stu-id="47f8e-149">hello following code example creates an application gateway with hello required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="47f8e-150">Aby uzyskać listę parametrów, które można podać podczas hello tworzenia, uruchom następujące polecenie: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="47f8e-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="47f8e-151">W tym przykładzie tworzy bramę aplikacji w warstwie podstawowa z domyślnych ustawień odbiornika hello, puli zaplecza, ustawienia http zaplecza i zasady.</span><span class="sxs-lookup"><span data-stu-id="47f8e-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="47f8e-152">Możesz zmodyfikować toosuit te ustawienia wdrożenia po aprowizacji hello zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="47f8e-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="47f8e-153">Jeśli masz już aplikację sieci web zdefiniowane z puli zaplecza hello w hello w poprzednich krokach utworzono raz, równoważenie obciążenia sieciowego rozpoczyna się.</span><span class="sxs-lookup"><span data-stu-id="47f8e-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="47f8e-154">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="47f8e-154">Get application gateway DNS name</span></span>

<span data-ttu-id="47f8e-155">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="47f8e-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="47f8e-156">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="47f8e-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="47f8e-157">Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="47f8e-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="47f8e-158">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="47f8e-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="47f8e-159">tooconfigure aliasu, pobrać szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone.</span><span class="sxs-lookup"><span data-stu-id="47f8e-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="47f8e-160">Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS.</span><span class="sxs-lookup"><span data-stu-id="47f8e-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="47f8e-161">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47f8e-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a><span data-ttu-id="47f8e-162">Usuwanie wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="47f8e-162">Delete all resources</span></span>

<span data-ttu-id="47f8e-163">toodelete wszystkie zasoby są tworzone w tym artykule pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="47f8e-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="47f8e-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47f8e-164">Next steps</span></span>

<span data-ttu-id="47f8e-165">Dowiedz się, jak sondy kondycji niestandardowych toocreate odwiedzając [utworzyć sondy kondycji niestandardowych](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="47f8e-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="47f8e-166">Dowiedz się, jak tooconfigure odciążanie protokołu SSL i kosztowne odszyfrowywania SSL podjęcia hello wyłączone serwerów sieci web, odwiedzając [skonfigurować odciążanie protokołu SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="47f8e-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
