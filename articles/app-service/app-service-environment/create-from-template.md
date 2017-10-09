---
title: "aaaCreate środowiska usługi aplikacji Azure przy użyciu szablonu usługi Resource Manager"
description: "Wyjaśniono, jak toocreate środowisku zewnętrznego lub ILB usłudze Azure App Service przy użyciu szablonu usługi Resource Manager"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>Utwórz ASE za pomocą szablonu usługi Azure Resource Manager

## <a name="overview"></a>Omówienie
Środowiska usługi aplikacji Azure (ASEs) mogą być tworzone z Internetu dostępnym punkcie końcowym lub punkt końcowy wewnętrznego adresu w sieci wirtualnej platformy Azure (VNet). Podczas tworzenia z wewnętrzny punkt końcowy tego punktu końcowego jest udostępniane przez platformę Azure składnika o nazwie wewnętrznego modułu równoważenia obciążenia (ILB). Witaj ASE na wewnętrzny adres IP jest nazywany ASE ILB. Hello ASE z publiczny punkt końcowy jest nazywany ASE zewnętrznych. 

ASE mogą być tworzone przy użyciu portalu Azure hello lub szablonu usługi Azure Resource Manager. W tym artykule przedstawiono kroki hello i składni konieczne toocreate ASE zewnętrznych lub ILB ASE z szablonami usługi Resource Manager. toolearn toocreate ASE w hello portalu Azure, zobacz temat [wprowadzić zewnętrznego ASE] [ MakeExternalASE] lub [upewnij ASE ILB][MakeILBASE].

Po utworzeniu ASE w hello portalu Azure, można utworzyć sieci wirtualnej na powitania sam czas lub wybierz istniejące wcześniej toodeploy sieci wirtualnej do. Po utworzeniu ASE z szablonu musi rozpoczynać się od: 

* Menedżer zasobów sieci wirtualnej.
* Podsieci w tej sieci wirtualnej. Firma Microsoft zaleca rozmiar podsieci ASE `/25` z przyszłego rozwoju tooaccomodate 128 adresów. Po utworzeniu hello ASE, nie można zmienić rozmiar hello.
* Identyfikator zasobu Hello z sieci wirtualnej. Te informacje można uzyskać z hello portalu Azure w obszarze właściwości sieci wirtualnej.
* Subskrypcja Hello interesujące toodeploy do.
* Witaj lokalizację toodeploy do.

tooautomate Twojego tworzenia ASE:

1. Utwórz hello ASE na podstawie szablonu. Jeśli utworzysz zewnętrznych ASE zakończeniu po wykonaniu tego kroku. Jeśli tworzysz ASE ILB, istnieje kilka toodo więcej czynności.

2. Po utworzeniu sieci ASE ILB przekazaniu pasujący domenę ILB ASE certyfikat SSL.

