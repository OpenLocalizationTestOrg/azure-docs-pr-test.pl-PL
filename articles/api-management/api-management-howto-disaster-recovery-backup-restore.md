---
title: "za pomocą odzyskiwania po awarii aaaImplement i przywracania kopii zapasowych w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse kopia zapasowa i przywracanie tooperform odzyskiwania po awarii w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>Jak za pomocą odzyskiwania po awarii tooimplement usługi tworzenia kopii zapasowej i przywracania w usłudze Azure API Management
Przez wybranie toopublish i zarządzanie nimi swoje interfejsy API za pomocą usługi Azure API Management wykorzystaniu wielu odporność na uszkodzenia i infrastruktury możliwości, które w przeciwnym razie trzeba toodesign, wdrożenia i zarządzania nimi. Witaj platformy Azure zmniejsza duża część potencjalnych błędów w ułamku hello kosztów.

toorecover od dostępności problemów wpływających na powitania regionu, w którym usługi Zarządzanie interfejsami API hostowany możesz powinna być gotowe tooreconstitute usługi w innym regionie w dowolnym momencie. W zależności od dostępności cele i celu czasu odzyskiwania może mają tooreserve usługi tworzenia kopii zapasowej w jednym lub więcej regionów i spróbuj toomaintain swojej konfiguracji i zawartości w synchronizacji z usługą active hello. Witaj usługi tworzenia kopii zapasowej i funkcja przywracania zapewnia niezbędne bloków konstrukcyjnych hello Implementowanie strategię odzyskiwania po awarii.

W tym przewodniku przedstawiono sposób żądań tooauthenticate usługi Azure Resource Manager i w jaki sposób toobackup i przywrócić swoich wystąpień usługi Zarządzanie interfejsami API.

