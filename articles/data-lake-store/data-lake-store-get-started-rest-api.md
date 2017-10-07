---
title: "wprowadzenie do usługi Data Lake Store tooget interfejsu API REST hello aaaUse | Dokumentacja firmy Microsoft"
description: "Używać interfejsów API REST WebHDFS tooperform operacji w usłudze Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem interfejsów API REST
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Zestaw SDK platformy .NET](data-lake-store-get-started-net-sdk.md)
> * [Zestaw SDK Java](data-lake-store-get-started-java-sdk.md)
> * [Interfejs API REST](data-lake-store-get-started-rest-api.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

W tym artykule dowiesz się, jak toouse interfejsów API REST WebHDFS i Data Lake magazynu REST API tooperform konto zarządzania, a także operacji systemu plików w usłudze Azure Data Lake Store. Usługa Azure Data Lake Store ujawnia swoje interfejsy API REST w celu wykonywania operacji zarządzania kontem. Jednak usługa Data Lake Store jest zgodna z systemem plików HDFS i ekosystemem Hadoop, dlatego umożliwia korzystanie z interfejsów API REST WebHDFS w celu wykonywania operacji systemu plików.

> [!NOTE]
> Aby uzyskać szczegółowe informacje na powitania Obsługa interfejsu API REST usługi Data Lake Store, zobacz [dokumentacja interfejsu API REST magazynu Azure Data Lake](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Utworzenie aplikacji usługi Azure Active Directory**. Używasz hello Azure AD aplikacji tooauthenticate hello usługi Data Lake Store aplikacji z usługą Azure AD. Istnieją różne podejścia tooauthenticate z usługą Azure AD, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**. Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). W tym artykule wykorzystano toodemonstrate cURL jak wywołuje toomake interfejsu API REST względem konta usługi Data Lake Store.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>W jaki sposób uwierzytelniać za pomocą usługi Azure Active Directory?
Możesz użyć dwóch tooauthenticate podejścia przy użyciu usługi Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Uwierzytelnianie użytkowników końcowych (interakcyjne)
W tym scenariuszu aplikacja hello monituje hello toolog użytkownika w i wszystkie operacje hello są wykonywane w kontekście hello hello użytkownika. Wykonaj następujące kroki, aby przeprowadzić uwierzytelnianie interakcyjne hello.

1. Za pomocą aplikacji Przekieruj toohello użytkownika hello następującego adresu URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<Identyfikator URI PRZEKIEROWANIA > musi toobe zakodowanego do użycia w adresie URL. Dlatego w celu zapisania adresu https://localhost użyj ciągu `https%3A%2F%2Flocalhost`
   > 
   > 
   
    Hello w celu tego samouczka możesz zastąpić symbole zastępcze hello w adresie URL hello powyżej i wklej go w pasku adresu przeglądarki sieci web. Będzie przekierowany tooauthenticate przy użyciu logowania do systemu Azure. Po pomyślnym zalogowaniu odpowiedź hello jest wyświetlany w pasku adresu przeglądarki hello. odpowiedź Hello będą hello następującego formatu:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Przechwyć hello kod autoryzacji z odpowiedzi hello. W tym samouczku możesz skopiować kod autoryzacji hello z paska adresu przeglądarki sieci web hello hello i przekazać go w hello POST żądania toohello punktu końcowego tokena, jak pokazano poniżej:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > W takim przypadku hello \<REDIRECT-URI > nie trzeba kodować.
   > 
   > 
3. odpowiedź Hello jest obiekt JSON, który zawiera token dostępu (np. `"access_token": "<ACCESS_TOKEN>"`) oraz token odświeżania (np. `"refresh_token": "<REFRESH_TOKEN>"`). Aplikacja używa tokenu dostępu hello podczas uzyskiwania dostępu do usługi Azure Data Lake Store i tooget token odświeżania hello inny token dostępu po wygaśnięciu tokenu dostępu.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Po wygaśnięciu tokenu dostępu hello mogą żądać tokenu dostępu przy użyciu tokenu odświeżania hello, jak pokazano poniżej:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Więcej informacji na temat interakcyjnego uwierzytelniania użytkownika zawiera temat [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx) (Przepływ udzielania kodu autoryzacji).

### <a name="service-to-service-authentication-non-interactive"></a>Uwierzytelnianie między usługami (nieinterakcyjne)
W tym scenariuszu hello hello aplikacja udostępnia własne poświadczenia tooperform hello operacji. W tym celu należy wygenerować żądanie POST, takich jak hello przedstawionego poniżej. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

Witaj dane wyjściowe tego żądania będą zawierać token autoryzacji (wskazywane przez `access-token` w danych wyjściowych hello poniżej), który można następnie będzie przekazywany w wywołaniach interfejsu API REST. Zapisz ten token uwierzytelniania w pliku tekstowym. Będzie on potrzebny w dalszej części tego artykułu.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

W tym artykule wykorzystano hello **nieinterakcyjnym** podejście. Aby uzyskać więcej informacji na podejścia nieinterakcyjnego (wywołań service-to-service), zobacz [wywołania tooservice przy użyciu poświadczeń usługi](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-store-account"></a>Tworzenie konta usługi Data Lake Store
Ta operacja jest oparta na wywołania interfejsu API REST hello zdefiniowane [tutaj](https://msdn.microsoft.com/library/mt694078.aspx).

Użyj następującego polecenia cURL hello. Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

W hello powyżej polecenia, Zastąp \< `REDACTED` \> hello tokenem autoryzacji pobranym wcześniej. Witaj ładunku żądania dla tego polecenia jest zawarty w hello **input.json** pliku dostarczonego dla hello `-d` parametru powyżej. Witaj zawartość pliku input.json hello przypominać następujące hello:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Tworzenie folderów w ramach konta usługi Data Lake Store
Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).

Użyj następującego polecenia cURL hello. Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

W hello powyżej polecenia, Zastąp \< `REDACTED` \> hello tokenem autoryzacji pobranym wcześniej. To polecenie tworzy katalog o nazwie **mytempdir** w folderze głównym hello konta usługi Data Lake Store.

Powinny pojawić się odpowiedź podobna Jeśli hello operacja zakończy się pomyślnie:

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Wyświetlanie listy folderów w ramach konta usługi Data Lake Store
Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).

Użyj następującego polecenia cURL hello. Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

W hello powyżej polecenia, Zastąp \< `REDACTED` \> hello tokenem autoryzacji pobranym wcześniej.

Powinny pojawić się odpowiedź podobna Jeśli hello operacja zakończy się pomyślnie:

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a>Przekazywanie danych do konta usługi Data Lake Store
Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).

