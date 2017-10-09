---
title: aaaActive Directory Federation Services na platformie Azure | Dokumentacja firmy Microsoft
description: "W tym dokumencie przedstawiono sposób toodeploy usług AD FS w systemie Azure dla o wysokiej dostępności."
keywords: "Wdrażanie usług AD FS w systemie azure, wdrażania usług AD FS azure, azure AD FS i usługi azure ad fs, wdrażania usług AD FS, wdrażania usług ad fs usługi AD FS w systemie azure, wdrażania usług AD FS w systemie azure, wdrażania usług AD FS w azure, azure AD FS, wprowadzenie tooAD FS, Azure, usługi AD FS na platformie Azure iaas, usługi AD FS, Przenieś tooazure usług AD FS"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2c39271f7569b9ce395dce2f53f5ba5a4897b132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Wdrażanie usług Active Directory Federation Services na platformie Azure
Usługi AD FS udostępniają uproszczone, zabezpieczone funkcje federacji tożsamości i logowania jednokrotnego (SSO) w sieci Web. Federacja z usługi Azure AD lub usługi Office 365 umożliwia użytkownikom tooauthenticate przy użyciu lokalnych poświadczeń i uzyskiwać dostęp do wszystkich zasobów w chmurze. W związku z tym staje się ważne toohave wysokiej dostępności usług AD FS tooensure infrastruktury dostępu tooresources lokalnie i w chmurze hello. Wdrażanie usług AD FS w systemie Azure mogą pomóc osiągnąć wysoką dostępność hello wymagana z minimalnym działań.
Wdrożenie usług AD FS na platformie Azure niesie ze sobą szereg korzyści, takich jak na przykład:

* **Wysoka dostępność** -o sile hello zestawami dostępności Azure, upewnij się infrastruktury wysokiej dostępności.
* **Łatwe tooScale** — wymagają więcej wydajności? Łatwo przeprowadzić migrację maszyny zaawansowanych toomore za pomocą kilku kliknięć na platformie Azure
* **Nadmiarowość geograficzna między** — z Azure nadmiarowość geograficzna można mieć pewność, infrastruktury jest wysokiej dostępności w Witaj świecie
* **Łatwe tooManage** — z opcjami bardzo uproszczonego zarządzania w portalu Azure, zarządzania infrastrukturą jest bardzo łatwe i kłopotliwy 

## <a name="design-principles"></a>Zasady projektowania
![Projekt wdrożenia](./media/active-directory-aadconnect-azure-adfs/deployment.png)

diagram Hello powyżej pokazuje hello zalecane toostart podstawową topologię wdrażania infrastruktury usług AD FS w systemie Azure. Poniżej wymieniono zasady Hello za hello różne składniki hello topologii:

* **Kontrolery domeny (DC) / serwery usług AD FS**: jeśli liczba użytkowników nie przekracza 1000, można po prostu zainstalować rolę usług AD FS na kontrolerach domeny. Jeśli nie ma żadnych wpływu na kontrolerach domeny hello lub jeśli masz więcej niż 1000 użytkowników, następnie wdrożyć usługi AD FS na różnych serwerach.
* **Serwer proxy** — jest konieczne toodeploy serwerów Proxy aplikacji sieci Web, dzięki czemu użytkownicy mogą korzystać z hello AD FS, gdy nie mają w sieci firmy hello również.
* **DMZ**: hello serwerów Proxy aplikacji sieci Web zostaną umieszczone w hello DMZ i między hello DMZ i podsieci wewnętrznej hello jest dozwolony dostęp tylko TCP/443.
* **Moduły równoważenia obciążenia**: tooensure wysoką dostępność serwerów usług AD FS i serwera Proxy aplikacji sieci Web, zalecamy użycie wewnętrznego modułu równoważenia obciążenia dla serwerów usług AD FS i usługi równoważenia obciążenia Azure dla serwerów Proxy aplikacji sieci Web.
* **Zestawy dostępności**: tooprovide nadmiarowość tooyour AD FS wdrożenia, zalecane jest, grupowanie co najmniej dwie maszyny wirtualne w zestawie dostępności dla podobnych obciążeń. Taka konfiguracja zapewnia dostępność co najmniej jednej maszyny wirtualnej podczas planowanych i nieplanowanych zdarzeń związanych z konserwacją.
* **Konta magazynu**: zalecane jest toohave dwóch kont magazynu. Mając konto magazynu pojedynczego może prowadzić toocreation pojedynczego punktu awarii i może powodować toobecome wdrożenia hello jest niedostępny w scenariuszu mało prawdopodobne, gdy konto magazynu hello ulegnie awarii. Użycie dwóch kont magazynu pozwala powiązać każde konto z linią awarii.
* **Separacja sieci**: serwery proxy aplikacji sieci Web powinny zostać wdrożone w oddzielnej sieci DMZ. Można podzielić na dwie podsieci jedną sieć wirtualną, a następnie wdrożyć serwery Proxy aplikacji sieci Web hello w izolowanej podsieci. Po prostu można skonfigurować hello ustawienia grupy zabezpieczeń sieci dla każdej podsieci i zezwolić tylko wymagane komunikację między dwoma podsieciami hello. Więcej szczegółów podano w poniższych scenariuszach wdrażania.

