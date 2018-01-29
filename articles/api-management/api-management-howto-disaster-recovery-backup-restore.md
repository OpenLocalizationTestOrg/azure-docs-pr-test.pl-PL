---
title: "Za pomocą odzyskiwania po awarii wdrożenie i przywracania kopii zapasowych w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać kopii zapasowej i przywracania do odzyskiwania po awarii w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2018
ms.author: apimpm
ms.openlocfilehash: 3fcd2fc4162cfbf549be979e15745934c2e4c6ff
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>Jak zaimplementować odzyskiwania po awarii przy użyciu usługi Kopia zapasowa i przywracanie w usłudze Azure API Management

Przez wybranie publikowanie i zarządzanie nimi swoje interfejsy API za pomocą usługi Azure API Management są korzystanie z wielu odporność na uszkodzenia i możliwości infrastruktury, które w przeciwnym razie byłyby projektowania, wdrożenia i zarządzania nimi. Platforma Azure zmniejsza duża część potencjalnych błędów w ułamku kosztów.

Aby odzyskać z dostępności problemów wpływających na region, w którym hostowana jest usługi API Management, możesz przystąpić do odtworzenia z usługą w innym regionie, w dowolnym momencie. W zależności od dostępności i celu czasu odzyskiwania można zarezerwować usługi tworzenia kopii zapasowej w jednym lub więcej regionów, a następnie spróbuj Obsługa swojej konfiguracji i zawartości w synchronizacji z usługą active. Funkcja "Kopia zapasowa i przywracanie" usługi zawiera niezbędne bloku konstrukcyjnego stosowania strategii odzyskiwania po awarii.

W tym przewodniku pokazano, jak do uwierzytelniania żądań usługi Azure Resource Manager oraz jak kopie zapasowe i przywracanie swoich wystąpień usługi Zarządzanie interfejsami API.

> [!NOTE]
> Proces tworzenia kopii zapasowych i przywracanie wystąpienia usługi Zarządzanie interfejsami API dla odzyskiwania po awarii można również do replikacji wystąpień usługi Zarządzanie interfejsami API dla scenariuszy, takich jak przemieszczania.
>
> Każda kopia zapasowa wygasa po upływie 30 dni. Próba przywrócenia kopii zapasowej, po wygaśnięciu 30-dniowy okres przywracania kończy się niepowodzeniem z `Cannot restore: backup expired` wiadomości.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Żądań uwierzytelniania usługi Azure Resource Manager

> [!IMPORTANT]
> Interfejs API REST dla kopii zapasowej i przywracania używa usługi Azure Resource Manager i ma mechanizm uwierzytelniania inny niż interfejsów API REST zarządzania jednostek zarządzanie interfejsami API. W tej sekcji opisano sposób do uwierzytelniania żądań usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz [żądań uwierzytelniania usługi Azure Resource Manager](http://msdn.microsoft.com/library/azure/dn790557.aspx).
>
>

Wszystkie zadania, które można wykonywać na zasobów przy użyciu usługi Azure Resource Manager musi zostać uwierzytelniony w usłudze Azure Active Directory, wykonując następujące czynności:

* Dodawanie aplikacji do dzierżawy usługi Azure Active Directory.
* Ustawianie uprawnień dla aplikacji, który został dodany.
* Pobierz token uwierzytelniania żądań do usługi Azure Resource Manager.

### <a name="create-an-azure-active-directory-application"></a>Tworzenie aplikacji usługi Azure Active Directory

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com). 
2. Przy użyciu subskrypcji, która zawiera wystąpienia usługi Zarządzanie interfejsami API, przejdź do **rejestracji aplikacji** kartę.

    > [!NOTE]
    > Jeśli domyślny katalog Azure Active Directory nie jest widoczna na koncie, skontaktuj się z administratorem subskrypcji platformy Azure można udzielić wymaganych uprawnień do konta.
3. Kliknij pozycję **Rejestrowanie nowej aplikacji**.

    **Utwórz** po prawej stronie zostanie wyświetlone okno. To, gdzie wprowadź odpowiednie informacje usługi AAD aplikacji.
