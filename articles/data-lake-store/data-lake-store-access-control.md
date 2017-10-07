---
title: "aaaOverview kontroli dostępu w usłudze Data Lake Store | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu działania kontroli dostępu w usłudze Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a>Kontrola dostępu w usłudze Azure Data Lake Store

Azure Data Lake Store implementuje model kontroli dostępu, która pochodzi z systemu plików HDFS, który z kolei jest pochodną model kontroli dostępu POSIX hello. Ten artykuł zawiera podsumowanie hello podstawy hello model kontroli dostępu dla usługi Data Lake Store. toolearn więcej informacji na temat hello model kontroli dostępu do systemu plików HDFS, zobacz [przewodnik uprawnienia systemu plików HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).

## <a name="access-control-lists-on-files-and-folders"></a>Listy kontroli dostępu do plików i folderów

Istnieją dwa typy list kontroli dostępu (ACL) — **Listy ACL dostępu** i **Domyślne listy ACL**.

* **Dostęp do listy ACL**: obiekt tooan tych kontroli dostępu. Pliki i foldery mają listy ACL dostępu.

* **Domyślne listy ACL**: "szablon" listy kontroli dostępu skojarzone z folderem ustalić hello dostępu ACL dla wszystkie elementy podrzędne, które zostały utworzone w tym folderze. Pliki nie mają domyślnych list ACL.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

Zarówno listy ACL dostępu, jak i domyślnej listy ACL mają hello tej samej struktury.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> Zmiana hello domyślnej listy ACL na element nadrzędny nie ma wpływu na powitania dostępu lub domyślnej listy ACL elementy podrzędne, które już istnieją.
>
>

## <a name="users-and-identities"></a>Użytkownicy i tożsamości

Każdy plik i folder ma różne uprawnienia do tych tożsamości:

* Witaj, będącej właścicielem, jeśli użytkownik hello pliku
* Witaj będący właścicielem grupy
* Użytkownicy nazwani
* Grupy nazwane
* Wszyscy pozostali użytkownicy

Witaj tożsamości użytkowników i grup są tożsamości usługi Azure Active Directory (Azure AD). Chyba że określono inaczej, "użytkownika" w kontekście hello Data Lake Store może oznaczać albo użytkownika usługi Azure AD lub grupy zabezpieczeń usługi Azure AD.

## <a name="permissions"></a>Uprawnienia

Witaj uprawnień do obiektu systemu plików są **odczytu**, **zapisu**, i **Execute**, i mogą być używane w pliki i foldery, jak pokazano w poniższej tabeli hello:

|            |    Plik     |   Folder |
|------------|-------------|----------|
| **Odczyt (R)** | Można odczytać zawartości pliku hello | Wymaga **odczytu** i **Execute** toolist hello zawartość folderu hello|
| **Zapis (W)** | Można zapisać lub Dołącz plik tooa | Wymaga **zapisu** i **Execute** toocreate elementy podrzędne w folderze |
| **Wykonanie (X)** | Nie oznacza niczego w kontekście hello Data Lake Store | Elementy podrzędne hello tootraverse wymaganego folderu |

### <a name="short-forms-for-permissions"></a>Krótkie formy uprawnień

**RWX** jest używane tooindicate **odczytu i zapisu i wykonać**. Zmniejszoną formularza liczbowych istnieje w którym **odczytu = 4**, **zapisu = 2**, i **Execute = 1**, Suma hello reprezentuje hello uprawnienia. Poniżej przedstawiono kilka przykładów.

| Forma liczbowa | Forma krótka |      Co to oznacza     |
|--------------|------------|------------------------|
| 7            | RWX        | Odczyt (R) + zapis (W) + wykonanie (X) |
| 5            | R-X        | Odczyt (R) + wykonanie (X)         |
| 4            | R--        | Odczyt                   |
| 0            | ---        | Brak uprawnień         |


### <a name="permissions-do-not-inherit"></a>Uprawnienia nie są dziedziczone

W modelu POSIX stylu hello jest używany przez usługi Data Lake Store uprawnienia dla elementu są przechowywane w samym elemencie hello. Innymi słowy uprawnienia dla elementu nie może być dziedziczona z hello elementów nadrzędnych.

## <a name="common-scenarios-related-toopermissions"></a>Typowe scenariusze toopermissions pokrewne