## <a name="steps-toodeploy-ad-fs-in-azure"></a>Kroki toodeploy usług AD FS w systemie Azure
Hello czynności wymienionych w tej sekcji konspektu hello przewodnik toodeploy hello poniżej przedstawiono ich tutaj infrastruktury usług AD FS w systemie Azure.

### <a name="1-deploying-hello-network"></a>1. Wdrażanie sieci hello
Zgodnie z powyższymi informacjami można utworzyć dwie podsieci w jednej sieci wirtualnej lub skonfigurować dwie całkowicie odrębne sieci wirtualne. W tym artykule omówiono wariant obejmujący wdrożenie jednej sieci wirtualnej, która zostanie podzielona na dwie podsieci. Ta funkcja jest obecnie łatwiejsze podejście jako dwa oddzielne sieci wirtualne wymagają bramy sieci wirtualnej tooVNet komunikacji.

**1.1 Tworzenie sieci wirtualnej**

![Tworzenie sieci wirtualnej](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

W hello portalu Azure i wybierz sieć wirtualną można wdrożyć sieci wirtualnej hello i jedną podsieć natychmiast jednym kliknięciem. INT podsieci jest także zdefiniowana i rozpocząć teraz dodany toobe maszyn wirtualnych.
Witaj, następnym krokiem jest tooadd innej sieci toohello podsieci, czyli hello DMZ podsieci. po prostu toocreate hello podsieci DMZ

* Wybierz nowo utworzony hello sieci
* We właściwościach hello Wybierz podsieć
* W panelu podsieci hello na powitania, kliknij przycisk Dodaj
* Podaj hello podsieci nazwy i adresu miejsca informacji toocreate hello podsieci

![Podsieć](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![Podsieć DMZ](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

**1.2. Tworzenie grup zabezpieczeń sieci hello**

Grupa zabezpieczeń sieci (NSG) zawiera listę reguł listy kontroli dostępu (ACL), które akceptować lub odrzucać ruch sieciowy tooyour wystąpień maszyn wirtualnych w sieci wirtualnej. Grupy NSG można kojarzyć z podsieciami lub poszczególnymi wystąpieniami maszyn wirtualnych w danej podsieci. Gdy grupa NSG jest skojarzona z podsiecią, reguły listy ACL hello zastosować wystąpień maszyn wirtualnych hello tooall w tej podsieci.
W celu hello tych wskazówek, utworzymy dwie grupy NSG: jeden dla każdej sieci wewnętrznej i strefą DMZ. Zostaną one odpowiednio oznaczone: NSG_INT i NSG_DMZ.

![Tworzenie sieciowej grupy zabezpieczeń](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

Po hello grupa NSG jest tworzona zostaną 0 reguł ruchu przychodzącego i 0 dla ruchu wychodzącego. Po zainstalowaniu i funkcjonalności hello ról na odpowiednich serwerach hello, następnie hello reguły ruchu przychodzącego i wychodzącego może się zgodnie z toohello żądany poziom zabezpieczeń.

![Inicjowanie sieciowej grupy zabezpieczeń](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

Po utworzeniu hello grupy NSG z podsiecią skojarzyć NSG_INT INT i NSG_DMZ z podsiecią DMZ. Poniżej znajduje się przykładowy zrzut ekranu:

![Konfigurowanie sieciowej grupy zabezpieczeń](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* Kliknij panel hello tooopen podsieci dla podsieci
* Wybierz hello tooassociate podsieci z hello NSG 

Po przeprowadzeniu konfiguracji panel hello podsieci powinna wyglądać poniżej:

![Podsieci skojarzone z sieciową grupą zabezpieczeń](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

**1.3. Tworzenie tooon połączenia lokalnego**

Potrzebujemy połączenia tooon lokalnie w kolejności toodeploy hello kontrolera domeny (DC) na platformie azure. System Azure oferuje różne tooconnect opcji łączności sieci tooyour infrastruktury lokalnej infrastruktury platformy Azure.

* Punkt-lokacja
* Lokacja-lokacja w sieci wirtualnej
* ExpressRoute

Zalecane jest toouse ExpressRoute. Usługa ExpressRoute umożliwia tworzenie prywatnych połączeń między centrami danych Azure i infrastrukturą lokalną lub wspólnym środowiskiem. Połączenia ExpressRoute nie został przekroczony hello publicznej sieci Internet. Oferują więcej niezawodności, szybkości szybsze, niższe opóźnienia i lepsze zabezpieczenia niż typowe połączenia za pośrednictwem hello Internet.
Zalecane jest toouse ExpressRoute, można dowolną metodę połączenia najodpowiedniejsza dla Twojej organizacji. więcej informacji na temat usługi ExpressRoute i hello toolearn różnych opcji łączności za pomocą usługi ExpressRoute, przeczytaj [opis techniczny ExpressRoute](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Tworzenie kont magazynu
W kolejności toomaintain wysokiej dostępności i uniknąć zależność od konta magazynu jednego, możesz utworzyć dwa konta magazynu. Podzielić na dwie grupy hello maszyny w każdym zestawie dostępności, a następnie przypisz każdej grupy oddzielnego konta magazynu.

![Tworzenie kont magazynu](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Tworzenie zestawów dostępności
Dla każdej roli (DC/AD FS i WAP) Utwórz zestawy dostępności, zawierające 2 maszyn na powitania minimalnej. Pozwoli to osiągnąć większą dostępność poszczególnych ról. Podczas tworzenia dostępności hello zestawy, jest ważne toodecide powitania po:

* **Odporność domen**: maszyny wirtualne w hello samego udziału domeny błędów hello tego samego źródła zasilania i fizyczny przełącznik sieciowy. Zaleca się korzystanie co najmniej z 2 domen błędów. Witaj, wartością domyślną jest 3 i można pozostawić go jako jest hello w celu tego wdrożenia
* **Aktualizowanie domeny**: komputerów należących do tej samej domenie aktualizacji są ponownie uruchamiane razem podczas aktualizacji toohello. Ma toohave co najmniej 2 domen aktualizacji. Hello domyślna wartość to 5 i pozostawić jest hello w celu tego wdrożenia

![Zestawy dostępności](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

Utwórz hello następujących zestawów dostępności

| Zestaw dostępności | Rola | Domeny błędów | Domeny aktualizacji |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Wdrażanie maszyn wirtualnych
Witaj następnym krokiem jest toodeploy maszyn wirtualnych, które będą obsługiwać hello różnych ról w ramach infrastruktury. Zaleca się wdrożenie co najmniej dwóch maszyn w każdym zestawie dostępności. Utwórz cztery maszyny wirtualne dla podstawowego wdrożenia hello.

| Maszyna | Rola | Podsieć | Zestaw dostępności | Konto magazynu | Adres IP |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |Statyczny |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |Statyczny |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |Statyczny |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |Statyczny |

Warto zauważyć, że nie określono sieciowej grupy zabezpieczeń. Jest to spowodowane azure umożliwia używanie grupy NSG na poziomie podsieci hello. Następnie ruchu sieciowego maszyny można kontrolować przy użyciu powitalne poszczególnych NSG skojarzone z albo hello podsieci w przeciwnym razie obiekt NIC hello. Więcej informacji można znaleźć w artykule [Co to jest grupa zabezpieczeń sieci](https://aka.ms/Azure/NSG)
Statyczny adres IP jest zalecane, jeśli zarządzasz hello DNS. Można użyć usługi Azure DNS i zamiast tego w hello rekordy DNS dla domeny, można znaleźć toohello nowych maszyn przy użyciu ich nazw FQDN Azure.
Okienko sieci maszyny wirtualnej powinna wyglądać poniżej po zakończeniu wdrożenia hello:

![Wdrożone maszyny wirtualne](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-hello-domain-controller--ad-fs-servers"></a>5. Konfigurowanie kontrolera domeny hello / serwerów usług AD FS
 W kolejności tooauthenticate przychodzącego żądania, usługi AD FS należy kontrolera domeny hello toocontact. toosave hello kosztownych podróży z kontrolera domeny lokalnej tooon Azure do uwierzytelniania, zalecane jest toodeploy repliki kontrolera domeny hello na platformie Azure. W kolejności tooattain wysokiej dostępności zalecane jest toocreate zestawu dostępności co najmniej 2 kontrolery.

| Kontroler domeny | Rola | Konto magazynu |
|:---:|:---:|:---:|
| contosodc1 |Replika |contososac1 |
| contosodc2 |Replika |contososac2 |

* Podwyższ poziom hello dwa serwery jako replik kontrolerów domeny z systemem DNS
* Konfigurowanie serwerów hello usług AD FS, instalując rolę hello usług AD FS za pomocą Menedżera serwera hello.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. Wdrażanie wewnętrznego modułu równoważenia obciążenia (ILB)
**6.1. Utwórz hello ILB**

toodeploy ILB, wybierz opcję usługi równoważenia obciążenia w hello portalu Azure i kliknij przycisk Dodaj (+).

> [!NOTE]
> Jeśli nie widzisz **usługi równoważenia obciążenia** w menu, kliknij przycisk **Przeglądaj** w hello lewy portalu hello dolny i przewiń **usługi równoważenia obciążenia**.  Następnie kliknij przycisk hello żółtą gwiazdkę tooadd on tooyour menu. Teraz wybierz hello nowej konfiguracji usługi równoważenia obciążenia ikona tooopen hello panelu toobegin hello usługi równoważenia obciążenia.
> 
> 

![Przeglądanie modułu równoważenia obciążenia](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* **Nazwa**: zapewniają każdą odpowiednią nazwę równoważenia obciążenia toohello
* **Schemat**: ponieważ ten moduł równoważenia obciążenia zostaną umieszczone przed serwerów hello usług AD FS i jest przeznaczony dla połączeń sieci wewnętrznej, wybierz "Internal"
* **Sieć wirtualna**: Wybierz sieć wirtualną hello wybranej do wdrożenia usługi AD FS
* **Podsieci**: Wybierz hello tutaj podsieci wewnętrznej
* **Przypisanie adresu IP**: Statyczne

![Wewnętrzny moduł równoważenia obciążenia](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

Po kliknięciu przycisku tworzenia i wdrażania hello ILB, powinny pojawić się ona na liście hello usługi równoważenia obciążenia:

![Moduły równoważenia obciążenia po skonfigurowaniu wewnętrznego modułu równoważenia obciążenia](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

Następnym krokiem jest tooconfigure hello puli zaplecza i hello badania wewnętrznej bazy danych.

**6.2. Konfigurowanie puli zaplecza wewnętrznego modułu równoważenia obciążenia**

Witaj wybierz nowo utworzony ILB w hello panelu usługi równoważenia obciążenia. Zostanie otwarty panel ustawień hello. 

1. Wybierz pule zaplecza w Panelu ustawień hello
2. W hello dodać panelu puli wewnętrznej bazy danych, kliknij polecenie Dodaj maszynę wirtualną
3. Zostanie wyświetlony panel umożliwiający wybranie zestawu dostępności
4. Wybierz zestaw dostępności hello usług AD FS

![Konfigurowanie puli zaplecza wewnętrznego modułu równoważenia obciążenia](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

**6.3. Konfigurowanie sondy**

W Panelu ustawień ILB hello wybierz sondy.

1. Kliknij pozycję Dodaj.
2. Podaj szczegóły sondy a. **Nazwa**: nazwa sondy b. **Protokół**: TCP c. **Port**: 443 (HTTPS) d. **Interwał**: 5 (wartość domyślna) — jest to interwał powitania jaką ILB będzie sondowania hello maszyn w puli zaplecza hello e. **Próg złej kondycji limit**: 2 (domyślna val ue) — jest to hello próg kolejnych niepowodzeń sondy po upływie których ILB deklaracją maszynę w hello zaplecza puli przestanie odpowiadać i zatrzymano wysyłanie ruchu tooit.

![Konfigurowanie sondy wewnętrznego modułu równoważenia obciążenia](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

**6.4. Tworzenie reguł równoważenia obciążenia**

W kolejności tooeffectively równoważenie hello ruchu hello ILB należy skonfigurować reguły równoważenia obciążenia. W kolejności toocreate regułę równoważenia obciążenia 

1. Wybierz regułę z panelu Ustawienia hello hello ILB równoważenia obciążenia
2. Panel reguły równoważenia obciążenia, kliknij pozycję Dodaj w hello
3. Hello Dodaj załadować równoważenia panelu reguły. **Nazwa**: Podaj nazwę dla reguły hello b. **Protokół**: wybierz opcję TCP c. **Port**: 443 d. **Port zaplecza**: 443 e. **Puli zaplecza**: Wybierz pulę powitania dla hello usług AD FS klastra f wcześniej utworzono. **Sonda**: sondowanie hello wybierz wcześniej utworzony dla serwerów usług AD FS

![Konfigurowanie reguł wewnętrznego modułu równoważenia obciążenia](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

**6.5. Aktualizowanie systemu DNS o dane wewnętrznego modułu równoważenia obciążenia**

Przejdź tooyour serwera DNS i utworzyć rekord CNAME dla hello ILB. Witaj CNAME powinien być dla usługi federacyjnej hello o adresie IP hello wskazuje adres IP toohello hello ILB. Na przykład jeśli adres ILB DIP hello jest 10.3.0.8 i zainstalowana usługa federacyjna hello jest fs.contoso.com, następnie utworzyć rekord CNAME dla wskazanie too10.3.0.8 fs.contoso.com.
Daje to pewność, że wszystkie komunikacji dotyczące Zakończ fs.contoso.com się na powitania ILB i są odpowiednio kierowane.

### <a name="7-configuring-hello-web-application-proxy-server"></a>7. Konfigurowanie serwera Proxy aplikacji sieci Web hello
**7.1. Konfigurowanie serwerów na powitania serwera Proxy aplikacji sieci Web serwerów tooreach AD FS**

W kolejności tooensure czy serwery Proxy aplikacji sieci Web są serwery usług AD FS hello stanie tooreach za hello ILB należy utworzyć rekord w hello %systemroot%\system32\drivers\etc\hosts dla hello ILB. Należy pamiętać, że hello nazwa wyróżniająca (DN) powinna być nazwą usługi federacyjnej hello, na przykład fs.contoso.com. I wpis IP hello powinno być hello ILB adresu IP (10.3.0.8 co w przykładzie hello).

**7.2. Instalowanie roli serwera Proxy aplikacji sieci Web hello**

Po upewnieniu się, że serwery Proxy aplikacji sieci Web są serwery usług AD FS hello stanie tooreach za ILB, można zainstalować obok hello serwerów Proxy aplikacji sieci Web. Serwery Proxy aplikacji sieci Web nie może być toohello przyłączone do domeny. Zainstalować role serwera Proxy aplikacji sieci Web hello na powitania dwóch serwerów Proxy aplikacji sieci Web, wybierając hello roli dostępu zdalnego. Menedżer serwera Hello przeprowadzi toocomplete hello WAP instalacji.
Aby uzyskać więcej informacji na temat toodeploy WAP, przeczytaj [zainstalować i skonfigurować serwer Proxy aplikacji sieci Web hello](https://technet.microsoft.com/library/dn383662.aspx).

### <a name="8--deploying-hello-internet-facing-public-load-balancer"></a>8.  Wdrażanie hello Internet ukierunkowane (publicznej) usługi równoważenia obciążenia
**8.1.  Tworzenie modułu równoważenia obciążenia połączonego z Internetem (publicznego)**

W portalu Azure hello wybierz usługi równoważenia obciążenia, a następnie kliknij polecenie Dodaj. W panelu usługi równoważenia obciążenia Utwórz hello wprowadź hello następujących informacji

1. **Nazwa**: nazwa dla usługi równoważenia obciążenia hello
2. **Schemat**: opcja Publiczny informuje platformę Azure, że ten moduł równoważenia obciążenia musi mieć adres publiczny.
3. **Adres IP**: utwórz nowy adres IP (dynamiczny).

![Moduł równoważenia obciążenia połączony z Internetem](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

Po wdrożeniu usługi równoważenia obciążenia hello pojawi się na liście modułów równoważenia obciążenia hello.

![Lista modułów równoważenia obciążenia](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

**8.2. Przypisz DNS etykiety toohello publicznego adresu IP**

Polecenie wpisu usługi równoważenia obciążenia hello nowo utworzony w hello obciążenia równoważenia panelu toobring się panelu hello konfiguracji. Wykonaj poniżej Etykieta DNS hello tooconfigure kroki hello publicznego adresu IP:

1. Polecenie hello publicznego adresu IP. Spowoduje to otwarcie panelu hello hello publicznego adresu IP i jego ustawień
2. Kliknij pozycję Konfiguracja.
3. Podaj etykietę DNS. Będzie to hello publicznego Etykieta DNS której będziesz mieć dostęp z dowolnego miejsca, na przykład contosofs.westus.cloudapp.azure.com. Można dodać wpisu w hello (contosofs.westus.cloudapp.azure.com) w moduł równoważenia obciążenia zewnętrznego serwera DNS dla usługi federacyjnej hello (na przykład fs.contoso.com), który jest rozpoznawany jako etykieta DNS toohello hello zewnętrznych.

![Konfigurowanie modułu równoważenia obciążenia połączonego z Internetem](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![Konfigurowanie modułu równoważenia obciążenia połączonego z Internetem (DNS)](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

**8.3. Konfigurowanie puli zaplecza dla modułu równoważenia obciążenia połączonego z** Internetem (publicznego) 

Witaj wykonaj kroki takie same jak tworzenie hello wewnętrznego modułu równoważenia obciążenia, ustawić puli zaplecza hello tooconfigure dla Internetu ukierunkowane (publicznej) moduł równoważenia obciążenia jako hello dostępności dla serwerów proxy hello. .

![Konfigurowanie puli zaplecza modułu równoważenia obciążenia połączonego z Internetem](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

**8.4. Konfigurowanie sondy**

Wykonaj kroki takie same jak konfigurowanie sondę modułu równoważenia obciążenia wewnętrznego hello hello tooconfigure hello puli wewnętrznej bazy danych z serwerów proxy hello.

![Konfigurowanie sondy modułu równoważenia obciążenia połączonego z Internetem](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

**8.5. Tworzenie reguł równoważenia obciążenia**

Wykonaj te same czynności, jak Równoważenie obciążenia hello tooconfigure ILB reguły dla TCP 443 hello.

![Konfigurowanie reguł modułu równoważenia obciążenia połączonego z Internetem](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-hello-network"></a>9. Zabezpieczanie hello sieci
**9.1. Zabezpieczanie hello wewnętrzna podsieć.**

Ogólnie należy hello reguły tooefficiently secure podsieć wewnętrznych (w kolejności hello wymienione poniżej)

| Reguła | Opis | Ruch |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Zezwalaj na komunikację HTTPS hello ze strefą DMZ |Przychodzący |
| DenyInternetOutbound |Nie toointernet dostępu |Wychodzący |

![Reguły dostępu WEWN. (ruch przychodzący)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

[komentarz]: <> (![reguły dostępu WEWN. (ruch przychodzący)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [komentarz]: <> (![reguły dostępu WEWN. (ruch wychodzący)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))

**9.2. Zabezpieczanie hello DMZ podsieci**

| Reguła | Opis | Ruch |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |Zezwalaj na HTTPS z Internetu toohello DMZ |Przychodzący |
| DenyInternetOutbound |Jakikolwiek inny niż HTTPS toointernet jest zablokowana |Wychodzący |

![Reguły dostępu ZEWN. (ruch przychodzący)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

[komentarz]: <> (![reguły dostępu ZEWN. (ruch przychodzący)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [komentarz]: <> (![reguły dostępu ZEWN. (ruch wychodzący)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))

> [!NOTE]
> Jeśli jest wymagane uwierzytelnianie certyfikatu klienta użytkownika (uwierzytelnianie usługi ClientTLS przy użyciu certyfikatów użytkownika X509), port TCP 49443 musi być włączony dla połączeń przychodzących z usługami AD FS.
> 
> 

### <a name="10-test-hello-ad-fs-sign-in"></a>10. Testowanie logowania hello usług AD FS
Witaj Najprostszym sposobem jest tootest usług AD FS jest przy użyciu hello IdpInitiatedSignon.aspx strony. W kolejności toobe toodo możliwe, że jest wymagane tooenable hello IdpInitiatedSignOn właściwości hello usług AD FS. Wykonaj kroki hello poniżej tooverify konfigurację usług AD FS

1. Uruchom hello poniżej polecenia cmdlet na powitania AD FS serwera przy użyciu programu PowerShell, tooset go tooenabled.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. Przy użyciu dowolnej maszyny zewnętrznej otwórz stronę https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx  
3. Powinna zostać wyświetlona strona hello usług AD FS, takich jak poniżej:

![Testowa strona logowania](./media/active-directory-aadconnect-azure-adfs/test1.png)

Po pomyślnym zalogowaniu zostanie wyświetlony poniższy komunikat:

![Test zakończony powodzeniem](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Szablon na potrzeby wdrażania usług AD FS na platformie Azure
Szablon Hello wdraża ustawienia 6 maszyny, 2 dla kontrolerów domeny, usługi AD FS i WAP.

[Usługi AD FS w szablonie wdrażania platformy Azure](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Podczas wdrażania tego szablonu możesz użyć istniejącej sieci wirtualnej lub utworzyć nową. powitalne różnych parametrów umożliwiających dostosowywanie wdrożenia hello poniżej przedstawiono opis hello użycie parametru hello w procesie wdrażania hello. 

| Parametr | Opis |
|:--- |:--- |
| Lokalizacja |Witaj region toodeploy hello zasoby do, np. wschodnie stany USA. |
| StorageAccountType |Typ Hello hello utworzono konto magazynu |
| VirtualNetworkUsage |Wskazuje, czy zostanie utworzona nowa sieć wirtualna, czy użyta istniejąca. |
| VirtualNetworkName |Nazwa Hello hello tooCreate sieci wirtualnej, obowiązkowa w przypadku zarówno istniejącego lub nowego użycia sieci wirtualnej |
| VirtualNetworkResourceGroupName |Określa nazwę hello hello zasobów grupy zawierającej hello istniejącej sieci wirtualnej. Podczas korzystania z istniejącej sieci wirtualnej, staje się on to parametr obowiązkowy, hello wdrożenia można znaleźć hello identyfikator hello istniejącej sieci wirtualnej |
| VirtualNetworkAddressRange |Witaj zakresu adresów hello nowej sieci Wirtualnej, obowiązkowa w przypadku tworzenia nowej sieci wirtualnej |
| InternalSubnetName |Nazwa Hello hello wewnętrzna podsieć, obowiązkowa w przypadku obu opcji użycia sieci wirtualnej (Nowa lub istniejąca) |
| InternalSubnetAddressRange |Hello zakres adresów podsieci wewnętrznej hello, który zawiera hello kontrolerów domen i usług AD FS serwery, wymagane w przypadku tworzenia nowej sieci wirtualnej. |
| DMZSubnetAddressRange |Witaj zakres adresów podsieci dmz hello, który zawiera hello Windows serwery proxy aplikacji, wymagane, jeśli Tworzenie nowej sieci wirtualnej. |
| DMZSubnetName |Nazwa Hello hello wewnętrzna podsieć, obowiązkowa w przypadku obu opcji użycia sieci wirtualnej (Nowa lub istniejąca). |
| ADDC01NICIPAddress |Witaj wewnętrzny adres IP hello pierwszego kontrolera domeny, ten adres IP zostaną statycznie przypisane toohello kontrolera domeny i musi być prawidłowy adres ip w podsieci wewnętrznej hello |
| ADDC02NICIPAddress |Witaj wewnętrzny adres IP hello kontrolera domeny, ten adres IP zostaną statycznie przypisane toohello kontrolera domeny i musi być prawidłowy adres ip w podsieci wewnętrznej hello |
| ADFS01NICIPAddress |Hello wewnętrzny adres IP pierwszego serwera usług AD FS hello, ten adres IP zostaną statycznie przypisane toohello serwera usług AD FS, a musi być prawidłowy adres ip w podsieci wewnętrznej hello |
| ADFS02NICIPAddress |Hello wewnętrzny adres IP hello drugiego serwera usług AD FS, ten adres IP zostaną statycznie przypisane toohello serwera usług AD FS, a musi być prawidłowy adres ip w podsieci wewnętrznej hello |
| WAP01NICIPAddress |Witaj wewnętrzny adres IP pierwszego serwera proxy hello, ten adres IP zostaną statycznie przypisane toohello serwerowi proxy aplikacji, musi być prawidłowy adres ip w podsieci DMZ hello |
| WAP02NICIPAddress |Hello wewnętrzny adres IP hello drugi serwer proxy, zostaną statycznie przypisane serwerowi toohello ten adres IP i musi być prawidłowy adres ip w podsieci DMZ hello |
| ADFSLoadBalancerPrivateIPAddress |Moduł równoważenia obciążenia Hello wewnętrzny adres IP hello usług AD FS, ten adres IP zostaną statycznie przypisane toohello modułu równoważenia obciążenia, a musi być prawidłowy adres ip w podsieci wewnętrznej hello |
| ADDCVMNamePrefix |Prefiks nazwy maszyny wirtualnej dla kontrolerów domeny. |
| ADFSVMNamePrefix |Prefiks nazwy maszyny wirtualnej dla serwerów usług ADFS. |
| WAPVMNamePrefix |Prefiks nazwy maszyny wirtualnej dla serwerów proxy aplikacji sieci Web. |
| ADDCVMSize |rozmiar maszyny wirtualnej Hello hello kontrolerów domeny |
| ADFSVMSize |rozmiar maszyny wirtualnej Hello hello serwerów usług AD FS |
| WAPVMSize |rozmiar maszyny wirtualnej Hello hello serwerów proxy |
| AdminUserName |Nazwa Hello hello administratora lokalnego hello maszyn wirtualnych |
| AdminPassword |Hello hasło dla konta lokalnego administratora hello hello maszyn wirtualnych |

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Zestawy dostępności](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [Wewnętrzne równoważenie obciążenia](https://aka.ms/Azure/ILB/Internal).
* [Moduł równoważenia obciążenia połączony z Internetem](https://aka.ms/Azure/ILB/Internet)
* [Konta magazynu](https://aka.ms/Azure/Storage)
* [Sieci wirtualne platformy Azure](https://aka.ms/Azure/VNet)
* [Linki prowadzące do informacji dotyczących usług AD FS i serwera proxy aplikacji sieci Web](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Następne kroki
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
* [Konfigurowanie usług AD FS i zarządzanie nimi za pomocą programu Azure AD Connect](active-directory-aadconnectfed-whatis.md)
* [Wdrażanie geograficznie rozproszonych usług AD FS o wysokiej dostępności na platformie Azure przy użyciu usługi Azure Traffic Manager](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

