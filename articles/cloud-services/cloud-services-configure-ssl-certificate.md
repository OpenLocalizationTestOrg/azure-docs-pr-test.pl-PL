---
title: "aaaConfigure protokołu SSL dla usługi w chmurze (klasyczne) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toospecify punkt końcowy HTTPS dla roli sieci web i jak tooupload SSL certyfikatów toosecure aplikacji."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
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
> 

Metoda zabezpieczania danych przesyłanych między hello hello najczęściej używane jest szyfrowanie Secure Socket Layer (SSL) internet. To zadanie typowe omówiono sposób toospecify punkt końcowy HTTPS dla roli sieci web i jak tooupload SSL certyfikatów toosecure aplikacji.

> [!NOTE]
> Usługi w chmurze tooAzure; Zastosuj Hello procedur w tym zadaniu dla usług aplikacji, zobacz [to](../app-service-web/web-sites-configure-ssl-certificate.md) artykułu.
> 
> 

To zadanie używa wdrożenia produkcyjnego. Informacji na temat używania tymczasowej wdrożenia znajduje się na powitania na końcu tego tematu.

Odczyt [to](cloud-services-how-to-create-deploy.md) najpierw artykułu, jeśli nie utworzono jeszcze usługi w chmurze.

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

3. W pliku definicji usługi, dodać **powiązanie** elementu w obrębie hello **witryny** sekcji. W tej sekcji dodaje toomap powiązanie HTTPS lokacji tooyour punktu końcowego:
   
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
   
   Wszystkie pliku definicji usługi toohello hello wymagane zmiany zostały ukończone, ale nadal potrzebujesz informacji o certyfikacie hello tooadd do pliku konfiguracji usługi hello.
4. W pliku konfiguracji usługi (CSCFG), ServiceConfiguration.Cloud.cscfg, Dodaj **certyfikaty** sekcji w hello **roli** sekcji, zastępując hello wartość odcisku palca dla przykładowych pokazano poniżej z który certyfikatu:
   
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

(hello poprzedzających przykładzie użyto **sha1** hello odcisku palca algorytmu. Określ hello odpowiednią wartość dla algorytmu odcisk palca certyfikatu).

Teraz, gdy hello definicji i usługa plików konfiguracyjnych usługi zostały zaktualizowane, pakiet wdrożenia do przekazywania tooAzure. Jeśli używasz **cspack**, nie używaj **/generateConfigurationFile** Flaga, jako który zastępuje wstawiono informacji o certyfikacie.

## <a name="step-3-upload-a-certificate"></a>Krok 3: Przekaż certyfikat
Pakiet wdrażania zostało zaktualizowane toouse hello certyfikatu, i dodano punkt końcowy HTTPS. Możesz teraz przekazać tooAzure certyfikatów i pakietów hello z hello klasycznego portalu Azure.

1. Zaloguj się za toohello [klasycznego portalu Azure][Azure classic portal]. 
2. Kliknij przycisk **usługi w chmurze** w okienku nawigacji po lewej stronie powitania.
3. Kliknij pozycję usługi w chmurze hello potrzebne.
4. Kliknij przycisk hello **certyfikaty** kartę.
   
    ![Kliknij kartę certyfikaty hello](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. Kliknij przycisk hello **przekazać** przycisku.
   
    ![Upload](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. Podaj hello **pliku**, **hasło**, następnie kliknij przycisk **Complete** (hello znacznikiem wyboru).

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Krok 4: Łączenie toohello wystąpienia roli przy użyciu protokołu HTTPS
Teraz, wdrożenie jest uruchomiona na platformie Azure, możesz połączyć tooit przy użyciu protokołu HTTPS.

1. W hello klasycznego portalu Azure, wybierz wdrożenie, a następnie kliknij łącze hello w obszarze **adres URL witryny**.
   
   ![Określić adres URL witryny][2]
2. W przeglądarce sieci web, należy zmodyfikować hello łącze toouse **https** zamiast **http**, a następnie odwiedź stronę hello.
   
   > [!NOTE]
   > Jeśli używasz certyfikatu z podpisem własnym, podczas przeglądania tooan punkt końcowy HTTPS skojarzoną z certyfikatu z podpisem własnym hello mogą pojawić się w przeglądarce hello błąd certyfikatu. Przy użyciu certyfikatu podpisanego przez zaufany urząd certyfikacji eliminuje ten problem. w hello międzyczasie, możesz zignorować błąd hello. (Inną możliwością jest tooadd hello certyfikatu z podpisem własnym toohello certyfikat zaufanego urzędu magazynu certyfikatów użytkownika).
   > 
   > 
   
   ![Przykład witryny sieci web protokołu SSL][3]

Jeśli chcesz toouse SSL przemieszczania wdrożenia zamiast wdrożenia produkcyjnego, należy najpierw toodetermine hello adres URL dla hello przemieszczania wdrożenia. Wdrażanie usługi toohello przemieszczania środowiska chmury bez uwzględniania certyfikatu lub żadnych informacji o certyfikacie. Po wdrożeniu, można określić adresu hello URL na podstawie identyfikatora GUID, który znajduje się na powitania klasycznego portalu Azure **adres URL witryny** pola. Utwórz certyfikat z hello typowych nazwa (CN) równy toohello oparta na identyfikatorze GUID adresem URL (na przykład **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**). Użyj hello Azure classic portal tooadd hello certyfikatu tooyour przemieszczane usługi w chmurze. Dodawaniu hello informacji tooyour CSDEF i CSCFG pliki certyfikatów, Spakuj ponownie aplikację i zaktualizować wdrożenia etapowego toouse hello nowego pakietu.

## <a name="next-steps"></a>Następne kroki
* [Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure.md).
* Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md).
* Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name.md).
* [Usługi w chmurze zarządzanie](cloud-services-how-to-manage.md).

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
