---
title: aaaHost wiele lokacji z bramy aplikacji Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera instrukcje tooconfigure istniejącą bramę aplikacji Azure do obsługi wielu aplikacji sieci web na powitania tej samej bramy z hello portalu Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a>Skonfigurować istniejącą bramę aplikacji do obsługi wielu aplikacji sieci web

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

Obsługa wielu lokacji pozwala toodeploy więcej niż jednej aplikacji sieci web na powitania tej samej bramy aplikacji. Opiera się na obecność nagłówek hosta w hello przychodzące żądanie HTTP, toodetermine odbiornika, które będzie odbierać dane. odbiornik Hello następnie kieruje ruch puli zaplecza tooappropriate zgodnie z konfiguracją w definicji reguły hello hello bramy. W aplikacji sieci web z włączonym protokołem SSL bramy aplikacji polega na powitania oznaczenia nazwy serwera (SNI) rozszerzenia toochoose hello poprawne odbiornika dla ruchu w sieci web hello. Zazwyczaj jest używane, do obsługi wielu lokacji tooload równoważenie żądań dla pul serwerów zaplecza toodifferent domeny innej witryny sieci web. Podobnie wielu poddomen powitalne tej samej domeny katalogu głównego może być również obsługiwane na hello tej samej bramy aplikacji.

## <a name="scenario"></a>Scenariusz

W hello poniższy przykład, bramy aplikacji jest obsługę ruchu dla domeny contoso.com i fabrikam.com z dwóch pul serwerów zaplecza: contoso puli serwerów i puli serwerów firmy fabrikam. Podobne instalacja może być poddomeny używane toohost jak app.contoso.com i blog.contoso.com.

![Scenariusz w wielu lokacjach][multisite]

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu dodaje obsługę wielu lokacji tooan istniejącą bramę aplikacji. toocomplete ten scenariusz istniejącą bramę aplikacji wymaga toobe tooconfigure dostępne. Odwiedź stronę [utworzyć bramę aplikacji przy użyciu portalu hello](application-gateway-create-gateway-portal.md) toolearn jak toocreate brama aplikacji w warstwie podstawowa w portalu hello.

Brama aplikacji hello tooupdate wymagane czynności hello to Hello następujące:

1. Tworzenie pul zaplecza toouse dla każdej lokacji.
2. Utwórz odbiornik dla każdej lokacji obsługuje bramy aplikacji.
3. Utwórz toomap reguły każdego odbiornika z hello odpowiednie zaplecza.

## <a name="requirements"></a>Wymagania

* **Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello. wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP. Można także nazwę FQDN.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.
* **Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello. Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.
* **Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL). Dla bramy aplikacji obsługującej obejmujący wiele lokacji nazwy hosta i wskaźniki SNI są również został dodany.
* **Reguła:** reguły hello wiąże hello odbiornika, hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika. Reguły są przetwarzane w kolejności hello, są one wyświetlane, a ruch zostanie skierowany za pośrednictwem hello pierwszą regułę odpowiadającą niezależnie od szczegółowością. Na przykład jeśli masz przy użyciu odbiornika podstawowe reguły i zasady przy użyciu odbiornika obejmujący wiele lokacji zarówno na powitania sam port hello reguły z hello obejmujący wiele lokacji odbiornika musi być wymienione przed reguły hello przy hello odbiornika podstawowych, aby hello toofunction reguły obejmujący wiele lokacji jako Oczekiwano. 
* **Certyfikaty:** każdego odbiornika wymaga unikatowego certyfikatu, w tym przykładzie 2 odbiorników są tworzone dla wielu witryn. Dwa certyfikaty PFX i hello hasła dla nich muszą toobe utworzony.

## <a name="create-back-end-pools-for-each-site"></a>Tworzenie pul zaplecza dla każdej lokacji

Dla każdej lokacji puli zaplecza, że aplikacja obsługuje bramy jest potrzebne, w tym przypadku 2 są można utworzyć, jeden dla contoso11.com i jeden dla fabrikam11.com.

### <a name="step-1"></a>Krok 1

