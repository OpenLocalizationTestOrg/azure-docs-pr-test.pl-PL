---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości - określenia strategii wdrażania cyklu życia tożsamości hybrydowej | Dokumentacja firmy Microsoft"
description: "Pomaga zdefiniować hello hybrydowego tożsamości zadań zarządzania zgodnie z toohello opcji dostępnych dla każdej fazy cyklu życia."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 420b6046-bd9b-4fce-83b0-72625878ae71
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 86ec0a9896f069bc93e49e06006954848f8e4d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-hybrid-identity-lifecycle-adoption-strategy"></a>Określić strategii wdrażania cyklu życia tożsamości hybrydowej
W tym zadaniu będziesz definiować strategii zarządzania hello tożsamości dla hybrydowych tożsamości rozwiązania toomeet hello wymagań biznesowych zdefiniowane w [określić zadań zarządzania tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md).

toodefine hello hybrydowego tożsamości zadań zarządzania zgodnie z cyklem życia tożsamości na trasie toohello przedstawione wcześniej w tym kroku, konieczne będzie tooconsider hello opcji dostępnych dla każdej fazy cyklu życia.

## <a name="access-management-and-provisioning"></a>Zarządzanie dostępem i inicjowania obsługi
Rozwiązania zarządzania kontem dobrych dostępu, w organizacji mogą śledzić dokładnie kto ma dostęp do informacji toowhat w organizacji hello.

Kontrola dostępu jest krytyczne funkcję inicjowania obsługi administracyjnej systemu scentralizowanego, jednego miejsca. Oprócz ochrony informacji poufnych, kontroli dostępu ujawnia istniejące konta, które mają niezatwierdzonych zezwolenia lub są już wymagane. przestarzałe kont toocontrol, hello inicjowania obsługi administracyjnej systemu łącza razem informacje o koncie autorytatywne informacje o hello posiadaczom hello kont. Informacje o tożsamości użytkownika autorytatywne zwykle są przechowywane w hello baz danych i katalogów zasobów ludzkich.

Kont w zaawansowanej przedsiębiorstw IT mają setki parametrów, które określają hello urzędów, a te informacje mogą być kontrolowane przez inicjowania obsługi administracyjnej systemu. Nowi użytkownicy można zidentyfikować przy użyciu hello zapewniają z hello wiarygodne źródło danych. możliwości zatwierdzania żądania dostępu Hello inicjuje procesom hello zatwierdzenia (lub nie) inicjowania obsługi administracyjnej dla nich zasobów.

