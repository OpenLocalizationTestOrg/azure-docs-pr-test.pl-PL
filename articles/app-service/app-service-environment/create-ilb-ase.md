---
title: "aaaCreate i użyj wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji Azure"
description: "Więcej informacji na temat toocreate i korzystania ze środowiska usługi aplikacji Azure izolowane internet"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a>Tworzenie i używanie wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji #

 Środowiska usługi aplikacji Azure to wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure (VNet). Istnieją dwa sposoby toodeploy środowiska usługi App Service (ASE): 

- Z adresów VIP na zewnętrzny adres IP często nazywane ASE zewnętrznych.
- Z adresów VIP na wewnętrzny adres IP często nazywane ASE ILB, ponieważ hello wewnętrzny punkt końcowy jest wewnętrzny moduł równoważenia obciążenia (ILB). 

W tym artykule opisano sposób toocreate ASE ILB. Omówienie hello ASE, zobacz [środowiska usługi tooApp wprowadzenie][Intro]. toolearn toocreate ASE zewnętrznych, zobacz temat [Tworzenie zewnętrznych ASE][MakeExternalASE].

## <a name="overview"></a>Omówienie ##

Można wdrożyć ASE z punktem końcowym dostęp do Internetu lub adres IP w sieci wirtualnej. tooset tooa adresów sieci wirtualnej, powitalne ASE muszą być wdrażane z ILB adresów hello IP. Podczas wdrażania sieci ASE z ILB, należy podać:

-   Własnej domeny, który jest używany podczas tworzenia aplikacji.
-   Witaj certyfikat używany do obsługi protokołu HTTPS.
-   Zarządzanie systemem DNS dla domeny.

W zamian można wykonać czynności takich jak:

-   Host aplikacji intranetowych bezpiecznie w chmurze hello dostęp za pośrednictwem sieci VPN platformy Azure ExpressRoute lub lokacja lokacja.
-   Aplikacje hosta w chmurze hello, które nie są wymienione w publicznych serwerów DNS.
-   Utwórz izolowaną internet zaplecza aplikacji, które frontonu aplikacji bezpiecznego można zintegrować z.

### <a name="disabled-functionality"></a>Funkcje wyłączone ###

Istnieje kilka kwestii, które nie można wykonać, gdy używasz ASE ILB:

-   Użyj opartych na protokole SSL.
-   Przypisz adresy IP toospecific aplikacji.
-   Kup i korzystać z certyfikatu z aplikacji za pośrednictwem hello portalu Azure. Można uzyskać certyfikatów bezpośrednio od urzędu certyfikacji i używać ich z aplikacjami. Nie można uzyskać je za pośrednictwem hello portalu Azure.

## <a name="create-an-ilb-ase"></a>Utwórz ILB ASE ##

toocreate ASE ILB:

1. Hello portalu Azure, wybierz **nowy** > **sieci Web i mobilność** > **środowiska usługi aplikacji**.

2. Wybierz subskrypcję.

3. Wybierz lub utwórz grupę zasobów.

4. Wybierz lub Utwórz sieć wirtualną.

5. W przypadku wybrania istniejącej sieci wirtualnej, należy toocreate hello toohold podsieci ASE. Upewnij się, tooset podsieci rozmiaru tooaccommodate wystarczająco duży przyszłego rozwoju ASE sieci. Firma Microsoft zaleca o rozmiarze `/25`, który 128 adresów i może obsłużyć ASE rozmiar maksymalny. Minimalny rozmiar Hello można wybrać jest `/28`. Po wymaga infrastruktury, ten rozmiar może być skalowana tooa maksymalna liczba wystąpień 11.

    * Wykracza poza hello domyślne maksymalnie 100 wystąpieniami w planów usługi aplikacji.

    * Skalowanie bliskie 100, ale także z bardziej szybkie skalowanie frontonu.

