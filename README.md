# utl_how_many_words_contain_at_least_one_number
How many words contain at least one number. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    How many words contain at least one number

    Same result in SAS and WPS

    github
    https://github.com/rogerjdeangelis/utl_how_many_words_contain_at_least_one_number

    see SAS Forum
    https://tinyurl.com/y9n4p98l
    https://communities.sas.com/t5/General-SAS-Programming/Help-with-PERL-string-count-for-address-var/m-p/451890


    INPUT
    =====

     WORK.HAVE total obs=17
                                                                                  RULES
      Obs    LYN                                                        |
                                                                        |  Numer of words with a Number
        1    189 ELIOT STREET | UNIT 112 | ROCKLAND | ON | K4K0G4 | CAN |      3  189 112 4 (3 words)
        2    1769 101A AVE | SURREY | BC | V4N5V8 | CAN                 |      2  1769 458 (2 Words)
        3    1769 A101 AVE | SURREY | BC | V4N5V8 | CAN                 |      2
        4    204 ALGONQUIN RD UNIT114                                   |      1
        5    BUREAU N2P1G1                                              |      1
        6    29-549 RGE RD 232                                          |      1
        7    |||||                                                      |      0  None
        8    ||||                                                       |      0
        9    ||                                                         |      0
       10    |                                                          |      0
       11    1|2|3|4|5                                                  |      5
       12    1|2|3|4                                                    |      4
       13    1|2                                                        |      2
       14    1||22||                                                    |      2
       15    |1||22|                                                    |      2
       16    ||                                                         |      0
       17    |                                                          |      0


    PROCESS  (all the code)
    =======

        * keep only '|' and '1234567890';
        * change '|' to a space;
        * count the remaining blank separaed words;

        data want;
          retain words_with_numbers;
          set have;
          words_with_numbers = countw(translate(compress(lyn,'|1234567890',"K"),' ','|'));
        run;quit;


    OUTPUT
    ======

       WORK.WANT total obs=17

               WORDS_
               WITH_
       Obs    NUMBERS    LYN

         1       3       189 ELIOT STREET | UNIT 112 | ROCKLAND | ON | K4K0G4 | CAN
         2       2       1769 101A AVE | SURREY | BC | V4N5V8 | CAN
         3       2       1769 A101 AVE | SURREY | BC | V4N5V8 | CAN
         4       1       204 ALGONQUIN RD UNIT114
         5       1       BUREAU N2P1G1
         6       1       29-549 RGE RD 232
         7       0       |||||
         8       0       ||||
         9       0       ||
        10       0       |
        11       5       1|2|3|4|5
        12       4       1|2|3|4
        13       2       1|2
        14       2       1||22||
        15       2       |1||22|
        16       0       ||
        17       0       |

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;


    data have;
      informat lyn $72.;
      input lyn & $;
    cards4;
    189 ELIOT STREET | UNIT 112 | ROCKLAND | ON | K4K0G4 | CAN
    1769 101A AVE | SURREY | BC | V4N5V8 | CAN
    1769 A101 AVE | SURREY | BC | V4N5V8 | CAN
    204 ALGONQUIN RD UNIT114
    BUREAU N2P1G1  106
    29-549 RGE RD 232  STURGEON COUNTY  AB  T8L5E9  CAN
    |||||
    ||||
    ||
    |
    1|2|3|4|5
    1|2|3|4
    1|2
    1||22||
    |1||22|
    ||
    |
    ;;;;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    SAS

    data want;
      retain words_with_numbers;
      set have;
      words_with_numbers = countw(translate(compress(lyn,'|1234567890',"K"),' ','|'));
    run;quit;

    WPS

    %utl_submit_wps64('
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    data wrk.want;
      retain words_with_numbers;
      set wrk.have;
      words_with_numbers = countw(translate(compress(lyn,"|1234567890","K")," ","|"));
    run;quit;
    ');