| Faza zarządzania cyklem życia | Lokalnie | Chmura | Połączenie hybrydowe |
| --- | --- | --- | --- |
| Zarządzanie kontami i inicjowania obsługi |Za pomocą roli serwera usług domenowych Active Directory® (AD DS) hello, możesz utworzyć skalowalne, bezpieczną i łatwą w obsłudze infrastrukturę do zarządzania użytkownikami i zasobami i zapewniają obsługę aplikacji obsługujących katalogi, takich jak Microsoft® Exchange Server. <br><br> [Można udostępniać grup w usługach AD DS za pomocą programu Identity manager](https://technet.microsoft.com/library/ff686261.aspx) <br>[Umożliwia obsługę użytkowników w usługach AD DS](https://technet.microsoft.com/library/ff686263.aspx) <br><br> Administratorzy mogą używać dostęp do sterowania toomanage użytkownika dostępu tooshared zasobów ze względów bezpieczeństwa. W usłudze Active Directory, podawana jest kontrola dostępu na poziomie obiektu hello przez ustawienie różnych poziomów dostępu lub uprawnienia, tooobjects, takie jak Pełna kontrola, odczytu, zapisu lub Brak dostępu. Kontrola dostępu w usłudze Active Directory definiuje sposób różnych użytkowników za pomocą obiektów usługi Active Directory. Domyślnie uprawnienia do obiektów w usłudze Active Directory są ustawiane toohello najbezpieczniejsze ustawienie. |Masz toocreate konta dla wszystkich użytkowników, którzy będą uzyskiwać dostęp do usługi w chmurze firmy Microsoft. Można również zmienić konta użytkowników lub usuwania ich, gdy nie są już potrzebne. Domyślnie użytkownicy nie mają uprawnień administratora, ale Opcjonalnie można przypisać. Aby uzyskać więcej informacji, zobacz [Zarządzanie użytkownikami w usłudze Azure AD](active-directory-create-users.md). <br><br> W usłudze Azure Active Directory jest jedną z głównych funkcji hello hello możliwości toomanage dostępu tooresources. Te zasoby mogą być częścią katalogu hello, tak jak przypadku hello obiektów toomanage uprawnienia za pomocą ról w katalogu hello lub zasobów, które są zewnętrzne toohello katalogu, takiego jak aplikacji SaaS, usług platformy Azure i witryn programu SharePoint lub lokalnymi zasoby. <br><br> Na powitania rozwiązania do zarządzania Centrum z usługą Azure Active Directory w dostępu to grupa zabezpieczeń hello. właściciel zasobu Hello (lub administratorem hello katalogu hello) można przypisać tooprovide grupy niektórych zasobów toohello prawa dostępu, których są właścicielami. Hello członkami grupy hello będą udostępniane hello dostępu i właściciel zasobu hello można delegować hello prawo toomanage hello członków listy grupy toosomeone else — takie jak Menedżer działu lub administratora pomocy technicznej<br> <br> Hello Zarządzanie grup w usłudze Azure AD temacie zamieszczono więcej informacji dotyczących zarządzania dostęp za pośrednictwem grup. |Rozszerzają tożsamości usługi Active Directory do chmury hello za pośrednictwem synchronizacji i Federacji |

## <a name="role-based-access-control"></a>Kontrola dostępu oparta na rolach
Kontrola dostępu oparta na rolach (RBAC) używa ról i inicjowania obsługi zasad tooevaluate, testowanie i wymuszać procesy biznesowe, a zasady dotyczące przyznawania toousers dostępu. Administratorzy klucza Utwórz zasady inicjowania obsługi i Przypisz użytkowników tooroles i definiującą zestawy tooresources uprawnienia dla tych ról. RBAC rozszerza hello tożsamości rozwiązania toouse opartych na oprogramowaniu procesów zarządzania i zmniejszyć ręczne interakcji z użytkownikiem w procesie inicjowania obsługi hello.
Azure AD RBAC umożliwia hello firmy toorestrict hello ilość czynności, które osoby mogą wykonywać, gdy ma on tooAzure dostęp do portalu zarządzania. Za pomocą portalu toohello dostępu toocontrol RBAC, zbliża się Administratorzy IT urzędu certyfikacji Delegowanie dostępu za pomocą hello zarządzania dostępem do następujących:

* **Przypisanie oparte na grupach roli**: można przypisać dostępu grup tooAzure AD, które można synchronizować z lokalnej usługi Active Directory. Dzięki temu tooleverage hello dotychczasowych inwestycji wprowadzone w narzędzi i procesów do zarządzania grupami organizacji. Umożliwia także funkcji zarządzania grupy delegowanego hello Azure AD Premium.
* **Wykorzystywanie wbudowane role na platformie Azure**: można użyć trzech ról — tooensure właściciela, współautora i czytnika, że użytkownicy i grupy mają uprawnienia toodo tylko hello zadania muszą toodo swoich zadań.
* **Szczegółowe dostępu tooresources**: można przypisać toousers ról i grup dla określonej subskrypcji, grupy zasobów lub pojedynczych zasobów platformy Azure, takich jak witryny sieci Web lub bazy danych. W ten sposób można upewnij się, że użytkownicy mają dostęp do zasobów hello tooall, które są im potrzebne i nie tooresources dostępu, że nie potrzebują oni toomanage.

## <a name="provisioning-and-other-customization-options"></a>Inicjowanie obsługi i inne opcje dostosowywania
Twojego zespołu za pomocą toodecide planów i wymagania biznesowe ile toocustomize hello tożsamości rozwiązania. Na przykład dużego przedsiębiorstwa mogą wymagać planu wdrożenie etapowe dla przepływów pracy i kart niestandardowych, które jest oparte na osi czasu przyrostowo udostępniania aplikacji, które są powszechnie używane na różnych obszarach geograficznych. Co najmniej dwa toobe aplikacje udostępniane w całej organizacji, po pomyślnym przetestowaniu udostępniać inny plan dostosowania. Interakcji aplikacji użytkownika mogą być dostosowywane i procedury dotyczące inicjowania obsługi administracyjnej zasobów może być zmienione tooaccommodate automatycznego inicjowania obsługi administracyjnej.

Można anulowanie zastrzeżenia tooremove usługi lub składnika. Na przykład anulowania obsługi konta oznacza, że konto hello jest usuwane z zasobu.

Hello hybrydowego modelu obsługi zasobów łączy żądania i opartej na rolach metod, które są obsługiwane przez usługę Azure AD. Dla podzbioru pracowników lub zarządzanych systemach firma może być tooautomate dostępu z przypisania opartego na rolach. Firma może również obsługi wszystkich żądań dostępu lub wyjątki poprzez model na podstawie żądań. Niektóre firmy mogą rozpoczynać się od ręcznego przypisania i rozwijać kierunku modelu hybrydowych, zamiaru wdrożenia pełni opartej na rolach w przyszłości.

Innych firm może być niepraktyczne dla firm powodów tooachieve pełną opartej na rolach inicjowania obsługi administracyjnej i miejsce docelowe rozwiązanie hybrydowe jako celem wymagana. Nadal innych firm, które mogą były tylko na podstawie żądań obsługi i nie mają tooinvest toodefine dodatkowego nakładu pracy i zarządzanie zasadami inicjowania obsługi opartej na rolach, automatycznej.

## <a name="license-management"></a>Zarządzanie licencjami
Zarządzanie licencjami na podstawie grupy w usłudze Azure AD umożliwia administratorom przypisanie grupy zabezpieczeń użytkownicy tooa i usługi Azure AD automatycznie przypisuje licencje tooall hello członkami grupy hello. Jeśli użytkownik jest następnie dodane do lub usunięte z grupy hello, licencji zostaną automatycznie przypisane lub usunięte odpowiednio.

Możesz użyć grup synchronizowani z lokalnej usługi AD lub zarządzania nimi w usłudze Azure AD. Parowanie to z usługą Azure AD premium samoobsługowego zarządzania grupami można łatwo delegować licencji przypisania toohello odpowiednie inne osoby podejmujące decyzje. Można mieć pewność, automatycznie sortowane problemów, takich jak konflikty licencji i danych lokalizacji Brak.

## <a name="self-regulating-user-administration"></a>Samoregulujące Administracja użytkownikami
Po uruchomieniu przez wszystkie organizacje wewnętrzny tooprovision zasobów organizacji zaimplementowaniem hello samoregulujące funkcji administracji użytkowników. Poza granicami organizacji, można zrealizować hello korzyści i zalet inicjowania obsługi użytkowników. W tym środowisku zmiany w stan użytkownika jest automatycznie odzwierciedlane w prawa dostępu między granicami organizacji i lokalizacji geograficznych. Można zmniejszyć koszty inicjowania obsługi administracyjnej i usprawnić hello dostępu i zatwierdzania procesów. Implementacja Hello realizuje hello potencjał zastosowania kontroli dostępu opartej na rolach dla zarządzania dostępem end-to-end w Twojej organizacji. Można zmniejszyć koszty administracyjne za pomocą zautomatyzowanych procedur dotyczących Inicjowanie obsługi użytkowników. Można zwiększyć poziom bezpieczeństwa, automatyzując egzekwowanie zasad zabezpieczeń i usprawnić i scentralizowanie zarządzania cyklem życia użytkownika i udostępnianie zasobów dla dużej liczby użytkowników populacji.

> [!NOTE]
> Aby uzyskać więcej informacji zobacz Konfigurowanie usługi Azure AD w celu zarządzania dostępem do aplikacji Sklep internetowy
> 
> 

(W oparciu o uprawnieniach) na podstawie licencji usługi Azure AD usług pracy przez aktywowania subskrypcji w dzierżawie usługi katalogowej/usługi Azure AD. Po hello subskrypcja jest aktywna hello możliwości usługi można zarządzane przez administratorów usługi katalogowej/i używane przez licencjonowanych użytkowników. Aby uzyskać więcej informacji zobacz temat jak Azure AD licencjonowania pracy?
Integracja z innych dostawców 3

Usługa Azure Active Directory zapewnia jednokrotnego na i ulepszone toothousands zabezpieczeń dostępu do aplikacji dla aplikacji SaaS i lokalnej aplikacji sieci web. Aby uzyskać szczegółową listę galerii aplikacji usługi Azure Active Directory dla obsługiwanych aplikacji SaaS, zobacz listę zgodności federacyjnych usługi Azure Active Directory: dostawcy tożsamości innych firm, które mogą być używane tooimplement logowanie jednokrotne

## <a name="define-synchronization-management"></a>Definiowanie zarządzania synchronizacji
Zintegrowanie katalogów lokalnych z usługą Azure AD zwiększa produktywność użytkowników, zapewniając wspólną tożsamość na potrzeby dostępu do zasobów, zarówno lokalnych, jak i w chmurze. Z tej integracji użytkowników i organizacji można korzystać z następujących hello:

* Organizacje mogą umożliwiać użytkownikom wspólną tożsamość hybrydowa między lokalnymi lub usług w chmurze korzystania z usługi Active Directory systemu Windows Server, a następnie łącząc tooAzure usługi Active Directory.
* Administratorzy mogą udostępnić dostępu warunkowego na podstawie zasobów aplikacji, urządzenia i tożsamości użytkownika, lokalizacji sieciowej i uwierzytelniania wieloskładnikowego.
* Użytkownicy mogą korzystać z ich wspólną tożsamość za pomocą konta w usłudze Azure AD tooOffice 365, Intune, aplikacje SaaS i aplikacje innych producentów.
* Deweloperzy mogą tworzyć aplikacje, które wykorzystują hello wspólnego modelu tożsamości, integrowanie aplikacje lokalne usługi Active Directory lub Azure dla aplikacji działających w chmurze

Witaj następujący rysunek zawiera przykład ogólny widok procesu synchronizacji tożsamości.

![](./media/hybrid-id-design-considerations/identitysync.png)

Proces synchronizacji tożsamości

Przejrzyj następujące opcje synchronizacji hello toocompare tabeli hello:

| Opcja zarządzania synchronizacji | Zalety | Wady |
| --- | --- | --- |
| Na podstawie synchronizacji (przy użyciu narzędzia DirSync lub AADConnect) |Użytkownicy i grupy synchronizowane z lokalnej i w chmurze <br>  **Zasady kontroli**: zasady konta można ustawić za pomocą usługi Active Directory, co daje zasady haseł toomanage możliwości hello hello administratora, stacji roboczej, ograniczenia, formanty blokady i, bez tooperform dodatkowe zadania w chmurze hello.  <br>  **Kontrola dostępu**: można ograniczyć dostęp do usługi w chmurze toohello tak, aby usługi hello jest możliwy za pośrednictwem hello środowiska firmy za pośrednictwem serwerów online lub oba. <br>  Zmniejszona wywołań obsługi: Jeśli użytkownicy mają mniej tooremember haseł, są one rzadziej tooforget je. <br>  Zabezpieczenia: Tożsamości użytkowników i informacje są chronione, ponieważ wszystkie serwery hello i usług używanych w rejestracji jednokrotnej, są zarządzane i kontrolowane lokalnymi. <br>  Obsługa silnego uwierzytelniania: można używać silnego uwierzytelniania (nazywanych również uwierzytelnianie dwuskładnikowe) z usługi w chmurze hello. Jednak użycie silnego uwierzytelniania, należy użyć rejestracji jednokrotnej. | |
| Na podstawie federacyjnych (za pośrednictwem usług AD FS) |Korzystając z usługi tokenu zabezpieczającego (STS). Podczas konfigurowania usługi STS tooprovide pojedynczego logowania jednokrotnego dostępu z usługą w chmurze firmy Microsoft, zostanie utworzony relację zaufania federacji między lokalną STS i domeny federacyjnej hello określone w dzierżawie usługi Azure AD. <br> Umożliwia użytkownikom końcowym hello toouse sam zestaw poświadczeń tooobtain dostęp do toomultiple zasobów <br>Użytkownicy końcowi nie mają toomaintain wiele zestawów poświadczeń. Jeszcze hello użytkownicy mają tooprovide ich poświadczenia tooeach jedną hello uwzględnionych zasobów., scenariusze B2B i B2C, które są obsługiwane. |Wymaga specjalnych personelu do wdrażania i konserwacji lokalnych dedykowanych serwerów usług AD FS. Jeśli planujesz toouse usług AD FS dla Twojej usługi STS istnieją ograniczenia dotyczące wykorzystania hello silnego uwierzytelniania. Aby uzyskać więcej informacji, zobacz [Konfigurowanie usług AD FS 2.0 zaawansowane opcje](http://go.microsoft.com/fwlink/?linkid=235649). |

> [!NOTE]
> Aby uzyskać więcej informacji, zobacz [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
> 
> 

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

