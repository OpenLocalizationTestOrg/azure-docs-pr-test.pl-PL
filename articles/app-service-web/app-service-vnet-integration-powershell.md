---
title: "aaaConnect Twojej sieci wirtualnej tooyour aplikacji przy użyciu programu PowerShell"
description: "Instrukcje dotyczące działania tooconnect tooand z sieci wirtualnych za pomocą programu PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>Połączenie sieci wirtualnej tooyour aplikacji przy użyciu programu PowerShell
## <a name="overview"></a>Omówienie
W usłudze Azure App Service można połączyć aplikacji (sieć web, mobilnych lub interfejsu API) tooan sieci wirtualnej platformy Azure (VNet) w ramach subskrypcji. Ta funkcja jest nazywana integracji sieci wirtualnej. Funkcja integracji z sieciami wirtualnymi Hello nie należy mylić z funkcją środowiska usługi aplikacji hello, dzięki czemu można toorun wystąpienia usługi Azure App Service w Twojej sieci wirtualnej.

Funkcja integracji z sieciami wirtualnymi Hello ma interfejsu użytkownika (UI) w hello nowego portalu służącego toointegrate z sieciami wirtualnymi, które zostały wdrożone przy użyciu modelu wdrażania usługi Azure Resource Manager hello albo hello klasycznego modelu wdrażania. Aby uzyskać dodatkowe informacje o funkcji hello toolearn zobacz [integracji aplikacji z sieci wirtualnej platformy Azure](web-sites-integrate-with-vnet.md).

Ten artykuł zawiera nie na temat sposobu toouse hello interfejsu użytkownika, ale raczej dotyczące integracji tooenable przy użyciu programu PowerShell. Ponieważ hello poleceń dla każdego modelu wdrażania są różne, w tym artykule ma sekcji do każdego modelu wdrażania.  

Przed kontynuowaniem w tym artykule upewnij się, że masz:

* Witaj, zainstalowany najnowszy zestaw SDK usługi Azure PowerShell. Można go zainstalować z hello Instalatora platformy sieci Web.
* Aplikacja w usłudze Azure App Service w Standard lub Premium jednostki SKU.

## <a name="classic-virtual-networks"></a>Klasycznych sieci wirtualnych
W tej sekcji opisano trzy zadania dla sieci wirtualnych korzystających z hello klasycznego modelu wdrażania:

1. Łączenie aplikacji tooa istniejących sieci wirtualnej i jest konfigurowane połączenie punkt lokacja z bramą.
2. Aktualizowanie informacji o integracji sieci wirtualnej dla aplikacji.
3. Aplikację można rozłączyć sieci wirtualnej.

### <a name="connect-an-app-tooa-classic-vnet"></a>Połącz tooa aplikacji klasycznej sieci wirtualnej
tooconnect aplikacji tooa sieci wirtualnej, wykonaj następujące trzy kroki:

1. Deklarowanie toohello aplikacji sieci web, że zostanie do niej dołączanie do określonej sieci wirtualnej. Aplikacja Hello wygeneruje certyfikat, który będzie mógł skorzystać z sieci wirtualnej toohello połączenia punkt lokacja.
2. Przekaż hello web app certyfikatu toohello wirtualnej sieci, a następnie pobrać hello identyfikator URI pakietu sieci VPN punkt lokacja.
3. Zaktualizuj połączenie sieci wirtualnej aplikacji sieci web hello z pakietem punkt lokacja hello identyfikatora URI.

Witaj pierwszy i trzeci kroki są w pełni skryptowe, ale drugi etap hello wymaga jednorazowe, ręczna Akcja za pośrednictwem portalu hello lub tooperform dostępu **PUT** lub **poprawka** akcje na powitania sieci wirtualnej Usługa Azure Resource Manager punktu końcowego. Skontaktuj się z pomocą techniczną platformy Azure toohave to włączone. Przed rozpoczęciem upewnij się, czy masz klasycznego siecią wirtualną, która ma już włączone połączenie punkt lokacja i wdrożone bramę. toocreate hello bramy i Włącz lokacji punktu połączenia, należy toouse hello portalu zgodnie z opisem w [Tworzenie bramy sieci VPN][createvpngateway].

Witaj klasycznej sieci wirtualnej musi toobe w hello tej samej subskrypcji co w usłudze App Service plan, który jest integrowany z aplikacja hello blokad.

