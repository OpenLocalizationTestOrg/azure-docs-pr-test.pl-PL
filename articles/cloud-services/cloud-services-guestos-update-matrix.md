---
title: "Dowiedz się więcej o najnowszych wersjach systemu operacyjnego gościa Azure | Dokumentacja firmy Microsoft"
description: "Najnowsze informacje o wersji i zestawu SDK zgodności w systemie operacyjnym gościa usługi w chmurze Azure."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 6306cafe-1153-44c7-8554-623b03d59a34
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 8/24/2017
ms.author: raiye
ms.openlocfilehash: a4439346817df9223c032abc1405a7cf9cbe780b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Azure wersji systemu operacyjnego gościa i zgodność pakietu SDK
Zapewnia użytkownikowi aktualne informacje o najnowszych systemu operacyjnego gościa Azure wersje usługi w chmurze. Informacje te pomagają sobie planowanie uaktualnienia przed wyłączeniem systemu operacyjnego gościa. Jeśli konfigurujesz role do użycia *automatyczne* aktualizacji systemu operacyjnego gościa, zgodnie z opisem w [ustawienia aktualizacji systemu operacyjnego gościa Azure][Azure Guest OS Update Settings], nie jest istotne, aby odczytać tę stronę.

> [!IMPORTANT]
> Ta strona dotyczy ról usługi w chmurze sieci web i proces roboczy, które działają ponad systemu operacyjnego gościa. Robi **nie stosuje się** do maszyn wirtualnych IaaS.
>
>


> [!NOTE]
> Źródło danych RSS niedawno została zastąpiona. Śledzenie aktualizacji na nowe źródło danych wkrótce!
>
>

