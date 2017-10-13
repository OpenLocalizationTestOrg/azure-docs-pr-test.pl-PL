---
title: "Wprowadzenie do języka Node.js — przewodnik | Microsoft Docs"
description: "Dowiedz się, jak utworzyć prostą aplikację sieci Web Node.js, a następnie wdrożyć ją do usługi w chmurze Azure."
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
ms.openlocfilehash: b1e08e79c7fe2acbdb9c17607641612ffa2934ee
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="build-and-deploy-a-nodejs-application-to-an-azure-cloud-service"></a>Tworzenie i wdrażanie aplikacji Node.js do usługi w chmurze Azure

Ten samouczek pokazuje, jak utworzyć prostą aplikację Node.js działającą w usłudze w chmurze Azure. Usługi Cloud Services są blokami konstrukcyjnymi skalowalnych aplikacji w chmurze na platformie Azure. Umożliwiają one rozdzielanie i skalowanie w poziomie składników frontonu i zaplecza aplikacji oraz niezależne zarządzanie nimi.  Usługi Cloud Services oferują specjalną maszynę wirtualną, która w niezawodny sposób hostuje poszczególne role.

Dalsze informacje na temat usług Cloud Services oraz ich porównanie z usługami Witryny sieci Web i Maszyny wirtualne Azure można znaleźć w temacie [Porównanie usług Azure: Witryny sieci Web, Cloud Services i Virtual Machines].

> [!TIP]
> Chcesz utworzyć prostą witrynę sieci Web? Jeśli scenariusz obejmuje tylko prosty fronton witryny sieci Web, rozważ użycie [korzystanie z lekkiej aplikacji sieci web]. Możesz łatwo przeprowadzić uaktualnienie do Usługi w chmurze w przypadku rozwoju witryny sieci Web lub zmiany wymagań.

Wykonując czynności opisane w tym samouczku, utworzysz prostą aplikację sieci Web hostowaną wewnątrz roli sieci Web. Będziesz testować aplikację w środowisku lokalnym przy użyciu emulatora obliczeń, a następnie wdrażać ją za pomocą narzędzi wiersza polecenia programu PowerShell.

Będzie to prosta aplikacja „hello world”:

![Przeglądarka wyświetlająca stronę sieci Web „Hello World”][A web browser displaying the Hello World web page]

## <a name="prerequisites"></a>Wymagania wstępne
> [!NOTE]
> W tym samouczku jest używany program Azure PowerShell, który wymaga systemu Windows.

* Zainstalowanie i skonfigurowanie programu [Azure PowerShell].
* Pobranie i zainstalowanie zestawu [Azure SDK for .NET 2.7]. Podczas instalacji wybierz następujące opcje:
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Tworzenie projektu Usługi w chmurze Azure
Wykonaj poniższe zadania w celu utworzenia nowego projektu Usługi w chmurze Azure oraz utworzenia podstawowych szkieletów języka Node.js:

1. Uruchom program **Windows PowerShell** jako administrator. Przy użyciu **menu Start** lub **ekranu startowego** wyszukaj program **Windows PowerShell**.
2. [Connect PowerShell] z subskrypcją.
3. Wprowadź następujące polecenie cmdlet programu PowerShell, aby utworzyć projekt:

        New-AzureServiceProject helloworld

    ![Wynik użycia polecenia New-AzureService helloworld][The result of the New-AzureService helloworld command]

    Polecenie cmdlet **New-AzureServiceProject** powoduje wygenerowanie podstawowej struktury publikowania aplikacji Node.js w Usłudze w chmurze. Zawiera ona pliki konfiguracji niezbędne do publikowania na platformie Azure. Polecenie cmdlet zmienia także katalog roboczy na katalog usługi.

    Polecenie cmdlet powoduje utworzenie następujących plików:

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** i **ServiceDefinition.csdef**: specyficzne dla platformy Azure pliki niezbędne do publikowania aplikacji. Aby uzyskać więcej informacji, zobacz [Tworzenie hostowanej usługi platformy Azure — omówienie].
   * **deploymentSettings.json**: przechowuje ustawienia lokalne, które są używane przez polecenia cmdlet programu Azure PowerShell dotyczące wdrożenia.
4. Wprowadź poniższe polecenie, aby dodać nową rolę sieci Web:

       Add-AzureNodeWebRole

   ![Dane wyjściowe polecenia Add-AzureNodeWebRole][The output of the Add-AzureNodeWebRole command]

   Polecenie cmdlet **Add-AzureNodeWebRole** służy do tworzenia podstawowej aplikacji Node.js. Powoduje ono również modyfikowanie plików **.csfg** i **.csdef** w celu dodania wpisów konfiguracji dla nowej roli.

   > [!NOTE]
   > Jeśli nie określisz nazwy roli, będzie używana nazwa domyślna. Nazwa może być pierwszym parametrem polecenia cmdlet: `Add-AzureNodeWebRole MyRole`

Aplikacja Node.js jest definiowana w pliku **server.js**, który znajduje się w katalogu dla roli sieci Web (domyślnie **WebRole1**). Oto kod:

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Ten kod jest zasadniczo taki sam jak przykładowy kod „Hello World” w witrynie sieci Web [nodejs.org], z wyjątkiem tego, że używa numeru portu przypisanego przez środowisko chmury.

## <a name="deploy-the-application-to-azure"></a>Wdrażanie aplikacji na platformie Azure

