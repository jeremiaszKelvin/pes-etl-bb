# pes-etl-bb

'''Kod działa w następujący sposób:
1. Plik Full.ipynb
-Ma za zadanie scalić dwa półrocza plus kwartał + dwa miesiące z roku 2022
Powód: Większa kontrola nad scalaniem, trwa to szybciej niż scalanie wszyskich plików 

2. Ulice_automatycznie

2.1 Kod pobiera scalony dataset dla Bielska Białej, następnie na podstawie pliku "Liczniki.xlsx" czyta: identyfikatory, ulicę i numer, typ licznika. 
Dla ulicy robi scalanie na zasadzie "Adres"_"Numer" -> "MieszkaI_44". 

2.2. Następnie kod tworzy tensor nazw- każda ulica staje się od tej chwili nazwą zmiennej, która przechowuje dane dla konkretnej ulicy w skali roku. 
Działa to tak, że wyszukuje df[df['ID_nadrz']] == ID_konkretnego_obiektu. 
Np. df[df['ID_nadrz']] == 484500 Zwróci dataframe'a dla MieszkaI 2

for i in range(10):
    vars()[adresy[i].replace(" ","")] = df[df['ID_nadrz']==int(liczniki[i])]
    print(adresy[i])
    ulice_zmienne.append(vars()[adresy[i].replace(" ","")])
    
2.3. Następnie do utworzoneh ulicy kod przypisuje konkretny typ licznika np. Dla Mieszka I 2 jest to licznik CO- czyli zostaje utworzona dodatkowa kolumna
"LicznikTyp" ze stałą wartością np. "LicznikCO"

for i in range(len(ulice_zmienne)):
    ulice_zmienne[i]["LicznikTyp"] = typy[i]
    
2.4. Następnie i-ta ulica jest zapisywana do pliku CSV za pomocą pętli. Instrukcja range jest tutaj nieco prostacka- aby mieć adresy indeksowane od np. 10-20, to należy 
wszędzie w instrukcjach dołożyć range(10,20) , potem np pierwsze 250 ulic: range(250) etc.
Reasumując: program pobiera ulice_zmienne[i], zapisuje go do CSV na zasadzie: "zapisz o nazwie adres[i] dodaj i-ty typ licznika
iter na końcu to mój artefakt- do usunięcia

for i in range(10):
    ulice_zmienne[i].to_csv(adresy[i].replace(" ","")+'_'+typy[i].replace("Licznik ", "")+'_ITER'+'.csv',index=False)
