---
title: "aaaConfigure niestandardowej nazwy domeny usług w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooexpose Twojego Azure toohello aplikacji lub danych internet na domenę niestandardową, konfigurując ustawienia DNS.  Poniższe przykłady użycia hello portalu Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Konfigurowanie niestandardowej nazwy domeny dla usługi w chmurze Azure
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-custom-domain-name-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-custom-domain-name.md)
> 
> 

Podczas tworzenia usługi w chmurze Azure przypisuje go poddomeną tooa **cloudapp.net**. Na przykład, jeśli usługi w chmurze ma nazwę "contoso", użytkownicy będą się mogli tooaccess aplikacji przy użyciu adresu URL, takie jak http://contoso.cloudapp.net. Azure przypisuje wirtualny adres IP.

Jednak pozwala również udostępnić aplikacji na własną nazwę domeny, takie jak **contoso.com**. W tym artykule opisano sposób tooreserve lub skonfigurować niestandardową nazwę domeny dla ról sieci web usługi w chmurze.

Czy można już zrozumieć, jakie CNAME i są? [Skok poza wyjaśnienie hello](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> Witaj procedury w tym zadaniu mają zastosowanie tooAzure usługi w chmurze. Dla usług aplikacji, zobacz [to](../app-service-web/web-sites-custom-domain-name.md). W przypadku kont magazynu, zobacz [to](../storage/blobs/storage-custom-domain-name.md).
> 
> 

<p/>

> [!TIP]
> Pracuj szybciej--Użyj hello Azure nowe [z przewodnikiem wskazówki](http://support.microsoft.com/kb/2990804)!  Powoduje skojarzenie niestandardowej nazwy domeny i zabezpieczania komunikacji (SSL) z usług Azure Cloud Services lub witryny sieci Web Azure bardzo proste.
> 
> 

## <a name="understand-cname-and-a-records"></a>Zrozumienie rekordów CNAME i A
CNAME (lub rekordy aliasu) i rekordy zarówno pozwalają tooassociate nazwy domeny z określonego serwera (lub usługi, w tym przypadku) jednak one działać inaczej. Istnieją również kilka zagadnień, podczas korzystania z usługi w chmurze Azure, które należy wziąć pod uwagę przed podjęciem decyzji, które toouse rekordów.

### <a name="cname-or-alias-record"></a>Rekord CNAME lub Alias
Rekord CNAME mapuje *określonych* domeny, takie jak **contoso.com** lub **www.contoso.com**, tooa nazwa kanoniczna domeny. W takim przypadku nazwa kanoniczna domeny hello jest hello **.cloudapp [moja_aplikacja] .net** nazwy domeny platformy Azure hostowanej aplikacji. Po utworzeniu hello CNAME tworzy alias dla hello **.cloudapp [moja_aplikacja] .net**. Hello wpis CNAME rozwiąże adres IP toohello Twojego **.cloudapp [moja_aplikacja] .net** usługi automatycznie, więc jeśli zmieni adres IP hello hello usługi w chmurze, nie masz tootake żadnych działań.

> [!NOTE]
> Niektóre domeny rejestratorów tylko pozwalają poddomen toomap przy użyciu rekordu CNAME, np. www.contoso.com i nie nazwy głównych, np. contoso.com. Więcej informacji o rekordy CNAME, można znaleźć w dokumentacji hello przez rejestratora, [hello wpis Wikipedia rekordu CNAME](http://en.wikipedia.org/wiki/CNAME_record), lub hello [nazwy domen IETF - wdrażania i specyfikację](http://tools.ietf.org/html/rfc1035) dokument.
> 
> 

### <a name="a-record"></a>Rekord
*A* rekord mapuje domeny, takie jak **contoso.com** lub **www.contoso.com**, *lub domena symboli wieloznacznych* takich jak  **\*. contoso.com**, tooan adresu IP. W przypadku hello usługi w chmurze platformy Azure hello wirtualnego adresu IP hello usługi. Dlatego hello Największą zaletą rekord A za pośrednictwem rekordu CNAME jest, że może mieć jeden wpis, który używa symboli wieloznacznych, takich jak \* **. contoso.com**, który będzie obsługiwać żądania wielu domen podrzędnych takich jak  **mail.contoso.com**, **login.contoso.com**, lub **www.contso.com**.

> [!NOTE]
> Ponieważ rekord jest mapowany tooa statyczny adres IP, nie może automatycznie rozwiązać zmian adresu IP toohello usługi w chmurze. Witaj adres IP używany przez usługi w chmurze jest przydzielony hello po raz pierwszy wdrażanie tooan pustego gniazda (produkcyjnego lub przemieszczania.) Po usunięciu wdrożenia hello gniazda hello hello adres IP został wydany przez Azure i dowolnego miejsca toohello przyszłych wdrożeniach. należy podać nowy adres IP.
> 
> Wygodnie hello adres IP miejsca danego wdrożenia (środowisko produkcyjne lub tymczasowe) jest trwały podczas wymiany między przemieszczania i wdrożeń produkcyjnych lub uaktualnianie w miejscu istniejącego wdrożenia. Aby uzyskać więcej informacji dotyczących wykonywania tych akcji, zobacz [jak usługi w chmurze toomanage](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Dodaj rekord CNAME dla domeny niestandardowej
toocreate rekord CNAME, należy dodać nowy wpis w tabeli DNS powitania dla domeny niestandardowej przy użyciu narzędzi hello dostarczonych przez rejestratora. Każdy rejestrator ma podobne, lecz nieco inne metody określania rekord CNAME, ale hello są pojęcia hello takie same.

1. Użyj jednej z tych metod hello toofind **. cloudapp.net** przypisaną usługi w chmurze tooyour nazwę domeny.
   
   * Toohello logowania [portalu Azure], wybierz usługi w chmurze, obejrzyj hello **Essentials** sekcji, a następnie znajdź hello **adres URL witryny** wpisu.
     
       ![adres URL witryny hello przedstawiający sekcji szybkiego dostępu][csurl]
     
       **LUB**
   * Instalowanie i konfigurowanie [programu Azure Powershell](/powershell/azure/overview), a następnie hello Użyj następującego polecenia:
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Zapisz nazwę domeny hello używane w hello adres URL zwracany przez metodę albo, jak będą one potrzebne podczas tworzenia rekordu CNAME.
2. Zaloguj się na tooyour DNS rejestratora witryny sieci Web i przejdź do strony toohello zarządzania DNS. Znajdź łącza lub obszarów witryny hello oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.
3. Teraz można znaleźć, gdzie wybierz lub wprowadź CNAME w. Może być tooselect hello rekord typu z listy rozwijanej lub przejdź tooan Zaawansowane ustawienia strony. Należy szukać słowa hello **CNAME**, **Alias**, lub **poddomen**.
4. Należy również podać hello domeny lub poddomeny aliasu dla hello CNAME, takich jak **www** Jeśli chcesz toocreate aliasu dla **www.customdomain.com**. Jeśli chcesz toocreate aliasu dla domeny głównej hello, może być wymieniona jako hello "**@**" symbol w narzędziach DNS rejestratora.
5. Następnie należy podać nazwę kanoniczną hosta, która jest aplikacji **cloudapp.net** domeny w tym przypadku.

Na przykład po rekord CNAME hello przekazuje cały ruch z **www.contoso.com** za**contoso.cloudapp.net**, hello niestandardowej nazwy domeny wdrożonej aplikacji:

| Nazwa aliasu/hosta/domeny podrzędnej | Canonical domeny |
| --- | --- |
| www |contoso.cloudapp.NET |

> [!NOTE]
> Obiekt odwiedzający **www.contoso.com** nigdy nie zobaczą hello true hosta (contoso.cloudapp.net), więc hello proces przesyłania jest niewidoczne toothe użytkownika końcowego.
> 
> Witaj w powyższym przykładzie dotyczy tylko tootraffic na powitania **www** poddomeny. Ponieważ rekordy CNAME nie można używać symboli wieloznacznych, należy utworzyć jeden CNAME dla każdej domeny/poddomeny. Jeśli chcesz, ruch toodirect z poddomenami, takich jak *. contoso.com, adres cloudapp.net tooyour, można skonfigurować **adres URL przekierowania** lub **adres URL do przodu** wpis w ustawieniach DNS lub Utwórz rekord a..
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Dodawanie rekordu A dla domeny niestandardowej
rekord A toocreate, musi najpierw odnaleźć hello wirtualnego adresu IP usługi w chmurze. Następnie dodaj nowy wpis hello tabeli DNS dla domeny niestandardowej przy użyciu narzędzi hello dostarczonych przez rejestratora. Każdy rejestrator ma podobne, lecz nieco inne metody określania rekord A, ale hello są pojęcia hello takie same.

1. Użyj jednej z hello następujące metody tooget hello adres IP usługi w chmurze.
   
   * Toohello logowania [portalu Azure], wybierz usługi w chmurze, obejrzyj hello **Essentials** sekcji, a następnie znajdź hello **publicznego adresu IP, adresy** wpisu.
     
       ![Wyświetlanie hello VIP sekcji szybkiego dostępu][vip]
     
       **LUB**
   * Instalowanie i konfigurowanie [programu Azure Powershell](/powershell/azure/overview), a następnie hello Użyj następującego polecenia:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Zapisz hello adresu IP, ponieważ będzie potrzebny podczas tworzenia rekordu A.
2. Zaloguj się na tooyour DNS rejestratora witryny sieci Web i przejdź do strony toohello zarządzania DNS. Znajdź łącza lub obszarów witryny hello oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.
3. Teraz można znaleźć, gdzie wybierz lub wprowadź rekordu. Może być tooselect hello rekord typu z listy rozwijanej lub przejdź tooan Zaawansowane ustawienia strony.
4. Wybierz lub wprowadź domenę hello lub poddomeny, który będzie używany przez ten rekord. Na przykład wybierz **www** Jeśli chcesz toocreate aliasu dla **www.customdomain.com**. Toocreate wpis symboli wieloznacznych dla wszystkich domen podrzędnych, należy wprowadzić "***". Wszystkich domen podrzędnych będzie on zawierał takie jak **mail.customdomain.com**, **login.customdomain.com**, i **www.customdomain.com**.
   
    Jeśli rekord A toocreate dla domeny głównej hello, może być wymieniona jako hello "**@**" symbol w narzędziach DNS rejestratora.
5. Wprowadź adres IP hello usługi w chmurze w hello podane pole. Skojarzenie wpis domeny hello hello rekordu A o adresie IP hello wdrożenia usługi chmury.

Na przykład po rekord hello przekazuje cały ruch z **contoso.com** za**137.135.70.239**, adres IP wdrożonej aplikacji hello:

| Nazwa hosta/domeny podrzędnej | Adres IP |
| --- | --- |
| @ |137.135.70.239 |

W tym przykładzie przedstawiono tworzenie rekordu A dla domeny głównej hello. W razie potrzeby toocreate toocover wpis symbolu wieloznacznego wszystkich domen podrzędnych, należy wprowadzić "***" jako hello poddomeny.

> [!WARNING]
> Adresy IP na platformie Azure są dynamiczne domyślnie. Prawdopodobnie zechcesz toouse [zastrzeżony adres IP](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure, który nie ulega zmianie adresu IP.
> 
> 

## <a name="next-steps"></a>Następne kroki
* [W jaki sposób tooManage usług w chmurze](cloud-services-how-to-manage.md)
* [Jak tooa CDN zawartości tooMap domeny niestandardowe](../cdn/cdn-map-content-to-custom-domain.md)
* [Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).
* Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).
* Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portalu Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