Użyj następującego polecenia cURL hello. Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

W hello powyżej składni **-T** parametr jest hello lokalizację pliku hello podczas przekazywania.

dane wyjściowe Hello są podobne toohello następujące czynności:
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Odczytywanie danych z konta usługi Data Lake Store
Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).

Odczytywanie danych z konta usługi Data Lake Store jest procesem dwuetapowym.

* Najpierw Prześlij żądanie GET względem punktu końcowego hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`. Spowoduje to przywrócenie lokalizacji toosubmit hello kolejne żądanie GET.
* Następnie przesłać hello żądanie GET względem punktu końcowego hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`. Spowoduje to wyświetlenie hello zawartość pliku hello.

Jednakże, ponieważ nie ma żadnej różnicy w hello parametrów wejściowych między hello najpierw i hello w drugim kroku, możesz użyć hello `-L` parametru toosubmit hello pierwszego żądania. `-L`Opcja zasadniczo łączy dwa żądania w jednym i spowoduje, że narzędzie cURL ponowi Żądanie hello na powitania nowej lokalizacji. Na koniec hello dane wyjściowe wszystkich wywołań żądań hello jest wyświetlana, tak samo, jak pokazano poniżej. Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

Powinny być widoczne następujące dane wyjściowe podobne toohello:

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Zmiana nazwy pliku w ramach konta usługi Data Lake Store
Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).

Użyj następujących hello cURL toorename polecenia pliku. Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

Powinny być widoczne następujące dane wyjściowe podobne toohello:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Usuwanie pliku z konta usługi Data Lake Store
Ta operacja jest oparta na wywołania interfejsu API REST WebHDFS hello zdefiniowane [tutaj](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).

Użyj następujących hello cURL toodelete polecenia pliku. Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Powinny pojawić się dane wyjściowe podobne do następujących hello:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Usuwanie konta usługi Data Lake Store
Ta operacja jest oparta na wywołania interfejsu API REST hello zdefiniowane [tutaj](https://msdn.microsoft.com/library/mt694075.aspx).

Użyj następujących hello cURL toodelete polecenia konto usługi Data Lake Store. Zastąp ciąg **\<yourstorename>** nazwą Twojej usługi Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Powinny pojawić się dane wyjściowe podobne do następujących hello:

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>Zobacz też
* [Open Source Big Data applications compatible with Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md) (Aplikacje danych big data typu open source zgodne z usługą Azure Data Lake Store)

