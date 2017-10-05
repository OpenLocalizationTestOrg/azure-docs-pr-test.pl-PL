---
title: "Łączenie aplikacji z siecią wirtualną za pomocą programu PowerShell"
description: "Instrukcje dotyczące sposobu nawiązać połączenie i pracować z sieci wirtualnych za pomocą programu PowerShell"
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
ms.openlocfilehash: 6fae6a6c162fa326161d2b47a259b3151d6e3dd0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-app-to-your-virtual-network-by-using-powershell"></a>Łączenie aplikacji z siecią wirtualną za pomocą programu PowerShell
## <a name="overview"></a>Omówienie
W usłudze Azure App Service można połączyć aplikacji (sieć web, mobilnych lub interfejsu API) do sieci wirtualnej platformy Azure (VNet) w ramach subskrypcji. Ta funkcja jest nazywana integracji sieci wirtualnej. Funkcja integracji sieci wirtualnej nie należy mylić z funkcji środowiska usługi aplikacji, która pozwala na uruchamianie wystąpienia usługi Azure App Service w Twojej sieci wirtualnej.

Funkcja integracji sieci wirtualnej ma interfejs użytkownika (UI) w nowego portalu, który służy do integracji z sieciami wirtualnymi, które zostały wdrożone przy użyciu klasycznego modelu wdrażania lub modelu wdrażania usługi Azure Resource Manager. Jeśli chcesz dowiedzieć się więcej na temat funkcji, zobacz [integracji aplikacji z sieci wirtualnej platformy Azure](web-sites-integrate-with-vnet.md).

W tym artykule jest nie o sposobie używania interfejsu użytkownika, ale raczej o włączaniu integracji przy użyciu programu PowerShell. Ponieważ polecenia dla każdego modelu wdrażania są różne, w tym artykule ma sekcji do każdego modelu wdrażania.  

Przed kontynuowaniem w tym artykule upewnij się, że masz:

* R zainstalowany zestaw SDK usługi Azure PowerShell. Można go zainstalować za pomocą Instalatora platformy sieci Web.
* Aplikacja w usłudze Azure App Service w Standard lub Premium jednostki SKU.

## <a name="classic-virtual-networks"></a>Klasycznych sieci wirtualnych
W tej sekcji opisano trzy zadania dla sieci wirtualnych, które używają klasycznym modelu wdrażania:

1. Łączenie aplikacji z istniejących sieci wirtualnej, i jest konfigurowane połączenie punkt lokacja z bramą.
2. Aktualizowanie informacji o integracji sieci wirtualnej dla aplikacji.
3. Aplikację można rozłączyć sieci wirtualnej.

### <a name="connect-an-app-to-a-classic-vnet"></a>Łączenie aplikacji klasycznej sieci wirtualnej
Aby połączyć aplikację z sieci wirtualnej, wykonaj następujące trzy kroki:

1. W aplikacji sieci web zadeklarować, że zostanie do niej dołączanie do określonej sieci wirtualnej. Aplikacja wygeneruje certyfikat, który będzie podane do sieci wirtualnej dla połączenia punkt lokacja.
2. Przekaż certyfikat aplikacji sieci web do sieci wirtualnej, a następnie pobrać identyfikator URI pakietu sieci VPN punkt lokacja.
3. Zaktualizuj połączenie wirtualnej sieci aplikacji sieci web z pakietem punkt lokacja identyfikatora URI.

Pierwszy i trzeci kroki są w pełni skryptowe, a drugi etap wymaga jednorazowe, ręczna Akcja za pośrednictwem portalu lub dostępu do wykonywania **PUT** lub **poprawka** akcje na wirtualnej sieci zasobów Azure Punkt końcowy menedżera. Skontaktuj się z pomocą techniczną platformy Azure ma to włączone. Przed rozpoczęciem upewnij się, czy masz klasycznego siecią wirtualną, która ma już włączone połączenie punkt lokacja i wdrożone bramę. Aby utworzyć bramę i Włącz połączenie punkt lokacja, należy korzystać z portalu zgodnie z opisem w [Tworzenie bramy sieci VPN][createvpngateway].

Klasyczne sieci wirtualnej musi być w tej samej subskrypcji co planu usługi aplikacji zawierający aplikację, która jest integrowany z.

##### <a name="set-up-azure-powershell-sdk"></a>Konfigurowanie programu Azure PowerShell SDK
Otwórz okno programu PowerShell i skonfigurować konto platformy Azure i subskrypcji przy użyciu:

    Login-AzureRmAccount

