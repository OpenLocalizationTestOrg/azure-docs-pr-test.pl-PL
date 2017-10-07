---
title: "aaaNode.js Wprowadzenie — przewodnik | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate proste Node.js aplikacja sieci web, a następnie wdrożyć go tooan usługi w chmurze Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>Tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure

Ten samouczek pokazuje, jak toocreate proste Node.js aplikacji uruchomionej w usłudze w chmurze Azure. Usługi w chmurze są blokami konstrukcyjnymi hello z skalowalnych aplikacji w chmurze na platformie Azure. Umożliwiają one separacji hello oraz niezależne zarządzanie i skalowania w poziomie składników frontonu i zaplecza aplikacji.  Usługi Cloud Services oferują specjalną maszynę wirtualną, która w niezawodny sposób hostuje poszczególne role.

Aby uzyskać więcej informacji dotyczących usługi w chmurze, oraz ich porównanie tooAzure witryn sieci Web i maszyn wirtualnych, zobacz [porównanie witryn sieci Web platformy Azure, usługi w chmurze i maszyn wirtualnych].

> [!TIP]
> Szukasz toobuild prosty witryny sieci Web? Jeśli scenariusz obejmuje tylko prosty fronton witryny sieci Web, rozważ użycie [korzystanie z lekkiej aplikacji sieci web]. Możesz łatwo przeprowadzić uaktualnienie tooa usługi w chmurze rozwoju witryny sieci web lub zmiany wymagań.

Wykonując czynności opisane w tym samouczku, utworzysz prostą aplikację sieci Web hostowaną wewnątrz roli sieci Web. Będzie korzystać z aplikacji tootest emulatora obliczeń hello lokalnie, a następnie wdróż je za pomocą narzędzia wiersza polecenia programu PowerShell.

Aplikacja Hello jest prostą aplikację "hello world":