6. Wybierz **wirtualnego lokalizacji** > **konfiguracji sieci wirtualnej**. Zestaw hello **typu VIP** za**wewnętrzne**.

7. Wprowadź nazwę domeny. Ta domena jest hello używane jako aplikacje utworzone w tym ASE. Istnieją pewne ograniczenia. Nie można go:

    * NET   

    * azurewebsites.NET

    * p.azurewebsites.NET

    * &lt;asename&gt;. p.azurewebsites.net

   Hello niestandardowej nazwy domeny używane do aplikacji i nazwy domeny hello używany przez Twoje ASE nie może nakładać się. Dla ASE ILB z nazwą domeny hello _contoso.com_, nie można użyć niestandardowych nazw domen dla twojej aplikacji, takich jak:

    * www.contoso.com

    * Abcd.def.contoso.com

    * Abcd.contoso.com

   Jeśli znasz hello niestandardowych nazw domen dla aplikacji, wybierz domenę dla hello ASE ILB, który nie występuje konflikt z tymi nazwami domen niestandardowych. W tym przykładzie, można użyć przypominać *contoso internal.com* dla domeny Twojej ASE hello ponieważ nie będących w konflikcie z nazwami domen niestandardowych, które kończą się *. contoso.com*.

8. Wybierz **OK**, a następnie wybierz **Utwórz**.

    ![Tworzenie środowiska ASE][1]

Na powitania **sieci wirtualnej** bloku jest **konfiguracja sieci wirtualnej** opcji. Służy on tooselect zewnętrznego adresu VIP lub jako wewnętrzny adres VIP. Domyślnie Hello **zewnętrznych**. W przypadku wybrania **zewnętrznych**, Twoje ASE używa VIP dostępny z Internetu. W przypadku wybrania **wewnętrzne**, Twoje ASE skonfigurowano ILB na adres IP w sieci wirtualnej.

Po wybraniu **wewnętrzne**, tooadd możliwości hello więcej adresów IP tooyour ASE zostanie usunięta. Zamiast tego należy tooprovide domeny hello hello ASE. W elemencie ASE z zewnętrznego adresu VIP hello nazwa hello ASE jest używany w domenie hello aplikacji utworzone w tym ASE.

Jeśli ustawisz **typu VIP** za**wewnętrzne**, nazwę ASE nie jest używany w domenie hello na powitania ASE. Należy jawnie określić domenę hello. Jeśli Twoja domena to *contoso.corp.net* i utworzyć aplikację, w tym o nazwie ASE *timereporting*, hello adres URL dla tej aplikacji jest timereporting.contoso.corp.net.


## <a name="create-an-app-in-an-ilb-ase"></a>Utwórz aplikację w elemencie ASE ILB ##

Utwórz aplikację w elemencie ASE ILB w hello samo tworzenie aplikacji w elemencie ASE normalnie.

1. Hello portalu Azure, wybierz **nowy** > **sieci Web i mobilność** > **Web** lub **Mobile** lub  **Aplikacja interfejsu API**.

2. Wprowadź nazwę aplikacji hello hello.

3. Wybierz subskrypcję hello.

4. Wybierz lub utwórz grupę zasobów.

5. Wybierz lub Utwórz plan usługi aplikacji. Toocreate nowy plan usługi aplikacji, wybierz opcję sieci ASE jako hello lokalizacji. Wybierz miejsce Twojego toobe planu usługi aplikacji utworzone puli procesów roboczych hello. Po utworzeniu planu usługi aplikacji hello wybierz Twoje ASE jako lokalizacji hello i hello puli procesów roboczych. Po określeniu nazwy hello aplikacji hello domeny hello pod nazwą aplikacji zastępuje hello domeny dla Twojego ASE.

6. Wybierz pozycję **Utwórz**. Tooappear aplikacji hello na pulpicie nawigacyjnym, zaznacz **toodashboard numeru Pin** pole wyboru.

    ![Tworzenie planu usługi aplikacji][2]

    W obszarze **Nazwa aplikacji**, nazwa domeny hello jest domeny hello zaktualizowane tooreflect Twojego ASE.