To polecenie spowoduje otwarcie wiersza, aby uzyskać poświadczenia platformy Azure. Po zalogowaniu w użyj jednej z następujących poleceń, aby wybrać subskrypcję, która ma być używany. Upewnij się, że używasz subskrypcji, że sieć wirtualna i plan usługi aplikacji znajdują się w.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

lub

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Zmienne używane w tym artykule
Aby uprościć poleceń, możemy ustawi **$Configuration** PowerShell zmienna o określonej konfiguracji.

Ustaw zmienną w następujący sposób w programie PowerShell z następującymi parametrami:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

Lokalizacja aplikacji powinna być lokalizacji bez spacji. Zachodnie stany USA jest na przykład westus.

    $Configuration.WebAppLocation = "[Your web app Location]"

Następny element jest, którym zapisany certyfikat. Należy ścieżką zapisu na komputerze lokalnym. Upewnij się uwzględnić .cer na końcu.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

Aby zobaczyć, jakie ustawiasz, wpisz **$Configuration**.

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

Pozostałej części tej sekcji założono, że utworzony zgodnie z opisem właśnie zmiennej.

##### <a name="declare-the-virtual-network-to-the-app"></a>Deklarowanie sieci wirtualnej do aplikacji
Użyj następującego polecenia aplikacji stwierdzić, że zostanie do niej używa tej określonej sieci wirtualnej. Spowoduje to aplikacji do wygenerowania niezbędnych certyfikatów:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Jeśli to polecenie zakończy się powodzeniem, **$vnet** powinien mieć **właściwości** zmiennej w nim. **Właściwości** zmienna powinna zawierać zarówno odcisku palca certyfikatu, jak i dane certyfikatu.

##### <a name="upload-the-web-app-certificate-to-the-virtual-network"></a>Przekaż certyfikat aplikacji sieci web do sieci wirtualnej
Ręczne, jednorazowe krok jest wymagany dla każdej kombinacji sieci wirtualnej i subskrypcji. Oznacza to, że łączysz aplikacji w ramach subskrypcji A A sieci wirtualnej, należy wykonać ten krok tylko wtedy, gdy niezależnie od tego, jak wiele aplikacji można skonfigurować. Jeśli dodajesz nową aplikację do innej sieci wirtualnej, należy ponownie. Przyczyną tego jest zestaw certyfikatów jest generowany na poziomie subskrypcji w usłudze Azure App Service, czy zestaw jest generowany raz dla każdej sieci wirtualnej, które aplikacje będą się łączyć.

Certyfikaty zostaną już zostały ustawione po wykonaniu tych kroków lub zintegrowana z tej samej sieci wirtualnej przy użyciu portalu.

Pierwszym krokiem jest generowanie pliku .cer. Drugim krokiem jest można przekazać pliku .cer do sieci wirtualnej. Aby wygenerować plik .cer w wywołaniu interfejsu API w poprzednim kroku, uruchom następujące polecenia.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

Będzie można znaleźć certyfikatu w lokalizacji który **$Configuration.GeneratedCertificatePath** określa.

Aby przekazać certyfikat ręcznie, należy użyć [portalu Azure] [ azureportal] i **Przeglądaj sieć wirtualna (klasyczna)** > **połączeń sieci VPN**  >  **Punkt lokacja** > **zarządzanie certyfikatami**. W tym miejscu przekazanie certyfikatu.

##### <a name="get-the-point-to-site-package"></a>Pobierz pakiet punkt lokacja
Następnym krokiem w procesie konfigurowania połączenia z wirtualną siecią w aplikacji sieci web jest pobrania pakietu punkt lokacja i przekazywanie ich do aplikacji sieci web.

Zapisz następującego szablonu w pliku o nazwie GetNetworkPackageUri.json gdzieś na komputerze, na przykład C:\Azure\Templates\GetNetworkPackageUri.json.

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

Wywołanie skryptu:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


Zmienna **$output. Outputs.packageUri** teraz będzie zawierać pakiet identyfikator URI do aplikacji sieci web.

##### <a name="upload-the-point-to-site-package-to-your-app"></a>Przekaż pakiet punkt lokacja, do aplikacji
Ostatnim krokiem jest zapewnienie aplikacji z tym pakietem. Po prostu uruchom następne polecenie:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Jeśli wiadomość prośba o potwierdzenie, że są zastępowania istniejącego zasobu, upewnij się umożliwić jego.

Po pomyślnym zainicjowaniu tego polecenia, aplikacji powinno być teraz połączone siecią wirtualną. Aby sprawdzić, powodzenia, przejdź do aplikacji konsoli, a następnie wpisz następujące polecenie:

    SET WEBSITE_

W przypadku zmienną środowiskową o nazwie WEBSITE_VNETNAME, który ma wartość, która jest zgodna z nazwą docelowej sieci wirtualnej, wszystkie konfiguracje mają zakończyło się pomyślnie.