Poniżej przedstawiono niektóre typowe scenariusze toohelp, zrozumieć, jakie uprawnienia są wymagane tooperform pewnych operacji na konto usługi Data Lake Store.

### <a name="permissions-needed-tooread-a-file"></a>Wymagane uprawnienia tooread pliku

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* Dla hello toobe pliku do odczytu, hello wywołujący musi **odczytu** uprawnienia.
* Dla wszystkich hello folderach hello struktury folderów zawierających plik hello, hello wywołujący musi **Execute** uprawnienia.

### <a name="permissions-needed-tooappend-tooa-file"></a>Plik tooa tooappend potrzebne uprawnienia

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* Dla hello toobe plik dołączany do, hello wywołujący musi **zapisu** uprawnienia.
* Dla wszystkich hello foldery, które zawierają hello pliku, hello wywołujący musi **Execute** uprawnienia.

### <a name="permissions-needed-toodelete-a-file"></a>Wymagane uprawnienia toodelete pliku

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* Dla folderu nadrzędnego hello, hello wywołujący musi **zapisu i wykonywania** uprawnienia.
* Dla wszystkich hello innych folderów w ścieżce pliku hello, hello wywołujący musi **Execute** uprawnienia.



> [!NOTE]
> Zapisu uprawnienia pliku hello nie są wymagane toodelete go tak długo, jak hello poprzednie dwa warunki są spełnione.
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a>Wymagane uprawnienia tooenumerate folderu

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* Dla tooenumerate folderu hello, hello wywołujący musi **Odczyt i wykonywanie** uprawnienia.
* Dla wszystkich hello foldery nadrzędne, hello wywołujący musi **Execute** uprawnienia.

## <a name="viewing-permissions-in-hello-azure-portal"></a>Wyświetlanie uprawnień w hello portalu Azure

Z hello **Eksploratora danych** bloku hello konta usługi Data Lake Store kliknij **dostępu** toosee hello listy ACL dla pliku lub folderu. Kliknij przycisk **dostępu** toosee hello listy ACL dla hello **katalogu** folder hello **mydatastore** konta.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

W tym bloku hello pierwsza sekcja zawiera omówienie hello uprawnienia użytkownika. (Hello zrzucie ekranu, użytkownik hello jest Bob). Po tym, że uprawnienia dostępu hello są wyświetlane. Po wykonaniu tej z hello **dostępu** bloku, kliknij przycisk **widoku uproszczonym** toosee hello prostsze widoku.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

Kliknij przycisk **widoku zaawansowanego** toosee hello bardziej zaawansowane widoku, gdy są pokazywane pojęcia hello domyślnej listy ACL, maska i administratora.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a>Witaj administratora

Nadtypem użytkownik ma hello większości prawa wszystkim użytkownikom hello w hello usługi Data Lake Store. Administrator:

* Zbyt uprawnieniami RWX**wszystkich** plików i folderów.
* Można zmienić uprawnienia hello plik lub folder.
* Można zmienić hello użytkownik będący właścicielem lub będący właścicielem grupy pliku lub folderu.

Na platformie Azure konto usługi Data Lake Store ma kilka ról platformy Azure, a w tym:

* Właściciele
* Współautorzy
* Czytelnicy

Wszyscy użytkownicy w hello **właścicieli** rolę dla konta usługi Data Lake Store jest automatycznie administratora dla tego konta. toolearn więcej, zobacz [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-configure.md).
Jeśli chcesz toocreate roli niestandardowej roli-— kontrola dostępu oparta na (rolach RBAC), która ma uprawnienia administratora musi hello toohave następujących uprawnień:
- Microsoft.DataLakeStore/accounts/Superuser/action
- Microsoft.Authorization/roleAssignments/write


## <a name="hello-owning-user"></a>Użytkownik będący właścicielem Hello

Hello użytkownika, który utworzył element hello jest automatycznie hello użytkownik hello element będący właścicielem. Użytkownik będący właścicielem może:

* Zmień uprawnienia hello pliku, który jest właścicielem.
* Zmiana będącej właścicielem grupy plików, która jest właścicielem tak długo, jak długo użytkownik będący właścicielem hello jest również członkiem grupy docelowej hello hello.

> [!NOTE]
> Użytkownik będący właścicielem Hello *nie* zmienić hello będącej właścicielem, jeśli użytkownik innego pliku należące do firmy. Tylko nadtypem użytkownicy mogą zmieniać hello będącej właścicielem, jeśli użytkownik pliku lub folderu.
>
>

