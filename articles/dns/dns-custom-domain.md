---
title: "aaaIntegrate usługi Azure DNS z zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse usługi Azure DNS wzdłuż tooprovide DNS dla zasobów platformy Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>Użyj ustawień domeny niestandardowej tooprovide usługi Azure DNS dla usługi Azure

Usługa DNS platformy Azure udostępnia DNS dla domeny niestandardowej dla każdego z zasobów platformy Azure czy obsługa domen niestandardowych lub które mają w pełni kwalifikowaną nazwą domeny (FQDN). Przykładem jest aplikacja sieci web platformy Azure i mają tooaccess Twojego użytkowników albo jej przy użyciu contoso.com lub www.contoso.com jako nazwy FQDN. W tym artykule przedstawiono konfigurowanie usługi Azure przy użyciu usługi Azure DNS dotyczące korzystania z niestandardowej domeny.

## <a name="prerequisites"></a>Wymagania wstępne

W kolejności toouse usługi Azure DNS dla domeny niestandardowej należy najpierw przekazać tooAzure Twojego domeny DNS. Odwiedź stronę [delegować tooAzure domeny DNS](./dns-delegate-domain-azure-dns.md) instrukcje na temat tooconfigure serwerów nazw dla delegowania. Po Twoja domena to tooyour delegowanej strefy DNS platformy Azure, są się rekordy DNS hello stanie tooconfigure niezbędne.

