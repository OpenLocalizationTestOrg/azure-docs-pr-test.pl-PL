---
title: "aaaUse środowiska usługi aplikacji Azure"
description: "Jak toocreate, publikowanie i skalowanie aplikacji w środowisku usługi aplikacji Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a>Użyj środowiska usługi aplikacji #

## <a name="overview"></a>Omówienie ##

Środowiska usługi aplikacji Azure to wdrożenie usługi Azure App Service w podsieci sieci wirtualnej platformy Azure klienta. Składa się z:

- **Zakończenia przód**: hello front końce są, gdzie HTTP/HTTPS kończy się w środowisku usługi aplikacji (ASE).
- **Pracownicy**: hello pracownicy są hello zasobów, które hosta aplikacji.
- **Baza danych**: hello bazy danych zawiera informacje określające hello środowiska.
- **Magazyn**: Magazyn hello jest używane toohost hello opublikowane klienta aplikacji.

> [!NOTE]
> Istnieją dwie wersje środowiska usługi aplikacji: ASEv1 i ASEv2. W ASEv1 możesz zarządzać zasobami hello przed ich użyciem. toolearn jak tooconfigure i zarządzać ASEv1, zobacz [skonfigurować v1 środowiska usługi aplikacji][ConfigureASEv1]. Witaj dalszej części tego artykułu koncentruje się na ASEv2.
>
>

ASE (ASEv1 i ASEv2) można wdrożyć z zewnętrznym lub wewnętrznym adresu VIP do uzyskania dostępu do aplikacji. Wdrażanie Hello za pomocą zewnętrznego wirtualnego adresu IP jest popularnie określany ASE zewnętrznych. wersja wewnętrznej Hello jest nazywana hello ILB ASE, ponieważ używa wewnętrznego modułu równoważenia obciążenia (ILB). Zobacz toolearn więcej informacji na temat hello ILB ASE [tworzenie i używanie ASE ILB][MakeILBASE].

## <a name="create-a-web-app-in-an-ase"></a>Tworzenie aplikacji sieci web w elemencie ASE ##

toocreate aplikacji sieci web w elemencie ASE używasz hello tego samego procesu jak podczas tworzenia go normalnie, ale z kilku niewielkie różnice. Podczas tworzenia nowego planu usługi aplikacji:

- Zamiast wybierać lokalizacji geograficznej które toodeploy aplikacji, wybierz polecenie ASE jako lokalizacji.
- Wszystkich utworzonych w elemencie ASE planów usługi aplikacji musi być izolowany warstwy cenowej.

Jeśli nie masz ASE, możesz utworzyć jedną wykonując instrukcje hello [tworzenie środowiska usługi aplikacji][MakeExternalASE].

toocreate aplikacji sieci web w elemencie ASE:

1. Wybierz **nowe** > **sieci Web i mobilność** > **sieci Web aplikacji**.

2. Wprowadź nazwę dla aplikacji sieci web hello. Jeśli plan usługi aplikacji jest już wybrana w elemencie ASE, hello nazwy domeny dla aplikacji hello odzwierciedla nazwy domeny hello hello ASE.

    ![Wybór nazwy aplikacji sieci Web][1]

3. Wybierz subskrypcję.

4. Wprowadź nazwę nowej grupy zasobów lub wybierz **Użyj istniejącego** i wybierz z listy rozwijanej hello.

5. Wybierz istniejący plan usługi aplikacji w Twojej ASE lub Utwórz nową, wykonując następujące kroki:

    a. Wybierz **tworzenia nowych**.

    b. Wprowadź nazwę planu usługi aplikacji hello.

    c. Wybierz użytkownika ASE hello **lokalizacji** listy rozwijanej.

    d. Wybierz **izolowany** warstwy cenowej. Wybierz **wybierz**.

    e. Kliknij przycisk **OK**.
    
    ![Izolowane warstw cenowych][2]

6. Wybierz pozycję **Utwórz**.

## <a name="how-scale-works"></a>Jak skalować działa ##

Każda aplikacja usługi aplikacji jest uruchamiany w plan usługi aplikacji. model kontenera Hello jest środowisk przytrzymaj planów usługi App Service i planów usługi App Service przechowywania aplikacji. Skalowanie aplikacji należy skalowanie hello planu usługi aplikacji i w związku z tym wszystkie aplikacje hello w hello sam plan.

W ASEv2 skalowanie planu usługi App Service infrastruktury hello potrzebne jest automatycznie dodawany. Istnieje opóźnienie operacji tooscale podczas infrastruktury hello jest dodawany. ASEv1 infrastruktury hello potrzebne muszą zostać dodane przed utworzeniem lub skalowanie planu usługi aplikacji. 

