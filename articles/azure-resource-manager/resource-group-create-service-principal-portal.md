---
title: "aaaCreate tożsamość aplikacji usługi Azure w portalu | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate nową aplikację usługi Azure Active Directory i usługi podmiotu zabezpieczeń, które mogą być używane z kontroli dostępu opartej na rolach hello w usłudze Azure Resource Manager toomanage dostępu tooresources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>Użyj portalu toocreate aplikacji usługi Azure Active Directory oraz nazwy głównej usługi, który ma dostęp do zasobów

Jeśli masz aplikację, która wymaga tooaccess lub modyfikowania zasobów, należy skonfigurować aplikację Azure Active Directory (AD) i przypisać hello wymagane uprawnienia tooit. Ta metoda jest preferowana toorunning aplikacji hello z poświadczeniami użytkownika ponieważ:

* Można przypisać uprawnienia toohello tożsamości aplikacji, które są inne niż własnych uprawnień. Zazwyczaj te uprawnienia są ograniczone tooexactly jakie aplikacji hello musi toodo.
* Nie masz aplikacji hello toochange poświadczenia, jeśli Twoje obowiązki zmiany. 
* Uwierzytelnianie tooautomate certyfikatu można użyć podczas wykonywania skryptu instalacji nienadzorowanej.

W tym temacie pokazano, jak tooperform te kroki za pośrednictwem portalu hello. Głównie aplikacji pojedynczej dzierżawy, gdzie aplikacja hello jest zamierzone toorun w tylko jednej z organizacji. Zwykle użyć pojedynczej dzierżawy aplikacji dla aplikacji — biznesowych, które uruchamiane w danej organizacji.
 
## <a name="required-permissions"></a>Wymagane uprawnienia
toocomplete w tym temacie, musi mieć wystarczające uprawnienia tooregister aplikację z dzierżawą usługi Azure AD i przypisać rolę tooa aplikacji hello w Twojej subskrypcji platformy Azure. Teraz upewnij się, że masz tooperform odpowiednie uprawnienia hello tych kroków.

