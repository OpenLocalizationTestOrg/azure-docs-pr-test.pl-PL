---
title: "aaaAzure usługi Active Directory na podstawie grupy licencjonowania dodatkowe scenariusze | Dokumentacja firmy Microsoft"
description: "Więcej scenariusze dotyczące usługi Azure Active Directory na podstawie grupy licencji"
services: active-directory
keywords: "Licencjonowanie usługi Azure AD"
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a>Scenariusze, ograniczenia i znane problemy dotyczące korzystania z grup toomanage Licencjonowanie w usłudze Azure Active Directory

Użyj hello następujące informacje i przykłady toogain dużo większą wiedzę na podstawie grupy licencjonowania usługi Azure Active Directory (Azure AD).

## <a name="usage-location"></a>Lokalizacja użytkowania

Pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach. Przed tooa użytkownika można przypisać licencji, hello administrator ma toospecify hello **lokalizacji użytkowania** właściwość hello użytkownika. W [hello portalu Azure](https://portal.azure.com), można określić w **użytkownika** &gt; **profilu** &gt; **ustawienia**.

Przypisywaniu licencji grupy użytkowników bez użycia lokalizacji określonej będzie dziedziczyć hello lokalizację katalogu hello. Jeśli masz użytkowników w wielu lokalizacjach upewnij tooreflect się, że poprawnie w obiektów użytkownika przed dodaniem użytkowników toogroups z licencjami.

> [!NOTE]
> Przypisanie do grupy licencji nie zmodyfikuje istniejącej wartości lokalizacji użytkowania na koncie użytkownika. Zaleca się zawsze ustawienie lokalizacji użytkowania jako część programu przepływu tworzenia użytkownika w usłudze Azure AD (np. za pomocą AAD Connect) -, który zapewni hello wynik przypisania licencji zawsze jest poprawna, a użytkownicy nie będą odbierać usług w lokalizacjach, które nie są dozwolone.

## <a name="use-group-based-licensing-with-dynamic-groups"></a>Za pomocą licencjonowania na podstawie grupy z grupami dynamicznymi

Za pomocą licencjonowania na podstawie grupy z żadną inną grupą zabezpieczeń, co oznacza, że można łączyć z grupami dynamicznymi w usłudze Azure AD. Uruchamia reguły z względem tooautomatically atrybutów obiektu użytkownika grup dynamicznych dodawać i usuwać użytkowników z grup.

Na przykład można utworzyć grupę dynamicznych dla niektórych zestawu produktów ma tooassign toousers. Każda grupa jest wypełniana przez regułę dodawania użytkowników według ich atrybutów, a każda grupa jest hello przypisanej licencji, że chcesz je tooreceive. Można przypisać hello atrybutu lokalnego, a jego synchronizacji z usługą Azure AD lub atrybut hello bezpośrednio w chmurze hello można zarządzać.

Licencje są przypisane użytkownika toohello później, po dodaniu ich toohello grupy. Po zmianie atrybutów hello hello użytkownik opuści hello grup i hello licencje zostaną usunięte.

### <a name="example"></a>Przykład

Rozważmy przykład hello rozwiązania zarządzania tożsamościami lokalnymi decyduje o tym, którzy użytkownicy powinni mieć dostęp tooMicrosoft sieci web usług. Używa **extensionAttribute1** toostore reprezentująca licencji hello hello użytkownik powinien mieć wartość ciągu. Azure AD Connect synchronizuje go z usługą Azure AD.

Użytkownicy mogą potrzebować jedną licencji, ale nie inna lub może być jednocześnie. Oto przykład, w którym jest rozpowszechniana Office 365 Enterprise E5 i pakietu Enterprise Mobility + Security (EMS) udziela licencji toousers w grupach:

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 Enterprise E5: podstawowe usługi

![Zrzut ekranu z pakietu Office 365 Enterprise E5 podstawowej usługi](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security: licencjonowani użytkownicy

![Zrzut ekranu Enterprise Mobility + Security licencjonowani użytkownicy](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

Na przykład zmodyfikować jednego użytkownika i ustawić ich wartości toohello extensionAttribute1 `EMS;E5_baseservices;` Jeśli chcesz toohave użytkownika hello zarówno licencji. Istnieje możliwość modyfikacji lokalnymi. Po hello zmienić jest synchronizowane z chmurą hello hello jest automatycznie dodawany tooboth grup i przypisanych licencji.

![Zrzut ekranu pokazujący sposób tooset hello extensionAttribute1 użytkownika](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> Modyfikowanie reguły członkostwa istniejącą grupę, należy zachować ostrożność. Gdy reguła zostanie zmieniona, hello członkostwo grupy hello będą ponownie oceniane i użytkowników, którzy nie odpowiadać hello nowych reguła zostanie usunięta (użytkowników, którzy nadal odpowiada hello Nowa reguła nie zostaną zmienione w trakcie tego procesu). Ci użytkownicy będą licencje usunięte podczas hello procesu, który może spowodować utratę pracy lub w niektórych przypadkach utraty danych.

> Jeśli masz dużą grupę dynamiczne zależą przypisywaniu licencji należy wziąć pod uwagę przed ich zastosowaniem grupy głównej toohello sprawdzania poprawności żadnych większych zmian w mniejszych grupie testowej.

## <a name="multiple-groups-and-multiple-licenses"></a>Wiele grup i wielu licencji

Użytkownik może należeć do wielu grup z licencjami. Poniżej przedstawiono niektóre tooconsider rzeczy:

- Wiele licencji dla samego produktu mogą nakładać się na powitalne i spowodować włączone usług są stosowane toohello użytkownika. Witaj poniższym przykładzie przedstawiono dwie grupy licencji: *usługi podstawowej E3* zawiera hello foundation toodeploy najpierw tooall użytkowników usług. I *E3 rozszerzony usług* zawiera dodatkowe usługi (kołysanie poprzeczne i planowania) toodeploy tylko toosome użytkowników. W tym przykładzie użytkownik hello został dodany tooboth grup:

  ![Zrzut ekranu przedstawiający włączone usługi](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  W związku z tym hello użytkownik ma 7 usług 12 hello w produkcie hello włączona, podczas korzystania z tylko jedną licencję dla tego produktu.

- Wybór hello *E3* licencji zawiera bardziej szczegółowe informacje, w tym informacje o tym, które grupy spowodowane toobe usług, jakie włączone dla użytkownika hello.

  ![Zrzut ekranu przedstawiający włączone usługi przez grupę](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>Bezpośrednie licencji współistnieć z grupy licencji

Gdy użytkownik dziedziczy grupę licencji, nie można bezpośrednio usunąć ani zmodyfikować tego przypisania licencji użytkownika hello właściwości. Zmiany muszą być wprowadzane w grupie hello, a następnie propagowany tooall użytkowników.

Jest to możliwe, jednak tooassign hello samej licencji produktu bezpośrednio toohello użytkownika w toohello dodanie dziedziczone licencji. Dodatkowe usługi z produktu hello tylko dla jednego użytkownika, można włączyć bez wpływu na innych użytkowników.

Bezpośrednie przypisane licencje można je usunąć i nie mają wpływu na dziedziczone licencji. Należy wziąć pod uwagę hello użytkownika, który dziedziczy z grupy licencji usługi Office 365 Enterprise E3.

1. Początkowo użytkownika hello dziedziczy hello licencji tylko hello *E3 podstawowe usługi* grupy, która umożliwia cztery planów usług, jak pokazano:

  ![Zrzut ekranu E3 włączona grupy usług](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. Możesz wybrać **przypisać** toodirectly przypisać użytkownika toohello licencji E3. W takim przypadku zostanie toodisable usługi wszystkie plany z wyjątkiem usługi Yammer przedsiębiorstwa:

  ![Zrzut ekranu przedstawiający sposób tooassign licencji bezpośrednio tooa użytkownika](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. W związku z tym hello użytkownik nadal używa tylko jedną licencję produktu hello E3. Ale hello usługi Yammer przedsiębiorstwa dla tego użytkownika tylko pozwala bezpośrednio przypisywać hello. Aby sprawdzić, usług, które są włączane przez członkostwo w grupie hello lub bezpośrednio przypisywać hello:

  ![Zrzut ekranu przedstawiający dziedziczone i bezpośredniego przypisania](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. Gdy używasz bezpośrednio przypisywać mogą hello następujące operacje:

  - Yammer przedsiębiorstwa można wyłączyć obiektu użytkownika hello bezpośrednio. Hello **Włącz/Wyłącz** Przełącz hello ilustracji został włączony dla tej usługi jako min. toohello inne usługi przełączników. Ponieważ usługa hello jest włączona bezpośrednio na powitania użytkownika, może być modyfikowany.
  - Dodatkowe usługi można włączyć również jako część hello bezpośrednio przypisać licencji.
  - Witaj **Usuń** przycisk może być używane tooremove hello bezpośredniego licencji hello użytkownika. Możesz sprawdzić, czy hello użytkownika teraz tylko hello dziedziczone grupy licencji, a pozostać włączone, tylko hello oryginalnego usługi:

    ![Zrzut ekranu pokazujący sposób tooremove bezpośrednie przypisania](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a>Zarządzanie usługami nowe dodane tooproducts
Gdy Microsoft dodaje nowy produkt tooa usługi, zostanie włączona domyślnie w wszystkich toowhich grup przypisano hello licencji produktu. Użytkownicy w Twojej dzierżawie, którzy są subskrybowanego toonotifications o zmianach produktu będziesz otrzymywać wiadomości e-mail wcześniejsze informacją o hello nadchodzących usługi dodatków.

Jako administrator można przejrzeć wszystkie grupy, który wpływa zmiana hello i podjąć działania, takie jak wyłączenie hello nową usługę w każdej grupie. Na przykład jeśli utworzono grup elementów docelowych tylko określone usługi do wdrożenia, możesz ponownie te grupy i upewnij się, że wszelkie nowo dodanych usługi zostały wyłączone.

Oto przykład co ten proces może wyglądać tak:

1. Pierwotnie przypisane hello *Office 365 Enterprise E5* grup tooseveral produktu. Jeden z tych grup, nazywany *O365 E5 - tylko program Exchange* została zaprojektowana tooenable tylko hello *usługi Exchange Online (Planowanie 2)* usługi dla jego elementów członkowskich.

2. Odebrano powiadomienie z firmy Microsoft, który hello E5 produktu zostanie rozszerzony o nową usługę - *Microsoft Stream*. Usługa hello stają się dostępne w Twojej dzierżawie, można wykonać następujące hello:

3. Przejdź toohello [ **usługi Azure Active Directory > licencji > wszystkie produkty** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) bloku, a następnie wybierz *Office 365 Enterprise E5*, a następnie wybierz pozycję **grupy licencji**  tooview listę wszystkich grup z tego produktu.

4. Kliknij na powitania grupy mają tooreview (w tym przypadku *O365 E5 - tylko program Exchange*). Spowoduje to otwarcie hello **licencji** kartę. Kliknięcie na powitania E5 licencji spowoduje otwarcie bloku listę wszystkich usług włączone.
> [!NOTE]
> Witaj *Microsoft Stream* usługi został automatycznie dodawane i włączone w tej grupie w toohello dodanie *usługi Exchange Online* usługi:

  ![Zrzut ekranu przedstawiający nową usługę dodane tooa grupy licencji](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. Toodisable hello nowej usługi w tej grupie, kliknij przycisk hello **Włącz/Wyłącz** Przełącz dalej toohello usługi, a następnie kliknij przycisk hello **zapisać** przycisk tooconfirm hello zmiany. Usługi Azure AD będzie teraz przetwarzać wszystkich użytkowników w przypadku zmiany hello tooapply grupy hello; dodaje żadnych nowych użytkowników toohello grupa nie ma hello *Microsoft Stream* włączona usługa.

  > [!NOTE]
  > Użytkownicy mogą nadal mieć usługi hello włączone przez niektóre inne przypisania licencji (innej grupy są członkami lub przypisania bezpośredniego licencji).

6. W razie potrzeby wykonaj hello przypisane same kroki dla innych grup z tego produktu.

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a>Użyj toosee programu PowerShell, który ma być dziedziczona i bezpośrednie licencji
Można użyć toocheck skrypt programu PowerShell, jeśli użytkownik ma licencję przypisane bezpośrednio lub odziedziczone po grupie.

1. Uruchom hello `connect-msolservice` tooauthenticate polecenia cmdlet i połącz tooyour dzierżawy.

2. `Get-MsolAccountSku`może być używane toodiscover wszystkie licencje elastycznie produktu w dzierżawie powitalnych.

  ![Zrzut ekranu przedstawiający polecenia cmdlet Get-Msolaccountsku hello](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. Użyj hello *AccountSkuId* wartość licencję hello planuje się [ten skrypt programu PowerShell](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group). Spowoduje to utworzenie listy użytkowników, którzy mają to licencja z hello informacji na temat sposobu licencji hello jest przypisany.

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a>Dzienniki inspekcji użycia toomonitor oparte na grupach działania licencjonowania

Można użyć [dzienników inspekcji usługi Azure AD](./active-directory-reporting-activity-audit-logs.md#audit-logs) toosee wszelkie działania związane z toogroup na podstawie licencji, w tym:
- kto zmienił licencji na grupy
- podczas uruchamiania systemu hello przetwarzania zmian grupy licencji, a po jego zakończeniu
- jakie licencji zmian użytkownika tooa wyniku przypisanie do grupy licencji.

>[!NOTE]
> Dzienniki inspekcji są dostępne w większości bloków w hello sekcji hello portalu usługi Azure Active Directory. W zależności od tego, gdzie można uzyskiwać do nich dostęp filtry mogą być wstępnie zastosowane tooonly Pokaż działania odpowiednich toohello kontekście hello bloku. Jeśli nie widzisz wyniki hello spodziewasz się, sprawdź [hello opcje filtrowania](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) ani uzyskiwać dostępu do dzienników inspekcji hello niefiltrowane w obszarze [ **usługi Azure Active Directory > działania > Dzienniki inspekcji** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>Sprawdzić, który zmodyfikował licencję grupy

1. Zestaw hello **działania** filtrować za*zestaw grupy licencji* i kliknij przycisk **Zastosuj**.
2. Witaj wyniki obejmują wszystkie przypadki licencji jest ustawiona lub modyfikować dla grupy.
>[!TIP]
> Możesz także wpisać nazwę hello grupy hello w hello *docelowej* filtrowanie wyników hello tooscope.

3. Kliknij element na powitania toosee listy wyświetlanie szczegółowych informacji o hello co się zmieniło. W obszarze *zmodyfikowane właściwości* starych i nowych wartości dla przypisania licencji hello są wymienione.

Oto przykład ostatnie zmiany licencji grupy, ze szczegółami:

![Zrzut ekranu grupy licencji zmiany](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>Dowiedzieć się, gdy zmiany w grupie rozpoczęcia i zakończenia przetwarzania

Po zmianie w grupie licencji usługi Azure AD rozpocznie się stosowanie hello zmiany tooall użytkowników.

1. toosee podczas grup Rozpoczęto przetwarzanie, ustaw hello **działania** filtrować za*rozpocząć stosowanie toousers licencji na podstawie grupy*. Należy zwrócić uwagę tego aktora hello jest operacja hello *usługi Microsoft Azure AD na podstawie grupy licencji* — system kontem, które jest używane tooexecute wszystkie zmiany w grupie licencji.
>[!TIP]
> Kliknij element hello listy toosee hello *zmodyfikowane właściwości* pola — przedstawia hello licencji zmiany, które zostały pobrana do przetwarzania. Jest to przydatne, jeśli wprowadzono wiele zmian tooa grupy, a nie masz pewności, która została przetworzona.

2. Podobnie, toosee po zakończeniu grup przetwarzania wartość filtru hello użyj *zastosowaniu toousers licencji na podstawie grupy*.
>[!TIP]
> W takim przypadku hello *zmodyfikowane właściwości* pole zawiera podsumowanie wyników hello — jest to przydatne tooquickly wyboru, jeśli przetwarzanie spowodowało błędy. Przykładowe dane wyjściowe:
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. Pełny dziennik hello toosee dla jak grupy został przetworzony, w tym wszystkich zmian użytkownika, ustaw hello następujące filtry:
  - **Zainicjowane przez (aktora)**: "Microsoft Azure AD na podstawie grupy licencji"
  - **Zakres dat** (opcjonalnie): niestandardowy zakres gdy znasz określonej grupy rozpoczęcia i zakończenia przetwarzania

To przykładowe dane wyjściowe pokazuje hello początku przetwarzania wszystkich wynikowe zmiany użytkowników i hello zakończenie przetwarzania.

![Zrzut ekranu grupy licencji zmiany](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> Klikając elementy powiązane zbyt*licencji użytkownika zmiany* wyświetli szczegóły dotyczące licencji zmiany zostały zastosowane tooeach poszczególnych użytkowników.

## <a name="limitations-and-known-issues"></a>Ograniczenia i znane problemy

Jeśli używasz licencjonowania na podstawie grupy, jest toofamiliarize dobrze samodzielnie z hello następujące listy ograniczeń i znane problemy.

- Na podstawie grupy licencjonowania aktualnie nie obsługuje grup, które zawierają inne (grup zagnieżdżonych). W przypadku zastosowania grup zagnieżdżonych tooa licencji, tylko członkowie natychmiastowego użytkownika pierwszego stopnia hello hello grupy mają licencje hello zastosowane.

- Funkcja Hello może być używana tylko z grup zabezpieczeń. Office grup nie są obecnie obsługiwane i nie będą mogli toouse ich w procesie przypisania licencji hello.

- Witaj [portalu administracyjnego usługi Office 365](https://portal.office.com ) nie obsługuje obecnie na podstawie grupy licencji. Jeśli użytkownik dziedziczy grupę licencji, ta licencja pojawia się w portalu administratora usługi Office hello jako licencji zwykłych użytkowników. Jeśli spróbujesz toomodify licencji lub spróbuj tooremove hello licencji portalu hello zwraca komunikat o błędzie. Odziedziczone grupy licencji, nie można zmodyfikować bezpośrednio na koncie użytkownika.

- Gdy użytkownik zostanie usunięty z grupy i traci hello licencji, hello planów usług z licencji (na przykład usługi SharePoint Online) są ustawione tooa **zawieszone** stanu. Witaj planów usługi nie są ustawione tooa ostateczna, stanu wyłączonego. W ten sposób można uniknąć przypadkowego usunięcia danych użytkownika, jeśli administrator wprowadza błędu w zarządzanie członkostwem grupy.

- Gdy licencje są przypisane lub modyfikować dla dużej grupy (na przykład 100 000 użytkowników), może ona wpływ na wydajność. W szczególności hello ilości generowanych przez usługi Azure AD automatyzacji zmian może niekorzystnie wpłynąć na wydajność hello synchronizacja usługi Azure AD Twojego katalogu i systemami lokalnymi.

- Automatyzacja zarządzania licencji nie reaguje automatycznie tooall typy zmian w środowisku hello. Na przykład możesz prawdopodobnie zabrakło licencji, co powoduje toobe niektórych użytkowników w stanie błędu. toofree się liczba dostępnych miejsc hello, możesz usunąć niektóre bezpośrednio przypisane licencje od innych użytkowników. Jednak hello system automatycznie zareagować toothis zmiany i Usuń użytkowników, w tym stanie błędu.

  Jako obejście toothese rodzaje ograniczenia może przejść toohello **grupy** bloku w usłudze Azure AD i kliknij przycisk **ponownie przetworzyć**. To polecenie przetwarza wszystkich użytkowników w tej grupie i rozpoznaje hello stanów błąd, jeśli to możliwe.

- Na podstawie grupy licencji nie rejestruje błędy podczas nie może zostać przypisana licencja użytkownika tooa ukończenia konfiguracji adresu proxy zduplikowane tooa w usłudze Exchange Online; takie użytkownicy są pomijane podczas przypisywania licencji. Aby uzyskać więcej informacji o tym, jak tooidentify i rozwiązać ten problem, zobacz [w tej sekcji](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online).

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat innych scenariuszy zarządzania licencji za pośrednictwem na podstawie grupy licencji, zobacz:

* [Co to jest oparte na grupach Licencjonowanie w usłudze Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Przypisywanie licencji tooa grupy w usłudze Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Identyfikowanie i rozwiązywanie problemów z licencji dla grupy w usłudze Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Jak osoba toomigrate — licencjonowani użytkownicy toogroup na podstawie Licencjonowanie w usłudze Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
