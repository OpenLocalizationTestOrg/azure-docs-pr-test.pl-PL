
## <a name="size-table-definitions"></a>Definicje tabel rozmiaru

- Pojemność magazynu jest podawana w jednostkach GiB (1024^3 bajtów). Gdy porównanie dysków mierzony w GB (1000 ^ 3 bajtów) toodisks mierzony w GiB (1024 ^ 3) należy pamiętać, że liczby pojemności podane w GiB może pojawić się mniejszą. Na przykład 1023 GiB = 1098,4 GB.
- Przepływność dysku mierzona jest jako liczba operacji wejścia/wyjścia na sekundę i MB/s, gdzie 1 MB/s = 10^6 bajtów/s.
- Dyski danych mogą działać w trybie buforowanym lub niebuforowanym. Dla operacji dysku danych z pamięci podręcznej, tryb buforowania hosta hello ustawiono zbyt**tylko do odczytu** lub **ReadWrite**.  Dla operacji dysku bez buforowania danych, hello hosta pamięci podręcznej jest tryb zbyt**Brak**.
- **Oczekiwano wydajność sieci** hello maksymalna przepustowość zagregowane zaalokowany typu maszyny Wirtualnej dla wszystkich kart dla wszystkich miejsc docelowych. Górne limity nie ma gwarancji, ale są zamierzone tooprovide wskazówki dotyczące wybranie hello odpowiedniego typu maszyny Wirtualnej dla aplikacji hello przeznaczone. Rzeczywista wydajność sieci będzie zależeć od wielu czynników, takich jak przeciążenie sieci, obciążenie aplikacji oraz ustawienia sieci. Aby uzyskać informacje na temat optymalizowania przepływności sieci, zobacz [Optimizing network throughput for Windows and Linux (Optymalizowanie przepływności sieci dla systemów Windows i Linux)](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md). Witaj tooachieve oczekiwano wydajność sieci w systemie Linux lub Windows, może być konieczne tooselect określonej wersji lub zoptymalizować maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [jak tooreliably testu dla maszyny wirtualnej przepływności](../articles/virtual-network/virtual-network-bandwidth-testing.md).

- &#8224; 16 vCPU wydajności spójnie osiągną hello górnego limitu w nową wersją.