W wielodostępnej hello usługi aplikacji, skalowanie jest zwykle natychmiastowego ponieważ puli zasobów jest łatwo dostępny toosupport go. W elemencie ASE istnieje takie buforu i zasoby są przydzielane na potrzeby.

W elemencie ASE można skalować too100 wystąpień. Te wystąpienia, 100 może być wszystko w jednym jednego planu usługi aplikacji lub rozproszone na wielu planów usługi aplikacji.

## <a name="ip-addresses"></a>Adresy IP ##

Usługa aplikacji musi tooallocate możliwości hello dedykowanego aplikacjami tooan adresu IP. Ta funkcja jest dostępna po skonfigurowaniu opartych na protokole SSL, zgodnie z opisem w [Powiąż istniejący niestandardowy SSL certyfikatu tooAzure aplikacje sieci web][ConfigureSSL]. W elemencie ASE istnieje jednak zauważalne wyjątku. Nie można dodać dodatkowe IP adresy używane do opartych na protokole SSL w elemencie ASE ILB toobe.

W ASEv1 należy adresy IP hello tooallocate jako zasoby przed ich użyciem. W ASEv2 można ich używać z aplikacji tak samo jak w wielodostępnej hello usługi aplikacji. Istnieje jeden adres zapasowe w ASEv2 się too30 adresów IP. Zawsze używany jest jeden, inny są dodawane, że adres zawsze jest gotowe do użycia. Wymagany czas opóźnienia jest tooallocate innego adresu IP, co uniemożliwia dodanie IP adresów szybkie naciśnięcie.

## <a name="front-end-scaling"></a>Skalowanie frontonu ##

W ASEv2, podczas skalowania planów usługi aplikacji, pracownicy są automatycznie dodawane toosupport je. Co ASE jest tworzony z przodu punktów końcowych. Ponadto hello front kończy się automatycznie skalować w poziomie z szybkością co frontonu dla każdego wystąpienia 15 w planów usługi aplikacji. Na przykład jeśli masz wystąpień 15 masz trzy front kończy się. Skala wystąpień too30 użytkownik ma cztery zakończenia przód i tak dalej.

Ten numer interfejsy powinny być to wystarczająca liczba dla większości scenariuszy. Jednak można skalować w poziomie szybsze. Współczynnik hello, który tooas mało jako jeden frontonu dla każdego wystąpienia pięć, można zmienić. Opłata za zmianę stosunek hello nie istnieje. Aby uzyskać więcej informacji, zobacz [cennik usługi aplikacji Azure][Pricing].

Frontonu zasoby są punktu końcowego HTTP/HTTPS hello hello ASE. Z hello frontonu konfiguracji domyślnej użycie pamięci na fronton jest stale około 60 procent. Obciążeń klientów nie działają na fronton. Witaj kluczowe znaczenie dla frontonu z tooscale względem jest hello Procesora, który jest wymuszany głównie przez ruchu HTTPS.

## <a name="app-access"></a>Dostęp do aplikacji ##

W zewnętrznej ASE hello domeny, który jest używany podczas tworzenia aplikacji różni się od wielodostępnej hello usługi aplikacji. Obejmuje on nazwę hello hello ASE. Aby uzyskać więcej informacji na temat toocreate ASE zewnętrznych, zobacz [tworzenie środowiska usługi aplikacji][MakeExternalASE]. wygląda Hello nazwę domeny w elemencie ASE zewnętrznych *.&lt; asename&gt;. p.azurewebsites.net*. Na przykład, jeśli nosi nazwę Twojej ASE _ase zewnętrzne_ i hosta aplikacji o nazwie _contoso_ w tym ASE, możesz uzyskać do niej dostęp na powitania następujące adresy URL:

- contoso.external ase.p.azurewebsites.net
- contoso.SCM.external ase.p.azurewebsites.net

adres URL Hello contoso.scm.external-ase.p.azurewebsites.net jest używane tooaccess hello Kudu konsoli lub do publikowania aplikacji za pomocą sieci web wdrażanie. Aby uzyskać informacje na powitania Kudu konsoli, zobacz [konsoli Kudu dla usługi Azure App Service][Kudu]. Hello Kudu konsoli zapewnia interfejsu użytkownika sieci web dla debugowania przekazywania plików, edytowanie plików i wiele innych.

W elemencie ASE ILB należy określić domeny hello w czasie wdrażania. Aby uzyskać więcej informacji na temat toocreate ILB ASE, zobacz temat [tworzenie i używanie ASE ILB][MakeILBASE]. Jeśli określisz nazwy domeny hello _ilb ase.info_, hello aplikacji, w tym ASE korzystania z tej domeny podczas tworzenia aplikacji. Dla aplikacji hello o nazwie _contoso_, adresy URL hello są:

