---
title: "Azure AD Connect: Zagadnienia dotyczące projektowania | Dokumentacja firmy Microsoft"
description: "W tym temacie szczegółowo niektórych obszarach projektowania implementacji"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Azure AD Connect: Zagadnienia dotyczące projektowania
Celem tego tematu Hello jest toodescribe obszarów, które muszą być uważane za pośrednictwem podczas projektu implementacji hello programu Azure AD Connect. Ten temat jest nowości w niektórych obszarach i tych pojęć krótko opisano w innych tematach również.

## <a name="sourceanchor"></a>sourceAnchor
Atrybut sourceAnchor Hello jest zdefiniowany jako *atrybutu niezmienialny w okresie istnienia hello obiektu*. Sposób unikatowy identyfikuje obiekt jako hello sam obiekt lokalnych i w usłudze Azure AD. Atrybut Hello jest również nazywany **nazwę immutableId** i Witaj dwie nazwy są używane wymienne.

Hello słowo niemodyfikowalny, "nie można zmienić", jest ważne toothis tematu. Ponieważ wartość tego atrybutu nie można zmienić po ustawieniu, jest ważne toopick projekt, który obsługuje danego scenariusza.

Atrybut Hello jest używany dla hello następujące scenariusze:

* Gdy nowy serwer aparatu synchronizacji jest skompilowany lub ponownie skompilowany od scenariusza odzyskiwania po awarii, ten atrybut łączy istniejące obiekty w usłudze Azure AD z obiektami lokalnymi.
* Jeśli przeniesiesz z modelu synchronizowanych tożsamości tooa tożsamości tylko w chmurze, a następnie ten atrybut umożliwia obiektów za "twardych dopasowania" istniejące obiekty w usłudze Azure AD z lokalnymi obiektami.
* Jeśli używasz federacyjnego, a następnie ten atrybut wraz z hello **userPrincipalName** jest używany w hello oświadczeń toouniquely identyfikacji użytkownika.

W tym temacie wspomniana sourceAnchor tylko pod kątem toousers. Witaj te same zasady stosowane tooall typów obiektów, ale tego problemu jest zwykle problemem jest tylko dla użytkowników.

### <a name="selecting-a-good-sourceanchor-attribute"></a>Wybranie atrybutu sourceAnchor dobra
wartość atrybutu Hello wykonaj hello następujące reguły:

* Zawierać mniej niż 60 znaków
  * Kodowania i liczone jak znaki 3 znaki nie są a-z, A-Z i 0-9
* Zawiera znaki specjalne: &#92;! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* Musi być globalnie unikatowa
* Musi być ciągiem, liczbą całkowitą lub danych binarnych
* Nie powinna być oparta na nazwę użytkownika, te zmiany
* Nie powinny być uwzględniana wielkość liter i uniknąć wartości, które mogą różnić się wielkością liter
* Powinien być przypisany podczas tworzenia obiektu hello

Jeśli hello wybrana sourceAnchor nie jest typu String, a następnie tooensure wartość atrybutu hello Azure AD Connect Base64Encode znaków specjalnych nie są wyświetlane. Użycie innego serwera federacyjnego niż usługi AD FS, upewnij się, serwer może również Base64Encode hello atrybutu.

Atrybut sourceAnchor Hello jest rozróżniana wielkość liter. Wartość "JanNowak" nie jest hello taki sam jak "JanNowak". Ale nie powinien mieć dwa różne obiekty z różnicą tylko wielkością liter.

Jeśli pojedynczy las jest w infrastrukturze lokalnej, następnie atrybutu hello należy używać **objectGUID**. Dotyczy to również atrybut hello używany, gdy Użyj ustawień ekspresowych w programie Azure AD Connect, a także hello atrybutu używane przez narzędzie DirSync.

Jeśli masz wiele lasów i nie przenoś użytkowników między lasami i domenami, następnie **objectGUID** toouse właściwego atrybutu nawet w tym przypadku jest.

Jeśli użytkownicy są przenoszone między lasami i domenami, następnie należy znaleźć atrybut, który nie ulega zmianie lub mogą zostać przeniesione z użytkownikami hello podczas przenoszenia hello. Zalecanym podejściem jest toointroduce syntetycznych atrybutu. Atrybut, który można umieścić element, który wygląda na to odpowiednia może być identyfikatorem GUID. Podczas tworzenia obiektu nowego identyfikatora GUID jest tworzony i widnieć hello użytkownika. Reguły niestandardowe synchronizacji mogą być tworzone w toocreate serwer aparatu synchronizacji hello tę wartość na powitania podstawie **objectGUID** i aktualizacji hello wybranego atrybutu w DODAJE. Podczas przenoszenia obiektu hello, upewnij się, że tooalso kopiowania hello zawartości tej wartości.

