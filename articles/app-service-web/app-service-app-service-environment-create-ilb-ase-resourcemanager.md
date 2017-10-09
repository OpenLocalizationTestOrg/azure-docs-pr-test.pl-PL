---
title: "tooCreate aaaHow ILB ASE przy użyciu usługi Azure Resource Manager szablonów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate jako wewnętrzne załadować ASE równoważenia przy użyciu szablonów usługi Azure Resource Manager."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>Jak tooCreate ILB ASE przy użyciu usługi Azure Resource Manager szablonów

> [!NOTE] 
> Ten artykuł dotyczy hello v1 środowiska usługi aplikacji. Istnieje nowsza wersja hello środowiska usługi aplikacji jest łatwiejsze toouse, który jest uruchamiany na bardziej zaawansowanych infrastruktury. więcej informacji na temat nowej wersji hello rozpoczynać hello toolearn [toohello wprowadzenie środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).
>

## <a name="overview"></a>Omówienie
Środowiska usługi aplikacji mogą być tworzone za pomocą adresu wewnętrznej sieci wirtualnej zamiast publicznego adresu VIP.  Ten adres wewnętrzny są udostępniane przez składnik Azure o nazwie hello wewnętrznego modułu równoważenia obciążenia (ILB).  ASE ILB mogą być tworzone przy użyciu hello portalu Azure.  Można również tworzyć, przy użyciu automatyzacji i szablony usługi Azure Resource Manager.  W tym artykule przedstawiono kroki hello i składni konieczne toocreate ASE ILB przy użyciu szablonów usługi Azure Resource Manager.

Istnieją trzy kroki związane z automatyzacji tworzenia ASE ILB:

