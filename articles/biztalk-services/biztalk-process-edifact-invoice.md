---
title: "Samouczek: Przetworzyć EDIFACT faktury za pomocą usług Azure BizTalk | Dokumentacja firmy Microsoft"
description: "Jak toocreate i konfigurowanie aplikacji hello łącznik pole lub interfejsu API i używać go w aplikacji logiki w usłudze Azure App Service"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>Samouczek: Proces EDIFACT faktury za pomocą usługi Azure BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Można używać hello tooconfigure Portal usługi BizTalk i wdróż X12 i EDIFACT umowy. W tym samouczku opisano, jak toocreate umowy EDIFACT wymiany faktury między partnerami handlowymi. Ten samouczek jest przeznaczony wokół obejmujące dwoma partnerami handlowymi Northwind i Contoso, które wymiany wiadomości EDIFACT firm end-to-end.  

## <a name="sample-based-on-this-tutorial"></a>Przykładowe na podstawie w tym samouczku
Ten samouczek jest przeznaczony wokół próbki **wysyłania EDIFACT faktury za pomocą usługi BizTalk Services**, który jest dostępny toodownload z hello [galerii kodu MSDN](http://go.microsoft.com/fwlink/?LinkId=401005). Można użyć przykładu hello i przejść przez ten samouczek toounderstand jak próbki hello został skompilowany. Można użyć tego samouczka toocreate własnych rozwiązań podstaw. W tym samouczku jest przeznaczona do drugiej metody hello tak, aby zrozumieć, jak to rozwiązanie został skompilowany. Również jak to możliwe, samouczek hello są zgodne z przykładowych hello i używa hello tych samych nazw artefaktów (na przykład, schematów, przekształceń), które jest używane w przykładowym hello.  

> [!NOTE]
> Ponieważ to rozwiązanie polega na wysyłanie wiadomości z EAI Mostek tooan EDI mostka, ponownie używa hello [Mostek usługi BizTalk łańcucha próbki](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) próbki.  
> 
> 

## <a name="what-does-hello-solution-do"></a>Do czego służy hello rozwiązania?
W tym rozwiązaniu Northwind odbiera faktury EDIFACT z firmy Contoso. Te faktury nie znajdują się w standardowym formacie EDI. Tak przed wysłaniem hello tooNorthwind faktury, musi ona być przekształcone tooan EDIFACT faktury (nazywanych również ZALICZKOWĄ) dokumentu. Po otrzymaniu Northwind musi przetworzyć hello EDIFACT faktury i zwracać tooContoso wiadomości (nazywanych również CONTRL) formantu.

![][1]  

tooachieve tego scenariusza biznesowego, firma Contoso używa hello funkcji udostępnionych w usługi BizTalk platformy Microsoft Azure.

* Firma Contoso używa EAI mostków tootransform hello oryginalnej faktury tooEDIFACT ZALICZKOWĄ.
* Mostek EAI Hello wysyła następnie tooan wiadomość hello EDI wysyłania Mostek wdrożone w ramach umowy skonfigurowane w hello Portal usługi BizTalk.
* Mostek wysyłania EDI Hello przetwarza hello ZALICZKOWĄ EDIFACT i kieruje je tooNorthwind.
* Po otrzymaniu hello faktury, Northwind zwraca CONTRL toohello wiadomości, EDI odbierania Mostek wdrożenia w ramach umowy hello.  

> [!NOTE]
> Opcjonalnie to rozwiązanie również pokazano, jak przetwarzanie wsadowe toosend hello toouse faktur w partii, zamiast wysyłać każdej faktury oddzielnie.  
> 
> 

Scenariusz hello toocomplete, korzystamy z kolejek usługi Service Bus toosend Faktura z firmy Contoso tooNorthwind lub odebranie potwierdzenia z Northwind. Te kolejki mogą być tworzone za pomocą aplikacji klienckiej, która jest dostępna do pobrania i znajduje się w hello przykładowy pakiet, który jest dostępny w ramach tego samouczka.  

## <a name="prerequisites"></a>Wymagania wstępne
* Musi mieć nazw usługi Service Bus. Aby uzyskać instrukcje dotyczące tworzenia przestrzeni nazw, zobacz [jak: utworzyć lub zmodyfikować Namespace usługi magistrali usługi](https://msdn.microsoft.com/library/azure/hh674478.aspx). Załóżmy już przestrzeń nazw magistrali usług alokacji o nazwie **edifactbts**.
* Musisz mieć subskrypcję usługi BizTalk Services. Aby uzyskać instrukcje, zobacz [Utwórz usługę BizTalk przy użyciu klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=302280). W tym samouczku, poinformuj nas założono, że masz subskrypcję usługi BizTalk Services o nazwie **contosowabs**.
* Zarejestruj subskrypcję usługi BizTalk Services na powitania Portal usługi BizTalk. Aby uzyskać instrukcje, zobacz [rejestrowanie wdrożenia usługi BizTalk na powitania Portal usługi BizTalk](https://msdn.microsoft.com/library/hh689837.aspx)
* Musi mieć zainstalowanego programu Visual Studio.
* Musisz mieć zainstalowany zestaw SDK usług BizTalk. Możesz pobrać hello SDK [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>Krok 1: Tworzenie hello kolejek usługi Service Bus
To rozwiązanie wymaga wiadomości tooexchange kolejek usługi Service Bus między partnerami handlowymi. Contoso i Northwind wysyłania komunikatów kolejek toohello z którym hello EAI i/lub EDI mostków mogły ich używać. W tym rozwiązaniu są potrzebne trzy kolejek usługi Service Bus:

* **northwindreceive** — Northwind odebrał faktury hello z Contoso za pośrednictwem tej kolejki.
* **contosoreceive** — Contoso odebrał potwierdzenia hello z Northwind za pośrednictwem tej kolejki.
* **zawieszone** — wszystkie wstrzymane wiadomości są routingiem toothis kolejki. Komunikaty są wstrzymane w razie awarii podczas przetwarzania.

Te kolejki usługi Service Bus można utworzyć za pomocą aplikacji klienckiej zawarte w pakiecie próbki hello.  

1. Z hello której pobrano próbki hello, otwórz **samouczek wysyłania faktury za pomocą usług BizTalk — wersja usługi EDI Bridges.sln**.
2. Naciśnij klawisz **F5** toobuild i rozpocząć hello **klienta samouczek** aplikacji.
3. Na ekranie powitania wprowadź przestrzeń nazw usługi ACS magistrali hello, nazwa wystawcy i klucza wystawcy.
   
   ![][2]  
4. Okno komunikatu monituje o tym, że zostaną utworzone trzy kolejki w przestrzeni nazw magistrali usług. Kliknij przycisk **OK**.
5. Pozostaw powitania klienta samouczek uruchomiona. Otwórz hello, kliknij pozycję **usługi Service Bus** > ***przestrzeni nazw usługi Service Bus*** > **kolejek**i sprawdź, czy hello trzech kolejki są tworzone.  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>Krok 2: Tworzenie i wdrażanie umowy z partnerem handlowym
Tworzenie umowy z partnerem handlowym między Contoso i Northwind. Umowy z partnerem handlowym definiuje kontrakt handlu między hello dwóch partnerów biznesowych, takich jak które toouse schematu komunikat, który wiadomości protokołu toouse itp. Umowy z partnerem handlowym obejmuje dwa mostków EDI, co toosend wiadomości partnerów tootrading (o nazwie hello **wysyłania EDI Mostek**) i jeden tooreceive komunikaty z partnerami handlowymi (o nazwie hello **odbierania EDI Mostek**).

W kontekście hello tego rozwiązania hello EDI wysyłania Mostek odpowiada toohello wysyłania po stronie powitania umowy i jest używany toosend hello EDIFACT faktury z Contoso tooNorthwind. Podobnie, hello EDI odbierania Mostek odpowiada toohello po stronie odbierającej hello umowy i jest używane tooreceive potwierdzeń z Northwind.  

### <a name="create-hello-trading-partners"></a>Utwórz hello partnerami handlowymi
toostart, Utwórz partnerami handlowymi Contoso i Northwind.  

1. W hello Portal usługi BizTalk, na powitania **partnerów** , kliknij pozycję **Dodaj**.
2. W nowej strony hello partnera, wprowadź **Contoso** Nazwa partnera, a następnie kliknij przycisk **zapisać**.
3. Hello Powtórz krok toocreate hello drugiego partnera, **Northwind**.  

### <a name="create-hello-agreement"></a>Tworzenie umowy z hello
Umowy z partnerami handlowymi są tworzone profilom biznesowych z partnerami handlowymi. To rozwiązanie wymaga hello domyślne partnera profilów, które są automatycznie tworzone podczas utworzyliśmy hello partnerów.  

1. W portalu usługi BizTalk hello, kliknij przycisk **umowy** > **Dodaj**.
2. Witaj nowe umowy **ustawienia ogólne** , określ wartości hello, jak pokazano w poniższym obrazie hello, a następnie kliknij przycisk **Kontynuuj**.
   
   ![][3]  
   
   Po kliknięciu **Kontynuuj**, dwie karty, **ustawienia odbierania** i **ustawienia wysyłania** staną się dostępne.
3. Tworzenie umowy wysyłania hello między Contoso i Northwind. Niniejsza Umowa decyduje o tym, jak Contoso wysyła hello EDIFACT faktury tooNorthwind.
   
   1. Kliknij przycisk **ustawień wysyłania**.
   2. Zachowaj wartości domyślne hello na powitania **adres URL komunikatów przychodzących**, **przekształcenie**, i **wsadowe** karty.
   3. Na powitania **protokołu** kartę, w obszarze hello **schematy** sekcji, Przekaż hello **EFACT_D93A_INVOIC.xsd** schematu. Ten schemat jest dostępna z pakietem próbki hello.
      
      ![][4]  
   4. Na powitania **transportu** karcie, określ szczegóły hello hello kolejek usługi Service Bus. Powitania po stronie wysyłania umowy, używamy hello **northwindreceive** kolejka toosend hello EDIFACT faktury tooNorthwind i hello **zawieszone** kolejka tooroute komunikaty, które nie są podczas przetwarzania i są zawieszone. Utworzono te kolejki w **krok 1: tworzenie kolejek usługi Service Bus hello** (w tym temacie).
      
      ![][5]  
      
      W obszarze **ustawienia transportu > Typ transportu** i **ustawienia zawieszenia wiadomości > Typ transportu**, wybierz usługi Azure Service Bus i podaj wartości hello, jak pokazano w obrazie hello.
4. Utwórz hello odbierania Umowę między Contoso i Northwind. Niniejsza Umowa decyduje o tym, jak Contoso odbiera potwierdzenia hello z Northwind.
   
   1. Kliknij przycisk **odbierają ustawienia**.
   2. Zachowaj wartości domyślne hello na powitania **transportu** i **przekształcenie** karty.
   3. Na powitania **protokołu** kartę, w obszarze hello **schematy** sekcji, Przekaż hello **EFACT_4.1_CONTRL.xsd** schematu. Ten schemat jest dostępna z pakietem próbki hello.
   4. Na powitania **trasy** karcie, Utwórz tooensure filtr który tylko potwierdzeń z Northwind tooContoso routingiem. W obszarze **ustawienia trasy**, kliknij przycisk **Dodaj** toocreate hello filtr routingu.
      
      ![][6]  
      
      1. Podaj wartości dla **Nazwa reguły**, **reguły trasy**, i **docelowy trasy** pokazane na powitania obrazu.
      2. Kliknij pozycję **Zapisz**.
   5. Na powitania **trasy** ponownie karcie, określ, gdzie potwierdzeń zawieszone (potwierdzeń, które nie są podczas przetwarzania) są kierowane do. Ustaw hello transportu typu tooAzure usługi Service Bus, zbyt route typ docelowy**kolejki**, uwierzytelnianie typu zbyt**sygnatura dostępu współdzielonego** (SAS), podaj parametry połączenia SAS hello hello usługi Service Bus przestrzeń nazw, a następnie wprowadź nazwę kolejki hello jako **zawieszone**.
5. Na koniec kliknij **Wdróż** toodeploy hello umowy. Punkty końcowe hello Uwaga gdzie hello wysyłania i odbierania umów wdrożony.
   
   * Na powitania **ustawienia wysyłania** , w obszarze **adres URL komunikatów przychodzących**, należy zwrócić uwagę hello punktu końcowego. toosend komunikat z tooNorthwind Contoso za pomocą hello EDI wysyłania mostek, możesz wysłać końcowy toothis komunikatu.
   * Na powitania **ustawienia odbierania** , w obszarze **transportu**, należy zwrócić uwagę hello punktu końcowego. toosend komunikat z tooContoso Northwind przy użyciu hello EDI otrzymywać mostek, musisz wysłać końcowy toothis komunikatu.  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>Krok 3: Tworzenie i wdrażanie hello projektu usługi BizTalk Services
W poprzednim kroku hello wdrożono hello EDI wysyłania i odbierania umów tooprocess EDIFACT faktury i potwierdzeń. Umowy te mogą tylko przetwarzania komunikatów o zgodnych ze standardami toohello standardowe EDIFACT komunikat schematu. Jednak na powitania scenariuszu dla tego rozwiązania firmy Contoso wysyła tooNorthwind faktury w schemacie zastrzeżonych wewnętrznych. Tak zanim toohello EDI wysyłania mostek jest wysyłana wiadomość hello, musi zostać przekształcone z hello wewnętrznych schematu toohello standardowe EDIFACT faktury schematu. Projekt BizTalk EAI usług Hello robi to.

projekt usługi BizTalk Services Hello, **InvoiceProcessingBridge**, że transformacje hello wiadomości jest również uwzględniony próbki hello został pobrany. Projekt Hello zawiera następujące artefakty hello:

* **INHOUSEINVOICE. XSD** — schematu hello faktury wewnętrznych wysyłany tooNorthwind.
* **EFACT_D93A_INVOIC. XSD** — schematu hello standardowe EDIFACT faktury.
* **EFACT_4.1_CONTRL. XSD** — schematu hello EDIFACT potwierdzenia, że Northwind wysyła tooContoso.
* **INHOUSEINVOICE_to_D93AINVOIC. TRFM** — Witaj przekształcenia mapujący hello wewnętrznych faktury schematu toohello standardowe EDIFACT faktury schematu.  

### <a name="create-hello-biztalk-services-project"></a>Tworzenie projektu usługi BizTalk Services hello
1. W hello rozwiązania Visual Studio rozwiń hello InvoiceProcessingBridge projektu, a następnie otwórz hello **MessageFlowItinerary.bcs** pliku.
2. Kliknij w dowolnym miejscu na kanwie hello i ustaw hello **adres URL usługi BizTalk** w hello toospecify pole właściwości nazwę subskrypcji usługi BizTalk Services. Na przykład `https://contosowabs.biztalk.windows.net`.
   
   ![][7]  
3. Przeciągnij z przybornika hello **Mostek One-Way Xml** toohello kanwy. Zestaw hello **nazwa jednostki** i **adres względny** właściwości hello zestawiania zbyt**ProcessInvoiceBridge**. Kliknij dwukrotnie **ProcessInvoiceBridge** tooopen hello Mostek konfiguracji powierzchni.
4. W ramach hello **typów komunikatów** , kliknij przycisk hello plus (**+**) przycisk toospecify hello schematu hello wiadomości przychodzącej. Ponieważ hello komunikat przychodzący dla hello Mostek EAI jest zawsze hello wewnętrznych faktury, ustaw tę wartość za**INHOUSEINVOICE**.
   
   ![][8]  
5. Kliknij przycisk hello **transformacji Xml** kształtu i w polu właściwości hello na powitania **mapy** właściwości, kliknij przycisk wielokropka hello (**...** ) przycisku. W hello **wybór mapy** okno dialogowe, wybierz opcję hello **INHOUSEINVOICE_to_D93AINVOIC** Przekształć plik, a następnie kliknij przycisk **OK**.
   
   ![][9]  
6. Wróć za**MessageFlowItinerary.bcs**i przeciągnij z przybornika hello **dwustronny zewnętrznego punktu końcowego usługi** toohello rogu hello **ProcessInvoiceBridge**. Ustaw jego **nazwa jednostki** właściwości zbyt**EDIBridge**.
7. W Eksploratorze rozwiązań hello, rozwiń węzeł hello **MessageFlowItinerary.bcs** i kliknij dwukrotnie hello **EDIBridge.config** pliku. Zamień zawartość hello hello **EDIBridge.config** następujący hello.
   
   > [!NOTE]
   > Dlaczego potrzebujesz pliku .config hello tooedit? Hello zewnętrznego punktu końcowego czy dodaliśmy kanwy projektanta Mostek toohello reprezentuje mostki EDI hello wdrożyliśmy wcześniej. Mostków EDI są mostków dwukierunkowe, z send i skalowanie po stronie. Jednak hello Mostek EAI, że dodaliśmy toohello Mostek projektanta jest mostek jednokierunkowe. Tak exchange inny komunikat wzorce toohandle hello mostków dwóch hello używamy zachowanie niestandardowych Mostek przez dołączenie jego konfigurację do pliku .config hello. Ponadto zachowania niestandardowego hello również obsługę uwierzytelniania hello toohello wysyłania EDI Mostek punktu końcowego. To zachowanie niestandardowych jest dostępna jako osobne próbki w [Mostek usługi BizTalk łańcucha próbki - EAI tooEDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104). To rozwiązanie hello próbki są ponownie używane.  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. Aktualizuj szczegóły konfiguracji tooinclude hello EDIBridge.config pliku
   
   * W obszarze  *<behaviors>* , podaj hello ACS przestrzeni nazw i klucz skojarzony z hello subskrypcji usługi BizTalk Services.
   * W obszarze  *<client>* , podaj punkt końcowy hello wdrożonym hello EDI Wyślij umowę.
   
   Zapisz zmiany i zamknij plik konfiguracji hello.
9. Z przybornika hello, kliknij przycisk hello **łącznik** i hello sprzężenia **ProcessInvoiceBridge** i **EDIBridge** składników. Wybierz łącznik hello, a w polu właściwości należy ustawić **warunek filtru** za**dopasowanie wszystkich**. Dzięki temu, że wszystkie komunikaty przetwarzane przez mostek EAI hello są kierowane Mostek EDI toohello.
   
   ![][10]  
10. Zapisz zmiany toohello rozwiązanie.  

### <a name="deploy-hello-project"></a>Wdrażanie projektu hello
1. Na komputerze hello, w której utworzono projekt usługi BizTalk Services hello Pobierz i zainstaluj certyfikat SSL powitania dla Twojej subskrypcji usługi BizTalk Services. W obszarze usługi BizTalk Services kliknij **pulpitu nawigacyjnego**, a następnie kliknij przycisk **Pobierz certyfikat SSL**. Kliknij dwukrotnie certyfikat hello i wykonaj hello monitu toocomplete hello instalacji. Upewnij się, że konieczne jest zainstalowanie certyfikatu hello w obszarze **zaufane główne urzędy certyfikacji** magazynu certyfikatów.
2. W Eksploratorze rozwiązań programu Visual Studio, kliknij prawym przyciskiem myszy hello **InvoiceProcessingBridge** projektu, a następnie kliknij przycisk **Wdróż**.
3. Podaj wartości hello, jak pokazano w obrazie hello, a następnie kliknij przycisk **Wdróż**. Możesz też uzyskać poświadczenia hello ACS usługi BizTalk, klikając **informacje o połączeniu** z pulpitu nawigacyjnego usługi BizTalk Services hello.
   
   ![][11]  
   
   W okienku danych wyjściowych hello, skopiuj punktu końcowego hello hello Mostek EAI wdrożonym, na przykład `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`. Ten adres URL punktu końcowego będą potrzebne później.  

## <a name="step-4-test-hello-solution"></a>Krok 4: Testowanie hello rozwiązania
W tym temacie opisano, jak tootest hello rozwiązania przy użyciu hello **klienta samouczek** aplikacji w ramach przykładu hello.  

1. W programie Visual Studio, naciśnij klawisz F5 toostart hello **klienta samouczek**.
2. ekranie powitania muszą znajdować się wartości hello wstępnie z kroku hello gdzie utworzyliśmy hello kolejek usługi Service Bus. Kliknij przycisk **Dalej**.
3. W następnym oknie hello, podaj poświadczenia ACS dla subskrypcji usługi BizTalk Services, a hello punkty końcowe gdzie EAI i EDI (odbierać) mostków są wdrażane.
   
   Punkt końcowy Mostek EAI hello skopiowany w poprzednim kroku hello. Dla EDI otrzymywać Mostek punktu końcowego, w portalu usługi BizTalk hello, przejdź umowy toohello > Ustawienia odbierania > transportu > punktu końcowego.
   
   ![][12]  
4. W następnym oknie hello, w obszarze Contoso, kliknij przycisk hello **Wyślij fakturę wewnętrznych** przycisku. Otwórz okno dialogowe hello pliku, otwórz plik INHOUSEINVOICE.txt hello. Sprawdź zawartość hello hello pliku, a następnie kliknij przycisk **OK** toosend hello faktury.
   
   ![][13]  
5. W kilka sekund hello faktury odebraniu Northwind. Kliknij przycisk hello **komunikat widoku** faktury hello toosee łącze otrzymane przez Northwind. Powiadomienia, jak hello faktury otrzymanej przez Northwind znajduje się w standardowe schematu EDIFACT podczas hello jedną wysyłane przez firmę Contoso został wewnętrznych schematu.
   
   ![][14]  
6. Wybierz hello faktury, a następnie kliknij przycisk **potwierdzenia wysyłania**. Okno dialogowe hello wyskakującej Zwróć uwagę wymiany hello, ten identyfikator jest taka sama we hello odebrane faktury i hello potwierdzenia wysyłania. Kliknij przycisk OK w hello **potwierdzenia wysyłania** okno dialogowe.
   
   ![][15]  
7. W ciągu kilku sekund potwierdzenia hello została odebrana pomyślnie w firmie Contoso.
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>Krok 5 (opcjonalny): faktury wysyłania EDIFACT w partiach
Mostków EDI usługi BizTalk obsługuje również tworzenie partii komunikatów wychodzących. Ta funkcja jest przydatna do odbierania partnerów, których preferowane tooreceive partii wiadomości (spełniające określone kryterium) zamiast poszczególnych wiadomości.

Hello najważniejszym aspektem podczas pracy z partii jest wersja rzeczywista hello partii hello, nazywane również hello wersji kryteria. kryteria wersji Hello może bazować na sposób odbierania partnera hello chce tooreceive wiadomości. Tworzenie plików wsadowych jest włączona, hello Mostek EDI nie wysyła hello wychodzących wiadomości toohello odbieranie partnera, dopóki hello wersji kryteria są spełnione. Na przykład, przetwarzanie wsadowe kryteria na podstawie komunikatów wysyła rozmiar partii tylko wtedy, gdy "n" wiadomości są przetwarzane wsadowo. Kryteria partii można też na podstawie czasu taki sposób, że plik wsadowy jest wysyłany o stałej godzinie każdego dnia. W tym rozwiązaniu spróbujemy hello rozmiar wiadomości na podstawie kryteriów.

1. W portalu usługi BizTalk hello kliknij przycisk umowy hello, utworzony wcześniej. Kliknij przycisk Wyślij Ustawienia > Przetwarzanie wsadowe > Dodaj partii.
2. Wprowadź nazwę usługi partia zadań **InvoiceBatch**, podaj opis, a następnie kliknij przycisk **dalej**.
3. Określ kryteria partii, które definiuje, które wiadomości musi można umieścić w partii. W tym rozwiązaniu możemy partii wszystkie komunikaty. Tak, wybierz hello zaawansowane definicje opcję i wprowadź **1 = 1**. To jest warunek, który będzie zawsze równa true, i dlatego wszystkie komunikaty będzie można umieścić w partii. Kliknij przycisk **Dalej**.
   
   ![][17]  
4. Określ kryteria wersji partii. Wybierz z listy pole hello, **MessageCountBased**oraz **liczba**, określ **3**. Oznacza to, że trzy komunikaty zbiorczo zostanie wysłany tooNorthwind. Kliknij przycisk **Dalej**.
   
   ![][18]  
5. Przejrzyj podsumowanie hello, a następnie kliknij przycisk **zapisać**. Kliknij przycisk **Wdróż** tooredeploy hello umowy.
6. Przejdź wstecz toohello **klienta samouczek**, kliknij przycisk **Wyślij fakturę wewnętrznych**i wykonaj hello monity toosend hello faktury. Można zauważyć, że w firmie Northwind nieodebrania nie faktury, ponieważ rozmiar partii hello nie są spełnione. Powtórz ten krok dwa razy, tak aby było możliwe tooNorthwind wysyłane wiadomości faktury. Spełnia on hello partii kryteria wersji 3 wiadomości i powinien zostać wyświetlony w firmie Northwind faktury.

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