### <a name="update-classic-vnet-integration-information"></a>Aktualizowanie klasycznych informacji integracji sieci wirtualnej
Aby zaktualizować lub ponownej synchronizacji danych, po prostu Powtórz kroki, które należy przestrzegać podczas integracji został utworzony w pierwszej kolejności. Te kroki są:

1. Zdefiniuj informacje o konfiguracji.
2. Deklarowanie sieci wirtualnej do aplikacji.
3. Pobierz pakiet punkt lokacja.
4. Przekaż pakiet punkt lokacja, do aplikacji.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Rozłączyć aplikacji klasycznej sieci wirtualnej
Aby odłączyć aplikacji, potrzebne są informacje o konfiguracji, która została ustawiona podczas integracji sieci wirtualnej. Za pomocą tych informacji, jest następnie jednego polecenia można rozłączyć aplikacji z sieci wirtualnej.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Sieci wirtualne usługi Resource Manager
Sieci wirtualne usługi Resource Manager ma interfejsów API usługi Azure Resource Manager, który uprościć niektóre procesy w porównaniu z klasycznych sieci wirtualnych. Mamy skrypt, który pomoże wykonać następujące zadania:

* Tworzenie sieci wirtualnej Resource Manager i integracji aplikacji z nim.
* Utwórz bramę, skonfiguruj połączenie punkt lokacja w istniejących sieci wirtualnych Menedżera zasobów, a następnie Integrowanie aplikacji z nim.
* Integracja aplikacji z istniejących Menedżera zasobów sieci wirtualnej bramy i włączyć łączność punkt do lokacji.
* Aplikację można rozłączyć sieci wirtualnej.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Skrypt integracji usługi aplikacji — Menedżer zasobów sieci wirtualnej
Skopiuj poniższy skrypt i zapisz go w pliku. Jeśli nie chcesz użyć skryptu, możesz także dowiedzieć się od niego na temat sposobu konfigurowania elementów sieci wirtualnych Menedżera zasobów.

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

        Write-Host "Adding a root certificate to this VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up to an hour."
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
            Write-Host "Currently, I will create a VNET with the following settings:"
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
            $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

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

        # We create the virtual network and add it here. The way this works is:
        # 1) Add the VNET association to the App. This allows the App to generate certificates, etc. for the VNET.
        # 2) Create the VNET and VNET gateway, add the certificates, create the public IP, etc., required for the gateway
        # 3) Get the VPN package from the gateway and pass it back to the App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association to VNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, the gateway should be able to be joined to an App, but may require some minor tweaking. We will declare to the App now to use this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET to integrate with" $vnets $vnetNames

        # We need to check if this VNET is able to be joined to a App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have the right certificate, we will need to add it.
                # If it doesn't have a point-to-site range, we will need to add it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need to create one.
            Write-Host "This Virtual Network has no gateway. I will need to create one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in the address space $($vnet.AddressSpace.AddressPrefixes), with the following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with the following settings:"
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
                $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

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

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need to create one.
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
                Write-Error "This gateway is not of the Vpn type. It cannot be joined to an App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined to an App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need to check if the certificate here exists in the gateway.
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

        # Now finish joining by getting the VPN package and giving it to the App
        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
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
            Write-Host "Currently connected to VNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected to a VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound to this account."
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

    $resourceGroup = Read-Host "Please enter the Resource Group of your App"

    $appName = Read-Host "Please enter the Name of your App"

    $options = @("Add a NEW Virtual Network to an App", "Add an EXISTING Virtual Network to an App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want to do?" $optionValues $options

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

Zapisz kopię skryptu. W tym artykule jest nazywany V2VnetAllinOne.ps1, ale możesz użyć innej nazwy. Nie ma żadnych argumentów w ramach tego skryptu. Wystarczy uruchomić go. W pierwszej kolejności skrypt będzie wykonywać jest wyświetlenie monitu zaloguj się. Po zalogowaniu, skrypt pobiera szczegółowe informacje o Twoim koncie i zwraca listę subskrypcji. Nie, licząc w żądanie o podanie poświadczeń, wykonywanie skryptu początkowej wygląda następująco:

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

    Wprowadź grupę zasobów aplikacji: zarządcy zasobów hcdemo wprowadź nazwę aplikacji: v2vnetpowershell co chcesz zrobić?

    1) Dodawanie nowej sieci wirtualnej do aplikacji
    2) Dodaj istniejące sieci wirtualnej do aplikacji
    3) Usuń sieć wirtualną z aplikacji

