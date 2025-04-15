# SQL DML Projects

This project contains exercises and examples related to SQL DML (Data Manipulation Language) operations. It covers operations such as inserting, updating, deleting data, and creating functions and procedures.

## Content

### Database Operations:
1. **Inserting Data:**
    - `INSERT INTO tur (ad) VALUES ('Biyografi');`
    - `INSERT INTO yazar (ad, soyad) VALUES ('Nurettin', 'Belek');`
    - `INSERT INTO tur (ad) VALUES ('Kişisel Gelişim');`

2. **Updating Data:**
    - `UPDATE ogrenci SET sinif = '10C' WHERE sinif = '10B';`
    - `UPDATE kitap SET puan = puan + 5;`
    - `UPDATE kitap SET turno = (SELECT turno FROM tur WHERE ad = 'Kişisel Gelişim') WHERE ad = 'Benim Üniversitelerim';`

3. **Deleting Data:**
    - `DELETE FROM yazar WHERE ad = 'Mehmet';`

4. **Functions and Procedures:**
    - **ogrencilistesi()**: Function to return a list of students.
      CREATE OR REPLACE FUNCTION ogrencilistesi()
RETURNS TABLE(
    ogrno BIGINT, 
    ad CHARACTER VARYING(45), 
    soyad CHARACTER VARYING(45), 
    cinsiyet CHARACTER VARYING(1), 
    sinif CHARACTER VARYING(3), 
    puan INT, 
    dtarih CHARACTER VARYING(20)
)
AS
$$
BEGIN
    RETURN QUERY
    SELECT ogrenci.ogrno, ogrenci.ad, ogrenci.soyad, ogrenci.cinsiyet, ogrenci.sinif, ogrenci.puan, ogrenci.dtarih
    FROM ogrenci;
END;
$$ LANGUAGE plpgsql;


    - **ekle()**: Procedure to add a new book.
      CREATE OR REPLACE PROCEDURE ekle(
    p_ad CHARACTER VARYING(45),
    p_puan INTEGER,
    p_yazarno BIGINT,
    p_turno BIGINT
)
LANGUAGE plpgsql
AS
$$
BEGIN
    INSERT INTO public.kitap (ad, puan, yazarno, turno)
    VALUES (p_ad, p_puan, p_yazarno, p_turno);
END;
$$;
      
    - **sil()**: Procedure to delete a student.
      CREATE OR REPLACE PROCEDURE sil(
    p_ogrno BIGINT
)
LANGUAGE plpgsql
AS
$$
BEGIN
    DELETE FROM ogrenci
    WHERE ogrno = p_ogrno;
END;
$$;


## Usage

1. **Database operations** can be executed to perform insert, update, and delete actions on the relevant tables.
2. Functions and procedures can be used to execute more complex operations, such as using the `ogrencilistesi()` function to list all student data, or calling the `ekle()` and `sil()` procedures to manage records.

## Setup

After setting up the database connection, execute the SQL queries above to create the required tables, functions, and procedures.