## <a name="hello-owning-group"></a>Witaj będący właścicielem grupy

W hello listy ACL POSIX każdy użytkownik, jest skojarzona z "podstawowej grupy". Na przykład "Alicja" użytkownik może należeć toohello "Finanse" grupy. Alicja może również należeć toomultiple grupy, ale jedna grupa zawsze jest oznaczony jako swojej grupy podstawowej. W POSIX gdy Alicja tworzy plik hello grupy tego pliku będącej właścicielem, wartość grupy podstawowej tooher, czyli w tym przypadku "Finanse".

Podczas tworzenia nowego elementu systemu plików usługi Data Lake Store przypisuje toohello wartość grupy będącej właścicielem.

* **Przypadek 1**: folder główny hello "/". Ten folder jest tworzony wraz z kontem usługi Data Lake Store. W takim przypadku hello będący właścicielem grupy ustawiono toohello użytkownika, który utworzył konto hello.
* **Przypadek 2** (każdego innego litery): podczas tworzenia nowego elementu hello będący właścicielem grupy zostaną skopiowane z hello folderu nadrzędnego.

Witaj będący właścicielem grupy może zostać zmieniona przez:
* każdy administrator;
* Użytkownik, będący właścicielem, jeśli użytkownik będący właścicielem hello jest również członkiem grupy docelowej hello Hello.

## <a name="access-check-algorithm"></a>Algorytm kontroli dostępu

Witaj następującej ilustracji reprezentuje hello dostępu wyboru algorytmu dla kont usługi Data Lake Store.