## <a name="post-ilb-ase-creation-validation"></a>Sprawdzanie poprawności tworzenia POST ILB ASE ##

ASE ILB są nieco inne niż hello nie - ILB ASE. Jak już zanotowane należy toomanage własne DNS. Masz również tooprovide swój własny certyfikat dla połączeń HTTPS.

Po utworzeniu sieci ASE hello nazwa domeny zawiera hello określonej domeny. Nowy element jest wyświetlany w **ustawienie** menu o nazwie **certyfikatu ILB**. Witaj ASE jest tworzony przy użyciu certyfikatu, który nie określa domeny ILB ASE hello. Korzystając z tego certyfikatu hello ASE, przeglądarki informuje, czy jest on nieprawidłowy. Ten certyfikat umożliwia łatwiejsze tootest HTTPS, ale należy tooupload własnego certyfikatu, który jest wiązana tooyour ILB ASE domeny. Ten krok jest niezbędny, niezależnie od tego, czy certyfikat z podpisem własnym, czy otrzymanego od urzędu certyfikacji.

![Nazwa domeny ILB ASE][3]

Twoje ASE ILB musi mieć prawidłowy certyfikat SSL. Użyj certyfikatu wewnętrznego urzędów, kupić certyfikat od zewnętrznego wystawcy lub Użyj certyfikatu z podpisem własnym. Niezależnie od źródła hello hello certyfikatu SSL hello następujące atrybuty certyfikatu należy toobe prawidłowo skonfigurowane:

* **Temat**: ten atrybut musi być ustawiony too*.your głównego domeny tutaj.
* **Alternatywna nazwa podmiotu**: ten atrybut musi zawierać zarówno **.your głównego domeny tutaj* i **.scm.your-głównego-domeny — w tym miejscu*. Toohello połączenia SSL SCM/Kudu lokacji skojarzone z każdej aplikacji używać adresu formularza hello *your-app-name.scm.your-root-domain-here*.

Konwertuj/Zapisz certyfikat SSL hello jako plik pfx. plik PFX Hello musi obejmować wszystkie pośrednie i certyfikaty główne. Zabezpiecz ją przy użyciu hasła.

Jeśli chcesz toocreate certyfikatu z podpisem własnym, można użyć poleceń programu PowerShell hello tutaj. Można toouse czy nazwy domeny ILB ASE zamiast *internal.contoso.com*: 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

certyfikat Hello generowanie tych poleceń programu PowerShell oflagowane przez przeglądarki, ponieważ hello certyfikat nie został utworzony przez urząd certyfikacji, który znajduje się w łańcuch zaufania w przeglądarce. tooget certyfikatu, który ufa przeglądarkę, uzyskaj od urzędu certyfikacji komercyjnych w łańcuchu zaufania w przeglądarce. 

![Zestaw ILB certyfikatu][4]

tooupload własne certyfikaty i test dostępu:

1. Po utworzeniu hello ASE Przejdź toohello ASE interfejsu użytkownika. Wybierz **ASE** > **ustawienia** > **certyfikatu ILB**.

2. tooset hello ILB certyfikat, wybierz plik .pfx certyfikatu hello i podaj hasło hello. Ten krok zajmuje kilka tooprocess czas. Pojawi się komunikat z informacją, że operacja przekazywania jest w toku.

3. Pobierz adres ILB hello Twojej ASE. Wybierz **ASE** > **właściwości** > **wirtualny adres IP**.

4. Tworzenie aplikacji sieci web w sieci ASE po utworzeniu hello ASE.

5. Tworzenie maszyny Wirtualnej, jeśli nie istnieje w tej sieci wirtualnej.

    > [!NOTE] 
    > Nie próbuj toocreate tej maszyny Wirtualnej w tej samej podsieci Witaj, jak hello ASE, ponieważ będzie zakończyć się niepowodzeniem lub spowodować problemy.
    >
    >