4. Wprowadź nazwę dla aplikacji.
5. Wybierz typ aplikacji **natywnego**.
6. Wprowadź adres URL symbolu zastępczego, takich jak `http://resources` dla **identyfikator URI przekierowania**, ponieważ jest to wymagane pole, ale nie jest używana wartość później. Kliknij pole wyboru, aby zapisać aplikację.
7. Kliknij przycisk **Utwórz**.

### <a name="add-an-application"></a>Dodawanie aplikacji

1. Po utworzeniu aplikacji, kliknij przycisk **ustawienia**.
2. Kliknij przycisk **wymagane uprawnienia**.
3. Kliknij przycisk **+ Dodaj**.
4. Naciśnij klawisz **wybierz interfejs API**.
5. Wybierz **Windows** **interfejsu API zarządzania usługami Azure**.
6. Naciśnij klawisz **wybierz**. 

    ![Dodaj uprawnienia](./media/api-management-howto-disaster-recovery-backup-restore/add-app.png)

7. Kliknij przycisk **delegowane uprawnienia** obok nowo dodanego aplikacji, pole wyboru dla **dostępu do usługi Azure Service Management (wersja zapoznawcza)**.
8. Naciśnij klawisz **wybierz**.

### <a name="configuring-your-app"></a>Konfigurowanie aplikacji

Przed wywołaniem interfejsów API, które Generowanie kopii zapasowej i przywrócenie go, należy uzyskać token. W poniższym przykładzie użyto [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) pakiet NuGet w celu pobrania tokenu.

```csharp
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
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

Zastąp `{tentand id}`, `{application id}`, i `{redirect uri}` z poniższymi instrukcjami:

1. Zastąp `{tenant id}` o identyfikatorze dzierżawy utworzoną aplikację usługi Azure Active Directory. Identyfikator można uzyskać, klikając **rejestracji aplikacji** -> **punkty końcowe**.

    ![Punkty końcowe][api-management-endpoint]
2. Zastąp `{application id}` o wartości, możesz uzyskać, przechodząc do **ustawienia** strony.
3. Zastąp adres URL z **identyfikator URI przekierowania** karta jest aplikacja usługi Azure Active Directory.

    Po wartości są określone, przykładowy kod powinien zwrócić token podobny do poniższego przykładu:

    ![Token][api-management-arm-token]

## <a name="calling-the-backup-and-restore-operations"></a>Podczas wywoływania operacji tworzenia kopii zapasowej i przywracania

Przed wywołaniem "Kopia zapasowa i przywracanie" czynności opisane w poniższych sekcjach, ustaw nagłówek żądania autoryzacji dla wywołania REST.

```csharp
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

### <a name="step1"></a>Utwórz kopię zapasową usługi Zarządzanie interfejsami API
Aby utworzyć kopię zapasową problem dotyczący usługi Zarządzanie interfejsami API następujące żądania HTTP:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

Gdzie:

* `subscriptionId`— Identyfikator subskrypcji zawierający usługi Zarządzanie interfejsami API próbujesz utworzyć kopię zapasową
* `resourceGroupName`-ciąg w formie "Api - Domyślnie — {usługi region}" gdzie `service-region` identyfikuje region platformy Azure, gdzie zarządzanie interfejsami API usługi próbujesz kopii zapasowej jest obsługiwany, na przykład`North-Central-US`
* `serviceName`-Nazwa usługi Zarządzanie interfejsami API tworzysz kopię zapasową określony w momencie jego tworzenia.
* `api-version`-Zamień`2014-02-14`

W treści żądania Określ nazwę konta magazynu Azure docelowej, klucz dostępu, nazwa kontenera obiektów blob i nazwa kopii zapasowej:

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Ustaw wartość `Content-Type` nagłówek żądania do `application/json`.

Kopia zapasowa jest operacją wymagającą dużo czasu, który może potrwać kilka minut.  Jeśli żądanie zostało pomyślnie zainicjowano proces tworzenia kopii zapasowej, zostanie wyświetlony `202 Accepted` kod stanu odpowiedzi z `Location` nagłówka.  Upewnij się, "GET" żądania na adres URL w `Location` nagłówka, aby sprawdzić stan operacji. Podczas tworzenia kopii zapasowej jest w toku, nadal jest wyświetlany kodu stanu "202 zaakceptowane". Kod odpowiedzi `200 OK` wskazuje ukończenie operacji tworzenia kopii zapasowej.