1. Pierwszy ASE podstawowej hello jest tworzony w sieć wirtualną przy użyciu adres usługi równoważenia obciążenia wewnętrznego, zamiast publicznego adresu VIP.  W ramach tego kroku nazwę domeny katalogu głównego jest przypisany toohello ILB ASE.
2. Po przekazaniu hello utworzone ILB ASE, certyfikat SSL.  
3. Witaj przekazano certyfikat SSL jest jawnie przypisanej toohello ILB ASE jako swojego certyfikatu SSL "domyślny".  Ten certyfikat protokołu SSL będzie służyć do tooapps ruchu protokołu SSL na powitania ILB ASE, gdy aplikacji hello są adresowane za pomocą hello wspólnej głównej domenie przypisane toohello ASE (np. https://someapp.mycustomrootcomain.com)

## <a name="creating-hello-base-ilb-ase"></a>Tworzenie hello Base ILB ASE
Przykład szablonu usługi Azure Resource Manager i jego pliku skojarzone z nimi parametry są dostępne w serwisie GitHub [tutaj][quickstartilbasecreate].

Większość parametrów hello na powitania *azuredeploy.parameters.json* plików są typowe toocreating zarówno ASEs ILB również ASEs powiązany tooa publicznego adresu VIP.  listy Hello poniżej wywołania parametry specjalne Uwaga out lub które są unikatowe, tworząc ASE ILB:

* *interalLoadBalancingMode*: W większości przypadków należy ustawić ten too3, co oznacza zarówno ruchu HTTP/HTTPS na porty 80/443, i portów kanału danych/sterowania hello nasłuch tooby usługi hello FTP na powitania ASE, zostaną powiązane tooan ILB przydzielone sieci wirtualnej wewnętrzny adres.  Jeśli ta właściwość ma wartość too2, zamiast tego, a następnie hello tylko usługa FTP związane z portów (kanały zarówno kontroli, jak i dane), który zostanie powiązany adres tooan ILB podczas pozostanie hello ruchu HTTP/HTTPS na powitania publicznego adresu VIP.
* *dnsSuffix*: ten parametr określa hello domyślnej główny domeny, zostanie przypisana toohello ASE.  W publicznej wersji hello Azure App Service, hello domyślna domena główna dla wszystkich aplikacji w sieci web to *azurewebsites.net*.  Jednak ponieważ ASE ILB wewnętrzny tooa klienta sieci wirtualnej, nie należy znaczeniu toouse hello publicznej usługi domyślnej domeny katalogu głównego.  Zamiast tego ASE ILB powinien mieć domyślnej domeny katalogu głównego, pasującą do użytku w wewnętrznej sieci wirtualnej firmy.  Na przykład użyć hipotetyczny Contoso Corporation domyślną domeną katalogu głównego *wewnętrzny contoso.com* dla aplikacji, które są przeznaczone tooonly być rozpoznawalna i jest dostępny w sieci wirtualnej firmy Contoso. 
* *ipSslAddressCount*: ten parametr jest automatycznie ustawiana domyślnie tooa wartość 0 w hello *azuredeploy.json* pliku, ponieważ ILB ASEs mieć tylko jeden adres ILB.  Nie ma żadnych jawnych adresów IP protokołu SSL dla ASE ILB, a więc hello puli adresów IP protokołu SSL dla ASE ILB musi być ustawiona toozero, w przeciwnym razie wystąpi błąd inicjowania obsługi administracyjnej. 

Raz hello *azuredeploy.parameters.json* pliku wprowadzony dla ASE ILB, hello ILB ASE można będzie utworzyć przy użyciu hello następującego fragmentu kodu programu Powershell.  Zmień toomatch ścieżki pliku hello lokalizację plików szablonów usługi Azure Resource Manager hello na tym komputerze.  Należy również pamiętać o toosupply własne wartości dla nazwy wdrożenia usługi Azure Resource Manager hello i nazwa grupy zasobów.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Po hello Azure Resource Manager szablonu jest złożone potrwa toobe ILB ASE hello utworzone po kilku godzinach.  Po zakończeniu tworzenia hello hello ILB ASE będą widoczne w portalu hello UX hello liście środowiska usługi aplikacji hello subskrypcji, która wyzwoliła hello wdrożenia.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>Przekazywanie i konfigurowanie hello "Default" certyfikat SSL
Raz hello jest tworzone ILB ASE, certyfikat SSL powinna być skojarzona z hello ASE jako domyślny"hello" korzystają z certyfikatów SSL do ustanawiania tooapps połączenia SSL.  Sufiks kontynuowaniem hipotetyczny przykład Contoso Corporation Witaj, jeśli hello ASE na domyślne DNS jest *wewnętrzny contoso.com*, następnie połączenie zbyt*https://some-random-app.internal-contoso.com*wymaga certyfikatu SSL, który jest prawidłowy dla **.internal contoso.com*. 

Istnieją różne sposoby tooobtain ważnego certyfikatu SSL tym wewnętrzne urzędy certyfikacji, zakup certyfikatu od zewnętrznego wystawcy i przy użyciu certyfikatu z podpisem własnym.  Niezależnie od źródła hello hello certyfikatu SSL hello następujące atrybuty certyfikatu należy toobe prawidłowo skonfigurowane:

* *Temat*: ten atrybut musi być ustawiony zbyt **.your głównego domeny here.com*
* *Alternatywna nazwa podmiotu*: ten atrybut musi zawierać zarówno **.your głównego domeny here.com*, i **.scm.your-głównego-domeny-here.com*.  Hello drugi wpis hello jest przyczyna tego toohello połączenia SSL witryny SCM/Kudu skojarzonej z każdej aplikacji zostaną wprowadzone przy użyciu adresu formularza hello *your-app-name.scm.your-root-domain-here.com*.

Przy użyciu prawidłowego certyfikatu SSL w ręcznie potrzebne są dwa dodatkowe czynności przygotowawczych.  certyfikat SSL Hello musi toobe przekonwertować/zapisany jako plik pfx.  Należy pamiętać, ten plik PFX hello wymaga tooinclude wszystkie pośrednie i certyfikaty główne, a musi również toobe zabezpieczony hasłem.

Następnie plik PFX wynikowe hello wymaga toobe przekonwertowany na ciąg base64, ponieważ certyfikat SSL hello zostaną przekazane za pomocą szablonu usługi Azure Resource Manager.  Ponieważ szablonów usługi Azure Resource Manager są plikami tekstowymi, plik PFX hello musi toobe przekonwertować na ciąg w formacie base64, może zostać dołączony jako parametr szablonu hello.

Poniższy fragment kodu programu Powershell Hello pokazano przykład generowania certyfikatu z podpisem własnym, eksportowanie certyfikatu hello jako plik PFX konwertowania pliku PFX hello na base64 ciąg kodowany w formacie, a następnie zapisując hello base64 zakodowany ciąg tooa oddzielny plik.  Witaj kod programu Powershell dla kodowania base64 pochodzi z hello [Blog skryptów Powershell][examplebase64encoding].

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

Po hello certyfikat SSL został pomyślnie wygenerowany i ciąg kodowany w formacie base64 tooa przekonwertowany, hello przykład szablonu usługi Azure Resource Manager w witrynie GitHub dla [Konfigurowanie certyfikatu SSL domyślne hello] [ configuringDefaultSSLCertificate] mogą być używane.

Witaj parametrów w hello *azuredeploy.parameters.json* plików wymienionych poniżej:

* *appServiceEnvironmentName*: Nazwa hello hello ASE ILB skonfigurowany.
* *existingAseLocation*: tekstem zawierającym ciąg hello region platformy Azure, w którym hello ILB ASE została wdrożona.  Na przykład: "Południowo-środkowe Stany".
* *pfxBlobString*: hello based64 zakodowany plik PFX hello reprezentację ciągu.  Przy użyciu hello fragment kodu pokazano wcześniej, czy kopiowania ciąg hello zawartych w "exportedcert.pfx.b64" i wklej go jako wartość hello hello *pfxBlobString* atrybutu.
* *hasło*: hello hasło używane toosecure hello pfx.
* *certificateThumbprint*: hello odcisk palca certyfikatu.  Jeśli pobierania tej wartości ze środowiska Powershell (np. *$certificate. Odcisk palca* z hello wcześniejszych fragment kodu), można użyć wartości hello jako — jest.  Jednak jeśli kopiujesz wartość hello z okna dialogowego certyfikatu Windows hello, należy pamiętać, toostrip limit hello usunięciu spacji.  Witaj *certificateThumbprint* powinien wyglądać mniej więcej tak: AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *certificateName*: identyfikator ciągu przyjazną wybranej przez użytkownika używane tooidentity hello certyfikatu.  Nazwa Hello jest używana jako część hello unikatowego identyfikatora Menedżera zasobów Azure dla hello *Microsoft.Web/certificates* jednostki reprezentujący hello certyfikatu SSL.  Nazwa Hello **musi** kończyć hello następującego sufiksu: \_yourASENameHere_InternalLoadBalancingASE.  Ten sufiks jest używana przez hello portal jako wskaźnik hello certyfikat służy do zabezpieczania ASE włączone ILB.

Przykład skróconej *azuredeploy.parameters.json* przedstawiono poniżej:

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

Raz hello *azuredeploy.parameters.json* wypełnione pliku, hello domyślnego certyfikatu SSL można skonfigurować przy użyciu hello następującego fragmentu kodu programu Powershell.  Zmień toomatch ścieżki pliku hello lokalizację plików szablonów usługi Azure Resource Manager hello na tym komputerze.  Należy również pamiętać o toosupply własne wartości dla nazwy wdrożenia usługi Azure Resource Manager hello i nazwa grupy zasobów.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Po hello Azure Resource Manager szablonu jest złożone potrwa około 40 minutach minut na zmianę hello frontonu tooapply ASE.  Na przykład z domyślną ASE rozmiarze przy użyciu dwa końce przodu, szablon hello potrwa około godzinę i dwadzieścia minut toocomplete.  Szablon hello jest uruchomiona hello ASE nie będą mogli tooscaled.  

Po zakończeniu szablonu hello aplikacje na powitania ILB ASE jest możliwy za pośrednictwem protokołu HTTPS i hello połączenia będzie można zabezpieczyć przy użyciu hello domyślnego certyfikatu SSL.  certyfikat SSL domyślny Hello będzie można użyć, gdy aplikacje na powitania ILB ASE są opisane przy użyciu kombinacji nazwy aplikacji hello oraz nazwa hosta domyślnego hello.  Na przykład *https://mycustomapp.internal-contoso.com* użyje hello domyślny certyfikat SSL na potrzeby **.internal contoso.com*.

Jednak podobnie jak aplikacje działające na usługę wielodostępną na publiczny hello, deweloperzy mogą również skonfigurować nazwy hosta niestandardowego dla poszczególnych aplikacji, a następnie skonfiguruj unikatowy powiązania certyfikatu SNI SSL dla poszczególnych aplikacji.  

## <a name="getting-started"></a>Wprowadzenie
tooget wprowadzenie do środowiska usługi App Service, zobacz [tooApp wprowadzenie środowiska usługi](app-service-app-service-environment-intro.md)

Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

