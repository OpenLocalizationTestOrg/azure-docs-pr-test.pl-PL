---
title: "Samouczek dotyczący aplikacji internetowej platformy Python Flask dla usługi Azure Cosmos DB | Microsoft Docs"
description: "Przejrzyj samouczek bazy danych na temat korzystania z usługi Azure Cosmos DB w celu przechowywania i uzyskiwania dostępu do danych z aplikacji internetowej platformy Python Flask hostowanej na platformie Azure. Znajdź rozwiązania do tworzenia aplikacji."
keywords: Application development, python flask, python web application, python web development
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed5284b5a265840c43dbc9890082a7c038d22975
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Tworzenie aplikacji internetowej platformy Python Flask za pomocą usługi Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Ten samouczek pokazuje, jak używać usługi Azure Cosmos DB do przechowywania i uzyskiwania dostępu do danych aplikacji internetowej utworzonej w języku Python i hostowanej na platformie Azure. Przyjęto w nim założenie, że użytkownik posiada już pewne doświadczenie związane z używaniem języka Python i witryn internetowych platformy Azure.

Ten samouczek bazy danych obejmuje następujące zagadnienia:

1. Tworzenie i Inicjowanie obsługi konta DB rozwiązania Cosmos.
2. Tworzenie aplikacji platformy Python Flask.
3. Nawiązywanie połączenia z usługą Azure Cosmos DB i korzystanie z niej z poziomu aplikacji internetowej.
4. Wdrażanie aplikacji sieci web na platformie Azure.

Wykonując poszczególne kroki tego samouczka, utworzysz prostą aplikację do głosowania, która umożliwia głosowanie w ankiecie.

