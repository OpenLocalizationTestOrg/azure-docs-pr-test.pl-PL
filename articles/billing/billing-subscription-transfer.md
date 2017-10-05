---
title: "Transfer własności subskrypcji platformy Azure na inne konto | Dokumentacja firmy Microsoft"
description: "Opisuje sposób transferu subskrypcji platformy Azure do innego użytkownika, a niektóre często zadawane pytania (FAQ) dotyczące procesu"
keywords: "przenieść subskrypcję transferu subskrypcji platformy azure, azure, Przenieś subskrypcji platformy azure do innego konta azure Zmień właściciela subskrypcji, transfer subskrypcji platformy azure na inne konto"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: c8ecdc1e-c9c5-468c-a024-94ae41e64702
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8a856c39eb11546f35cb4e8c21e6bdcce98857a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-ownership-of-an-azure-subscription-to-another-account"></a>Transfer własności subskrypcji platformy Azure do innego konta

Płatność za rzeczywiste użycie, Visual Studio, pakiet akcji lub BizSpark subskrypcje w Centrum konta można przenieść swoją subskrypcję do innego użytkownika. Firma Microsoft obsługuje transfer zewnętrznych usług platformy Azure dla tego typu subskrypcji. 

Może zaistnieć potrzeba przeniesienia własności subskrypcji platformy Azure, jeśli użytkownik:

* Należy przekazać rozliczeń posiadania subskrypcji platformy Azure do innej osoby.
* Czy chcesz zmienić konto używane do tworzenia konta platformy Azure. Być może użyć Account Microsoft, ale przeznaczone do pracy Użyj zamiast niego konta służbowego.
* Czy chcesz przenieść Twojej subskrypcji platformy Azure z jednego katalogu.
* Mają Azure i usługi Office 365 w różnych dzierżawców i do konsolidacji.

Aby zmienić subskrypcję do innej oferty, zobacz [Przełącz subskrypcji platformy Azure do innej oferty](billing-how-to-switch-azure-offer.md). 