6. Ustaw hello DNS dla domeny ASE. Za pomocą symbolu wieloznacznego i domeny w systemie DNS. toodo prostych testów, Edytuj plik hosts hello na Twojej maszyny Wirtualnej tooset hello sieci web aplikacji Nazwa toohello adres VIP:

    a. Jeśli Twoje ASE ma nazwę domeny hello _. ilbase.com_ i utworzysz aplikację sieci web hello o nazwie _mytestapp_, jest skierowana na _mytestapp.ilbase.com_. Następnie ustaw _mytestapp.ilbase.com_ tooresolve toohello ILB adresu. (W systemie Windows, plik hosts hello jest na _C:\Windows\System32\drivers\etc\_.)

    b. tootest sieci web wdrożenia publikowania lub dostęp toohello zaawansowane konsoli, Utwórz rekord _mytestapp.scm.ilbase.com_.

7. Korzystanie z przeglądarki na tej maszynie Wirtualnej, przejdź do http://mytestapp.ilbase.com. (Lub przejdź toowhatever, którego nazwę aplikacji sieci web z domeną.)

8. Korzystanie z przeglądarki na tej maszynie Wirtualnej, przejdź do https://mytestapp.ilbase.com. Jeśli używasz certyfikatu z podpisem własnym, należy zaakceptować hello braku zabezpieczeń.

    adres IP Twojego ILB Hello jest wyświetlana w obszarze **adresów IP**. Ta lista zawiera również hello adresy IP używane przez zewnętrznych adresów VIP hello i ruchu przychodzącego zarządzania.

    ![Adres ILB IP][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a>Sieci Web zadania, funkcje i hello ILB ASE

Zarówno funkcje i zadania sieci web są obsługiwane w elemencie ASE ILB, ale hello portalu toowork z nimi, musisz mieć lokacji SCM toohello dostępu do sieci.  Oznacza to, że na hoście, który jest albo połączenia wirtualnej sieci toohello musi być przeglądarki.  

Gdy używasz usługi Azure Functions w elemencie ASE ILB, może pobrać komunikat o błędzie stwierdzający "nie jesteśmy w stanie tooretrieve funkcji w tej chwili. Spróbuj ponownie później." Ten błąd występuje, ponieważ hello interfejsu użytkownika funkcji wykorzystuje hello SCM lokacji za pośrednictwem protokołu HTTPS i certyfikatu głównego hello nie znajduje się w przeglądarce hello łańcuch zaufania. Zadania Web Job ma podobny problem. tooavoid ten problem, można wykonać jedną z następujących hello:

- Dodawanie magazynu zaufanych certyfikatów tooyour certyfikatu hello. Odblokowuje to Edge i przeglądarki Internet Explorer.
- Użyj Chrome i odwiedź witrynę SCM toohello najpierw, Zaakceptuj hello niezaufany certyfikat, a następnie przejdź toohello portalu.
- Użyj komercyjnych certyfikat w łańcuchu zaufania przeglądarki.  Jest to hello najlepszym rozwiązaniem.  

## <a name="dns-configuration"></a>Konfiguracja DNS ##

Gdy używasz zewnętrznego adresu VIP hello DNS jest zarządzana przez platformę Azure. Wszystkich aplikacji utworzonych w Twojej ASE jest automatycznie dodawany tooAzure DNS, który jest publicznym systemie DNS. W elemencie ASE ILB możesz zarządzać własną DNS. Dla danej domeny, takie jak _contoso.net_, należy toocreate A systemu DNS są rejestrowane w systemie DNS tego adresu ILB tooyour punktu dla:

- *. contoso.net
- *. scm.contoso.net

Jeśli domenę ILB ASE jest używany dla wielu elementów poza tym ASE, może być konieczne toomanage DNS na podstawie ciągu app-name. Ta metoda może być trudne, ponieważ potrzebna tooadd każdej nowej nazwy aplikacji w systemie DNS podczas jego tworzenia. Z tego powodu zaleca się użycie dedykowanych domeny.

## <a name="publish-with-an-ilb-ase"></a>Publikowanie za pomocą ILB ASE ##

Każda aplikacja, która zostanie utworzona są dwa punkty końcowe. W elemencie ASE ILB masz  *&lt;Nazwa aplikacji >.&lt; Domeny ASE ILB >* i  *&lt;Nazwa aplikacji > .scm.&lt; Domeny ASE ILB >*. 

Nazwa witryny SCM Hello przyjmuje konsoli Kudu toohello, nazywanym hello **portal zaawansowane**, poziomu hello portalu Azure. Konsola Kudu Hello umożliwia wyświetlanie zmiennych środowiskowych, Eksploruj hello dysku, użyj konsoli i o wiele więcej. Aby uzyskać więcej informacji, zobacz [konsoli Kudu dla usługi Azure App Service][Kudu]. 

W wielodostępnej hello usługi aplikacji i zewnętrznego ASE Brak rejestracji jednokrotnej między hello portalu Azure i hello Kudu konsoli. Dla hello ILB ASE jednak należy toouse Twojego publikowania toosign poświadczeń do hello Kudu konsoli.

Internetowych systemów elementu konfiguracji, takich jak GitHub i Visual Studio Team Services nie działają z ASE ILB, ponieważ hello punkt końcowy publikowania nie jest dostępny internet. Zamiast tego należy toouse systemu elementu konfiguracji, który wykorzystuje model ściągania, takich jak Dropbox.

Witaj publikowania punktów końcowych dla aplikacji w elemencie ASE ILB korzystania z domeny hello tego hello ILB ASE została utworzona z. Ta domena jest wyświetlany w profilu publikowania aplikacji hello i w bloku portalu aplikacji hello (**omówienie** > **Essentials** , a także **właściwości**). Jeśli masz ASE ILB z poddomeny hello *contoso.net* i aplikację o nazwie *test*, użyj *mytest.contoso.net* dla FTP i *mytest.scm.contoso.net*  wdrożenia sieci web.

## <a name="couple-an-ilb-ase-with-a-waf-device"></a>Połączenie ASE ILB z urządzenia zapory aplikacji sieci Web ##

Usługa aplikacji Azure udostępnia wiele środki bezpieczeństwa, które ochrona powitalnych systemu. Ułatwiają również toodetermine czy aplikacji zostało zaatakowane. Witaj ochrony najlepsze dla aplikacji sieci web jest toocouple hostingu platformie, takich jak usługi Azure App Service za pomocą zapory aplikacji sieci web (WAF). Ponieważ hello ILB ASE ma punkt końcowy aplikacji izolowane sieci, jest odpowiednie do takiego użycia.

więcej informacji na temat tooconfigure Twojego ASE ILB z urządzenia zapory aplikacji sieci Web, zobacz temat toolearn [Konfigurowanie zapory aplikacji sieci web ze środowiskiem usługi aplikacji][ASEWAF]. W tym artykule przedstawiono sposób toouse Barracuda urządzenie wirtualne z Twojej ASE. Innym rozwiązaniem jest toouse Azure Application Gateway. Brama aplikacji w używa hello OWASP podstawowe reguły toosecure umieścić wszystkie aplikacje za nią. Aby uzyskać więcej informacji na temat bramy aplikacji, zobacz [zapory aplikacji sieci web platformy Azure toohello wprowadzenie][AppGW].

## <a name="get-started"></a>Rozpoczęcie pracy ##

Wszystkie artykuły i jak tooinstructions dla ASEs są dostępne w [Plik README dla środowiska usługi aplikacji][ASEReadme].

* tooget wprowadzenie ASEs, zobacz [środowiska usługi tooApp wprowadzenie][Intro].
* Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
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