![Algorytm list ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a>Maska Hello i "czynne uprawnienia"

Hello **maski** jest RWX wartość czyli dostęp toolimit używane dla **nazwani użytkownicy**, hello **grupy będącej właścicielem**, i **o nazwie grupy** czasie wykonywanie hello dostępu wyboru algorytmu. Poniżej przedstawiono podstawowe pojęcia hello hello maski.

* Maska Hello tworzy "czynne uprawnienia." Oznacza to modyfikuje uprawnienia hello w czasie hello kontroli dostępu.
* Maska Hello można edytować bezpośrednio przez właściciela pliku hello i nadtypem użytkowników.
* Maska Hello można usunąć uprawnienia toocreate hello czynne uprawnienia. Maska Hello *nie* dodać skuteczne toohello uprawnieniami.

Przyjrzyjmy się kilku przykładom. W hello poniższy przykład, maska hello ustawiono zbyt**RWX**, co oznacza, że maska hello nie powoduje usunięcia żadnych uprawnień. Hello czynnych uprawnień hello o nazwie użytkownika, grupy będącej właścicielem, a o nazwie grupy nie zostały zmienione podczas sprawdzania dostępu hello.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

W hello poniższy przykład, maska hello ustawiono zbyt**R X**. Oznacza to, że **wyłącza uprawnienia zapisu hello** dla **o nazwie użytkownika**, **grupy będącej właścicielem**, i **o nazwie grupy** w czasie hello dostępu Sprawdź.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

Odwołanie w tym miejscu jest gdzie hello maska dla pliku lub folderu będzie wyświetlana w hello portalu Azure.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> Dla nowego konta usługi Data Lake Store, maskę hello hello dostępu i domyślne listy ACL hello głównego folderu ("/"), domyślnie przyjmowana tooRWX.
>
>

## <a name="permissions-on-new-files-and-folders"></a>Uprawnienia do nowych plików i folderów

Gdy nowy plik lub folder utworzony na podstawie istniejącego folderu, określa hello domyślnej listy kontroli dostępu folderu nadrzędnego hello:

- domyślną listę ACL i listę ACL dostępu folderu podrzędnego;
- listę ACL dostępu pliku podrzędnego (pliki nie mają domyślnej listy ACL);

### <a name="hello-access-acl-of-a-child-file-or-folder"></a>Witaj dostępu ACL podrzędnego pliku lub folderu

Po utworzeniu podrzędnego pliku lub folderu nadrzędnego hello domyślne ACL jest kopiowana jako hello dostępu ACL hello podrzędnego pliku lub folderu. Ponadto jeśli **innych** użytkownik ma uprawnienia RWX nadrzędnego hello domyślnej listy kontroli dostępu, zostanie ono usunięte z elementu podrzędnego hello dostępu ACL.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

W większości przypadków informacje poprzednich hello są wszystkie potrzebne tooknow o jak element podrzędny dostępu ACL jest określana. Jednak jeśli znasz POSIX systemów i chcesz toounderstand szczegółowe jak uzyskuje się tej transformacji, zobacz sekcję hello [umask — w roli w tworzeniu hello dostępu ACL dla nowych plików i folderów](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) dalszej części tego artykułu.


### <a name="a-child-folders-default-acl"></a>Domyślna lista ACL folderu podrzędnego

Po utworzeniu folderu podrzędnego w folderze nadrzędnym ACL domyślny folder nadrzędny hello jest kopiowana za pośrednictwem jest folder podrzędny toohello domyślne ACL.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a>Zaawansowane tematy związane z listami ACL w usłudze Data Lake Store

Poniżej przedstawiono niektóre toohelp Tematy zaawansowane zrozumieć, jak listy kontroli dostępu są określone dla usługi Data Lake Store plików lub folderów.

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a>Umask — w roli w tworzeniu hello dostępu ACL dla nowych plików i folderów

W systemie standardem POSIX, ogólnej koncepcji hello jest tego umask — 9-bitową wartość folderu nadrzędnego hello używanej tootransform hello uprawnienia dla **użytkownik będący właścicielem**, **grupy będącej właścicielem**, i  **inne** na powitania dostępu ACL podrzędnego nowego pliku lub folderu. bity Hello umask — określić które tooturn usługi bits poza hello podrzędny element dostępu ACL. W związku z tym służy tooselectively zapobiec hello propagację uprawnień dla **użytkownik będący właścicielem**, **grupy będącej właścicielem**, i **innych**.

W systemie HDFS umask — Witaj jest zwykle w całym serwisie opcji konfiguracji, które są kontrolowane przez administratorów. Usługa Data Lake Store używa **maski umask obejmującej całe konto**, której nie można zmienić. Witaj w następującej tabeli przedstawiono hello maskowanie dla usługi Data Lake Store.

| Grupa użytkowników  | Ustawienie | Wpływ na listę ACL dostępu nowego elementu podrzędnego |
|------------ |---------|---------------------------------------|
| Użytkownik będący właścicielem | ---     | Brak wpływu                             |
| Grupa będąca właścicielem| ---     | Brak wpływu                             |
| Inne       | RWX     | Usuwanie uprawnień do odczytu, zapisu, wykonania         |

Hello następującej ilustracji przedstawiono ten umask — w akcji. Efekt netto Hello jest tooremove **odczytu i zapisu i wykonać** dla **innych** użytkownika. Ponieważ hello umask — nie określono bitów dla **użytkownik będący właścicielem** i **grupy będącej właścicielem**, te uprawnienia nie są przekształcane.

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a>bit trwałe Hello

bit trwałe Hello jest bardziej zaawansowanych funkcji systemu plików POSIX. W kontekście hello usługi Data Lake Store najprawdopodobniej tego bit trwałe hello będą potrzebne.

Witaj poniższej tabeli przedstawiono jak hello trwałe bitowa działa w usłudze Data Lake Store.

| Grupa użytkowników         | Plik    | Folder |
|--------------------|---------|-------------------------|
| Sticky bit **WYŁ.** | Brak wpływu   | Brak wpływu.           |
| Sticky bit **WŁ.**  | Brak wpływu   | Każda osoba, z wyjątkiem uniemożliwia **nadtypem użytkowników** i hello **użytkownik będący właścicielem** elementu podrzędnego, usuwanie lub zmiana nazwy elementu podrzędnego.               |

bit trwałe Hello nie jest wyświetlany w hello portalu Azure.

## <a name="common-questions-about-acls-in-data-lake-store"></a>Często zadawane pytania dotyczące list ACL w usłudze Data Lake Store

Oto kilka często zadawanych pytań dotyczących list ACL w usłudze Data Lake Store.

### <a name="do-i-have-tooenable-support-for-acls"></a>Obsługa tooenable listy ACL są dostępne?

Nie. Kontrola dostępu za pośrednictwem list ACL jest zawsze włączona dla konta usługi Data Lake Store.

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a>Jakie uprawnienia są wymagane toorecursively Usuń folder i jego zawartość?

* folder nadrzędny Hello musi mieć **zapisu i wykonywania** uprawnienia.
* Witaj toobe folderu usunięte i wymaga każdego folderu, to **odczytu i zapisu i wykonać** uprawnienia.

> [!NOTE]
> Nie należy, uprawnienia do zapisu plików toodelete w folderach. Ponadto hello folderu głównego "/" można **nigdy nie** można usunąć.
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a>Kto jest właścicielem hello pliku lub folderu?

Twórca Hello pliku lub folderu staje się właścicielem hello.

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a>Grupy, do której jest ustawiony jako hello-właściciel pliku lub folderu podczas tworzenia grupy?

Grupa będący właścicielem Hello jest kopiowana z hello-właściciel grupy hello folderu nadrzędnego, w których hello jest tworzony nowy plik lub folder.

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a>Jestem hello użytkownik pliku będący właścicielem, ale nie mam hello RWX uprawnienia, które należy. Co mam zrobić?

Hello będący właścicielem użytkownik może zmienić uprawnień hello hello pliku toogive się żadnych uprawnień RWX, które są im potrzebne.

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a>Podczas wyświetlania listy kontroli dostępu w portalu Azure hello widać nazwy użytkownika, ale za pośrednictwem interfejsów API, wyświetlane identyfikatory GUID, dlaczego?

Wpisy w hello listy ACL są przechowywane jako identyfikatory GUID, które odpowiadają toousers w usłudze Azure AD. Witaj interfejsów API zwraca hello identyfikatorów GUID, ponieważ jest. Witaj portalu Azure próbuje toouse łatwiejsze toomake listy ACL przez tłumaczenie hello identyfikatorów GUID do przyjaznych nazw, gdy jest to możliwe.

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a>Dlaczego czasami wyświetlane identyfikatory GUID w listy ACL hello Kiedy używam hello portalu Azure?

Identyfikator GUID jest wyświetlany, jeśli użytkownik hello nie istnieje w usłudze Azure AD już. Zazwyczaj dzieje się tak podczas hello użytkownik opuścił hello firmy lub jeśli ich konto zostało usunięte w usłudze Azure AD.

### <a name="does-data-lake-store-support-inheritance-of-acls"></a>Czy usługa Data Lake Store obsługuje dziedziczenie list ACL?

Nie.

### <a name="what-is-hello-difference-between-mask-and-umask"></a>Jaka jest różnica hello maski i umask —?

| maska | maska umask|
|------|------|
| Witaj **maski** właściwość jest dostępna na każdym plików i folderów. | Witaj **umask —** jest właściwością hello konta usługi Data Lake Store. To jest tylko jeden umask — hello usługi Data Lake Store.    |
| może się zmienić właściwości mask Hello pliku lub folderu w hello będącej właścicielem, użytkownika lub grupy plików lub nadtypem użytkownika będącej właścicielem. | Nie można zmodyfikować właściwości umask — Witaj przez dowolnego użytkownika, nawet administratora. Jest to niezmienna, stała wartość.|
| Właściwość maska Hello jest używany podczas algorytmu sprawdzania dostępu hello na toodetermine środowiska uruchomieniowego, czy użytkownik ma prawo tooperform hello na operacji na pliku lub folderu. Rola Hello maski hello jest toocreate "czynnych uprawnień" w czasie hello kontroli dostępu. | umask — Witaj nie jest używany podczas sprawdzania dostępu w ogóle. umask — Hello jest używany toodetermine hello dostępu ACL nowych elementów podrzędnych folderu. |
| Maska Hello jest 3-bitową wartość RWX, która dotyczy użytkownika toonamed, nazwaną grupę i będący właścicielem użytkownika w czasie hello kontroli dostępu.| Witaj umask — jest wartość 9-bitowego, która dotyczy toohello będącej właścicielem, jeśli użytkownik będący właścicielem grupy, a **innych** nowego elementu podrzędnego.|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a>Gdzie można dowiedzieć się więcej na temat modelu kontroli dostępu POSIX?

* [Listy kontroli dostępu w modelu POSIX w systemie Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [Przewodnik po uprawnieniach systemu plików HDFS](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [POSIX — często zadawane pytania](http://www.opengroup.org/austin/papers/posix_faq.html)

* [POSIX 1003.1 2008](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [POSIX 1003.1 2013](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [POSIX 1003.1 2016](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [Listy ACL modelu POSIX w systemie Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs)

* [Listy ACL korzystające z list kontroli dostępu w systemie Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a>Zobacz też

* [Omówienie usługi Azure Data Lake Store](data-lake-store-overview.md)