3. Witaj przekazano certyfikat SSL jest przypisany toohello ILB ASE jako swojego certyfikatu SSL "domyślny".  Ten certyfikat służy do tooapps ruchu protokołu SSL na powitania ILB ASE przy korzystaniu z hello wspólnej główny domeny, która jest przypisany toohello ASE (na przykład https://someapp.mycustomrootcomain.com).


## <a name="create-hello-ase"></a>Utwórz hello ASE
Szablon usługi Resource Manager, który pozwala ASE i jego pliku skojarzone z nimi parametry jest dostępna [w przykładzie] [ quickstartasev2create] w witrynie GitHub.

Toomake ASE ILB, należy użyć tych szablonu usługi Resource Manager [przykłady][quickstartilbasecreate]. Przypadek użycia toothat ich obsługę. Większość parametrów hello na powitania *azuredeploy.parameters.json* plików są typowe tworzenia toohello ILB ASEs i ASEs zewnętrznych. Witaj poniżej uwidacznia parametry specjalne uwagi lub są unikatowe, podczas tworzenia ASE ILB:

* *interalLoadBalancingMode*: W większości przypadków należy ustawić ten too3, czyli zarówno ruchu HTTP/HTTPS na porty 80/443 i portów kanału danych/sterowania hello nasłuch tooby usługi hello FTP na powitania ASE, będą powiązane tooan przydzielone ILB sieci wirtualnej wewnętrzny adres. Jeśli ta właściwość jest ustawiona too2, tylko hello FTP związane z usługą porty (kanały zarówno kontroli, jak i dane) są powiązane tooan ILB adresu. pozostaje Hello ruchu HTTP/HTTPS na powitania publicznego adresu VIP.
* *dnsSuffix*: ten parametr określa hello domyślne główny domeny, która jest przypisany toohello ASE. W publicznej wersji hello Azure App Service, hello domyślna domena główna dla wszystkich aplikacji w sieci web to *azurewebsites.net*. Ponieważ ASE ILB wewnętrzny tooa klienta sieci wirtualnej, nie rozsądne znaczeniu toouse hello publicznej usługi domyślnej domeny katalogu głównego. Zamiast tego ASE ILB powinien mieć domyślnej domeny katalogu głównego, pasującą do użytku w wewnętrznej sieci wirtualnej firmy. Na przykład firma Contoso może użyć domyślną domeną katalogu głównego *wewnętrzny contoso.com* dla aplikacji, które są przeznaczone toobe rozpoznawany i dostępny tylko w ramach sieci wirtualnej firmy Contoso. 
* *ipSslAddressCount*: ten parametr automatycznie domyślnie przyjmowana jest wartość 0 w hello tooa *azuredeploy.json* pliku, ponieważ ILB ASEs mieć tylko jeden adres ILB. Nie ma żadnych jawnych adresów IP protokołu SSL dla ASE ILB. W związku z tym hello puli adresów IP protokołu SSL dla ASE ILB musi być ustawiona toozero. W przeciwnym razie wystąpi błąd inicjowania obsługi administracyjnej. 

Po hello *azuredeploy.parameters.json* plik zostanie wypełnione, Utwórz hello ASE przy użyciu fragment kodu hello programu PowerShell. Zmiana hello ścieżki toomatch hello Menedżera zasobów pliku szablonu lokalizacji na komputerze. Należy pamiętać o toosupply własne wartości hello wdrożenia usługi Resource Manager i nazwy grupy zasobów hello:

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Trwa około godziny na powitania ASE toobe utworzony. Następnie hello ASE zostaną wyświetlone w portalu hello hello liście ASEs hello subskrypcji, która wyzwoliła hello wdrożenia.

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>Przekazać i skonfigurować certyfikat SSL "domyślne" hello
Certyfikat SSL musi być skojarzony z hello ASE jako certyfikat SSL "domyślne" hello jest tooapps połączenia SSL tooestablish używane. Jeśli hello ASE na domyślny sufiks DNS jest *wewnętrzny contoso.com*, toohttps://some-random-app.internal-contoso.com połączenie wymaga certyfikatu SSL, który jest prawidłowy dla **.internal contoso.com* . 

Uzyskaj prawidłowy certyfikat SSL przy użyciu certyfikatu wewnętrznego urzędów, zakup certyfikatu od zewnętrznego wystawcy lub przy użyciu certyfikatu z podpisem własnym. Niezależnie od źródła hello hello certyfikatu SSL hello następujące atrybuty certyfikatu musi być prawidłowo skonfigurowane:

* **Temat**: ten atrybut musi być ustawiony zbyt **.your głównego domeny here.com*.
* **Alternatywna nazwa podmiotu**: ten atrybut musi zawierać zarówno **.your głównego domeny here.com* i **.scm.your-głównego-domeny-here.com*. Toohello połączenia SSL SCM/Kudu lokacji skojarzone z każdej aplikacji używać adresu formularza hello *your-app-name.scm.your-root-domain-here.com*.

Przy użyciu prawidłowego certyfikatu SSL w ręcznie potrzebne są dwa dodatkowe czynności przygotowawczych. Konwertuj/Zapisz certyfikat SSL hello jako plik pfx. Należy pamiętać, ten plik PFX hello musi obejmować wszystkie pośrednie i certyfikaty główne. Zabezpiecz ją przy użyciu hasła.

plik PFX Hello wymaga toobe konwertowane na ciąg w formacie base64, ponieważ certyfikat SSL hello jest przekazywany za pomocą szablonu usługi Resource Manager. Ponieważ szablonów Resource Manager są plikami tekstowymi, plik PFX hello musi można przekonwertować na ciąg w formacie base64. W ten sposób może zostać dołączony jako parametr szablonu hello.

Użyj następującego fragmentu kodu programu PowerShell hello:

* Wygeneruj certyfikat z podpisem własnym.
* Wyeksportuj certyfikat hello jako plik pfx.
* Konwertowanie pliku PFX hello na ciąg kodowany w formacie base64.
* Zapisz hello ciąg kodowany w formacie base64 tooa oddzielny plik. 

Ten kod programu PowerShell dla kodowania base64 został hello [blogu skrypty programu PowerShell][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Po hello certyfikat SSL został prawidłowo wygenerowany i przekonwertować na ciąg kodowany w formacie base64 tooa, użyj szablonu usługi Resource Manager przykład hello [certyfikat SSL domyślny hello Konfiguruj] [ quickstartconfiguressl] w witrynie GitHub. 

Witaj parametrów w hello *azuredeploy.parameters.json* plików są wyświetlane tutaj:

* *appServiceEnvironmentName*: Nazwa hello hello ASE ILB skonfigurowany.
* *existingAseLocation*: tekstem zawierającym ciąg hello region platformy Azure, w którym hello ILB ASE została wdrożona.  Na przykład: "Południowo-środkowe Stany".
* *pfxBlobString*: hello ciąg kodowany w formacie based64 reprezentację hello pliku .pfx. Fragment kodu hello przedstawiona wcześniej przy użyciu, a następnie skopiuj ciąg hello zawartych w "exportedcert.pfx.b64". Wklej go jako wartość hello hello *pfxBlobString* atrybutu.
* *hasło*: hello hasło używane toosecure hello pfx.
* *certificateThumbprint*: hello odcisk palca certyfikatu. Jeśli pobierania tej wartości ze środowiska PowerShell (na przykład *$certificate. Odcisk palca* z hello wcześniejszych fragment kodu), można użyć wartości hello jest. Po skopiowaniu hello wartości w oknie dialogowym hello certyfikat systemu Windows należy pamiętać toostrip limit hello usunięciu spacji. Witaj *certificateThumbprint* powinien wyglądać jak AF3143EB61D43F6727842115BB7F17BBCECAECAE.
* *certificateName*: identyfikator ciągu przyjazną wybranej przez użytkownika używane tooidentity hello certyfikatu. Nazwa Hello jest używana jako część hello unikatowego identyfikatora Menedżera zasobów dla hello *Microsoft.Web/certificates* jednostki, która reprezentuje hello certyfikatu SSL. Nazwa Hello *musi* kończyć hello następującego sufiksu: \_yourASENameHere_InternalLoadBalancingASE. Witaj portalu Azure używa ten sufiks wskaźnik hello certyfikat jest używany toosecure ASE włączone ILB.

Przykład skróconej *azuredeploy.parameters.json* jest następujący:

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Po hello *azuredeploy.parameters.json* plik zostanie wypełnione, skonfigurować hello domyślnego certyfikatu SSL za pomocą fragmentu kodu hello programu PowerShell. Zmień toomatch ścieżki pliku hello lokalizację plików szablonu usługi Resource Manager hello na tym komputerze. Należy pamiętać o toosupply własne wartości hello wdrożenia usługi Resource Manager i nazwy grupy zasobów hello:

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Trwa około 40 minut na ASE frontonu tooapply hello zmianę. Na przykład dla ASE o rozmiarze domyślnym wykorzystuje dwa końce frontonu, szablon hello ma około godzinę i 20 minut toocomplete. Szablon hello jest uruchomiona, nie można skalować hello ASE.  

Po zakończeniu szablonu hello aplikacje na powitania ILB ASE są dostępne za pośrednictwem protokołu HTTPS. połączenia Hello są chronione przy użyciu hello domyślnego certyfikatu SSL. certyfikat SSL domyślny Hello jest używany podczas aplikacje na powitania ILB ASE dotyczą przy użyciu kombinacji nazwy aplikacji hello oraz hello domyślną nazwę hosta. Na przykład https://mycustomapp.internal-contoso.com używa hello domyślny certyfikat SSL na potrzeby **.internal contoso.com*.

Jednak podobnie jak w aplikacji, które można uruchamiać na powitania publicznej usługi wielodostępnym, deweloperzy mogą konfigurować nazwy hosta niestandardowego dla poszczególnych aplikacji. Może również skonfigurować unikatowe powiązania certyfikatu SNI SSL dla poszczególnych aplikacji.

## <a name="app-service-environment-v1"></a>Środowisko usługi App Service — wersja 1 ##
Środowiska usługi aplikacji ma dwie wersje: ASEv1 i ASEv2. Witaj poprzedzających informacji oparto na ASEv2. Ten przedstawia sekcji hello różnice między ASEv1 i ASEv2.

ASEv1 zarządzania wszystkie zasoby hello ręcznie. Zawierającej front kończy się hello, pracowników i adresy IP używane dla opartych na protokole SSL. Zanim można skalować w poziomie planu usługi aplikacji, musisz skalowanie w poziomie hello puli procesów roboczych, które mają toohost go.

ASEv1 używa innego modelu cenowego z ASEv2. W ASEv1 płacisz za każdego rdzenia przydzielone. Zawierającej rdzeni, używanych do interfejsy lub pracowników, którzy nie są hosting dowolnych zadań. W ASEv1 hello domyślny rozmiar maksymalny skali ASE jest 55 hosty łącznie. Zawierającej pracowników i interfejsy. Jeden tooASEv1 korzyści jest, czy może on zostać wdrożony w klasycznej sieci wirtualnej i sieci wirtualnych Menedżera zasobów. toolearn więcej informacji na temat ASEv1, zobacz [wprowadzenie v1 środowiska usługi aplikacji][ASEv1Intro].

toocreate ASEv1 przy użyciu szablonu usługi Resource Manager, zobacz [utworzyć przy użyciu szablonu usługi Resource Manager v1 ILB ASE][ILBASEv1Template].


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