Można skonfigurować niestandardowych lub domeny niestandardowej dla [aplikacji funkcji Azure](#azure-function-app), [Azure IoT](#azure-iot), [publicznego adresu IP, adresy](#public-ip-address), [usługi aplikacji (aplikacje sieci Web)](#app-service-web-apps), [magazynu obiektów Blob](#blob-storage), i [Azure CDN](#azure-cdn).

## <a name="azure-function-app"></a>Aplikacji Azure — funkcja

tooconfigure domeny niestandardowej dla aplikacji funkcja Azure oraz konfigurację na powitania funkcja aplikacja zostaje utworzony rekord CNAME.
 
Przejdź za**innych** > **aplikacji funkcji** i wybierz aplikację funkcji. Kliknij przycisk **funkcji platformy** i w obszarze **sieci** kliknij **domen niestandardowych**.

![Funkcja bloku aplikacji](./media/dns-custom-domain/functionapp.png)

Należy zwrócić uwagę hello bieżący adres url na powitania **domen niestandardowych** bloku, ten adres jest używana jako hello alias hello rekord DNS utworzony.

![Blok domeny niestandardowej](./media/dns-custom-domain/functionshostname.png)

Przejdź tooyour strefę DNS, a następnie kliknij przycisk **+ zestawu rekordów**. Wypełnij następujące informacje na powitania hello **dodać zestaw rekordów** bloku i kliknij przycisk **OK** toocreate go.

|Właściwość  |Wartość  |Opis  |
|---------|---------|---------|
|Nazwa     | myfunctionapp        | Ta wartość wraz z etykieta nazwy domeny hello jest hello nazwy FQDN dla hello niestandardowej nazwy domeny.        |
|Typ     | CNAME        | Użyj rekord CNAME jest za pomocą aliasu.        |
|CZAS WYGAŚNIĘCIA     | 1        | 1 jest używany przez godzinę        |
|Czas wygaśnięcia jednostki     | Godziny        | Godziny są używane jako hello pomiar czasu         |
|Alias     | adatumfunction.azurewebsites.NET        | Nazwa DNS Hello powoduje utworzenie hello alias, w tym przykładzie jest nazwa DNS adatumfunction.azurewebsites.net hello udostępniane przez domyślny toohello funkcji aplikacji.        |

Przejdź wstecz tooyour funkcji aplikacji, kliknij pozycję **funkcji platformy**, a następnie w obszarze **sieci** kliknij **domen niestandardowych**, następnie w obszarze **Hostnames**kliknij **+ Dodaj hostname**.

Na powitania **dodać nazwę hosta** bloku, wprowadź hello rekord CNAME w hello **hostname** pole tekstowe, kliknij przycisk **weryfikacji**. Jeśli rekord hello toobe można znaleźć, hello **dodać nazwę hosta** pojawi się przycisk. Kliknij przycisk **dodać nazwę hosta** tooadd hello alias.

![host name blok dodawania aplikacji funkcji](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>Azure IoT

Azure IoT nie ma żadnych dostosowania, które są wymagane na powitania samej usługi. toouse domeny niestandardowej z Centrum IoT wymagany jest tylko do rekordu CNAME wskazywana toohello zasobów.

Przejdź za**Internetu rzeczy** > **Centrum IoT** i wybierz pozycję Centrum IoT. Na powitania **omówienie** bloku hello Uwaga FQDN hello Centrum IoT.

![Blok centrum IoT](./media/dns-custom-domain/iot.png)

Następnie przejdź tooyour strefy DNS i kliknij przycisk **+ zestawu rekordów**. Wypełnij następujące informacje na powitania hello **dodać zestaw rekordów** bloku i kliknij przycisk **OK** toocreate go.


|Właściwość  |Wartość  |Opis  |
|---------|---------|---------|
|Nazwa     | myiothub        | Ta wartość wraz z etykieta nazwy domeny hello jest hello nazwy FQDN dla hello Centrum IoT.        |
|Typ     | CNAME        | Użyj rekord CNAME jest za pomocą aliasu.
|CZAS WYGAŚNIĘCIA     | 1        | 1 jest używany przez godzinę        |
|Czas wygaśnięcia jednostki     | Godziny        | Godziny są używane jako hello pomiar czasu         |
|Alias     | adatumIOT.azure devices.net        | Nazwa DNS Hello powoduje utworzenie aliasu hello, w tym przykładzie jest nazwa hosta adatumIOT.azure devices.net hello udostępniane przez Centrum IoT hello.

Po utworzeniu rekordu hello przetestowanie rozpoznawania nazw przy użyciu rekordu CNAME hello`nslookup`

## <a name="public-ip-address"></a>Publiczny adres IP

tooconfigure niestandardową domenę na potrzeby usług korzystających z publicznym adresem IP adresów zasobów, takich jak bramy aplikacji, usługi równoważenia obciążenia, usługi w chmurze maszyn wirtualnych Menedżera zasobów, i klasycznych maszyn wirtualnych, rekord CNAME jest używany.

Przejdź za**sieci** > **publicznego adresu IP**, wybierz zasób publicznego adresu IP hello i kliknij przycisk **konfiguracji**. Zapisania hello adres IP wyświetlany.

![Blok publicznego adresu ip](./media/dns-custom-domain/publicip.png)

Przejdź tooyour strefę DNS, a następnie kliknij przycisk **+ zestawu rekordów**. Wypełnij następujące informacje na powitania hello **dodać zestaw rekordów** bloku i kliknij przycisk **OK** toocreate go.


|Właściwość  |Wartość  |Opis  |
|---------|---------|---------|
|Nazwa     | mywebserver        | Ta wartość wraz z etykieta nazwy domeny hello jest hello nazwy FQDN dla hello niestandardowej nazwy domeny.        |
|Typ     | A        | Przy użyciu rekordu A jako zasób hello jest adres IP.        |
|CZAS WYGAŚNIĘCIA     | 1        | 1 jest używany przez godzinę        |
|Czas wygaśnięcia jednostki     | Godziny        | Godziny są używane jako hello pomiar czasu         |
|Adres IP     | <your ip address>       | Witaj publicznego adresu IP.|

![Utwórz rekord a.](./media/dns-custom-domain/arecord.png)

Po utworzeniu rekordu hello A uruchom `nslookup` rozpoznaje toovalidate hello rekordu.

![wyszukiwania dns publicznego adresu ip](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>Usługi aplikacji (aplikacje sieci Web)

Witaj poniższe kroki przedstawiają skonfigurowanie domeny niestandardowej dla aplikacji sieci web usługi aplikacji.

Przejdź za**sieci Web i mobilnych** > **usługi aplikacji** i wybierz zasób hello są Konfigurowanie niestandardowej nazwy domeny i kliknij przycisk **domen niestandardowych**.

Należy zwrócić uwagę hello bieżący adres url na powitania **domen niestandardowych** bloku, ten adres jest używana jako hello alias hello rekord DNS utworzony.

![domen niestandardowych bloku](./media/dns-custom-domain/url.png)

Przejdź tooyour strefę DNS, a następnie kliknij przycisk **+ zestawu rekordów**. Wypełnij następujące informacje na powitania hello **dodać zestaw rekordów** bloku i kliknij przycisk **OK** toocreate go.


|Właściwość  |Wartość  |Opis  |
|---------|---------|---------|
|Nazwa     | mywebserver        | Ta wartość wraz z etykieta nazwy domeny hello jest hello nazwy FQDN dla hello niestandardowej nazwy domeny.        |
|Typ     | CNAME        | Użyj rekord CNAME jest za pomocą aliasu. Jeśli zasób hello jest używany adres IP, mogą być wykorzystane rekord A.        |
|CZAS WYGAŚNIĘCIA     | 1        | 1 jest używany przez godzinę        |
|Czas wygaśnięcia jednostki     | Godziny        | Godziny są używane jako hello pomiar czasu         |
|Alias     | WebServer.azurewebsites.NET        | Nazwa DNS Hello powoduje utworzenie aliasu hello, w tym przykładzie nazwa DNS webserver.azurewebsites.net hello dostarczone przez aplikację sieci web toohello domyślny nie jest.        |


![Utwórz rekord CNAME](./media/dns-custom-domain/createcnamerecord.png)

Przejdź wstecz toohello app service jest skonfigurowany dla hello niestandardowej nazwy domeny. Kliknij przycisk **domen niestandardowych**, następnie kliknij przycisk **Hostnames**. Kliknij pozycję utworzony rekord CNAME hello tooadd **+ Dodaj hostname**.

![rysunek 1](./media/dns-custom-domain/figure1.png)

Po zakończeniu procesu hello uruchomić **nslookup** toovalidate rozpoznawania nazw działa.

![rysunek 1](./media/dns-custom-domain/finalnslookup.png)

toolearn więcej informacji na temat mapowania tooApp domeny niestandardowej usługi, odwiedź stronę [mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacje sieci Web](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).

Toopurchase niestandardową domenę, należy odwiedzić [kupić niestandardowej nazwy domeny dla aplikacji sieci Web Azure](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn więcej informacji na temat domen z usługi aplikacji.

## <a name="blob-storage"></a>Blob Storage

Witaj poniższe kroki przedstawiają Konfigurowanie rekord CNAME dla konta magazynu obiektów blob przy użyciu metody asverify hello. Ta metoda gwarantuje, że nie istnieje bez przestojów.

Przejdź za**magazynu** > **kont magazynu**, wybierz konto magazynu i kliknij przycisk **domeny niestandardowe**. Zapisania hello nazwy FQDN w kroku 2, ta wartość jest używana toocreate hello pierwszy rekord CNAME

![domeny niestandardowej magazynu obiektów blob](./media/dns-custom-domain/blobcustomdomain.png)

Przejdź tooyour strefę DNS, a następnie kliknij przycisk **+ zestawu rekordów**. Wypełnij następujące informacje na powitania hello **dodać zestaw rekordów** bloku i kliknij przycisk **OK** toocreate go.


|Właściwość  |Wartość  |Opis  |
|---------|---------|---------|
|Nazwa     | asverify.mystorageaccount        | Ta wartość wraz z etykieta nazwy domeny hello jest hello nazwy FQDN dla hello niestandardowej nazwy domeny.        |
|Typ     | CNAME        | Użyj rekord CNAME jest za pomocą aliasu.        |
|CZAS WYGAŚNIĘCIA     | 1        | 1 jest używany przez godzinę        |
|Czas wygaśnięcia jednostki     | Godziny        | Godziny są używane jako hello pomiar czasu         |
|Alias     | asverify.adatumfunctiona9ed.blob.Core.Windows.NET        | Nazwa DNS Hello powoduje utworzenie aliasu hello, w tym przykładzie jest nazwa DNS asverify.adatumfunctiona9ed.blob.core.windows.net hello udostępniane przez domyślne konto magazynu toohello.        |

Przejdź wstecz tooyour konta magazynu, klikając **magazynu** > **kont magazynu**, wybierz konto magazynu i kliknij przycisk **domeny niestandardowe**. Wpisz alias został utworzony bez prefiksu asverify hello w polu tekstowym hello wyboru hello ** Użyj pośredniej weryfikacji CNAME, a następnie kliknij przycisk **zapisać**. Po wykonaniu tego kroku zwracać tooyour strefy DNS i utworzyć rekord CNAME, bez prefiksu asverify hello.  Po tym etapie jest rekord CNAME hello bezpieczne toodelete z prefiksem cdnverify hello.

![domeny niestandardowej magazynu obiektów blob](./media/dns-custom-domain/indirectvalidate.png)

Sprawdź poprawność rozpoznawania nazw DNS, uruchamiając`nslookup`

więcej informacji na temat mapowania punktu końcowego magazynu obiektów blob tooa domen niestandardowych można znaleźć toolearn [Konfigurowanie niestandardowej nazwy domeny dla punktu końcowego magazynu obiektów Blob](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>Usługa Azure CDN

Witaj poniższe kroki przedstawiają Konfigurowanie rekord CNAME dla punktu końcowego usługi CDN przy użyciu metody cdnverify hello. Ta metoda gwarantuje, że nie istnieje bez przestojów.

Przejdź za**sieci** > **profilów usługi CDN**, a następnie wybierz profil CDN i kliknij przycisk **punkty końcowe** w obszarze **ogólne**.

Wybierz końcowy hello pracy z, kliknij przycisk **+ domeny niestandardowe**. Uwaga hello **hosta punktu końcowego** jako rekord hello jest ta wartość wskazuje hello rekordu CNAME.

![Domena niestandardowa CDN](./media/dns-custom-domain/endpointcustomdomain.png)

Przejdź tooyour strefę DNS, a następnie kliknij przycisk **+ zestawu rekordów**. Wypełnij następujące informacje na powitania hello **dodać zestaw rekordów** bloku i kliknij przycisk **OK** toocreate go.

|Właściwość  |Wartość  |Opis  |
|---------|---------|---------|
|Nazwa     | cdnverify.mycdnendpoint        | Ta wartość wraz z etykieta nazwy domeny hello jest hello nazwy FQDN dla hello niestandardowej nazwy domeny.        |
|Typ     | CNAME        | Użyj rekord CNAME jest za pomocą aliasu.        |
|CZAS WYGAŚNIĘCIA     | 1        | 1 jest używany przez godzinę        |
|Czas wygaśnięcia jednostki     | Godziny        | Godziny są używane jako hello pomiar czasu         |
|Alias     | cdnverify.adatumcdnendpoint.azureedge.NET        | Nazwa DNS Hello powoduje utworzenie aliasu hello, w tym przykładzie jest nazwa DNS cdnverify.adatumcdnendpoint.azureedge.net hello udostępniane przez domyślne konto magazynu toohello.        |

Przejdź wstecz tooyour punktu końcowego CDN, klikając **sieci** > **profilów usługi CDN**i wybierz profil CDN. Kliknij przycisk **+ domeny niestandardowe** i wprowadź aliasu rekordu CNAME bez prefiksu cdnverify hello i kliknij przycisk **Dodaj**.

Po wykonaniu tego kroku zwracać tooyour strefy DNS i utworzyć rekord CNAME, bez prefiksu cdnverify hello.  Po tym etapie jest rekord CNAME hello bezpieczne toodelete z prefiksem cdnverify hello. Aby uzyskać więcej informacji o sieci CDN i jak tooconfigure domeny niestandardowej bez hello rejestracji pośredniego kroku można znaleźć [domeny niestandardowej tooa zawartości mapy usługi Azure CDN](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za[skonfigurować wstecznego DNS dla usługi hostowanej na platformie Azure](dns-reverse-dns-for-azure-services.md).