![Przeglądarka wyświetlająca stronę sieci web Hello World hello][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>Wymagania wstępne
> [!NOTE]
> W tym samouczku jest używany program Azure PowerShell, który wymaga systemu Windows.

* Zainstalowanie i skonfigurowanie programu [Azure PowerShell].
* Pobierz i zainstaluj hello [zestaw Azure SDK for .NET 2.7]. W hello instalacji Instalatora, wybierz opcję:
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Tworzenie projektu Usługi w chmurze Azure
Wykonaj następujące zadania toocreate nowy projekt usługi w chmurze Azure, wraz z podstawowych szkieletów języka Node.js hello:

1. Uruchom **programu Windows PowerShell** jako Administrator; z hello **Start Menu** lub **ekranu startowego**, wyszukaj **programu Windows PowerShell**.
2. [Connect PowerShell] tooyour subskrypcji.
3. Wprowadź hello następującego środowiska PowerShell polecenia cmdlet toocreate toocreate hello projektu:

        New-AzureServiceProject helloworld

    ![wynik Hello hello New-AzureService helloworld polecenia][hello result of hello New-AzureService helloworld command]

    Witaj **New-AzureServiceProject** polecenia cmdlet wygenerowanie podstawowej struktury publikowania tooa aplikacji Node.js usługi w chmurze. Zawiera ona pliki konfiguracji niezbędne do publikowania tooAzure. Witaj polecenie cmdlet zmienia także katalog roboczy katalogu toohello hello usługi.

    polecenie cmdlet Hello tworzy hello następujące pliki:

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** i **ServiceDefinition.csdef**: specyficzne dla platformy Azure pliki niezbędne do publikowania aplikacji. Aby uzyskać więcej informacji, zobacz [Tworzenie hostowanej usługi platformy Azure — omówienie].
   * **deploymentSettings.json**: przechowuje ustawienia lokalne, które są używane przez hello polecenia cmdlet wdrażania programu Azure PowerShell.
4. Wprowadź hello następujące polecenia tooadd nową rolę sieci web:

       Add-AzureNodeWebRole

   ![dane wyjściowe Hello hello polecenia Add-AzureNodeWebRole][hello output of hello Add-AzureNodeWebRole command]

   Witaj **Add-AzureNodeWebRole** polecenie cmdlet tworzy podstawowej aplikacji Node.js. Także modyfikuje hello **.csfg** i **csdef** tooadd wpisów konfiguracji dla nowej roli hello pliki.

   > [!NOTE]
   > Jeśli nie określisz nazwy roli, będzie używana nazwa domyślna. Można podać nazwę jako pierwszym parametrem polecenia cmdlet hello:`Add-AzureNodeWebRole MyRole`

Aplikacja Node.js Hello jest zdefiniowana w pliku hello **server.js**, który znajduje się w katalogu hello hello roli sieci web (**WebRole1** domyślnie). Oto kod hello:

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Ten kod jest zasadniczo hello tak samo jak Witaj "Hello World" przykładowe na powitania [nodejs.org] witryny sieci Web, z wyjątkiem używa hello numeru portu przypisanego przez hello środowiska chmury.

## <a name="deploy-hello-application-tooazure"></a>Wdrażanie tooAzure aplikacji hello

> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) lub [zarejestrować się w celu uzyskania bezpłatnego konta](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-hello-azure-publishing-settings"></a>Pobierz hello Azure ustawienia publikowania
toodeploy Twojego tooAzure aplikacji, należy najpierw pobrać hello publikowania ustawienia dla Twojej subskrypcji platformy Azure.

1. Uruchom następujące polecenia cmdlet programu Azure PowerShell hello:

       Get-AzurePublishSettingsFile

   Zostaną użyte przeglądarkę toonavigate toohello strona pobierania ustawień publikowania. Może być zostanie wyświetlony monit o toolog za pomocą Account firmy Microsoft. Jeśli tak, użyj konta hello skojarzonego z subskrypcją platformy Azure.

   Hello pobrany profil tooa pliku lokalizacji, które łatwo uzyskiwać dostęp do zapisu.
2. Uruchom następujące polecenia cmdlet tooimport hello pobrany profil publikowania:

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > Po zaimportowaniu hello ustawień publikowania, rozważ usunięcie hello pobrany plik .publishSettings, ponieważ zawiera on informacje, które mogłyby umożliwić innym osobom tooaccess Twojego konta.

### <a name="publish-hello-application"></a>Publikowanie aplikacji hello
toopublish, uruchom następujące polecenia hello:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** Określa nazwę hello hello wdrożenia. To musi być unikatowa nazwa, w przeciwnym razie hello publikowanie proces zakończy się niepowodzeniem. Witaj **Get-Date** polecenia uwzględnia ciąg daty/godziny, który powinien zapewnić, że nazwa hello unikatowy.
* **-Lokalizacji** określa hello centrum danych, którego aplikacja hello będzie obsługiwana w systemie. listę dostępnych centrów danych, użyj hello toosee **Get-AzureLocation** polecenia cmdlet.
* **-Launch** otwiera okno przeglądarki i przechodzi toohello hostowane usługi, po zakończeniu wdrożenia.

Po publikowanie powiedzie się, zostanie wyświetlony poniżej toohello podobne odpowiedzi:

![dane wyjściowe Hello hello polecenia Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> Ona potrwać kilka minut toodeploy aplikacji hello i stają się dostępne po pierwszej publikacji.

Po zakończeniu wdrażania hello oknie przeglądarki zostanie Otwórz i przejdź toohello usługi w chmurze.

![Okno przeglądarki zawierające hello hello world strony; adres URL Hello wskazuje, że strona hello jest obsługiwana na platformie Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

Aplikacja działa teraz na platformie Azure.

Witaj **Publish-AzureServiceProject** polecenia cmdlet wykonuje hello następujące kroki:

1. Tworzy toodeploy pakietu. Pakiet HELLO zawiera wszystkie pliki hello w folderze aplikacji.
2. Tworzy nowe **konto magazynu**, jeśli takie konto jeszcze nie istnieje. Witaj kontem magazynu platformy Azure jest pakiet aplikacji hello toostore używane podczas wdrażania. Można bezpiecznie usunąć konto magazynu powitania po ukończeniu wdrażania.
3. Tworzy nową **usługę w chmurze**, jeśli taka usługa jeszcze nie istnieje. A **usługi w chmurze** jest kontenerem hello, w którym aplikacja jest hostowana po tooAzure wdrożone. Aby uzyskać więcej informacji, zobacz [Tworzenie hostowanej usługi platformy Azure — omówienie].
4. Publikuje hello wdrożenia pakietu tooAzure.

## <a name="stopping-and-deleting-your-application"></a>Zatrzymywanie i usuwanie aplikacji
Po wdrożeniu aplikacji, może być toodisable go, aby uniknąć dodatkowych kosztów. Opłaty za wystąpienia ról sieci Web na platformie Azure są naliczane za godzinę korzystania z serwera. Czas serwera jest używany, gdy aplikacja jest wdrażana, nawet jeśli hello wystąpień nie są uruchomione i są w stanie hello zatrzymana.

1. W oknie programu PowerShell Windows hello Zatrzymaj wdrożenie usługi hello utworzony w poprzedniej sekcji hello z hello następującego polecenia cmdlet:

       Stop-AzureService

   Zatrzymywanie usługi hello może potrwać kilka minut. Witaj, usługa zostanie zatrzymana, pojawi się komunikat wskazujący, że usługa została zatrzymana.

   ![Stan Hello polecenia hello Stop-AzureService][hello status of hello Stop-AzureService command]
2. Usługa hello toodelete, wywołanie hello następującego polecenia cmdlet:

       Remove-AzureService

   Po wyświetleniu monitu wprowadź **Y** toodelete hello usługi.

   Usuwanie hello usługi może potrwać kilka minut. Po usunięciu hello usługi pojawi się komunikat wskazujący, że usługa hello została usunięta.

   ![Stan Hello polecenia hello Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > Usunięcie usługi hello nie powoduje usunięcia konta magazynu hello, które zostało utworzone po początkowym opublikowaniu usługi hello i będzie toobe rozliczane użycie magazynu. Jeśli nic nie używa hello magazynu, może być toodelete go.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów środowiska Node.js].

<!-- URL List -->

[porównanie witryn sieci Web platformy Azure, usługi w chmurze i maszyn wirtualnych]: ../app-service-web/choose-web-site-cloud-service-vm.md
[korzystanie z lekkiej aplikacji sieci web]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[zestaw Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Tworzenie hostowanej usługi platformy Azure — omówienie]: https://azure.microsoft.com/documentation/services/cloud-services/
[Centrum deweloperów środowiska Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
