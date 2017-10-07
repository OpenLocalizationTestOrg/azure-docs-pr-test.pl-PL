---
title: "aaaUse grup toomanage tooresources dostępu w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toouse grup w usłudze Azure Active Directory toomanage użytkownika dostępu tooon lokalnych i aplikacji w chmurze i zasobów."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory
Azure Active Directory (Azure AD) to kompleksowe tożsamościami i dostępem zarządzania rozwiązanie, które oferuje niezawodny zestaw możliwości toomanage dostępu tooon lokalnych i aplikacji w chmurze i zasobów w tym usługi online firmy Microsoft, takich jak usługi Office 365 i world aplikacji SaaS innych niż Microsoft. Ten artykuł zawiera omówienie, ale jeśli chcesz od razu grup toostart przy użyciu usługi Azure AD, postępuj zgodnie z instrukcjami hello [Zarządzanie grupami zabezpieczeń w usłudze Azure AD](active-directory-accessmanagement-manage-groups.md). Jeśli chcesz, aby toosee korzystania z programu PowerShell toomanage grup w usłudze Azure Active directory można znaleźć więcej informacji, zobacz [polecenia cmdlet usługi Azure Active Directory dla grupy zarządzania](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

> [!NOTE]
> toouse usługi Azure Active Directory, należy konta platformy Azure. Jeśli nie masz konta, możesz [Załóż bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

W ramach usługi Azure AD jest jedną z głównych funkcji hello hello możliwości toomanage dostępu tooresources. Te zasoby mogą być częścią katalogu hello, tak jak przypadku hello obiektów toomanage uprawnienia za pomocą ról w katalogu hello lub zasobów, które są zewnętrzne toohello katalogu, takiego jak aplikacji SaaS, usług platformy Azure i witryn programu SharePoint lub lokalnymi zasoby. Istnieją cztery sposoby użytkownika można przypisać zasobów tooa praw dostępu:

1. Przypisania bezpośredniego

    Użytkownicy mogą być przypisani bezpośrednio tooa zasobów przez właściciela hello tego zasobu.
2. Członkostwo w grupie

    Grupy można przypisać tooa zasobów przez właściciela zasobu hello i w ten sposób, udzielanie hello członkami zasób toohello dostęp do tej grupy. Członkostwo w grupie hello zarządza następnie hello właściciela grupy hello. Ostatecznie delegatów właściciela zasobu hello hello uprawnienia tooassign użytkowników tootheir toohello właściciel zasobu hello grupy.
3. Na podstawie reguł

    właściciel zasobu Hello służy tooexpress reguły, użytkowników, którzy powinni należeć dostępu tooa zasobów. wynik Hello hello reguły zależy od atrybutów hello używane w tej regule i ich wartości dla określonych użytkowników, i w ten sposób właściciel zasobu hello skutecznie deleguje hello toomanage prawo dostępu tootheir zasobów toohello autorytatywne źródło hello atrybuty, które są używane w regule hello. właściciel zasobu Hello nadal zarządza reguły hello, sama i określa atrybuty i wartości, które zapewniają dostęp do zasobów tootheir.
4. Zewnętrznego urzędu

    Witaj dostępu tooa zasobów pochodzi ze źródła zewnętrznego; na przykład grupa, która jest zsynchronizowany z wiarygodnego źródła, takich jak katalog lokalny lub aplikacji SaaS, takich jak produktu WorkDay. właściciel zasobu Hello przypisuje hello grupy tooprovide dostępu toohello zasobów oraz źródła zewnętrznego hello zarządza hello członkami grupy hello.

   ![Omówienie dostępu administracyjnego diagramu](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>Obejrzyj klip wideo, który objaśnia zarządzanie dostępem
Można obejrzeć krótki film, który objaśnia, więcej informacji na ten temat:

**Azure AD: Wprowadzenie toodynamic członkostwa w grupach**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>Jak uzyskać dostępu do zarządzania w pracy z usługą Azure Active Directory?
Na powitania center hello rozwiązania do zarządzania dostęp do usługi Azure AD jest hello grupy zabezpieczeń. Korzystanie z zabezpieczeń grupy toomanage dostępu tooresources jest dobrze znanego modelu, który umożliwia elastyczne i zrozumiałymi sposób tooprovide dostępu tooa zasobu dla hello przeznaczone grupy użytkowników. właściciel zasobu Hello (lub administratorem hello katalogu hello) można przypisać tooprovide grupy niektórych zasobów toohello prawa dostępu, których są właścicielami. Hello członkami grupy hello będą udostępniane hello dostępu i właściciel zasobu hello można delegować hello prawo toomanage hello członków listy grupy toosomeone innego, na przykład manager działu lub administratora pomocy technicznej.

![Azure diagram zarządzania dostęp do usługi Active Directory](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

Hello właściciel grupy może także udostępnić tej grupy dla żądań samoobsługi. W ten sposób użytkownik końcowy można wyszukiwać i znaleźć grupy hello i wprowadzić toojoin żądania, skutecznie wyszukiwanie zasobów hello tooaccess uprawnienia, które są zarządzane przez grupę hello. Witaj właściciela grupy hello można skonfigurować grupy hello żądań dołączenia są automatycznie zatwierdzane lub wymagają zatwierdzenia przez właściciela hello hello grupy. Gdy użytkownik tworzy toojoin żądania grupy, żądanie dołączenia hello jest przekazywany toohello właścicieli grupy hello. Jeśli jeden z właścicieli hello zatwierdza Żądanie hello, hello żądania użytkownik jest powiadamiany o i użytkownik hello jest toohello dołączonego do grupy. Jeśli jeden z właścicieli hello odrzuca żądanie hello, użytkownika żądającego hello jest powiadamiany o, ale nie przyłączona do grupy toohello.

## <a name="getting-started-with-access-management"></a>Wprowadzenie do zarządzania dostępem
Rozpoczęto gotowe tooget? Należy spróbować niektórych hello podstawowe zadania, które można wykonać za pomocą grup usługi Azure AD. Za pomocą tych możliwości tooprovide specjalizowany dostępu toodifferent grupy użytkowników dla różnych zasobów w organizacji. Poniżej przedstawiono listę podstawowych pierwsze kroki.

* [Tworzenie prostego reguły tooconfigure dynamiczne zarządzanie członkostwem w grupie](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [Przy użyciu aplikacji tooSaaS grupy toomanage dostępu](active-directory-accessmanagement-group-saasapps.md)
* [Udostępnianie grupy dla użytkownika samoobsługi](active-directory-accessmanagement-self-service-group-management.md)
* [Trwa synchronizowanie tooAzure grupy lokalnej za pomocą usługi Azure AD Connect](active-directory-aadconnect.md)
* [Zarządzanie właścicielami grupy](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>Następne kroki
Teraz, możesz zrozumienie hello podstawowe informacje dotyczące funkcji zarządzania dostępem poniżej przedstawiono niektóre dodatkowe funkcje zaawansowane dostępne w usłudze Azure Active Directory do zarządzania dostępu tooyour aplikacji i zasobów.

* [Przy użyciu atrybutów toocreate zaawansowane zasady](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Zarządzanie grupami zabezpieczeń w usłudze Azure AD](active-directory-accessmanagement-manage-groups.md)
* [Konfigurowanie grupy dedykowane w usłudze Azure AD](active-directory-accessmanagement-dedicated-groups.md)
* [Interfejs API Graph odwołania dla grup](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy](active-directory-accessmanagement-groups-settings-cmdlets.md)
