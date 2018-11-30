# utl-do-not-add-data-transformations-to-create-csv-files-from-excel-or-any-other-data-structure
Do not add data transformations to create csv files from excel or any other data structure
    Do not add data transformations to create csv files from excel or any other data structure

    The more transformation you do the more unlikely the data will true.
    If you do need to do some transformation do them using passthru with native languages.

    In the case of imbedeed control characters a csv often becomes indeterminate.

    github
    https://tinyurl.com/yb9u7odt
    https://github.com/rogerjdeangelis/utl-do-not-add-data-transformations-to-create-csv-files-from-excel-or-any-other-data-structure

    https://tinyurl.com/y9advbb6
    https://communities.sas.com/t5/SAS-Programming/Illegible-freq-values-when-reading-CVS-excel-file-with-narrative/m-p/516031



    INPUT  ('0A'x is alt enter. Other control chars possible ie '09'x(TAB,QUOTES)
    =====

     d:/xls/noXpo.xlsx

       +----------------------------------------------------------------------+
       |     A               |    B    |     C      |    D       |    E       |
       +----------------------------------------------------------------------+
    1  |   NAME              |   SEX   |    AGE     |  HEIGHT    |  WEIGHT    |
       +---------------------+---------+------------+------------+------------+
    2  |  Alfred0A'xSMITH    |    M    |    14      |    69      |  112.5     |
       +---------------------+---------+------------+------------+------------+
        ...
       +---------------------+---------+------------+------------+------------+
    19 |  WILLIAM'0A'xSMITH  |    M    |    15      |   66.5     |  112       |
       +---------------------+---------+------------+------------+------------+

     [HAVE]



    EXAMPLE OUTPUT
    --------------


            ** NOTE THE '0A' BETWEEN **

    NAME                NAME                 SEX        AGE     HEIGHT     WEIGHT

    Alfred  416C66726564 0A 534D49544820       M         14         69      112.5
    SMITH

    Alice   416C696365 0A 534D4954482020       F         13       56.5         84
    SMITH

    Barbara 42617262617261 0A 534D495448       F         13       65.3         98
    SMITH

    Carol   4361726F6C 0A 534D4954482020       F         14       62.8      102.5
    SMITH
    Henry   48656E7279 0A 534D4954482020       M         14       63.5      102.5

    OUTPUT
    ======

    see above

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;


    %utlfkil(d:/xls/noXpo.xlsx);
    libname xel "d:/xls/noXpo.xlsx";
    data xel.have;
      length name $32;
      set sashelp.class(obs=5);
      name=cats(name,'0A'x,'SMITH');
    run;quit;
    libname xel clear;