> [!NOTE]
> można także Hello procesu tworzenia kopii zapasowych i przywracanie wystąpienia usługi Zarządzanie interfejsami API dla odzyskiwania po awarii do replikowania wystąpień usługi Zarządzanie interfejsami API dla scenariuszy, takich jak przemieszczania.
>
> Należy pamiętać, że każda kopia zapasowa wygaśnie po upływie 30 dni. Jeśli toorestore kopii zapasowej po wygaśnięciu okresu wygaśnięcia 30-dniowej hello, przywracania hello zakończy się niepowodzeniem z `Cannot restore: backup expired` wiadomości.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Żądań uwierzytelniania usługi Azure Resource Manager
> [!IMPORTANT]
> Hello interfejsu API REST dla kopii zapasowej i przywracania używa usługi Azure Resource Manager i ma mechanizm uwierzytelniania inny niż hello interfejsów API REST zarządzania jednostek zarządzanie interfejsami API. Witaj w tej sekcji opisano sposób żądań tooauthenticate usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz [żądań uwierzytelniania usługi Azure Resource Manager](http://msdn.microsoft.com/library/azure/dn790557.aspx).
>
>

Wszystkie zadania hello, które można wykonywać na zasobów przy użyciu usługi Azure Resource Manager hello musi zostać uwierzytelniony w usłudze Azure Active Directory przy użyciu hello następujące kroki.

* Dodaj dzierżawę usługi Azure Active Directory toohello aplikacji.
* Ustawianie uprawnień dla aplikacji hello, który został dodany.
* Pobierz hello token do uwierzytelniania żądań tooAzure Menedżera zasobów.

pierwszym krokiem Hello jest toocreate aplikację usługi Azure Active Directory. Zaloguj się do hello [klasycznego portalu Azure](http://manage.windowsazure.com/) przy użyciu subskrypcji hello, który zawiera usługi Zarządzanie interfejsami API wystąpienia, a następnie przejdź toohello **aplikacji** kartę domyślnej usługi Azure Active Directory.

> [!NOTE]
> Jeśli hello Azure Active Directory domyślny katalog nie jest widoczne tooyour konta, administrator kontaktu hello Witaj Witaj toogrant subskrypcji platformy Azure wymagane uprawnienia tooyour konta.

![Utwórz aplikację usługi Azure Active Directory][api-management-add-aad-application]

Kliknij przycisk **Dodaj**, **Dodaj aplikację moją organizację**i wybierz polecenie **aplikację Native client**. Wprowadź opisową nazwę, a następnie kliknij strzałkę dalej hello. Wprowadź adres URL symbolu zastępczego, takich jak `http://resources` dla hello **identyfikator URI przekierowania**, ponieważ jest to wymagane pole, ale hello nie jest używana wartość później. Kliknij przycisk hello pole wyboru toosave hello aplikacji.

Po zapisaniu aplikacji hello, kliknij przycisk **Konfiguruj**, przewiń w dół toohello **uprawnienia aplikacji tooother** sekcji, a następnie kliknij polecenie **Dodaj aplikację**.

![Dodaj uprawnienia][api-management-aad-permissions-add]

Wybierz **Windows** **interfejs API zarządzania usługami Azure** i kliknij przycisk hello wyboru tooadd hello aplikacji.

![Dodaj uprawnienia][api-management-aad-permissions]

Kliknij przycisk **delegowane uprawnienia** obok hello nowo dodanych **Windows** **interfejs API zarządzania usługami Azure** aplikacji, pole wyboru hello **Azure dostępu Zarządzanie usługami (wersja zapoznawcza)**i kliknij przycisk **zapisać**.

![Dodaj uprawnienia][api-management-aad-delegated-permissions]

Wcześniejsze tooinvoking hello interfejsów API, który generuje hello kopii zapasowej i przywrócenie go, jest konieczne tooget tokenu. Witaj poniższym przykładzie użyto hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) token hello tooretrieve pakietu nuget.

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

Zastąp `{tentand id}`, `{application id}`, i `{redirect uri}` przy użyciu hello, postępując zgodnie z instrukcjami.

Zastąp `{tenant id}` o identyfikatorze dzierżawy hello hello utworzoną aplikację usługi Azure Active Directory. Identyfikator hello można uzyskać, klikając **wyświetlić punkty końcowe**.

![Punkty końcowe][api-management-aad-default-directory]

![Punkty końcowe][api-management-endpoint]

Zastąp `{application id}` i `{redirect uri}` przy użyciu hello **identyfikator klienta** i hello adres URL z hello **identyfikator URI przekierowania** sekcji z poziomu aplikacji usługi Azure Active Directory **Konfiguruj**  kartę.

![Zasoby][api-management-aad-resources]

Po hello wartości są określone, hello przykładowy kod powinien zwrócić token toohello podobnie poniższy przykład.

![Token][api-management-arm-token]

Przed wywołaniem hello kopii zapasowej i przywracania czynności opisane w hello następujące sekcje, ustaw nagłówek żądania autoryzacji hello połączenia REST.

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"></a>Utwórz kopię zapasową usługi Zarządzanie interfejsami API
tooback się hello problem usługi Zarządzanie interfejsami API następujące żądania HTTP:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

Gdzie:

* `subscriptionId`— Identyfikator subskrypcji hello zawierający usługi Zarządzanie interfejsami API hello próbujesz toobackup
* `resourceGroupName`-ciąg w formie "Api - Domyślnie — {usługi region}" hello gdzie `service-region` identyfikuje hello region platformy Azure, gdzie jest hostowana hello próbujesz toobackup usługi Zarządzanie interfejsami API, np.`North-Central-US`
* `serviceName`-Nazwa hello hello usługi Zarządzanie interfejsami API określona w momencie jego tworzenia hello są tworzenie kopii zapasowej
* `api-version`-Zamień`2014-02-14`

W treści żądania hello hello Określ nazwę konta magazynu Azure docelowy hello, klucz dostępu, nazwa kontenera obiektów blob i nazwa kopii zapasowej:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Ustaw wartość hello hello `Content-Type` nagłówek żądania zbyt`application/json`.

Kopia zapasowa jest operacją wymagającą dużo czasu, który może potrwać kilka minut toocomplete.  Jeśli Żądanie hello powiodło się i zainicjowano proces tworzenia kopii zapasowej hello otrzymasz `202 Accepted` kod stanu odpowiedzi z `Location` nagłówka.  Marka "GET" żądań URL toohello w hello `Location` toofind nagłówka się stan hello hello operacji. W trakcie tworzenia kopii zapasowej hello będzie tooreceive kodu stanu "202 zaakceptowane". Kod odpowiedzi `200 OK` wskaże, że ukończenie operacji tworzenia kopii zapasowej hello.

Należy pamiętać, hello następujące ograniczenia, podczas tworzenia kopii zapasowej żądania.

* **Kontener** określony w treści żądania hello **musi istnieć**.
* Gdy trwa wykonywanie kopii zapasowej możesz **nie powinny podejmować żadnych operacji zarządzania usługi** takich jak jednostki SKU uaktualnienia lub starszą wersję, zmiana nazwy domeny, itp.
* Przywracanie **kopii zapasowej jest gwarantowana tylko przez 30 dni** od hello momencie jego tworzenia.
* **Dane użycia** używany do tworzenia raportów analizy **nie jest dołączana** hello kopii zapasowej. Użyj [interfejsu API REST Azure API Management] [ Azure API Management REST API] tooperiodically pobrać raportów analizy w bezpiecznym miejscu.
* Hello częstotliwość, z którym wykonywanie kopii zapasowych usługi będzie miało wpływ na celu punktu odzyskiwania. toominimize go zaleca się wdrożenie regularnych kopii zapasowych, a także wykonywanie kopii zapasowych na żądanie po wprowadzeniu ważne zmiany usługi Zarządzanie interfejsami API tooyour.
* **Zmiany** toohello dokonano konfiguracji usługi (np. interfejsów API, zasady, wygląd portalu deweloperów) podczas operacji tworzenia kopii zapasowej jest w toku **mogą nie zostać uwzględnione w kopii zapasowej hello i w związku z tym zostaną utracone**.

## <a name="step2"></a>Przywrócenia usługi Zarządzanie interfejsami API
toorestore usługi API Management z wcześniej utworzonej kopii zapasowej należy hello następujące żądania HTTP:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

Gdzie:

* `subscriptionId`— Identyfikator subskrypcji hello zawierający usługi Zarządzanie interfejsami API hello są przywracanie kopii zapasowej do
* `resourceGroupName`-ciąg w formie "Api - Domyślnie — {usługi region}" hello gdzie `service-region` identyfikuje hello region platformy Azure, gdzie jest hostowana hello są przywracanie kopii zapasowej do usługi API Management, np.`North-Central-US`
* `serviceName`-Nazwa hello hello zarządzanie interfejsami API usługi są przywracane do określonego na powitania czasu jej utworzenia
* `api-version`-Zamień`2014-02-14`

W treści hello hello żądania Określ lokalizację pliku kopii zapasowej hello, tj. Nazwa konta magazynu platformy Azure, klucz dostępu, nazwa kontenera obiektów blob i nazwa kopii zapasowej:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Ustaw wartość hello hello `Content-Type` nagłówek żądania zbyt`application/json`.

Przywracanie jest operacją wymagającą dużo czasu, który może potrwać too30 lub więcej toocomplete minut.  Jeśli Żądanie hello powiodło się i został zainicjowany proces przywracania hello otrzymasz `202 Accepted` kod stanu odpowiedzi z `Location` nagłówka.  Marka "GET" żądań URL toohello w hello `Location` toofind nagłówka się stan hello hello operacji. W trakcie przywracania hello będzie kod stanu tooreceive "202 zaakceptowane". Kod odpowiedzi `200 OK` będą wskazywać pomyślne zakończenie operacji przywracania hello.

> [!IMPORTANT]
> **Hello SKU** usługi hello są przywracane do **musi odpowiadać** hello SKU hello kopii zapasowej przywracanej usługi.
>
> **Zmiany** toohello dokonano konfiguracji usługi (np. interfejsów API, zasady, wygląd portalu deweloperów) podczas operacji przywracania jest w toku **mogą zostać zastąpione**.
>
>

## <a name="next-steps"></a>Następne kroki
Zapoznaj się z następujących blogach firmy Microsoft dla dwóch różnych wskazówki dotyczące procesu tworzenia kopii zapasowej/przywracania hello hello.

* [Replikowanie usługi Azure API Management kont](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * Dziękujemy tooGisela dla swojego udziału toothis artykułu.
* [Usługi Azure API Management: Tworzenie kopii zapasowej i przywracanie konfiguracji](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * podejście Hello szczegółowych przy Stuart jest niezgodna z oficjalnego wskazówki hello, ale jest bardzo interesujące.

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
