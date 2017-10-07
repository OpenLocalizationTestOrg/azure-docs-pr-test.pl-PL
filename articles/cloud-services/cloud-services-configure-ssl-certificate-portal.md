---
title: "aaaConfigure protokołu SSL dla usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toospecify punkt końcowy HTTPS dla roli sieci web i jak tooupload SSL certyfikatów toosecure aplikacji. Poniższe przykłady użycia hello portalu Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a>Konfigurowanie protokołu SSL dla aplikacji na platformie Azure
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-configure-ssl-certificate-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-configure-ssl-certificate.md)
>

Metoda zabezpieczania danych przesyłanych między hello hello najczęściej używane jest szyfrowanie Secure Socket Layer (SSL) internet. To zadanie typowe omówiono sposób toospecify punkt końcowy HTTPS dla roli sieci web i jak tooupload SSL certyfikatów toosecure aplikacji.

> [!NOTE]
> Usługi w chmurze tooAzure; Zastosuj Hello procedur w tym zadaniu dla usług aplikacji, zobacz [to](../app-service-web/web-sites-configure-ssl-certificate.md).
>

To zadanie używa wdrożenia produkcyjnego. Informacji na temat używania tymczasowej wdrożenia znajduje się na powitania na końcu tego tematu.

Odczyt [to](cloud-services-how-to-create-deploy-portal.md) pierwszy, jeśli nie utworzono jeszcze usługi w chmurze.

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>Krok 1: Uzyskiwanie certyfikatu SSL.
tooconfigure protokołu SSL dla aplikacji, należy najpierw tooget certyfikat SSL, który został podpisany przez urząd certyfikacji, zaufanych innej firmy, który wystawia certyfikaty w tym celu. Jeśli nie masz już jeden, należy tooobtain jedną z firmy, która sprzedaje certyfikatów SSL.

Hello certyfikatu musi spełniać następujące wymagania dotyczące certyfikatów SSL na platformie Azure hello:

* Witaj, certyfikat musi zawierać klucz prywatny.
* Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, można eksportować tooa plik wymiany informacji osobistych (pfx).
* Hello nazwa podmiotu certyfikatu musi odpowiadać usługi hello tooaccess hello domeny użytej w chmurze. Nie można uzyskać certyfikatu SSL z urzędu certyfikacji (CA) dla domeny cloudapp.net hello. Należy uzyskać toouse nazwy domeny niestandardowej podczas dostępu usługi. Podczas żądania certyfikatu z urzędu certyfikacji, nazwa podmiotu certyfikatu hello musi odpowiadać hello domenę niestandardową nazwę używaną tooaccess aplikacji. Na przykład jeśli nazwą domeny niestandardowej jest **contoso.com** może zażądać certyfikatu od urzędu certyfikacji dla ***. contoso.com** lub **www.contoso.com**.
* Witaj certyfikatu należy użyć co najmniej 2048-bitowego szyfrowania.

Do celów testowych możesz [utworzyć](cloud-services-certs-create.md) i użycia certyfikatu z podpisem własnym. Certyfikatu z podpisem własnym nie jest uwierzytelniony za pośrednictwem urzędu certyfikacji i używać jako adres URL witryny sieci Web hello hello cloudapp.net domeny. Na przykład hello następujące zadanie używa certyfikatu z podpisem własnym w których hello jest nazwa pospolita (CN) używane w certyfikacie hello **sslexample.cloudapp.net**.

Następnie musi zawierać informacje o certyfikacie hello w definicji usługi oraz pliki konfiguracji usługi.

<a name="modify"> </a>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>Krok 2: Modyfikowanie plików definicji i konfiguracji usługi hello
Aplikacja musi być skonfigurowany toouse hello certyfikatu, a punkt końcowy HTTPS muszą zostać dodane. W związku z tym hello definicji usługi i pliki konfiguracji usługi wymagają toobe aktualizacji.

1. W środowisku projektowania, otwórz plik definicji hello usługi (CSDEF), Dodaj **certyfikaty** sekcji w hello **sieć Web** sekcji, a obejmują hello następujących informacji certyfikat (i certyfikaty pośrednie):

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   Witaj **certyfikaty** sekcja definiuje nazwę hello naszych certyfikatu, jego lokalizację i nazwę hello magazynu hello, w którym znajduje się.

   Uprawnienia (`permisionLevel` atrybutów) mogą być tooone zestawu z hello następujące wartości:

   | Wartość uprawnienia | Opis |
   | --- | --- |
   | limitedOrElevated |**(Ustawienie domyślne)**  Wszystkie procesy roli można uzyskać dostępu do klucza prywatnego hello. |
   | z podwyższonym poziomem uprawnień |Tylko procesów z podwyższonym poziomem uprawnień można uzyskać dostępu do klucza prywatnego hello. |