Należy zauważyć następujące ograniczenia, podczas tworzenia kopii zapasowej żądania.

* **Kontener** określony w treści żądania **musi istnieć**.
* Gdy trwa wykonywanie kopii zapasowej możesz **nie powinny podejmować żadnych operacji zarządzania usługi** takich jak jednostki SKU uaktualnienia lub starszą wersję, zmiana nazwy domeny, itp.
* Przywracanie **kopii zapasowej jest gwarantowana tylko przez 30 dni** od momentu jego utworzenia.
* **Dane użycia** używany do tworzenia raportów analizy **nie jest dołączana** w kopii zapasowej. Użyj [interfejsu API REST Azure API Management] [ Azure API Management REST API] okresowo pobrać raportów analizy w bezpiecznym miejscu.
* Częstotliwość, z którym wykonywanie kopii zapasowych usługi wpływa na celu punktu odzyskiwania. Aby zminimalizować, zalecenie jest implementacja regularnych kopii zapasowych podobnie jak wykonywanie kopii zapasowych na żądanie po wprowadzeniu istotnych zmian do usługi API Management.
* **Zmiany** wprowadzone w konfiguracji usługi (na przykład interfejsów API, zasady, wygląd portalu deweloperów) podczas tworzenia kopii zapasowej operacja jest w toku **mogą nie zostać uwzględnione w kopii zapasowej i w związku z tym zostaną utracone**.

### <a name="step2"></a>Przywrócenia usługi Zarządzanie interfejsami API
Aby przywrócić zarządzanie interfejsami API usługi z kopii zapasowej utworzonej wcześniej upewnij następujące żądania HTTP:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

Gdzie:

* `subscriptionId`— Identyfikator subskrypcji zawierający usługi Zarządzanie interfejsami API są przywracanie kopii zapasowej do
* `resourceGroupName`-ciąg w formie "Api - Domyślnie — {usługi region}" gdzie `service-region` identyfikuje region platformy Azure, w którym hostowana jest usługi Zarządzanie interfejsami API są przywracane do kopii zapasowej, na przykład`North-Central-US`
* `serviceName`-Nazwa zarządzanie interfejsami API usługi są przywracane do określonych w momencie jego tworzenia
* `api-version`-Zamień`2014-02-14`

W treści żądania Określ lokalizację pliku kopii zapasowej, który jest, nazwa konta magazynu platformy Azure, klucz dostępu, nazwa kontenera obiektów blob i nazwa kopii zapasowej:

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Ustaw wartość `Content-Type` nagłówek żądania do `application/json`.

Przywracanie jest operacją wymagającą dużo czasu, który może potrwać do co najmniej 30 minut, aby zakończyć. Jeśli żądanie zostało wykonane i zainicjowano proces przywracania, pojawi się `202 Accepted` kod stanu odpowiedzi z `Location` nagłówka. Upewnij się, "GET" żądania na adres URL w `Location` nagłówka, aby sprawdzić stan operacji. Podczas przywracania jest w toku, nadal jest wyświetlany "202 zaakceptowane" Kod stanu. Kod odpowiedzi `200 OK` wskazuje na pomyślne zakończenie operacji przywracania.

> [!IMPORTANT]
> **Jednostka SKU** usługi są przywracane do **musi odpowiadać** jednostki SKU usługi kopii zapasowej przywracanej.
>
> **Zmiany** wprowadzone w konfiguracji usługi (na przykład interfejsów API, zasady, wygląd portalu deweloperów) podczas przywracania operacja jest w toku **mogą zostać zastąpione**.
>
>

## <a name="next-steps"></a>Kolejne kroki
Zapoznaj się z następujących blogach firmy Microsoft dla dwóch różnych wskazówki dotyczące procesu tworzenia kopii zapasowej/przywracania.

* [Replikowanie usługi Azure API Management kont](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
* [Usługi Azure API Management: Tworzenie kopii zapasowej i przywracanie konfiguracji](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * Podejście szczegółowych przy Stuart jest niezgodny z oficjalnego wytyczne, ale jest interesujące.

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