Przejdź tooan istniejącą bramę aplikacji w portalu Azure (https://portal.azure.com) hello. Wybierz **pul zaplecza** i kliknij przycisk **Dodaj**

![Dodawanie pul zaplecza][7]

### <a name="step-2"></a>Krok 2

Wprowadź informacje hello puli zaplecza hello **pool1**, dodawanie hello adresy ip lub nazwy FQDN dla serwerów zaplecza hello i kliknij przycisk **OK**

![Ustawienia pool1 puli wewnętrznej bazy danych][8]

### <a name="step-3"></a>Krok 3

W bloku pul zaplecza powitania kliknij **Dodaj** tooadd dodatkowe puli zaplecza **pool2**, dodawanie hello adresy ip lub nazwy FQDN dla serwerów zaplecza hello i kliknij przycisk **OK**

![Ustawienia pool2 puli wewnętrznej bazy danych][9]

## <a name="create-listeners-for-each-back-end"></a>Tworzenie odbiorników dla każdego zaplecza

Brama aplikacji w korzysta z protokołu HTTP 1.1 toohost nagłówków hosta więcej niż jednej witryny sieci Web na hello sam publiczny adres IP i portu. odbiornik podstawowe Hello utworzone w portalu hello nie zawiera tej właściwości.

### <a name="step-1"></a>Krok 1

Kliknij przycisk **odbiorników** hello istniejącą bramę aplikacji i kliknij przycisk **obejmujący wiele lokacji** tooadd hello pierwszy odbiornika.

![obiekty nasłuchujące bloku — omówienie][1]

### <a name="step-2"></a>Krok 2

Wprowadź informacje powitania dla odbiornika hello. W tym przykładzie protokół SSL jest skonfigurowany zakończenia, Utwórz nowy port serwera sieci Web. Przekaż toobe certyfikatu PFX hello używane do kończenia żądań SSL. Jedyną różnicą Hello tego bloku standardowe odbiornika podstawowe toohello porównywana blok jest hello nazwy hosta.

![odbiornik bloku właściwości][2]

### <a name="step-3"></a>Krok 3

Kliknij przycisk **obejmujący wiele lokacji** i utwórz inny odbiornik, zgodnie z opisem w poprzednim kroku hello hello drugiej witryny. Upewnij się, że toouse innego certyfikatu dla odbiornika drugi hello. Jedyną różnicą Hello tego bloku standardowe odbiornika podstawowe toohello porównywana blok jest hello nazwy hosta. Podanie informacji powitania dla odbiornika hello, a następnie kliknij przycisk **OK**.

![odbiornik bloku właściwości][3]

> [!NOTE]
> Tworzenie odbiorników w portalu Azure bramy aplikacji hello jest długotrwałych zadań, może upłynąć niektórych hello toocreate czasu dwa odbiorniki w tym scenariuszu. Gdy odbiorników pełną hello wyświetlane w portalu hello w powitania po obrazu:

![odbiornik — omówienie][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a>Tworzenie reguł toomap odbiorników toobackend pule

### <a name="step-1"></a>Krok 1

Przejdź tooan istniejącą bramę aplikacji w portalu Azure (https://portal.azure.com) hello. Wybierz **reguły** i wybrać istniejącą regułę domyślną hello **rule1** i kliknij przycisk **Edytuj**.

### <a name="step-2"></a>Krok 2

Wypełnij bloku zasady hello w powitania po obrazu. Wybieranie odbiornika pierwszy hello i pierwszej puli, a następnie klikając polecenie **zapisać** po zakończeniu.

![Edytuj istniejącą regułę][6]

### <a name="step-3"></a>Krok 3

Kliknij przycisk **podstawowe reguły** toocreate hello drugą regułę. Wypełnij formularz hello z hello drugi odbiornika, a drugie puli zaplecza, a następnie kliknij przycisk **OK** toosave.

![Dodawanie bloku podstawowe reguły][10]

W tym scenariuszu kończy się konfigurowanie istniejącą bramę aplikacji z obsługą wielu lokacji za pośrednictwem hello portalu Azure.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooprotect witryny sieci Web z [Application Gateway - zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