##### <a name="set-up-azure-powershell-sdk"></a>Konfigurowanie programu Azure PowerShell SDK
Otwórz okno programu PowerShell i skonfigurować konto platformy Azure i subskrypcji przy użyciu:

    Login-AzureRmAccount

To polecenie spowoduje otwarcie tooget monitu o poświadczenia platformy Azure. Po zalogowaniu, użyj jednej z powitania po subskrypcji hello tooselect poleceń, które mają toouse. Upewnij się, że używasz hello subskrypcji, że sieć wirtualna i plan usługi aplikacji znajdują się w.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

lub

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Zmienne używane w tym artykule
polecenia toosimplify, możemy ustawi **$Configuration** PowerShell zmienna o określonej konfiguracji hello.

Ustaw zmienną w następujący sposób w programie PowerShell z hello następujące parametry:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

Lokalizacja aplikacji Hello powinna być hello lokalizacji bez spacji. Zachodnie stany USA jest na przykład westus.

    $Configuration.WebAppLocation = "[Your web app Location]"

Następny element Hello jest miejsca zapisu hello certyfikatu. Należy ścieżką zapisu na komputerze lokalnym. Upewnij się, że .cer tooinclude na końcu hello.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee zostanie ustawiona, typ **$Configuration**.

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

Witaj pozostałej części tej sekcji założono, że utworzony zgodnie z opisem właśnie zmiennej.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Deklarowanie hello sieci wirtualnej toohello aplikacji
Użyj hello następujące polecenie aplikacji hello tootell, że zostanie do niej używa tej określonej sieci wirtualnej. Spowoduje to toogenerate aplikacji hello niezbędnych certyfikatów:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Jeśli to polecenie zakończy się powodzeniem, **$vnet** powinien mieć **właściwości** zmiennej w nim. Witaj **właściwości** zmienna powinna zawierać zarówno certyfikat odcisk palca i hello danych certyfikatu.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Przekaż hello web app certyfikatu toohello wirtualnej sieci
Ręczne, jednorazowe krok jest wymagany dla każdej kombinacji sieci wirtualnej i subskrypcji. Oznacza to jeśli łączysz się z aplikacji w subskrypcji A tooVirtual sieci A, konieczne będzie toodo ten krok tylko raz, niezależnie od tego, jak wiele aplikacji można skonfigurować. W przypadku dodawania nowej sieci wirtualnej tooanother aplikacji, musisz toodo ponownie. Witaj przyczyną tego błędu jest zestaw certyfikatów jest generowany na poziomie subskrypcji w usłudze Azure App Service, czy zestaw hello jest generowany raz dla każdej sieci wirtualnej, którą aplikacji hello połączy się.

Hello certyfikaty będą już zostały ustawione po wykonaniu tych kroków lub zintegrowana z hello sam sieci wirtualnej przy użyciu portalu hello.

pierwszym krokiem Hello jest plik cer hello toogenerate. drugim krokiem Hello jest tooupload hello .cer pliku tooyour wirtualnej sieci. plik .cer hello toogenerate z wywołania interfejsu API hello w hello wcześniejszym kroku, uruchom następujące polecenia hello.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

certyfikat Hello zostaną znalezione w lokalizacji hello który **$Configuration.GeneratedCertificatePath** określa.

tooupload hello certyfikat ręcznie, użyj hello [portalu Azure] [ azureportal] i **Przeglądaj sieć wirtualna (klasyczna)** > **połączeń sieci VPN**  >  **Punkt lokacja** > **zarządzanie certyfikatami**. W tym miejscu przekazanie certyfikatu.

##### <a name="get-hello-point-to-site-package"></a>Pobierz pakiet punkt lokacja hello
Hello następnego kroku w procesie konfigurowania połączenia z wirtualną siecią w aplikacji sieci web jest tooget hello punkt lokacja pakietu i podaj go tooyour aplikacji sieci web.

Zapisz hello następującego szablonu tooa pliku o nazwie GetNetworkPackageUri.json gdzieś na komputerze, na przykład C:\Azure\Templates\GetNetworkPackageUri.json.

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


Ustaw parametry wejściowe:

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Wywołanie skryptu hello:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


