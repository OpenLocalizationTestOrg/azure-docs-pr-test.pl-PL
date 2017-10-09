Maszyna wirtualna platformy Azure obsługuje dołączanie wielu dysków danych. Aby uzyskać optymalną wydajność można toolimit hello liczba dysków wysokiej wykorzystywanych dołączony toohello maszyny wirtualnej tooavoid możliwości ograniczania. Jeśli wszystkie dyski są nie jest wysoce włączona na powitania tym samym czasie hello konta magazynu może obsługiwać większych dysków numer.

* **Na dyskach platformy Azure zarządzanego:** limit liczby dysków zarządzane ma charakteru regionalnego i zależy od typu magazynu hello. Hello domyślne, a także hello maksymalny limit jest 10 000 dla poszczególnych subskrypcji, na region i typ magazynu. Na przykład można utworzyć zapasowej too10, 000 standard zarządzane dysków, a także 10 000 premium zarządzane dyski w subskrypcji i regionu. 

    Zarządzane migawki i obrazy są uwzględniane powitalne ograniczyć dysków zarządzanych.

* **Konto magazynu w warstwie Standardowa:** maksymalna całkowita liczba żądań dla konta magazynu w warstwie Standardowa to 20 000 operacji wejścia/wyjścia na sekundę (IOPS). Witaj całkowita IOPS wszystkich dysków maszyny wirtualnej w ramach konta magazynu w warstwie standardowa nie może przekraczać ten limit.
  
    Numer hello wysokiej wykorzystywanych dysków obsługiwanych przez jeden standard konta magazynu, oparte na limit szybkości żądania hello około można obliczyć. Na przykład do warstwy podstawowa maszyna wirtualna, hello maksymalną liczbę wysokiej użycia dysków jest około 66 (20 000/300 IOPS dla każdego dysku), oraz standardowe warstwy maszyny wirtualnej, jest około 40 (20 000/500 IOPS dla każdego dysku), jak pokazano w poniższej tabeli hello. 
* **Konta magazynu w warstwie Premium:** maksymalna całkowita przepływność konta magazynu w warstwie Premium to 50 Gb/s. Witaj ogólnej przepustowości we wszystkich dysków maszyny Wirtualnej nie może przekraczać ten limit.

