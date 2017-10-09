---
title: "aaaAdd SSL certyfikatów tooyour aplikacji usługi Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd SSL certyfikatów tooyour aplikacji usługi app Service."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>Kup i skonfiguruj certyfikat SSL dla usługi Azure App Service

W tym samouczku zostanie zabezpieczenia aplikacji sieci web po zakupie certyfikatu SSL dla Twojej  **[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, bezpieczne przechowywanie ich w [usługi Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)i kojarzenie go z domeny niestandardowej.

## <a name="step-1---log-in-tooazure"></a>Krok 1 — Logowanie tooAzure

Zaloguj się za toohello portalu Azure w http://portal.azure.com

## <a name="step-2---place-an-ssl-certificate-order"></a>Krok 2 — złóż zamówienie certyfikat SSL

Kolejność certyfikat SSL można umieścić przez utworzenie nowej [certyfikatu usługi aplikacji](https://portal.azure.com/#create/Microsoft.SSL) w hello **portalu Azure**.

![Tworzenie certyfikatu](./media/app-service-web-purchase-ssl-web-site/createssl.png)

Wprowadź przyjazną nazwę w polu **nazwa** certyfikatów dla ustawienia zabezpieczeń SSL, a następnie wprowadź hello **nazwy domeny**

> [!NOTE]
> To jest jednym z najważniejszych części procesu zakupu hello hello. Upewnij się, że tooenter Popraw nazwę hosta (domena niestandardowych), które mają tooprotect z tym certyfikatem. **NIE** Dołącz hello nazwy hosta z sieci Web. 
>

Wybierz użytkownika **subskrypcji**, **grupy zasobów**, i **certyfikatu jednostki SKU**

> [!WARNING]
> Certyfikaty usługi aplikacji można używać tylko przez inne usługi aplikacji w ramach hello tej samej subskrypcji.  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>Krok 3 — magazynu hello certyfikatu w magazynie kluczy Azure

> [!NOTE]
> [Magazyn kluczy](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) jest usługą platformy Azure, która pomaga w zabezpieczaniu kluczy kryptograficznych i kluczy tajnych używanych przez usługi i aplikacje w chmurze.
>

Po zakończeniu hello zakupu certyfikatów SSL, należy tooopen [certyfikaty usługi aplikacji](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) bloku zasobów.

![Wstaw obraz gotowy toostore w KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

Można zauważyć, że stan certyfikatu jest **"Oczekujące wystawiania"** jako obejmuje kilka kroków więcej potrzebujesz toocomplete przed rozpoczęciem używania tego certyfikatu.

Kliknij przycisk **Konfiguracja certyfikatów** wewnątrz bloku właściwości certyfikatu, kliknij polecenie **krok 1: magazyn** toostore ten certyfikat w magazynie kluczy Azure.

Z **klucza magazynu stanu** bloku, kliknij przycisk **klucza magazynu repozytorium** toochoose istniejących toostore Key Vault tego certyfikatu **lub Utwórz nowy magazyn kluczy** toocreate nowy klucz magazynu w tej samej subskrypcji i grupie zasobów.

> [!NOTE]
> Usługa Azure Key Vault ma minimalny opłat do przechowywania certyfikatu.
> Aby uzyskać więcej informacji, zobacz  **[szczegóły cennika usługi Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.
>

Po wybraniu hello toostore repozytorium magazynu klucza tego certyfikatu, hello **magazynu** opcji powinny być widoczne Powodzenie.

![Wstaw obraz sukcesu magazynu w KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>Krok 4. Sprawdź hello własność domeny

> [!NOTE]
> Istnieją trzy typy weryfikację domeny obsługiwane przez certyfikaty usługi aplikacji: domeny poczty, ręczne weryfikacji. Te omówiono bardziej szczegółowo w hello [zaawansowane sekcji](#advanced).

Z hello sam **Konfiguracja certyfikatów** bloku używane w kroku 3, kliknij przycisk **krok 2: Sprawdź**.

**Weryfikacja domeny** proces najodpowiedniejszym hello **tylko w przypadku** masz  **[zakupionych domeny niestandardowej z usługi aplikacji Azure.](custom-dns-web-site-buydomains-web-app.md)**
Polecenie **Sprawdź** przycisk toocomplete ten krok.

![Wstaw obraz weryfikację domeny](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

Po kliknięciu przycisku **Sprawdź**, użyj hello **Odśwież** przycisku do hello **Sprawdź** opcji powinny być widoczne Powodzenie.

![Wstaw obraz sprawdzić, czy w KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>Krok 5 — przypisać tooApp certyfikatu usługi aplikacji

> [!NOTE]
> Przed wykonaniem kroków hello w tej sekcji, muszą mieć skojarzone nazwy domeny niestandardowej z aplikacją. Aby uzyskać więcej informacji, zobacz  **[Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web.](app-service-web-tutorial-custom-domain.md)**
>

W hello  **[portalu Azure](https://portal.azure.com/)**, kliknij przycisk hello **usługi aplikacji** opcję na powitania po lewej stronie hello.

Kliknij nazwę hello toowhich Twojej aplikacji ma tooassign tego certyfikatu.

W hello **ustawienia**, kliknij przycisk **certyfikaty SSL**.

Kliknij przycisk **Importowanie certyfikatu usługi aplikacji** i hello wybierz certyfikat, które zostały zakupione.

![Wstaw obraz Importowanie certyfikatu](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

W hello **powiązania ssl** sekcji kliknij na **dodać powiązania**, hello listę rozwijaną tooselect hello domeny nazwa toosecure za pomocą protokołu SSL i hello toouse certyfikatu. Można również wybrać czy toouse  **[oznaczenia nazwy serwera (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  lub adresu IP na podstawie protokołu SSL.

![Wstaw obraz z wiązaniami SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

Kliknij przycisk **Dodawanie powiązania** toosave hello zmian i Włącz protokół SSL.

> [!NOTE]
> W przypadku wybrania **IP na podstawie SSL** i domeny niestandardowej jest konfigurowana przy użyciu rekordu A, musisz wykonać następujące dodatkowe kroki hello. Te omówiono bardziej szczegółowo w hello [zaawansowane sekcji](#Advanced).

W tym momencie możesz powinno być możliwe toovisit przy użyciu aplikacji `HTTPS://` zamiast `HTTP://` tooverify, który hello certyfikat został poprawnie skonfigurowany.

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>Krok 6 — zadania związane z zarządzaniem

### <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>Advanced

### <a name="verifying-domain-ownership"></a>Weryfikowanie własność domeny

Istnieją dwa typy więcej weryfikacji domeny obsługiwane przez certyfikaty usługi aplikacji: poczty i weryfikacja ręcznego.

#### <a name="mail-verification"></a>Weryfikacja poczty

Weryfikacja e-mail została już wysłana toohello adresy E-mail skojarzony z tym domeny niestandardowej.
Witaj toocomplete E-mail weryfikacji, otwórz hello poczty e-mail i kliknij łącze weryfikacji hello.

![Wstaw obraz Weryfikacja adresu e-mail](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

Jeśli potrzebujesz tooresend hello weryfikacji w wiadomości e-mail, kliknij przycisk hello **ponowne wysyłanie wiadomości E-mail** przycisku.

#### <a name="manual-verification"></a>Weryfikacja ręczna

> [!IMPORTANT]
> HTML strony sieci Web weryfikacji (dotyczy tylko wersji Standard certyfikatu)
>

1. Utwórz plik HTML o nazwie **"starfield.html"**

1. Zawartość tego pliku powinna być hello dokładną nazwę hello domeny weryfikacji tokenu. (Możesz skopiować hello token z hello bloku stanu weryfikacji domeny)

1. Przekazywanie tego pliku w katalogu głównym powitania serwera sieci web hello hosting domeny`/.well-known/pki-validation/starfield.html`

1. Kliknij przycisk **Odśwież** tooupdate stanu certyfikatu powitania po zakończeniu weryfikacji. Może upłynąć kilka minut, aż toocomplete weryfikacji.

> [!TIP]
> Sprawdź, czy w terminalu przy użyciu `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello odpowiedź powinna zawierać hello `<verification-token>`.

#### <a name="dns-txt-record-verification"></a>Weryfikacja rekordu DNS TXT

1. Korzystanie z Menedżera DNS utworzyć rekord TXT na powitania `@` poddomeny z domeny weryfikacji tokenu toohello takie same wartości.
1. Kliknij przycisk **"Odśwież"** tooupdate hello stanu certyfikatu po zakończeniu weryfikacji.

> [!TIP]
> Należy toocreate rekord TXT na `@.<domain>` o wartości `<verification-token>`.

### <a name="assign-certificate-tooapp-service-app"></a>Przypisz tooApp certyfikatu usługi aplikacji

W przypadku wybrania **IP na podstawie SSL** i domeny niestandardowej jest konfigurowana przy użyciu rekordu A, musisz wykonać następujące dodatkowe kroki hello:

Po skonfigurowaniu adresów IP na podstawie powiązania SSL, dedykowany adres IP jest przypisany tooyour aplikacji. Ten adres IP można znaleźć na powitania **domeny niestandardowe** w obszarze Ustawienia aplikacji, nad hello **Hostnames** sekcji. Jest on wyświetlany jako **zewnętrzny adres IP**

![Wstaw obraz z protokołu SSL z adresu IP](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

Należy pamiętać, że ten adres IP jest inny niż hello wirtualnego adresu IP używane wcześniej rekord A hello tooconfigure dla danej domeny. Jeśli są skonfigurowane toouse SNI na podstawie protokołu SSL lub nie są skonfigurowane toouse SSL, żaden adres jest wymienionych dla tego wpisu.

Za pomocą narzędzi hello dostarczonych przez rejestratora nazw domen, zmodyfikuj hello rekordu adresu IP toohello toopoint nazwy domeny niestandardowej hello w poprzednim kroku.

## <a name="rekey-and-sync-hello-certificate"></a>Ponowne tworzenie klucza i zsynchronizuj hello certyfikatu

Jeśli kiedykolwiek zajdzie tooRekey certyfikat, wybierz **ponowne tworzenie klucza i zsynchronizuj** opcję **właściwości certyfikatu** bloku.

Kliknij przycisk **ponowne tworzenie klucza** przycisk tooinitiate hello procesu. Ten proces może potrwać toocomplete 1 – 10 minut.

![Wstaw obraz ponowne tworzenie klucza protokołu SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

Ponowne tworzenie klucza certyfikatu przedstawia hello certyfikatu przy użyciu nowego certyfikatu wystawionego przez urząd certyfikacji hello.

## <a name="next-steps"></a>Następne kroki

* [Dodawanie sieci dostarczania zawartości](app-service-web-tutorial-content-delivery-network.md)