Zmienna Hello **$output. Outputs.packageUri** teraz będzie zawierać toobe identyfikator URI pakietu hello podane tooyour aplikacji sieci web.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Przekaż aplikację tooyour pakietu punkt lokacja hello
Ostatnim krokiem Hello jest aplikacja hello tooprovide z tym pakietem. Po prostu uruchom następne polecenie hello:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Jeśli wiadomość zostanie wyświetlona prośba tooconfirm, że są zastępowania istniejącego zasobu, upewnij się, że tooallow go.

Po pomyślnym zainicjowaniu tego polecenia, aplikacji powinno być teraz toohello połączonych sieci wirtualnej. Powodzenie tooconfirm Przejdź tooyour aplikacji konsoli, a następnie wpisz następujące hello:

    SET WEBSITE_

Jeśli zmienna środowiskowa o nazwie WEBSITE_VNETNAME wartości, który odpowiada nazwie hello hello docelowy wirtualnej sieci pomyślnie wszystkie konfiguracje.

### <a name="update-classic-vnet-integration-information"></a>Aktualizowanie klasycznych informacji integracji sieci wirtualnej
tooupdate lub ponownej synchronizacji danych, po prostu Powtórz kroki hello, których należy przestrzegać podczas tworzenia integracji hello w miejscu pierwszego hello. Te kroki są:

1. Zdefiniuj informacje o konfiguracji.
2. Deklarowanie hello sieci wirtualnej toohello aplikacji.
3. Pobierz pakiet punkt lokacja hello.
4. Przekaż hello pakietu punkt lokacja tooyour aplikacji.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Rozłączyć aplikacji klasycznej sieci wirtualnej
Aplikacja hello toodisconnect, należy hello informacje o konfiguracji, która została ustawiona podczas integracji sieci wirtualnej. Za pomocą tych informacji, istnieje jeden toodisconnect polecenia aplikacji z sieci wirtualnej.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Sieci wirtualne usługi Resource Manager
Sieci wirtualne usługi Resource Manager ma interfejsów API usługi Azure Resource Manager, który uprościć niektóre procesy w porównaniu z klasycznych sieci wirtualnych. Mamy skrypt, który pomoże Ci się ukończyć powitalnych następujące zadania:

* Tworzenie sieci wirtualnej Resource Manager i integracji aplikacji z nim.
* Utwórz bramę, skonfiguruj połączenie punkt lokacja w istniejących sieci wirtualnych Menedżera zasobów, a następnie Integrowanie aplikacji z nim.
* Integracja aplikacji z istniejących Menedżera zasobów sieci wirtualnej bramy i włączyć łączność punkt do lokacji.
* Aplikację można rozłączyć sieci wirtualnej.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Skrypt integracji usługi aplikacji — Menedżer zasobów sieci wirtualnej
Skopiuj hello następujący skrypt i zapisać go w pliku tooa. Jeśli nie chcesz toouse hello skryptu, możesz toolearn wolne od niego toosee jak rzeczy tooset się z siecią wirtualną Menedżera zasobów.

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

Zapisz kopię hello skryptu. W tym artykule jest nazywany V2VnetAllinOne.ps1, ale możesz użyć innej nazwy. Nie ma żadnych argumentów w ramach tego skryptu. Wystarczy uruchomić go. Witaj po pierwsze hello skrypt będzie wykonywać jest monit toosign w. Po zalogowaniu, skrypt hello pobiera szczegółowe informacje o Twoim koncie i zwraca listę subskrypcji. Nie, licząc w żądania hello o podanie poświadczeń, wykonywanie skryptu początkowej hello wygląda następująco:

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Wersja demonstracyjna dla subskrypcji (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) Test MS (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Pokaz purpurowa subskrypcji (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Wybierz jedną z opcji: 3

    Konto: ccompy@microsoft.com środowiska: subskrypcji AzureCloud: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d dzierżawy: 722278f-fef1-499f-91ab-2323d011db47

    Podaj nazwę grupy zasobów aplikacji hello: zarządcy zasobów hcdemo wprowadź nazwę aplikacji hello: v2vnetpowershell czego użytkownik ma toodo?

    1) Dodaj nową sieć wirtualną tooan aplikacji
    2) Dodawanie istniejącej sieci wirtualnej tooan aplikacji
    3) Usuń sieć wirtualną z aplikacji