- contoso.ilb ase.info
- contoso.SCM.ilb ase.info

## <a name="publishing"></a>Publikowanie ##

Podobnie jak w przypadku wielodostępnej hello usługi aplikacji, w elemencie ASE można opublikować z:

- Wdrażanie sieci Web.
- FTP.
- Ciągłej integracji.
- Przeciągnij i upuść hello Kudu konsoli.
- IDE, takie jak Visual Studio, Eclipse lub IntelliJ IDEA

Te opcje publikowania, wszystkie działały z zewnętrznego ASE hello takie same. Aby uzyskać więcej informacji, zobacz [wdrożenia w usłudze Azure App Service][AppDeploy]. 

Główna różnica Hello z publikowaniem się względem tooan ILB ASE. Z ASE ILB hello publikowania punkty końcowe będą dostępne tylko za pośrednictwem hello ILB. Witaj ILB znajduje się na prywatnego adresu IP w podsieci ASE hello w hello sieci wirtualnej. Jeśli nie masz toohello dostępu do sieci ILB, nie można opublikować żadnej aplikacji na tym ASE. Zgodnie z opisem w [tworzenie i używanie ASE ILB][MakeILBASE], należy dla aplikacji hello tooconfigure DNS w systemie hello. Która zawiera punkt końcowy SCM hello. Jeśli nie są prawidłowo zdefiniowane, nie można opublikować. Twoje IDEs może też być konieczne toohello dostępu do sieci toohave ILB w kolejności toopublish tooit bezpośrednio.

Internetowych systemów elementu konfiguracji, takich jak GitHub i Visual Studio Team Services nie działają z ASE ILB, ponieważ punkt końcowy publikowania hello nie jest dostępny Internet. Zamiast tego należy toouse systemu elementu konfiguracji, który wykorzystuje model ściągania, takich jak Dropbox.

Witaj publikowania punktów końcowych dla aplikacji w elemencie ASE ILB korzystania z domeny hello tego hello ILB ASE została utworzona z. Można to sprawdzić w profilu publikowania aplikacji hello i w bloku portalu aplikacji hello (w **omówienie** > **Essentials** oraz w **właściwości**). 

## <a name="pricing"></a>Cennik ##

Witaj cennik SKU o nazwie **izolowany** został utworzony do użytku z ASEv2. Wszystkie plany usługi aplikacji, które znajdują się w ASEv2 znajdują się w hello izolowany cennik jednostki SKU. Izolowane stawki planu usługi aplikacji może się różnić dla regionu. 

Ponadto plany toohello cen usługi App, jest stawka płaski ASE samej siebie. Hello szybkość płaski nie zmienia się rozmiar hello Twojej ASE i płaci infrastruktury hello ASE na domyślny skalowanie szybkość 1 dodatkowe frontonu dla każdego 15 wystąpieniach planu usługi aplikacji.  

Jeśli szybkość skali domyślne hello 1 frontonu dla każdego 15 wystąpieniach planu usługi aplikacji nie jest wystarczająca, można dostosować stosunek hello jaką zakończenia przód są dodawane lub hello rozmiar końców przodu hello.  Po zmodyfikowaniu stosunek hello lub rozmiar płacisz za hello rdzeni frontonu, które nie zostanie dodany domyślnie.  

Na przykład jeśli można dopasować too10 współczynnik skali hello, fronton jest dodawany do co 10 wystąpień w planów usługi aplikacji. stałe opłaty Hello obejmuje współczynnika skalowania jeden frontonu dla każdego wystąpienia 15. O stosunku skali 10 opłaty opłacać hello trzeci fronton, który został dodany do hello 10 wystąpieniach planu usługi aplikacji. Nie trzeba toopay go po osiągnięciu 15 wystąpienia, ponieważ zostało dodane automatycznie.

Jeśli dostosować rozmiar hello hello zakończenia przód too2 rdzeni, ale nie ustawiaj stosunek hello, a następnie płacisz za hello dodatkowe rdzenie.  ASE jest tworzony z 2 przodu zakończenia, dlatego nawet poniżej hello automatycznego skalowania progu 2 dodatkowe rdzenie będą opłacać po zwiększeniu hello rozmiar too2 core przodu końców.

Aby uzyskać więcej informacji, zobacz [cennik usługi aplikacji Azure][Pricing].

## <a name="delete-an-ase"></a>Usuń ASE ##

toodelete ASE: 

1. Użyj **usunąć** u góry hello hello **środowiska usługi aplikacji** bloku. 

2. Wprowadź nazwę użytkownika tooconfirm ASE, które mają toodelete hello go. Po usunięciu ASE, Usuń wszystkie hello zawartości w niej. 

    ![Usuwanie ASE][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


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