Pozostałej części tej sekcji opisano każdy z tych trzech opcji.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Tworzenie sieci wirtualnej Resource Manager oraz integrują się z jej
Aby utworzyć nową sieć wirtualną, która używa modelu wdrażania usługi Resource Manager i zintegrować ją z aplikacji, wybierz **1) Dodawanie nowej sieci wirtualnej do aplikacji**. To spowoduje wyświetlenie monitu o nazwę sieci wirtualnej. W przypadku mojej jak widać w następujących ustawieniach I użyta nazwa v2pshell.

Skrypt podaje szczegółowe informacje o sieci wirtualnej, która jest tworzona. Jeśli ma, można zmienić wartości. Podczas wykonywania tego przykładu I utworzyć sieci wirtualnej, który ma następujące ustawienia:

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

Jeśli chcesz zmienić wartości, wpisz **Y** i wprowadź zmiany. W przypadku modyfikowania ustawień sieci wirtualnej wpisz **N** lub po prostu naciśnij klawisz Enter po wyświetleniu monitu o zmianę ustawień. Z tego miejsca na aż do zakończenia skryptu informuje o niektórych jakie "być czynności do chwili jego uruchomienia utworzyć bramę sieci wirtualnej. Ten krok może potrwać do godziny. Nie jest wskaźnik postępu, nie w tej fazie, ale skrypt poinformuje użytkownika po utworzeniu bramy.

Po zakończeniu działania skryptu jest wyświetlany tekst **Zakończono**. W tym momencie będzie mieć Resource Manager sieć wirtualna, która ma nazwę i ustawienia, które zostały wybrane. Ta nowa sieć wirtualna będzie również być zintegrowane z aplikacji.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Integracja aplikacji z istniejących zasobów Menedżera sieci wirtualnej
Gdy w przypadku integracji z istniejących sieci wirtualnej, jeśli podasz Menedżera zasobów sieci wirtualnej, która nie ma bramy lub połączenie punkt lokacja, skrypt zostanie skonfigurowany który. Jeśli sieć wirtualna ma już tych problemów, konfigurowanie, skrypt trafia bezpośrednio do integracji aplikacji. Aby uruchomić ten proces, po prostu zaznacz **2) Dodaj istniejącej sieci wirtualnej do aplikacji**.

Ta opcja działa tylko wtedy, gdy masz istniejących Resource Manager siecią wirtualną, która znajduje się w tej samej subskrypcji co aplikacja. Po wybraniu opcji, zostanie wyświetlona lista sieci wirtualne usługi Resource Manager.   

    Select a VNET to integrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Wybierz jedną z opcji: 5

Po prostu wybierz sieć wirtualną, który chcesz zintegrować z. Jeśli masz już bramy, która ma włączone połączenie punkt lokacja, skrypt po prostu integracji aplikacji z sieci wirtualnej. Jeśli nie masz bramy, należy określić podsieć bramy. Podsieć bramy musi być w przestrzeni adresowej sieci wirtualnej, a nie może być w innej podsieci. Jeśli masz bez bramy sieci wirtualnej, a następnie uruchom ten krok, rzeczy wyglądać następująco:

    This Virtual Network has no gateway. I will need to create one.
    Your VNET is in the address space 172.16.0.0/16, with the following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

W tym przykładzie można utworzyć bramy sieci wirtualnej, która ma następujące ustawienia:

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association to VNET

Jeśli chcesz zmienić te ustawienia, możesz to zrobić. W przeciwnym razie naciśnij klawisz Enter, a skrypt utworzy bramy i dołączyć aplikacji do sieci wirtualnej. Czas utworzenia bramy jest nadal godzinę, mimo że, upewnij się, że należy pamiętać, że. Gdy wszystko jest gotowe, będzie napisane skrypt **Zakończono**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Rozłączyć aplikacji z Menedżera zasobów sieci wirtualnej
Odłączanie aplikacji od sieci wirtualnej nie wyłączyć bramy lub Wyłącz połączenie punkt lokacja. Być może używasz go do czegoś innego. On również nie odłączenie go od innych aplikacji, innego niż podany. Aby wykonać tę akcję, wybierz **3) Usuń sieć wirtualną z aplikacji**. Jeśli tak zrobisz, zostanie wyświetlony podobny do następującego:

    Currently connected to VNET v2pshell

    Confirm
    Are you sure you want to delete the following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Mimo że skrypt jest wyświetlany komunikat delete nie powoduje usunięcia sieci wirtualnej. Jest on tylko usuwanie integracji. Po upewnieniu się, że jest to, co chcesz zrobić, polecenie jest bardzo szybko przetwarzane i pozwalają określić **True** po jej zakończeniu.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