Hello pozostałej części tej sekcji opisano każdy z tych trzech opcji.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Tworzenie sieci wirtualnej Resource Manager oraz integrują się z jej
Wybierz nową sieć wirtualną, że używa hello modelu wdrażania usługi Resource Manager i zintegrować ją z aplikacją, toocreate **1) Dodaj nową sieć wirtualną tooan aplikacji**. To wyświetli monit o nazwę hello hello sieci wirtualnej. W przypadku mojej jak widać w hello następujące ustawienia, I użyto nazwy hello, v2pshell.

skrypt Hello szczegółowo hello hello sieci wirtualnej, która jest tworzona. Jeśli ma, można zmienić wartości hello. Podczas wykonywania tego przykładu I utworzyć sieć wirtualną mającą hello następujące ustawienia:

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

Toochange hello wartości, należy wpisać **Y** i wprowadź zmiany hello. W przypadku modyfikowania ustawień sieci wirtualnej hello wpisz **N** lub po prostu naciśnij klawisz Enter po wyświetleniu monitu o zmianę ustawień hello. Z tego miejsca na aż do zakończenia skryptu hello informuje o niektórych jakie "być wykonanie do momentu rozpoczęcia bramy sieci wirtualnej hello toocreate. Ten krok może potrwać godzinę tooan. Nie jest wskaźnik postępu, nie w tej fazie, ale skryptu hello poinformuje użytkownika po utworzeniu bramy hello.

Po zakończeniu działania skryptu hello jest wyświetlany tekst **Zakończono**. W tym momencie będzie mieć Menedżera zasobów sieci wirtualnej o nazwie hello i wybrane ustawienia. Ta nowa sieć wirtualna będzie również być zintegrowane z aplikacji.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Integracja aplikacji z istniejących zasobów Menedżera sieci wirtualnej
Gdy w przypadku integracji z istniejących sieci wirtualnej, jeśli podasz Menedżera zasobów sieci wirtualnej, która nie ma bramy lub połączenie punkt lokacja, skrypt hello skonfiguruje który. Jeśli hello sieci Wirtualnej ma już tych problemów, konfigurowanie, skrypt hello przechodzi toohello prostej aplikacji integracji. toostart ten proces, po prostu zaznacz **2) Dodaj tooan istniejącej sieci wirtualnej aplikacji**.

Ta opcja działa tylko wtedy, gdy w przypadku istniejących sieci wirtualnych Menedżera zasobów, w hello tej samej subskrypcji co aplikacja. Po wybraniu opcji hello, zostanie wyświetlona lista sieci wirtualne usługi Resource Manager.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Wybierz jedną z opcji: 5

Po prostu wybierz hello sieci wirtualnej, który ma toointegrate z. Jeśli masz już bramy, która ma włączone połączenie punkt lokacja, skrypt powitania po prostu integracji aplikacji z sieci wirtualnej. Jeśli nie ma bramę, konieczne będzie podsieci bramy hello toospecify. Podsieć bramy musi być w przestrzeni adresowej sieci wirtualnej, a nie może być w innej podsieci. Jeśli masz bez bramy sieci wirtualnej, a następnie uruchom ten krok, rzeczy wyglądać następująco:

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

W tym przykładzie można utworzyć bramy sieci wirtualnej, która ma hello następujące ustawienia:

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

Jeśli chcesz toochange dowolne z tych ustawień, możesz to zrobić. W przeciwnym razie naciśnij klawisz Enter, a skrypt hello Tworzenie bramy i Dołącz sieć wirtualna tooyour aplikacji. Czas utworzenia bramy Hello jest nadal godzinę, mimo że, upewnij się, że należy pamiętać, że. Gdy wszystko jest gotowe, będzie napisane skryptu hello **Zakończono**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Rozłączyć aplikacji z Menedżera zasobów sieci wirtualnej
Odłączanie aplikacji od sieci wirtualnej nie wyłączyć hello bramy lub Wyłącz połączenie punkt lokacja. Być może używasz go do czegoś innego. Go również nie odłączenie go od innych aplikacji innych niż hello co podane. tooperform tę akcję, wybierz opcję **3) Usuń sieć wirtualną z aplikacji**. Jeśli tak zrobisz, zostanie wyświetlony podobny do następującego:

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Mimo że skryptu hello mówi delete, nie powoduje usunięcia hello sieci wirtualnej. Jest on tylko usuwanie hello integracji. Po upewnieniu się, że jest to czego chcesz toodo, polecenie hello jest bardzo szybko przetwarzane i pozwalają określić **True** po jej zakończeniu.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
