---
title: "aaaHigh dostępności geograficznej między AD FS wdrożenia na platformie Azure z usługą Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym dokumencie przedstawiono sposób toodeploy usług AD FS w systemie Azure dla o wysokiej dostępności."
keywords: "Usługi AD fs z usługi Azure traffic manager, usługi AD FS z usługi Azure Traffic Manager, geograficzne, wielu centrów danych, geograficzny centrów danych, wielu geograficzny centrów danych, wdrażanie usług AD FS w systemie azure, wdrażania usług AD FS azure, azure AD FS i usługi azure ad fs, wdrażania usług AD FS, wdrażanie usług ad fs usługi AD FS w systemie azure, Wdrażanie usług AD FS w systemie azure, wdrażanie usług AD FS w azure, azure AD FS, wprowadzenie tooAD FS, Azure, usługi AD FS w systemie Azure iaas, usługi AD FS, Przenieś tooazure usług AD FS"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Wdrażanie geograficznie rozproszonych usług AD FS o wysokiej dostępności na platformie Azure przy użyciu usługi Azure Traffic Manager
[Wdrażanie usług AD FS w systemie Azure](active-directory-aadconnect-azure-adfs.md) zawiera wskazówki krok po kroku jako toohow można wdrożyć prosty infrastruktury usług AD FS w organizacji na platformie Azure. W tym artykule przedstawiono kolejne kroki hello toocreate cross geograficznego wdrażania usług AD FS za pomocą usługi Azure [usługi Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). Usługi Azure Traffic Manager ułatwia tworzenie geograficznie rozpowszechniania wysokiej dostępności i wysokiej wydajności infrastruktury usług AD FS w organizacji przez użycie zakresu metod routingu różnych dostępnych toosuit wymaga od hello infrastruktury.

Geograficznie rozproszona infrastruktura usług AD FS o wysokiej dostępności umożliwia wykonywanie następujących czynności:

* **Eliminacja pojedynczego punktu awarii:** z możliwości trybu failover z usługi Azure Traffic Manager, można osiągnąć wysokiej dostępności infrastruktury usług AD FS, nawet w przypadku awarii jednego z centrów danych hello w części Witaj świecie
* **Większa wydajność:** można użyć hello sugerowane wdrożenia w tym artykule tooprovide infrastruktury usług AD FS wysokiej wydajności, które mogą ułatwić użytkownikom szybciej uwierzytelniania. 

