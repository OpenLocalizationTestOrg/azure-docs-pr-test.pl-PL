---
title: "aaaManage magazynu kluczy Azure przy użyciu interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Korzystanie z tego samouczka tooautomate typowych zadań usługi Key Vault, za pomocą hello interfejsu wiersza polecenia"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a>Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia

Usługa Azure Key Vault jest dostępna w większości regionów. Aby uzyskać więcej informacji, zobacz hello [cennik usługi Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Wprowadzenie

Użyj tego samouczka toohelp otrzymasz wprowadzenie do usługi Azure Key Vault toocreate wzmocnionego kontenera (magazynu) na platformie Azure, toostore i zarządzanie nimi kluczy kryptograficznych i kluczy tajnych na platformie Azure. Przeprowadza użytkownika przez proces hello przy użyciu interfejsu wiersza polecenia platformy Azure i Platform toocreate magazynu, który zawiera klucz lub hasło, które następnie można za pomocą aplikacji Azure. Następnie pokaże Ci, jak aplikacja może następnie użyć tego klucza lub hasła.

**Szacowany czas toocomplete:** 20 minut

> [!NOTE]
> Ten samouczek nie zawiera instrukcji dotyczących sposobu toowrite hello aplikacji Azure, która zawiera jeden z kroków hello, który pokazuje, jak tooauthorize toouse aplikacji klucza lub klucza tajnego klucza hello magazynu.
> 
> Obecnie nie można skonfigurować usługi Azure Key Vault w hello portalu Azure. Użyj tych instrukcji Międzyplatformowego interfejsu wiersza polecenia. Lub, aby uzyskać instrukcje programu Azure PowerShell, zobacz [tym równoważnym samouczku](key-vault-get-started.md).
> 
> 

Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka, musi mieć następujące hello:

* TooMicrosoft subskrypcji Azure. Jeśli nie masz, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial).
* Interfejs wiersza polecenia w wersji od 0.9.1 lub nowszym. tooinstall hello najnowszej wersji i połącz tooyour subskrypcji platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia platformy Azure i Platform hello](../cli-install-nodejs.md).
* Aplikacja, która będzie skonfigurowany toouse hello klucza lub hasła utworzonego w ramach tego samouczka. Przykładowa aplikacja jest dostępna z hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343). Aby uzyskać instrukcje Zobacz hello towarzyszący plik Readme.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Uzyskiwanie pomocy z interfejsu wiersza polecenia platformy Azure i Platform

Ten samouczek zakłada, że znasz hello interfejsu wiersza polecenia (Bash, terminali, wiersza polecenia)

Witaj — pomoc lub -h parametr może być używany dla określonych poleceń tooview pomocy. Alternatywnie hello azure help [polecenie] [opcje] format może być również używane tooreturn hello tych samych informacji. Na przykład następujące hello polecenia wszystkie powrotu hello tych samych informacji:

    azure account set --help

    azure account set -h

    azure help account set

W przypadku wątpliwości dotyczących parametrów hello potrzebne za pomocą polecenia można znaleźć przy użyciu toohelp — pomoc, -h lub azure help [polecenie].

Możesz przeczytać następujące samouczki tooget zapoznać się z usługą Azure Resource Manager w interfejsu wiersza polecenia platformy Azure i Platform hello:

* [Jak tooinstall i Konfigurowanie interfejsu wiersza polecenia i Platform Azure](../cli-install-nodejs.md)
* [Przy użyciu interfejsu wiersza polecenia platformy Azure i Platform z usługą Azure Resource Manager](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a>Połącz tooyour subskrypcji

toolog za pomocą konta organizacyjnego, hello Użyj następującego polecenia:

    azure login -u username -p password

lub jeśli użytkownik chce toolog wpisując interakcyjnego

    azure login

> [!NOTE]
> Metoda logowania Hello działa tylko za pomocą konta organizacyjnego. Konta organizacyjnego jest użytkownik, który jest zarządzanych przez swoją organizację, a zdefiniowane w dzierżawie usługi Azure Active Directory w organizacji.
> 
> 

Jeśli aktualnie nie masz konta organizacyjnego i przy użyciu toolog konta Microsoft w tooyour subskrypcji platformy Azure, można łatwo utworzyć go przy użyciu hello następujące kroki.

1. Logowania toohello logowania toohello [portalu zarządzania Azure](https://manage.windowsazure.com/)i kliknij na usłudze Active Directory.
2. Jeśli katalog nie istnieje, wybierz opcję tworzenia katalogu i podaj hello wymagane informacje.
3. Wybierz katalog, a następnie dodaj nowego użytkownika. Ten nowy użytkownik jest kontem organizacyjnym. Podczas tworzenia hello hello użytkownika należy podać zarówno adres e-mail dla hello użytkownika i hasło tymczasowe. Zapisz te informacje, które jest używane w kolejnym kroku.
4. W portalu hello wybierz ustawienia, a następnie wybierz administratorów. Wybierz opcję Dodaj i dodania nowego użytkownika hello jako współadministrator. Dzięki temu toomanage konta organizacyjnego hello subskrypcji platformy Azure.
5. Na koniec Wyloguj hello portalu Azure i następnie ponowne zalogowanie przy użyciu nowego konta organizacyjnego hello. Jeśli jest to hello pierwszego czasu logowania się za pomocą tego konta, będzie toochange zostanie wyświetlony monit o hasło hello.

Aby uzyskać więcej informacji o platformie Microsoft Azure za pomocą konta organizacyjnego, zobacz [utworzyć konto Microsoft Azure jako organizacja](../active-directory/sign-up-organization.md).

Jeśli masz wiele subskrypcji i chcesz toospecify określonych toouse jeden dla usługi Azure Key Vault, wpisz powitania po toosee hello subskrypcje dla swojego konta:

    azure account list

Następnie toospecify hello subskrypcji toouse, wpisz:

    azure account set <subscription name>

Aby uzyskać więcej informacji o konfigurowaniu Azure Międzyplatformowego interfejsu wiersza polecenia, zobacz [jak tooInstall i Konfigurowanie interfejsu wiersza polecenia i Platform Azure](../cli-install-nodejs.md).

## <a name="switch-toousing-azure-resource-manager"></a>Przełącz toousing usługi Azure Resource Manager
Hello Key Vault wymaga usługi Azure Resource Manager, dlatego wpisz powitania po tryb usługi Resource Manager tooAzure tooswitch:

    azure config mode arm

## <a name="create-a-new-resource-group"></a>Utworzenie nowej grupy zasobów
Podczas korzystania z usługi Azure Resource Manager, wszystkie powiązane zasoby są tworzone wewnątrz grupy zasobów. W tym samouczku utworzymy nową grupę zasobów "ContosoResourceGroup".

    azure group create 'ContosoResourceGroup' 'East Asia'

pierwszy parametr Hello jest nazwa grupy zasobów i hello drugi parametr jest hello lokalizacji. Dla lokalizacji, użyj polecenia hello `azure location list` tooidentify jak toospecify alternatywną lokalizację toohello co w tym przykładzie. Aby uzyskać więcej informacji, wpisz:`azure help location`

## <a name="register-hello-key-vault-resource-provider"></a>Rejestrowanie dostawcy zasobów usługi Key Vault hello
Upewnij się, że tego dostawcy zasobów usługi Key Vault jest zarejestrowany w ramach Twojej subskrypcji:

`azure provider register Microsoft.KeyVault`

Wymagane tylko toobe wykonywane raz dla subskrypcji.

## <a name="create-a-key-vault"></a>Tworzenie magazynu kluczy

Użyj hello `azure keyvault create` toocreate polecenie magazynu kluczy. Ten skrypt ma trzy obowiązkowe parametry: Nazwa grupy zasobów, nazwa magazynu kluczy i hello lokalizacji geograficznej.

Na przykład jeśli używasz nazwy magazynu hello ContosoKeyVault, nazwę grupy zasobów hello ContosoResourceGroup i hello lokalizacji Azja Wschodnia, wpisz:

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

Hello dane wyjściowe tego polecenia pokazują właściwości magazynu kluczy hello nowo utworzony. Witaj dwie najważniejsze właściwości to:

* **Nazwa**: W przykładzie hello jest ContosoKeyVault. Ta nazwa będzie używana do innych poleceń cmdlet usługi Key Vault.
* **vaultUri**: W przykładzie hello jest https://contosokeyvault.vault.azure.net. Aplikacje korzystające z magazynu za pomocą jego interfejsu API REST muszą używać tego identyfikatora URI.

Konto platformy Azure jest teraz autoryzowanych tooperform żadnych operacji dla tego klucza magazynu. Nikt inny nie jest do tego upoważniony.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Dodawanie klucza lub magazynu kluczy tajnych toohello

Usługa Azure Key Vault toocreate klucza chronionego przez oprogramowanie dla Ciebie, należy użyć hello `azure key create` polecenia i wpisz następujące hello:

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

Jednak jeśli masz istniejący klucz w pliku PEM, zapisany jako plik lokalny w pliku o nazwie softkey.pem, które mają tooAzure tooupload Key Vault, wpisz powitania po klucz hello tooimport z hello. Plik PEM, który chroni klucz hello przez oprogramowanie w usłudze Key Vault hello:

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

Teraz możesz odwoływać się hello klucz został utworzony lub przekazany tooAzure Key Vault, za pomocą jego identyfikatora URI. Użyj **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways uzyskać hello bieżącą wersję oraz **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget tę konkretną wersję.

tooadd magazynu toohello tajny, który jest hasłem o nazwie SQLPassword i ma hello wartość Pa$ $w0rd tooAzure Key Vault hello typu następujące:

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

Teraz możesz odwoływać się to hasło, dodać tooAzure Key Vault, za pomocą jego identyfikatora URI. Użyj **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways uzyskać hello bieżącą wersję oraz **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget tę konkretną wersję.

Teraz wyświetlić hello klucz lub klucz tajny, który został właśnie utworzony:

* tooview Twojego klucza, wpisz:`azure keyvault key list --vault-name 'ContosoKeyVault'`
* tooview tajne, typu:`azure keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>Rejestrowanie aplikacji w usłudze Azure Active Directory

Ten krok będzie zazwyczaj wykonywany przez programistę na innym komputerze. Nie jest określonym tooAzure Key Vault, ale został tu zawarty, aby informacje były kompletne.

> [!IMPORTANT]
> toocomplete hello samouczek, Twoje konto, Magazyn hello i aplikacji hello, która zarejestruje się w tym kroku musi być w hello tego samego katalogu Azure.
> 
> 

Aplikacje używające magazynu kluczy muszą zostać uwierzytelnione przy użyciu tokenu z usługi Azure Active Directory. toodo hello, właściciel aplikacji hello aplikacji hello najpierw należy zarejestrować w usłudze Azure Active Directory. Na powitania koniec rejestracji właściciel aplikacji hello pobiera hello następujące wartości:

* **Identyfikator aplikacji** (znanej także jako identyfikator klienta) i **klucz uwierzytelniania** (znanej także jako hello wspólny klucz tajny). Witaj, aplikacja musi przedstawić obie te wartości tooAzure usługi Active Directory, tooget tokenu. Jak aplikacja hello jest skonfigurowany toodo, który zależy od aplikacji hello. Dla usługi Key Vault Przykładowa aplikacja hello hello właściciel aplikacji ustawia te wartości w pliku app.config hello.

Aplikacja hello tooregister w usłudze Azure Active Directory:

1. Zaloguj się toohello portalu Azure.
2. Powitania po lewej stronie, kliknij przycisk **usługi Active Directory**, a następnie wybierz katalog hello, w którym będzie rejestrować aplikacji. <br> <br> 

>[!NOTE] 
> Musisz wybrać hello tym samym katalogu, który zawiera hello subskrypcji platformy Azure, z którym zostanie utworzony magazyn kluczy. Jeśli nie znasz katalog ten jest, kliknij przycisk **ustawienia**zidentyfikować hello subskrypcji, z którym zostanie utworzony magazyn kluczy i w ostatniej kolumnie hello wyświetlana nazwa hello Uwaga hello katalogu.

3. Kliknij pozycję **APLIKACJE**. Brak aplikacja nie została dodana tooyour katalogu, ta strona wyświetli tylko hello **Dodaj aplikację** łącza. Kliknij łącze hello, lub też kliknąć hello **dodać** na powitania paska poleceń.
4. W hello **Dodawanie aplikacji** kreatora, na powitania **co chcesz toodo?** kliknij przycisk **Dodaj aplikację moją organizację**.
5. Na powitania **Powiedz nam o aplikacji** , określ nazwę aplikacji i wybrać opcję **interfejsu API sieci WEB i/lub aplikacji sieci WEB** (hello domyślną). Kliknij ikonę dalej hello.
6. Na powitania **właściwości aplikacji** Określ hello **adres URL logowania** i **identyfikator URI aplikacji** dla aplikacji sieci web. Jeśli aplikacja nie ma tych wartości, możesz je wymyślić na potrzeby tego kroku (na przykład możesz wpisać adres http://test1.contoso.com w obu polach). Nie ma znaczenia, czy taka strona istnieje; ważne jest, aplikacja hello identyfikator URI dla każdej aplikacji jest różne dla każdej aplikacji w katalogu. katalog Hello używa tego ciągu tooidentify aplikacji.
7. Kliknij przycisk toosave pełną ikona hello zmiany w Kreatorze hello.
8. Na stronie Szybki Start powitania kliknij **Konfiguruj**.
9. Przewiń toohello **klucze** sekcji, wybierz czas trwania hello, a następnie kliknij przycisk **ZAPISAĆ**. Strona Hello odświeżona i pojawi się wartość klucza. Należy skonfigurować aplikację za pomocą wartości klucza i hello **identyfikator klienta** wartość. (Instrukcje dotyczące tej konfiguracji będą specyficzne dla aplikacji).
10. Skopiuj wartość Identyfikatora powitania klienta z tej strony, który będzie używany w hello następny krok tooset uprawnień dotyczących magazynu.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Autoryzowanie hello aplikacji toouse hello klucza lub klucza tajnego
Witaj tooaccess aplikacji hello tooauthorize klucza lub klucza tajnego w magazynie hello, użyj hello `azure keyvault set-policy` polecenia.

Na przykład jeśli nazwa Twojego magazynu to ContosoKeyVault i hello aplikacji ma tooauthorize ma identyfikator klienta 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed i toodecrypt aplikacji hello tooauthorize i zaloguj się za pomocą kluczy w magazynie, a następnie uruchom hello następujące:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> Uruchamiasz w wierszu polecenia systemu Windows, należy zastąpić pojedynczych cudzysłowów podwójnych cudzysłowów i również escape hello wewnętrzny podwójnego cudzysłowu. Na przykład: "[\"odszyfrować\",\"znak\"]".
> 
> 

Jeśli chcesz tooauthorize tego samego hasła tooread aplikacji w magazynie, uruchom następujące hello:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Jeśli chcesz, aby toouse sprzętowego modułu zabezpieczeń (HSM)
Dla dodatkowego bezpieczeństwa możesz zaimportować lub wygenerować klucze w sprzętowych modułów zabezpieczeń (HSM), które nigdy nie opuszczają granicy modułów HSM hello. Witaj sprzętowych modułów zabezpieczeń są FIPS 140-2 poziom 2 zweryfikowany. Jeśli te wymagania nie odnoszą się tooyou, Pomiń tę sekcję i przejdź zbyt[usunąć hello magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate klucze chronionego przez moduł HSM musi mieć subskrypcję magazynu obsługującą klucze chronione przez moduł HSM.

Podczas tworzenia hello keyvault, Dodaj parametr "sku" hello:

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

Można dodać klucze chronione oprogramowaniem (jak pokazano wcześniej) i magazynu toothis klucze chronione przez moduł HSM. toocreate klucza chronionego przez moduł HSM, zestaw hello przeznaczenia parametru too'HSM ":

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

Możesz użyć hello następujące polecenia tooimport klucz z pliku PEM na tym komputerze. To polecenie importuje klucz hello do sprzętowych modułów zabezpieczeń w usłudze Key Vault hello:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

Witaj następne polecenie importuje "bring your own key" (BYOK) pakietu. Umożliwia generowanie klucza w lokalnym module HSM i przeniesienie go tooHSMs w hello usługi Key Vault bez opuszczania hello granic modułu HSM klucz hello:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

Aby uzyskać szczegółowe instrukcje dotyczące toogenerate pakietu BYOK, zobacz [jak toouse HSM-Protected klucze w usłudze Azure Key Vault](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Usuń hello magazynu kluczy oraz skojarzonych kluczy i kluczy tajnych
Jeśli nie są już potrzebne hello magazynu kluczy oraz klucz hello lub klucz tajny, który zawiera można usunąć magazynu kluczy hello za pomocą polecenia delete keyvault hello azure:

    azure keyvault delete --vault-name 'ContosoKeyVault'

Lub usunięciem całej grupy zasobów platformy Azure, w tym magazynie kluczy hello i inne zasoby, które zostały dodane do tej grupy:

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Inne polecenia interfejsu wiersza polecenia platformy Azure i Platform
Inne polecenia użytkownik może przydatne do zarządzania usługą Azure Key Vault.

To polecenie wyświetla tabelaryczny widok wszystkich kluczy i wybranych właściwości:

    azure keyvault key list --vault-name 'ContosoKeyVault'

To polecenie wyświetla pełną listę właściwości dla określonego klucza hello:

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

To polecenie wyświetla tabelaryczny widok wszystkich nazw kluczy tajnych i wybranych właściwości:

    azure keyvault secret list --vault-name 'ContosoKeyVault'

Poniżej przedstawiono przykładowy sposób tooremove określonego klucza:

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

Poniżej przedstawiono przykładowy sposób tooremove określonego klucza tajnego:

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a>Następne kroki
Odwołania dotyczące programowania, zobacz [hello przewodnik dewelopera usługi Azure Key Vault](key-vault-developers-guide.md).