## <a name="transfer-ownership-of-an-azure-subscription"></a>Transfer własności subskrypcji platformy Azure
> [!VIDEO https://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/Transfer-an-Azure-subscription/player]
>
>

1. Zaloguj się na stronie <https://account.windowsazure.com/Subscriptions>. Musisz być administratorem konta, aby przeprowadzić transfer własności. Aby dowiedzieć się, który jest administratorem konta subskrypcji, zobacz [— często zadawane pytania](#faq).

2. Wybierz subskrypcję do transferu.

3. Kliknij przycisk **Transfer subskrypcji** opcji. Zobacz [— często zadawane pytania](#no-button) Jeśli nie widzisz przycisku.

   ![Karta subskrypcje konto platformy Azure](./media/billing-subscription-transfer/image1.png)
4. Określ adresata.

   ![Okno dialogowe transfer subskrypcji](./media/billing-subscription-transfer/image2.PNG)
5. Adresat automatycznie otrzymuje wiadomość e-mail z linkiem umożliwiającym akceptację.

   ![E-mail transfer subskrypcji do adresata](./media/billing-subscription-transfer/image3.png)
6. Adresat klika link i postępuje zgodnie z instrukcjami, co obejmuje również wprowadzenie informacji dotyczących płatności.

   ![Pierwszej strony sieci web transfer subskrypcji](./media/billing-subscription-transfer/image4.png)

   ![Drugi strony sieci web transfer subskrypcji](./media/billing-subscription-transfer/image5.png)
7. Powodzenie! Subskrypcja jest obecnie przenoszona.

## <a name="transfer-subscription-ownership-for-enterprise-agreement-ea-customers"></a>Transfer własności subskrypcji dla klientów Enterprise Agreement (EA)
Administrator przedsiębiorstwa może przenieść własność subskrypcji w ramach rejestracji. Aby rozpocząć, zobacz [Transfer własności kont](https://ea.azure.com/helpdocs/changeAccountOwnerForASubscription) w portalu EA.

## <a name="next-steps-after-accepting-ownership-of-a-subscription"></a>Następne kroki po zaakceptowaniu własności subskrypcji
1. Jesteś teraz administratorem konta. Przejrzeć i zaktualizować administratora usługi i Współadministratorzy. Zarządzanie Administratorzy w [klasycznego portalu Azure](https://manage.windowsazure.com) , przechodząc do ustawienia. [Dowiedz się więcej o rolach administratora](billing-add-change-azure-subscription-administrator.md).

2. Umożliwia także kontroli dostępu opartej na rolach (RBAC) dla usług i subskrypcji. Odwiedź witrynę [Azure Portal](https://portal.azure.com). [Dowiedz się więcej o RBAC](../active-directory/role-based-access-control-configure.md)

3. Aktualizuj poświadczenia skojarzone z usługami tej subskrypcji w tym:
   
   * Certyfikaty zarządzania, które Przyznaj użytkownikowi uprawnień administratora do zasobów subskrypcji. Aby uzyskać więcej informacji, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure](../cloud-services/cloud-services-certs-create.md)
   
   * Klawisze dostępu dla usług, takich jak magazynu. Aby uzyskać więcej informacji, zobacz [konta magazynu Azure — informacje](../storage/common/storage-create-storage-account.md)
   
   * Poświadczenia dostępu zdalnego dla usług, takich jak maszyny wirtualne platformy Azure. 

4. [Aktualizuj alerty dotyczące rozliczeń dla tej subskrypcji](billing-set-up-alerts.md) w [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions). 

5. Jeśli współpracujesz z partnerem, należy rozważyć aktualizowanie Identyfikatora partnera w tej subskrypcji. Można zaktualizować Identyfikatora partnera w [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions).

<a id="faq"></a>

## <a name="frequently-asked-questions-faq"></a>Często zadawane pytania
* <a name="whoisaa"></a>**Się administratorem konta subskrypcji?**

  Konto administratora jest osobą, która utworzył konto na lub zakupiono subskrypcję platformy Azure. Użytkownik jest uprawniony do dostępu [Centrum konta](https://account.windowsazure.com/Home/Index) i wykonywać różne zadania zarządzania, jak tworzyć subskrypcje, anulowanie subskrypcji, zmienić rozliczeń w ramach subskrypcji, zmienić administratora usługi. Jeśli nie masz pewności, który jest administratorem konta subskrypcji, aby dowiedzieć się, należy użyć następujące kroki.

  1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
  2. W menu Centrum wybierz **subskrypcji**.
  3. Wybierz subskrypcję, którą chcesz sprawdzić, a następnie sprawdź w obszarze **ustawienia**.
  4. Wybierz **właściwości**. Administratora konta subskrypcji jest wyświetlany w **administrator konta** pole.  

* **Wszystko transferu? Łącznie z grupami zasobów, maszyn wirtualnych, dysków i inne uruchomione usługi?**

  Tak, wszystkie zasoby, takie jak maszyn wirtualnych, dysków i transfer witryn sieci Web dla nowego właściciela. Jednak wszystkie [ról administratora](billing-add-change-azure-subscription-administrator.md) i [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) po skonfigurowaniu zasad nie są przenoszone w różnych katalogach.

* <a id="no-button"></a>**Dlaczego nie widzę przycisk Transfer subskrypcji?**

  Jeśli nie widzisz **Transfer subskrypcji** przycisk, a następnie transfer subskrypcji nie jest obsługiwane dla danej oferty. [Skontaktuj się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

* **Przenoszenie subskrypcji skutkuje przestój usługi?**

  Nie ma to wpływu na usługę. Przekazanie subskrypcji spowoduje anulowanie subskrypcji w obszarze bieżącego konta administratora i tworzy subskrypcję w ramach konta adresata. Nowa subskrypcja jest skojarzona z podstawowej usług Azure. Identyfikator subskrypcji jest taka sama.

* **Jak używać tego procesu można zmienić katalogu dla subskrypcji?**

  Subskrypcja platformy Azure jest tworzony w katalogu, do którego należy administratora konta. Aby zmienić katalog, należy przenieść subskrypcję do konta użytkownika w katalogu docelowym. Po ukończeniu tego użytkownika kroki, aby zaakceptować transfer subskrypcji jest automatycznie przeniesiony do katalogu docelowego.

* **Jeśli przejąć własność rozliczeń subskrypcji z innej organizacji są one nadal mieć dostęp do moich zasobów?**

  Jeśli subskrypcja jest przenoszona do innego dzierżawcę, użytkownicy skojarzone z dzierżawcą poprzedniej utratę dostępu do subskrypcji. Nawet jeśli użytkownik nie jest administratorem usługi lub współadministratora, może nadal mają dostęp do subskrypcji za pośrednictwem innych mechanizmów zabezpieczeń, w tym:

  * Certyfikaty zarządzania, które Przyznaj użytkownikowi uprawnień administratora do zasobów subskrypcji. Aby uzyskać więcej informacji, zobacz [tworzenie i przekazywanie certyfikatu zarządzania platformy Azure](../cloud-services/cloud-services-certs-create.md).
  * Klawisze dostępu dla usług, takich jak magazynu. Aby uzyskać więcej informacji, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).
  * Poświadczenia dostępu zdalnego dla usług, takich jak maszyny wirtualne platformy Azure.

 Jeśli odbiorca musi ograniczyć dostęp do zasobów, należy rozważyć, aktualizowanie żadnych kluczy tajnych skojarzony z usługą. Najwięcej zasobów można aktualizować za pomocą następujących kroków:

    1. Przejdź do witryny [Azure Portal](https://portal.azure.com).
    2. W menu Centrum wybierz **wszystkie zasoby**.
    3. Wybierz zasób. 
    4. W bloku zasobów, kliknij przycisk **ustawienia**. W tym miejscu można wyświetlić i zaktualizować istniejące kluczy tajnych.

* **Czy mogę przenieść subskrypcję w trakcie cyklu rozliczeniowego, cyklu odbiorcy płatności dla całego rozliczeń?**

  Nadawca jest odpowiedzialny za płatności za bez użycia, który został zgłoszony do punktu zakończeniu transferu. Odbiorca jest odpowiedzialny za użycie zgłoszone od chwili transferu i jego nowszych wersjach. Może to być niektóre zastosowania, które miały miejsce przed przeniesieniem, ale został zgłoszony później. Użycie jest dołączony do rachunku adresata.

* **Odbiorca ma dostęp do użycia i rozliczeń historii?**

  Tylko adresat będzie mógł odczytać informacji jest kwota rachunku ostatniego lub jeśli subskrypcja przeniesiono przed pierwszym rachunku został wygenerowany, bieżące saldo. Pozostała część użycia i Historia rozliczeń nie są przekazywane z subskrypcją.

* **Oferta, dla której można zmienić podczas transferu?**

  Oferta, dla której musi być taka sama. Aby zmienić ofertę, zobacz [Przełącz subskrypcji platformy Azure do innej oferty](billing-how-to-switch-azure-offer.md).

* **Czy można przenieść subskrypcję, do konta użytkownika w innym kraju?**

  Nie, transfer subskrypcji z kontem użytkownika w innym kraju nie jest obsługiwany. Konto użytkownika adresata musi być w tym samym kraju.

* **Odbiorca może użyć innej metody płatności?**

  Tak. Ale Historia rozliczeń subskrypcji jest podzielić na dwa konta.  

* **Metodę płatności pogarsza po przeniesieniu subskrypcji platformy Azure?**

  Aby zaakceptować transfer subskrypcji, karta kredytowa lub podobne płatności — metoda należy podać płatności za subskrypcję. Na przykład jeśli Bob przekaże Magdalena subskrypcji, Magdalena akceptuje transferu Magdalena podać formę płatności, aby zwrócić dla subskrypcji. Po zakończeniu przenoszenia Magdalena jest on rozliczany subskrypcji nie Roberta.

* **Jak migrację danych i usługi dla subskrypcji platformy Azure do nowej subskrypcji?**

  Jeśli nie można przetransferować własność subskrypcji, można migrować ręcznie zasobów. Zobacz [przenoszenia zasobów do nowej grupy zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md).



## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu. 