![Zrzut ekranu przedstawiający aplikację do głosowania utworzone przez tego samouczka bazy danych](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Wymagania wstępne dotyczące samouczka
Przed wykonaniem instrukcji zawartych w tym artykule upewnij się, że masz następujące elementy:

* Aktywne konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
 
    LUB 

    Lokalna instalacja [emulatora usługi Azure Cosmos DB](local-emulator.md).
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).  
* [Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).  
* [Zestaw Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/). 
* [Python 2.7.13](https://www.python.org/downloads/windows/). 

> [!IMPORTANT]
> Jeśli instalujesz środowisko Python 2.7 po raz pierwszy, upewnij się, na ekranie dostosować Python 2.7.13 wybranym **Dodaj python.exe do ścieżki**.
> 
> ![Zrzut ekranu Customize Python 2.7.11 (Dostosowywanie środowiska Python 2.7.11), na którym należy wybrać pozycję Add python.exe to Path (Dodaj plik python.exe do ścieżki)](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>Krok 1. Tworzenie konta bazy danych usługi Azure Cosmos DB
Zacznijmy od utworzenia konta usługi Cosmos DB. Jeśli masz już konto lub jeśli korzystasz z emulatora usługi Azure Cosmos DB na potrzeby tego samouczka, możesz od razu przejść do sekcji [Krok 2. Tworzenie nowej aplikacji internetowej platformy Python Flask](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
Teraz przejdziemy przez proces tworzenia nowej aplikacji sieci Web platformy Python Flask od podstaw.

## <a name="step-2-create-a-new-python-flask-web-application"></a>Krok 2. Tworzenie nowej aplikacji sieci Web platformy Python Flask
1. W menu **Plik** programu Visual Studio wskaż pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.
   
    Zostanie wyświetlone okno dialogowe **Nowy projekt**.
2. W lewym okienku rozwiń pozycję **Szablony** i **Python**, a następnie kliknij pozycję **Sieć Web**. 
3. W środkowym okienku wybierz pozycję **Projekt sieci Web platformy Flask**, a następnie w polu **Nazwa** wpisz wartość **tutorial** i kliknij przycisk **OK**. Pamiętaj, że wszystkie nazwy pakietów języka Python powinny być pisane małymi literami, zgodnie z opisem zawartym w publikacji [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names) (Przewodnik po stylu kodu Python).
   
    Python Flask to platforma programistyczna aplikacji sieci Web, która umożliwia szybsze tworzenie aplikacji sieci Web w języku Python.
   
    ![Zrzut ekranu okna Nowy projekt w programie Visual Studio z wyróżnioną po lewej stronie pozycją Python, zaznaczoną w środkowej części pozycją Projekt sieci Web platformy Python Flask oraz nazwą tutorial w polu Nazwa](./media/documentdb-python-application/image9.png)
4. W oknie **Python Tools for Visual Studio** kliknij pozycję **Zainstaluj w środowisku wirtualnym**. 
   
    ![Zrzut ekranu samouczka bazy danych — okno Python Tools for Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. W oknie **Dodawanie środowiska wirtualnego** możesz zaakceptować wartości domyślne i użyć środowiska Python 2.7 jako podstawowego środowiska, ponieważ pakiet PyDocumentDB nie obsługuje obecnie środowiska Python 3.x, a następnie kliknij przycisk **Utwórz**. Spowoduje to skonfigurowanie wymaganego środowiska wirtualnego Python dla Twojego projektu.
   
    ![Zrzut ekranu samouczka bazy danych — okno Python Tools for Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    Po pomyślnym zainstalowaniu środowiska w oknie Dane wyjściowe zostanie wyświetlona informacja `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.`.

## <a name="step-3-modify-the-python-flask-web-application"></a>Krok 3. Modyfikowanie aplikacji sieci Web platformy Python Flask
### <a name="add-the-python-flask-packages-to-your-project"></a>Dodawanie pakietów platformy Python Flask do projektu
Po skonfigurowaniu projektu musisz dodać do niego wymagane pakiety platformy Flask, w tym pydocumentdb — pakiet języka Python dla usługi DocumentDB.

1. W Eksploratorze rozwiązań otwórz plik o nazwie **requirements.txt** i zastąp jego zawartość następującym kodem:
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. Zapisz plik **requirements.txt**. 
3. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy pozycję **env**, a następnie kliknij polecenie **Zainstaluj z pliku requirements.txt**.
   
    ![Zrzut ekranu przedstawiający wybraną pozycję env (Python 2.7) oraz polecenie Zainstaluj z pliku requirements.txt wyróżnione na liście](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    Po pomyślnej instalacji w oknie Dane wyjściowe zostaną wyświetlone następujące informacje:
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > W rzadkich przypadkach w oknie Dane wyjściowe może zostać wyświetlony błąd. Jeśli tak się stanie, sprawdź, czy błąd jest związany z oczyszczaniem. Czasami oczyszczanie nie powiedzie się, ale instalacja i tak zakończy się pomyślnie (aby to sprawdzić, przewiń w górę w oknie Dane wyjściowe). Instalację można sprawdzić przez [zweryfikowanie środowiska wirtualnego](#verify-the-virtual-environment). Jeśli instalacja nie powiodła się, ale weryfikacja zakończyła się pomyślnie, można kontynuować.
   > 
   > 

### <a name="verify-the-virtual-environment"></a>Weryfikowanie środowiska wirtualnego
Upewnijmy się, że wszystko jest poprawnie zainstalowane.

1. Skompiluj rozwiązanie, naciskając klawisze **Ctrl**+**Shift**+**B**.
2. Gdy kompilacja zakończy się powodzeniem, uruchom witrynę sieci Web, naciskając klawisz **F5**. Powoduje to uruchomienie serwera programistycznego platformy Flask i przeglądarki sieci Web. Powinna zostać wyświetlona następująca strona.
   
    ![Pusty projekt aplikacji sieci Web platformy Python Flask wyświetlony w przeglądarce](./media/documentdb-python-application/image12.png)
3. Zatrzymaj debugowanie witryny sieci Web, naciskając klawisze **Shift**+**F5** w programie Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Tworzenie definicji bazy danych, kolekcji i dokumentu
Teraz utwórzmy aplikację do głosowania przez dodanie nowych plików i zaktualizowanie pozostałych.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **tutorial**, kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Nowy element**. Wybierz pozycję **Pusty plik Python** i nazwij ten plik **forms.py**.  
2. Dodaj następujący kod do pliku forms.py, a następnie zapisz plik.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a>Dodawanie wymaganych importów do pliku views.py
1. W Eksploratorze rozwiązań rozwiń folder **tutorial**, a następnie otwórz plik **views.py**. 
2. Dodaj następujące instrukcje importu u góry pliku **views.py**, a następnie zapisz plik. Spowoduje to zaimportowanie zestawu SDK Python usługi Cosmos DB oraz pakietów platformy Flask.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>Tworzenie bazy danych, kolekcji i dokumentu
* Dodaj następujący kod na końcu pliku **views.py**. Odpowiada on za tworzenie bazy danych używanej przez formularz. Nie usuwaj żadnego kodu znajdującego się w pliku **views.py**. Po prostu dołącz podany kod na końcu.

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a>Odczytywanie bazy danych, kolekcji i dokumentów oraz przesyłanie formularza
* Dodaj następujący kod na końcu pliku **views.py**. Odpowiada on za konfigurowanie formularza oraz odczytywanie bazy danych, kolekcji i dokumentu. Nie usuwaj żadnego kodu znajdującego się w pliku **views.py**. Po prostu dołącz podany kod na końcu.

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-the-html-files"></a>Tworzenie plików HTML
1. W Eksploratorze rozwiązań, w folderze **tutorial** kliknij prawym przyciskiem myszy folder **templates**, potem polecenie **Dodaj**, a następnie kliknij pozycję **Nowy element**. 
2. Wybierz pozycję **Strona HTML**, a następnie w polu nazwy wpisz **create.html**. 
3. Powtórz kroki 1 i 2, aby utworzyć dwa dodatkowe pliki HTML: results.html i vote.html.
4. Dodaj następujący kod do pliku **create.html** w elemencie `<body>`. Służy do wyświetlania komunikatu informującego o tym, że utworzyliśmy nową bazę danych, kolekcję i dokument.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Dodaj następujący kod do pliku **results.html** w elemencie `<body`>. Służy do wyświetlania wyników ankiety.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. Dodaj następujący kod do pliku **vote.html** w elemencie `<body`>. Służy do wyświetlania ankiety i akceptowania oddanych głosów. Po zarejestrowaniu głosów kontrola jest przekazywana do pliku views.py, gdzie oddany głos jest rozpoznawany i odpowiednie dane są dołączane do dokumentu.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. W folderze **templates** zastąp zawartość pliku **index.html** poniższym kodem. Będzie to strona docelowa dla Twojej aplikacji.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a>Dodawanie pliku konfiguracji i zmienianie pliku \_\_init\_\_.py
1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **tutorial**, kliknij polecenie **Dodaj**, potem pozycję **Nowy element**, następnie wybierz opcję **Pusty plik Python**, a na końcu podaj nazwę pliku, **config.py**. Ten plik konfiguracji jest wymagany przez formularze na platformie Flask. Można go również użyć, aby dostarczyć klucz tajny. Ten klucz nie jest jednak potrzebny w tym samouczku.
2. Dodaj poniższy kod do pliku config.py. Konieczna będzie zmiana wartości **DOCUMENTDB\_HOST** i **DOCUMENTDB\_KEY** w następnym kroku.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. W witrynie [Azure Portal](https://portal.azure.com/) przejdź do bloku **Klucze**, klikając pozycję **Przeglądaj**, **Konta usługi Azure Cosmos DB**, kliknij dwukrotnie nazwę konta, którego chcesz użyć, a następnie kliknij przycisk **Klucze** w obszarze **Podstawy**. W bloku **Klucze** skopiuj wartość **URI** i wklej ją do pliku **config.py** jako wartość właściwości **DOCUMENTDB\_HOST**. 
4. W witrynie Azure Portal, w bloku **Klucze** skopiuj wartość **Klucz podstawowy** lub **Klucz pomocniczy** i wklej ją do pliku **config.py** jako wartość właściwości **DOCUMENTDB\_KEY**.
5. W pliku **\_\_init\_\_.py** dodaj następujący wiersz. 
   
        app.config.from_object('config')
   
    Plik powinien mieć następującą zawartość:
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. Po dodaniu wszystkich plików Eksplorator rozwiązań powinien wyglądać następująco:
   
    ![Zrzut ekranu okna Eksploratora rozwiązań programu Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>Krok 4. Uruchamianie aplikacji sieci Web lokalnie
1. Skompiluj rozwiązanie, naciskając klawisze **Ctrl**+**Shift**+**B**.
2. Gdy kompilacja zakończy się powodzeniem, uruchom witrynę sieci Web, naciskając klawisz **F5**. Na ekranie powinna być widoczna następująca strona.
   
    ![Zrzut ekranu aplikacji do głosowania opartej na języku Python i usłudze Azure Cosmos DB wyświetlonej w przeglądarce internetowej](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Kliknij przycisk **Create/Clear the Voting Database** (Utwórz/wyczyść bazę danych głosowania), aby wygenerować bazę danych.
   
    ![Zrzut ekranu strony tworzenia w aplikacji sieci Web — szczegóły programowania](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. Następnie kliknij przycisk **Vote** (Głosuj) i wybierz jedną z opcji.
   
    ![Zrzut ekranu aplikacji sieci Web z pytaniem, na które należy udzielić odpowiedzi](./media/documentdb-python-application/cosmos-db-vote.png)
5. Każdy oddany głos powoduje zwiększenie odpowiedniego licznika.
   
    ![Zrzut ekranu strony Results of the vote (Wyniki głosowania)](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Zatrzymaj debugowanie projektu przez naciśnięcie klawiszy Shift+F5.

## <a name="step-5-deploy-the-web-application-to-azure"></a>Krok 5: Wdrażanie aplikacji sieci web na platformie Azure
Teraz, gdy kompletna aplikacja działa poprawnie z rozwiązania Cosmos DB, chcemy to wdrażanie na platformie Azure.

1. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań (upewnij się, że nie jest uruchomiony lokalnie) i wybierz polecenie **Publikuj**.  
   
     ![Zrzut ekranu przedstawiający pozycję tutorial wybraną w Eksploratorze rozwiązań oraz wyróżnione polecenie Publikuj](./media/documentdb-python-application/image20.png)
2. W **publikowania** okno dialogowe, wybierz opcję **Microsoft Azure App Service**, wybierz pozycję **Utwórz nowy**, a następnie kliknij przycisk **publikowania**.
   
    ![Zrzut ekranu okna publikowanie w sieci Web wyróżnione program Microsoft Azure App Service](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. W **Tworzenie usługi App Service** okna dialogowego wprowadź nazwę dla aplikacji sieci web, wraz z Twojej **subskrypcji**, **grupy zasobów**, i **planu usługi App Service**, następnie kliknij przycisk **Utwórz**.
   
    ![Zrzut ekranu okna Microsoft Azure Web Apps](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. W ciągu kilku sekund program Visual Studio zakończy publikowanie aplikacji usługi i uruchomi przeglądarkę, w którym można zobaczyć Twojej handiwork działające na platformie Azure!

    ![Zrzut ekranu okna Microsoft Azure Web Apps](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli jest to pierwsza aplikacja napisana w języku Python uruchomiona na Twoim komputerze, upewnij się, że następujące foldery (lub odpowiadające im lokalizacje instalacji) są uwzględnione w zmiennej PATH:

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Jeśli wystąpi błąd na stronie głosowania, a nazwa projektu jest inna niż **tutorial**, upewnij się, że plik **\_\_init\_\_.py** odwołuje się do właściwej nazwy projektu w wierszu: `import tutorial.view`.

## <a name="next-steps"></a>Następne kroki
Gratulacje! Po prostu ma wykonać swoją pierwszą aplikację sieci web języka Python za pomocą rozwiązania Cosmos bazy danych i opublikować ją w usłudze Azure.

Często aktualizujemy i poprawiamy ten temat na podstawie opinii czytelników.  Po ukończeniu samouczka użyj przycisków głosowania znajdujących się u góry i u dołu tej strony oraz napisz swoją opinię na temat tego, co możemy ulepszyć. Jeśli chcesz, abyśmy skontaktowali się z Tobą bezpośrednio, możesz w komentarzach podać swój adres e-mail.

Aby dodać dodatkowe funkcje do aplikacji sieci web, zapoznaj się z interfejsami API dostępnymi w [Azure rozwiązania Cosmos DB Python SDK](documentdb-sdk-python.md).

Aby uzyskać więcej informacji na temat platformy Azure, programu Visual Studio i języka Python, zobacz [Centrum deweloperów języka Python](https://azure.microsoft.com/develop/python/). 

Dodatkowe samouczki dotyczące platformy Python Flask znajdziesz na stronie [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world) (Megasamouczek platformy Flask, część I: Witaj, świecie!). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