Nie wiesz, o jaką systemu operacyjnego gościa jest lub jak systemu operacyjnego gościa wersje robocze? Odczyt [to](#how-it-works) sekcji.

## <a name="news-updates"></a>Wiadomości

###### <a name="august-24-2017"></a>**24 sierpnia 2017 r.**
Wydała sierpnia systemu operacyjnego gościa.

###### <a name="august-3-2017"></a>**3 sierpnia 2017 r.**
Wydała lipca systemu operacyjnego gościa.

###### <a name="july-19-2017"></a>**19 lipca 2017 r.**
Wdrożenie systemu operacyjnego gościa lipca rozpoczyna lipca 19 i ma planowanego wersji 8 sierpnia.

###### <a name="july-7-2017"></a>**7 lipca 2017 r.**
Wydała czerwca systemu operacyjnego gościa.

###### <a name="june-16-2017"></a>**16 czerwca 2017 r.**
Wdrożenie systemu operacyjnego gościa czerwca uruchamia 16 czerwca i ma planowanego zlecenia lipca 11.

###### <a name="june-5-2017"></a>**5 czerwca 2017 r.**
Może wydała systemu operacyjnego gościa.

###### <a name="may-17-2017"></a>**17 maja 2017 r.**
Z powodu błędu zabezpieczeń, możemy wyłączania następujące grudnia 2016 i stycznia 2017 r poszczególnych wersji systemu operacyjnego, które nie mają [rozwiązać] z portalu: WA — GOŚCIA — systemu operacyjnego — 5.4_201612 — WA 01, — GOŚCIA — systemu operacyjnego — 4.39_201612-01, WA — GOŚCIA — systemu operacyjnego — 3.46_201612-01, WA-GOŚCIA-OS-2.59_201701-01

###### <a name="may-12-2017"></a>**12 maja 2017 r.**
Wdrożenie systemu operacyjnego gościa może rozpoczyna maja 12 i ma planowanego wersji 13 czerwca.

###### <a name="april-18-2017"></a>**18 kwietnia 2017 r.**
Wdrożenie systemu operacyjnego gościa kwietnia rozpoczyna 18 kwietnia i ma planowanego wersji może 9.

###### <a name="april-10-2017"></a>**10 kwietnia 2017 r.**
Wdrożenie systemu operacyjnego gościa marca uruchomiona 14 marca 2017 r i wydanej w dniu 10 kwietnia 2017 r.

###### <a name="january-10-2017"></a>**10 stycznia 2017 r.**
System operacyjny gościa stycznia zawiera poprawki, których wpływ tylko na rodziny systemów operacyjnych 2 (Windows Server 2008 R2). Dlatego firma Microsoft wydała tylko obraz systemu operacyjnego z rodziny 2 (WA-GOŚCIA-OS-2.59_201701-01) w tym miesiącu. Dla wszystkich innych rodzin systemu operacyjnego, systemu operacyjnego grudnia (201612 - 01) pozostaje najnowszą.


## <a name="releases"></a>Wersje
## <a name="family-5-releases"></a>Zwalnia rodziny 5
**W systemie Windows Server 2016**

Zainstalowany program .NET framework: 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2

> [!NOTE]
> Daty z * są może ulec zmianie.
>
> Hasło RDP 5 rodziny systemu operacyjnego musi mieć co najmniej 10 znaków.
>

| Ciąg konfiguracji | Data wydania | Wyłącz daty | Wygasłe daty |
| --- | --- | --- | --- |
| WA-GOŚCIA-OS-5.10_201708-01 |24 sierpnia 2017 r. |Post 5.12 |TBD |
| WA-GOŚCIA-OS-5.9_201707-01 |3 sierpnia 2017 r. |Post 5.11 |TBD |
| WA-GOŚCIA-OS-5.8_201706-01 |7 lipca 2017 r. |Post 5.10 |TBD |
|~~WA-GOŚCIA-OS-5.7_201705-01~~ |5 czerwca 2017 r. |24 sierpnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-5.6_201704-01~~ |9 maja 2017 r. |3 sierpnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-5.5_201703-01~~ |10 kwietnia 2017 r. |7 lipca 2017 r. |TBD |
|~~WA-GOŚCIA-OS-5.4_201612-01~~ |10 stycznia 2017 r. |5 czerwca 2017 r.|TBD |
|~~WA-GOŚCIA-OS-5.3_201611-01~~ |14 grudnia 2016 r. |9 maja 2017 r. |TBD |
|~~WA-GOŚCIA-OS-5.2_201610-02~~ |1 listopada 2016 r. |10 kwietnia 2017 r. |TBD |

## <a name="family-4-releases"></a>Zwalnia rodziny 4
**Windows Server 2012 R2**

Obsługuje platformy .NET 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Daty z * są może ulec zmianie
>
>

| Ciąg konfiguracji | Data wydania | Wyłącz daty | Wygasłe daty |
| --- | --- | --- | --- |
| WA-GOŚCIA-OS-4.45_201708-01 |24 sierpnia 2017 r. |Post 4.47 |TBD |
| WA-GOŚCIA-OS-4.44_201707-01 |3 sierpnia 2017 r. |Post 4.46 |TBD |
| WA-GOŚCIA-OS-4.43_201706-01 |7 lipca 2017 r. |Post 4,45 |TBD |
|~~WA-GOŚCIA-OS-4.42_201705-01~~ |5 czerwca 2017 r. |24 sierpnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-4.41_201704-01~~ |9 maja 2017 r. |3 sierpnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-4.40_201703-01~~ |10 kwietnia 2017 r. |7 lipca 2017 r. |TBD |
|~~WA-GOŚCIA-OS-4.39_201612-01~~ |10 stycznia 2017 r. |5 czerwca 2017 r. |TBD |
|~~WA-GOŚCIA-OS-4.38_201611-01~~ |14 grudnia 2016 r. |9 maja 2017 r. |TBD |
|~~WA-GOŚCIA-OS-4.37_201610-02~~ |16 listopada 2016 r. |10 kwietnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-4.36_201609-01~~ |13 października 2016 r. |14 stycznia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-4.35_201608-01~~ |13 wrześniu 2016 r. |16 grudnia 2016 r. |TBD |
|~~WA-GOŚCIA-OS-4.34_201607-01~~ |8 sierpnia 2016 r. |13 listopada 2016 r. |TBD |


## <a name="family-3-releases"></a>Zwalnia rodziny 3
**Windows Server 2012**

Obsługuje platformy .NET 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Daty z * są może ulec zmianie
>
>

| Ciąg konfiguracji | Data wydania | Wyłącz daty | Wygasłe daty |
| --- | --- | --- | --- |
| WA-GOŚCIA-OS-3.52_201708-01 |24 sierpnia 2017 r. |Post 3.54 |TBD |
| WA-GOŚCIA-OS-3.51_201707-01 |3 sierpnia 2017 r. |Post 3.53 |TBD |
| WA-GOŚCIA-OS-3.50_201706-01 |7 lipca 2017 r. |Post 3.52 |TBD |
|~~WA-GOŚCIA-OS-3.49_201705-01~~ |5 czerwca 2017 r. |24 sierpnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-3.48_201704-01~~ |9 maja 2017 r. |3 sierpnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-3.47_201703-01~~ |10 kwietnia 2017 r. |7 lipca 2017 r. |TBD |
|~~WA-GOŚCIA-OS-3.46_201612-01~~ |10 stycznia 2017 r. |5 czerwca 2017 r. |TBD |
|~~WA-GOŚCIA-OS-3.45_201611-01~~ |14 grudnia 2016 r. |9 maja 2017 r. |TBD |
|~~WA-GOŚCIA-OS-3.44_201610-02~~ |16 listopada 2016 r. |1 maja 2017 r. |TBD |
|~~WA-GOŚCIA-OS-3.43_201609-01~~ |13 października 2016 r. |14 stycznia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-3.42_201608-01~~ |13 wrześniu 2016 r. |16 grudnia 2016 r. |TBD |
|~~WA-GOŚCIA-OS-3.41_201607-01~~ |8 sierpnia 2016 r. |13 listopada 2016 r. |TBD |


## <a name="family-2-releases"></a>Zwalnia rodziny 2
**Windows Server 2008 R2 z dodatkiem SP1**

Obsługuje .NET 3.5, 4.0, 4.5, 4.5.1, 4.5.2

> [!NOTE]
> Daty z * są może ulec zmianie
>
>

| Ciąg konfiguracji | Data wydania | Wyłącz daty | Wygasłe daty |
| --- | --- | --- | --- |
| WA-GOŚCIA-OS-2.65_201708-01 |24 sierpnia 2017 r. |Post 2.67 |TBD |
| WA-GOŚCIA-OS-2.64_201707-01 |3 sierpnia 2017 r. |Post 2,66 |TBD |
| WA-GOŚCIA-OS-2.63_201706-01 |7 lipca 2017 r. |Post 2.65 |TBD |
|~~WA-GOŚCIA-OS-2.62_201705-01~~ |5 czerwca 2017 r. |24 sierpnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-2.61_201704-01~~ |9 maja 2017 r. |3 sierpnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-2.60_201703-01~~ |10 kwietnia 2017 r. |7 lipca 2017 r. |TBD |
|~~WA-GOŚCIA-OS-2.59_201701-01~~ |10 stycznia 2017 r. |5 czerwca 2017 r. |TBD |
|~~WA-GOŚCIA-OS-2.58_201612-01~~ |10 stycznia 2017 r. |9 maja 2017 r.|TBD |
|~~WA-GOŚCIA-OS-2.57_201611-01~~ |14 grudnia 2016 r. |10 kwietnia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-2.56_201610-02~~ |16 listopada 2016 r. |10 lutego 2017 r. |TBD |
|~~WA-GOŚCIA-OS-2.55_201609-01~~ |13 października 2016 r. |14 stycznia 2017 r. |TBD |
|~~WA-GOŚCIA-OS-2.54_201608-01~~ |13 wrześniu 2016 r. |16 grudnia 2016 r. |TBD |
|~~WA-GOŚCIA-OS-2.53_201607-01~~ |8 sierpnia 2016 r. |13 listopada 2016 r. |TBD |



## <a name="msrc-patch-updates"></a>MSRC poprawek i aktualizacji
Lista poprawek, które są dołączone do każdej miesięcznej wersji systemu operacyjnego gościa jest dostępna [tutaj][patches].

## <a name="sdk-support"></a>Obsługa w zestawie SDK
Mimo że [wycofywania zasad dla zestawu Azure SDK] [ retire policy sdk] wskazuje, czy tylko wersje powyżej 2.2 są obsługiwane, określonych rodzin systemu operacyjnego gościa umożliwiają używanie wcześniejszych wersji. Należy zawsze używać najnowszej obsługiwanym zestawem SDK.

| Rodzina systemów operacyjnych gościa | Wersje zgodne zestawu SDK |
| --- | --- |
| 5 |Wersja 2.9.5.1+ |
| 4 |W wersji 2.1 + |
| 3 |W wersji 1.8 + |
| 2 |W wersji 1.3 + |
| 1 |W wersji 1.0 + |

## <a name="guest-os-release-information"></a>Informacje o wersji systemu operacyjnego gościa
Istnieją trzy daty, które są ważne dla poszczególnych wersji systemu operacyjnego gościa: **wersji** daty, **wyłączone** daty, i **wygaśnięcia** daty. Systemu operacyjnego gościa jest uważany za dostępny, gdy znajduje się w portalu, a jako element docelowy systemu operacyjnego gościa można wybrać. Gdy osiągnie systemu operacyjnego gościa **wyłączone** daty, zostanie ono usunięte z platformy Azure. Jednak wszystkie usługi w chmurze przeznaczonych dla tego systemu operacyjnego gościa nadal będzie działać jako standardowa.

Okno między **wyłączone** daty i **wygaśnięcia** Data zawiera buforu do łatwe przejście z jednego systemu operacyjnego gościa do jednego nowsza. Jeśli używasz *automatyczne* jako system operacyjny gościa, zawsze będzie w najnowszej wersji i nie trzeba martwić się o jego wygaśnięcia.

Gdy **wygaśnięcia** data przekazuje wszystkie usługi w chmurze w dalszym ciągu używają tego systemu operacyjnego gościa będzie można zatrzymać, usunięty lub zmuszony do uaktualnienia. Więcej o zasadach wycofania [tutaj][retirepolicy].

## <a name="guest-os-family-version-explanation"></a>Wyjaśnienie rodziny wersja systemu operacyjnego gościa
Rodzin systemu operacyjnego gościa są oparte na wersji systemu Microsoft Windows Server. System operacyjny gościa jest system operacyjny, działającą z usługi w chmurze Azure. Każdego systemu operacyjnego gościa ma rodziny, wersji i wydania numer.

* **Rodzina systemów operacyjnych gościa**  
  Wersja systemu operacyjnego Windows Server, na podstawie systemu operacyjnego gościa. Na przykład *rodziny 3* jest oparta na systemie Windows Server 2012.
* **Wersja systemu operacyjnego gościa**  
  Specyficzne dla rodziny obraz systemu operacyjnego gościa oraz odpowiednie [Microsoft Security odpowiedzi Center (MSRC)] [ msrc] poprawki, które są dostępne w dniu powstaje nowej wersji systemu operacyjnego gościa. Nie wszystkie poprawki można uwzględnić.

    Numery rozpoczynają się od 0 i 1 zwiększenia zawsze, gdy zostanie dodany nowy zestaw aktualizacji. Końcowe zero są wyświetlane tylko jeśli jest to ważne. Wersja 2.10 jest inny, kiedy wersję niż wersja 2.1.
* **Wersja systemu operacyjnego gościa**  
  Ponowne wydanie wersji systemu operacyjnego gościa. Ponowne wydanie występuje, gdy zauważamy problemów podczas testowania; wymagające zmiany. Najnowsza wersja zawsze zastępuje wszystkie poprzednie wersje, publiczny lub nie. Azure portal tylko pozwoli użytkownikom do pobrania najnowszej wersji dla danej wersji. Wdrożenia z poprzedniej wersji nie są zwykle życie uaktualnienia w zależności od ważności usterki.

W poniższym przykładzie 2 to rodzina, 12, jest to wersja i "rel2" jest wersją.

**Wersji systemu operacyjnego gościa** — 2.12 rel2

**Ciągu konfiguracji dla tej wersji** — WA-GOŚCIA-OS-2.12_201208-02

Ciąg konfiguracji dla systemu operacyjnego gościa ma te same informacje osadzone w nim, oraz datę przedstawiający poprawki MSRC, które zostały uznane za w tej wersji. W tym przykładzie MSRC poprawek dla systemu Windows Server 2008 R2 do klasy i, w tym — sierpień 2012 zostały uwzględnione w. Uwzględniane są tylko poprawek, w szczególności stosowania do tej wersji systemu Windows Server. Na przykład jeśli poprawka MSRC odnosi się do programu Microsoft Office, nie zostanie on uwzględniony ponieważ tego produktu nie jest częścią obrazu podstawowego systemu Windows Server.

## <a name="guest-os-system-update-process"></a>Proces aktualizacji systemu systemu operacyjnego gościa
Ta strona zawiera informacje o kolejnych wersjach systemu operacyjnego gościa. Klienci wskazał, czy chce wiedzieć, kiedy zlecenia występuje, ponieważ ich role usługi w chmurze zostanie ponownie uruchomiony, jeśli są ustawione na "Automatyczny" aktualizacji. Wersje systemu operacyjnego gościa zwykle występuje co najmniej pięć (5) dni po MSRC aktualizacji wersji, która występuje w drugi wtorek każdego miesiąca. Nowości obejmują wszystkie odpowiednie poprawki MSRC dla każdej rodziny systemów operacyjnych gościa.

Microsoft Azure stale udostępnia aktualizacji. System operacyjny gościa jest tylko jeden taki aktualizacji w potoku. Zlecenia może niekorzystnie wpływać wiele czynników zbyt duża, aby wyświetlić w tym miejscu. Ponadto Azure wykorzystuje dosłownie setki tysięcy komputerów. Oznacza to, czy jest możliwe umieszczenie dokładnej dacie i godzinie, gdy zostanie ponownie uruchomiony z rolami. Pracujemy nad planu w celu ograniczenia lub czas ponownego uruchomienia.

Po opublikowaniu nowej wersji systemu operacyjnego gościa może upłynąć czas pełni są propagowane na platformie Azure. Ponieważ usługi są aktualizowane do nowego systemu operacyjnego gościa, ich są ponownie uruchamiane ramach domen aktualizacji. Usługi skonfigurowane do korzystania z aktualizacji "Automatyczny" otrzyma zlecenia pierwszy. Po aktualizacji zostanie wyświetlone na liście usługi w portalu Azure nowej wersji systemu operacyjnego gościa. Ponownych wydań mogą wystąpić podczas tego okresu. Niektóre wersje może wdrożyć przez dłuższy czas i automatyczne ponowne uruchomienie uaktualnienia nie może wystąpić wiele tygodni po dacie oficjalnego wydania. Po udostępnieniu systemu operacyjnego gościa, można jawnie wybrać tej wersji w portalu lub w pliku konfiguracji.

Dla dużą cennych informacji na temat ponownego uruchomienia i wskaźniki, aby uzyskać więcej informacji technicznych szczegółów aktualizacji systemu operacyjnego hosta i gościa, zobacz blog MSDN post zatytułowany [roli wystąpienia uruchamia ponownie z powodu uaktualnienia systemu operacyjnego] [ restarts].

Jeśli ręcznie zaktualizować system operacyjny gościa, zobacz [systemu operacyjnego gościa wycofywania zasad] [ retirepolicy] Aby uzyskać dodatkowe informacje.

## <a name="guest-os-supportability-and-retirement-policy"></a>Możliwość obsługi systemu operacyjnego gościa i wycofywania zasad
Zasady obsługi i wycofania systemu operacyjnego gościa jest wyjaśniono [tutaj][retirepolicy].

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure.md
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
[rozwiązać]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
