---
title: "aaaBind istniejących SSL niestandardowych certyfikatów aplikacji sieci Web tooAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się tootoobind niestandardowej aplikacji sieci web tooyour certyfikatu SSL, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>Powiąż istniejący niestandardowy SSL certyfikatu tooAzure aplikacji sieci Web

Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web. Ten samouczek pokazuje, jak toobind SSL niestandardowych certyfikatów, czemu zakupionego od zaufanego urzędu certyfikacji za[Azure Web Apps](app-service-web-overview.md). Po zakończeniu będziesz w stanie tooaccess aplikacji sieci web na punkt końcowy HTTPS hello DNS domeny niestandardowej.

![Aplikacja sieci Web z niestandardowego certyfikatu SSL](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Uaktualnij warstwę cenową aplikacji
> * Powiąż z niestandardowych tooApp certyfikatu SSL usługi
> * Wymuszanie protokołu HTTPS dla aplikacji
> * Powiązania certyfikatu SSL za pomocą skryptów automatyzacji

> [!NOTE]
> Tooget niestandardowego certyfikatu SSL, należy możesz pobrać go w portalu Azure hello bezpośrednio i powiązać ją tooyour aplikacji sieci web. Wykonaj hello [certyfikaty usługi aplikacji — samouczek](web-sites-purchase-ssl-web-site.md).

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

- [Utwórz aplikację usługi aplikacji](/azure/app-service/)
- [Mapy niestandardowej aplikacji sieci web tooyour nazwy DNS](app-service-web-tutorial-custom-domain.md)
- Uzyskanie certyfikatu SSL z zaufanego urzędu certyfikacji

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>Wymagania dotyczące certyfikatu SSL

toouse certyfikatów w usłudze App Service, hello certyfikatu musi spełniać wszystkie hello następujące wymagania:

* Podpisane przez zaufany urząd certyfikacji
* Eksportowane jako chronionego hasłem pliku PFX
* Zawiera klucz prywatny co najmniej 2048 bitów długo
* Zawiera wszystkie certyfikaty pośrednie w łańcuchu certyfikatów hello

> [!NOTE]
> **Certyfikaty krzywa Cryptography (ECC) eliptycznej** może współpracować z usługi aplikacji, ale nie są objęte w tym artykule. Współpraca z urzędu certyfikacji na powitania kolejnych kroków toocreate ECC certyfikatów.

## <a name="prepare-your-web-app"></a>Przygotowanie aplikacji sieci web

toobind SSL niestandardowych certyfikatów tooyour aplikacji sieci web, z [planu usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/) musi być w hello **podstawowe**, **standardowe**, lub **Premium** warstwy. W tym kroku możesz upewnij się, że aplikacja sieci web jest w hello obsługiwane warstwy cenowej.

### <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Otwórz hello [portalu Azure](https://portal.azure.com).

### <a name="navigate-tooyour-web-app"></a>Przejdź do aplikacji sieci web tooyour

W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web.

![Wybierz aplikację sieci web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

Jest strony Zarządzanie hello aplikacji sieci web.  

### <a name="check-hello-pricing-tier"></a>Sprawdź hello warstwy cenowej

W nawigacji po lewej stronie powitania strony aplikacji sieci web, przewiń toohello **ustawienia** a następnie wybierz opcję **skalowanie w górę (plan usługi App Service)**.

![Skalowanie w pionie menu](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

Sprawdź toomake się, że aplikacja sieci web nie jest hello **wolne** lub **Shared** warstwy. Warstwa bieżąca aplikacja sieci web jest wyróżniony ciemny niebieskie pole.

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

Niestandardowe SSL nie jest obsługiwany w hello **wolne** lub **Shared** warstwy. Jeśli potrzebujesz tooscale zapasowych, wykonaj kroki hello w następnej sekcji hello. W przeciwnym razie Zamknij hello **wybierz warstwę cenową** strony i pominąć zbyt[przekazywanie i powiązać certyfikatu SSL](#upload).

### <a name="scale-up-your-app-service-plan"></a>Skalowanie w górę plan usługi aplikacji

Wybierz jedną z hello **podstawowe**, **standardowe**, lub **Premium** warstw.

Kliknij pozycję **Wybierz**.

![Wybierz warstwę cenową](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

Po wyświetleniu powiadomienia hello hello skali operacja została zakończona.

![Skalowanie w górę powiadomień](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>Powiąż certyfikat protokołu SSL

Możesz są gotowe tooupload aplikację sieci web uzyskiwania informacji na temat tooyour certyfikatu SSL.

### <a name="merge-intermediate-certificates"></a>Certyfikaty pośrednie scalenia

Urzędu certyfikacji zawiera wiele certyfikatów w łańcuchu certyfikatów hello, należy najpierw toomerge hello certyfikaty w kolejności. 

toodo to open każdego certyfikatu otrzymane w edytorze tekstów. 

Utwórz plik certyfikatu scalonych hello, nazywany _mergedcertificate.crt_. W edytorze tekstów skopiuj zawartość hello każdy z certyfikatów do tego pliku. kolejność Hello certyfikaty powinna wyglądać hello następującego szablonu:

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>Eksportuj certyfikat tooPFX

Eksportowanie scalonych certyfikatu SSL z kluczem prywatnym hello wygenerowania żądania certyfikatu z.

Jeśli generowany jest żądanie certyfikatu przy użyciu biblioteki OpenSSL, został utworzony plik klucza prywatnego. tooexport Twojego tooPFX certyfikat, uruchom następujące polecenie hello. Zastąp symbole zastępcze hello  _&lt;plików kluczy prywatnych >_ i  _&lt;scalić — plik certyfikatu >_.

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

Po wyświetleniu monitu, należy określić hasło eksportu. To hasło będzie używany podczas przekazywania z protokołu SSL certyfikatu tooApp usługi później.

Jeśli używasz usług IIS lub _Certreq.exe_ toogenerate Twojego żądania certyfikatu, zainstaluj hello certyfikatu tooyour komputera lokalnego, a następnie [wyeksportować hello certyfikatu tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).

### <a name="upload-your-ssl-certificate"></a>Przekaż certyfikat protokołu SSL

tooupload certyfikatu SSL, kliknij przycisk **certyfikaty SSL** w hello lewy pasek nawigacyjny aplikacji sieci web.

Kliknij przycisk **Przekaż certyfikat**.

W **plik certyfikatu PFX**, wybierz plik w formacie PFX. W **hasło certyfikatu**, wpisz hasło hello, utworzonego podczas eksportowania pliku PFX hello.

Kliknij pozycję **Przekaż**.

![Przekazywanie certyfikatu](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

Po zakończeniu przekazywania certyfikatu usługi aplikacji był w hello **certyfikaty SSL** strony.

![Przekazany certyfikat](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>Powiąż certyfikat protokołu SSL

W hello **powiązania SSL** kliknij **dodać powiązanie**.

W hello **Dodaj powiązanie SSL** Użyj hello listę rozwijaną tooselect hello domeny nazwa toosecure i hello toouse certyfikatu.

> [!NOTE]
> Jeśli zostały przekazane certyfikat, ale nie ma nazwy domeny hello w hello **Hostname** listy rozwijanej, spróbuj odświeżyć stronę przeglądarki hello.
>
>

W **typu SSL**, wybierz pozycję czy toouse  **[oznaczenia nazwy serwera (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  lub opartych na protokole SSL.

- **SSL opartego na protokole SNI** -powiązania SSL opartego na wiele SNI mogą zostać dodane. Ta opcja umożliwia wielu toosecure certyfikaty SSL wielu domen na powitania tego samego adresu IP. Większość nowoczesnych przeglądarek (w tym programu Internet Explorer, Chrome, Firefox i Opera) obsługuje SNI (znaleźć bardziej szczegółowe informacje pomocy technicznej przeglądarki na [wskaźnika nazwy serwera](http://wikipedia.org/wiki/Server_Name_Indication)).
- **Oparte na protokole SSL** — mogą być dodawane tylko jednego powiązania SSL opartego na protokole IP. Ta opcja umożliwia tylko jeden toosecure certyfikatu SSL dedykowanych publicznego adresu IP. toosecure wiele domen, należy zabezpieczyć je przy użyciu wszystkich hello tego samego certyfikatu SSL. To jest opcją tradycyjnych hello powiązania SSL.

Kliknij przycisk **dodać powiązanie**.

![Powiąż certyfikat protokołu SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

Po zakończeniu przekazywania certyfikatu usługi aplikacji był w hello **powiązania SSL** sekcje.

![Certyfikat powiązany tooweb aplikacji](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>Ponowne mapowanie rekord dla protokołu SSL z adresu IP

Jeśli nie używasz w aplikacji sieci web opartych na protokole SSL, Pomiń zbyt[HTTPS testu dla domeny niestandardowej](#test).

Domyślnie aplikacja sieci web używa udostępnionego publicznego adresu IP. Gdy Powiąż certyfikat z SSL opartego na protokole IP, usługi aplikacji — tworzy nowy, dedykowany adres IP dla aplikacji sieci web.

Jeśli zamapowaniu aplikacji sieci web tooyour rekordów A, zaktualizować rejestr domeny ten nowy, dedykowany adres IP.

Aplikacja sieci web **domeny niestandardowe** strona zostanie zaktualizowana przy hello nowy, dedykowany adres IP. [Skopiuj ten adres IP](app-service-web-tutorial-custom-domain.md#info), następnie [ponownego mapowania hello rekord](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nowego adresu IP.

<a name="test"></a>

## <a name="test-https"></a>Test protokołu HTTPS

Teraz opuścił toodo jest toomake się upewnić, że HTTPS działa dla domeny niestandardowej. W różnych przeglądarkach, Przeglądaj zbyt`https://<your.custom.domain>` toosee pełniącą zapasowej swojej aplikacji sieci web.

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> Jeśli aplikacja sieci web udostępnia certyfikatu błędy sprawdzania poprawności, prawdopodobnie używasz certyfikatu z podpisem własnym.
>
> Jeśli nie jest to przypadek hello, mogą być przechowywane poza certyfikaty pośrednie podczas eksportowania pliku PFX toohello certyfikatu.

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>Wymuszanie protokołu HTTPS

Usługa aplikacji ma *nie* Wymuszanie protokołu HTTPS, więc każdy może nadal uzyskiwać dostęp do aplikacji sieci web przy użyciu protokołu HTTP. tooenforce HTTPS dla aplikacji sieci web, zdefiniuj reguły ponownego zapisywania w hello _web.config_ plików dla aplikacji sieci web. Ten plik, niezależnie od hello strukturę języka aplikacji sieci web korzysta z usługi aplikacji.

> [!NOTE]
> Jest specyficzny dla języka Przekierowywanie żądań. ASP.NET MVC można użyć hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtru zamiast reguły ponownego zapisywania hello w _web.config_.

Jeśli jesteś deweloperem .NET stosunkowo zapoznaj się z tym plikiem. Znajduje się w głównym hello rozwiązania.

Można również w przypadku tworzenia z PHP, Node.js, Python lub Java, jest stosowany ten plik w Twoim imieniu możemy generowane w usłudze App Service.

Łączenie aplikacji sieci web tooyour końcowego FTP wykonując instrukcje hello [wdrażanie tooAzure Twojej aplikacji App Service przy użyciu FTP/S](app-service-deploy-ftp.md).

Ten plik powinien znajdować się w _/home/site/wwwroot_. Jeśli nie, należy utworzyć _web.config_ plik w tym folderze z powitania po XML:

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

Dla istniejącej _web.config_ plików, skopiować cały hello `<rule>` element do Twojej _web.config_w `configuration/system.webServer/rewrite/rules` elementu. Jeśli istnieją inne `<rule>` elementów w Twojej _web.config_, hello miejsce skopiowane `<rule>` element przed hello innych `<rule>` elementów.

Ta reguła zwraca protokół HTTP 301 (Stałe przekierowanie) toohello HTTPS zawsze, gdy użytkownik hello sprawia, że aplikacja sieci web tooyour żądania HTTP. Na przykład przekierowuje z `http://contoso.com` zbyt`https://contoso.com`.

Aby uzyskać więcej informacji na powitania moduł ponowne zapisywanie adresów URL usług IIS, zobacz hello [ponowne zapisywanie adresów URL](http://www.iis.net/downloads/microsoft/url-rewrite) dokumentacji.

## <a name="enforce-https-for-web-apps-on-linux"></a>Wymuszanie protokołu HTTPS dla aplikacji sieci Web w systemie Linux

Usługa aplikacji w systemie Linux ma *nie* Wymuszanie protokołu HTTPS, więc każdy może nadal uzyskiwać dostęp do aplikacji sieci web przy użyciu protokołu HTTP. tooenforce HTTPS dla aplikacji sieci web, zdefiniuj reguły ponownego zapisywania w hello _.htaccess_ plików dla aplikacji sieci web. 

Łączenie aplikacji sieci web tooyour końcowego FTP wykonując instrukcje hello [wdrażanie tooAzure Twojej aplikacji App Service przy użyciu FTP/S](app-service-deploy-ftp.md).

W _/home/site/wwwroot_, Utwórz _.htaccess_ pliku z hello następującego kodu:

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

Ta reguła zwraca protokół HTTP 301 (Stałe przekierowanie) toohello HTTPS zawsze, gdy użytkownik hello sprawia, że aplikacja sieci web tooyour żądania HTTP. Na przykład przekierowuje z `http://contoso.com` zbyt`https://contoso.com`.

## <a name="automate-with-scripts"></a>Zautomatyzować za pomocą skryptów

Można zautomatyzować powiązań SSL dla aplikacji sieci web za pomocą skryptów przy użyciu hello [interfejsu wiersza polecenia Azure](/cli/azure/install-azure-cli) lub [programu Azure PowerShell](/powershell/azure/overview).

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

Witaj następujące polecenia przekazuje wyeksportowanego pliku PFX i pobiera hello odcisk palca.

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

Witaj następujące polecenie dodaje powiązania SSL opartego na protokole SNI, za pomocą odcisku palca hello z hello poprzednie polecenie.

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

Witaj następujące polecenie przekazuje wyeksportowanego pliku PFX i dodaje powiązania SSL opartego na SNI.

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Uaktualnij warstwę cenową aplikacji
> * Powiąż z niestandardowych tooApp certyfikatu SSL usługi
> * Wymuszanie protokołu HTTPS dla aplikacji
> * Powiązania certyfikatu SSL za pomocą skryptów automatyzacji

Jak przejść dalej toolearn samouczka toohello toouse Azure Content Delivery Network.

> [!div class="nextstepaction"]
> [Dodaj tooan sieci dostarczania zawartości (CDN) usługi Azure App Service](app-service-web-tutorial-content-delivery-network.md)