2. W pliku definicji usługi, dodać **InputEndpoint** elementu w obrębie hello **punkty końcowe** sekcji tooenable HTTPS:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. W pliku definicji usługi, dodać **powiązanie** elementu w obrębie hello **witryny** sekcji. Ten element dodaje toomap powiązanie HTTPS lokacji tooyour punktu końcowego:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   Zostały ukończone wszystkie pliku definicji usługi toohello hello wymagane zmiany; jednak nadal potrzebujesz informacji o certyfikacie hello tooadd do pliku konfiguracji usługi hello.
4. W pliku konfiguracji usługi (CSCFG), ServiceConfiguration.Cloud.cscfg, Dodaj **certyfikaty** wartości z tego certyfikatu. Witaj Poniższy przykładowy kod zawiera szczegółowe informacje o hello **certyfikaty** części, z wyjątkiem hello wartość odcisku palca.

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

(W tym przykładzie użyto **sha1** hello odcisku palca algorytmu. Określ hello odpowiednią wartość dla algorytmu odcisk palca certyfikatu).

Teraz, gdy hello definicji i usługa plików konfiguracyjnych usługi zostały zaktualizowane, pakiet wdrożenia do przekazywania tooAzure. Jeśli używasz **cspack**, nie używaj **/generateConfigurationFile** Flaga, jako który zastąpi wstawione informacje o certyfikacie.

## <a name="step-3-upload-a-certificate"></a>Krok 3: Przekaż certyfikat
Połącz toohello portalu Azure i...

1. W hello **wszystkie zasoby** sekcji hello portalu, wybierz usługi w chmurze.

    ![Publikowanie usługi w chmurze](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. Kliknij przycisk **certyfikaty**.

    ![Kliknij ikonę certyfikaty hello](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. Kliknij przycisk **przekazać** u góry hello obszaru certyfikaty hello.

    ![Kliknij element menu hello przekazywania](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. Podaj hello **pliku**, **hasło**, następnie kliknij przycisk **przekazać** u dołu hello obszar wprowadzania danych hello.

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Krok 4: Łączenie toohello wystąpienia roli przy użyciu protokołu HTTPS
Teraz, wdrożenie jest uruchomiona na platformie Azure, możesz połączyć tooit przy użyciu protokołu HTTPS.

1. Kliknij przycisk hello **adres URL witryny** tooopen hello przeglądarkę sieci web.

   ![Kliknij przycisk hello adres URL witryny](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. W przeglądarce sieci web, należy zmodyfikować hello łącze toouse **https** zamiast **http**, a następnie odwiedź stronę hello.

   > [!NOTE]
   > Jeśli używasz certyfikatu z podpisem własnym, podczas przeglądania tooan punkt końcowy HTTPS skojarzoną z certyfikatu z podpisem własnym hello mogą pojawić się w przeglądarce hello błąd certyfikatu. Przy użyciu certyfikatu podpisanego przez zaufany urząd certyfikacji eliminuje ten problem. w hello międzyczasie, możesz zignorować błąd hello. (Inną możliwością jest tooadd hello certyfikatu z podpisem własnym toohello certyfikat zaufanego urzędu magazynu certyfikatów użytkownika).
   >
   >

   ![Wersja zapoznawcza witryny](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > Jeśli chcesz toouse SSL przemieszczania wdrożenia zamiast wdrożenia produkcyjnego, najpierw należy toodetermine hello adres URL dla hello przemieszczania wdrożenia. Po wdrożeniu usługi w chmurze toohello adres URL hello środowiska przemieszczania jest określany przez hello **identyfikator wdrożenia** identyfikator GUID w następującym formacie:`https://deployment-id.cloudapp.net/`  
   >
   > Utwórz certyfikat z hello typowych nazwa (CN) równy toohello oparta na identyfikatorze GUID adresem URL (na przykład **328187776e774ceda8fc57609d404462.cloudapp.net**). Użyj hello portalu tooadd hello certyfikatu tooyour przemieszczane usługi w chmurze. Dodawaniu hello informacji tooyour CSDEF i CSCFG pliki certyfikatów, Spakuj ponownie aplikację i zaktualizować wdrożenia etapowego toouse hello nowego pakietu.
   >

## <a name="next-steps"></a>Następne kroki
* [Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).
* Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).
* Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).
* [Usługi w chmurze zarządzanie](cloud-services-how-to-manage-portal.md).