> [!NOTE]
> Do ukończenia tego samouczka jest potrzebne konto platformy Azure. Możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) lub [zarejestrować się w celu uzyskania bezpłatnego konta](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-the-azure-publishing-settings"></a>Pobieranie ustawień publikowania na platformie Azure
Aby wdrożyć aplikację na platformie Azure, należy najpierw pobrać ustawienia publikowania dla subskrypcji platformy Azure.

1. Uruchom poniższe polecenie cmdlet programu Azure PowerShell:

       Get-AzurePublishSettingsFile

   Spowoduje to przejście do strony pobierania ustawień publikowania w przeglądarce. Może pojawić się monit o zalogowanie się przy użyciu konta Microsoft. W takiej sytuacji należy użyć konta skojarzonego z subskrypcją platformy Azure.

   Zapisz pobrany profil w łatwo dostępnej lokalizacji pliku.
2. Uruchom poniższe polecenie cmdlet, aby zaimportować pobrany profil publikowania:

       Import-AzurePublishSettingsFile [path to file]

    > [!NOTE]
    > Po zaimportowaniu ustawień publikowania rozważ usunięcie pobranego pliku .publishSettings, ponieważ zawiera on informacje, które mogłyby umożliwić innym osobom uzyskanie dostępu do Twojego konta.

### <a name="publish-the-application"></a>Publikowanie aplikacji
Aby opublikować aplikację, uruchom następujące polecenie:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** — określa nazwę wdrożenia. Musi być to nazwa unikatowa. W przeciwnym razie proces publikowania zakończy się niepowodzeniem. Polecenie **Get-Date** uwzględnia ciąg daty i godziny, który powinien zapewnić unikatowość nazwy.
* **-Location** — określa centrum danych, w którym aplikacja będzie hostowana. Aby wyświetlić listę dostępnych centrów danych, użyj polecenia cmdlet **Get-AzureLocation**.
* **-Launch** — otwiera okno przeglądarki i przechodzi do usługi hostowanej po zakończeniu wdrożenia.

Po pomyślnym zakończeniu publikowania zostanie wyświetlona odpowiedź podobna do następującej:

![Dane wyjściowe polecenia Publish-AzureService][The output of the Publish-AzureService command]

> [!NOTE]
> W przypadku publikowania aplikacji po raz pierwszy jej wdrożenie i udostępnienie może potrwać kilka minut.

Po zakończeniu wdrożenia zostanie otwarte okno przeglądarki i nastąpi przejście do usługi w chmurze.

![Okno przeglądarki ze stroną „hello world”; adres URL wskazuje, że strona jest obsługiwana na platformie Azure.][A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]

Aplikacja działa teraz na platformie Azure.

Polecenie cmdlet **Publish-AzureServiceProject** wykonuje następujące czynności:

1. Tworzy pakiet do wdrożenia. Pakiet zawiera wszystkie pliki w folderze aplikacji.
2. Tworzy nowe **konto magazynu**, jeśli takie konto jeszcze nie istnieje. Konto magazynu Azure jest używane do przechowywania pakietu aplikacji podczas wdrażania. Po ukończeniu wdrażania konto magazynu można bezpiecznie usunąć.
3. Tworzy nową **usługę w chmurze**, jeśli taka usługa jeszcze nie istnieje. **Usługa w chmurze** to kontener, w którym aplikacja jest hostowana po wdrożeniu na platformie Azure. Aby uzyskać więcej informacji, zobacz [Tworzenie hostowanej usługi platformy Azure — omówienie].
4. Publikuje pakiet wdrożeniowy na platformie Azure.

## <a name="stopping-and-deleting-your-application"></a>Zatrzymywanie i usuwanie aplikacji
Po wdrożeniu aplikacji można ją wyłączyć, aby uniknąć dodatkowych kosztów. Opłaty za wystąpienia ról sieci Web na platformie Azure są naliczane za godzinę korzystania z serwera. Czas serwera jest używany po wdrożeniu aplikacji, nawet jeśli wystąpienia nie zostały uruchomione i są w stanie zatrzymania.

1. W oknie programu Windows PowerShell zatrzymaj wdrożenie usługi utworzone w poprzedniej sekcji za pomocą następującego polecenia cmdlet:

       Stop-AzureService

   Zatrzymywanie usługi może potrwać kilka minut. Po zatrzymaniu usługi pojawi się komunikat wskazujący, że usługa została zatrzymana.

   ![Stan polecenia Stop-AzureService][The status of the Stop-AzureService command]
2. Aby usunąć usługę, wywołaj następujące polecenie cmdlet:

       Remove-AzureService

   Po wyświetleniu monitu wpisz **Y**, aby usunąć usługę.

   Usuwanie usługi może potrwać kilka minut. Po usunięciu usługi pojawi się komunikat z informacją, że usługa została usunięta.

   ![Stan polecenia Remove-AzureService][The status of the Remove-AzureService command]

   > [!NOTE]
   > Usunięcie usługi nie powoduje usunięcia konta magazynu, które zostało utworzone po początkowym opublikowaniu usługi, a opłaty za użycie magazynu będą nadal naliczane. Jeśli nic innego nie korzysta z magazynu, możesz go usunąć.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, odwiedź stronę [Centrum deweloperów środowiska Node.js].

<!-- URL List -->

[Porównanie usług Azure: Witryny sieci Web, Cloud Services i Virtual Machines]: ../app-service/choose-web-site-cloud-service-vm.md
[korzystanie z lekkiej aplikacji sieci web]: ../app-service/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Tworzenie hostowanej usługi platformy Azure — omówienie]: https://azure.microsoft.com/documentation/services/cloud-services/
[Centrum deweloperów środowiska Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[The result of the New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[The output of the Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying the Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[The status of the Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[The status of the Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
