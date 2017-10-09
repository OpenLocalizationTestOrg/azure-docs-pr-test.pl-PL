---
title: aaaAzure pakiet IoT i Azure Active Directory | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak pakiet IoT Azure używa usługi Azure Active Directory toomanage uprawnienia."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a>Uprawnienia w witrynie azureiotsuite.com hello

## <a name="what-happens-when-you-sign-in"></a>Co się stanie po zalogowaniu

Witaj pierwszym zalogowaniu się na [azureiotsuite.com][lnk-azureiotsuite], lokacji hello Określa poziomy uprawnień hello oparte na powitania aktualnie wybrane dzierżawy usługi Azure Active Directory (AAD) i Azure Subskrypcja.

1. Najpierw toopopulate hello listę dzierżawców widoczne dalej tooyour username, hello lokacji znajduje z platformy Azure dzierżaw usługi AAD, które należą do. Obecnie hello witryny można uzyskać tokeny użytkownika dla jednego dzierżawcy w czasie. W związku z tym po przełączeniu dzierżawcy przy użyciu listy rozwijanej hello w prawym górnym rogu hello lokacji hello loguje użytkownika w tokenach hello tooobtain dzierżawy toothat dla tej dzierżawy.

2. Następnie hello lokacji znajduje z dzierżawy wybrane subskrypcje, które zostały skojarzone z hello Azure. Podczas tworzenia nowego rozwiązania wstępnie skonfigurowane są wyświetlane hello dostępnych subskrypcji.

3. Na koniec hello lokacji pobiera wszystkie zasoby hello w subskrypcjach hello i grup zasobów oznakowane jako wstępnie skonfigurowanych rozwiązań i wypełnia hello Kafelki na stronie głównej hello.

Hello następujące sekcje opisują role hello, kontrolujących dostęp toohello wstępnie rozwiązania.

## <a name="aad-roles"></a>Role usługi AAD

role AAD Hello kontrolować hello możliwości należy wstępnie skonfigurować rozwiązań i zarządzanie użytkownikami w wstępnie skonfigurowane rozwiązanie.

Można znaleźć więcej informacji na temat ról administratorów w usłudze AAD w [przypisywanie ról administratorów w usłudze Azure AD][lnk-aad-admin]. Witaj bieżącego artykuł skupia się na powitania **administratora globalnego** i hello **użytkownika** ról katalogu jako używane przez hello wstępnie rozwiązania.

### <a name="global-administrator"></a>Administrator globalny

Może istnieć wiele Administratorzy globalni na dzierżawę usługi AAD:

* Podczas tworzenia dzierżawy usługi AAD, są przez administratora globalnego hello domyślne tej dzierżawy.
* administrator globalny Hello można udostępnić wstępnie skonfigurowane rozwiązanie i przypisano **Admin** roli dla aplikacji hello wewnątrz ich dzierżawę usługi AAD.
* Jeśli inny użytkownik w hello sam dzierżawę usługi AAD tworzy aplikację, hello domyślna rola przyznaje jest administrator globalny toohello **tylko do odczytu**.
* Administrator globalny można przypisać tooroles użytkowników dla aplikacji za pomocą hello [portalu Azure][lnk-portal].

### <a name="domain-user"></a>Użytkownik domeny

Może istnieć wiele użytkowników domeny w dzierżawie usługi AAD:

* Użytkownik domeny można udostępnić wstępnie skonfigurowane rozwiązanie za pośrednictwem hello [azureiotsuite.com] [ lnk-azureiotsuite] lokacji. Domyślnie program hello domeny użytkownik otrzymuje hello **Admin** roli w hello zainicjowano obsługę administracyjną aplikacji.
* Użytkownik domeny, można utworzyć aplikację przy użyciu skryptu build.cmd hello w hello [azure iot — zdalnego monitorowania][lnk-rm-github-repo], [azure-iot —-konserwacji predykcyjnej] [ lnk-pm-github-repo], lub [azure iot — połączony fabryka] [ lnk-cf-github-repo] repozytorium. Jednak hello domyślnej roli przyznano jest użytkownik domeny toohello **tylko do odczytu**, ponieważ użytkownik domeny nie ma uprawnień tooassign ról.
* Jeśli inny użytkownik w dzierżawie usługi AAD hello tworzy aplikację, użytkownika domeny hello jest przypisany hello **tylko do odczytu** roli domyślnie dla tej aplikacji.
* Użytkownik domeny nie można przypisać role w aplikacji; w związku z tym użytkownikiem domeny nie można dodać użytkowników lub ról użytkowników dla aplikacji, nawet jeśli ich obsługi administracyjnej.