### <a name="check-azure-active-directory-permissions"></a>Sprawdź uprawnienia usługi Azure Active Directory
1. Zaloguj się za tooyour konto platformy Azure za pośrednictwem hello [portalu Azure](https://portal.azure.com).
2. Wybierz **usługi Azure Active Directory**.

     ![Wybierz usługę azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. W usłudze Azure Active Directory, zaznacz **ustawienia użytkownika**.

     ![Wybierz ustawienia użytkownika](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. Sprawdź hello **rejestracji aplikacji** ustawienie. Jeśli ustawiona zbyt**tak**, użytkownicy niebędący administratorami można zarejestrować aplikacji usługi AD. To ustawienie oznacza, że każdy użytkownik w dzierżawie usługi Azure AD hello można zarejestrować aplikacji. Możesz przejść za[uprawnienia subskrypcji Azure Sprawdź](#check-azure-subscription-permissions).

     ![Wyświetlanie rejestracji aplikacji](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. Jeśli ustawienie rejestracji aplikacji hello ustawiono zbyt**nr**tylko administrator użytkownicy będą mogli zarejestrować aplikacji. Należy toocheck, czy Twoje konto jest administratora dla dzierżawy usługi Azure AD hello. Wybierz **omówienie** i **znaleźć użytkownika** z szybkiego zadania.

     ![Znajdź użytkownika](./media/resource-group-create-service-principal-portal/find-user.png)
6. Wyszukaj Twoje konto i wybrania go podczas go znaleźć.

     ![Wyszukaj użytkownika](./media/resource-group-create-service-principal-portal/show-user.png)
7. Dla Twojego konta, wybierz **roli katalogu**. 

     ![Rola katalogu](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. Wyświetl roli użytkownika przypisany katalog w usłudze Azure AD. Jeśli konto jest przypisaną rolę użytkownika toohello, ale hello ustawienia rejestracji aplikacji (w poprzednich krokach hello) jest ograniczona tooadmin użytkowników, poproś tooeither Twojego administratora przypisać możesz tooan rolę administratora lub tooenable użytkowników tooregister aplikacji.

     ![Rola widoku](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>Sprawdź uprawnienia subskrypcji platformy Azure
W Twojej subskrypcji platformy Azure, jego konto musi mieć `Microsoft.Authorization/*/Write` dostępu tooassign roli tooa aplikacji usługi AD. Ta akcja jest przyznawane za pośrednictwem hello [właściciela](../active-directory/role-based-access-built-in-roles.md#owner) roli lub [Administrator dostępu użytkowników](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) roli. Jeśli Twoje konto jest przypisany toohello **współautora** roli, nie masz odpowiedniego uprawnienia. Podczas próby tooassign hello usługi tooa głównej roli, zostanie zwrócony błąd. 

toocheck uprawnienia subskrypcji:

1. Jeśli nie już poszukujesz konta usługi Azure AD z hello w poprzednich krokach, wybierz **usługi Azure Active Directory** w okienku po lewej stronie powitania.

2. Znajdź konto usługi Azure AD. Wybierz **omówienie** i **znaleźć użytkownika** z szybkiego zadania.

     ![Znajdź użytkownika](./media/resource-group-create-service-principal-portal/find-user.png)
2. Wyszukaj Twoje konto i wybrania go podczas go znaleźć.

     ![Wyszukaj użytkownika](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. Wybierz **zasobów Azure**.

     ![Wybierz zasoby](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. Wyświetl przypisane role i określić, czy tooassign odpowiednie uprawnienia roli tooa aplikacji usługi AD. Jeśli nie, poproś tooadd administratora z subskrypcji możesz tooUser dostępu do roli administratora. W hello po obrazu użytkownik hello jest toohello przypisanej roli dla dwóch subskrypcji, co oznacza, że użytkownik ma odpowiednie uprawnienia. 

     ![Pokaż uprawnienia](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>Tworzenie aplikacji usługi Azure Active Directory
1. Zaloguj się za tooyour konto platformy Azure za pośrednictwem hello [portalu Azure](https://portal.azure.com).
2. Wybierz **usługi Azure Active Directory**.

     ![Wybierz usługę azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. Wybierz **rejestracji aplikacji**.   

     ![Wybierz rejestracji aplikacji](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. Wybierz pozycję **Dodaj**.

     ![Dodaj aplikację](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Podaj nazwę i adres URL dla aplikacji hello. Wybierz opcję **aplikacji sieci Web / interfejs API** lub **natywnego** dla typu aplikacji hello ma toocreate. Po ustawieniu wartości hello, wybierz **Utwórz**.

     ![Nazwa aplikacji](./media/resource-group-create-service-principal-portal/create-app.png)

Utworzono aplikację.

## <a name="get-application-id-and-authentication-key"></a>Pobierz klucz aplikacji identyfikator i uwierzytelniania
Podczas logowania programowo, potrzebny jest identyfikator hello aplikacji i klucz uwierzytelniania. tooget tych wartości, użyj hello następujące kroki:

1. Z **rejestracji aplikacji** w usłudze Azure Active Directory, wybierz aplikację.

     ![Wybierz aplikację](./media/resource-group-create-service-principal-portal/select-app.png)
2. Kopiuj hello **identyfikator aplikacji** i zapisze go w kodzie aplikacji. Witaj aplikacji hello [przykładowe aplikacje](#sample-applications) toothis wartość jako hello identyfikator klienta można znaleźć sekcji.

     ![Identyfikator klienta](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. Wybierz toogenerate klucz uwierzytelniania **klucze**.

     ![Wybierz klucze](./media/resource-group-create-service-principal-portal/select-keys.png)
4. Podaj opis klucza hello i czas trwania hello klucza. Po zakończeniu wybierz **zapisać**.

     ![Zapisz klucz](./media/resource-group-create-service-principal-portal/save-key.png)

     Po zapisaniu hello klucza, jest wyświetlana wartość hello hello klucza. Skopiować tę wartość, ponieważ nie ma klucza hello tooretrieve można później. Podanie wartości klucza hello toolog identyfikator aplikacji hello w jako aplikacja hello. Zapisywanie wartości klucza hello gdzie aplikacji mogą być pobierane.

     ![zapisano klucza](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>Uzyskanie Identyfikatora dzierżawy
Podczas logowania programowo, potrzebny jest identyfikator dzierżawcy hello toopass do żądania uwierzytelniania. 

1. Identyfikator dzierżawy hello tooget, wybierz **właściwości** dla dzierżawy usługi Azure AD. 

     ![Wybierz właściwości usługi Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. Kopiuj hello **identyfikator katalogu**. Ta wartość jest swojego identyfikatora dzierżawcy.

     ![Identyfikator dzierżawy](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>Przypisz toorole aplikacji
tooaccess zasobów w ramach subskrypcji, należy przypisać rolę tooa aplikacji hello. Zdecyduj, które roli reprezentuje hello odpowiednich uprawnień dla aplikacji hello. Zobacz toolearn o dostępnych ról hello [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).

Zakres hello można ustawić na poziomie hello hello subskrypcji, grupy zasobów lub zasobów. Uprawnienia są dziedziczone toolower poziomy zakresu. Na przykład dodając rolę czytelnika toohello aplikacji dla grupy zasobów oznacza, że mogą odczytywać hello grupy zasobów i wszystkie zasoby, które zawiera.

1. Przejdź na poziom toohello zakresu, które mają tooassign aplikacji hello. Na przykład tooassign rola w zakresie subskrypcji hello, wybierz pozycję **subskrypcje**. Zamiast tego możesz określić, grupy zasobów lub zasobu.

     ![Wybierz subskrypcję](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. Wybierz hello określonej subskrypcji (grupę zasobów lub zasobów) tooassign hello aplikacji.

     ![Wybierz subskrypcję do przypisania](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. Wybierz **(IAM) kontroli dostępu**.

     ![Wybierz dostępu](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. Wybierz pozycję **Dodaj**.

     ![Wybierz opcję Dodaj](./media/resource-group-create-service-principal-portal/select-add.png)
6. Wybierz rolę hello mają tooassign toohello aplikacji. Witaj poniższy obraz przedstawia hello **czytnika** roli.

     ![Wybierz rolę](./media/resource-group-create-service-principal-portal/select-role.png)

8. Wyszukaj aplikację i zaznacz go.

     ![Wyszukiwanie aplikacji](./media/resource-group-create-service-principal-portal/search-app.png)
9. Wybierz **OK** toofinish przypisywanie roli hello. Zostanie wyświetlona aplikacja hello na liście Użytkownicy z przypisaną rolę tooa dla tego zakresu.

## <a name="log-in-as-hello-application"></a>Zaloguj się jako aplikacji hello

Aplikacja jest teraz skonfigurowane w usłudze Azure Active Directory. Masz identyfikator i toouse kluczy dla logowania jako aplikacja hello. Aplikacja Hello jest przypisaną rolę tooa, zapewniająca pewne akcje, które może wykonywać. Aby uzyskać informacje o zalogowanie się jako aplikacji hello za pomocą różnych platform zobacz:

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [Interfejs wiersza polecenia platformy Azure](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>Następne kroki
* tooset się aplikację wielu dzierżawców, zobacz [tooauthorization przewodnik dewelopera programu z interfejsu API usługi Azure Resource Manager hello](resource-manager-api-authentication.md).
* toolearn dotyczące określania zasad zabezpieczeń, zobacz [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md).  
* Aby uzyskać listę dostępnych akcji, które można udzielić lub odmówić toousers, zobacz [operacji dostawcy zasobów usługi Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).