Innym rozwiązaniem jest toopick istniejący atrybut, których znasz nie ulega zmianie. Często używane atrybuty obejmują **identyfikator pracownika**. Należy wziąć pod uwagę atrybut, który zawiera litery, aby upewnić się, że nie hello szansy (wielkie i małe litery), można zmienić wartości atrybutu hello. Złe atrybuty, które nie powinny być używane zawiera te atrybuty o nazwie hello hello użytkownika. Unieważnienie lub rozwodu nazwa hello jest oczekiwany toochange, co jest niedozwolone dla tego atrybutu. Dotyczy to również jedną z przyczyn Dlaczego atrybutów, takich jak **userPrincipalName**, **poczty**, i **targetAddress** nie są możliwe nawet tooselect hello Azure AD Connect instalacji Kreator. Te atrybuty również zawierać hello "@" znak, który jest niedozwolony w hello sourceAnchor.

### <a name="changing-hello-sourceanchor-attribute"></a>Zmiana atrybutu sourceAnchor hello
wartość atrybutu sourceAnchor Hello nie można zmienić po utworzeniu obiektu hello w usłudze Azure AD i hello tożsamość jest zsynchronizowana.

Z tego powodu hello następujące ograniczenia zastosować tooAzure AD Connect:

* Atrybut sourceAnchor Hello można ustawić tylko podczas instalacji początkowej. Jeśli uruchomisz hello Kreatora instalacji, ta opcja jest tylko do odczytu. Jeśli potrzebujesz toochange to ustawienie, należy odinstalować i zainstalować ponownie.
* Jeśli zainstalujesz innego serwera Azure AD Connect, możesz musi wybierz hello tego samego atrybutu sourceAnchor wcześniej używane. Jeśli wcześniej została przy użyciu narzędzia DirSync i przenieść tooAzure AD Connect, należy użyć **objectGUID** ponieważ jest atrybutem hello używanym przez narzędzie DirSync.
* Jeśli wartość hello sourceAnchor zostaną zmienione po hello obiekt został wyeksportowany tooAzure AD, następnie Azure AD Connect synchronizacji wygeneruje błąd i nie zezwala na zmiany w tym obiekcie przed hello problem został rozwiązany i hello sourceAnchor jest zmieniany na powitania katalog źródłowy.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>Przy użyciu msDS-ConsistencyGuid jako sourceAnchor
Domyślnie program Azure AD Connect (wersja 1.1.486.0 i starszych) używa objectGUID jako hello atrybutu sourceAnchor. Atrybut ObjectGUID jest generowanych przez system. Nie można określić jego wartości podczas tworzenia lokalnych obiektów usługi AD. Jak opisano w sekcji [sourceAnchor](#sourceanchor), istnieją scenariusze, w których należy toospecify hello sourceAnchor wartość. Jeśli scenariusze hello są stosowane tooyou, należy użyć jako atrybut sourceAnchor hello można skonfigurować atrybut AD (na przykład msDS-ConsistencyGuid).

Azure AD Connect (wersja 1.1.524.0 oraz po) ułatwia teraz hello użycie msDS-ConsistencyGuid jako atrybut sourceAnchor. Podczas korzystania z tej funkcji Azure AD Connect automatycznie konfiguruje reguły synchronizacji hello:

1. Użyj msDS-ConsistencyGuid jako atrybut sourceAnchor hello obiektów użytkownika. Atrybut ObjectGUID jest używana do innych obiektów.

2. Dla żadnej podanej lokalnych użytkowników usługi AD obiektu, którego atrybut msDS-ConsistencyGuid nie jest wypełnione, Azure AD Connect zapisuje jej atrybutu msDS-ConsistencyGuid objectGUID wartość toohello Wstecz w lokalnej usłudze Active Directory. Po atrybutu msDS-ConsistencyGuid hello zostanie wypełnione, Azure AD Connect następnie eksportuje hello tooAzure obiektu AD.

>[!NOTE]
> Raz lokalnego obiektu usługi Active Directory jest importowany do usługi Azure AD Connect (który jest importowany do hello przestrzeni łącznika usługi AD i przedstawione jako hello Metaverse), nie można już zmienić jej wartość sourceAnchor. wartość sourceAnchor hello toospecify podane lokalnymi AD obiektów, skonfiguruj jego atrybut msDS-ConsistencyGuid przed ich zaimportowaniem do usługi Azure AD Connect.

### <a name="permission-required"></a>Wymagane uprawnienia
Ta toowork funkcja hello AD DS konto używane toosynchronize z lokalną usługą Active Directory muszą mieć uprawnienie zapisu uprawnienia toohello msDS-ConsistencyGuid atrybutu w lokalnej usłudze Active Directory.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>Jak tooenable hello funkcji ConsistencyGuid — nowa instalacja
Użycie hello ConsistencyGuid jako sourceAnchor można włączyć podczas instalacji nowego. W tej sekcji omówiono zarówno Express, jak i niestandardowe instalacji w szczegółach.

  >[!NOTE]
  > Tylko nowsze wersje programu Azure AD Connect (1.1.524.0 oraz po) obsługuje hello użyciem ConsistencyGuid sourceAnchor podczas instalacji nowego.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>Jak tooenable hello ConsistencyGuid funkcji
Obecnie funkcja hello można włączyć tylko podczas nowej instalacji usługi Azure AD Connect.

#### <a name="express-installation"></a>Instalacja ekspresowa
Podczas instalacji programu Azure AD Connect z trybem Express, Kreator Azure AD Connect hello automatycznie określa hello AD najbardziej odpowiedni atrybut toouse jako atrybut sourceAnchor hello przy użyciu następującego logiki hello:

* Po pierwsze hello Azure AD Connect Kreatora kwerend atrybut hello AD tooretrieve dzierżawy usługi Azure AD stosowane hello atrybutu sourceAnchor hello poprzedniej usługi Azure AD Connect instalacji (jeśli istnieje). Jeśli te informacje są dostępne, Azure AD Connect używa atrybutu hello tego samego AD.

  >[!NOTE]
  > Tylko nowsze wersje programu Azure AD Connect (1.1.524.0 oraz po) magazynów informacje w dzierżawie usługi Azure AD atrybutu sourceAnchor hello jest używany podczas instalacji. Starsze wersje programu Azure AD Connect, czy nie.

* Jeśli informacje o hello atrybut sourceAnchor jest niedostępna, Kreator hello sprawdza, stan hello atrybutu msDS-ConsistencyGuid hello w lokalnej usługi Active Directory. Jeśli atrybut hello nie jest skonfigurowana dla dowolnego obiektu w katalogu hello, Kreator hello używa hello msDS-ConsistencyGuid jako atrybut sourceAnchor hello. Jeśli atrybut hello jest skonfigurowany w co najmniej jednego obiektu w katalogu hello, Kreator hello zawiera atrybut hello jest używany przez inne aplikacje i nie nadaje się jako atrybut sourceAnchor...

* W takim przypadku Kreator hello powraca toousing objectGUID jako hello atrybutu sourceAnchor.

* Po decyzji atrybutu sourceAnchor hello hello kreator zapisuje informacje hello w dzierżawy usługi Azure AD. Witaj informacje będą korzystali przyszłych instalacji programu Azure AD Connect.

Po zakończeniu instalacji ekspresowej, Kreator hello informuje, atrybut, którego została pobrana jako atrybut zakotwiczenia źródła hello.

![Kreator informuje pobrane dla elementu sourceAnchor atrybutów AD](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>Instalacja niestandardowa
Podczas instalacji programu Azure AD Connect z trybem niestandardowe, Kreator Azure AD Connect hello oferuje dwie opcje podczas konfigurowania atrybutu sourceAnchor:

![Instalacja niestandardowa - sourceAnchor konfiguracji](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| Ustawienie | Opis |
| --- | --- |
| Let Zarządzanie zakotwiczenie źródła hello Azure | Wybierz tę opcję, jeśli ma atrybut hello toopick usługi Azure AD dla Ciebie. Jeśli wybierzesz tę opcję, Azure AD Connect, Kreator stosuje hello sam [logiki wybór atrybutu sourceAnchor używane podczas instalacji ekspresowej](#express-installation). Podobne tooExpress instalacji, Kreator hello informuje o atrybut, którego została pobrana jako hello atrybut zakotwiczenia źródła po zakończeniu instalacji niestandardowej. |
| Określony atrybut | Wybierz tę opcję, jeśli chcesz toospecify istniejący atrybut AD jako atrybut sourceAnchor hello. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>Jak tooenable hello funkcji ConsistencyGuid - istniejącego wdrożenia
Jeśli masz istniejące wdrożenie usługi Azure AD Connect, za pomocą objectGUID jako atrybut zakotwiczenia źródła hello można przełączać jej toousing ConsistencyGuid zamiast tego.

>[!NOTE]
> Tylko nowsze wersje programu Azure AD Connect (1.1.552.0 oraz po) obsługuje przełączenie z tooConsistencyGuid ObjectGuid jako atrybut zakotwiczenia źródła hello.

tooswitch z tooConsistencyGuid objectGUID jako atrybut zakotwiczenia źródła hello:

1. Uruchom kreatora Połącz hello Azure AD i kliknij przycisk **Konfiguruj** toogo toohello zadania ekranu.

2. Wybierz hello **Konfiguruj zakotwiczenia źródła** zadań opcję i kliknij przycisk **dalej**.

   ![Włącz ConsistencyGuid dla istniejącego wdrożenia — krok 2](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Wprowadź swoje poświadczenia usługi Azure AD administratora, a następnie kliknij przycisk **dalej**.

4. Kreator Azure AD Connect analizuje stan hello atrybutu msDS-ConsistencyGuid hello w lokalnej usługi Active Directory. Jeśli atrybut hello nie jest skonfigurowane na żadnym obiektu w katalogu, Azure AD Connect stwierdza, że żadna inna aplikacja używa obecnie atrybut hello i jest bezpieczne toouse powitalne go jako atrybut zakotwiczenia źródła hello. Kliknij przycisk **dalej** toocontinue.

   ![Włącz ConsistencyGuid dla istniejącego wdrożenia — krok 4](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. W hello **gotowe tooConfigure** kliknij **Konfiguruj** zmianę konfiguracji hello toomake.

   ![Włącz ConsistencyGuid dla istniejącego wdrożenia — krok 5](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Po zakończeniu konfiguracji hello, Kreator hello wskazuje, że ten msDS-ConsistencyGuid jest teraz używany jako atrybut zakotwiczenia źródła hello.

   ![Włącz ConsistencyGuid dla istniejącego wdrożenia — krok 6](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Podczas analizy hello (krok 4) Jeśli atrybut hello jest skonfigurowany w co najmniej jednego obiektu w katalogu hello kreatora hello zawiera atrybut hello jest używany przez inną aplikację i zwraca błąd, jak pokazano na poniższym diagramie hello. Jeśli masz pewność, że ten atrybut hello nie jest używana przez istniejące aplikacje, należy toocontact pomocy technicznej Aby uzyskać informacje dotyczące sposobu toosuppress hello błędu.

![Włącz ConsistencyGuid dla istniejącego wdrożenia — błąd](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>Wpływ na usługi AD FS lub konfiguracji federacyjne innych firm
Jeśli używasz usługi Azure AD Connect toomanage lokalnego wdrożenia usług AD FS, hello Azure AD Connect automatycznie aktualizuje atrybut reguły oświadczeń hello hello tego samego AD toouse jako sourceAnchor. Dzięki temu roszczenie nazwę ImmutableID hello generowanych przez usługi AD FS jest zgodna z hello sourceAnchor wartości wyeksportowanej tooAzure AD.

Jeśli zarządzasz usług AD FS poza Azure AD Connect lub serwery federacyjne innych firm jest używany do uwierzytelniania, należy ręcznie zaktualizować reguły oświadczeń hello na nazwę ImmutableID toobe oświadczenie zgodne z wartościami sourceAnchor hello wyeksportowane tooAzure AD jako opisane w sekcji artykułu [reguł oświadczeń Modyfikuj AD FS](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims). Kreator Hello zwraca hello następujące ostrzeżenie po zakończeniu instalacji:

![Konfiguracja federacyjnego innych firm](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>Dodawanie nowego wdrożenia tooexisting katalogów
Załóżmy, że wdrożono Azure AD Connect z włączoną funkcją ConsistencyGuid hello, a teraz chcesz tooadd inne wdrożenie toohello katalogu. Podczas próby tooadd hello katalogu Kreator Azure AD Connect sprawdza stan hello atrybutu mSDS-ConsistencyGuid hello w katalogu hello. Jeśli atrybut hello jest skonfigurowany w co najmniej jednego obiektu w katalogu hello, Kreator hello zawiera atrybut hello jest używany przez inne aplikacje i zwraca błąd, jak pokazano na poniższym diagramie hello. Jeśli masz pewność, że ten atrybut hello nie jest używana przez istniejące aplikacje, należy toocontact pomocy technicznej Aby uzyskać informacje dotyczące sposobu toosuppress hello błędu.

![Dodawanie nowego wdrożenia tooexisting katalogów](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Azure AD logowania
Podczas integracji katalogu lokalnego z usługą Azure AD, jest ważne toounderstand wpływ hello sposób użytkownika ustawienia synchronizacji hello uwierzytelnia. Użytkownik hello tooauthenticate userPrincipalName (UPN) korzysta z usługi Azure AD. Jednak po zsynchronizowaniu użytkowników, musisz wybrać toobe atrybutu hello używany dla wartości userPrincipalName uważnie.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>Wybieranie atrybutu userPrincipalName hello
Podczas wybierania atrybutu hello zapewniające hello wartość UPN toobe używane w przypadku Azure powinien zapewnić

* wartości atrybutów Hello jest zgodna z składnię nazwy UPN toohello (RFC 822), która jest powinna mieć ona hello formatusername@domain
* sufiks Hello tooone dopasowania wartości hello z hello zweryfikować domen niestandardowych w usłudze Azure AD

W ustawieniach ekspresowych hello przyjęto userPrincipalName jest rozwiązaniem dla atrybutu hello. Jeśli atrybut userPrincipalName hello nie zawiera wartości hello ma toosign Twojego użytkowników w tooAzure, a następnie należy wybrać **Instalacja niestandardowa**.

### <a name="custom-domain-state-and-upn"></a>Stan domeny niestandardowe i UPN
Jest ważne tooensure zweryfikowanej domeny dla sufiks nazwy UPN hello istnieje.

Jan jest użytkownikiem w domenie contoso.com. Ma Jan toouse hello UPN lokalnymi john@contoso.com toosign w tooAzure po zsynchronizowaniu użytkowników tooyour usługi Azure AD directory contoso.onmicrosoft.com. toodo tak, należy tooadd i sprawdź contoso.com jako niestandardową domenę, w usłudze Azure AD przed rozpoczęciem Trwa synchronizowanie hello użytkowników. Jeśli sufiks nazwy UPN hello John, na przykład contoso.com, nie odpowiada zweryfikowanej domeny w usłudze Azure AD, następnie usługi Azure AD zastępuje sufiks nazwy UPN hello contoso.onmicrosoft.com.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>UPN dla usługi Azure AD i lokalnej obsługi routingu domen
Niektóre organizacje mają nierutowalny domen, takich jak contoso.local lub prostego domen jak contoso. Nie jesteś tooverify stanie nierutowalny domeny w usłudze Azure AD. Azure AD Connect można synchronizować tooonly zweryfikowanej domeny w usłudze Azure AD. Podczas tworzenia katalogu usługi Azure AD, tworzy domenę routingu, która staje się domyślną domenę usługi Azure AD na przykład contoso.onmicrosoft.com. W związku z tym okaże się konieczne tooverify innej domeny routingu w takiej sytuacji w przypadku, gdy nie chcesz, aby toosync toohello domyślnej domeny onmicrosoft.com.

Odczyt [tooAzure nazwa Twojej niestandardową domenę usługi Active Directory dodać](../active-directory-add-domain.md) uzyskać więcej informacji dotyczących dodawania i weryfikowania domeny.

Wykrywa Azure AD Connect, jeśli są uruchomione w środowisku domeny bez obsługi routingu i będzie odpowiednio ostrzegać z wyprzedzeniem korzystanie z ustawień ekspresowych. Jeśli pracujesz w domenie bez obsługi routingu, a następnie prawdopodobne jest, że hello UPN użytkowników hello ma zbyt sufiksy bez obsługi routingu. Na przykład jeśli używane do uruchamiania contoso.local, Azure AD Connect sugeruje możesz toouse ustawienia niestandardowe, a nie przy użyciu ustawień ekspresowych. Za pomocą ustawień niestandardowych, jest możliwe toospecify hello atrybut, który powinien być używany jako toosign nazwy UPN w tooAzure po hello użytkownicy są zsynchronizowane tooAzure AD.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