## <a name="design-principles"></a>Zasady projektowania
![Ogólny projekt](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

zasady projektowania podstawowe Hello będzie taka sama, jak wymienionych w zasadach projektowania w artykule hello wdrożenia usług AD FS w systemie Azure. diagram Hello powyżej pokazuje rozszerzenie prostego powitania regionu geograficznego tooanother podstawowego wdrożenia. Poniżej przedstawiono niektóre tooconsider punktów podczas rozszerzania regionu geograficznego toonew wdrożenia

* **Sieć wirtualna:** należy utworzyć nową sieć wirtualną w regionie geograficznym hello ma toodeploy dodatkowe AD FS infrastruktury. W powyższym diagramie hello jest wyświetlana Geo1 sieci Wirtualnej i sieci Wirtualnej Geo2 jako Witaj dwie sieci wirtualne w każdym regionie geograficznym.
* **Kontrolery domeny i serwery usług AD FS w nowej sieci Wirtualnej geograficzne:** zalecane jest toodeploy kontrolerów domeny w nowej regionu geograficznego hello tak, aby serwery usług AD FS hello w regionie nowe hello nie mają toocontact kontrolera domeny w innym zakresie usunięta w ramach optymalizacji sieci toocomplete uwierzytelniania i tym samym poprawę wydajności hello.
* **Konta magazynu:** Konta magazynu są skojarzone z regionem. Ponieważ wdrażania maszyn w nowych regionu geograficznego, konieczne będzie toocreate toobe używany w regionie hello nowego konta magazynu.  
* **Grupy zabezpieczeń sieci:** Ponieważ są one kontami magazynu, grup zabezpieczeń sieci utworzonych w danym regionie nie można używać w innym regionie geograficznym. W związku z tym należy toocreate nowej sieci zabezpieczeń grupy podobne toothose w regionie geograficznym pierwszy hello INT i strefą DMZ podsieci w regionie geograficznym nowe hello.
* **Etykiety DNS dla publicznych adresów IP:** usługi Azure Traffic Manager można znaleźć tooendpoints tylko za pomocą etykiety DNS. W związku z tym jest wymagana toocreate etykiety DNS dla publicznych adresów IP hello zewnętrznej usługi równoważenia obciążenia.
* **Menedżer ruchu Azure:** Menedżera ruchu Microsoft Azure umożliwia rozpowszechnianie hello toocontrol użytkownika ruchu tooyour punktów końcowych usługi uruchomione w różnych centrach danych wokół hello world. Menedżer ruchu Azure działa na powitania poziom DNS. Używa ona DNS odpowiedzi toodirect użytkownika końcowego ruchu rozproszonych tooglobally punktów końcowych. Następnie łączyć klienci punkty końcowe toothose bezpośrednio. Przy użyciu różnych opcji routingu wydajności, ważone i priorytet można łatwo wybrać opcję routingu hello najlepiej dostosowane do potrzeb organizacji. 
* **V net tooV net łączność między dwóch regionach:** nie ma potrzeby toohave łączności między sieciami wirtualnymi hello samej siebie. Ponieważ każdej sieci wirtualnej ma dostęp do kontrolerów toodomain oraz serwera usług AD FS i WAP w sobie, mogą one działać bez żadnych połączenia między sieciami wirtualnymi hello w różnych regionach. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>Kroki toointegrate usługi Azure Traffic Manager
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>Wdrażanie usług AD FS w regionie geograficznym nowe hello
Wykonaj kroki hello i wskazówkami w [wdrożenia usług AD FS w systemie Azure](active-directory-aadconnect-azure-adfs.md) toodeploy hello samej topologii w regionie geograficznym nowe hello.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>Etykiety DNS dla publicznych adresów IP hello ukierunkowane Internet równoważenia obciążenia (publiczne)
Jak wspomniano powyżej, hello Azure Traffic Manager można odwoływać się tylko tooDNS etykiety jako punktów końcowych i dlatego jest ważne toocreate etykiety DNS dla publicznych adresów IP hello zewnętrznej usługi równoważenia obciążenia. Poniżej zrzut ekranu pokazuje, jak można skonfigurować etykiety DNS dla publicznego adresu IP hello. 

![Etykieta DNS](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Wdrażanie usługi Azure Traffic Manager
Wykonaj kroki hello poniżej toocreate profilu Menedżera ruchu. Aby uzyskać więcej informacji, można także skorzystać zbyt[Zarządzanie profilem usługi Azure Traffic Manager](../traffic-manager/traffic-manager-manage-profiles.md).

1. **Tworzenie profilu usługi Traffic Manager:** Nadaj profilowi usługi Traffic Manager unikatową nazwę. Ta nazwa profilu hello jest częścią nazwy DNS hello i działa jako prefiksu dla etykiety nazwy domeny usługi Traffic Manager hello. Nazwa Hello / prefiks jest dodane toocreate too.trafficmanager.net etykietę DNS dla Menedżera ruchu. Poniższy zrzut ekranu Hello pokazuje Menedżera ruchu hello ustawiany jak mysts i wynikowy Etykieta DNS zostanie mysts.trafficmanager.net prefiks DNS. 
   
    ![Tworzenie profilu usługi Traffic Manager](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Metoda routingu ruchu:** W usłudze Traffic Manager są dostępne trzy opcje routingu:
   
   * Priorytet 
   * Wydajność
   * Ważona
     
     **Wydajność** hello zaleca się opcja tooachieve szybkiego AD FS infrastruktury. Można jednak wybrać dowolną metodę routingu najlepiej dopasowaną do potrzeb wdrożenia. Witaj AD FS funkcji nie ma wpływu na powitania wybraną opcją routingu. Zobacz [Metody routingu ruchu w usłudze Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md), aby uzyskać więcej informacji. Witaj zrzut ekranu przykładu powyżej, które zawiera hello **wydajności** wybranej metody.
3. **Skonfiguruj punkty końcowe:** na stronie Menedżera ruchu powitania kliknij punkty końcowe i wybierz pozycję Dodaj. Spowoduje to otwarcie Dodaj punkt końcowy strony podobne toohello Poniższy zrzut ekranu
   
   ![Konfigurowanie punktów końcowych](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   W przypadku hello różnych komponentów, wykonaj poniższe wytyczne hello:
   
   **Typ:** wybierz punktu końcowego platformy Azure, jak firma Microsoft będzie wskazywać tooan Azure publicznego adresu IP.
   
   **Nazwa:** utworzyć nazwę, które mają tooassociate z punktem końcowym hello. To nie jest nazwą DNS hello i nie ma żadnego wpływu na rekordy DNS.
   
   **Docelowy typ zasobu:** wybierz publiczny adres IP jako właściwość toothis wartość hello. 
   
   **Zasób docelowy:** zapewni toochoose opcji z innej etykiety DNS hello masz dostępnych w ramach Twojej subskrypcji. Wybierz hello odpowiedniego punktu końcowego toohello konfigurowanej etykiety DNS.
   
   Dodaj punkt końcowy dla każdego regionu geograficznego, interesujące hello Azure Traffic Manager tooroute ruchu.
   Aby uzyskać więcej informacji oraz szczegółowe kroki dotyczące tooadd / skonfiguruj punkty końcowe w Menedżerze ruchu, zapoznaj się zbyt[Dodawanie, wyłączanie, włączanie lub usuwanie punktów końcowych](../traffic-manager/traffic-manager-endpoints.md)
4. **Skonfiguruj sondowania:** na stronie Menedżera ruchu powitania kliknij w konfiguracji. Na stronie konfiguracji hello potrzebna toochange hello monitor ustawienia tooprobe HTTP portu 80 oraz /adfs/probe ścieżki względnej
   
    ![Konfigurowanie sondy](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Upewnij się, że hello stan punktów końcowych hello jest ONLINE po zakończeniu konfiguracji hello**. Jeśli wszystkie punkty końcowe są w stanie "obniżeniem", usługi Azure Traffic Manager wykona najlepsze próba tooroute hello ruchu sieciowego przy założeniu, że hello diagnostyki jest nieprawidłowy, a wszystkie punkty końcowe są dostępne.
   > 
   > 
5. **Modyfikowanie rekordów DNS dla usługi Azure Traffic Manager:** usługi federacyjnej powinna być nazwą DNS Menedżera ruchu Azure toohello CNAME. Utwórz rekord CNAME w hello publicznych rekordów DNS tak, aby rzeczywiście kto próbuje usługi federacyjnej hello tooreach osiągnie hello Azure Traffic Manager.
   
    Na przykład toopoint hello federacyjnych usługi fs.fabidentity.com toohello Menedżera ruchu, będzie potrzebny tooupdate Twojego hello toobe rekordów zasobów DNS po:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>Testowanie hello routingu i logowania usług AD FS
### <a name="routing-test"></a>Test routingu
Bardzo podstawowy test routingu hello byłoby tootry ping hello nazwa usługi federacyjnej DNS na komputerze w każdym regionie geograficznym. W zależności od wybranej metody routingu hello hello punktu końcowego, który faktycznie pakiety usługi ping zostaną odzwierciedlone w hello ping wyświetlania. Na przykład w przypadku wybrania wydajności hello routingu, następnie końcowy hello najbliżej toohello region powitania klienta zostanie podjęta. Poniżej znajdują się hello migawkę dwa polecenia ping z dwóch komputerów klienckich w innym regionie, co w regionie EastAsia i jeden w zachodnie stany USA. 

![Test routingu](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>Test logowania za pomocą usług AD FS
Hello Najprostszym sposobem tootest usług AD FS jest przy użyciu hello IdpInitiatedSignon.aspx strony. W kolejności toobe toodo możliwe, że jest wymagane tooenable hello IdpInitiatedSignOn właściwości hello usług AD FS. Wykonaj kroki hello poniżej tooverify konfigurację usług AD FS

1. Uruchom hello poniżej polecenia cmdlet na powitania AD FS serwera przy użyciu programu PowerShell, tooset go tooenabled. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. Przy użyciu dowolnej maszyny zewnętrznej otwórz stronę https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. Powinna zostać wyświetlona strona hello usług AD FS, takich jak poniżej:
   
    ![Test usług AD FS — żądanie uwierzytelnienia](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    Po pomyślnym zalogowaniu zostanie wyświetlony poniższy komunikat:
   
    ![Test usług AD FS — uwierzytelnianie powiodło się](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Powiązane linki
* [Podstawowe wdrożenie usług AD FS na platformie Azure](active-directory-aadconnect-azure-adfs.md)
* [Microsoft Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)
* [Metody routingu ruchu w usłudze Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>Następne kroki
* [Zarządzanie profilem usługi Azure Traffic Manager](../traffic-manager/traffic-manager-manage-profiles.md)
* [Dodawanie, usuwanie, włączanie i wyłączanie punktów końcowych](../traffic-manager/traffic-manager-endpoints.md) 