### <a name="guest-user"></a>Gość

Może istnieć wiele gości na dzierżawę usługi AAD. Goście mają ograniczony zestaw praw w dzierżawie usługi AAD hello. W związku z tym gości nie może obsłużyć wstępnie skonfigurowane rozwiązanie w dzierżawie usługi AAD hello.

Aby uzyskać więcej informacji dotyczących użytkowników i role w usłudze AAD zobacz następujące zasoby hello:

* [Tworzenie użytkowników w usłudze Azure AD][lnk-create-edit-users]
* [Przypisywanie użytkowników tooapps][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Role administratorów subskrypcji platformy Azure

Role administratora platformy Azure Hello kontrolować hello możliwości toomap dzierżawę tooan AD subskrypcji platformy Azure.

Dowiedz się więcej o rolach administratora platformy Azure hello w artykule hello [jak tooadd lub zmień Współadministratorem Azure, Administrator usługi i konto administratora][lnk-admin-roles].

## <a name="application-roles"></a>Role aplikacji

Role aplikacji Hello kontroli dostępu toodevices w wstępnie skonfigurowane rozwiązanie.

Istnieją dwa zdefiniowanych ról i jedną rolę niejawne zdefiniowanych w aplikacji udostępnione:

* **Administrator:** ma pełną kontrolę tooadd, zarządzania, usuń urządzenia i zmodyfikować ustawienia.
* **Tylko do odczytu:** mogą wyświetlać urządzenia, zasad, akcje, zadania i dane telemetryczne.

Można znaleźć roli tooeach w hello przypisane uprawnienia hello [RolePermissions.cs] [ lnk-resource-cs] pliku źródłowego.

### <a name="changing-application-roles-for-a-user"></a>Zmiana aplikacji ról użytkownika

Możesz użyć hello następujące procedury toomake użytkownika w usłudze Active Directory administrator wstępnie skonfigurowanych rozwiązań.

Musi być AAD administratora globalnego toochange role dla użytkownika:

1. Przejdź toohello [portalu Azure][lnk-portal].
2. Wybierz **usługi Azure Active Directory**.
3. Upewnij się, że używasz hello katalog, który wybrano w azureiotsuite.com podczas przydzielania rozwiązania. Jeśli masz wiele katalogów, skojarzonymi z Twoją subskrypcją, można przełączać się między nimi po kliknięciu nazwę swojego konta w hello prawym górnym rogu portalu hello.
4. Kliknij przycisk **aplikacje dla przedsiębiorstw**, następnie **wszystkie aplikacje**.
4. Pokaż **wszystkie aplikacje** z **żadnych** stanu. Następnie wyszukaj aplikację o nazwie wstępnie skonfigurowanych rozwiązań.
5. Kliknij nazwę hello aplikacji hello, która jest zgodna z nazwą wstępnie skonfigurowane rozwiązanie.
6. Kliknij przycisk **użytkowników i grup**.
7. Wybierz użytkownika hello ma tooswitch ról.
8. Kliknij przycisk **przypisać** i wybierz hello roli (takich jak **Admin**) ma tooassign toohello użytkownika, kliknij znacznik wyboru hello.

## <a name="faq"></a>Często zadawane pytania

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>Jestem administratorem usługi, a chcę toochange hello katalogu mapowania między mojej subskrypcji i określonych dzierżawę usługi AAD. Jak wykonać to zadanie?

1. Przejdź toohello [klasycznego portalu Azure][lnk-classic-portal], kliknij przycisk **ustawienia** liście hello usług na powitania po lewej stronie.
2. Wybierz subskrypcję hello, którą chcesz mapowanie katalogu hello toochange na.
3. Kliknij przycisk **Edytuj katalog**.
4. Wybierz hello **katalogu** chcesz toouse w hello listy rozwijanej. Kliknij strzałkę w przód hello.
5. Potwierdź mapowanie katalogu hello i wpływ współadministratorów. Jeśli przenosisz z innego katalogu, wszystkie hello współadministratorów z oryginalnym katalogu hello są usuwane.

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a>Jestem użytkownika/członek domeny na powitania dzierżawę usługi AAD i utworzono wstępnie skonfigurowanych rozwiązań. Jak pobrać przypisane roli dla mojej aplikacji?

Użytkownik administrator globalny na powitania AAD dzierżawy i przypisz role toousers samodzielnie, poproś toomake administratora globalnego. Alternatywnie, poproś tooassign administratora globalnego należy bezpośrednio roli. Jeśli chcesz dzierżawę usługi AAD hello toochange wdrożonej wstępnie skonfigurowane rozwiązanie w Zobacz hello następne pytanie.

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a>Jak zmienić hello dzierżawę usługi AAD, który Moje zdalnego monitorowania wstępnie skonfigurowane rozwiązanie i aplikacji, które są przypisane do?

Można uruchamiać wdrożeń w chmurze z <https://github.com/Azure/azure-iot-remote-monitoring> i wdrożenie z nowo utworzonego dzierżawę usługi AAD. Ponieważ jesteś, domyślnie administratorem globalnym, podczas tworzenia dzierżawy usługi AAD, mają uprawnienia użytkowników tooadd i przypisz role użytkowników toothose.

1. Tworzenie katalogu usługi AAD w hello [portalu Azure][lnk-portal].
2. Przejdź za<https://github.com/Azure/azure-iot-remote-monitoring>.
3. Uruchom `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (na przykład `build.cmd cloud debug myRMSolution`)
4. Po wyświetleniu monitu, ustaw hello **tenantid** toobe nowo utworzone dzierżawy zamiast poprzedniego dzierżawy.

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>Chcę toochange administratorem usługi ani Współadministratorem podczas logowania się za pomocą konta organizacyjnego

Zobacz artykuł pomocy technicznej hello [zmiany administratora usługi i Współadministrator podczas logowania się przy użyciu konta organizacyjne][lnk-service-admins].

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>Dlaczego widzę ten błąd? "Twoje konto nie ma toocreate odpowiednie uprawnienia hello rozwiązania. Spróbuj skontaktować się z administratorem konta lub za pomocą innego konta."

Obejrzyj powitania po diagramu w celu uzyskania wskazówek:

![][img-flowchart]

> [!NOTE]
> Jeśli będziesz kontynuować toosee hello błąd po weryfikacji jesteś administratorem globalnym dzierżawcy usługi AAD hello i współadministrator subskrypcji hello, poproś administratora konta, Usuń hello użytkownika i przypisać odpowiednie uprawnienia w tej kolejności. Najpierw dodaj hello użytkownika jako administratora globalnego, a następnie dodaj użytkownika jako administratora współpracującego na powitania subskrypcji platformy Azure. Jeśli problemy będą się powtarzać, skontaktuj się z [Pomoc i obsługa techniczna][lnk-help-support].

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>Dlaczego widzę ten błąd gdy subskrypcji platformy Azure? "Subskrypcji platformy Azure jest wymagane toocreate wstępnie skonfigurowanych rozwiązań. Użytkownik może utworzyć bezpłatne konto próbne w zaledwie kilka minut."

Jeśli masz pewność, że masz subskrypcję platformy Azure, sprawdź poprawność mapowania dla Twojej subskrypcji dzierżawcy hello i upewnij się, że wybrano hello poprawne dzierżawy w listy rozwijanej hello. Jeśli zostały sprawdzone hello potrzeby czy dzierżawy jest prawidłowa, postępuj zgodnie hello poprzedzających diagram i sprawdzić poprawności mapowania hello subskrypcji i tego dzierżawę usługi AAD.

## <a name="next-steps"></a>Następne kroki
toocontinue poznawania pakiet IoT, zobacz temat [dostosować wstępnie skonfigurowane rozwiązanie][lnk-customize].

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
