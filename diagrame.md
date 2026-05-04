# Diagrame Bază de Date - Sistem Management Clinică

Acest fișier conține diagrama conceptuală și diagrama entitate-relație (ER) pentru sistemul de management al clinicii medicale.

## 1. Diagrama Conceptuală
Această diagramă prezintă entitățile principale și relațiile logice dintre ele, fără a detalia atributele.

```mermaid
erDiagram
    SECTII ||--o{ CABINETE : "coordonează"
    SECTII ||--o{ MEDICI : "angajează"
    CABINETE ||--o{ MEDICI : "găzduiește"
    PERSOANE ||--|| MEDICI : "este (specializare)"
    PERSOANE ||--|| PACIENTI : "este (specializare)"
    ASIGURATORI ||--o{ PACIENTI : "asigură"
    PACIENTI ||--|| DOSARE_MEDICALE : "deține"
    MEDICI ||--o{ PROGRAMARI : "efectuează"
    PACIENTI ||--o{ PROGRAMARI : "participă"
    SERVICII_MEDICALE ||--o{ PROGRAMARI : "este prestat în"
    MEDICI ||--o{ RETETE : "eliberează"
    PACIENTI ||--o{ RETETE : "primește"
    RETETE }|--|{ MEDICAMENTE : "conține"
```

## 2. Diagrama Entitate-Relație (ER)
Această diagramă detaliază structura tabelelor, atributele, tipurile de date și constrângerile de integritate.

```mermaid
erDiagram
    SECTII {
        number ID_Sectie PK
        string Nume_Sectie
        number Etaj
    }

    CABINETE {
        number ID_Sectie PK, FK
        number Numar_Cabinet PK
        string Descriere
    }

    PERSOANE {
        string CNP PK
        string Nume
        string Prenume
        string Telefon
        date Data_Nasterii
    }

    MEDICI {
        string CNP PK, FK
        string Cod_Parafa UK
        string Specializare
        number ID_Sectie FK
        number Numar_Cabinet FK
    }

    PACIENTI {
        string CNP PK, FK
        string Grupa_Sanguina
        string Alergii
        number ID_Asigurator FK
    }

    ASIGURATORI {
        number ID_Asigurator PK
        string Nume_Companie
        string Telefon_Contact
    }

    DOSARE_MEDICALE {
        number ID_Dosar PK
        string CNP_Pacient UK, FK
        date Data_Deschidere
        string Istoric_General
    }

    SERVICII_MEDICALE {
        number ID_Serviciu PK
        string Denumire_Serviciu
        number Pret
        number Durata_Minute
    }

    PROGRAMARI {
        number ID_Programare PK
        string CNP_Medic FK
        string CNP_Pacient FK
        number ID_Serviciu FK
        timestamp Data_Ora
        string Status
    }

    RETETE {
        number ID_Reteta PK
        string CNP_Medic FK
        string CNP_Pacient FK
        date Data_Eliberare
        number Valabilitate_Zile
    }

    MEDICAMENTE {
        number ID_Medicament PK
        string Denumire
        string Substanta_Activa
        number Pret_Unitar
    }

    DETALII_RETETA {
        number ID_Reteta PK, FK
        number ID_Medicament PK, FK
        number Cantitate
        string Dozaj
    }

    SECTII ||--o{ CABINETE : "1:N"
    SECTII ||--o{ MEDICI : "1:N"
    CABINETE ||--o{ MEDICI : "1:N"
    PERSOANE ||--|| MEDICI : "IS-A"
    PERSOANE ||--|| PACIENTI : "IS-A"
    ASIGURATORI ||--o{ PACIENTI : "1:N"
    PACIENTI ||--|| DOSARE_MEDICALE : "1:1"
    MEDICI ||--o{ PROGRAMARI : "1:N"
    PACIENTI ||--o{ PROGRAMARI : "1:N"
    SERVICII_MEDICALE ||--o{ PROGRAMARI : "1:N"
    MEDICI ||--o{ RETETE : "1:N"
    PACIENTI ||--o{ RETETE : "1:N"
    RETETE ||--o{ DETALII_RETETA : "1:N"
    MEDICAMENTE ||--o{ DETALII_RETETA : "1:N"
```
